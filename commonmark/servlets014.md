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
<td><a href="servlets013.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets015.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.14 Protocol Upgrade Processing

In HTTP/1.1, clients can request to switch to a different protocol on
the current connection by using the `Upgrade` header field. If the
server accepts the request to switch to the protocol indicated by the
client, it generates an HTTP response with status 101 (switching
protocols). After this exchange, the client and the server communicate
using the new protocol.

For example, a client can make an HTTP request to switch to the XYZP
protocol as follows:

``` oac_no_warn
GET /xyzpresource HTTP/1.1
Host: localhost:8080
Accept: text/html
Upgrade: XYZP
Connection: Upgrade
OtherHeaderA: Value
```

The client can specify parameters for the new protocol using HTTP
headers. The server can accept the request and generate a response as
follows:

``` oac_no_warn
HTTP/1.1 101 Switching Protocols
Upgrade: XYZP
Connection: Upgrade
OtherHeaderB: Value

(XYZP data)
```

Java EE supports the HTTP protocol upgrade functionality in servlets, as
described in [Table 17-7](#BEIBDHAG).

Table 17-7 Protocol Upgrade Support

<table style="width:31%;">
<colgroup>
<col width="31%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Class or Interface</th>
<th>Method</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">HttpServletRequest</code></p></td>
<td><p><code dir="ltr">HttpUpgradeHandler upgrade(Class handler)</code></p>
<p>The upgrade method starts the protocol upgrade processing. This method instantiates a class that implements the <code dir="ltr">HttpUpgradeHandler</code> interface and delegates the connection to it.</p>
<p>You call the <code dir="ltr">upgrade</code> method inside a service method when accepting a request from a client to switch protocols.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">HttpUpgradeHandler</code></p></td>
<td><p><code dir="ltr">void init(WebConnection wc)</code></p>
<p>The <code dir="ltr">init</code> method is called when the servlet accepts the request to switch protocols. You implement this method and obtain input and output streams from the <code dir="ltr">WebConnection</code> object to implement the new protocol.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">HttpUpgradeHandler</code></p></td>
<td><p><code dir="ltr">void destroy()</code></p>
<p>The <code dir="ltr">destroy</code> method is called when the client disconnects. You implement this method and free any resources associated with processing the new protocol.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">WebConnection</code></p></td>
<td><p><code dir="ltr">ServletInputStream getInputStream()</code></p>
<p>The <code dir="ltr">getInputStream</code> method provides access to the input stream of the connection. You can use <a href="servlets013.htm#BEIHICDH">Nonblocking I/O</a> with the returned stream to implement the new protocol.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">WebConnection</code></p></td>
<td><p><code dir="ltr">ServletOutputStream getOutputStream()</code></p>
<p>The <code dir="ltr">getOutputStream</code> method provides access to the output stream of the connection. You can use <a href="servlets013.htm#BEIHICDH">Nonblocking I/O</a> with the returned stream to implement the new protocol.</p></td>
</tr>
</tbody>
</table>

  

The following code demonstrates how to accept an HTTP protocol upgrade
request from a client:

``` oac_no_warn
@WebServlet(urlPatterns={"/xyzpresource"})
public class XYZPUpgradeServlet extends HttpServlet {
   @Override
   public void doGet(HttpServletRequest request, 
                     HttpServletResponse response) {
      if ("XYZP".equals(request.getHeader("Upgrade"))) {
         /* Accept upgrade request */
         response.setStatus(101);
         response.setHeader("Upgrade", "XYZP");
         response.setHeader("Connection", "Upgrade");
         response.setHeader("OtherHeaderB", "Value");
         /* Delegate the connection to the upgrade handler */
         XYZPUpgradeHandler = request.upgrade(XYZPUpgradeHandler.class);
         /* (the service method returns immedately) */
      } else {
         /* ... write error response ... */
      }
   }
}
```

The `XYZPUpgradeHandler` class handles the connection:

``` oac_no_warn
public class XYZPUpgradeHandler implements HttpUpgradeHandler {
   @Override
   public void init(WebConnection wc) {
      ServletInputStream input = wc.getInputStream();
      ServletOutputStream output = wc.getOutputStream();
      /* ... implement XYZP using these streams (protocol-specific) ... */
   }
   @Override
   public void destroy() { ... }
}
```

The class that implements `HttpUpgradeHandler` uses the streams from the
current connection to communicate with the client using the new
protocol. See the Servlet 3.1 specification at
`http://jcp.org/en/jsr/detail?id=340` for details on HTTP protocol
upgrade support.

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
<td><a href="servlets013.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets015.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
