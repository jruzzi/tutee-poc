[Go to primary content](#BEGIN)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Java Platform, Enterprise Edition The Java EE Tutorial</strong><br />
<strong>Release 7 Java Platform, Enterprise Edition</strong><br />
E39031-02</td>
<td><table>
<tbody>
<tr class="odd">
<td> </td>
<td><a href="toc.htm"><img src="../../dcommon/gifs/toc.gif" alt="Go To Table Of Contents" /><br />
<span class="icon">Contents</span></a></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

-----

<table>
<tbody>
<tr class="odd">
<td><a href="servlets016.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets018.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.17 The dukeetf Example Application

The `dukeetf` example application, located in the
tut-install`/examples/web/dukeetf/` directory, demonstrates how to use
asynchronous processing in a servlet to provide data updates to web
clients. The example resembles a service that provides periodic updates
on the price and trading volume of an electronically traded fund (ETF).

The following topics are addressed here:

  - [Section 17.17.1, "Architecture of the dukeetf Example
    Application"](#CHDBBEDA)

  - [Section 17.17.2, "Running the dukeetf Example
    Application"](#CHDHBBBI)

## 17.17.1 Architecture of the dukeetf Example Application

The `dukeetf` example application consists of a servlet, an enterprise
bean, and an HTML page.

  - The servlet puts requests in asynchronous mode, stores them in a
    queue, and writes the responses when new data for price and trading
    volume becomes available.

  - The enterprise bean updates the price and volume information once
    every second.

  - The HTML page uses JavaScript code to make requests to the servlet
    for new data, parse the response from the servlet, and update the
    price and volume information without reloading the page.

The `dukeetf` example application uses a programming model known as long
polling. In the traditional HTTP request and response model, the user
must make an explicit request (such as clicking a link or submitting a
form) to get any new information from the server, and the page has to be
reloaded. Long polling provides a mechanism for web applications to push
updates to clients using HTTP without the user making an explicit
request. The server handles connections asynchronously, and the client
uses JavaScript to make new connections. In this model, clients make a
new request immediately after receiving new data, and the server keeps
the connection open until new data becomes available.

### 17.17.1.1 The Servlet

The `DukeETFServlet` class uses asynchronous processing:

``` oac_no_warn
@WebServlet(urlPatterns={"/dukeetf"}, asyncSupported=true)
public class DukeETFServlet extends HttpServlet {
...
}
```

In the following code, the `init` method initializes a queue to hold
client requests and registers the servlet with the enterprise bean that
provides the price and volume updates. The `send` method gets called
once per second by the `PriceVolumeBean` to send updates and close the
connection:

``` oac_no_warn
@Override
public void init(ServletConfig config) {
   /* Queue for requests */
   requestQueue = new ConcurrentLinkedQueue<>();
   /* Register with the enterprise bean that provides price/volume updates */
   pvbean.registerServlet(this);
}

/* PriceVolumeBean calls this method every second to send updates */
public void send(double price, int volume) {
   /* Send update to all connected clients */
   for (AsyncContext acontext : requestQueue) {
      try {
         String msg = String.format("%.2f / %d", price, volume);
         PrintWriter writer = acontext.getResponse().getWriter();
         writer.write(msg);
         logger.log(Level.INFO, "Sent: {0}", msg);
         /* Close the connection
          * The client (JavaScript) makes a new one instantly */
         acontext.complete();
      } catch (IOException ex) {
         logger.log(Level.INFO, ex.toString());
      }
   }
}
```

The service method puts client requests in asynchronous mode and adds a
listener to each request. The listener is implemented as an anonymous
class that removes the request from the queue when the servlet finishes
writing a response or when there is an error. Finally, the service
method adds the request to the request queue created in the `init`
method. The service method is the following:

``` oac_no_warn
@Override
public void doGet(HttpServletRequest request, 
                  HttpServletResponse response) {
   response.setContentType("text/html");
   /* Put request in async mode */
   final AsyncContext acontext = request.startAsync();
   /* Remove from the queue when done */
   acontext.addListener(new AsyncListener() {
      public void onComplete(AsyncEvent ae) throws IOException {
         requestQueue.remove(acontext);
      }
      public void onTimeout(AsyncEvent ae) throws IOException {
         requestQueue.remove(acontext);
      }
      public void onError(AsyncEvent ae) throws IOException {
         requestQueue.remove(acontext);
      }
      public void onStartAsync(AsyncEvent ae) throws IOException {}
   });
   /* Add to the queue */
   requestQueue.add(acontext);
}
```

### 17.17.1.2 The Enterprise Bean

The `PriceVolumeBean` class is an enterprise bean that uses the timer
service from the container to update the price and volume information
and call the servlet's `send` method once every second:

``` oac_no_warn
@Startup
@Singleton
public class PriceVolumeBean {
    /* Use the container's timer service */
    @Resource TimerService tservice;
    private DukeETFServlet servlet;
    ...
    
    @PostConstruct
    public void init() {
        /* Initialize the EJB and create a timer */
        random = new Random();
        servlet = null;
        tservice.createIntervalTimer(1000, 1000, new TimerConfig());
    }
    
    public void registerServlet(DukeETFServlet servlet) {
        /* Associate a servlet to send updates to */
        this.servlet = servlet;
    }
    
    @Timeout
    public void timeout() {
        /* Adjust price and volume and send updates */
        price += 1.0*(random.nextInt(100)-50)/100.0;
        volume += random.nextInt(5000) - 2500;
        if (servlet != null)
            servlet.send(price, volume);
    }
}
```

See [Using the Timer Service](ejb-basicexamples005.htm#BNBOY) in
[Chapter 34, "Running the Enterprise Bean
Examples"](ejb-basicexamples.htm#GIJRB) for more information on the
timer service.

### 17.17.1.3 The HTML Page

The HTML page consists of a table and some JavaScript code. The table
contains two fields referenced from JavaScript code:

``` oac_no_warn
<html xmlns="http://www.w3.org/1999/xhtml">
<head>...</head>
<body onload="makeAjaxRequest();">
  ...
  <table>
    ...
    <td id="price">--.--</td>
    ...
    <td id="volume">--</td>
    ...
  </table>
</body>
</html>
```

The JavaScript code uses the `XMLHttpRequest` API, which provides
functionality for transferring data between a client and a server. The
script makes an asynchronous request to the servlet and designates a
callback method. When the server provides a response, the callback
method updates the fields in the table and makes a new request. The
JavaScript code is the following:

``` oac_no_warn
var ajaxRequest;
function updatePage() {
   if (ajaxRequest.readyState === 4) {
      var arraypv = ajaxRequest.responseText.split("/");
      document.getElementById("price").innerHTML = arraypv[0];
      document.getElementById("volume").innerHTML = arraypv[1];
      makeAjaxRequest();
   }
}
function makeAjaxRequest() {
   ajaxRequest = new XMLHttpRequest();
   ajaxRequest.onreadystatechange = updatePage;
   ajaxRequest.open("GET", "http://localhost:8080/dukeetf/dukeetf", 
                    true);
   ajaxRequest.send(null);
}
```

The `XMLHttpRequest` API is supported by most modern browsers, and it is
widely used in Ajax web client development (Asynchronous JavaScript and
XML).

See [The dukeetf2 Example Application](websocket011.htm#BABGCEHE) in
[Chapter 18, "Java API for WebSocket"](websocket.htm#GKJIQ5) for an
equivalent version of this example implemented using a WebSocket
endpoint.

## 17.17.2 Running the dukeetf Example Application

This section describes how to run the `dukeetf` example application
using NetBeans IDE and from the command line.

The following topics are addressed here:

  - [Section 17.17.2.1, "To Run the dukeetf Example Application Using
    NetBeans IDE"](#CHDCGCJD)

  - [Section 17.17.2.2, "To Run the dukeetf Example Application Using
    Maven"](#CHDHHAFG)

### 17.17.2.1 To Run the dukeetf Example Application Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/servlet
    ```

4.  Select the `dukeetf` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `dukeetf` project and select
    Run.
    
    This command builds and packages the application into a WAR file
    (`dukeetf.war`) located in the `target` directory, deploys it to the
    server, and launches a web browser window with the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/dukeetf/
    ```
    
    Open the same URL in a different web browser to see how both pages
    get price and volume updates simultaneously.

### 17.17.2.2 To Run the dukeetf Example Application Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/servlet/dukeetf/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```

4.  Open a web browser window and type the following address:
    
    ``` oac_no_warn
    http://localhost:8080/dukeetf/
    ```
    
    Open the same URL in a different web browser to see how both pages
    get price and volume updates simultaneously.

-----

<table style="width:66%;">
<colgroup>
<col width="33%" />
<col width="0%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><table style="width:96%;">
<colgroup>
<col width="0%" />
<col width="48%" />
<col width="48%" />
</colgroup>
<tbody>
<tr class="odd">
<td> </td>
<td><a href="servlets016.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets018.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
</tr>
</tbody>
</table></td>
<td><img src="../../dcommon/gifs/oracle.gif" alt="Oracle Logo" class="copyrightlogo" /> <a href="../../dcommon/html/cpyr.htm"><br />
<span class="copyrightlogo">Copyright © 2014, Oracle and/or its affiliates. All rights reserved.</span></a></td>
<td><table>
<tbody>
<tr class="odd">
<td> </td>
<td><a href="toc.htm"><img src="../../dcommon/gifs/toc.gif" alt="Go To Table Of Contents" /><br />
<span class="icon">Contents</span></a></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

ORACLE CONFIDENTIAL. For authorized use only. Do not distribute to third parties.
