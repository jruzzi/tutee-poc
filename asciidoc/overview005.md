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
<td align="center"><a href="overview004.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a>&nbsp;</td>
<td align="center"><a href="overview006.md"><img src="img/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td>&nbsp;</td>
</tr>
</table>
++++

[[BNABO]]

[[JEETT00309]]
[[java-ee-containers]]
1.5 Java EE Containers
----------------------

Normally, thin-client multitiered applications are hard to write because
they involve many lines of intricate code to handle transaction and
state management, multithreading, resource pooling, and other complex
low-level details. The component-based and platform-independent Java EE
architecture makes applications easy to write because business logic is
organized into reusable components. In addition, the Java EE server
provides underlying services in the form of a container for every
component type. Because you do not have to develop these services
yourself, you are free to concentrate on solving the business problem at
hand.

[[BNABP]]

[[JEETT00849]]
[[container-services]]
1.5.1 Container Services
~~~~~~~~~~~~~~~~~~~~~~~~

Containers are the interface between a component and the low-level,
platform-specific functionality that supports the component. Before it
can be executed, a web, enterprise bean, or application client component
must be assembled into a Java EE module and deployed into its container.

The assembly process involves specifying container settings for each
component in the Java EE application and for the Java EE application
itself. Container settings customize the underlying support provided by
the Java EE server, including such services as security, transaction
management, Java Naming and Directory Interface (JNDI) API lookups, and
remote connectivity. Here are some of the highlights.

* The Java EE security model lets you configure a web component or
enterprise bean so that system resources are accessed only by authorized
users.
* The Java EE transaction model lets you specify relationships among
methods that make up a single transaction so that all methods in one
transaction are treated as a single unit.
* JNDI lookup services provide a unified interface to multiple naming
and directory services in the enterprise so that application components
can access these services.
* The Java EE remote connectivity model manages low-level communications
between clients and enterprise beans. After an enterprise bean is
created, a client invokes methods on it as if it were in the same
virtual machine.

Because the Java EE architecture provides configurable services,
components within the same application can behave differently based on
where they are deployed. For example, an enterprise bean can have
security settings that allow it a certain level of access to database
data in one production environment and another level of database access
in another production environment.

The container also manages nonconfigurable services, such as enterprise
bean and servlet lifecycles, database connection resource pooling, data
persistence, and access to the Java EE platform APIs (see
link:overview008.md#BNACJ[Java EE 7 APIs]).

[[BNABQ]]

[[JEETT00850]]
[[container-types]]
1.5.2 Container Types
~~~~~~~~~~~~~~~~~~~~~

The deployment process installs Java EE application components in the
Java EE containers, as illustrated in link:#BNABR[Figure 1-5].

[[JEETT00005]]
[[BNABR]]

Figure 1-5 Java EE Server and Containers

image:img/jeett_dt_005.png[Description of Figure 1-5 follows] +
link:img_text/jeett_dt_005.md[Description of "Figure 1-5 Java EE Server
and Containers"] +
 +

The server and containers are as follows:

* Java EE server: The runtime portion of a Java EE product. A Java EE
server provides EJB and web containers.
* EJB container: Manages the execution of enterprise beans for Java EE
applications. Enterprise beans and their container run on the Java EE
server.
* Web container: Manages the execution of web pages, servlets, and some
EJB components for Java EE applications. Web components and their
container run on the Java EE server.
* Application client container: Manages the execution of application
client components. Application clients and their container run on the
client.
* Applet container: Manages the execution of applets. Consists of a web
browser and a Java Plug-in running on the client together.

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
<td align="center"><a href="overview004.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a>&nbsp;</td>
<td align="center"><a href="overview006.md"><img src="img/rightnav.gif" alt="Next" /><br />
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