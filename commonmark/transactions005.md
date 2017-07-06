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
<td><a href="transactions004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="transactions006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 51.5 Bean-Managed Transactions

In bean-managed transaction demarcation, the code in the session or
message-driven bean explicitly marks the boundaries of the transaction.
Although beans with container-managed transactions require less coding,
they have one limitation: When a method is executing, it can be
associated with either a single transaction or no transaction at all. If
this limitation will make coding your bean difficult, you should
consider using bean-managed transactions.

The following pseudocode illustrates the kind of fine-grained control
you can obtain with application-managed transactions. By checking
various conditions, the pseudocode decides whether to start or stop
certain transactions within the business method:

``` oac_no_warn
begin transaction
...
    update table-a
...
    if (condition-x)
   commit transaction
    else if (condition-y)
   update table-b
   commit transaction
    else
   rollback transaction
   begin transaction
   update table-c
   commit transaction
```

When coding an application-managed transaction for session or
message-driven beans, you must decide whether to use Java Database
Connectivity or JTA transactions. The sections that follow discuss both
types of transactions.

## 51.5.1 JTA Transactions

JTA, or the Java Transaction API, allows you to demarcate transactions
in a manner that is independent of the transaction manager
implementation. GlassFish Server implements the transaction manager with
the Java Transaction Service (JTS). However, your code doesn't call the
JTS methods directly but instead invokes the JTA methods, which then
call the lower-level JTS routines.

A JTA transaction is controlled by the Java EE transaction manager. You
may want to use a JTA transaction because it can span updates to
multiple databases from different vendors. A particular DBMS's
transaction manager may not work with heterogeneous databases. However,
the Java EE transaction manager does have one limitation: It does not
support nested transactions. In other words, it cannot start a
transaction for an instance until the preceding transaction has ended.

To demarcate a JTA transaction, you invoke the `begin`, `commit`, and
`rollback` methods of the `javax.transaction.UserTransaction` interface.

## 51.5.2 Returning without Committing

In a stateless session bean with bean-managed transactions, a business
method must commit or roll back a transaction before returning. However,
a stateful session bean does not have this restriction.

In a stateful session bean with a JTA transaction, the association
between the bean instance and the transaction is retained across
multiple client calls. Even if each business method called by the client
opens and closes the database connection, the association is retained
until the instance completes the transaction.

In a stateful session bean with a JDBC transaction, the JDBC connection
retains the association between the bean instance and the transaction
across multiple calls. If the connection is closed, the association is
not retained.

## 51.5.3 Methods Not Allowed in Bean-Managed Transactions

Do not invoke the `getRollbackOnly` and `setRollbackOnly` methods of the
`EJBContext` interface in bean-managed transactions. These methods
should be used only in container-managed transactions. For bean-managed
transactions, invoke the `getStatus` and `rollback` methods of the
`UserTransaction` interface.

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
<td><a href="transactions004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="transactions006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
