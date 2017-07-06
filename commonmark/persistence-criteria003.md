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
<td><a href="persistence-criteria002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-string-queries.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft:
2017-06-12

# 40.3 Using the Criteria API and Metamodel API to Create Basic Typesafe Queries

The basic semantics of a Criteria query consists of a `SELECT` clause, a
`FROM` clause, and an optional `WHERE` clause, similar to a JPQL query.
Criteria queries set these clauses by using Java programming language
objects, so the query can be created in a typesafe manner.

The following topics are addressed here:

  - [Section 40.3.1, "Creating a Criteria Query"](#GJIVS)

  - [Section 40.3.2, "Query Roots"](#GJIVQ)

  - [Section 40.3.3, "Querying Relationships Using Joins"](#GJIUV)

  - [Section 40.3.4, "Path Navigation in Criteria Queries"](#GJIVE)

  - [Section 40.3.5, "Restricting Criteria Query Results"](#GJIVI)

  - [Section 40.3.6, "Managing Criteria Query Results"](#GJIXE)

  - [Section 40.3.7, "Executing Queries"](#GJIVY)

## 40.3.1 Creating a Criteria Query

The `javax.persistence.criteria.CriteriaBuilder` interface is used to
construct

  - Criteria queries

  - Selections

  - Expressions

  - Predicates

  - Ordering

To obtain an instance of the `CriteriaBuilder` interface, call the
`getCriteriaBuilder` method on either an `EntityManager` or an
`EntityManagerFactory` instance.

The following code shows how to obtain a `CriteriaBuilder` instance by
using the `EntityManager.getCriteriaBuilder` method:

``` oac_no_warn
EntityManager em = ...;
CriteriaBuilder cb = em.getCriteriaBuilder();
```

Criteria queries are constructed by obtaining an instance of the
following interface:

``` oac_no_warn
javax.persistence.criteria.CriteriaQuery
```

`CriteriaQuery` objects define a particular query that will navigate
over one or more entities. Obtain `CriteriaQuery` instances by calling
one of the `CriteriaBuilder.createQuery` methods. To create typesafe
queries, call the `CriteriaBuilder.createQuery` method as follows:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
```

The `CriteriaQuery` object's type should be set to the expected result
type of the query. In the preceding code, the object's type is set to
`CriteriaQuery<Pet>` for a query that will find instances of the `Pet`
entity.

The following code snippet creates a `CriteriaQuery` object for a query
that returns a `String`:

``` oac_no_warn
CriteriaQuery<String> cq = cb.createQuery(String.class);
```

## 40.3.2 Query Roots

For a particular `CriteriaQuery` object, the root entity of the query,
from which all navigation originates, is called the query root. It is
similar to the `FROM` clause in a JPQL query.

Create the query root by calling the `from` method on the
`CriteriaQuery` instance. The argument to the `from` method is either
the entity class or an `EntityType<T>` instance for the entity.

The following code sets the query root to the `Pet` entity:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
```

The following code sets the query root to the `Pet` class by using an
`EntityType<T>` instance:

``` oac_no_warn
EntityManager em = ...;
Metamodel m = em.getMetamodel();
EntityType<Pet> Pet_ = m.entity(Pet.class);
Root<Pet> pet = cq.from(Pet_);
```

Criteria queries may have more than one query root. This usually occurs
when the query navigates from several entities.

The following code has two `Root` instances:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet1 = cq.from(Pet.class);
Root<Pet> pet2 = cq.from(Pet.class);
```

## 40.3.3 Querying Relationships Using Joins

For queries that navigate to related entity classes, the query must
define a join to the related entity by calling one of the `From.join`
methods on the query root object or another join object. The `join`
methods are similar to the `JOIN` keyword in JPQL.

The target of the join uses the Metamodel class of type `EntityType<T>`
to specify the persistent field or property of the joined entity.

The `join` methods return an object of type `Join<X, Y>`, where `X` is
the source entity and `Y` is the target of the join. In the following
code snippet, `Pet` is the source entity, `Owner` is the target, and
`Pet_` is a statically generated metamodel class:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);

Root<Pet> pet = cq.from(Pet.class);
Join<Pet, Owner> owner = pet.join(Pet_.owners);
```

You can chain joins together to navigate to related entities of the
target entity without having to create a `Join<X, Y>` instance for each
join:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);

Root<Pet> pet = cq.from(Pet.class);
Join<Owner, Address> address = pet.join(Pet_.owners).join(Owner_.addresses);
```

## 40.3.4 Path Navigation in Criteria Queries

`Path` objects, which are used in the `SELECT` and `WHERE` clauses of a
Criteria query, can be query root entities, join entities, or other
`Path` objects. Use the `Path.get` method to navigate to attributes of
the entities of a query.

The argument to the `get` method is the corresponding attribute of the
entity's Metamodel class. The attribute can be either a single-valued
attribute, specified by `@SingularAttribute` in the Metamodel class, or
a collection-valued attribute, specified by one of
`@CollectionAttribute`, `@SetAttribute`, `@ListAttribute`, or
`@MapAttribute`.

The following query returns the names of all the pets in the data store.
The `get` method is called on the query root, `pet`, with the `name`
attribute of the `Pet` entity's Metamodel class, `Pet_`, as the
argument:

``` oac_no_warn
CriteriaQuery<String> cq = cb.createQuery(String.class);

Root<Pet> pet = cq.from(Pet.class);
cq.select(pet.get(Pet_.name));
```

## 40.3.5 Restricting Criteria Query Results

Conditions that are set by calling the `CriteriaQuery.where` method can
restrict the results of a query on the `CriteriaQuery` object. Calling
the `where` method is analogous to setting the `WHERE` clause in a JPQL
query.

The `where` method evaluates instances of the `Expression` interface to
restrict the results according to the conditions of the expressions. To
create `Expression` instances, use methods defined in the `Expression`
and `CriteriaBuilder` interfaces.

### 40.3.5.1 The Expression Interface Methods

An `Expression` object is used in a query's `SELECT`, `WHERE`, or
`HAVING` clause. [Table 40-1](#GJIWW) shows conditional methods you can
use with `Expression` objects.

Table 40-1 Conditional Methods in the Expression Interface

<table style="width:20%;">
<colgroup>
<col width="20%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">isNull</code></p></td>
<td><p>Tests whether an expression is null</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">isNotNull</code></p></td>
<td><p>Tests whether an expression is not null</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">in</code></p></td>
<td><p>Tests whether an expression is within a list of values</p></td>
</tr>
</tbody>
</table>

  

The following query uses the `Expression.isNull` method to find all pets
where the `color` attribute is null:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
cq.where(pet.get(Pet_.color).isNull());
```

The following query uses the `Expression.in` method to find all brown
and black pets:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
cq.where(pet.get(Pet_.color).in("brown", "black"));
```

The `in` method can also check whether an attribute is a member of a
collection.

### 40.3.5.2 Expression Methods in the CriteriaBuilder Interface

The `CriteriaBuilder` interface defines additional methods for creating
expressions. These methods correspond to the arithmetic, string, date,
time, and case operators and functions of JPQL. [Table 40-2](#GJIXL)
shows conditional methods you can use with `CriteriaBuilder` objects.

Table 40-2 Conditional Methods in the CriteriaBuilder Interface

<table style="width:20%;">
<colgroup>
<col width="20%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Conditional Method</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">equal</code></p></td>
<td><p>Tests whether two expressions are equal</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">notEqual</code></p></td>
<td><p>Tests whether two expressions are not equal</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">gt</code></p></td>
<td><p>Tests whether the first numeric expression is greater than the second numeric expression</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">ge</code></p></td>
<td><p>Tests whether the first numeric expression is greater than or equal to the second numeric expression</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">lt</code></p></td>
<td><p>Tests whether the first numeric expression is less than the second numeric expression</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">le</code></p></td>
<td><p>Tests whether the first numeric expression is less than or equal to the second numeric expression</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">between</code></p></td>
<td><p>Tests whether the first expression is between the second and third expression in value</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">like</code></p></td>
<td><p>Tests whether the expression matches a given pattern</p></td>
</tr>
</tbody>
</table>

  

The following code uses the `CriteriaBuilder.equal` method:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
cq.where(cb.equal(pet.get(Pet_.name), "Fido"));
```

The following code uses the `CriteriaBuilder.gt` method:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
Date someDate = new Date(...);
cq.where(cb.gt(pet.get(Pet_.birthday), date));
```

The following code uses the `CriteriaBuilder.between` method:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
Date firstDate = new Date(...);
Date secondDate = new Date(...);
cq.where(cb.between(pet.get(Pet_.birthday), firstDate, secondDate));
```

The following code uses the `CriteriaBuilder.like` method:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
cq.where(cb.like(pet.get(Pet_.name), "*do"));
```

To specify multiple conditional predicates, use the compound predicate
methods of the `CriteriaBuilder` interface, as shown in [Table
40-3](#GJIWU).

Table 40-3 Compound Predicate Methods in the CriteriaBuilder Interface

<table style="width:20%;">
<colgroup>
<col width="20%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">and</code></p></td>
<td><p>A logical conjunction of two Boolean expressions</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">or</code></p></td>
<td><p>A logical disjunction of two Boolean expressions</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">not</code></p></td>
<td><p>A logical negation of the given Boolean expression</p></td>
</tr>
</tbody>
</table>

  

The following code shows the use of compound predicates in queries:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
cq.where(cb.equal(pet.get(Pet_.name), "Fido")
        .and(cb.equal(pet.get(Pet_.color), "brown")));
```

## 40.3.6 Managing Criteria Query Results

For queries that return more than one result, it is often helpful to
organize those results. The `CriteriaQuery` interface defines the
following ordering and grouping methods:

  - The `orderBy` method orders query results according to attributes of
    an entity

  - The `groupBy` method groups the results of a query together
    according to attributes of an entity, and the `having` method
    restricts those groups according to a condition

The following topics are addressed here:

  - [Section 40.3.6.1, "Ordering Results"](#GJIWO)

  - [Section 40.3.6.2, "Grouping Results"](#GJIXG)

### 40.3.6.1 Ordering Results

To order the results of a query, call the `CriteriaQuery.orderBy`
method, passing in an `Order` object. To create an `Order` object, call
either the `CriteriaBuilder.asc` or the `CriteriaBuilder.desc` method.
The `asc` method is used to order the results by ascending value of the
passed expression parameter. The `desc` method is used to order the
results by descending value of the passed expression parameter. The
following query shows the use of the `desc` method:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
cq.select(pet);
cq.orderBy(cb.desc(pet.get(Pet_.birthday)));
```

In this query, the results will be ordered by the pet's birthday from
highest to lowest. That is, pets born in December will appear before
pets born in May.

The following query shows the use of the `asc` method:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
Join<Owner, Address> address = pet.join(Pet_.owners).join(Owner_.address);
cq.select(pet);
cq.orderBy(cb.asc(address.get(Address_.postalCode)));
```

In this query, the results will be ordered by the pet owner's postal
code from lowest to highest. That is, pets whose owner lives in the
10001 zip code will appear before pets whose owner lives in the 91000
zip code.

If more than one `Order` object is passed to `orderBy`, the precedence
is determined by the order in which they appear in the argument list of
`orderBy`. The first `Order` object has precedence.

The following code orders results by multiple criteria:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
Join<Pet, Owner> owner = pet.join(Pet_.owners);
cq.select(pet);
cq.orderBy(cb.asc(owner.get(Owner_.lastName)), owner.get(Owner_.firstName)));
```

The results of this query will be ordered alphabetically by the pet
owner's last name, then first name.

### 40.3.6.2 Grouping Results

The `CriteriaQuery.groupBy` method partitions the query results into
groups. To set these groups, pass an expression to `groupBy`:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
cq.groupBy(pet.get(Pet_.color));
```

This query returns all `Pet` entities and groups the results by the
pet's color.

Use the `CriteriaQuery.having` method in conjunction with `groupBy` to
filter over the groups. The `having` method, which takes a conditional
expression as a parameter, restricts the query result according to the
conditional expression:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
cq.groupBy(pet.get(Pet_.color));
cq.having(cb.in(pet.get(Pet_.color)).value("brown").value("blonde"));
```

In this example, the query groups the returned `Pet` entities by color,
as in the preceding example. However, the only returned groups will be
`Pet` entities where the `color` attribute is set to `brown` or
`blonde`. That is, no gray-colored pets will be returned in this query.

## 40.3.7 Executing Queries

To prepare a query for execution, create a `TypedQuery<T>` object with
the type of the query result, passing the `CriteriaQuery` object to
`EntityManager.createQuery`.

To execute a query, call either `getSingleResult` or `getResultList` on
the `TypedQuery<T>` object.

### 40.3.7.1 Single-Valued Query Results

Use the `TypedQuery<T>.getSingleResult` method to execute queries that
return a single result:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
...
TypedQuery<Pet> q = em.createQuery(cq);
Pet result = q.getSingleResult();
```

### 40.3.7.2 Collection-Valued Query Results

Use the `TypedQuery<T>.getResultList` method to execute queries that
return a collection of objects:

``` oac_no_warn
CriteriaQuery<Pet> cq = cb.createQuery(Pet.class);
...
TypedQuery<Pet> q = em.createQuery(cq);
List<Pet> results = q.getResultList();
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
<td><a href="persistence-criteria002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-string-queries.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
