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
<td align="center"><a href="overview009.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a>&nbsp;</td>
<td align="center"><a href="usingexamples.md"><img src="img/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td>&nbsp;</td>
</tr>
</table>
++++

[[BNADF]]

[[JEETT00316]]
[[glassfish-server-tools]]
1.10 GlassFish Server Tools
---------------------------

GlassFish Server is a compliant implementation of the Java EE 7
platform. In addition to supporting all the APIs described in the
previous sections, GlassFish Server includes a number of Java EE tools
that are not part of the Java EE 7 platform but are provided as a
convenience to the developer.

This section briefly summarizes the tools that make up GlassFish Server.
Instructions for starting and stopping GlassFish Server, starting the
Administration Console, and starting and stopping the Java DB server are
in link:usingexamples.md#GFIUD[Chapter 2, "Using the Tutorial
Examples"].

GlassFish Server contains the tools listed in link:#BNADH[Table 1-1].
Basic usage information for many of the tools appears throughout the
tutorial. For detailed information, see the online help in the GUI
tools.

[[JEETT1346]]
[[BNADH]]

Table 1-1 GlassFish Server Tools

[width="27%",options="header"]
|=======================================================================
|Tool |Description
|Administration Console |A web-based GUI GlassFish Server administration utility. Used to stop
GlassFish Server and to manage users, resources, and applications.

|`asadmin` |A command-line GlassFish Server administration utility. Used
to start and stop GlassFish Server and to manage users, resources, and
applications.

|`appclient` |A command-line tool that launches the application client
container and invokes the client application packaged in the application
client JAR file.

|`capture-schema` |A command-line tool to extract schema information
from a database, producing a schema file that GlassFish Server can use
for container-managed persistence.

|`package-appclient` |A command-line tool to package the application
client container libraries and JAR files.

|Java DB database |A copy of the Java DB server.

|`xjc` |A command-line tool to transform, or bind, a source XML schema
to a set of JAXB content classes in the Java programming language.

|`schemagen` |A command-line tool to create a schema file for each
namespace referenced in your Java classes.

|`wsimport` |A command-line tool to generate JAX-WS portable artifacts
for a given WSDL file. After generation, these artifacts can be packaged
in a WAR file with the WSDL and schema documents, along with the
endpoint implementation, and then deployed.

|`wsgen` |A command-line tool to read a web service endpoint class and
generate all the required JAX-WS portable artifacts for web service
deployment and invocation.
|=======================================================================

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
<td align="center"><a href="overview009.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a>&nbsp;</td>
<td align="center"><a href="usingexamples.md"><img src="img/rightnav.gif" alt="Next" /><br />
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