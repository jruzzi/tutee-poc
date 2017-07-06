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
<td><a href="jsf-configure001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 16.2 Using Annotations to Configure Managed Beans

JavaServer Faces support for bean annotations is introduced in [Chapter
7, "JavaServer Faces Technology"](jsf-intro.htm#BNAPH). Bean annotations
can be used for configuring JavaServer Faces applications.

The `@Named` (`javax.inject.Named`) annotation in a class, along with a
scope annotation, automatically registers that class as a resource with
the JavaServer Faces implementation. A bean that uses these annotations
is a CDI managed bean.

The following shows the use of the `@Named` and `@SessionScoped`
annotations in a class:

``` oac_no_warn
@Named("cart")
@SessionScoped
public class ShoppingCart ... { ... }
```

The above code snippet shows a bean that is managed by the JavaServer
Faces implementation and is available for the length of the session.

You can annotate beans with any of the scopes listed in the next
section, [Using Managed Bean Scopes](#GIRCR).

All classes will be scanned for annotations at startup unless the
`faces-config` element in the `faces-config.xml` file has the
`metadata-complete` attribute set to `true`.

Annotations are also available for other artifacts, such as components,
converters, validators, and renderers, to be used in place of
application configuration resource file entries. These are discussed,
along with registration of custom listeners, custom validators, and
custom converters, in [Chapter 15, "Creating Custom UI Components and
Other Custom Objects"](jsf-custom.htm#BNAVG).

## 16.2.1 Using Managed Bean Scopes

You can use annotations to define the scope in which the bean will be
stored. You can specify one of the following scopes for a bean class.

  - Application (`javax.enterprise.context.ApplicationScoped`):
    Application scope persists across all users' interactions with a web
    application.

  - Session (`javax.enterprise.context.SessionScoped`): Session scope
    persists across multiple HTTP requests in a web application.

  - Flow (`javax.faces.flows.FlowScoped`): Flow scope persists during a
    user's interaction with a specific flow of a web application. See
    [Using Faces Flows](jsf-configure004.htm#CHDGFCJF) for more
    information.

  - Request (`javax.enterprise.context.RequestScoped`): Request scope
    persists during a single HTTP request in a web application.

  - Dependent (`javax.enterprise.context.Dependent`): Indicates that the
    bean depends on some other bean.

You may want to use `@Dependent` when a managed bean references another
managed bean. The second bean should not be in a scope (`@Dependent`) if
it is supposed to be created only when it is referenced. If you define a
bean as `@Dependent`, the bean is instantiated anew each time it is
referenced, so it does not get saved in any scope.

If your managed bean is referenced by the `binding` attribute of a
component tag, you should define the bean with a request scope. If you
placed the bean in session or application scope instead, the bean would
need to take precautions to ensure thread safety, because
`javax.faces.component.UIComponent` instances each depend on running
inside of a single thread.

If you are configuring a bean that allows attributes to be associated
with the view, you can use the view scope. The attributes persist until
the user has navigated to the next view.

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
<td><a href="jsf-configure001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
