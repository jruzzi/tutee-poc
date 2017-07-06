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
<td><a href="servlets001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.2 Servlet Lifecycle

The lifecycle of a servlet is controlled by the container in which the
servlet has been deployed. When a request is mapped to a servlet, the
container performs the following steps.

1.  If an instance of the servlet does not exist, the web container:
    
    1.  Loads the servlet class
    
    2.  Creates an instance of the servlet class
    
    3.  Initializes the servlet instance by calling the `init` method
        (initialization is covered in [Creating and Initializing a
        Servlet](servlets004.htm#BNAFU))

2.  The container invokes the `service` method, passing request and
    response objects. Service methods are discussed in [Writing Service
    Methods](servlets005.htm#BNAFV).

If it needs to remove the servlet, the container finalizes the servlet
by calling the servlet's `destroy` method. For more information, see
[Finalizing a Servlet](servlets010.htm#BNAGS).

## 17.2.1 Handling Servlet Lifecycle Events

You can monitor and react to events in a servlet's lifecycle by defining
listener objects whose methods get invoked when lifecycle events occur.
To use these listener objects, you must define and specify the listener
class.

### 17.2.1.1 Defining the Listener Class

You define a listener class as an implementation of a listener
interface. [Table 17-1](#BNAFL) lists the events that can be monitored
and the corresponding interface that must be implemented. When a
listener method is invoked, it is passed an event that contains
information appropriate to the event. For example, the methods in the
`HttpSessionListener` interface are passed an `HttpSessionEvent`, which
contains an `HttpSession`.

Table 17-1 Servlet Lifecycle Events

<table style="width:40%;">
<colgroup>
<col width="18%" />
<col width="22%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Object</th>
<th>Event</th>
<th>Listener Interface and Event Class</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Web context</p></td>
<td><p>Initialization and destruction</p></td>
<td><p><code dir="ltr">javax.servlet.ServletContextListener</code> and <code dir="ltr">ServletContextEvent</code></p></td>
</tr>
<tr class="even">
<td><p>Web context</p></td>
<td><p>Attribute added, removed, or replaced</p></td>
<td><p><code dir="ltr">javax.servlet.ServletContextAttributeListener</code> and <code dir="ltr">ServletContextAttributeEvent</code></p></td>
</tr>
<tr class="odd">
<td><p>Session</p></td>
<td><p>Creation, invalidation, activation, passivation, and timeout</p></td>
<td><p><code dir="ltr">javax.servlet.http.HttpSessionListener</code>, <code dir="ltr">javax.servlet.http.HttpSessionActivationListener</code>, and <code dir="ltr">HttpSessionEvent</code></p></td>
</tr>
<tr class="even">
<td><p>Session</p></td>
<td><p>Attribute added, removed, or replaced</p></td>
<td><p><code dir="ltr">javax.servlet.http.HttpSessionAttributeListener</code> and <code dir="ltr">HttpSessionBindingEvent</code></p></td>
</tr>
<tr class="odd">
<td><p>Request</p></td>
<td><p>A servlet request has started being processed by web components</p></td>
<td><p><code dir="ltr">javax.servlet.ServletRequestListener</code> and <code dir="ltr">ServletRequestEvent</code></p></td>
</tr>
<tr class="even">
<td><p>Request</p></td>
<td><p>Attribute added, removed, or replaced</p></td>
<td><p><code dir="ltr">javax.servlet.ServletRequestAttributeListener</code> and <code dir="ltr">ServletRequestAttributeEvent</code></p></td>
</tr>
</tbody>
</table>

  

Use the `@WebListener` annotation to define a listener to get events for
various operations on the particular web application context. Classes
annotated with `@WebListener` must implement one of the following
interfaces:

``` oac_no_warn
javax.servlet.ServletContextListener
javax.servlet.ServletContextAttributeListener
javax.servlet.ServletRequestListener
javax.servlet.ServletRequestAttributeListener
javax.servlet..http.HttpSessionListener
javax.servlet..http.HttpSessionAttributeListener
```

For example, the following code snippet defines a listener that
implements two of these interfaces:

``` oac_no_warn
import javax.servlet.ServletContextAttributeListener;
import javax.servlet.ServletContextListener;
import javax.servlet.annotation.WebListener;

@WebListener()
public class SimpleServletListener implements ServletContextListener,
        ServletContextAttributeListener {
    ...
```

## 17.2.2 Handling Servlet Errors

Any number of exceptions can occur when a servlet executes. When an
exception occurs, the web container generates a default page containing
the following message:

``` oac_no_warn
A Servlet Exception Has Occurred
```

But you can also specify that the container should return a specific
error page for a given exception.

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
<td><a href="servlets001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
