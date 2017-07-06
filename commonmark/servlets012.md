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
<td><a href="servlets011.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets013.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.12 Asynchronous Processing

Web containers in application servers normally use a server thread per
client request. Under heavy load conditions, containers need a large
amount of threads to serve all the client requests. Scalability
limitations include running out of memory or exhausting the pool of
container threads. To create scalable web applications, you must ensure
that no threads associated with a request are sitting idle, so the
container can use them to process new requests.

There are two common scenarios in which a thread associated with a
request can be sitting idle.

  - The thread needs to wait for a resource to become available or
    process data before building the response. For example, an
    application may need to query a database or access data from a
    remote web service before generating the response.

  - The thread needs to wait for an event before generating the
    response. For example, an application may have to wait for a JMS
    message, new information from another client, or new data available
    in a queue before generating the response.

These scenarios represent blocking operations that limit the scalability
of web applications. Asynchronous processing refers to assigning these
blocking operations to a new thread and retuning the thread associated
with the request immediately to the container.

## 17.12.1 Asynchronous Processing in Servlets

Java EE provides asynchronous processing support for servlets and
filters. If a servlet or a filter reaches a potentially blocking
operation when processing a request, it can assign the operation to an
asynchronous execution context and return the thread associated with the
request immediately to the container without generating a response. The
blocking operation completes in the asynchronous execution context in a
different thread, which can generate a response or dispatch the request
to another servlet.

To enable asynchronous processing on a servlet, set the parameter
`asyncSupported` to `true` on the `@WebServlet` annotation as follows:

``` oac_no_warn
@WebServlet(urlPatterns={"/asyncservlet"}, asyncSupported=true)
public class AsyncServlet extends HttpServlet { ... }
```

The `javax.servlet.AsyncContext` class provides the functionality that
you need to perform asynchronous processing inside service methods. To
obtain an instance of `AsyncContext`, call the `startAsync()` method on
the request object of your service method; for example:

``` oac_no_warn
public void doGet(HttpServletRequest req, HttpServletResponse resp) {
   ...
   AsyncContext acontext = req.startAsync();
   ...
}
```

This call puts the request into asynchronous mode and ensures that the
response is not committed after exiting the service method. You have to
generate the response in the asynchronous context after the blocking
operation completes or dispatch the request to another servlet.

[Table 17-3](#BEICFIEC) describes the basic functionality provided by
the `AsyncContext` class.

Table 17-3 Functionality Provided by the AsyncContext Class

<table style="width:38%;">
<colgroup>
<col width="38%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Method Signature</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">void start(Runnable run)</code></p></td>
<td><p>The container provides a different thread in which the blocking operation can be processed.</p>
<p>You provide code for the blocking operation as a class that implements the <code dir="ltr">Runnable</code> interface. You can provide this class as an inner class when calling the <code dir="ltr">start</code> method or use another mechanism to pass the <code dir="ltr">AsyncContext</code> instance to your class.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">ServletRequest getRequest()</code></p></td>
<td><p>Returns the request used to initialize this asynchronous context. In the example above, the request is the same as in the service method.</p>
<p>You can use this method inside the asynchronous context to obtain parameters from the request.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ServletResponse getResponse()</code></p></td>
<td><p>Returns the response used to initialize this asynchronous context. In the example above, the response is the same as in the service method.</p>
<p>You can use this method inside the asynchronous context to write to the response with the results of the blocking operation.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">void complete()</code></p></td>
<td><p>Completes the asynchronous operation and closes the response associated with this asynchronous context.</p>
<p>You call this method after writing to the response object inside the asynchronous context.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">void dispatch(String path)</code></p></td>
<td><p>Dispatches the request and response objects to the given path.</p>
<p>You use this method to have another servlet write to the response after the blocking operation completes.</p></td>
</tr>
</tbody>
</table>

  

## 17.12.2 Waiting for a Resource

This section demonstrates how to use the functionality provided by the
`AsyncContext` class for the following use case:

1.  A servlet receives a parameter from a GET request.

2.  The servlet uses a resource, such as a database or a web service, to
    retrieve information based on the value of the parameter. The
    resource can be slow at times, so this may be a blocking operation.

3.  The servlet generates a response using the result from the resource.

The following code shows a basic servlet that does not use asynchronous
processing:

``` oac_no_warn
@WebServlet(urlPatterns={"/syncservlet"})
public class SyncServlet extends HttpServlet {
   private MyRemoteResource resource;
   @Override
   public void init(ServletConfig config) {
      resource = MyRemoteResource.create("config1=x,config2=y");
   }

   @Override
   public void doGet(HttpServletRequest request, 
                     HttpServletResponse response) {
      response.setContentType("text/html;charset=UTF-8");
      String param = request.getParameter("param");
      String result = resource.process(param);
      /* ... print to the response ... */
   }
}
```

The following code shows the same servlet using asynchronous processing:

``` oac_no_warn
@WebServlet(urlPatterns={"/asyncservlet"}, asyncSupported=true)
public class AsyncServlet extends HttpServlet {
   /* ... Same variables and init method as in SyncServlet ... */

   @Override
   public void doGet(HttpServletRequest request, 
                     HttpServletResponse response) {
      response.setContentType("text/html;charset=UTF-8");
      final AsyncContext acontext = request.startAsync();
      acontext.start(new Runnable() {
         public void run() {
            String param = acontext.getRequest().getParameter("param");
            String result = resource.process(param);
            HttpServletResponse response = acontext.getResponse();
            /* ... print to the response ... */
            acontext.complete();
   }
}
```

`AsyncServlet` adds `asyncSupported=true` to the `@WebServlet`
annotation. The rest of the differences are inside the service method.

  - `request.startAsync()` causes the request to be processed
    asynchronously; the response is not sent to the client at the end of
    the service method.

  - `acontext.start(new Runnable() {...})` gets a new thread from the
    container.

  - The code inside the `run()` method of the inner class executes in
    the new thread. The inner class has access to the asynchronous
    context to read parameters from the request and write to the
    response. Calling the `complete()` method of the asynchronous
    context commits the response and sends it to the client.

The service method of `AsyncServlet` returns immediately, and the
request is processed in the asynchronous context.

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
<td><a href="servlets011.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets013.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
