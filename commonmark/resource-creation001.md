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
<td><a href="resource-creation.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="resource-creation002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 3.1 Resources and JNDI Naming

In a distributed application, components need to access other components
and resources, such as databases. For example, a servlet might invoke
remote methods on an enterprise bean that retrieves information from a
database. In the Java EE platform, the Java Naming and Directory
Interface (JNDI) naming service enables components to locate other
components and resources.

A resource is a program object that provides connections to systems,
such as database servers and messaging systems. (A Java Database
Connectivity resource is sometimes referred to as a data source.) Each
resource object is identified by a unique, people-friendly name, called
the JNDI name. For example, the JNDI name of the preconfigured JDBC
resource for the Java DB database that is shipped with GlassFish Server
is `java:comp/DefaultDataSource`.

An administrator creates resources in a JNDI namespace. In GlassFish
Server, you can use either the Administration Console or the `asadmin`
command to create resources. Applications then use annotations to inject
the resources. If an application uses resource injection, GlassFish
Server invokes the JNDI API, and the application is not required to do
so. However, it is also possible for an application to locate resources
by making direct calls to the JNDI API.

A resource object and its JNDI name are bound together by the naming and
directory service. To create a new resource, a new name/object binding
is entered into the JNDI namespace. You inject resources by using the
`@Resource` annotation in an application.

You can use a deployment descriptor to override the resource mapping
that you specify in an annotation. Using a deployment descriptor allows
you to change an application by repackaging it rather than by both
recompiling the source files and repackaging. However, for most
applications a deployment descriptor is not necessary.

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
<td><a href="resource-creation.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="resource-creation002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
