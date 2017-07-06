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
<td><a href="servlets002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.3 Sharing Information

Web components, like most objects, usually work with other objects to
accomplish their tasks. Web components can do so by doing the following.

  - Using private helper objects (for example, JavaBeans components).

  - Sharing objects that are attributes of a public scope.

  - Using a database.

  - Invoking other web resources. The Java Servlet technology mechanisms
    that allow a web component to invoke other web resources are
    described in [Invoking Other Web Resources](servlets007.htm#BNAGI).

## 17.3.1 Using Scope Objects

Collaborating web components share information by means of objects that
are maintained as attributes of four scope objects. You access these
attributes by using the `getAttribute` and `setAttribute` methods of the
class representing the scope. [Table 17-2](#BNAFQ) lists the scope
objects.

Table 17-2 Scope Objects

<table style="width:54%;">
<colgroup>
<col width="16%" />
<col width="38%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Scope Object</th>
<th>Class</th>
<th>Accessible From</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Web context</p></td>
<td><p><code dir="ltr">javax.servlet.ServletContext</code></p></td>
<td><p>Web components within a web context. See <a href="servlets008.htm#BNAGL">Accessing the Web Context</a>.</p></td>
</tr>
<tr class="even">
<td><p>Session</p></td>
<td><p><code dir="ltr">javax.servlet.http.HttpSession</code></p></td>
<td><p>Web components handling a request that belongs to the session. See <a href="servlets009.htm#BNAGM">Maintaining Client State</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Request</p></td>
<td><p>Subtype of <code dir="ltr">javax.servlet.ServletRequest</code></p></td>
<td><p>Web components handling the request.</p></td>
</tr>
<tr class="even">
<td><p>Page</p></td>
<td><p><code dir="ltr">javax.servlet.jsp.JspContext</code></p></td>
<td><p>The JSP page that creates the object.</p></td>
</tr>
</tbody>
</table>

  

## 17.3.2 Controlling Concurrent Access to Shared Resources

In a multithreaded server, shared resources can be accessed
concurrently. In addition to scope object attributes, shared resources
include in-memory data, such as instance or class variables, and
external objects, such as files, database connections, and network
connections.

Concurrent access can arise in several situations.

  - Multiple web components accessing objects stored in the web context.

  - Multiple web components accessing objects stored in a session.

  - Multiple threads within a web component accessing instance
    variables. A web container will typically create a thread to handle
    each request. To ensure that a servlet instance handles only one
    request at a time, a servlet can implement the `SingleThreadModel`
    interface. If a servlet implements this interface, no two threads
    will execute concurrently in the servlet's service method. A web
    container can implement this guarantee by synchronizing access to a
    single instance of the servlet or by maintaining a pool of web
    component instances and dispatching each new request to a free
    instance. This interface does not prevent synchronization problems
    that result from web components' accessing shared resources, such as
    static class variables or external objects.

When resources can be accessed concurrently, they can be used in an
inconsistent fashion. You prevent this by controlling the access using
the synchronization techniques described in the Threads lesson at
`http://docs.oracle.com/javase/tutorial/essential/concurrency/`.

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
<td><a href="servlets002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
