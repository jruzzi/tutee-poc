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
<td><a href="cdi-basic007.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basic009.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 23.8 Using Scopes

For a web application to use a bean that injects another bean class, the
bean needs to be able to hold state over the duration of the user's
interaction with the application. The way to define this state is to
give the bean a scope. You can give an object any of the scopes
described in [Table 23-1](#GJDBG), depending on how you are using it.

Table 23-1 Scopes

<table style="width:49%;">
<colgroup>
<col width="22%" />
<col width="27%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Scope</th>
<th>Annotation</th>
<th>Duration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Request</p></td>
<td><p><code dir="ltr">@RequestScoped</code></p></td>
<td><p>A user's interaction with a web application in a single HTTP request.</p></td>
</tr>
<tr class="even">
<td><p>Session</p></td>
<td><p><code dir="ltr">@SessionScoped</code></p></td>
<td><p>A user's interaction with a web application across multiple HTTP requests.</p></td>
</tr>
<tr class="odd">
<td><p>Application</p></td>
<td><p><code dir="ltr">@ApplicationScoped</code></p></td>
<td><p>Shared state across all users' interactions with a web application.</p></td>
</tr>
<tr class="even">
<td><p>Dependent</p></td>
<td><p><code dir="ltr">@Dependent</code></p></td>
<td><p>The default scope if none is specified; it means that an object exists to serve exactly one client (bean) and has the same lifecycle as that client (bean).</p></td>
</tr>
<tr class="odd">
<td><p>Conversation</p></td>
<td><p><code dir="ltr">@ConversationScoped</code></p></td>
<td><p>A user's interaction with a servlet, including JavaServer Faces applications. The conversation scope exists within developer-controlled boundaries that extend it across multiple requests for long-running conversations. All long-running conversations are scoped to a particular HTTP servlet session and may not cross session boundaries.</p></td>
</tr>
</tbody>
</table>

  

The first three scopes are defined by both JSR 346 and the JavaServer
Faces specification. The last two are defined by JSR 346.

All predefined scopes except `@Dependent` are contextual scopes. CDI
places beans of contextual scope in the context whose lifecycle is
defined by the Java EE specifications. For example, a session context
and its beans exist during the lifetime of an HTTP session. Injected
references to the beans are contextually aware. The references always
apply to the bean that is associated with the context for the thread
that is making the reference. The CDI container ensures that the objects
are created and injected at the correct time as determined by the scope
that is specified for these objects.

You can also define and implement custom scopes, but that is an advanced
topic. Custom scopes are likely to be used by those who implement and
extend the CDI specification.

A scope gives an object a well-defined lifecycle context. A scoped
object can be automatically created when it is needed and automatically
destroyed when the context in which it was created ends. Moreover, its
state is automatically shared by any clients that execute in the same
context.

Java EE components, such as servlets and enterprise beans, and JavaBeans
components do not by definition have a well-defined scope. These
components are one of the following:

  - Singletons, such as Enterprise JavaBeans singleton beans, whose
    state is shared among all clients

  - Stateless objects, such as servlets and stateless session beans,
    which do not contain client-visible state

  - Objects that must be explicitly created and destroyed by their
    client, such as JavaBeans components and stateful session beans,
    whose state is shared by explicit reference passing between clients

If, however, you create a Java EE component that is a managed bean, it
becomes a scoped object, which exists in a well-defined lifecycle
context.

The web application for the `Printer` bean will use a simple request and
response mechanism, so the managed bean can be annotated as follows:

``` oac_no_warn
import javax.enterprise.context.RequestScoped;
import javax.inject.Inject;

@RequestScoped
public class Printer {

    @Inject @Informal Greeting greeting;
    ...
}
```

Beans that use session, application, or conversation scope must be
serializable, but beans that use request scope do not have to be
serializable.

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
<td><a href="cdi-basic007.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basic009.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
