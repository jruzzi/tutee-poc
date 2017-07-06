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
<td><a href="persistence-criteria001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-criteria003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 40.2 Using the Metamodel API to Model Entity Classes

Use the Metamodel API to create a metamodel of the managed entities in a
particular persistence unit. For each entity class in a particular
package, a metamodel class is created with a trailing underscore and
with attributes that correspond to the persistent fields or properties
of the entity class.

The following entity class, `com.example.Pet`, has four persistent
fields: `id`, `name`, `color`, and `owners`:

``` oac_no_warn
package com.example;
...
@Entity
public class Pet {
    @Id
    protected Long id;
    protected String name;
    protected String color;
    @ManyToOne
    protected Set<Person> owners;
    ...
}
```

The corresponding Metamodel class is as follows:

``` oac_no_warn
package com.example;
...
@Static Metamodel(Pet.class)
public class Pet_ {

    public static volatile SingularAttribute<Pet, Long> id;
    public static volatile SingularAttribute<Pet, String> name;
    public static volatile SingularAttribute<Pet, String> color;
    public static volatile SetAttribute<Pet, Person> owners;
}
```

Criteria queries use the metamodel class and its attributes to refer to
the managed entity classes and their persistent state and relationships.

## 40.2.1 Using Metamodel Classes

Metamodel classes that correspond to entity classes are of the following
type:

``` oac_no_warn
javax.persistence.metamodel.EntityType<T>
```

Annotation processors typically generate metamodel classes either at
development time or at runtime. Developers of applications that use
Criteria queries may do either of the following:

  - Generate static metamodel classes by using the persistence
    provider's annotation processor

  - Obtain the metamodel class by doing one of the following:
    
      - Call the `getModel` method on the query root object
    
      - Obtain an instance of the `Metamodel` interface and then pass
        the entity type to the instance's `entity` method

The following code snippet shows how to obtain the `Pet` entity's
metamodel class by calling `Root<T>.getModel`:

``` oac_no_warn
EntityManager em = ...;
CriteriaBuilder cb = em.getCriteriaBuilder();
CriteriaQuery cq = cb.createQuery(Pet.class);
Root<Pet> pet = cq.from(Pet.class);
EntityType<Pet> Pet_ = pet.getModel();
```

The following code snippet shows how to obtain the `Pet` entity's
metamodel class by first obtaining a metamodel instance by using
`EntityManager.getMetamodel` and then calling `entity` on the metamodel
instance:

``` oac_no_warn
EntityManager em = ...;
Metamodel m = em.getMetamodel();
EntityType<Pet> Pet_ = m.entity(Pet.class);
```

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
The most common use case is to generate typesafe static metamodel classes at development time. Obtaining the metamodel classes dynamically, by calling <code dir="ltr">Root&lt;T&gt;.getModel</code> or <code dir="ltr">EntityManager.getMetamodel</code> and then the <code dir="ltr">entity</code> method, doesn't allow for type safety and doesn't allow the application to call persistent field or property names on the metamodel class.</td>
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
<td><a href="persistence-criteria001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-criteria003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
