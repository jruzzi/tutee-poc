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
<td><a href="jsf-intro009.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 8 Introduction to Facelets

The term Facelets refers to the view declaration language for JavaServer
Faces technology. Facelets is a part of the JavaServer Faces
specification and also the preferred presentation technology for
building JavaServer Faces technology–based applications. JavaServer
Pages (JSP) technology, previously used as the presentation technology
for JavaServer Faces, does not support all the new features available in
JavaServer Faces in the Java EE 7 platform. JSP technology is considered
to be a deprecated presentation technology for JavaServer Faces.

The following topics are addressed here:

  - [What Is Facelets?](jsf-facelets001.htm#GIJTU)

  - [The Lifecycle of a Facelets Application](jsf-facelets002.htm#GIPRR)

  - [Developing a Simple Facelets Application: The guessnumber-jsf
    Example Application](jsf-facelets003.htm#GIPOB)

  - [Using Facelets Templates](jsf-facelets004.htm#GIQXP)

  - [Composite Components](jsf-facelets005.htm#GIQZR)

  - [Web Resources](jsf-facelets006.htm#GIRGM)

  - [Relocatable Resources](jsf-facelets007.htm#BABHGBJI)

  - [Resource Library Contracts](jsf-facelets008.htm#BABHAHDF)

  - [HTML5-Friendly Markup](jsf-facelets009.htm#BABGECCJ)

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
<td><a href="jsf-intro009.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
