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
<td><a href="transactions006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="transactions008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 51.7 Updating Multiple Databases

The Java EE transaction manager controls all enterprise bean
transactions except for bean-managed JDBC transactions. The Java EE
transaction manager allows an enterprise bean to update multiple
databases within a transaction. [Figure 51-2](#BNCJE) and [Figure
51-3](#BNCJF) show two scenarios for updating multiple databases in a
single transaction.

In [Figure 51-2](#BNCJE), the client invokes a business method in
`Bean-A`. The business method begins a transaction, updates Database X,
updates Database Y, and invokes a business method in `Bean-B`. The
second business method updates Database Z and returns control to the
business method in `Bean-A`, which commits the transaction. All three
database updates occur in the same transaction.

In [Figure 51-3](#BNCJF), the client calls a business method in
`Bean-A`, which begins a transaction and updates Database X. Then
`Bean-A` invokes a method in `Bean-B`, which resides in a remote Java EE
server. The method in `Bean-B` updates Database Y. The transaction
managers of the Java EE servers ensure that both databases are updated
in the same transaction.

Figure 51-2 Updating Multiple Databases

![Description of Figure 51-2 follows](img/jeett_dt_051.png)  
[Description of "Figure 51-2 Updating Multiple
Databases"](img_text/jeett_dt_051.htm)  
  

Figure 51-3 Updating Multiple Databases Across Java EE Servers

![Description of Figure 51-3 follows](img/jeett_dt_052.png)  
[Description of "Figure 51-3 Updating Multiple Databases Across Java EE
Servers"](img_text/jeett_dt_052.htm)  
  

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
<td><a href="transactions006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="transactions008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
