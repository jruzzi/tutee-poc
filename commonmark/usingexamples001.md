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
<td><a href="usingexamples.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="usingexamples002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 2.1 Required Software

The following software is required to run the examples:

  - [Java Platform, Standard Edition](#GEXAE)

  - [Java EE 7 Software Development Kit](#GEXAB)

  - [Java EE 7 Tutorial Component](#GEXBA)

  - [NetBeans IDE](#GEXAZ)

  - [Apache Maven](#GEXAA)

## 2.1.1 Java Platform, Standard Edition

To build, deploy, and run the examples, you need a copy of the Java
Platform, Standard Edition Development Kit (JDK). You must use JDK 7
Update 65 or above or JDK 8 Update 20 or above. You can download JDK
software from
`http://www.oracle.com/technetwork/java/javase/downloads/index.html`.

## 2.1.2 Java EE 7 Software Development Kit

GlassFish Server Open Source Edition 4.1 is targeted as the build and
runtime environment for the tutorial examples. To build, deploy, and run
the examples, you need a copy of GlassFish Server and, optionally,
NetBeans IDE. To obtain GlassFish Server, you must install the Java EE 7
Software Development Kit (SDK) Update 1, which you can download from
`http://www.oracle.com/technetwork/java/javaee/downloads/index.html`.
Make sure that you download the Java EE 7 SDK Update 1, not the Java EE
7 Web Profile SDK Update 1.

### 2.1.2.1 SDK Installation Tips

The Java EE 7 SDK Update 1 is installed from a ZIP file. It sets the
default administration user name as `admin` with no required password.
The Admin Port is set to 4848, and the HTTP Port is set to 8080.

This tutorial refers to as-install-parent, the directory where you
install GlassFish Server. For example, the default installation
directory on Microsoft Windows is `C:\glassfish4`, so as-install-parent
is `C:\glassfish4`. GlassFish Server itself is installed in as-install,
the `glassfish` directory under as-install-parent. So on Microsoft
Windows, as-install is `C:\glassfish4\glassfish`.

After you install GlassFish Server, add the following directories to
your `PATH` to avoid having to specify the full path when you use
commands:

``` oac_no_warn
as-install-parent/bin
as-install/bin
```

## 2.1.3 Java EE 7 Tutorial Component

The tutorial component, including the documentation and example source,
is contained in the Java EE 7 SDK Update 1.

Updates to the Java EE 7 Tutorial are published periodically. For
details on obtaining these updates, see [Getting the Latest Updates to
the Tutorial](usingexamples008.htm#GIQWR).

## 2.1.4 NetBeans IDE

The NetBeans integrated development environment (IDE) is a free,
open-source IDE for developing Java applications, including enterprise
applications. NetBeans IDE supports the Java EE platform. You can build,
package, deploy, and run the tutorial examples from within NetBeans IDE.

To run the tutorial examples, you need the latest version of NetBeans
IDE. You can download NetBeans IDE from
`https://netbeans.org/downloads/index.html`. Make sure that you download
the Java EE bundle.

### 2.1.4.1 To Install NetBeans IDE without GlassFish Server

When you install NetBeans IDE, do not install the version of GlassFish
Server that comes with NetBeans IDE. To skip the installation of
GlassFish Server, follow these steps.

1.  On the first page of the NetBeans IDE Installer wizard, deselect the
    check box for GlassFish Server and click OK.

2.  Accept both the License Agreement and the Junit License Agreement.
    
    A few of the tutorial examples use the Junit library, so you should
    install it.

3.  Continue with the installation of NetBeans IDE.

### 2.1.4.2 To Add GlassFish Server as a Server Using NetBeans IDE

To run the tutorial examples in NetBeans IDE, you must add your
GlassFish Server as a server in NetBeans IDE. Follow these instructions
to add GlassFish Server to NetBeans IDE.

1.  From the Tools menu, choose Servers.

2.  In the Servers wizard, click Add Server.

3.  Under Choose Server, select GlassFish Server and click Next.

4.  Under Server Location, browse to the location of the Java EE 7 SDK
    and click Next.

5.  Under Domain Location, select Register Local Domain.

6.  Click Finish.

## 2.1.5 Apache Maven

Maven is a Java technology–based build tool developed by the Apache
Software Foundation and is used to build, package, and deploy the
tutorial examples. To run the tutorial examples from the command line,
you need Maven 3.0 or higher. If you do not already have Maven, you can
install it from:

`http://maven.apache.org`

Be sure to add the maven-install`/bin` directory to your path.

If you are using NetBeans IDE to build and run the examples, it includes
a copy of Maven.

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
<td><a href="usingexamples.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="usingexamples002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
