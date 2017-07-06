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
<td><a href="persistence-criteria.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-criteria002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 40.1 Overview of the Criteria and Metamodel APIs

Similar to JPQL, the Criteria API is based on the abstract schema of
persistent entities, their relationships, and embedded objects. The
Criteria API operates on this abstract schema to allow developers to
find, modify, and delete persistent entities by invoking Java
Persistence API entity operations. The Metamodel API works in concert
with the Criteria API to model persistent entity classes for Criteria
queries.

The Criteria API and JPQL are closely related and are designed to allow
similar operations in their queries. Developers familiar with JPQL
syntax will find equivalent object-level operations in the Criteria API.

The following simple Criteria query returns all instances of the `Pet`
entity in the data source:

``` oac_no_warn
EntityManager em = ...;
CriteriaBuilder cb = em.getCriteriaBuilder();
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
cq.select(pet);
TypedQuery<Pet> q = em.createQuery(cq);
List<Pet> allPets = q.getResultList();
```

The equivalent JPQL query is

``` oac_no_warn
SELECT p
FROM Pet p
```

This query demonstrates the basic steps to create a Criteria query.

1.  Use an `EntityManager` instance to create a `CriteriaBuilder`
    object.

2.  Create a query object by creating an instance of the `CriteriaQuery`
    interface. This query object's attributes will be modified with the
    details of the query.

3.  Set the query root by calling the `from` method on the
    `CriteriaQuery` object.

4.  Specify what the type of the query result will be by calling the
    `select` method of the `CriteriaQuery` object.

5.  Prepare the query for execution by creating a `TypedQuery<T>`
    instance, specifying the type of the query result.

6.  Execute the query by calling the `getResultList` method on the
    `TypedQuery<T>` object. Because this query returns a collection of
    entities, the result is stored in a `List`.

The tasks associated with each step are discussed in detail in this
chapter.

To create a `CriteriaBuilder` instance, call the `getCriteriaBuilder`
method on the `EntityManager` instance:

``` oac_no_warn
CriteriaBuilder cb = em.getCriteriaBuilder();
```

Use the `CriteriaBuilder` instance to create a query object:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
```

The query will return instances of the `Pet` entity. To create a
typesafe query, specify the type of the query when you create the
`CriteriaQuery` object.

Call the `from` method of the query object to set the `FROM` clause of
the query and to specify the root of the query:

``` oac_no_warn
Root<Pet> pet = cq.from(Pet.class);
```

Call the `select` method of the query object, passing in the query root,
to set the `SELECT` clause of the query:

``` oac_no_warn
cq.select(pet);
```

Now, use the query object to create a `TypedQuery<T>` object that can be
executed against the data source. The modifications to the query object
are captured to create a ready-to-execute query:

``` oac_no_warn
TypedQuery<Pet> q = em.createQuery(cq);
```

Execute this typed query object by calling its `getResultList` method,
because this query will return multiple entity instances. The following
statement stores the results in a `List<Pet>` collection-valued object:

``` oac_no_warn
List<Pet> allPets = q.getResultList();
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
<td><a href="persistence-criteria.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-criteria002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
