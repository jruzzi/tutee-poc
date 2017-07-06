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
<td><a href="ejb-intro002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-intro004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 32.3 What Is a Message-Driven Bean?

A message-driven bean is an enterprise bean that allows Java EE
applications to process messages asynchronously. This type of bean
normally acts as a JMS message listener, which is similar to an event
listener but receives JMS messages instead of events. The messages can
be sent by any Java EE component (an application client, another
enterprise bean, or a web component) or by a JMS application or system
that does not use Java EE technology. Message-driven beans can process
JMS messages or other kinds of messages.

The following topics are addressed here:

  - [Section 32.3.1, "What Makes Message-Driven Beans Different from
    Session Beans?"](#GIPMJ)

  - [Section 32.3.2, "When to Use Message-Driven Beans"](#GIPJX)

## 32.3.1 What Makes Message-Driven Beans Different from Session Beans?

The most visible difference between message-driven beans and session
beans is that clients do not access message-driven beans through
interfaces. Interfaces are described in the section [Accessing
Enterprise Beans](ejb-intro004.htm#GIPJF). Unlike a session bean, a
message-driven bean has only a bean class.

In several respects, a message-driven bean resembles a stateless session
bean.

  - A message-driven bean's instances retain no data or conversational
    state for a specific client.

  - All instances of a message-driven bean are equivalent, allowing the
    EJB container to assign a message to any message-driven bean
    instance. The container can pool these instances to allow streams of
    messages to be processed concurrently.

  - A single message-driven bean can process messages from multiple
    clients.

The instance variables of the message-driven bean instance can contain
some state across the handling of client messages, such as a JMS API
connection, an open database connection, or an object reference to an
enterprise bean object.

Client components do not locate message-driven beans and invoke methods
directly on them. Instead, a client accesses a message-driven bean
through, for example, JMS by sending messages to the message destination
for which the message-driven bean class is the `MessageListener`. You
assign a message-driven bean's destination during deployment by using
GlassFish Server resources.

Message-driven beans have the following characteristics.

  - They execute upon receipt of a single client message.

  - They are invoked asynchronously.

  - They are relatively short-lived.

  - They do not represent directly shared data in the database, but they
    can access and update this data.

  - They can be transaction-aware.

  - They are stateless.

When a message arrives, the container calls the message-driven bean's
`onMessage` method to process the message. The `onMessage` method
normally casts the message to one of the five JMS message types and
handles it in accordance with the application's business logic. The
`onMessage` method can call helper methods or can invoke a session bean
to process the information in the message or to store it in a database.

A message can be delivered to a message-driven bean within a transaction
context, so all operations within the `onMessage` method are part of a
single transaction. If message processing is rolled back, the message
will be redelivered. For more information, see [Receiving Messages
Asynchronously Using a Message-Driven Bean](jms-examples007.htm#BNBPK)
and [Chapter 51, "Transactions"](transactions.htm#BNCIH).

## 32.3.2 When to Use Message-Driven Beans

Session beans allow you to send JMS messages and to receive them
synchronously but not asynchronously. To avoid tying up server
resources, do not to use blocking synchronous receives in a server-side
component; in general, JMS messages should not be sent or received
synchronously. To receive messages asynchronously, use a message-driven
bean.

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
<td><a href="ejb-intro002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-intro004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
