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
<td><a href="packaging.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="packaging002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 5.1 Packaging Applications

A Java EE application is delivered in a Java Archive (JAR) file, a Web
Archive (WAR) file, or an Enterprise Archive (EAR) file. A WAR or EAR
file is a standard JAR (`.jar`) file with a `.war` or `.ear` extension.
Using JAR, WAR, and EAR files and modules makes it possible to assemble
a number of different Java EE applications using some of the same
components. No extra coding is needed; it is only a matter of assembling
(or packaging) various Java EE modules into Java EE JAR, WAR, or EAR
files.

An EAR file (see [Figure 5-1](#BCGHHIIH)) contains Java EE modules and,
optionally, deployment descriptors. A deployment descriptor, an XML
document with an `.xml` extension, describes the deployment settings of
an application, a module, or a component. Because deployment descriptor
information is declarative, it can be changed without the need to modify
the source code. At runtime, the Java EE server reads the deployment
descriptor and acts upon the application, module, or component
accordingly.

Deployment information is most commonly specified in the source code by
annotations. Deployment descriptors, if present, override what is
specified in the source code.

Figure 5-1 EAR File Structure

![Description of Figure 5-1 follows](img/jeett_dt_010.png)  
[Description of "Figure 5-1 EAR File
Structure"](img_text/jeett_dt_010.htm)  
  

The two types of deployment descriptors are Java EE and runtime. A Java
EE deployment descriptor is defined by a Java EE specification and can
be used to configure deployment settings on any Java EE-compliant
implementation. A runtime deployment descriptor is used to configure
Java EE implementation-specific parameters. For example, the GlassFish
Server runtime deployment descriptor contains such information as the
context root of a web application as well as GlassFish Server
implementation-specific parameters, such as caching directives. The
GlassFish Server runtime deployment descriptors are named
`glassfish-`moduleType`.xml` and are located in the same `META-INF`
directory as the Java EE deployment descriptor.

A Java EE module consists of one or more Java EE components for the same
container type and, optionally, one component deployment descriptor of
that type. An enterprise bean module deployment descriptor, for example,
declares transaction attributes and security authorizations for an
enterprise bean. A Java EE module can be deployed as a stand-alone
module.

Java EE modules are of the following types:

  - EJB modules, which contain class files for enterprise beans and,
    optionally, an EJB deployment descriptor. EJB modules are packaged
    as JAR files with a `.jar` extension.

  - Web modules, which contain servlet class files, web files,
    supporting class files, GIF and HTML files, and, optionally, a web
    application deployment descriptor. Web modules are packaged as JAR
    files with a `.war` (web archive) extension.

  - Application client modules, which contain class files and,
    optionally, an application client deployment descriptor. Application
    client modules are packaged as JAR files with a `.jar` extension.

  - Resource adapter modules, which contain all Java interfaces,
    classes, native libraries, and, optionally, a resource adapter
    deployment descriptor. Together, these implement the Connector
    architecture (see [Java EE Connector
    Architecture](overview008.htm#BNACZ)) for a particular EIS. Resource
    adapter modules are packaged as JAR files with an `.rar` (resource
    adapter archive) extension.

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
<td><a href="packaging.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="packaging002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
