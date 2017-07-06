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
<td><a href="overview009.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="usingexamples.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 1.10 GlassFish Server Tools

GlassFish Server is a compliant implementation of the Java EE 7
platform. In addition to supporting all the APIs described in the
previous sections, GlassFish Server includes a number of Java EE tools
that are not part of the Java EE 7 platform but are provided as a
convenience to the developer.

This section briefly summarizes the tools that make up GlassFish Server.
Instructions for starting and stopping GlassFish Server, starting the
Administration Console, and starting and stopping the Java DB server are
in [Chapter 2, "Using the Tutorial Examples"](usingexamples.htm#GFIUD).

GlassFish Server contains the tools listed in [Table 1-1](#BNADH). Basic
usage information for many of the tools appears throughout the tutorial.
For detailed information, see the online help in the GUI tools.

Table 1-1 GlassFish Server Tools

<table style="width:27%;">
<colgroup>
<col width="27%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tool</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administration Console</p>
<br />
</td>
<td><p>A web-based GUI GlassFish Server administration utility. Used to stop GlassFish Server and to manage users, resources, and applications.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">asadmin</code></p></td>
<td><p>A command-line GlassFish Server administration utility. Used to start and stop GlassFish Server and to manage users, resources, and applications.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">appclient</code></p></td>
<td><p>A command-line tool that launches the application client container and invokes the client application packaged in the application client JAR file.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">capture-schema</code></p></td>
<td><p>A command-line tool to extract schema information from a database, producing a schema file that GlassFish Server can use for container-managed persistence.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">package-appclient</code></p></td>
<td><p>A command-line tool to package the application client container libraries and JAR files.</p></td>
</tr>
<tr class="even">
<td><p>Java DB database</p></td>
<td><p>A copy of the Java DB server.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xjc</code></p></td>
<td><p>A command-line tool to transform, or bind, a source XML schema to a set of JAXB content classes in the Java programming language.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">schemagen</code></p></td>
<td><p>A command-line tool to create a schema file for each namespace referenced in your Java classes.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">wsimport</code></p></td>
<td><p>A command-line tool to generate JAX-WS portable artifacts for a given WSDL file. After generation, these artifacts can be packaged in a WAR file with the WSDL and schema documents, along with the endpoint implementation, and then deployed.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">wsgen</code></p></td>
<td><p>A command-line tool to read a web service endpoint class and generate all the required JAX-WS portable artifacts for web service deployment and invocation.</p></td>
</tr>
</tbody>
</table>

  

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
<td><a href="overview009.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="usingexamples.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
