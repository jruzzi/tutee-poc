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
<td><a href="jsf-advanced-cc.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-advanced-cc002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 14.1 Attributes of a Composite Component

A composite component is a special type of JavaServer Faces template
that acts as a component. If you are new to composite components, see
[Composite Components](jsf-facelets005.htm#GIQZR) before you proceed
with this chapter.

You define an attribute of a composite component by using the
`composite:attribute` tag. [Table 14-1](#GKHVF) lists the commonly used
attributes of this tag.

Table 14-1 Commonly Used Attributes of the composite:attribute Tag

<table style="width:26%;">
<colgroup>
<col width="26%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">name</code></p></td>
<td><p>Specifies the name of the composite component attribute to be used in the using page. Alternatively, the <code dir="ltr">name</code> attribute can specify standard event handlers such as <code dir="ltr">action</code>, <code dir="ltr">actionListener</code>, and managed bean.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">default</code></p></td>
<td><p>Specifies the default value of the composite component attribute.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">required</code></p></td>
<td><p>Specifies whether it is mandatory to provide a value for the attribute.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">method-signature</code></p></td>
<td><p>Specifies a subclass of <code dir="ltr">java.lang.Object</code> as the type of the composite component's attribute. The <code dir="ltr">method-signature</code> element declares that the composite component attribute is a method expression. The <code dir="ltr">type</code> attribute and the <code dir="ltr">method-signature</code> attribute are mutually exclusive. If you specify both, <code dir="ltr">method-signature</code> is ignored. The default type of an attribute is <code dir="ltr">java.lang.Object.</code></p>
<p><span class="bold">Note:</span> Method expressions are similar to value expressions, but rather than supporting the dynamic retrieval and setting of properties, method expressions support the invocation of a method of an arbitrary object, passing a specified set of parameters and returning the result from the called method (if any).</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">type</code></p></td>
<td><p>Specifies a fully qualified class name as the type of the attribute. The <code dir="ltr">type</code> attribute and the <code dir="ltr">method-signature</code> attribute are mutually exclusive. If you specify both, <code dir="ltr">method-signature</code> is ignored. The default type of an attribute is <code dir="ltr">java.lang.Object.</code></p></td>
</tr>
</tbody>
</table>

  

The following code snippet defines a composite component attribute and
assigns it a default value:

``` oac_no_warn
<composite:attribute name="username" default="admin"/>
```

The following code snippet uses the `method-signature` element:

``` oac_no_warn
<composite:attribute name="myaction"
                     method-signature="java.lang.String action()"/>
```

The following code snippet uses the `type` element:

``` oac_no_warn
<composite:attribute name="dateofjoining" type="java.util.Date"/>
```

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
<td><a href="jsf-advanced-cc.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-advanced-cc002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
