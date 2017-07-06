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
<td><a href="jsonp.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsonp002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 19.1 Introduction to JSON

JSON is a text-based data exchange format derived from JavaScript that
is used in web services and other connected applications. The following
sections provide an introduction to JSON syntax, an overview of JSON
uses, and a description of the most common approaches to generate and
parse JSON.

The following topics are addressed here:

  - [Section 19.1.1, "JSON Syntax"](#BABGHEHG)

  - [Section 19.1.2, "Uses of JSON"](#CEGJHJAB)

  - [Section 19.1.3, "Generating and Parsing JSON Data"](#BABJJACI)

## 19.1.1 JSON Syntax

JSON defines only two data structures: objects and arrays. An object is
a set of name-value pairs, and an array is a list of values. JSON
defines seven value types: string, number, object, array, true, false,
and null.

The following example shows JSON data for a sample object that contains
name-value pairs. The value for the name `"phoneNumbers"` is an array
whose elements are two objects.

``` oac_no_warn
{
   "firstName": "Duke",
   "lastName": "Java",
   "age": 18,
   "streetAddress": "100 Internet Dr",
   "city": "JavaTown",
   "state": "JA",
   "postalCode": "12345",
   "phoneNumbers": [
      { "Mobile": "111-111-1111" },
      { "Home": "222-222-2222" }
   ]
}
```

JSON has the following syntax.

  - Objects are enclosed in braces (`{}`), their name-value pairs are
    separated by a comma (`,`), and the name and value in a pair are
    separated by a colon (`:`). Names in an object are strings, whereas
    values may be of any of the seven value types, including another
    object or an array.

  - Arrays are enclosed in brackets (`[]`), and their values are
    separated by a comma (`,`). Each value in an array may be of a
    different type, including another array or an object.

  - When objects and arrays contain other objects or arrays, the data
    has a tree-like structure.

## 19.1.2 Uses of JSON

JSON is often used as a common format to serialize and deserialize data
in applications that communicate with each other over the Internet.
These applications are created using different programming languages and
run in very different environments. JSON is suited to this scenario
because it is an open standard, it is easy to read and write, and it is
more compact than other representations.

RESTful web services use JSON extensively as the format for the data
inside requests and responses. The HTTP header used to indicate that the
content of a request or a response is JSON data is

``` oac_no_warn
Content-Type: application/json
```

JSON representations are usually more compact than XML representations
because JSON does not have closing tags. Unlike XML, JSON does not have
a widely accepted schema for defining and validating the structure of
JSON data.

## 19.1.3 Generating and Parsing JSON Data

For generating and parsing JSON data, there are two programming models,
which are similar to those used for XML documents.

  - The object model creates a tree that represents the JSON data in
    memory. The tree can then be navigated, analyzed, or modified. This
    approach is the most flexible and allows for processing that
    requires access to the complete contents of the tree. However, it is
    often slower than the streaming model and requires more memory. The
    object model generates JSON output by navigating the entire tree at
    once.

  - The streaming model uses an event-based parser that reads JSON data
    one element at a time. The parser generates events and stops for
    processing when an object or an array begins or ends, when it finds
    a key, or when it finds a value. Each element can be processed or
    discarded by the application code, and then the parser proceeds to
    the next event. This approach is adequate for local processing, in
    which the processing of an element does not require information from
    the rest of the data. The streaming model generates JSON output to a
    given stream by making a function call with one element at a time.

There are many JSON generators and parsers available for different
programming languages and environments. [JSON Processing in the Java EE
Platform](jsonp002.htm#BABDFHHD) describes the functionality provided by
the Java API for JSON Processing (JSR 353).

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
<td><a href="jsonp.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsonp002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
