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
<td><a href="servlets008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets010.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.9 Maintaining Client State

Many applications require that a series of requests from a client be
associated with one another. For example, a web application can save the
state of a user's shopping cart across requests. Web-based applications
are responsible for maintaining such state, called a session, because
HTTP is stateless. To support applications that need to maintain state,
Java Servlet technology provides an API for managing sessions and allows
several mechanisms for implementing sessions.

## 17.9.1 Accessing a Session

Sessions are represented by an `HttpSession` object. You access a
session by calling the `getSession` method of a request object. This
method returns the current session associated with this request; or, if
the request does not have a session, this method creates one.

## 17.9.2 Associating Objects with a Session

You can associate object-valued attributes with a session by name. Such
attributes are accessible by any web component that belongs to the same
web context and is handling a request that is part of the same session.

Recall that your application can notify web context and session listener
objects of servlet lifecycle events ([Handling Servlet Lifecycle
Events](servlets002.htm#BNAFJ)). You can also notify objects of certain
events related to their association with a session, such as the
following.

  - When the object is added to or removed from a session. To receive
    this notification, your object must implement the
    `javax.servlet.http.HttpSessionBindingListener` interface.

  - When the session to which the object is attached will be passivated
    or activated. A session will be passivated or activated when it is
    moved between virtual machines or saved to and restored from
    persistent storage. To receive this notification, your object must
    implement the `javax.servlet.http.HttpSessionActivationListener`
    interface.

## 17.9.3 Session Management

Because an HTTP client has no way to signal that it no longer needs a
session, each session has an associated timeout so that its resources
can be reclaimed. The timeout period can be accessed by using a
session's `getMaxInactiveInterval` and `setMaxInactiveInterval` methods.

  - To ensure that an active session is not timed out, you should
    periodically access the session by using service methods because
    this resets the session's time-to-live counter.

  - When a particular client interaction is finished, you use the
    session's `invalidate` method to invalidate a session on the server
    side and remove any session data.

### 17.9.3.1 To Set the Timeout Period Using NetBeans IDE

To set the timeout period in the deployment descriptor using NetBeans
IDE, follow these steps.

1.  Open the project if you haven't already.

2.  Expand the node of your project in the Projects tab.

3.  Expand the Web Pages and WEB-INF nodes that are under the project
    node.

4.  Double-click `web.xml`.

5.  Click General at the top of the editor.

6.  In the Session Timeout field, enter an integer value.
    
    The integer value represents the number of minutes of inactivity
    that must pass before the session times out.

## 17.9.4 Session Tracking

To associate a session with a user, a web container can use several
methods, all of which involve passing an identifier between the client
and the server. The identifier can be maintained on the client as a
cookie, or the web component can include the identifier in every URL
that is returned to the client.

If your application uses session objects, you must ensure that session
tracking is enabled by having the application rewrite URLs whenever the
client turns off cookies. You do this by calling the response's
`encodeURL(URL)` method on all URLs returned by a servlet. This method
includes the session ID in the URL only if cookies are disabled;
otherwise, the method returns the URL unchanged.

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
<td><a href="servlets008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets010.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
