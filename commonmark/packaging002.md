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
<td><a href="packaging001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="packaging003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 5.2 Packaging Enterprise Beans

This section explains how enterprise beans can be packaged in EJB JAR or
WAR modules. It includes the following sections:

  - [Section 5.2.1, "Packaging Enterprise Beans in EJB JAR
    Modules"](#CHDFCDBG)

  - [Section 5.2.2, "Packaging Enterprise Beans in WAR
    Modules"](#CHDJABEJ)

## 5.2.1 Packaging Enterprise Beans in EJB JAR Modules

An EJB JAR file is portable and can be used for various applications.

To assemble a Java EE application, package one or more modules, such as
EJB JAR files, into an EAR file, the archive file that holds the
application. When deploying the EAR file that contains the enterprise
bean's EJB JAR file, you also deploy the enterprise bean to GlassFish
Server. You can also deploy an EJB JAR that is not contained in an EAR
file. [Figure 5-2](#BCGFJIJI) shows the contents of an EJB JAR file.

Figure 5-2 Structure of an Enterprise Bean JAR

![Description of Figure 5-2 follows](img/jeett_dt_011.png)  
[Description of "Figure 5-2 Structure of an Enterprise Bean
JAR"](img_text/jeett_dt_011.htm)  
  

## 5.2.2 Packaging Enterprise Beans in WAR Modules

Enterprise beans often provide the business logic of a web application.
In these cases, packaging the enterprise bean within the web
application's WAR module simplifies deployment and application
organization. Enterprise beans may be packaged within a WAR module as
Java programming language class files or within a JAR file that is
bundled within the WAR module.

To include enterprise bean class files in a WAR module, the class files
should be in the `WEB-INF/classes` directory.

To include a JAR file that contains enterprise beans in a WAR module,
add the JAR to the `WEB-INF/lib` directory of the WAR module.

WAR modules that contain enterprise beans do not require an
`ejb-jar.xml` deployment descriptor. If the application uses
`ejb-jar.xml`, it must be located in the WAR module's `WEB-INF`
directory.

JAR files that contain enterprise bean classes packaged within a WAR
module are not considered EJB JAR files, even if the bundled JAR file
conforms to the format of an EJB JAR file. The enterprise beans
contained within the JAR file are semantically equivalent to enterprise
beans located in the WAR module's `WEB-INF/classes` directory, and the
environment namespace of all the enterprise beans are scoped to the WAR
module.

For example, suppose that a web application consists of a shopping cart
enterprise bean, a credit card–processing enterprise bean, and a Java
servlet front end. The shopping cart bean exposes a local, no-interface
view and is defined as follows:

``` oac_no_warn
package com.example.cart;

@Stateless
public class CartBean { ... }
```

The credit card–processing bean is packaged within its own JAR file,
`cc.jar`, exposes a local, no-interface view, and is defined as follows:

``` oac_no_warn
package com.example.cc;

@Stateless
public class CreditCardBean { ... }
```

The servlet, `com.example.web.StoreServlet`, handles the web front end
and uses both `CartBean` and `CreditCardBean`. The WAR module layout for
this application is as follows:

``` oac_no_warn
WEB-INF/classes/com/example/cart/CartBean.class
WEB-INF/classes/com/example/web/StoreServlet
WEB-INF/lib/cc.jar
WEB-INF/ejb-jar.xml
WEB-INF/web.xml
```

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
<td><a href="packaging001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="packaging003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
