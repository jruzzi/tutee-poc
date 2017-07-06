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
<td><a href="jsf-page.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-page002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 10.1 Setting Up a Page

A typical JavaServer Faces web page includes the following elements:

  - A set of namespace declarations that declare the JavaServer Faces
    tag libraries

  - Optionally, the HTML head (`h:head`) and body (`h:body`) tags

  - A form tag (`h:form`) that represents the user input components

To add the JavaServer Faces components to your web page, you need to
provide the page access to the two standard tag libraries: the
JavaServer Faces HTML render kit tag library and the JavaServer Faces
core tag library. The [JavaServer Faces standard HTML tag
library](olink:JSFRK) defines tags that represent common HTML user
interface components. The JavaServer Faces core tag library defines tags
that perform core actions and are independent of a particular render
kit.

For a complete list of JavaServer Faces Facelets tags and their
attributes, refer to the [JavaServer Faces Facelets Tag Library
documentation](olink:JSFTL).

To use any of the JavaServer Faces tags, you need to include appropriate
directives at the top of each page specifying the tag libraries.

For Facelets applications, the XML namespace directives uniquely
identify the tag library URI and the tag prefix.

For example, when you create a Facelets XHTML page, include namespace
directives as follows:

``` oac_no_warn
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:h="http://xmlns.jcp.org/jsf/html"
      xmlns:f="http://xmlns.jcp.org/jsf/core">
```

The XML namespace URI identifies the tag library location, and the
prefix value is used to distinguish the tags belonging to that specific
tag library. You can also use other prefixes instead of the standard `h`
or `f`. However, when including the tag in the page you must use the
prefix that you have chosen for the tag library. For example, in the
following web page the `form` tag must be referenced using the `h`
prefix because the preceding tag library directive uses the `h` prefix
to distinguish the tags defined in the HTML tag library:

``` oac_no_warn
<h:form ...>
```

The sections [Adding Components to a Page Using HTML Tag Library
Tags](jsf-page002.htm#BNARF) and [Using Core
Tags](jsf-page003.htm#BNARC) describe how to use the component tags from
the JavaServer Faces standard HTML tag library and the core tags from
the JavaServer Faces core tag library.

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
<td><a href="jsf-page.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-page002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
