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
<td><a href="websocket001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 18.2 Creating WebSocket Applications in the Java EE Platform

The Java EE platform includes the Java API for WebSocket (JSR 356),
which enables you to create, configure, and deploy WebSocket endpoints
in web applications. The WebSocket client API specified in JSR 356 also
enables you to access remote WebSocket endpoints from any Java
application.

The Java API for WebSocket consists of the following packages.

  - The `javax.websocket.server` package contains annotations, classes,
    and interfaces to create and configure server endpoints.

  - The `javax.websocket` package contains annotations, classes,
    interfaces, and exceptions that are common to client and server
    endpoints.

WebSocket endpoints are instances of the `javax.websocket.Endpoint`
class. The Java API for WebSocket enables you to create two kinds of
endpoints: programmatic endpoints and annotated endpoints. To create a
programmatic endpoint, you extend the `Endpoint` class and override its
lifecycle methods. To create an annotated endpoint, you decorate a Java
class and some of its methods with the annotations provided by the
packages mentioned previously. After you have created an endpoint, you
deploy it to an specific URI in the application so that remote clients
can connect to it.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
In most cases, it is easier to create and deploy an annotated endpoint than a programmatic endpoint. This chapter provides a simple example of a programmatic endpoint, but it focuses on annotated endpoints.</td>
</tr>
</tbody>
</table>

  

## 18.2.1 Creating and Deploying a WebSocket Endpoint

The process for creating and deploying a WebSocket endpoint:

1.  Create an endpoint class.

2.  Implement the lifecycle methods of the endpoint.

3.  Add your business logic to the endpoint.

4.  Deploy the endpoint inside a web application.

The process is slightly different for programmatic endpoints and
annotated endpoints, and it is covered in detail in the following
sections.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
As opposed to servlets, WebSocket endpoints are instantiated multiple times. The container creates an instance of an endpoint per connection to its deployment URI. Each instance is associated with one and only one connection. This facilitates keeping user state for each connection and makes development easier, because there is only one thread executing the code of an endpoint instance at any given time.</td>
</tr>
</tbody>
</table>

  

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
<td><a href="websocket001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
