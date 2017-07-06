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
<td><a href="jsf-el003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-el005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 9.4 Operations on Collection Objects

The EL supports operations on collection objects: sets, lists, and maps.
It allows the dynamic creation of collection objects, which can then be
operated on using streams and pipelines.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
Like lambda expressions, operations on collection objects are part of Java SE 8, but you can use them in EL expressions with Java SE 7, the Java version associated with the Java EE 7 platform.</td>
</tr>
</tbody>
</table>

  

For example, you can construct a set as follows:

``` oac_no_warn
{1,2,3}
```

You can construct a list as follows; a list can contain various types of
items:

``` oac_no_warn
[1,2,3]
[1, "two", [three,four]]
```

You can construct a map by using a colon to define the entries, as
follows:

``` oac_no_warn
{"one":1, "two":2, "three":3}
```

You operate on collection objects using method calls to the stream of
elements derived from the collection. Some operations return another
stream, which allows additional operations. Therefore, you can chain
these operations together in a pipeline.

A stream pipeline consists of the following:

  - A source (the `Stream` object)

  - Any number of intermediate operations that return a stream (for
    example, `filter` and `map`)

  - A terminal operation that does not return a stream (for example,
    `toList()`)

The `stream` method obtains a `Stream` from a `java.util.Collection` or
a Java array. The stream operations do not modify the original
collection object.

For example, you might generate a list of titles of history books as
follows:

``` oac_no_warn
books.stream().filter(b->b.category == 'history')
              .map(b->b.title)
              .toList()
```

The following simpler example returns a sorted version of the original
list:

``` oac_no_warn
[1,3,5,2].stream().sorted().toList()
```

Streams and stream operations are documented in the Java SE 8 API
documentation, available at `http://docs.oracle.com/javase/8/docs/api/`.
The following subset of operations is supported by the EL:

  
`allMatch`  
`anyMatch`  
`average`  
`count`  
`distinct`  
`filter`  
`findFirst`  
`flatMap`  
`forEach`  
`iterator`  
`limit`  
`map`  
`max`  
`min`  
`noneMatch`  
`peek`  
`reduce`  
`sorted`  
`substream`  
`sum`  
`toArray`  
`toList`  

See the EL specification at `http://www.jcp.org/en/jsr/detail?id=341`
for details on these operations.

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
<td><a href="jsf-el003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-el005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
