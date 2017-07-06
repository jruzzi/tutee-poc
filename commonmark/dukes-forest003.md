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
<td><a href="dukes-forest002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-forest004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 59.3 Building and Deploying the Duke's Forest Case Study Application

You can use NetBeans IDE or Maven to build and deploy Duke's Forest.

The following topics are addressed here:

  - [Section 59.3.1, "To Build and Deploy the Duke's Forest Application
    Using NetBeans IDE"](#CHDJDIFH)

  - [Section 59.3.2, "To Build and Deploy the Duke's Forest Application
    Using
Maven"](#CHDEJHBJ)

## 59.3.1 To Build and Deploy the Duke's Forest Application Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)), as well as
    the database server (see [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/case-studies
    ```

4.  Select the `dukes-forest` folder.

5.  Select the Open Required Projects check box and click Open Project.

6.  Right-click the `dukes-forest` folder and select Build.
    
    This task configures the server, creates and populates the database,
    builds all the subprojects, assembles them into JAR and WAR files,
    and deploys the `dukes-payment`, `dukes-store,` and `dukes-shipment`
    applications.
    
    To configure the server, this task creates a JDBC security realm
    named jdbcRealm, enables default principal-to-role mapping, and
    enables single sign-on (SSO) for the HTTP Service.

## 59.3.2 To Build and Deploy the Duke's Forest Application Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)), as well as
    the database server (see [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/case-studies/dukes-forest/
    ```

3.  Enter the following command to configure the server, create and
    populate the database, build all the subprojects, assemble them into
    JAR and WAR files, and deploy the `dukes-payment`, `dukes-store,`
    and `dukes-shipment` applications:
    
    ``` oac_no_warn
    mvn install
    ```
    
    To configure the server, this task creates a JDBC security realm
    named jdbcRealm, enables default principal-to-role mapping, and
    enables single sign-on (SSO) for the HTTP Service.

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
<td><a href="dukes-forest002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-forest004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
