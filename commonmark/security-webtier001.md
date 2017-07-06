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
<td><a href="security-webtier.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-webtier002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 48.1 Overview of Web Application Security

A web application is accessed using a web browser over a network, such
as the Internet or a company's intranet. As discussed in [Distributed
Multitiered Applications](overview004.htm#BNAAY), the Java EE platform
uses a distributed multitiered application model, and web applications
run in the web tier.

Web applications contain resources that can be accessed by many users.
These resources often traverse unprotected, open networks, such as the
Internet. In such an environment, a substantial number of web
applications will require some type of security.

Securing applications and their clients in the business tier and the EIS
tier is discussed in [Chapter 49, "Getting Started Securing Enterprise
Applications"](security-javaee.htm#BNBYK).

In the Java EE platform, web components provide the dynamic extension
capabilities for a web server. Web components can be Java servlets or
JavaServer Faces pages.

Certain aspects of web application security can be configured when the
application is installed, or deployed, to the web container. Annotations
and/or deployment descriptors are used to relay information to the
deployer about security and other aspects of the application. Specifying
this information in annotations or in the deployment descriptor helps
the deployer set up the appropriate security policy for the web
application. Any values explicitly specified in the deployment
descriptor override any values specified in annotations.

Security for Java EE web applications can be implemented in the
following ways.

  - Declarative security can be implemented using either metadata
    annotations or an application's deployment descriptor. See [Overview
    of Java EE Security](security-intro001.htm#BNBWK) for more
    information.
    
    Declarative security for web applications is described in [Securing
    Web Applications](security-webtier002.htm#GKBAA).

  - Programmatic security is embedded in an application and can be used
    to make security decisions when declarative security alone is not
    sufficient to express the security model of an application.
    Declarative security alone may not be sufficient when conditional
    login in a particular work flow, instead of for all cases, is
    required in the middle of an application. See [Overview of Java EE
    Security](security-intro001.htm#BNBWK) for more information.
    
    Servlet 3.1 provides the `authenticate`, `login`, and `logout`
    methods of the `HttpServletRequest` interface. With the addition of
    the `authenticate`, `login`, and `logout` methods to the Servlet
    specification, an application deployment descriptor is no longer
    required for web applications but may still be used to further
    specify security requirements beyond the basic default values.
    
    Programmatic security is discussed in [Using Programmatic Security
    with Web Applications](security-webtier003.htm#GJIIE).

  - Message security works with web services and incorporates security
    features, such as digital signatures and encryption, into the header
    of a SOAP message, working in the application layer, ensuring
    end-to-end security. Message security is not a component of Java EE
    7 and is mentioned here for informational purposes only.

Some of the material in this chapter builds on material presented
earlier in this tutorial. In particular, this chapter assumes that you
are familiar with the information in the following chapters:

  - [Chapter 6, "Getting Started with Web
    Applications"](webapp.htm#BNADR)

  - [Chapter 7, "JavaServer Faces Technology"](jsf-intro.htm#BNAPH)

  - [Chapter 17, "Java Servlet Technology"](servlets.htm#BNAFD)

  - [Chapter 47, "Introduction to Security in the Java EE
    Platform"](security-intro.htm#BNBWJ)

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
<td><a href="security-webtier.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-webtier002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
