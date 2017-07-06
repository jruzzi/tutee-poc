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
<td><a href="concurrency-utilities002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="concurrency-utilities004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 56.3 Concurrency and Transactions

The most basic operations for transactions are commit and rollback, but,
in a distributed environment with concurrent processing, it can be
difficult to guarantee that commit or rollback operations will be
successfully processed, and the transaction can be spread among
different threads, CPU cores, physical machines, and networks.

Ensuring that a rollback operation will successfully execute in such a
scenario is crucial. Concurrency Utilities relies on the Java
Transaction API (JTA) to implement and support transactions on its
components through `javax.transaction.UserTransaction`, allowing
application developers to explicitly manage transaction boundaries. More
information is available in the JTA specification.

Optionally, context objects can begin, commit, or roll back
transactions, but these objects cannot enlist in parent component
transactions.

The following code snippet illustrates a `Runnable` task that obtains a
`UserTransaction` and then starts and commits a transaction while
interacting with other transactional components, such as an enterprise
bean and a database:

``` oac_no_warn
public class MyTransactionalTask implements Runnable {
 
   UserTransaction ut = ... // obtained through JNDI or injection
 
   public void run() {
 
       // Start a transaction
       ut.begin();
 
       // Invoke a Service or an EJB
       myEJB.businessMethod();
 
       // Update a database entity using an XA JDBC driver
       myEJB.updateCustomer(customer);
 
       // Commit the transaction
       ut.commit();
 
   }
} 
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
<td><a href="concurrency-utilities002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="concurrency-utilities004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
