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
<td><a href="overview.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="overview002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 1.1 Introduction to Java EE

Developers today increasingly recognize the need for distributed,
transactional, and portable applications that leverage the speed,
security, and reliability of server-side technology. Enterprise
applications provide the business logic for an enterprise. They are
centrally managed and often interact with other enterprise software. In
the world of information technology, enterprise applications must be
designed, built, and produced for less money, with greater speed, and
with fewer resources.

With the Java Platform, Enterprise Edition (Java EE), development of
Java enterprise applications has never been easier or faster. The aim of
the Java EE platform is to provide developers with a powerful set of
APIs while shortening development time, reducing application complexity,
and improving application performance.

The Java EE platform is developed through the Java Community Process
(JCP), which is responsible for all Java technologies. Expert groups
composed of interested parties have created Java Specification Requests
(JSRs) to define the various Java EE technologies. The work of the Java
Community under the JCP program helps to ensure Java technology's
standards of stability and cross-platform compatibility.

The Java EE platform uses a simplified programming model. XML deployment
descriptors are optional. Instead, a developer can simply enter the
information as an annotation directly into a Java source file, and the
Java EE server will configure the component at deployment and runtime.
These annotations are generally used to embed in a program data that
would otherwise be furnished in a deployment descriptor. With
annotations, you put the specification information in your code next to
the program element affected.

In the Java EE platform, dependency injection can be applied to all
resources a component needs, effectively hiding the creation and lookup
of resources from application code. Dependency injection can be used in
Enterprise JavaBeans (EJB) containers, web containers, and application
clients. Dependency injection allows the Java EE container to
automatically insert references to other required components or
resources, using annotations.

This tutorial uses examples to describe the features available in the
Java EE platform for developing enterprise applications. Whether you are
a new or experienced enterprise developer, you should find the examples
and accompanying text a valuable and accessible knowledge base for
creating your own solutions.

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
<td><a href="overview.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="overview002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
