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
<td><a href="cdi-basic001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basic003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 23.2 Overview of CDI

CDI is a set of services that, used together, make it easy for
developers to use enterprise beans along with JavaServer Faces
technology in web applications. Designed for use with stateful objects,
CDI also has many broader uses, allowing developers a great deal of
flexibility to integrate various kinds of components in a loosely
coupled but typesafe way

CDI 1.1 is specified by JSR 346. Related specifications that CDI uses
include the following:

  - JSR 330, Dependency Injection for Java

  - The Managed Beans specification, an offshoot of the Java EE 7
    platform specification (JSR 342)

The most fundamental services provided by CDI are as follows.

  - Contexts: This service enables you to bind the lifecycle and
    interactions of stateful components to well-defined but extensible
    lifecycle contexts.

  - Dependency injection: This service enables you to inject components
    into an application in a typesafe way and to choose at deployment
    time which implementation of a particular interface to inject.

In addition, CDI provides the following services:

  - Integration with the Expression Language (EL), which allows any
    component to be used directly within a JavaServer Faces page or a
    JavaServer Pages page

  - The ability to decorate injected components

  - The ability to associate interceptors with components using typesafe
    interceptor bindings

  - An event-notification model

  - A web conversation scope in addition to the three standard scopes
    (request, session, and application) defined by the Java Servlet
    specification

  - A complete Service Provider Interface (SPI) that allows third-party
    frameworks to integrate cleanly in the Java EE 7 environment

A major theme of CDI is loose coupling. CDI does the following:

  - Decouples the server and the client by means of well-defined types
    and qualifiers, so that the server implementation may vary

  - Decouples the lifecycles of collaborating components by
    
      - Making components contextual, with automatic lifecycle
        management
    
      - Allowing stateful components to interact like services, purely
        by message passing

  - Completely decouples message producers from consumers, by means of
    events

  - Decouples orthogonal concerns by means of Java EE interceptors

Along with loose coupling, CDI provides strong typing by

  - Eliminating lookup using string-based names for wiring and
    correlations so that the compiler will detect typing errors

  - Allowing the use of declarative Java annotations to specify
    everything, largely eliminating the need for XML deployment
    descriptors, and making it easy to provide tools that introspect the
    code and understand the dependency structure at development time

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
<td><a href="cdi-basic001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basic003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
