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
<td><a href="cdi-adv003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 25.4 Using Predefined Beans in CDI Applications

Java EE provides predefined beans that implement the following
interfaces.

  - `javax.transaction.UserTransaction`: A Java Transaction API (JTA)
    user transaction.

  - `java.security.Principal`: The abstract notion of a principal, which
    represents any entity, such as an individual, a corporation, or a
    login ID. Whenever the injected principal is accessed, it always
    represents the identity of the current caller. For example, a
    principal is injected into a field at initialization. Later, a
    method that uses the injected principal is called on the object into
    which the principal was injected. In this situation, the injected
    principal represents the identity of the current caller when the
    method is run.

  - `javax.validation.Validator`: A validator for bean instances. The
    bean that implements this interface enables a `Validator` object for
    the default bean validation object `ValidatorFactory` to be
    injected.

  - `javax.validation.ValidatorFactory`: A factory class for returning
    initialized `Validator` instances. The bean that implements this
    interface enables the default bean validation `ValidatorFactory`
    object to be injected.

  - `javax.servlet.http.HttpServletRequest`: An HTTP request from a
    client. The bean that implements this interface enables a servlet to
    obtain all the details of a request.

  - `javax.servlet.http.HttpSession`: An HTTP session between a client
    and a server. The bean that implements this interface enables a
    servlet to access information about a session and to bind objects to
    a session.

  - `javax.servlet.ServletContext`: A context object that servlets can
    use to communicate with the servlet container.

To inject a predefined bean, create an injection point to obtain an
instance of the bean by using the `javax.annotation.Resource` annotation
for resources or the `javax.inject.Inject` annotation for CDI beans. For
the bean type, specify the class name of the interface the bean
implements.

Table 25-1 Injection of Predefined Beans

<table style="width:51%;">
<colgroup>
<col width="24%" />
<col width="27%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Predefined Bean</th>
<th>Resource or CDI Bean</th>
<th>Injection Example</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">UserTransaction</code></p></td>
<td><p>Resource</p></td>
<td><p><code dir="ltr">@Resource UserTransaction transaction;</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">Principal</code></p></td>
<td><p>Resource</p></td>
<td><p><code dir="ltr">@Resource Principal principal;</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">Validator</code></p></td>
<td><p>Resource</p></td>
<td><p><code dir="ltr">@Resource Validator validator;</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">ValidatorFactory</code></p></td>
<td><p>Resource</p></td>
<td><p><code dir="ltr">@Resource ValidatorFactory factory;</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">HttpServletRequest</code></p></td>
<td><p>CDI bean</p></td>
<td><p><code dir="ltr">@Inject HttpServletRequest req;</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">HttpSession</code></p></td>
<td><p>CDI bean</p></td>
<td><p><code dir="ltr">@Inject HttpSession session;</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ServletContext</code></p></td>
<td><p>CDI bean</p></td>
<td><p><code dir="ltr">@Inject ServletContext context;</code></p></td>
</tr>
</tbody>
</table>

  

Predefined beans are injected with dependent scope and the predefined
default qualifier `@Default`.

For more information about injecting resources, see [Resource
Injection](injection001.htm#BABHDCAI).

The following code snippet shows how to use the `@Resource` and
`@Inject` annotations to inject predefined beans. This code snippet
injects a user transaction and a context object into the servlet class
`TransactionServlet`. The user transaction is an instance of the
predefined bean that implements the `javax.transaction.UserTransaction`
interface. The context object is an instance of the predefined bean that
implements the `javax.servlet.ServletContext` interface.

``` oac_no_warn
import javax.annotation.Resource;
import javax.inject.Inject;
import javax.servlet.http.HttpServlet;
import javax.transaction.UserTransaction;
...
public class TransactionServlet extends HttpServlet {
    @Resource UserTransaction transaction;
    @Inject ServletContext context;
    ...
}
```

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
<td><a href="cdi-adv003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
