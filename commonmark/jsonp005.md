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
<td><a href="jsonp004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsonp006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 19.5 JSON in Java EE RESTful Web Services

This section explains how the Java API for JSON Processing is related to
other Java EE packages that provide JSON support for RESTful web
services. See [Chapter 29, "Building RESTful Web Services with
JAX-RS,"](jaxrs.htm#GIEPU) for more information on RESTful web services.

Jersey, the reference implementation for JAX-RS (JSR 311) included in
GlassFish Server, provides support for binding JSON data from RESTful
resource methods to Java objects using JAXB, as described in [Using
JAX-RS with JAXB](jaxrs-advanced007.htm#GKKNJ) in [Chapter 31, "JAX-RS:
Advanced Topics and an Example"](jaxrs-advanced.htm#GJJXE). However,
JSON support is not part of JAX-RS (JSR 311) or JAXB (JSR 222), so that
procedure may not work for Java EE implementations other than GlassFish
Server.

The Java API for JSON Processing (JSR 353) does not explicitly support
JSON binding in Java. A future JSR (JSON Binding) that is similar to
JAXB for XML is under consideration for a future release of Java EE.

You can still use the Java API for JSON Processing with JAX-RS resource
methods. For more information, see the sample code for JSON Processing
included with the Java EE 7 SDK.

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
<td><a href="jsonp004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsonp006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
