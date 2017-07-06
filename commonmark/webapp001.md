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
<td><a href="webapp.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="webapp002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 6.1 Web Applications

A web application is a dynamic extension of a web or application server.
Web applications are of the following types:

  - Presentation-oriented: A presentation-oriented web application
    generates interactive web pages containing various types of markup
    language (HTML, XHTML, XML, and so on) and dynamic content in
    response to requests. Development of presentation-oriented web
    applications is covered in [Chapter 7, "JavaServer Faces
    Technology,"](jsf-intro.htm#BNAPH) through [Chapter 17, "Java
    Servlet Technology."](servlets.htm#BNAFD)

  - Service-oriented: A service-oriented web application implements the
    endpoint of a web service. Presentation-oriented applications are
    often clients of service-oriented web applications. Development of
    service-oriented web applications is covered in [Chapter 28,
    "Building Web Services with JAX-WS,"](jaxws.htm#BNAYL) and [Chapter
    29, "Building RESTful Web Services with JAX-RS,"](jaxrs.htm#GIEPU)
    in [Part III, "Web Services."](partwebsvcs.htm#BNAYK)

In the Java EE platform, web components provide the dynamic extension
capabilities for a web server. Web components can be Java servlets, web
pages implemented with JavaServer Faces technology, web service
endpoints, or JSP pages. [Figure 6-1](#BNADS) illustrates the
interaction between a web client and a web application that uses a
servlet. The client sends an HTTP request to the web server. A web
server that implements Java Servlet and JavaServer Pages technology
converts the request into an `HTTPServletRequest` object. This object is
delivered to a web component, which can interact with JavaBeans
components or a database to generate dynamic content. The web component
can then generate an `HTTPServletResponse` or can pass the request to
another web component. A web component eventually generates a
`HTTPServletResponse` object. The web server converts this object to an
HTTP response and returns it to the client.

Figure 6-1 Java Web Application Request Handling

![Description of Figure 6-1 follows](img/jeett_dt_013.png)  
[Description of "Figure 6-1 Java Web Application Request
Handling"](img_text/jeett_dt_013.htm)  
  

Servlets are Java programming language classes that dynamically process
requests and construct responses. Java technologies, such as JavaServer
Faces and Facelets, are used for building interactive web applications.
(Frameworks can also be used for this purpose.) Although servlets and
JavaServer Faces and Facelets pages can be used to accomplish similar
things, each has its own strengths. Servlets are best suited for
service-oriented applications (web service endpoints can be implemented
as servlets) and the control functions of a presentation-oriented
application, such as dispatching requests and handling nontextual data.
JavaServer Faces and Facelets pages are more appropriate for generating
text-based markup, such as XHTML, and are generally used for
presentation-oriented applications.

Web components are supported by the services of a runtime platform
called a web container. A web container provides such services as
request dispatching, security, concurrency, and lifecycle management. A
web container also gives web components access to such APIs as naming,
transactions, and email.

Certain aspects of web application behavior can be configured when the
application is installed, or deployed, to the web container. The
configuration information can be specified using Java EE annotations or
can be maintained in a text file in XML format called a web application
deployment descriptor (DD). A web application DD must conform to the
schema described in the Java Servlet specification.

This chapter gives a brief overview of the activities involved in
developing web applications. First, it summarizes the web application
lifecycle and explains how to package and deploy very simple web
applications on GlassFish Server. The chapter then moves on to
configuring web applications and discusses how to specify the most
commonly used configuration parameters.

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
<td><a href="webapp.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="webapp002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
