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
<td><a href="transactions003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="transactions005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 51.4 Container-Managed Transactions

In an enterprise bean with container-managed transaction demarcation,
the EJB container sets the boundaries of the transactions. You can use
container-managed transactions with any type of enterprise bean: session
or message-driven. Container-managed transactions simplify development
because the enterprise bean code does not explicitly mark the
transaction's boundaries. The code does not include statements that
begin and end the transaction. By default, if no transaction demarcation
is specified, enterprise beans use container-managed transaction
demarcation.

Typically, the container begins a transaction immediately before an
enterprise bean method starts and commits the transaction just before
the method exits. Each method can be associated with a single
transaction. Nested or multiple transactions are not allowed within a
method.

Container-managed transactions do not require all methods to be
associated with transactions. When developing a bean, you can set the
transaction attributes to specify which of the bean's methods are
associated with transactions.

Enterprise beans that use container-managed transaction demarcation must
not use any transaction-management methods that interfere with the
container's transaction demarcation boundaries. Examples of such methods
are the `commit`, `setAutoCommit`, and `rollback` methods of
`java.sql.Connection` or the `commit` and `rollback` methods of
`javax.jms.Session`. If you require control over the transaction
demarcation, you must use application-managed transaction demarcation.

Enterprise beans that use container-managed transaction demarcation also
must not use the `javax.transaction.UserTransaction` interface.

## 51.4.1 Transaction Attributes

