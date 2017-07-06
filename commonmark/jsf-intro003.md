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
<td><a href="jsf-intro002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-intro004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 7.3 JavaServer Faces Technology Benefits

One of the greatest advantages of JavaServer Faces technology is that it
offers a clean separation between behavior and presentation for web
applications. A JavaServer Faces application can map HTTP requests to
component-specific event handling and manage components as stateful
objects on the server. JavaServer Faces technology allows you to build
web applications that implement the finer-grained separation of behavior
and presentation that is traditionally offered by client-side UI
architectures.

The separation of logic from presentation also allows each member of a
web application development team to focus on a single piece of the
development process and provides a simple programming model to link the
pieces. For example, page authors with no programming expertise can use
JavaServer Faces technology tags in a web page to link to server-side
objects without writing any scripts.

Another important goal of JavaServer Faces technology is to leverage
familiar component and web-tier concepts without limiting you to a
particular scripting technology or markup language. JavaServer Faces
technology APIs are layered directly on top of the Servlet API, as shown
in [Figure 7-2](#GJEPW).

Figure 7-2 Java Web Application Technologies

![Description of Figure 7-2 follows](img/jeett_dt_015.png)  
[Description of "Figure 7-2 Java Web Application
Technologies"](img_text/jeett_dt_015.htm)  
  

This layering of APIs enables several important application use cases,
such as using different presentation technologies, creating your own
custom components directly from the component classes, and generating
output for various client devices.

Facelets technology, available as part of JavaServer Faces technology,
is the preferred presentation technology for building JavaServer Faces
technology–based web applications. For more information on Facelets
technology features, see [Chapter 8, "Introduction to
Facelets"](jsf-facelets.htm#GIEPX).

Facelets technology offers several advantages.

  - Code can be reused and extended for components through the
    templating and composite component features.

  - You can use annotations to automatically register the managed bean
    as a resource available for JavaServer Faces applications. In
    addition, implicit navigation rules allow developers to quickly
    configure page navigation (see [Navigation
    Model](jsf-intro006.htm#BNAQL) for details). These features reduce
    the manual configuration process for applications.

  - Most important, JavaServer Faces technology provides a rich
    architecture for managing component state, processing component
    data, validating user input, and handling events.

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
<td><a href="jsf-intro002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-intro004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
