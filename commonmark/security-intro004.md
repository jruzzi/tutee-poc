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
<td><a href="security-intro003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-intro005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 47.4 Securing GlassFish Server

This tutorial describes deployment to GlassFish Server, which provides
highly secure, interoperable, and distributed component computing based
on the Java EE security model. GlassFish Server supports the Java EE 7
security model. You can configure GlassFish Server for the following
purposes.

  - Adding, deleting, or modifying authorized users. For more
    information on this topic, see [Working with Realms, Users, Groups,
    and Roles](security-intro005.htm#BNBXJ).

  - Configuring secure HTTP and Internet Inter-Orb Protocol (IIOP)
    listeners.

  - Configuring secure Java Management Extensions (JMX) connectors.

  - Adding, deleting, or modifying existing or custom realms.

  - Defining an interface for pluggable authorization providers using
    Java Authorization Contract for Containers (JACC). JACC defines
    security contracts between GlassFish Server and authorization policy
    modules. These contracts specify how the authorization providers are
    installed, configured, and used in access decisions.

  - Using pluggable audit modules.

  - Customizing authentication mechanisms. All implementations of Java
    EE 7 compatible web containers are required to support the Servlet
    Profile of JSR 196, which offers an avenue for customizing the
    authentication mechanism applied by the web container on behalf of
    one or more applications.

  - Setting and changing policy permissions for an application.

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
<td><a href="security-intro003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-intro005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
