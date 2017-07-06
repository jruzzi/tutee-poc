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
<td><a href="persistence-cache001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partmessaging.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 44.2 Specifying the Cache Mode Settings to Improve Performance

To adjust the cache mode settings for a persistence unit, specify one of
the cache modes as the value of the `shared-cache-mode` element in the
`persistence.xml` deployment descriptor (shown in bold):

``` oac_no_warn
<persistence-unit name="examplePU" transaction-type="JTA">
    <provider>org.eclipse.persistence.jpa.PersistenceProvider</provider>
    <jta-data-source>java:comp/DefaultDataSource</jta-data-source>
    <shared-cache-mode>DISABLE_SELECTIVE</shared-cache-mode>
</persistence-unit>
```

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
Because support for a second-level cache is not required by the Java Persistence API specification, setting the second-level cache mode in <code dir="ltr">persistence.xml</code> will have no effect when you use a persistence provider that does not implement a second-level cache.</td>
</tr>
</tbody>
</table>

  

Alternatively, you can specify the shared cache mode by setting the
`javax.persistence.sharedCache.mode` property to one of the shared cache
mode settings:

``` oac_no_warn
EntityManagerFactory emf = 
    Persistence.createEntityManagerFactory(
        "myExamplePU", new Properties().add(
            "javax.persistence.sharedCache.mode", "ENABLE_SELECTIVE"));
```

## 44.2.1 Setting the Cache Retrieval and Store Modes

If you have enabled the second-level cache for a persistence unit by
setting the shared cache mode, you can further modify the behavior of
the second-level cache by setting the
`javax.persistence.cache.retrieveMode` and
`javax.persistence.cache.storeMode` properties. You can set these
properties at the persistence context level by passing the property name
and value to the `EntityManager.setProperty` method, or you can set them
on a per-`EntityManager` operation (`EntityManager.find` or
`EntityManager.refresh`) or on a per-query level.

### 44.2.1.1 Cache Retrieval Mode

The cache retrieval mode, set by the `javax.persistence.retrieveMode`
property, controls how data is read from the cache for calls to the
`EntityManager.find` method and from queries.

You can set the `retrieveMode` property to one of the constants defined
by the `javax.persistence.CacheRetrieveMode` enumerated type, either
`USE` (the default) or `BYPASS`.

When the property is set to `USE`, data is retrieved from the
second-level cache, if available. If the data is not in the cache, the
persistence provider will read it from the database.

When the property is set to `BYPASS`, the second-level cache is bypassed
and a call to the database is made to retrieve the data.

### 44.2.1.2 Cache Store Mode

The cache store mode, set by the `javax.persistence.storeMode` property,
controls how data is stored in the cache.

The `storeMode` property can be set to one of the constants defined by
the `javax.persistence.CacheStoreMode` enumerated type: either `USE`
(the default), `BYPASS`, or `REFRESH`.

When the property is set to `USE`, the cache data is created or updated
when data is read from or committed to the database. If data is already
in the cache, setting the store mode to `USE` will not force a refresh
when data is read from the database.

When the property is set to `BYPASS`, data read from or committed to the
database is not inserted or updated in the cache. That is, the cache is
unchanged.

When the property is set to `REFRESH`, the cache data is created or
updated when data is read from or committed to the database, and a
refresh is forced on data in the cache upon database reads.

### 44.2.1.3 Setting the Cache Retrieval or Store Mode

To set the cache retrieval or store mode for the persistence context,
call the `EntityManager.setProperty` method with the property name and
value pair:

``` oac_no_warn
EntityManager em = ...;
em.setProperty("javax.persistence.cache.storeMode", "BYPASS");
```

To set the cache retrieval or store mode when calling the
`EntityManager.find` or `EntityManager.refresh` methods, first create a
`Map<String, Object>` instance and add a name/value pair as follows:

