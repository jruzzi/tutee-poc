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
<td><a href="websocket.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 18.1 Introduction to WebSocket

In the traditional request-response model used in HTTP, the client
requests resources, and the server provides responses. The exchange is
always initiated by the client; the server cannot send any data without
the client requesting it first. This model worked well for the World
Wide Web when clients made occasional requests for documents that
changed infrequently, but the limitations of this approach are
increasingly relevant as content changes quickly and users expect a more
interactive experience on the Web. The WebSocket protocol addresses
these limitations by providing a full-duplex communication channel
between the client and the server. Combined with other client
technologies, such as JavaScript and HTML5, WebSocket enables web
applications to deliver a richer user experience.

In a WebSocket application, the server publishes a WebSocket endpoint,
and the client uses the endpoint's URI to connect to the server. The
WebSocket protocol is symmetrical after the connection has been
established; the client and the server can send messages to each other
at any time while the connection is open, and they can close the
connection at any time. Clients usually connect only to one server, and
servers accept connections from multiple clients.

The WebSocket protocol has two parts: handshake and data transfer. The
client initiates the handshake by sending a request to a WebSocket
endpoint using its URI. The handshake is compatible with existing
HTTP-based infrastructure: web servers interpret it as an HTTP
connection upgrade request. An example handshake from a client looks
like this:

``` oac_no_warn
GET /path/to/websocket/endpoint HTTP/1.1
Host: localhost
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: xqBt3ImNzJbYqRINxEFlkg==
Origin: http://localhost
Sec-WebSocket-Version: 13
```

An example handshake from the server in response to the client looks
like this:

``` oac_no_warn
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: K7DJLdLooIwIG/MOpvWFB3y3FE8=
```

The server applies a known operation to the value of the
`Sec-WebSocket-Key` header to generate the value of the
`Sec-WebSocket-Accept` header. The client applies the same operation to
the value of the `Sec-WebSocket-Key` header, and the connection is
established successfully if the result matches the value received from
the server. The client and the server can send messages to each other
after a successful handshake.

WebSocket supports text messages (encoded as UTF-8) and binary messages.
The control frames in WebSocket are close, ping, and pong (a response to
a ping frame). Ping and pong frames may also contain application data.

WebSocket endpoints are represented by URIs that have the following
form:

``` oac_no_warn
ws://host:port/path?query
wss://host:port/path?query
```

The `ws` scheme represents an unencrypted WebSocket connection, and the
`wss` scheme represents an encrypted connection. The `port` component is
optional; the default port number is 80 for unencrypted connections and
443 for encrypted connections. The `path` component indicates the
location of an endpoint within a server. The `query` component is
optional.

Modern web browsers implement the WebSocket protocol and provide a
JavaScript API to connect to endpoints, send messages, and assign
callback methods for WebSocket events (such as opened connections,
received messages, and closed connections).

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
<td><a href="websocket.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
