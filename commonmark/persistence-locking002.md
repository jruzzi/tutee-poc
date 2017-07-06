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
<td><a href="persistence-locking001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-entitygraphs.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 42.2 Lock Modes

The application may increase the level of locking for an entity by
specifying the use of lock modes. Lock modes may be specified to
increase the level of optimistic locking or to request the use of
pessimistic locks.

The use of optimistic lock modes causes the persistence provider to
check the version attributes for entities that were read (but not
modified) during a transaction as well as for entities that were
updated.

The use of pessimistic lock modes specifies that the persistence
provider is to immediately acquire long-term read or write locks for the
database data corresponding to entity state.

You can set the lock mode for an entity operation by specifying one of
the lock modes defined in the `javax.persistence.LockModeType`
enumerated type, listed in [Table 42-1](#GKJIE).

Table 42-1 Lock Modes for Concurrent Entity Access

<table style="width:38%;">
<colgroup>
<col width="38%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Lock Mode</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">OPTIMISTIC</code></p></td>
<td><p>Obtain an optimistic read lock for all entities with version attributes.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">OPTIMISTIC_FORCE_INCREMENT</code></p></td>
<td><p>Obtain an optimistic read lock for all entities with version attributes, and increment the version attribute value.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">PESSIMISTIC_READ</code></p></td>
<td><p>Immediately obtain a long-term read lock on the data to prevent the data from being modified or deleted. Other transactions may read the data while the lock is maintained, but may not modify or delete the data.</p>
<p>The persistence provider is permitted to obtain a database write lock when a read lock was requested, but not vice versa.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">PESSIMISTIC_WRITE</code></p></td>
<td><p>Immediately obtain a long-term write lock on the data to prevent the data from being read, modified, or deleted.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">PESSIMISTIC_FORCE_INCREMENT</code></p></td>
<td><p>Immediately obtain a long-term lock on the data to prevent the data from being modified or deleted, and increment the version attribute of versioned entities.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">READ</code></p></td>
<td><p>A synonym for <code dir="ltr">OPTIMISTIC</code>. Use of <code dir="ltr">LockModeType.OPTIMISTIC</code> is to be preferred for new applications.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">WRITE</code></p></td>
<td><p>A synonym for <code dir="ltr">OPTIMISTIC_FORCE_INCREMENT</code>. Use of <code dir="ltr">LockModeType.OPTIMISTIC_FORCE_INCREMENT</code> is to be preferred for new applications.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">NONE</code></p></td>
<td><p>No additional locking will occur on the data in the database.</p></td>
</tr>
</tbody>
</table>

  

## 42.2.1 Setting the Lock Mode

To specify the lock mode, use one of the following techniques:

1.  Call the `EntityManager.lock` method, passing in one of the lock
    modes:
    
    ``` oac_no_warn
    EntityManager em = ...;
    Person person = ...;
    em.lock(person, LockModeType.OPTIMISTIC);
    ```

2.  Call one of the `EntityManager.find` methods that take the lock mode
    as a parameter:
    
    ``` oac_no_warn
    EntityManager em = ...;
    String personPK = ...;
    Person person = em.find(Person.class, personPK, 
        LockModeType.PESSIMISTIC_WRITE);
    ```

3.  Call one of the `EntityManager.refresh` methods that take the lock
    mode as a parameter:
    
    ``` oac_no_warn
    EntityManager em = ...;
    String personPK = ...;
    Person person = em.find(Person.class, personPK);
    ...
    em.refresh(person, LockModeType.OPTIMISTIC_FORCE_INCREMENT);
    ```

4.  Call the `Query.setLockMode` or `TypedQuery.setLockMode` method,
    passing the lock mode as the parameter:
    
    ``` oac_no_warn
    Query q = em.createQuery(...);
    q.setLockMode(LockModeType.PESSIMISTIC_FORCE_INCREMENT);
    ```

5.  Add a `lockMode` element to the `@NamedQuery` annotation:
    
    ``` oac_no_warn
    @NamedQuery(name="lockPersonQuery",
      query="SELECT p FROM Person p WHERE p.name LIKE :name",
      lockMode=PESSIMISTIC_READ)
    ```

## 42.2.2 Using Pessimistic Locking

Versioned entities, as well as entities that do not have version
attributes, can be locked pessimistically.

To lock entities pessimistically, set the lock mode to
`PESSIMISTIC_READ`, `PESSIMISTIC_WRITE`, or
`PESSIMISTIC_FORCE_INCREMENT`.

If a pessimistic lock cannot be obtained on the database rows, and the
failure to lock the data results in a transaction rollback, a
`PessimisticLockException` is thrown. If a pessimistic lock cannot be
obtained, but the locking failure doesn't result in a transaction
rollback, a `LockTimeoutException` is thrown.

Pessimistically locking a versioned entity with
`PESSIMISTIC_FORCE_INCREMENT` results in the version attribute being
incremented even if the entity data is unmodified. When pessimistically
locking a versioned entity, the persistence provider will perform the
version checks that occur during optimistic locking, and if the version
check fails, an `OptimisticLockException` will be thrown. An attempt to
lock a non-versioned entity with `PESSIMISTIC_FORCE_INCREMENT` is not
portable and may result in a `PersistenceException` if the persistence
provider does not support optimistic locks for non-versioned entities.
Locking a versioned entity with `PESSIMISTIC_WRITE` results in the
version attribute being incremented if the transaction was successfully
committed.

### 42.2.2.1 Pessimistic Locking Timeouts

Use the `javax.persistence.lock.timeout` property to specify the length
of time in milliseconds the persistence provider should wait to obtain a
lock on the database tables. If the time it takes to obtain a lock
exceeds the value of this property, a `LockTimeoutException` will be
thrown, but the current transaction will not be marked for rollback. If
you set this property to `0`, the persistence provider should throw a
`LockTimeoutException` if it cannot immediately obtain a lock.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
Portable applications should not rely on the setting of <code dir="ltr">javax.persistence.lock.timeout</code>, because the locking strategy and underlying database may mean that the timeout value cannot be used. The value of <code dir="ltr">javax.persistence.lock.timeout</code> is a hint, not a contract.</td>
</tr>
</tbody>
</table>

  

This property may be set programmatically by passing it to the
`EntityManager` methods that allow lock modes to be specified, the
`Query.setLockMode` and `TypedQuery.setLockMode` methods, the
`@NamedQuery` annotation, and the
`Persistence.createEntityManagerFactory` method. It may also be set as a
property in the `persistence.xml` deployment descriptor.

If `javax.persistence.lock.timeout` is set in multiple places, the value
will be determined in the following order:

1.  The argument to one of the `EntityManager` or `Query` methods

2.  The setting in the `@NamedQuery` annotation

3.  The argument to the `Persistence.createEntityManagerFactory` method

4.  The value in the `persistence.xml` deployment descriptor

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
<td><a href="persistence-locking001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-entitygraphs.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
