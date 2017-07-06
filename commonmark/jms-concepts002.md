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
<td><a href="jms-concepts001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jms-concepts003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 45.2 Basic JMS API Concepts

This section introduces the most basic JMS API concepts, the ones you
must know to get started writing simple application clients that use the
JMS API.

The next section introduces the JMS API programming model. Later
sections cover more advanced concepts, including the ones you need in
order to write applications that use message-driven beans.

The following topics are addressed here:

  - [Section 45.2.1, "JMS API Architecture"](#BNCDY)

  - [Section 45.2.2, "Messaging Styles"](#BNCEA)

  - [Section 45.2.3, "Message Consumption"](#BNCEG)

## 45.2.1 JMS API Architecture

A JMS application is composed of the following parts.

  - A JMS provider is a messaging system that implements the JMS
    interfaces and provides administrative and control features. An
    implementation of the Java EE platform that supports the full
    profile includes a JMS provider.

  - JMS clients are the programs or components, written in the Java
    programming language, that produce and consume messages. Any Java EE
    application component can act as a JMS client.
    
    Java SE applications can also act as JMS clients; the Message Queue
    Developer's Guide for Java Clients in the GlassFish Server
    documentation (`https://glassfish.java.net/docs/`) explains how to
    make this work.

  - Messages are the objects that communicate information between JMS
    clients.

  - Administered objects are JMS objects configured for the use of
    clients. The two kinds of JMS administered objects are destinations
    and connection factories, described in [JMS Administered
    Objects](jms-concepts003.htm#BNCEJ). An administrator can create
    objects that are available to all applications that use a particular
    installation of GlassFish Server; alternatively, a developer can use
    annotations to create objects that are specific to a particular
    application.

[Figure 45-2](#BNCDZ) illustrates the way these parts interact.
Administrative tools or annotations allow you to bind destinations and
connection factories into a JNDI namespace. A JMS client can then use
resource injection to access the administered objects in the namespace
and then establish a logical connection to the same objects through the
JMS provider.

Figure 45-2 JMS API Architecture

![Description of Figure 45-2 follows](img/jeett_dt_027.png)  
[Description of "Figure 45-2 JMS API
Architecture"](img_text/jeett_dt_027.htm)  
  

## 45.2.2 Messaging Styles

Before the JMS API existed, most messaging products supported either the
point-to-point or the publish/subscribe style of messaging. The JMS
specification defines compliance for each style. A JMS provider must
implement both styles, and the JMS API provides interfaces that are
specific to each. The following subsections describe these messaging
styles.

The JMS API, however, makes it unnecessary to use only one of the two
styles. It allows you to use the same code to send and receive messages
using either the PTP or the pub/sub style. The destinations you use
remain specific to one style, and the behavior of the application will
depend in part on whether you are using a queue or a topic. However, the
code itself can be common to both styles, making your applications
flexible and reusable. This tutorial describes and illustrates this
coding approach, using the greatly simplified API provided by JMS 2.0.

### 45.2.2.1 Point-to-Point Messaging Style

A point-to-point (PTP) product or application is built on the concept of
message queues, senders, and receivers. Each message is addressed to a
specific queue, and receiving clients extract messages from the queues
established to hold their messages. Queues retain all messages sent to
them until the messages are consumed or expire.

PTP messaging, illustrated in [Figure 45-3](#BNCEC), has the following
characteristics.

  - Each message has only one consumer.

  - The receiver can fetch the message whether or not it was running
    when the client sent the message.

Figure 45-3 Point-to-Point Messaging

![Description of Figure 45-3 follows](img/jeett_dt_028.png)  
[Description of "Figure 45-3 Point-to-Point
Messaging"](img_text/jeett_dt_028.htm)  
  

Use PTP messaging when every message you send must be processed
successfully by one consumer.

### 45.2.2.2 Publish/Subscribe Messaging Style

In a publish/subscribe (pub/sub) product or application, clients address
messages to a topic, which functions somewhat like a bulletin board.
Publishers and subscribers can dynamically publish or subscribe to the
topic. The system takes care of distributing the messages arriving from
a topic's multiple publishers to its multiple subscribers. Topics retain
messages only as long as it takes to distribute them to subscribers.

With pub/sub messaging, it is important to distinguish between the
consumer that subscribes to a topic (the subscriber) and the
subscription that is created. The consumer is a JMS object within an
application, while the subscription is an entity within the JMS
provider. Normally, a topic can have many consumers, but a subscription
has only one subscriber. It is possible, however, to create shared
subscriptions; see [Creating Shared
Subscriptions](jms-concepts003.htm#BABJCIGJ) for details. See [Consuming
Messages from Topics](jms-concepts003.htm#BABEEJJJ) for details on the
semantics of pub/sub messaging.

Pub/sub messaging has the following characteristics.

  - Each message can have multiple consumers.

  - A client that subscribes to a topic can consume only messages sent
    after the client has created a subscription, and the consumer must
    continue to be active in order for it to consume messages.
    
    The JMS API relaxes this requirement to some extent by allowing
    applications to create durable subscriptions, which receive messages
    sent while the consumers are not active. Durable subscriptions
    provide the flexibility and reliability of queues but still allow
    clients to send messages to many recipients. For more information
    about durable subscriptions, see [Creating Durable
    Subscriptions](jms-concepts003.htm#BNCGD).

Use pub/sub messaging when each message can be processed by any number
of consumers (or none). [Figure 45-4](#BNCEE) illustrates pub/sub
messaging.

Figure 45-4 Publish/Subscribe Messaging

![Description of Figure 45-4 follows](img/jeett_dt_029.png)  
[Description of "Figure 45-4 Publish/Subscribe
Messaging"](img_text/jeett_dt_029.htm)  
  

## 45.2.3 Message Consumption

Messaging products are inherently asynchronous: There is no fundamental
timing dependency between the production and the consumption of a
message. However, the JMS specification uses this term in a more precise
sense. Messages can be consumed in either of two ways.

  - Synchronously: A consumer explicitly fetches the message from the
    destination by calling the `receive` method. The `receive` method
    can block until a message arrives or can time out if a message does
    not arrive within a specified time limit.

  - Asynchronously: An application client or a Java SE client can
    register a message listener with a consumer. A message listener is
    similar to an event listener. Whenever a message arrives at the
    destination, the JMS provider delivers the message by calling the
    listener's `onMessage` method, which acts on the contents of the
    message. In a Java EE application, a message-driven bean serves as a
    message listener (it too has an `onMessage` method), but a client
    does not need to register it with a consumer.

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
<td><a href="jms-concepts001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jms-concepts003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
