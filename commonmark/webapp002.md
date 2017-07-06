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
<td><a href="webapp001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="webapp003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 6.2 Web Application Lifecycle

A web application consists of web components; static resource files,
such as images and cascading style sheets (CSS); and helper classes and
libraries. The web container provides many supporting services that
enhance the capabilities of web components and make them easier to
develop. However, because a web application must take these services
into account, the process for creating and running a web application is
different from that of traditional stand-alone Java classes.

The process for creating, deploying, and executing a web application can
be summarized as follows:

1.  Develop the web component code.

2.  Develop the web application deployment descriptor, if necessary.

3.  Compile the web application components and helper classes referenced
    by the components.

4.  Optionally, package the application into a deployable unit.

5.  Deploy the application into a web container.

6.  Access a URL that references the web application.

Developing web component code is covered in the later chapters. Steps 2
through 4 are expanded on in the following sections and illustrated with
a Hello, World–style, presentation-oriented application. This
application allows a user to enter a name into an HTML form and then
displays a greeting after the name is submitted.

The Hello application contains two web components that generate the
greeting and the response. This chapter discusses the following simple
applications:

  - `hello1`, a JavaServer Faces technology–based application that uses
    two XHTML pages and a managed bean

  - `hello2`, a servlet-based web application in which the components
    are implemented by two servlet classes

The applications are used to illustrate tasks involved in packaging,
deploying, configuring, and running an application that contains web
components.

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
<td><a href="webapp001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="webapp003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
