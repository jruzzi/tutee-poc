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
<td><a href="jsf-intro001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-intro003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 7.2 What Is a JavaServer Faces Application?

The functionality provided by a JavaServer Faces application is similar
to that of any other Java web application. A typical JavaServer Faces
application includes the following parts.

  - A set of web pages in which components are laid out.

  - A set of tags to add components to the web page.

  - A set of managed beans, which are lightweight, container-managed
    objects (POJOs). In a JavaServer Faces application, managed beans
    serve as backing beans, which define properties and functions for UI
    components on a page.

  - A web deployment descriptor (`web.xml` file).

  - Optionally, one or more application configuration resource files,
    such as a `faces-config.xml` file, which can be used to define page
    navigation rules and configure beans and other custom objects, such
    as custom components.

  - Optionally, a set of custom objects, which can include custom
    components, validators, converters, or listeners, created by the
    application developer.

  - Optionally, a set of custom tags for representing custom objects on
    the page.

[Figure 7-1](#BNAPI) shows the interaction between client and server in
a typical JavaServer Faces application. In response to a client request,
a web page is rendered by the web container that implements JavaServer
Faces technology.

Figure 7-1 Responding to a Client Request for a JavaServer Faces Page

![Description of Figure 7-1 follows](img/jeett_dt_014.png)  
[Description of "Figure 7-1 Responding to a Client Request for a
JavaServer Faces Page"](img_text/jeett_dt_014.htm)  
  

The web page, `myfacelet.xhtml`, is built using JavaServer Faces
component tags. Component tags are used to add components to the `view`
(represented by `myView` in the diagram), which is the server-side
representation of the page. In addition to components, the web page can
also reference objects, such as the following:

  - Any event listeners, validators, and converters that are registered
    on the components

  - The JavaBeans components that capture the data and process the
    application-specific functionality of the components

On request from the client, the view is rendered as a response.
Rendering is the process whereby, based on the server-side view, the web
container generates output, such as HTML or XHTML, that can be read by
the client, such as a browser.

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
<td><a href="jsf-intro001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-intro003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
