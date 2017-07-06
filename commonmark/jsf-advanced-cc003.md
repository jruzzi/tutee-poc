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
<td><a href="jsf-advanced-cc002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-advanced-cc004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 14.3 Validating Composite Component Values

JavaServer Faces provides the following tags for validating values of
input components. These tags can be used with the
`composite:valueHolder` or the `composite:editableValueHolder` tag.

[Table 14-2](#GKHVG) lists commonly used validator tags. See [Using the
Standard Validators](jsf-page-core003.htm#BNATC) for details and a
complete list.

Table 14-2 Validator Tags

<table style="width:27%;">
<colgroup>
<col width="27%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">f:validateBean</code></p></td>
<td><p>Delegates the validation of the local value to the Bean Validation API.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:validateRegex</code></p></td>
<td><p>Uses the <code dir="ltr">pattern</code> attribute to validate the wrapping component. The entire pattern is matched against the <code dir="ltr">String</code> value of the component. If it matches, it is valid.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">f:validateRequired</code></p></td>
<td><p>Enforces the presence of a value. Has the same effect as setting the <code dir="ltr">required</code> element of a composite component's attribute to <code dir="ltr">true</code>.</p></td>
</tr>
</tbody>
</table>

  

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
<td><a href="jsf-advanced-cc002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-advanced-cc004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
