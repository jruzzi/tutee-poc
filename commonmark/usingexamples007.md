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
<td><a href="usingexamples006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="usingexamples008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 2.7 Java EE 7 Maven Archetypes in the Tutorial

Some of the chapters have instructions on how to build an example
application using Maven archetypes. Archetypes are templates for
generating a particular Maven project. The Tutorial includes several
Maven archetypes for generating Java EE 7 projects.

## 2.7.1 Installing the Tutorial Archetypes

You must install the included Maven archetypes into your local Maven
repository before you can create new projects based on the archetypes.
You can install the archetypes using NetBeans IDE or Maven.

### 2.7.1.1 Installing the Tutorial Archetypes Using NetBeans IDE

1.  From the File menu, choose Open Project.

2.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples
    ```

3.  Select the `archetypes` folder.

4.  Click Open Project.

5.  In the Projects tab, right-click the `archetypes` project and select
    Build.

### 2.7.1.2 Installing the Tutorial Archetypes Using Maven

1.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/archetypes/
    ```

2.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```

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
<td><a href="usingexamples006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="usingexamples008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
