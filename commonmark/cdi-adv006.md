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
<td><a href="cdi-adv005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 25.6 Using Interceptors in CDI Applications

An interceptor is a class used to interpose in method invocations or
lifecycle events that occur in an associated target class. The
interceptor performs tasks, such as logging or auditing, that are
separate from the business logic of the application and are repeated
often within an application. Such tasks are often called cross-cutting
tasks. Interceptors allow you to specify the code for these tasks in one
place for easy maintenance. When interceptors were first introduced to
the Java EE platform, they were specific to enterprise beans. On the
Java EE 7 platform, you can use them with Java EE managed objects of all
kinds, including managed beans.

For information on Java EE interceptors, see [Chapter 54, "Using Java EE
Interceptors"](interceptors.htm#GKEED).

An interceptor class often contains a method annotated `@AroundInvoke`,
which specifies the tasks the interceptor will perform when intercepted
methods are invoked. It can also contain a method annotated
`@PostConstruct`, `@PreDestroy`, `@PrePassivate`, or `@PostActivate`, to
specify lifecycle callback interceptors, and a method annotated
`@AroundTimeout`, to specify EJB timeout interceptors. An interceptor
class can contain more than one interceptor method, but it must have no
more than one method of each type.

Along with an interceptor, an application defines one or more
interceptor binding types, which are annotations that associate an
interceptor with target beans or methods. For example, the `billpayment`
example contains an interceptor binding type named `@Logged` and an
interceptor named `LoggedInterceptor`. The interceptor binding type
declaration looks something like a qualifier declaration, but it is
annotated with `javax.interceptor.InterceptorBinding`:

``` oac_no_warn
@Inherited
@InterceptorBinding
@Retention(RUNTIME)
@Target({METHOD, TYPE})
public @interface Logged {
}
```

An interceptor binding also has the `java.lang.annotation.Inherited`
annotation, to specify that the annotation can be inherited from
superclasses. The `@Inherited` annotation also applies to custom scopes
(not discussed in this tutorial) but does not apply to qualifiers.

An interceptor binding type may declare other interceptor bindings.

The interceptor class is annotated with the interceptor binding as well
as with the `@Interceptor` annotation. For an example, see [The
LoggedInterceptor Interceptor Class](cdi-adv-examples005.htm#GKHRQ).

Every `@AroundInvoke` method takes a
`javax.interceptor.InvocationContext` argument, returns a
`java.lang.Object`, and throws an `Exception`. It can call
`InvocationContext` methods. The `@AroundInvoke` method must call the
`proceed` method, which causes the target class method to be invoked.

Once an interceptor and binding type are defined, you can annotate beans
and individual methods with the binding type to specify that the
interceptor is to be invoked either on all methods of the bean or on
specific methods. For example, in the `billpayment` example, the
`PaymentHandler` bean is annotated `@Logged`, which means that any
invocation of its business methods will cause the interceptor's
`@AroundInvoke` method to be invoked:

``` oac_no_warn
@Logged
@SessionScoped
public class PaymentHandler implements Serializable {...}
```

However, in the `PaymentBean` bean, only the `pay` and `reset` methods
have the `@Logged` annotation, so the interceptor is invoked only when
these methods are invoked:

``` oac_no_warn
@Logged
public String pay() {...}

@Logged
public void reset() {...}
```

In order for an interceptor to be invoked in a CDI application, it must,
like an alternative, be specified in the `beans.xml` file. For example,
the `LoggedInterceptor` class is specified as follows:

``` oac_no_warn
<interceptors>
    <class>javaeetutorial.billpayment.interceptors.LoggedInterceptor</class>
</interceptors>
```

If an application uses more than one interceptor, the interceptors are
invoked in the order specified in the `beans.xml` file.

The interceptors that you specify in the `beans.xml` file apply only to
classes in the same archive. Use the `@Priority` annotation to specify
interceptors globally for an application that consists of multiple
modules, as in the following example:

``` oac_no_warn
@Logged
@Interceptor
@Priority(Interceptor.Priority.APPLICATION)
public class LoggedInterceptor implements Serializable { ... }
```

Interceptors with lower priority values are called first. You do not
need to specify the interceptor in the `beans.xml` file when you use the
`@Priority` annotation.

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
<td><a href="cdi-adv005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
