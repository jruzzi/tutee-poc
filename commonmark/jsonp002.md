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
<td><a href="jsonp001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsonp003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 19.2 JSON Processing in the Java EE Platform

Java EE includes support for JSR 353, which provides an API to parse,
transform, and query JSON data using the object model or the streaming
model described in [Generating and Parsing JSON
Data](jsonp001.htm#BABJJACI). The Java API for JSON Processing contains
the following packages.

  - The `javax.json` package contains a reader interface, a writer
    interface, and a model builder interface for the object model. This
    package also contains other utility classes and Java types for JSON
    elements. [Table 19-1](#CHDJJCBE) lists the main classes and
    interfaces in this package.

  - The `javax.json.stream` package contains a parser interface and a
    generator interface for the streaming model. [Table 19-2](#CHDIHCEG)
    lists the main classes and interfaces in this package.

Table 19-1 Main Classes and Interfaces in javax.json

<table style="width:25%;">
<colgroup>
<col width="25%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Class or Interface</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">Json</code></p></td>
<td><p>Contains static methods to create instances of JSON parsers, builders, and generators. This class also contains methods to create parser, builder, and generator factory objects.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">JsonReader</code></p></td>
<td><p>Reads JSON data from a stream and creates an object model in memory.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">JsonObjectBuilder</code></p>
<p><code dir="ltr">JsonArrayBuilder</code></p></td>
<td><p>Create an object model or an array model in memory by adding elements from application code.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">JsonWriter</code></p></td>
<td><p>Writes an object model from memory to a stream.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">JsonValue</code></p></td>
<td><p>Represents an element (such as an object, an array, or a value) in JSON data.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">JsonStructure</code></p></td>
<td><p>Represents an object or an array in JSON data. This interface is a subtype of <code dir="ltr">JsonValue</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">JsonObject</code></p>
<p><code dir="ltr">JsonArray</code></p></td>
<td><p>Represent an object or an array in JSON data. These two interfaces are subtypes of <code dir="ltr">JsonStructure</code>.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">JsonString</code></p>
<p><code dir="ltr">JsonNumber</code></p></td>
<td><p>Represent data types for elements in JSON data. These two interfaces are subtypes of <code dir="ltr">JsonValue</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">JsonException</code></p></td>
<td><p>Indicates that a problem occurred during JSON processing.</p></td>
</tr>
</tbody>
</table>

  

Table 19-2 Main Classes and Interfaces in javax.json.stream

<table style="width:25%;">
<colgroup>
<col width="25%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Class or Interface</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">JsonParser</code></p></td>
<td><p>Represents an event-based parser that can read JSON data from a stream or from an object model.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">JsonGenerator</code></p></td>
<td><p>Writes JSON data to a stream one element at a time.</p></td>
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
<td><a href="jsonp001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsonp003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
