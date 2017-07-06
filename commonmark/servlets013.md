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
<td><a href="servlets012.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets014.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.13 Nonblocking I/O

Web containers in application servers normally use a server thread per
client request. To develop scalable web applications, you must ensure
that threads associated with client requests are never sitting idle
waiting for a blocking operation to complete. [Asynchronous
Processing](servlets012.htm#BEIGCFDF) provides a mechanism to execute
application-specific blocking operations in a new thread, returning the
thread associated with the request immediately to the container. Even if
you use asynchronous processing for all the application-specific
blocking operations inside your service methods, threads associated with
client requests can be momentarily sitting idle because of input/output
considerations.

For example, if a client is submitting a large HTTP POST request over a
slow network connection, the server can read the request faster than the
client can provide it. Using traditional I/O, the container thread
associated with this request would be sometimes sitting idle waiting for
the rest of the request.

Java EE provides nonblocking I/O support for servlets and filters when
processing requests in asynchronous mode. The following steps summarize
how to use nonblocking I/O to process requests and write responses
inside service methods.

1.  Put the request in asynchronous mode as described in [Asynchronous
    Processing](servlets012.htm#BEIGCFDF).

2.  Obtain an input stream and/or an output stream from the request and
    response objects in the service method.

3.  Assign a read listener to the input stream and/or a write listener
    to the output stream.

4.  Process the request and the response inside the listener's callback
    methods.

[Table 17-4](#BEIFDICJ) and [Table 17-5](#BEIFIIIH) describe the methods
available in the servlet input and output streams for nonblocking I/O
support. [Table 17-6](#BEIFGJCG) describes the interfaces for read
listeners and write listeners.

Table 17-4 Nonblocking I/O Support in javax.servlet.ServletInputStream

<table style="width:50%;">
<colgroup>
<col width="50%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">void setReadListener(ReadListener rl)</code></p></td>
<td><p>Associates this input stream with a listener object that contains callback methods to read data asynchronously. You provide the listener object as an anonymous class or use another mechanism to pass the input stream to the read listener object.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">boolean isReady()</code></p></td>
<td><p>Returns true if data can be read without blocking.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">boolean isFinished()</code></p></td>
<td><p>Returns true when all the data has been read.</p></td>
</tr>
</tbody>
</table>

  

Table 17-5 Nonblocking I/O Support in javax.servlet.ServletOutputStream

<table style="width:50%;">
<colgroup>
<col width="0%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Method</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">void setWriteListener(WriteListener wl)</code></p></td>
<td><p>Associates this output stream with a listener object that contains callback methods to write data asynchronously. You provide the write listener object as an anonymous class or use another mechanism to pass the output stream to the write listener object.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">boolean isReady()</code></p></td>
<td><p>Returns true if data can be written without blocking.</p></td>
</tr>
</tbody>
</table>

  

Table 17-6 Listener Interfaces for Nonblocking I/O Support

<table style="width:52%;">
<colgroup>
<col width="19%" />
<col width="33%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Interface</th>
<th>Methods</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">ReadListener</code></p></td>
<td><p><code dir="ltr">void onDataAvailable()</code></p>
<p><code dir="ltr">void onAllDataRead()</code></p>
<p><code dir="ltr">void onError(Throwable t)</code></p></td>
<td><p>A <code dir="ltr">ServletInputStream</code> instance calls these methods on its listener when there is data available to read, when all the data has been read, or when there is an error.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">WriteListener</code></p></td>
<td><p><code dir="ltr">void onWritePossible()</code></p>
<p><code dir="ltr">void onError(Throwable t)</code></p></td>
<td><p>A <code dir="ltr">ServletOutputStream</code> instance calls these methods on its listener when it is possible to write data without blocking or when there is an error.</p></td>
</tr>
</tbody>
</table>

  

## 17.13.1 Reading a Large HTTP POST Request Using Nonblocking I/O

The code in this section shows how to read a large HTTP POST request
inside a servlet by putting the request in asynchronous mode (as
described in [Asynchronous Processing](servlets012.htm#BEIGCFDF)) and
using the nonblocking I/O functionality from [Table 17-4](#BEIFDICJ) and
[Table 17-6](#BEIFGJCG).

``` oac_no_warn
@WebServlet(urlPatterns={"/asyncioservlet"}, asyncSupported=true)
public class AsyncIOServlet extends HttpServlet {
   @Override
   public void doPost(HttpServletRequest request, 
                      HttpServletResponse response)
                      throws IOException {
      final AsyncContext acontext = request.startAsync();
      final ServletInputStream input = request.getInputStream();
      
      input.setReadListener(new ReadListener() {
         byte buffer[] = new byte[4*1024];
         StringBuilder sbuilder = new StringBuilder();
         @Override
         public void onDataAvailable() {
            try {
               do {
                  int length = input.read(buffer);
                  sbuilder.append(new String(buffer, 0, length));
               } while(input.isReady());
            } catch (IOException ex) { ... }
         }
         @Override
         public void onAllDataRead() {
            try {
               acontext.getResponse().getWriter()
                                     .write("...the response...");
            } catch (IOException ex) { ... }
            acontext.complete();
         }
         @Override
         public void onError(Throwable t) { ... }
      });
   }
}
```

This example declares the web servlet with asynchronous support using
the `@WebServlet` annotation parameter `asyncSupported=true`. The
service method first puts the request in asynchronous mode by calling
the `startAsync()` method of the request object, which is required in
order to use nonblocking I/O. Then, the service method obtains an input
stream associated with the request and assigns a read listener defined
as an inner class. The listener reads parts of the request as they
become available and then writes some response to the client when it
finishes reading the request.

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
<td><a href="servlets012.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets014.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
