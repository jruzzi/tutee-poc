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
<td><a href="websocket003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 18.4 Annotated Endpoints

The following example shows how to create the same endpoint from
[Programmatic Endpoints](websocket003.htm#BABGJEIG) using annotations
instead:

``` oac_no_warn
@ServerEndpoint("/echo")
public class EchoEndpoint {
   @OnMessage
   public void onMessage(Session session, String msg) {
      try {
         session.getBasicRemote().sendText(msg);
      } catch (IOException e) { ... }
   }
}
```

The annotated endpoint is simpler than the equivalent programmatic
endpoint, and it is deployed automatically with the application to the
relative path defined in the `ServerEndpoint` annotation. Instead of
having to create an additional class for the message handler, this
example uses the `OnMessage` annotation to designate the method invoked
to handle messages.

[Table 18-1](#BABDGEJH) lists the annotations available in the
`javax.websocket` package to designate the methods that handle lifecycle
events. The examples in the table show the most common parameters for
these methods. See the API reference for details on what combinations of
parameters are allowed in each case.

Table 18-1 WebSocket Endpoint Lifecycle Annotations

<table style="width:46%;">
<colgroup>
<col width="19%" />
<col width="27%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Annotation</th>
<th>Event</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">OnOpen</code></p></td>
<td><p>Connection opened</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@OnOpen
public void open(Session session, 
                 EndpointConfig conf) { }</code></pre></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">OnMessage</code></p></td>
<td><p>Message received</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@OnMessage
public void message(Session session, 
                    String msg) { }</code></pre></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">OnError</code></p></td>
<td><p>Connection error</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@OnError
public void error(Session session, 
                  Throwable error) { }</code></pre></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">OnClose</code></p></td>
<td><p>Connection closed</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@OnClose
public void close(Session session, 
                  CloseReason reason) { }</code></pre></td>
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
<td><a href="websocket003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
