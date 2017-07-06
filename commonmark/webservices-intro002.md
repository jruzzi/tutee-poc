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
<td><a href="webservices-intro001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="webservices-intro003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 27.2 Types of Web Services

On the conceptual level, a service is a software component provided
through a network-accessible endpoint. The service consumer and provider
use messages to exchange invocation request and response information in
the form of self-containing documents that make very few assumptions
about the technological capabilities of the receiver.

On a technical level, web services can be implemented in various ways.
The two types of web services discussed in this section can be
distinguished as "big" web services and "RESTful" web services.

The following topics are addressed here:

  - [Section 27.2.1, ""Big" Web Services"](#GKCDG)

  - [Section 27.2.2, "RESTful Web Services"](#GKCAW)

## 27.2.1 "Big" Web Services

In Java EE 7, JAX-WS provides the functionality for "big" web services,
which are described in [Chapter 28, "Building Web Services with
JAX-WS"](jaxws.htm#BNAYL). Big web services use XML messages that follow
the Simple Object Access Protocol (SOAP) standard, an XML language
defining a message architecture and message formats. Such systems often
contain a machine-readable description of the operations offered by the
service, written in the Web Services Description Language (WSDL), an XML
language for defining interfaces syntactically.

The SOAP message format and the WSDL interface definition language have
gained widespread adoption. Many development tools, such as NetBeans
IDE, can reduce the complexity of developing web service applications.

A SOAP-based design must include the following elements.

  - A formal contract must be established to describe the interface that
    the web service offers. WSDL can be used to describe the details of
    the contract, which may include messages, operations, bindings, and
    the location of the web service. You may also process SOAP messages
    in a JAX-WS service without publishing a WSDL.

  - The architecture must address complex nonfunctional requirements.
    Many web service specifications address such requirements and
    establish a common vocabulary for them. Examples include
    transactions, security, addressing, trust, coordination, and so on.

  - The architecture needs to handle asynchronous processing and
    invocation. In such cases, the infrastructure provided by standards,
    such as Web Services Reliable Messaging (WSRM), and APIs, such as
    JAX-WS, with their client-side asynchronous invocation support, can
    be leveraged out of the box.

## 27.2.2 RESTful Web Services

In Java EE 7, JAX-RS provides the functionality for Representational
State Transfer (RESTful) web services. REST is well suited for basic, ad
hoc integration scenarios. RESTful web services, often better integrated
with HTTP than SOAP-based services are, do not require XML messages or
WSDL service-API definitions.

Project Jersey is the production-ready reference implementation for the
JAX-RS specification. Jersey implements support for the annotations
defined in the JAX-RS specification, making it easy for developers to
build RESTful web services with Java and the Java Virtual Machine (JVM).

Because RESTful web services use existing well-known W3C and Internet
Engineering Task Force (IETF) standards (HTTP, XML, URI, MIME) and have
a lightweight infrastructure that allows services to be built with
minimal tooling, developing RESTful web services is inexpensive and thus
has a very low barrier for adoption. You can use a development tool such
as NetBeans IDE to further reduce the complexity of developing RESTful
web services.

A RESTful design may be appropriate when the following conditions are
met.

  - The web services are completely stateless. A good test is to
    consider whether the interaction can survive a restart of the
    server.

  - A caching infrastructure can be leveraged for performance. If the
    data that the web service returns is not dynamically generated and
    can be cached, the caching infrastructure that web servers and other
    intermediaries inherently provide can be leveraged to improve
    performance. However, the developer must take care because such
    caches are limited to the HTTP `GET` method for most servers.

  - The service producer and service consumer have a mutual
    understanding of the context and content being passed along. Because
    there is no formal way to describe the web services interface, both
    parties must agree out of band on the schemas that describe the data
    being exchanged and on ways to process it meaningfully. In the real
    world, most commercial applications that expose services as RESTful
    implementations also distribute so-called value-added toolkits that
    describe the interfaces to developers in popular programming
    languages.

  - Bandwidth is particularly important and needs to be limited. REST is
    particularly useful for limited-profile devices, such as PDAs and
    mobile phones, for which the overhead of headers and additional
    layers of SOAP elements on the XML payload must be restricted.

  - Web service delivery or aggregation into existing websites can be
    enabled easily with a RESTful style. Developers can use such
    technologies as JAX-RS and Asynchronous JavaScript with XML (Ajax)
    and such toolkits as Direct Web Remoting (DWR) to consume the
    services in their web applications. Rather than starting from
    scratch, services can be exposed with XML and consumed by HTML pages
    without significantly refactoring the existing website architecture.
    Existing developers will be more productive because they are adding
    to something they are already familiar with rather than having to
    start from scratch with new technology.

RESTful web services are discussed in [Chapter 29, "Building RESTful Web
Services with JAX-RS"](jaxrs.htm#GIEPU). This chapter contains
information about generating the skeleton of a RESTful web service using
both NetBeans IDE and the Maven project-management tool.

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
<td><a href="webservices-intro001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="webservices-intro003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
