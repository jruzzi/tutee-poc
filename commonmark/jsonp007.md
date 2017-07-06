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
<td><a href="jsonp006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsonp008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 19.7 The jsonpstreaming Example Application

This section describes how to build and run the `jsonpstreaming` example
application. This example is a web application that demonstrates how to
create JSON data from form data, how to parse JSON data, and how to
write JSON output using the streaming API.

The `jsonpstreaming` example application is in the
tut-install`/examples/web/jsonp/jsonpstreaming` directory.

The following topics are addressed here:

  - [Section 19.7.1, "Components of the jsonpstreaming Example
    Application"](#CEGDBIID)

  - [Section 19.7.2, "Running the jsonpstreaming Example
    Application"](#CEGGHFIG)

## 19.7.1 Components of the jsonpstreaming Example Application

The `jsonpstreaming` example application contains the following files.

  - Three JavaServer Faces pages.
    
      - The `index.xhtml` page contains a form to collect information.
    
      - The `filewritten.xhtml` page contains a text area that displays
        JSON data.
    
      - The `parsed.xhtml` page contains a table that lists the events
        from the parser.

  - The `StreamingBean.java` managed bean, a session-scoped managed bean
    that stores the data from the form and directs the navigation
    between the Facelets pages. This file also contains code that uses
    the JSON streaming API.

The code used in `StreamingBean.java` to write JSON data to a file is
similar to the example in [Writing JSON Data Using a
Generator](jsonp004.htm#BABGJEEF). The code to parse JSON data from a
file is similar to the example in [Reading JSON Data Using a
Parser](jsonp004.htm#BABGCHIG).

## 19.7.2 Running the jsonpstreaming Example Application

This section describes how to run the `jsonpstreaming` example
application using NetBeans IDE and from the command line.

The following topics are addressed here:

  - [Section 19.7.2.1, "To Run the jsonpstreaming Example Application
    Using NetBeans IDE"](#CEGJCBCG)

  - [Section 19.7.2.2, "To Run the jsonpstreaming Example Application
    Using
Maven"](#CEGCGDDJ)

### 19.7.2.1 To Run the jsonpstreaming Example Application Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsonp
    ```

4.  Select the `jsonpstreaming` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `jsonpstreaming` project and
    select Run.
    
    This command builds and packages the application into a WAR file
    (`jsonpstreaming.war`) located in the `target` directory, deploys it
    to the server, and opens a web browser window with the following
    URL:
    
    ``` oac_no_warn
    http://localhost:8080/jsonpstreaming/
    ```

7.  Edit the data on the page and click Write a JSON Object to a File to
    submit the form and write a JSON object to a text file. The
    following page shows the contents of the text file.

8.  Click Parse JSON from File. The following page contains a table that
    lists the parser events for the JSON data in the text file.

### 19.7.2.2 To Run the jsonpstreaming Example Application Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsonp/jsonpstreaming/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```

4.  Open a web browser window and enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/jsonpstreaming/
    ```

5.  Edit the data on the page and click Write a JSON Object to a File to
    submit the form and write a JSON object to a text file. The
    following page shows the contents of the text file.

6.  Click Parse JSON from File. The following page contains a table that
    lists the parser events for the JSON data in the text file.

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
<td><a href="jsonp006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsonp008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
