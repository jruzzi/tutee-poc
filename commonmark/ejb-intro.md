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
<td><a href="partentbeans.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-intro001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 32 Enterprise Beans

Enterprise beans are Java EE components that implement Enterprise
JavaBeans (EJB) technology. Enterprise beans run in the EJB container, a
runtime environment within GlassFish Server (see [Container
Types](overview005.htm#BNABQ)). Although transparent to the application
developer, the EJB container provides system-level services, such as
transactions and security, to its enterprise beans. These services
enable you to quickly build and deploy enterprise beans, which form the
core of transactional Java EE applications.

The following topics are addressed here:

  - [What Is an Enterprise Bean?](ejb-intro001.htm#GIPMB)

  - [What Is a Session Bean?](ejb-intro002.htm#GIPJG)

  - [What Is a Message-Driven Bean?](ejb-intro003.htm#GIPKO)

  - [Accessing Enterprise Beans](ejb-intro004.htm#GIPJF)

  - [The Contents of an Enterprise Bean](ejb-intro005.htm#GIPIO)

  - [Naming Conventions for Enterprise Beans](ejb-intro006.htm#GIPKS)

  - [The Lifecycles of Enterprise Beans](ejb-intro007.htm#GIPLJ)

  - [Further Information about Enterprise Beans](ejb-intro008.htm#GIPLG)

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
<td><a href="partentbeans.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-intro001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
