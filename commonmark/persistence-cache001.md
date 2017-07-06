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
<td><a href="persistence-cache.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-cache002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 44.1 Overview of the Second-Level Cache

A second-level cache is a local store of entity data managed by the
persistence provider to improve application performance. A second-level
cache helps improve performance by avoiding expensive database calls,
keeping the entity data local to the application. A second-level cache
is typically transparent to the application, as it is managed by the
persistence provider and underlies the persistence context of an
application. That is, the application reads and commits data through the
normal entity manager operations without knowing about the cache.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
Persistence providers are not required to support a second-level cache. Portable applications should not rely on support by persistence providers for a second-level cache.</td>
</tr>
</tbody>
</table>

  

The second-level cache for a persistence unit may be configured to one
of several second-level cache modes. The following cache mode settings
are defined by the Java Persistence API.

Table 44-1 Cache Mode Settings for the Second-Level Cache

<table style="width:29%;">
<colgroup>
<col width="28%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Cache Mode Setting</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">ALL</code></p></td>
<td><p>All entity data is stored in the second-level cache for this persistence unit.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">NONE</code></p></td>
<td><p>No data is cached in the persistence unit. The persistence provider must not cache any data.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ENABLE_SELECTIVE</code></p></td>
<td><p>Enable caching for entities that have been explicitly set with the <code dir="ltr">@Cacheable</code> annotation.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">DISABLE_SELECTIVE</code></p></td>
<td><p>Enable caching for all entities except those that have been explicitly set with the <code dir="ltr">@Cacheable(false)</code> annotation.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">UNSPECIFIED</code></p></td>
<td><p>The caching behavior for the persistence unit is undefined. The persistence provider's default caching behavior will be used.</p></td>
</tr>
</tbody>
</table>

  

One consequence of using a second-level cache in an application is that
the underlying data may have changed in the database tables, while the
value in the cache has not, a circumstance called a stale read. To avoid
stale reads, use any of these strategies:

  - Change the second-level cache to one of the cache mode settings

  - Control which entities may be cached (see [Controlling whether
    Entities May Be Cached](#GKJIW))

  - Change the cache's retrieval or store modes (see [Setting the Cache
    Retrieval and Store Modes](persistence-cache002.htm#GKJDK))

Which of these strategies works best to avoid stale reads depends upon
the application.

## 44.1.1 Controlling whether Entities May Be Cached

The `javax.persistence.Cacheable` annotation is used to specify that an
entity class, and any subclasses, may be cached when using the
`ENABLE_SELECTIVE` or `DISABLE_SELECTIVE` cache modes. Subclasses may
override the `@Cacheable` setting by adding a `@Cacheable` annotation
and changing the value.

To specify that an entity may be cached, add a `@Cacheable` annotation
at the class level:

``` oac_no_warn
@Cacheable
@Entity
public class Person { ... }
```

By default, the `@Cacheable` annotation is `true`. The following example
is equivalent:

``` oac_no_warn
@Cacheable(true)
@Entity
public class Person{ ... }
```

To specify that an entity must not be cached, add a `@Cacheable`
annotation and set it to `false`:

``` oac_no_warn
@Cacheable(false)
@Entity
public class OrderStatus { ... }
```

When the `ENABLE_SELECTIVE` cache mode is set, the persistence provider
will cache any entities that have the `@Cacheable(true)` annotation and
any subclasses of that entity that have not been overridden. The
persistence provider will not cache entities that have
`@Cacheable(false)` or have no `@Cacheable` annotation. That is, the
`ENABLE_SELECTIVE` mode will cache only entities that have been
explicitly marked for the cache using the `@Cacheable` annotation.

When the `DISABLE_SELECTIVE` cache mode is set, the persistence provider
will cache any entities that do not have the `@Cacheable(false)`
annotation. Entities that do not have `@Cacheable` annotations, and
entities with the `@Cacheable(true)` annotation, will be cached. That
is, the `DISABLE_SELECTIVE` mode will cache all entities that have not
been explicitly prevented from being cached.

If the cache mode is set to `UNDEFINED`, or is left unset, the behavior
of entities annotated with `@Cacheable` is undefined. If the cache mode
is set to `ALL` or `NONE`, the value of the `@Cacheable` annotation is
ignored by the persistence provider.

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
<td><a href="persistence-cache.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-cache002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
