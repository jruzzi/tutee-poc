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
<td><a href="websocket004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 18.5 Sending and Receiving Messages

WebSocket endpoints can send and receive text and binary messages. In
addition, they can also send ping frames and receive pong frames. This
section describes how to use the `Session` and `RemoteEndpoint`
interfaces to send messages to the connected peer and how to use the
`OnMessage` annotation to receive messages from it.

The following topics are addressed here:

  - [Section 18.5.1, "Sending Messages"](#CIHEHFCB)

  - [Section 18.5.2, "Receiving Messages"](#CIHIDFHD)

## 18.5.1 Sending Messages

Follow these steps to send messages in an endpoint.

1.  Obtain the `Session` object from the connection.
    
    The `Session` object is available as a parameter in the annotated
    lifecycle methods of the endpoint, like those in [Table
    18-1](websocket004.htm#BABDGEJH). When your message is a response to
    a message from the peer, you have the `Session` object available
    inside the method that received the message (the method annotated
    with `@OnMessage`). If you have to send messages that are not
    responses, store the `Session` object as an instance variable of the
    endpoint class in the method annotated with `@OnOpen` so that you
    can access it from other methods.

2.  Use the `Session` object to obtain a `RemoteEndpoint` object.
    
    The `Session.getBasicRemote` method and the `Session.getAsyncRemote`
    method return `RemoteEndpoint.Basic` and `RemoteEndpoint.Async`
    objects respectively. The `RemoteEndpoint.Basic` interface provides
    blocking methods to send messages; the `RemoteEndpoint.Async`
    interface provides nonblocking methods.

3.  Use the `RemoteEndpoint` object to send messages to the peer.
    
    The following list shows some of the methods you can use to send
    messages to the peer.
    
      - `void RemoteEndpoint.Basic.sendText(String text)`
        
        Send a text message to the peer. This method blocks until the
        whole message has been transmitted.
    
      - `void RemoteEndpoint.Basic.sendBinary(ByteBuffer data)`
        
        Send a binary message to the peer. This method blocks until the
        whole message has been transmitted.
    
      - `void RemoteEndpoint.sendPing(ByteBuffer appData)`
        
        Send a ping frame to the peer.
    
      - `void RemoteEndpoint.sendPong(ByteBuffer appData)`
        
        Send a pong frame to the peer.

The example in [Annotated Endpoints](websocket004.htm#BABFEBGA)
demonstrates how to use this procedure to reply to every incoming text
message.

### 18.5.1.1 Sending Messages to All Peers Connected to an Endpoint

Each instance of an endpoint class is associated with one and only one
connection and peer; however, there are cases in which an endpoint
instance needs to send messages to all connected peers. Examples include
chat applications and online auctions. The `Session` interface provides
the `getOpenSessions` method for this purpose. The following example
demonstrates how to use this method to forward incoming text messages to
all connected peers:

``` oac_no_warn
@ServerEndpoint("/echoall")
public class EchoAllEndpoint {
   @OnMessage
   public void onMessage(Session session, String msg) {
      try {
         for (Session sess : session.getOpenSessions()) {
            if (sess.isOpen())
               sess.getBasicRemote().sendText(msg);
         }
      } catch (IOException e) { ... }
   }
}
```

## 18.5.2 Receiving Messages

The `OnMessage` annotation designates methods that handle incoming
messages. You can have at most three methods annotated with `@OnMessage`
in an endpoint, one for each message type: text, binary, and pong. The
following example demonstrates how to designate methods to receive all
three types of messages:

``` oac_no_warn
@ServerEndpoint("/receive")
public class ReceiveEndpoint {
   @OnMessage
   public void textMessage(Session session, String msg) {
      System.out.println("Text message: " + msg);
   }
   @OnMessage
   public void binaryMessage(Session session, ByteBuffer msg) {
      System.out.println("Binary message: " + msg.toString());
   }
   @OnMessage
   public void pongMessage(Session session, PongMessage msg) {
      System.out.println("Pong message: " + 
                          msg.getApplicationData().toString());
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
<td><a href="websocket004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
