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
<td><a href="jaxws002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxws004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 28.3 Types Supported by JAX-WS

JAX-WS delegates the mapping of Java programming language types to and
from XML definitions to JAXB. Application developers don't need to know
the details of these mappings but should be aware that not every class
in the Java language can be used as a method parameter or return type in
JAX-WS.

The following sections explain the default schema-to-Java and
Java-to-schema data type bindings:

  - [Section 28.3.1, "Schema-to-Java Mapping"](#BNAZT)

  - [Section 28.3.2, "Java-to-Schema Mapping"](#BNAZW)

## 28.3.1 Schema-to-Java Mapping

The Java language provides a richer set of data types than XML schema.
[Table 28-1](#BNAZU) lists the mapping of XML data types to Java data
types in JAXB.

Table 28-1 Mapping of XML Data Types to Java Data Types in JAXB

<table style="width:27%;">
<colgroup>
<col width="27%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>XML Schema Type</th>
<th>Java Data Type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">xsd:string</code></p></td>
<td><p><code dir="ltr">java.lang.String</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:integer</code></p></td>
<td><p><code dir="ltr">java.math.BigInteger</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:int</code></p></td>
<td><p><code dir="ltr">int</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd.long</code></p></td>
<td><p><code dir="ltr">long</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:short</code></p></td>
<td><p><code dir="ltr">short</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:decimal</code></p></td>
<td><p><code dir="ltr">java.math.BigDecimal</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:float</code></p></td>
<td><p><code dir="ltr">float</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:double</code></p></td>
<td><p><code dir="ltr">double</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:boolean</code></p></td>
<td><p><code dir="ltr">boolean</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:byte</code></p></td>
<td><p><code dir="ltr">byte</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:QName</code></p></td>
<td><p><code dir="ltr">javax.xml.namespace.QName</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:dateTime</code></p></td>
<td><p><code dir="ltr">javax.xml.datatype.XMLGregorianCalendar</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:base64Binary</code></p></td>
<td><p><code dir="ltr">byte[]</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:hexBinary</code></p></td>
<td><p><code dir="ltr">byte[]</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:unsignedInt</code></p></td>
<td><p><code dir="ltr">long</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:unsignedShort</code></p></td>
<td><p><code dir="ltr">int</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:unsignedByte</code></p></td>
<td><p><code dir="ltr">short</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:time</code></p></td>
<td><p><code dir="ltr">javax.xml.datatype.XMLGregorianCalendar</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:date</code></p></td>
<td><p><code dir="ltr">javax.xml.datatype.XMLGregorianCalendar</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:g</code></p></td>
<td><p><code dir="ltr">javax.xml.datatype.XMLGregorianCalendar</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:anySimpleType</code></p></td>
<td><p><code dir="ltr">java.lang.Object</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:anySimpleType</code></p></td>
<td><p><code dir="ltr">java.lang.String</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">xsd:duration</code></p></td>
<td><p><code dir="ltr">javax.xml.datatype.Duration</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">xsd:NOTATION</code></p></td>
<td><p><code dir="ltr">javax.xml.namespace.QName</code></p></td>
</tr>
</tbody>
</table>

  

## 28.3.2 Java-to-Schema Mapping

[Table 28-2](#BNAZX) shows the default mapping of Java classes to XML
data types.

Table 28-2 Mapping of Java Classes to XML Data Types in JAXB

<table style="width:49%;">
<colgroup>
<col width="0%" />
<col width="49%" />
</colgroup>
<thead>
<tr class="header">
<th>Java Class</th>
<th>XML Data Type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">java.lang.String</code></p></td>
<td><p><code dir="ltr">xs:string</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">java.math.BigInteger</code></p></td>
<td><p><code dir="ltr">xs:integer</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">java.math.BigDecimal</code></p></td>
<td><p><code dir="ltr">xs:decimal</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">java.util.Calendar</code></p></td>
<td><p><code dir="ltr">xs:dateTime</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">java.util.Date</code></p></td>
<td><p><code dir="ltr">xs:dateTime</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.xml.namespace.QName</code></p></td>
<td><p><code dir="ltr">xs:QName</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">java.net.URI</code></p></td>
<td><p><code dir="ltr">xs:string</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.xml.datatype.XMLGregorianCalendar</code></p></td>
<td><p><code dir="ltr">xs:anySimpleType</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.xml.datatype.Duration</code></p></td>
<td><p><code dir="ltr">xs:duration</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">java.lang.Object</code></p></td>
<td><p><code dir="ltr">xs:anyType</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">java.awt.Image</code></p></td>
<td><p><code dir="ltr">xs:base64Binary</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.activation.DataHandler</code></p></td>
<td><p><code dir="ltr">xs:base64Binary</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.xml.transform.Source</code></p></td>
<td><p><code dir="ltr">xs:base64Binary</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">java.util.UUID</code></p></td>
<td><p><code dir="ltr">xs:string</code></p></td>
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
<td><a href="jaxws002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxws004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
