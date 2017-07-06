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
<td><a href="servlets018.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 18 Java API for WebSocket

This chapter describes the Java API for WebSocket (JSR 356), which
provides support for creating WebSocket applications. WebSocket is an
application protocol that provides full-duplex communications between
two peers over the TCP protocol.

The following topics are addressed here:

  - [Introduction to WebSocket](websocket001.htm#BABDABHF)

  - [Creating WebSocket Applications in the Java EE
    Platform](websocket002.htm#BABEAEFC)

  - [Programmatic Endpoints](websocket003.htm#BABGJEIG)

  - [Annotated Endpoints](websocket004.htm#BABFEBGA)

  - [Sending and Receiving Messages](websocket005.htm#BABFCGBJ)

  - [Maintaining Client State](websocket006.htm#BABGJCAD)

  - [Using Encoders and Decoders](websocket007.htm#BABGADFG)

  - [Path Parameters](websocket008.htm#BABEJIJI)

  - [Handling Errors](websocket009.htm#BABDEJHB)

  - [Specifying an Endpoint Configurator
    Class](websocket010.htm#BABJAIGH)

  - [The dukeetf2 Example Application](websocket011.htm#BABGCEHE)

  - [The websocketbot Example Application](websocket012.htm#BABCDBBC)

  - [Further Information about WebSocket](websocket013.htm#BABDFIFD)

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
<td><a href="servlets018.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
