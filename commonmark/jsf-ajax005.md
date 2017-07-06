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
<td><a href="jsf-ajax004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 13.5 Monitoring Events on the Client

To monitor ongoing Ajax requests, use the `onevent` attribute of the
`f:ajax` tag. The value of this attribute is the name of a JavaScript
function. JavaServer Faces calls the `onevent` function at each stage of
the processing of an Ajax request: begin, complete, and success.

When calling the JavaScript function assigned to the `onevent` property,
JavaServer Faces passes a data object to it. The data object contains
the properties listed in [Table 13-3](#GKGOE).

Table 13-3 Properties of the onevent Data Object

<table style="width:20%;">
<colgroup>
<col width="20%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">responseXML</code></p></td>
<td><p>The response to the Ajax call in XML format</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">responseText</code></p></td>
<td><p>The response to the Ajax call in text format</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">responseCode</code></p></td>
<td><p>The response to the Ajax call in numeric code</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">source</code></p></td>
<td><p>The source of the current Ajax event: the DOM element</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">status</code></p></td>
<td><p>The status of the current Ajax call: <code dir="ltr">begin</code>, <code dir="ltr">complete</code>, or <code dir="ltr">success</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">type</code></p></td>
<td><p>The type of the Ajax call: <code dir="ltr">event</code></p></td>
</tr>
</tbody>
</table>

  

By using the `status` property of the data object, you can identify the
current status of the Ajax request and monitor its progress. In the
following example, `monitormyajaxevent` is a JavaScript function that
monitors the Ajax request sent by the
event:

``` oac_no_warn
<f:ajax event="click" render="statusmessage" onevent="monitormyajaxevent"/>
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
<td><a href="jsf-ajax004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
