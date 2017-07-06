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
<td><a href="injection001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="injection003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 4.2 Dependency Injection

Dependency injection enables you to turn regular Java classes into
managed objects and to inject them into any other managed object. Using
dependency injection, your code can declare dependencies on any managed
object. The container automatically provides instances of these
dependencies at the injection points at runtime, and it also manages the
lifecycle of these instances for you.

Dependency injection in Java EE defines scopes, which determine the
lifecycle of the objects that the container instantiates and injects.
For example, a managed object that is only needed to respond to a single
client request (such as a currency converter) has a different scope than
a managed object that is needed to process multiple client requests
within a session (such as a shopping cart).

You can define managed objects (also called managed beans) that you can
later inject by assigning a scope to a regular class:

``` oac_no_warn
@javax.enterprise.context.RequestScoped
public class CurrencyConverter { ... }
```

Use the `javax.inject.Inject` annotation to inject managed beans; for
example:

``` oac_no_warn
public class MyServlet extends HttpServlet {
    @Inject CurrencyConverter cc;
    ...
}
```

As opposed to resource injection, dependency injection is typesafe
because it resolves by type. To decouple your code from the
implementation of the managed bean, you can reference the injected
instances using an interface type and have your managed bean implement
that interface.

For more information about dependency injection, see [Chapter 23,
"Introduction to Contexts and Dependency Injection for Java
EE"](cdi-basic.htm#GIWHB) and JSR 299 (Contexts and Dependency Injection
for the Java EE Platform).

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
<td><a href="injection001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="injection003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
