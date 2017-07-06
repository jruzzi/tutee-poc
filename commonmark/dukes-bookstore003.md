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
<td><a href="dukes-bookstore002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-tutoring.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 57.3 Running the Duke's Bookstore Case Study Application

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the Duke's Bookstore application.

The following topics are addressed here:

  - [Section 57.3.1, "To Build and Deploy Duke's Bookstore Using
    NetBeans IDE"](#GLPQG)

  - [Section 57.3.2, "To Build and Deploy Duke's Bookstore Using
    Maven"](#GLPQN)

  - [Section 57.3.3, "To Run Duke's Bookstore"](#BABEHDEG)

## 57.3.1 To Build and Deploy Duke's Bookstore Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/case-studies
    ```

4.  Select the `dukes-bookstore` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `dukes-bookstore` project and
    select Build.
    
    This will build, package, and deploy Duke's Bookstore to GlassFish
    Server.

## 57.3.2 To Build and Deploy Duke's Bookstore Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)), as well as
    the database server (see [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/case-studies/dukes-bookstore/
    ```

3.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds the application and packages it in a WAR file in
    the tut-install`/examples/case-studies/dukes-bookstore/target/`
    directory. It then deploys the application to GlassFish Server.

## 57.3.3 To Run Duke's Bookstore

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/dukes-bookstore/
    ```

2.  On the Duke's Bookstore main page, click a book in the graphic, or
    click one of the links at the bottom of the page.

3.  Use the pages in the application to view and purchase books.

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
<td><a href="dukes-bookstore002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-tutoring.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
