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
<td><a href="jaxrs-client003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 31 JAX-RS: Advanced Topics and an Example

The Java API for RESTful Web Services (JAX-RS, defined in JSR 339) is
designed to make it easy to develop applications that use the REST
architecture. This chapter describes advanced features of JAX-RS. If you
are new to JAX-RS, see [Chapter 29, "Building RESTful Web Services with
JAX-RS"](jaxrs.htm#GIEPU) before you proceed with this chapter.

JAX-RS is integrated with Contexts and Dependency Injection for Java EE
(CDI), Enterprise JavaBeans (EJB) technology, and Java Servlet
technology.

The following topics are addressed here:

  - [Annotations for Field and Bean Properties of Resource
    Classes](jaxrs-advanced001.htm#GKKRB)

  - [Validating Resource Data with Bean
    Validation](jaxrs-advanced002.htm#BABCJEDF)

  - [Subresources and Runtime Resource
    Resolution](jaxrs-advanced003.htm#GKNAV)

  - [Integrating JAX-RS with EJB Technology and
    CDI](jaxrs-advanced004.htm#GKNCY)

  - [Conditional HTTP Requests](jaxrs-advanced005.htm#GKQDA)

  - [Runtime Content Negotiation](jaxrs-advanced006.htm#GKQBQ)

  - [Using JAX-RS with JAXB](jaxrs-advanced007.htm#GKKNJ)

  - [The customer Example Application](jaxrs-advanced008.htm#GKOIB)

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
<td><a href="jaxrs-client003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
