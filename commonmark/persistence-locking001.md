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
<td><a href="persistence-locking.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-locking002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 42.1 Overview of Entity Locking and Concurrency

Entity data is concurrently accessed if the data in a data source is
accessed at the same time by multiple applications. Ensure that the
underlying data's integrity is preserved when it is accessed
concurrently.

When data is updated in the database tables in a transaction, the
persistence provider assumes the database management system will hold
short-term read locks and long-term write locks to maintain data
integrity. Most persistence providers will delay database writes until
the end of the transaction, except when the application explicitly calls
for a flush (that is, the application calls the `EntityManager.flush`
method or executes queries with the flush mode set to `AUTO`).

By default, persistence providers use optimistic locking, where, before
committing changes to the data, the persistence provider checks that no
other transaction has modified or deleted the data since the data was
read. This is accomplished by a version column in the database table,
with a corresponding version attribute in the entity class. When a row
is modified, the version value is incremented. The original transaction
checks the version attribute, and if the data has been modified by
another transaction, a `javax.persistence.OptimisticLockException` will
be thrown, and the original transaction will be rolled back. When the
application specifies optimistic lock modes, the persistence provider
verifies that a particular entity has not changed since it was read from
the database even if the entity data was not modified.

Pessimistic locking goes further than optimistic locking. With
pessimistic locking, the persistence provider creates a transaction that
obtains a long-term lock on the data until the transaction is completed,
which prevents other transactions from modifying or deleting the data
until the lock has ended. Pessimistic locking is a better strategy than
optimistic locking when the underlying data is frequently accessed and
modified by many transactions.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
Using pessimistic locks on entities that are not subject to frequent modification may result in decreased application performance.</td>
</tr>
</tbody>
</table>

  

## 42.1.1 Using Optimistic Locking

Use the `javax.persistence.Version` annotation to mark a persistent
field or property as a version attribute of an entity. The version
attribute enables the entity for optimistic concurrency control. The
persistence provider reads and updates the version attribute when an
entity instance is modified during a transaction. The application may
read the version attribute, but must not modify the value.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
Although some persistence providers may support optimistic locking for entities that do not have version attributes, portable applications should always use entities with version attributes when using optimistic locking. If the application attempts to lock an entity that does not have a version attribute, and the persistence provider does not support optimistic locking for non-versioned entities, a <code dir="ltr">PersistenceException</code> will be thrown.</td>
</tr>
</tbody>
</table>

  

The `@Version` annotation has the following requirements.

  - Only a single `@Version` attribute may be defined per entity.

  - The `@Version` attribute must be in the primary table for an entity
    mapped to multiple tables.

  - The type of the `@Version` attribute must be one of the following:
    `int`, `Integer`, `long`, `Long`, `short`, `Short`, or
    `java.sql.Timestamp`.

The following code snippet shows how to define a version attribute in an
entity with persistent fields:

``` oac_no_warn
@Version
protected int version;
```

The following code snippet shows how to define a version attribute in an
entity with persistent properties:

``` oac_no_warn
@Version
protected Short getVersion() { ... }
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
<td><a href="persistence-locking.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-locking002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
