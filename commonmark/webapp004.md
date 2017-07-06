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
<td><a href="webapp003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="webapp005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 6.4 A Web Module That Uses Java Servlet Technology: The hello2 Example

The `hello2` application is a web module that uses Java Servlet
technology to display a greeting and response. You can use a text editor
to view the application files, or you can use NetBeans IDE.

The source code for this application is in the
tut-install`/examples/web/servlet/hello2/` directory.

The following topics are addressed here:

  - [Section 6.4.1, "Mapping URLs to Web Components"](#BNAEP)

  - [Section 6.4.2, "Examining the hello2 Web Module"](#GJWWG)

  - [Section 6.4.3, "Running the hello2 Example"](#GKBLH)

## 6.4.1 Mapping URLs to Web Components

When it receives a request, the web container must determine which web
component should handle the request. The web container does so by
mapping the URL path contained in the request to a web application and a
web component. A URL path contains the context root and, optionally, a
URL pattern:

``` oac_no_warn
http://host:port/context-root[/url-pattern]
```

You set the URL pattern for a servlet by using the `@WebServlet`
annotation in the servlet source file. For example, the
`GreetingServlet.java` file in the `hello2` application contains the
following annotation, specifying the URL pattern as `/greeting`:

``` oac_no_warn
@WebServlet("/greeting")
public class GreetingServlet extends HttpServlet {
    ...
```

This annotation indicates that the URL pattern `/greeting` follows the
context root. Therefore, when the servlet is deployed locally, it is
accessed with the following URL:

``` oac_no_warn
http://localhost:8080/hello2/greeting
```

To access the servlet by using only the context root, specify `"/"` as
the URL pattern.

## 6.4.2 Examining the hello2 Web Module

The `hello2` application behaves almost identically to the `hello1`
application, but it is implemented using Java Servlet technology instead
of JavaServer Faces technology. You can use a text editor to view the
application files, or you can use NetBeans IDE.

### 6.4.2.1 To View the hello2 Web Module Using NetBeans IDE

To view the `hello2` web module using NetBeans IDE:

1.  From the File menu, choose Open Project.

2.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/servlet
    ```

3.  Select the `hello2` folder and click Open Project.

4.  Expand the Source Packages node, then expand the
    `javaeetutorial.hello2` node.

5.  Double-click the `GreetingServlet.java` file to view it.
    
    This servlet overrides the `doGet` method, implementing the `GET`
    method of HTTP. The servlet displays a simple HTML greeting form
    whose Submit button, like that of `hello1`, specifies a response
    page for its action. The following excerpt begins with the
    `@WebServlet` annotation, which specifies the URL pattern relative
    to the context root:
    
    ``` oac_no_warn
    @WebServlet("/greeting")
    public class GreetingServlet extends HttpServlet {
    
        @Override
        public void doGet(HttpServletRequest request,
                HttpServletResponse response)
                throws ServletException, IOException {
    
            response.setContentType("text/html");
            response.setBufferSize(8192);
            try (PrintWriter out = response.getWriter()) {
                out.println("<html lang=\"en\">"
                        + "<head><title>Servlet Hello</title></head>");
    
                // then write the data of the response
                out.println("<body  bgcolor=\"#ffffff\">"
                    + "<img src=\"duke.waving.gif\" "
                    + "alt=\"Duke waving his hand\">"
                    + "<form method=\"get\">"
                    + "<h2>Hello, my name is Duke. What's yours?</h2>"
                    + "<input title=\"My name is: \"type=\"text\" "
                    + "name=\"username\" size=\"25\">"
                    + "<p></p>"
                    + "<input type=\"submit\" value=\"Submit\">"
                    + "<input type=\"reset\" value=\"Reset\">"
                    + "</form>");
    
                String username = request.getParameter("username");
                if (username != null && username.length()> 0) {
                    RequestDispatcher dispatcher =
                        getServletContext().getRequestDispatcher("/response");
    
                    if (dispatcher != null) {
                        dispatcher.include(request, response);
                    }
                }
                out.println("</body></html>");
            }
        }
        ...
    ```

6.  Double-click the `ResponseServlet.java` file to view it.
    
    This servlet also overrides the `doGet` method, displaying only the
    response. The following excerpt begins with the `@WebServlet`
    annotation, which specifies the URL pattern relative to the context
    root:
    
    ``` oac_no_warn
    @WebServlet("/response")
    public class ResponseServlet extends HttpServlet {
    
        @Override
        public void doGet(HttpServletRequest request,
                HttpServletResponse response)
                throws ServletException, IOException {
            try (PrintWriter out = response.getWriter()) {
    
                // then write the data of the response
                String username = request.getParameter("username");
                if (username != null && username.length()> 0) {
                    out.println("<h2>Hello, " + username + "!</h2>");
                }
            }
        }
        ...
    ```

## 6.4.3 Running the hello2 Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `hello2` example.

The following topics are addressed here:

  - [Section 6.4.3.1, "To Run the hello2 Example Using NetBeans
    IDE"](#GJSED)

  - [Section 6.4.3.2, "To Run the hello2 Example Using Maven"](#GJSHX)

### 6.4.3.1 To Run the hello2 Example Using NetBeans IDE

To run the `hello2` example using NetBeans IDE:

1.  Start GlassFish Server as described in [To Start GlassFish Server
    Using NetBeans IDE](usingexamples002.htm#CHDCACDI), if you have not
    already done so.

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/servlet
    ```

4.  Select the `hello2` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `hello2` project and select
    Build to package and deploy the project.

7.  In a web browser, open the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/hello2/greeting
    ```
    
    The URL specifies the context root, followed by the URL pattern.
    
    The application looks much like the `hello1` application. The major
    difference is that after you click Submit the response appears below
    the greeting, not on a separate page.

### 6.4.3.2 To Run the hello2 Example Using Maven

To run the `hello2` example using Maven:

1.  Start GlassFish Server as described in [To Start GlassFish Server
    Using the Command Line](usingexamples002.htm#CHDBDDAF), if you have
    not already done so.

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/servlet/hello2/
    ```

3.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This target builds the WAR file, copies it to the
    tut-install`/examples/web/hello2/target/` directory, and deploys it.

4.  In a web browser, open the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/hello2/greeting
    ```
    
    The URL specifies the context root, followed by the URL pattern.
    
    The application looks much like the `hello1` application. The major
    difference is that after you click Submit the response appears below
    the greeting, not on a separate page.

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
<td><a href="webapp003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="webapp005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
