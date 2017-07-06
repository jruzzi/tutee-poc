++++
<table cellspacing="0" cellpadding="0" width="100%">
<tr>
<td align="left" valign="top"><b>Java Platform, Enterprise Edition The Java EE Tutorial</b><br />
<b>Release 7 Java Platform, Enterprise Edition</b><br />
E39031-02</td>
<td valign="bottom" align="right">
<table cellspacing="0" cellpadding="0" width="225">
<tr>
<td>&nbsp;</td>
<td align="center" valign="top"><a href="toc.md"><img src="img/toc.gif" alt="Go To Table Of Contents" /><br />
<span class="icon">Contents</span></a></td>
</tr>
</table>
</td>
</tr>
</table>
<hr />
<table cellspacing="0" cellpadding="0" width="100">
<tr>
<td align="center"><a href="overview008.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a>&nbsp;</td>
<td align="center"><a href="overview010.md"><img src="img/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td>&nbsp;</td>
</tr>
</table>
++++

[[GIRDR]]

[[JEETT00315]]
[[java-ee-7-apis-in-the-java-platform-standard-edition-7]]
1.9 Java EE 7 APIs in the Java Platform, Standard Edition 7
-----------------------------------------------------------

Several APIs that are required by the Java EE 7 platform are included in
the Java Platform, Standard Edition 7 (Java SE 7) and are thus available
to Java EE applications.

[[BNADA]]

[[JEETT00876]]
[[java-database-connectivity-api]]
1.9.1 Java Database Connectivity API
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Java Database Connectivity (JDBC) API lets you invoke SQL commands
from Java programming language methods. You use the JDBC API in an
enterprise bean when you have a session bean access the database. You
can also use the JDBC API from a servlet or a JSP page to access the
database directly without going through an enterprise bean.

The JDBC API has two parts:

* An application-level interface used by the application components to
access a database
* A service provider interface to attach a JDBC driver to the Java EE
platform

The Java SE 7 platform requires JDBC 4.1.

[[BNADC]]

[[JEETT00877]]
[[java-naming-and-directory-interface-api]]
1.9.2 Java Naming and Directory Interface API
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Java Naming and Directory Interface (JNDI) API provides naming and
directory functionality, enabling applications to access multiple naming
and directory services, such as LDAP, DNS, and NIS. The JNDI API
provides applications with methods for performing standard directory
operations, such as associating attributes with objects and searching
for objects using their attributes. Using JNDI, a Java EE application
can store and retrieve any type of named Java object, allowing Java EE
applications to coexist with many legacy applications and systems.

Java EE naming services provide application clients, enterprise beans,
and web components with access to a JNDI naming environment. A naming
environment allows a component to be customized without the need to
access or change the component's source code. A container implements the
component's environment and provides it to the component as a JNDI
naming context.

The naming environment provides four logical namespaces: `java:comp`,
`java:module`, `java:app`, and `java:global` for objects available to
components, modules, or applications or shared by all deployed
applications. A Java EE component can access named system-provided and
user-defined objects. The names of some system-provided objects, such as
a default JDBC `DataSource` object, a default JMS connection factory,
and a JTA `UserTransaction` object, are stored in the `java:comp`
namespace. The Java EE platform allows a component to name user-defined
objects, such as enterprise beans, environment entries, JDBC
`DataSource` objects, and messaging destinations.

A Java EE component can also locate its environment naming context by
using JNDI interfaces. A component can create a
`javax.naming.InitialContext` object and look up the environment naming
context in `InitialContext` under the name `java:comp/env`. A
component's naming environment is stored directly in the environment
naming context or in any of its direct or indirect subcontexts.

[[BNACT]]

[[JEETT00878]]
[[javabeans-activation-framework]]
1.9.3 JavaBeans Activation Framework
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The JavaBeans Activation Framework (JAF) is used by the JavaMail API.
JAF provides standard services to determine the type of an arbitrary
piece of data, encapsulate access to it, discover the operations
available on it, and create the appropriate JavaBeans component to
perform those operations.

[[BNACU]]

[[JEETT00879]]
[[java-api-for-xml-processing]]
1.9.4 Java API for XML Processing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Java API for XML Processing (JAXP), part of the Java SE platform,
supports the processing of XML documents using Document Object Model
(DOM), Simple API for XML (SAX), and Extensible Stylesheet Language
Transformations (XSLT). JAXP enables applications to parse and transform
XML documents independently of a particular XML-processing
implementation.

