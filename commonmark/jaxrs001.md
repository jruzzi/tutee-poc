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
<td><a href="jaxrs.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 29.1 What Are RESTful Web Services?

RESTful web services are loosely coupled, lightweight web services that
are particularly well suited for creating APIs for clients spread out
across the internet. Representational State Transfer (REST) is an
architectural style of client-server application centered around the
transfer of representations of resources through requests and responses.
In the REST architectural style, data and functionality are considered
resources and are accessed using Uniform Resource Identifiers (URIs),
typically links on the Web. The resources are represented by documents
and are acted upon by using a set of simple, well-defined operations.

For example, a REST resource might be the current weather conditions for
a city. The representation of that resource might be an XML document, an
image file, or an HTML page. A client might retrieve a particular
representation, modify the resource by updating its data, or delete the
resource entirely.

The REST architectural style is designed to use a stateless
communication protocol, typically HTTP. In the REST architecture style,
clients and servers exchange representations of resources by using a
standardized interface and protocol.

The following principles encourage RESTful applications to be simple,
lightweight, and fast:

  - Resource identification through URI: A RESTful web service exposes a
    set of resources that identify the targets of the interaction with
    its clients. Resources are identified by URIs, which provide a
    global addressing space for resource and service discovery. See [The
    @Path Annotation and URI Path Templates](jaxrs002.htm#GINPW) for
    more information.

  - Uniform interface: Resources are manipulated using a fixed set of
    four create, read, update, delete operations: PUT, GET, POST, and
    DELETE. PUT creates a new resource, which can be then deleted by
    using DELETE. GET retrieves the current state of a resource in some
    representation. POST transfers a new state onto a resource. See
    [Responding to HTTP Methods and Requests](jaxrs002.htm#GIPYS) for
    more information.

  - Self-descriptive messages: Resources are decoupled from their
    representation so that their content can be accessed in a variety of
    formats, such as HTML, XML, plain text, PDF, JPEG, JSON, and other
    document formats. Metadata about the resource is available and used,
    for example, to control caching, detect transmission errors,
    negotiate the appropriate representation format, and perform
    authentication or access control. See [Responding to HTTP Methods
    and Requests](jaxrs002.htm#GIPYS) and [Using Entity Providers to Map
    HTTP Response and Request Entity Bodies](jaxrs002.htm#GIPZE) for
    more information.

  - Stateful interactions through links: Every interaction with a
    resource is stateless; that is, request messages are self-contained.
    Stateful interactions are based on the concept of explicit state
    transfer. Several techniques exist to exchange state, such as URI
    rewriting, cookies, and hidden form fields. State can be embedded in
    response messages to point to valid future states of the
    interaction. See [Using Entity Providers to Map HTTP Response and
    Request Entity Bodies](jaxrs002.htm#GIPZE) and "Building URIs" in
    the JAX-RS Overview document for more information.

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
<td><a href="jaxrs.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
