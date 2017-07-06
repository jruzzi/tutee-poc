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
<td><a href="partcdi.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basic001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 23 Introduction to Contexts and Dependency Injection for Java EE

This chapter describes Contexts and Dependency Injection for Java EE
(CDI) which is one of several Java EE features that help to knit
together the web tier and the transactional tier of the Java EE
platform.

The following topics are addressed here:

  - [Getting Started](cdi-basic001.htm#BABJDJGA)

  - [Overview of CDI](cdi-basic002.htm#GIWHL)

  - [About Beans](cdi-basic003.htm#GJEBJ)

  - [About CDI Managed Beans](cdi-basic004.htm#GJFZI)

  - [Beans as Injectable Objects](cdi-basic005.htm#GIZKS)

  - [Using Qualifiers](cdi-basic006.htm#GJBCK)

  - [Injecting Beans](cdi-basic007.htm#GJBAN)

  - [Using Scopes](cdi-basic008.htm#GJBBK)

  - [Giving Beans EL Names](cdi-basic009.htm#GJBAK)

  - [Adding Setter and Getter Methods](cdi-basic010.htm#GJBBP)

  - [Using a Managed Bean in a Facelets Page](cdi-basic011.htm#GJBBU)

  - [Injecting Objects by Using Producer
    Methods](cdi-basic012.htm#GJDID)

  - [Configuring a CDI Application](cdi-basic013.htm#GJBNZ)

  - [Using the @PostConstruct and @PreDestroy Annotations with CDI
    Managed Bean Classes](cdi-basic014.htm#BABJFEAI)

  - [Further Information about CDI](cdi-basic015.htm#GIWEL)

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
<td><a href="partcdi.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basic001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
