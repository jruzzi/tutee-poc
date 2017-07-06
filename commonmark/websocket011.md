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
<td><a href="websocket010.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket012.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 18.11 The dukeetf2 Example Application

The `dukeetf2` example application, located in the
tut-install`/examples/web/websocket/dukeetf2/` directory, demonstrates
how to use a WebSocket endpoint to provide data updates to web clients.
The example resembles a service that provides periodic updates on the
price and trading volume of an electronically traded fund (ETF).

The following topics are addressed here:

  - [Section 18.11.1, "Architecture of the dukeetf2 Sample
    Application"](#CIHJHJCD)

  - [Section 18.11.2, "Running the dukeetf2 Example
    Application"](#CIHHBAIC)

## 18.11.1 Architecture of the dukeetf2 Sample Application

The `dukeetf2` example application consists of a WebSocket endpoint, an
enterprise bean, and an HTML page.

  - The endpoint accepts connections from clients and sends them updates
    when new data for price and trading volume becomes available.

  - The enterprise bean updates the price and volume information once
    every second.

  - The HTML page uses JavaScript code to connect to the WebSocket
    endpoint, parse incoming messages, and update the price and volume
    information without reloading the page.

### 18.11.1.1 The Endpoint

The WebSocket endpoint is implemented in the `ETFEndpoint` class, which
stores all connected sessions in a queue and provides a method that the
enterprise bean calls when there is new information available to send:

``` oac_no_warn
@ServerEndpoint("/dukeetf")
public class ETFEndpoint {
   private static final Logger logger = Logger.getLogger("ETFEndpoint");
   /* Queue for all open WebSocket sessions */
   static Queue<Session> queue = new ConcurrentLinkedQueue<>();

   /* PriceVolumeBean calls this method to send updates */
   public static void send(double price, int volume) {
      String msg = String.format("%.2f / %d", price, volume);
      try {
         /* Send updates to all open WebSocket sessions */
         for (Session session : queue) {
            session.getBasicRemote().sendText(msg);
            logger.log(Level.INFO, "Sent: {0}", msg);
         }
      } catch (IOException e) {
         logger.log(Level.INFO, e.toString());
      }
    }
    ...
}
```

The lifecycle methods of the endpoint add and remove sessions to and
from the queue:

``` oac_no_warn
@ServerEndpoint("/dukeetf")
public class ETFEndpoint {
   ...
   @OnOpen
   public void openConnection(Session session) {
      /* Register this connection in the queue */
      queue.add(session);
      logger.log(Level.INFO, "Connection opened.");
   }

   @OnClose
   public void closedConnection(Session session) {
      /* Remove this connection from the queue */
      queue.remove(session);
      logger.log(Level.INFO, "Connection closed.");
   }

   @OnError
   public void error(Session session, Throwable t) {
      /* Remove this connection from the queue */
      queue.remove(session);
      logger.log(Level.INFO, t.toString());
      logger.log(Level.INFO, "Connection error.");
   }
}
```

### 18.11.1.2 The Enterprise Bean

The enterprise bean uses the timer service to generate new price and
volume information every second:

``` oac_no_warn
@Startup
@Singleton
public class PriceVolumeBean {
   /* Use the container's timer service */
   @Resource TimerService tservice;
   private Random random;
   private volatile double price = 100.0;
   private volatile int volume = 300000;
   private static final Logger logger = Logger.getLogger("PriceVolumeBean");
   
   @PostConstruct
   public void init() {
       /* Initialize the EJB and create a timer */
       logger.log(Level.INFO, "Initializing EJB.");
       random = new Random();
       tservice.createIntervalTimer(1000, 1000, new TimerConfig());
   }
   
   @Timeout
   public void timeout() {
       /* Adjust price and volume and send updates */
       price += 1.0*(random.nextInt(100)-50)/100.0;
       volume += random.nextInt(5000) - 2500;
       ETFEndpoint.send(price, volume);
   }
}
```

The enterprise bean calls the `send` method of the `ETFEndpoint` class
in the timeout method. See [Using the Timer
Service](ejb-basicexamples005.htm#BNBOY) in [Chapter 34, "Running the
Enterprise Bean Examples"](ejb-basicexamples.htm#GIJRB) for more
information on the timer service.

### 18.11.1.3 The HTML Page

The HTML page consists of a table and some JavaScript code. The table
contains two fields referenced from JavaScript code:

``` oac_no_warn
<!DOCTYPE html>
<html>
<head>...</head>
<body>
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

The JavaScript code uses the WebSocket API to connect to the server
endpoint and to designate a callback method for incoming messages. The
callback method updates the page with the new information.

``` oac_no_warn
var wsocket;
function connect() {
   wsocket = new WebSocket("ws://localhost:8080/dukeetf2/dukeetf");
   wsocket.onmessage = onMessage;
}
function onMessage(evt) {
   var arraypv = evt.data.split("/");
   document.getElementById("price").innerHTML = arraypv[0];
   document.getElementById("volume").innerHTML = arraypv[1];
}
window.addEventListener("load", connect, false);
```

The WebSocket API is supported by most modern browsers, and it is widely
used in HTML5 web client development.

## 18.11.2 Running the dukeetf2 Example Application

This section describes how to run the `dukeetf2` example application
using NetBeans IDE and from the command line.

The following topics are addressed here:

  - [Section 18.11.2.1, "To Run the dukeetf2 Example Application Using
    NetBeans IDE"](#CIHEBIAH)

  - [Section 18.11.2.2, "To Run the dukeetf2 Example Application Using
    Maven"](#CIHDJCGJ)

### 18.11.2.1 To Run the dukeetf2 Example Application Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/websocket
    ```

4.  Select the `dukeetf2` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `dukeetf2` project and select
    Run.
    
    This command builds and packages the application into a WAR file
    (`dukeetf2.war`) located in the `target/` directory, deploys it to
    the server, and launches a web browser window with the following
    URL:
    
    ``` oac_no_warn
    http://localhost:8080/dukeetf2/
    ```
    
    Open the same URL on a different web browser tab or window to see
    how both pages get price and volume updates simultaneously.

### 18.11.2.2 To Run the dukeetf2 Example Application Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/websocket/dukeetf2/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```

4.  Open a web browser window and enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/dukeetf2/
    ```
    
    Open the same URL on a different web browser tab or window to see
    how both pages get price and volume updates simultaneously.

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
<td><a href="websocket010.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket012.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
