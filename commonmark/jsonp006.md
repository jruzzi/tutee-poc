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
<td><a href="jsonp005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsonp007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 19.6 The jsonpmodel Example Application

This section describes how to build and run the `jsonpmodel` example
application. This example is a web application that demonstrates how to
create an object model from form data, how to parse JSON data, and how
write JSON data using the object model API.

The `jsonpmodel` example application is in the
tut-install`/examples/web/jsonp/jsonpmodel` directory.

The following topics are addressed here:

  - [Section 19.6.1, "Components of the jsonpmodel Example
    Application"](#CEGHHCCC)

  - [Section 19.6.2, "Running the jsonpmodel Example
    Application"](#CEGEFHFH)

## 19.6.1 Components of the jsonpmodel Example Application

The `jsonpmodel` example application contains the following files.

  - Three JavaServer Faces pages.
    
      - The `index.xhtml` page contains a form to collect information.
    
      - The `modelcreated.xhtml` page contains a text area that displays
        JSON data.
    
      - The `parsejson.xhtml` page contains a table that shows the
        elements of the object model.

  - The `ObjectModelBean.java` managed bean, which is a session-scoped
    managed bean that stores the data from the form and directs the
    navigation between the Facelets pages. This file also contains code
    that uses the JSON object model API.

The code used in `ObjectModelBean.java` to create an object model from
the data in the form is similar to the example in [Creating an Object
Model from Application Code](jsonp003.htm#BABIGIAF). The code to write
JSON output from the model is similar to the example in [Writing an
Object Model to a Stream](jsonp003.htm#BABHEJFF). The code to navigate
the object model tree is similar to the example in [Navigating an Object
Model](jsonp003.htm#BABJHEHG).

## 19.6.2 Running the jsonpmodel Example Application

This section describes how to run the `jsonpmodel` example application
using NetBeans IDE and from the command line.

The following topics are addressed here:

  - [Section 19.6.2.1, "To Run the jsonpmodel Example Application Using
    NetBeans IDE"](#CEGFECCB)

  - [Section 19.6.2.2, "To Run the jsonpmodel Example Application Using
    Maven"](#CEGGJBFA)

### 19.6.2.1 To Run the jsonpmodel Example Application Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsonp
    ```

4.  Select the `jsonpmodel` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `jsonpmodel` project and select
    Run.
    
    This command builds and packages the application into a WAR file
    (`jsonpmodel.war`) located in the `target` directory, deploys it to
    the server, and opens a web browser window with the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/jsonpmodel/
    ```

7.  Edit the data on the page and click Create a JSON Object to submit
    the form. The following page shows a JSON object that contains the
    data from the form.

8.  Click Parse JSON. The following page contains a table that lists the
    nodes of the object model tree.

### 19.6.2.2 To Run the jsonpmodel Example Application Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsonp/jsonpmodel
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```

4.  Open a web browser window and enter the following address:
    
    ``` oac_no_warn
    http://localhost:8080/jsonpmodel/
    ```

5.  Edit the data on the page and click Create a JSON Object to submit
    the form. The following page shows a JSON object that contains the
    data from the form.

6.  Click Parse JSON. The following page contains a table that lists the
    nodes of the object model tree.

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
<td><a href="jsonp005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsonp007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
