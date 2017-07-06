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
<td><a href="security-intro002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-intro004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 47.3 Securing Containers

In Java EE, the component containers are responsible for providing
application security. A container provides two types of security:
declarative and programmatic.

The following topics are addressed here:

  - [Section 47.3.1, "Using Annotations to Specify Security
    Information"](#BNBXG)

  - [Section 47.3.2, "Using Deployment Descriptors for Declarative
    Security"](#BNBXF)

  - [Section 47.3.3, "Using Programmatic Security"](#BNBXH)

## 47.3.1 Using Annotations to Specify Security Information

Annotations enable a declarative style of programming and so encompass
both the declarative and programmatic security concepts. Users can
specify information about security within a class file by using
annotations. GlassFish Server uses this information when the application
is deployed. Not all security information can be specified by using
annotations, however. Some information must be specified in the
application deployment descriptors.

Specific annotations that can be used to specify security information
within an enterprise bean class file are described in [Securing an
Enterprise Bean Using Declarative
Security](security-javaee002.htm#GJGDI). [Chapter 48, "Getting Started
Securing Web Applications"](security-webtier.htm#BNCAS), describes how
to use annotations to secure web applications where possible. Deployment
descriptors are described only where necessary.

For more information on annotations, see [Further Information about
Security](security-intro007.htm#BNBYJ).

## 47.3.2 Using Deployment Descriptors for Declarative Security

Declarative security can express an application component's security
requirements by using deployment descriptors. Because deployment
descriptor information is declarative, it can be changed without the
need to modify the source code. At runtime, the Java EE server reads the
deployment descriptor and acts upon the corresponding application,
module, or component accordingly. Deployment descriptors must provide
certain structural information for each component if this information
has not been provided in annotations or is not to be defaulted.

This part of the tutorial does not document how to create deployment
descriptors; it describes only the elements of the deployment descriptor
relevant to security. NetBeans IDE provides tools for creating and
modifying deployment descriptors.

Different types of components use different formats, or schemas, for
their deployment descriptors. The security elements of deployment
descriptors discussed in this tutorial include the following.

  - Web components may use a web application deployment descriptor named
    `web.xml`.
    
    The schema for web component deployment descriptors is provided in
    Chapter 14 of the Java Servlet 3.1 specification (JSR 340), which
    can be downloaded from `http://jcp.org/en/jsr/detail?id=340`.

  - Enterprise JavaBeans components may use an EJB deployment descriptor
    named `META-INF/ejb-jar.xml`, contained in the EJB JAR file.
    
    The schema for enterprise bean deployment descriptors is provided in
    Chapter 14 of the EJB 3.2 Core Contracts and Requirements
    Specification (JSR 345), which can be downloaded from
    `http://jcp.org/en/jsr/detail?id=345`.

## 47.3.3 Using Programmatic Security

Programmatic security is embedded in an application and is used to make
security decisions. Programmatic security is useful when declarative
security alone is not sufficient to express the security model of an
application. The API for programmatic security consists of methods of
the `EJBContext` interface and the `HttpServletRequest` interface. These
methods allow components to make business-logic decisions based on the
security role of the caller or remote user.

Programmatic security is discussed in more detail in the following
sections:

  - [Using Programmatic Security with Web
    Applications](security-webtier003.htm#GJIIE)

  - [Securing an Enterprise Bean
    Programmatically](security-javaee002.htm#GJGCS)

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
<td><a href="security-intro002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-intro004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