JAXP also provides namespace support, which lets you work with schemas
that might otherwise have naming conflicts. Designed to be flexible,
JAXP lets you use any XML-compliant parser or XSL processor from within
your application and supports the Worldwide Web Consortium (W3C) schema.
You can find information on the W3C schema at
`http://www.w3.org/XML/Schema`.

[[BNACW]]

[[JEETT00880]]
[[java-architecture-for-xml-binding]]
1.9.5 Java Architecture for XML Binding
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Java Architecture for XML Binding (JAXB) provides a convenient way
to bind an XML schema to a representation in Java language programs.
JAXB can be used independently or in combination with JAX-WS, in which
case it provides a standard data binding for web service messages. All
Java EE application client containers, web containers, and EJB
containers support the JAXB API.

The Java EE 7 platform requires JAXB 2.2.

[[BNACV]]

[[JEETT00882]]
[[java-api-for-xml-web-services]]
1.9.6 Java API for XML Web Services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Java API for XML Web Services (JAX-WS) specification provides
support for web services that use the JAXB API for binding XML data to
Java objects. The JAX-WS specification defines client APIs for accessing
web services as well as techniques for implementing web service
endpoints. The Implementing Enterprise Web Services specification
describes the deployment of JAX-WS-based services and clients. The EJB
and Java Servlet specifications also describe aspects of such
deployment. JAX-WS-based applications can be deployed using any of these
deployment models.

The JAX-WS specification describes the support for message handlers that
can process message requests and responses. In general, these message
handlers execute in the same container and with the same privileges and
execution context as the JAX-WS client or endpoint component with which
they are associated. These message handlers have access to the same JNDI
namespace as their associated component. Custom serializers and
deserializers, if supported, are treated in the same way as message
handlers.

The Java EE 7 platform requires JAX-WS 2.2.

[[BNACX]]

[[JEETT00881]]
[[soap-with-attachments-api-for-java]]
1.9.7 SOAP with Attachments API for Java
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The SOAP with Attachments API for Java (SAAJ) is a low-level API on
which JAX-WS depends. SAAJ enables the production and consumption of
messages that conform to the SOAP 1.1 and 1.2 specifications and the
SOAP with Attachments note. Most developers do not use the SAAJ API,
instead using the higher-level JAX-WS API.

[[BNADD]]

[[JEETT00883]]
[[java-authentication-and-authorization-service]]
1.9.8 Java Authentication and Authorization Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Java Authentication and Authorization Service (JAAS) provides a way
for a Java EE application to authenticate and authorize a specific user
or group of users to run it.

JAAS is a Java programming language version of the standard Pluggable
Authentication Module (PAM) framework, which extends the Java platform
security architecture to support user-based authorization.

[[JEETT1345]]
[[sthref12]]

[[common-annotations-for-the-java-platform]]
1.9.9 Common Annotations for the Java Platform
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Annotations enable a declarative style of programming in the Java
platform.

The Java EE 7 platform requires Common Annotations for the Java Platform
1.2.

++++
<hr />
<table cellspacing="0" cellpadding="0" width="100%">
<col width="33%" />
<col width="*" />
<col width="33%" />
<tr>
<td valign="bottom">
<table cellspacing="0" cellpadding="0" width="100">
<col width="*" />
<col width="48%" />
<col width="48%" />
<tr>
<td>&nbsp;</td>
<td align="center"><a href="overview008.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a>&nbsp;</td>
<td align="center"><a href="overview010.md"><img src="img/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
</tr>
</table>
</td>
<td><img src="img/oracle.gif" alt="Oracle Logo" /> <a href="img/cpyr.md"><br />
<span>Copyright&nbsp;&copy;&nbsp;2014,&nbsp;Oracle&nbsp;and/or&nbsp;its&nbsp;affiliates.&nbsp;All&nbsp;rights&nbsp;reserved.</a><br>
ORACLE&nbsp;CONFIDENTIAL.&nbsp;For&nbsp;authorized&nbsp;use&nbsp;only.&nbsp;Do&nbsp;not&nbsp;distribute&nbsp;to&nbsp;third&nbsp;parties.</span></td>
<td valign="bottom" align="right">
<table cellspacing="0" cellpadding="0" width="225">
<tr>
<td>&nbsp;</td>
<td align="center" valign="top"><a href="toc.md"><img src="img/toc.gif" alt="Go To Table Of Contents" /><br />
<span>Contents</span></a></td>
</tr>
</table>
</td>
</tr>
</table>
<p align="center"></p>
++++