``` oac_no_warn
EntityManager em = ...;
Map<String, Object> props = new HashMap<String, Object>();
props.put("javax.persistence.cache.retrieveMode", "BYPASS");
String personPK = ...;
Person person = em.find(Person.class, personPK, props);
```

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
The cache retrieval mode is ignored when calling the <code dir="ltr">EntityManager.refresh</code> method, as calls to <code dir="ltr">refresh</code> always result in data being read from the database, not the cache.</td>
</tr>
</tbody>
</table>

  

To set the retrieval or store mode when using queries, call the
`Query.setHint` or `TypedQuery.setHint` methods, depending on the type
of query:

``` oac_no_warn
EntityManager em = ...;
CriteriaQuery<Person> cq = ...;
TypedQuery<Person> q = em.createQuery(cq);
q.setHint("javax.persistence.cache.storeMode", "REFRESH");
...
```

Setting the store or retrieve mode in a query or when calling the
`EntityManager.find` or `EntityManager.refresh` method overrides the
setting of the entity manager.

## 44.2.2 Controlling the Second-Level Cache Programmatically

The `javax.persistence.Cache` interface defines methods for interacting
with the second-level cache programmatically.

The following topics are addressed here:

  - [Section 44.2.2.1, "Overview of the javax.persistence.Cache
    Interface"](#CHDEECCF)

  - [Section 44.2.2.2, "Checking whether an Entity's Data Is
    Cached"](#GKJDZ)

  - [Section 44.2.2.3, "Removing an Entity from the Cache"](#GKJDQ)

  - [Section 44.2.2.4, "Removing All Data from the Cache"](#GKJDA)

### 44.2.2.1 Overview of the javax.persistence.Cache Interface

The `Cache` interface defines methods to do the following:

  - Check whether a particular entity has cached data

  - Remove a particular entity from the cache

  - Remove all instances (and instances of subclasses) of an entity
    class from the cache

  - Clear the cache of all entity data

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
If the second-level cache has been disabled, calls to the <code dir="ltr">Cache</code> interface's methods have no effect, except for <code dir="ltr">contains</code>, which will always return <code dir="ltr">false</code>.</td>
</tr>
</tbody>
</table>

  

### 44.2.2.2 Checking whether an Entity's Data Is Cached

To find out whether a given entity is currently in the second-level
cache:

1.  Call the `Cache.contains` method . The `contains` method returns
    `true` if the entity's data is cached, and `false` if the data is
    not in the cache:
    
    ``` oac_no_warn
    EntityManager em = ...;
    Cache cache = em.getEntityManagerFactory().getCache();
    String personPK = ...;
    if (cache.contains(Person.class, personPK)) {
      // the data is cached
    } else {
      // the data is NOT cached
    }
    ```

### 44.2.2.3 Removing an Entity from the Cache

To remove a particular entity or all entities of a given type from the
second-level cache:

1.  Call one of the `Cache.evict` methods .
    
    1.  To remove a particular entity from the cache, call the `evict`
        method and pass in the entity class and the primary key of the
        entity:
        
        ``` oac_no_warn
        EntityManager em = ...;
        Cache cache = em.getEntityManagerFactory().getCache();
        String personPK = ...;
        cache.evict(Person.class, personPK);
        ```
    
    2.  To remove all instances of a particular entity class, including
        subclasses, call the `evict` method and specify the entity
        class:
        
        ``` oac_no_warn
        EntityManager em = ...;
        Cache cache = em.getEntityManagerFactory().getCache();
        cache.evict(Person.class);
        ```

All instances of the `Person` entity class will be removed from the
cache. If the `Person` entity has a subclass, `Student`, calls to the
above method will remove all instances of `Student` from the cache as
well.

### 44.2.2.4 Removing All Data from the Cache

To completely clear the second-level cache:

1.  Call the `Cache.evictAll` method.
    
    ``` oac_no_warn
    EntityManager em = ...;
    Cache cache = em.getEntityManagerFactory().getCache();
    cache.evictAll();
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
<td><a href="persistence-cache001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partmessaging.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
