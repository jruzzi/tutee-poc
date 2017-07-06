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
<td><a href="jsf-ajax005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 13.6 Handling Errors

JavaServer Faces handles Ajax errors through use of the `onerror`
attribute of the `f:ajax` tag. The value of this attribute is the name
of a JavaScript function.

When there is an error in processing a Ajax request, JavaServer Faces
calls the defined `onerror` JavaScript function and passes a data object
to it. The data object contains all the properties available for the
`onevent` attribute and, in addition, the following properties:

  - `description`

  - `errorName`

  - `errorMessage`

The `type` is `error`. The `status` property of the data object contains
one of the valid error values listed in [Table 13-4](#GKGOU).

Table 13-4 Valid Error Values for the Data Object status Property

<table style="width:20%;">
<colgroup>
<col width="20%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Values</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">emptyResponse</code></p></td>
<td><p>No Ajax response from server.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">httpError</code></p></td>
<td><p>One of the valid HTTP errors: <code dir="ltr">request.status==null</code> or <code dir="ltr">request.status==undefined</code> or <code dir="ltr">request.status&lt;200</code> or <code dir="ltr">request.status&gt;=300</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">malformedXML</code></p></td>
<td><p>The Ajax response is not well formed.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">serverError</code></p></td>
<td><p>The Ajax response contains an <code dir="ltr">error</code> element.</p></td>
</tr>
</tbody>
</table>

  

In the following example, any errors that occurred in processing the
Ajax request are handled by the `handlemyajaxerror` JavaScript
function:

``` oac_no_warn
<f:ajax event="click" render="errormessage" onerror="handlemyajaxerror"/>
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
<td><a href="jsf-ajax005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
