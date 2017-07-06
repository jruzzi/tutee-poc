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
<td><a href="servlets006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.7 Invoking Other Web Resources

Web components can invoke other web resources both indirectly and
directly. A web component indirectly invokes another web resource by
embedding a URL that points to another web component in content returned
to a client. While it is executing, a web component directly invokes
another resource by either including the content of another resource or
forwarding a request to another resource.

To invoke a resource available on the server that is running a web
component, you must first obtain a `RequestDispatcher` object by using
the `getRequestDispatcher("URL")` method. You can get a
`RequestDispatcher` object from either a request or the web context;
however, the two methods have slightly different behavior. The method
takes the path to the requested resource as an argument. A request can
take a relative path (that is, one that does not begin with a `/`), but
the web context requires an absolute path. If the resource is not
available or if the server has not implemented a `RequestDispatcher`
object for that type of resource, `getRequestDispatcher` will return
null. Your servlet should be prepared to deal with this condition.

## 17.7.1 Including Other Resources in the Response

It is often useful to include another web resource, such as banner
content or copyright information, in the response returned from a web
component. To include another resource, invoke the `include` method of a
`RequestDispatcher` object:

``` oac_no_warn
include(request, response);
```

If the resource is static, the `include` method enables programmatic
server-side includes. If the resource is a web component, the effect of
the method is to send the request to the included web component, execute
the web component, and then include the result of the execution in the
response from the containing servlet. An included web component has
access to the request object but is limited in what it can do with the
response object.

  - It can write to the body of the response and commit a response.

  - It cannot set headers or call any method, such as `setCookie`, that
    affects the headers of the response.

## 17.7.2 Transferring Control to Another Web Component

In some applications, you might want to have one web component do
preliminary processing of a request and have another component generate
the response. For example, you might want to partially process a request
and then transfer to another component, depending on the nature of the
request.

To transfer control to another web component, you invoke the `forward`
method of a `RequestDispatcher`. When a request is forwarded, the
request URL is set to the path of the forwarded page. The original URI
and its constituent parts are saved as the following request attributes:

``` oac_no_warn
javax.servlet.forward.request_uri
javax.servlet.forward.context_path
javax.servlet.forward.servlet_path
javax.servlet.forward.path_info
javax.servlet.forward.query_string
```

The `forward` method should be used to give another resource
responsibility for replying to the user. If you have already accessed a
`ServletOutputStream` or `PrintWriter` object within the servlet, you
cannot use this method; doing so throws an `IllegalStateException`.

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
<td><a href="servlets006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