A transaction attribute controls the scope of a transaction. [Figure
51-1](#BNCIL) illustrates why controlling the scope is important. In the
diagram, `method-A` begins a transaction and then invokes `method-B` of
`Bean-2`. When `method-B` executes, does it run within the scope of the
transaction started by `method-A`, or does it execute with a new
transaction? The answer depends on the transaction attribute of
`method-B`.

Figure 51-1 Transaction Scope

![Description of Figure 51-1 follows](img/jeett_dt_050.png)  
[Description of "Figure 51-1 Transaction
Scope"](img_text/jeett_dt_050.htm)  
  

A transaction attribute can have one of the following values:

  - `Required`

  - `RequiresNew`

  - `Mandatory`

  - `NotSupported`

  - `Supports`

  - `Never`

### 51.4.1.1 Required Attribute

If the client is running within a transaction and invokes the enterprise
bean's method, the method executes within the client's transaction. If
the client is not associated with a transaction, the container starts a
new transaction before running the method.

The `Required` attribute is the implicit transaction attribute for all
enterprise bean methods running with container-managed transaction
demarcation. You typically do not set the `Required` attribute unless
you need to override another transaction attribute. Because transaction
attributes are declarative, you can easily change them later.

### 51.4.1.2 RequiresNew Attribute

If the client is running within a transaction and invokes the enterprise
bean's method, the container takes the following steps:

1.  Suspends the client's transaction

2.  Starts a new transaction

3.  Delegates the call to the method

4.  Resumes the client's transaction after the method completes

If the client is not associated with a transaction, the container starts
a new transaction before running the method.

You should use the `RequiresNew` attribute when you want to ensure that
the method always runs within a new transaction.

### 51.4.1.3 Mandatory Attribute

If the client is running within a transaction and invokes the enterprise
bean's method, the method executes within the client's transaction. If
the client is not associated with a transaction, the container throws a
`TransactionRequiredException`.

Use the `Mandatory` attribute if the enterprise bean's method must use
the transaction of the client.

### 51.4.1.4 NotSupported Attribute

If the client is running within a transaction and invokes the enterprise
bean's method, the container suspends the client's transaction before
invoking the method. After the method has completed, the container
resumes the client's transaction.

If the client is not associated with a transaction, the container does
not start a new transaction before running the method.

Use the `NotSupported` attribute for methods that don't need
transactions. Because transactions involve overhead, this attribute may
improve performance.

### 51.4.1.5 Supports Attribute

If the client is running within a transaction and invokes the enterprise
bean's method, the method executes within the client's transaction. If
the client is not associated with a transaction, the container does not
start a new transaction before running the method.

Because the transactional behavior of the method may vary, you should
use the `Supports` attribute with caution.

### 51.4.1.6 Never Attribute

If the client is running within a transaction and invokes the enterprise
bean's method, the container throws a `RemoteException`. If the client
is not associated with a transaction, the container does not start a new
transaction before running the method.

### 51.4.1.7 Summary of Transaction Attributes

[Table 51-1](#BNCIT) summarizes the effects of the transaction
attributes. Both the `T1` and the `T2` transactions are controlled by
the container. A `T1` transaction is associated with the client that
calls a method in the enterprise bean. In most cases, the client is
another enterprise bean. A `T2` transaction is started by the container
just before the method executes.

In the last column of [Table 51-1](#BNCIT), the word "None" means that
the business method does not execute within a transaction controlled by
the container. However, the database calls in such a business method
might be controlled by the transaction manager of the database
management system.

Table 51-1 Transaction Attributes and Scope

<table style="width:58%;">
<colgroup>
<col width="28%" />
<col width="28%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Transaction Attribute</th>
<th>Client's Transaction</th>
<th>Business Method's Transaction</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">Required</code></p></td>
<td><p>None</p></td>
<td><p>T2</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">Required</code></p></td>
<td><p>T1</p></td>
<td><p>T1</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">RequiresNew</code></p></td>
<td><p>None</p></td>
<td><p>T2</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">RequiresNew</code></p></td>
<td><p>T1</p></td>
<td><p>T2</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">Mandatory</code></p></td>
<td><p>None</p></td>
<td><p>Error</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">Mandatory</code></p></td>
<td><p>T1</p></td>
<td><p>T1</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">NotSupported</code></p></td>
<td><p>None</p></td>
<td><p>None</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">NotSupported</code></p></td>
<td><p>T1</p></td>
<td><p>None</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">Supports</code></p></td>
<td><p>None</p></td>
<td><p>None</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">Supports</code></p></td>
<td><p>T1</p></td>
<td><p>T1</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">Never</code></p></td>
<td><p>None</p></td>
<td><p>None</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">Never</code></p></td>
<td><p>T1</p></td>
<td><p>Error</p></td>
</tr>
</tbody>
</table>

  

### 51.4.1.8 Setting Transaction Attributes

Transaction attributes are specified by decorating the enterprise bean
class or method with a `javax.ejb.TransactionAttribute` annotation and
setting it to one of the `javax.ejb.TransactionAttributeType` constants.

If you decorate the enterprise bean class with `@TransactionAttribute`,
the specified `TransactionAttributeType` is applied to all the business
methods in the class. Decorating a business method with
`@TransactionAttribute` applies the `TransactionAttributeType` only to
that method. If a `@TransactionAttribute` annotation decorates both the
class and the method, the method `TransactionAttributeType` overrides
the class `TransactionAttributeType`.

The `TransactionAttributeType` constants shown in [Table 51-2](#GKCFD)
encapsulate the transaction attributes described earlier in this
section.

Table 51-2 TransactionAttributeType Constants

<table style="width:34%;">
<colgroup>
<col width="34%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Transaction Attribute</th>
<th>TransactionAttributeType Constant</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">Required</code></p></td>
<td><p><code dir="ltr">TransactionAttributeType.REQUIRED</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">RequiresNew</code></p></td>
<td><p><code dir="ltr">TransactionAttributeType.REQUIRES_NEW</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">Mandatory</code></p></td>
<td><p><code dir="ltr">TransactionAttributeType.MANDATORY</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">NotSupported</code></p></td>
<td><p><code dir="ltr">TransactionAttributeType.NOT_SUPPORTED</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">Supports</code></p></td>
<td><p><code dir="ltr">TransactionAttributeType.SUPPORTS</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">Never</code></p></td>
<td><p><code dir="ltr">TransactionAttributeType.NEVER</code></p></td>
</tr>
</tbody>
</table>

  

The following code snippet demonstrates how to use the
`@TransactionAttribute` annotation:

``` oac_no_warn
@TransactionAttribute(NOT_SUPPORTED)
@Stateful
public class TransactionBean implements Transaction {
...
    @TransactionAttribute(REQUIRES_NEW)
    public void firstMethod() {...}

    @TransactionAttribute(REQUIRED)
    public void secondMethod() {...}

    public void thirdMethod() {...}

    public void fourthMethod() {...}
}
```

In this example, the `TransactionBean` class's transaction attribute has
been set to `NotSupported`, `firstMethod` has been set to `RequiresNew`,
and `secondMethod` has been set to `Required`. Because a
`@TransactionAttribute` set on a method overrides the class
`@TransactionAttribute`, calls to `firstMethod` will create a new
transaction, and calls to `secondMethod` will either run in the current
transaction or start a new transaction. Calls to `thirdMethod` or
`fourthMethod` do not take place within a transaction.

## 51.4.2 Rolling Back a Container-Managed Transaction

There are two ways to roll back a container-managed transaction. First,
if a system exception is thrown, the container will automatically roll
back the transaction. Second, by invoking the `setRollbackOnly` method
of the `EJBContext` interface, the bean method instructs the container
to roll back the transaction. If the bean throws an application
exception, the rollback is not automatic but can be initiated by a call
to `setRollbackOnly`.

## 51.4.3 Synchronizing a Session Bean's Instance Variables

The `SessionSynchronization` interface, which is optional, allows
stateful session bean instances to receive transaction synchronization
notifications. For example, you could synchronize the instance variables
of an enterprise bean with their corresponding values in the database.
The container invokes the `SessionSynchronization` methods
(`afterBegin`, `beforeCompletion`, and `afterCompletion`) at each of the
main stages of a transaction.

The `afterBegin` method informs the instance that a new transaction has
begun. The container invokes `afterBegin` immediately before it invokes
the business method.

The container invokes the `beforeCompletion` method after the business
method has finished but just before the transaction commits. The
`beforeCompletion` method is the last opportunity for the session bean
to roll back the transaction (by calling `setRollbackOnly`).

The `afterCompletion` method indicates that the transaction has
completed. This method has a single `boolean` parameter whose value is
`true` if the transaction was committed and `false` if it was rolled
back.

## 51.4.4 Methods Not Allowed in Container-Managed Transactions

You should not invoke any method that might interfere with the
transaction boundaries set by the container. The following methods are
prohibited:

  - The `commit`, `setAutoCommit`, and `rollback` methods of
    `java.sql.Connection`

  - The `getUserTransaction` method of `javax.ejb.EJBContext`

  - Any method of `javax.transaction.UserTransaction`

You can, however, use these methods to set boundaries in
application-managed transactions.

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
<td><a href="transactions003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="transactions005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
