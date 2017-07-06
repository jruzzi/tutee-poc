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
<td><a href="persistence-querylanguage003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-querylanguage005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 39.4 Simplified Query Language Syntax

This section briefly describes the syntax of the query language so that
you can quickly move on to [Example
Queries](persistence-querylanguage005.htm#BNBTL). When you are ready to
learn about the syntax in more detail, see [Full Query Language
Syntax](persistence-querylanguage006.htm#BNBUF).

The following topics are addressed here:

  - [Section 39.4.1, "Select Statements"](#BNBTJ)

  - [Section 39.4.2, "Update and Delete Statements"](#BNBTK)

## 39.4.1 Select Statements

A select query has six clauses: `SELECT`, `FROM`, `WHERE`, `GROUP BY`,
`HAVING`, and `ORDER BY`. The `SELECT` and `FROM` clauses are required,
but the `WHERE`, `GROUP BY`, `HAVING`, and `ORDER BY` clauses are
optional. Here is the high-level BNF syntax of a query language select
query:

``` oac_no_warn
QL_statement ::= select_clause from_clause 
  [where_clause][groupby_clause][having_clause][orderby_clause]
```

The BNF syntax defines the following clauses.

  - The `SELECT` clause defines the types of the objects or values
    returned by the query.

  - The `FROM` clause defines the scope of the query by declaring one or
    more identification variables, which can be referenced in the
    `SELECT` and `WHERE` clauses. An identification variable represents
    one of the following elements:
    
      - The abstract schema name of an entity
    
      - An element of a collection relationship
    
      - An element of a single-valued relationship
    
      - A member of a collection that is the multiple side of a
        one-to-many relationship

  - The `WHERE` clause is a conditional expression that restricts the
    objects or values retrieved by the query. Although the clause is
    optional, most queries have a `WHERE` clause.

  - The `GROUP BY` clause groups query results according to a set of
    properties.

  - The `HAVING` clause is used with the `GROUP BY` clause to further
    restrict the query results according to a conditional expression.

  - The `ORDER BY` clause sorts the objects or values returned by the
    query into a specified order.

## 39.4.2 Update and Delete Statements

Update and delete statements provide bulk operations over sets of
entities. These statements have the following syntax:

``` oac_no_warn
update_statement :: = update_clause [where_clause] 
delete_statement :: = delete_clause [where_clause]
```

The update and delete clauses determine the type of the entities to be
updated or deleted. The `WHERE` clause may be used to restrict the scope
of the update or delete operation.

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
<td><a href="persistence-querylanguage003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-querylanguage005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
