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
<td><a href="jsf-facelets.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 8.1 What Is Facelets?

Facelets is a powerful but lightweight page declaration language that is
used to build JavaServer Faces views using HTML style templates and to
build component trees. Facelets features include the following:

  - Use of XHTML for creating web pages

  - Support for Facelets tag libraries in addition to JavaServer Faces
    and JSTL tag libraries

  - Support for the Expression Language (EL)

  - Templating for components and pages

The advantages of Facelets for large-scale development projects include
the following:

  - Support for code reuse through templating and composite components

  - Functional extensibility of components and other server-side objects
    through customization

  - Faster compilation time

  - Compile-time EL validation

  - High-performance rendering

In short, the use of Facelets reduces the time and effort that needs to
be spent on development and deployment.

Facelets views are usually created as XHTML pages. JavaServer Faces
implementations support XHTML pages created in conformance with the
XHTML Transitional Document Type Definition (DTD), as listed at
`http://www.w3.org/TR/xhtml1/#a_dtd_XHTML-1.0-Transitional`. By
convention, web pages built with XHTML have an `.xhtml` extension.

JavaServer Faces technology supports various tag libraries to add
components to a web page. To support the JavaServer Faces tag library
mechanism, Facelets uses XML namespace declarations. [Table 8-1](#GJBOX)
lists the tag libraries supported by Facelets.

Table 8-1 Tag Libraries Supported by Facelets

<table style="width:60%;">
<colgroup>
<col width="13%" />
<col width="0%" />
<col width="12%" />
<col width="18%" />
<col width="17%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag Library</th>
<th>URI</th>
<th>Prefix</th>
<th>Example</th>
<th>Contents</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>JavaServer Faces Facelets Tag Library</p></td>
<td><p><code dir="ltr">http://xmlns.jcp.org/jsf/facelets</code></p></td>
<td><p><code dir="ltr">ui:</code></p></td>
<td><p><code dir="ltr">ui:component</code></p>
<p><code dir="ltr">ui:insert</code></p></td>
<td><p>Tags for templating</p></td>
</tr>
<tr class="even">
<td><p>JavaServer Faces HTML Tag Library</p></td>
<td><p><code dir="ltr">http://xmlns.jcp.org/jsf/html</code></p></td>
<td><p><code dir="ltr">h:</code></p></td>
<td><p><code dir="ltr">h:head</code></p>
<p><code dir="ltr">h:body</code></p>
<p><code dir="ltr">h:outputText</code></p>
<p><code dir="ltr">h:inputText</code></p></td>
<td><p>JavaServer Faces component tags for all <code dir="ltr">UIComponent</code> objects</p></td>
</tr>
<tr class="odd">
<td><p>JavaServer Faces Core Tag Library</p></td>
<td><p><code dir="ltr">http://xmlns.jcp.org/jsf/core</code></p></td>
<td><p><code dir="ltr">f:</code></p></td>
<td><p><code dir="ltr">f:actionListener</code></p>
<p><code dir="ltr">f:attribute</code></p></td>
<td><p>Tags for JavaServer Faces custom actions that are independent of any particular render kit</p></td>
</tr>
<tr class="even">
<td><p>Pass-through Elements Tag Library</p></td>
<td><p><code dir="ltr">http://xmlns.jcp.org/jsf</code></p></td>
<td><p><code dir="ltr">jsf:</code></p></td>
<td><p><code dir="ltr">jsf:id</code></p></td>
<td><p>Tags to support HTML5-friendly markup</p></td>
</tr>
<tr class="odd">
<td><p>Pass-through Attributes Tag Library</p></td>
<td><p><code dir="ltr">http://xmlns.jcp.org/jsf/passthrough</code></p></td>
<td><p><code dir="ltr">p:</code></p></td>
<td><p><code dir="ltr">p:type</code></p></td>
<td><p>Tags to support HTML5-friendly markup</p></td>
</tr>
<tr class="even">
<td><p>Composite Component Tag Library</p></td>
<td><p><code dir="ltr">http://xmlns.jcp.org/jsf/composite</code></p></td>
<td><p><code dir="ltr">cc:</code></p></td>
<td><p><code dir="ltr">cc:interface</code></p></td>
<td><p>Tags to support composite components</p></td>
</tr>
<tr class="odd">
<td><p>JSTL Core Tag Library</p></td>
<td><p><code dir="ltr">http://xmlns.jcp.org/jsp/jstl/core</code></p></td>
<td><p><code dir="ltr">c:</code></p></td>
<td><p><code dir="ltr">c:forEach</code></p>
<p><code dir="ltr">c:catch</code></p></td>
<td><p>JSTL 1.2 Core Tags</p></td>
</tr>
<tr class="even">
<td><p>JSTL Functions Tag Library</p></td>
<td><p><code dir="ltr">http://xmlns.jcp.org/jsp/jstl/functions</code></p></td>
<td><p><code dir="ltr">fn:</code></p></td>
<td><p><code dir="ltr">fn:toUpperCase</code></p>
<p><code dir="ltr">fn:toLowerCase</code></p></td>
<td><p>JSTL 1.2 Functions Tags</p></td>
</tr>
</tbody>
</table>

  

Facelets provides two namespaces to support HTML5-friendly markup. For
details, see [HTML5-Friendly Markup](jsf-facelets009.htm#BABGECCJ).

Facelets supports tags for composite components, for which you can
declare custom prefixes. For more information on composite components,
see [Composite Components](jsf-facelets005.htm#GIQZR).

The namespace prefixes shown in the table are conventional, not
mandatory. As is always the case when you declare an XML namespace, you
can specify any prefix in your Facelets page. For example, you can
declare the prefix for the composite component tag library as

``` oac_no_warn
xmlns:composite="http://java.sun.com/jsf/composite"
```

instead of as

``` oac_no_warn
xmlns:cc="http://java.sun.com/jsf/composite"
```

Based on the JavaServer Faces support for Expression Language (EL)
syntax, Facelets uses EL expressions to reference properties and methods
of managed beans. EL expressions can be used to bind component objects
or values to methods or properties of managed beans that are used as
backing beans. For more information on using EL expressions, see [Using
the EL to Reference Managed Beans](jsf-develop001.htm#BNAQP).

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
<td><a href="jsf-facelets.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
