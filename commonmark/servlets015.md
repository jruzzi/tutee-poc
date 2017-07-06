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
<td><a href="servlets014.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets016.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.15 The mood Example Application

The `mood` example application, located in the
tut-install`/examples/web/servlet/mood/` directory, is a simple example
that displays Duke's moods at different times during the day. The
example shows how to develop a simple application by using the
`@WebServlet`, `@WebFilter`, and `@WebListener` annotations to create a
servlet, a listener, and a filter.

The following topics are addressed here:

  - [Section 17.15.1, "Components of the mood Example
    Application"](#CHDEBFCB)

  - [Section 17.15.2, "Running the mood Example"](#GKCOJ)

## 17.15.1 Components of the mood Example Application

The `mood` example application is comprised of three components:
`mood.web.MoodServlet`, `mood.web.TimeOfDayFilter`, and
`mood.web.SimpleServletListener`.

`MoodServlet`, the presentation layer of the application, displays
Duke's mood in a graphic, based on the time of day. The `@WebServlet`
annotation specifies the URL pattern:

``` oac_no_warn
@WebServlet("/report")
public class MoodServlet extends HttpServlet {
    ...
```

`TimeOfDayFilter` sets an initialization parameter indicating that Duke
is awake:

``` oac_no_warn
@WebFilter(filterName = "TimeOfDayFilter",
urlPatterns = {"/*"},
initParams = {
    @WebInitParam(name = "mood", value = "awake")})
public class TimeOfDayFilter implements Filter {
    ...
```

The filter calls the `doFilter` method, which contains a `switch`
statement that sets Duke's mood based on the current time.

`SimpleServletListener` logs changes in the servlet's lifecycle. The log
entries appear in the server log.

## 17.15.2 Running the mood Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `mood` example.

The following topics are addressed here:

  - [Section 17.15.2.1, "To Run the mood Example Using NetBeans
    IDE"](#GKCOB)

  - [Section 17.15.2.2, "To Run the mood Example Using Maven"](#GKCPJ)

### 17.15.2.1 To Run the mood Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/servlet
    ```

4.  Select the `mood` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `mood` project and select
    Build.

7.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/mood/report
    ```
    
    The URL specifies the context root, followed by the URL pattern.
    
    A web page appears with the title "Servlet MoodServlet at /mood", a
    text string describing Duke's mood, and an illustrative graphic.

### 17.15.2.2 To Run the mood Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/servlet/mood/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```

4.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/mood/report
    ```
    
    The URL specifies the context root, followed by the URL pattern.
    
    A web page appears with the title "Servlet MoodServlet at /mood", a
    text string describing Duke's mood, and an illustrative graphic.

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
<td><a href="servlets014.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets016.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
