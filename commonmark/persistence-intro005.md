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
<td><a href="persistence-intro004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-intro006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 37.5 Querying Entities

The Java Persistence API provides the following methods for querying
entities.

  - The Java Persistence query language (JPQL) is a simple, string-based
    language similar to SQL used to query entities and their
    relationships. See [Chapter 39, "The Java Persistence Query
    Language"](persistence-querylanguage.htm#BNBTG) for more
    information.

  - The Criteria API is used to create typesafe queries using Java
    programming language APIs to query for entities and their
    relationships. See [Chapter 40, "Using the Criteria API to Create
    Queries"](persistence-criteria.htm#GJITV) for more information.

Both JPQL and the Criteria API have advantages and disadvantages.

Just a few lines long, JPQL queries are typically more concise and more
readable than Criteria queries. Developers familiar with SQL will find
it easy to learn the syntax of JPQL. JPQL named queries can be defined
in the entity class using a Java programming language annotation or in
the application's deployment descriptor. JPQL queries are not typesafe,
however, and require a cast when retrieving the query result from the
entity manager. This means that type-casting errors may not be caught at
compile time. JPQL queries don't support open-ended parameters.

Criteria queries allow you to define the query in the business tier of
the application. Although this is also possible using JPQL dynamic
queries, Criteria queries provide better performance because JPQL
dynamic queries must be parsed each time they are called. Criteria
queries are typesafe and therefore don't require casting, as JPQL
queries do. The Criteria API is just another Java programming language
API and doesn't require developers to learn the syntax of another query
language. Criteria queries are typically more verbose than JPQL queries
and require the developer to create several objects and perform
operations on those objects before submitting the query to the entity
manager.

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
<td><a href="persistence-intro004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-intro006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
