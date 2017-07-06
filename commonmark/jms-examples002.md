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
<td><a href="jms-examples001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jms-examples003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 46.2 Overview of the JMS Examples

The following tables list the examples used in this chapter, describe
what they do, and link to the section that describes them fully. The
example directory for each example is relative to the
tut-install`/examples/jms/` directory.

Table 46-1 JMS Examples That Show the Use of Java EE Application Clients

<table style="width:37%;">
<colgroup>
<col width="37%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Example Directory</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">simple/producer</code></p></td>
<td><p>Using an application client to send messages; see <a href="jms-examples003.htm#BABIHCAE">Sending Messages</a></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">simple/synchconsumer</code></p></td>
<td><p>Using an application client to receive messages synchronously; see <a href="jms-examples003.htm#BNCFB">Receiving Messages Synchronously</a></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">simple/asynchconsumer</code></p></td>
<td><p>Using an application client to receive messages asynchronously; see <a href="jms-examples003.htm#BNCFH">Using a Message Listener for Asynchronous Message Delivery</a></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">simple/messagebrowser</code></p></td>
<td><p>Using an application client to use a <code dir="ltr">QueueBrowser</code> to browse a queue; see <a href="jms-examples003.htm#BNCFL">Browsing Messages on a Queue</a></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">simple/clientackconsumer</code></p></td>
<td><p>Using an application client to acknowledge messages received synchronously; see <a href="jms-examples003.htm#BNCFX">Acknowledging Messages</a></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">durablesubscriptionexample</code></p></td>
<td><p>Using an application client to create a durable subscription on a topic; see <a href="jms-examples004.htm#BNCGG">Using Durable Subscriptions</a></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">transactedexample</code></p></td>
<td><p>Using an application client to send and receive messages in local transactions (also uses request-reply messaging); see <a href="jms-examples004.htm#BNCGJ">Using Local Transactions</a></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">shared/sharedconsumer</code></p></td>
<td><p>Using an application client to create shared nondurable topic subscriptions; see <a href="jms-examples005.htm#BABIBEAC">Using Shared Nondurable Subscriptions</a></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">shared/shareddurableconsumer</code></p></td>
<td><p>Using an application client to create shared durable topic subscriptions; see <a href="jms-examples005.htm#BABEJBHA">Using Shared Durable Subscriptions</a></p></td>
</tr>
</tbody>
</table>

  

Table 46-2 JMS Examples That Show the Use of Java EE Web and EJB
Components

<table style="width:27%;">
<colgroup>
<col width="27%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Example Directory</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">websimplemessage</code></p></td>
<td><p>Using managed beans to send messages and to receive messages synchronously; see <a href="jms-examples006.htm#BABBABFC">Sending and Receiving Messages Using a Simple Web Application</a></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">simplemessage</code></p></td>
<td><p>Using an application client to send messages, and using a message-driven bean to receive messages asynchronously; see <a href="jms-examples007.htm#BNBPK">Receiving Messages Asynchronously Using a Message-Driven Bean</a></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">clientsessionmdb</code></p></td>
<td><p>Using a session bean to send messages, and using a message-driven bean to receive messages; see <a href="jms-examples008.htm#BNCGW">Sending Messages from a Session Bean to an MDB</a></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">clientmdbentity</code></p></td>
<td><p>Using an application client, two message-driven beans, and JPA persistence to create a simple HR application; see <a href="jms-examples009.htm#BNCHF">Using an Entity to Join Messages from Two MDBs</a></p></td>
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
<td><a href="jms-examples001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jms-examples003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
