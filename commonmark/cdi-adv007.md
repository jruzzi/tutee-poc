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
<td><a href="cdi-adv006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 25.7 Using Decorators in CDI Applications

A decorator is a Java class that is annotated
`javax.decorator.Decorator` and that has a corresponding `decorators`
element in the `beans.xml` file.

A decorator bean class must also have a delegate injection point, which
is annotated `javax.decorator.Delegate`. This injection point can be a
field, a constructor parameter, or an initializer method parameter of
the decorator class.

Decorators are outwardly similar to interceptors. However, they actually
perform tasks complementary to those performed by interceptors.
Interceptors perform cross-cutting tasks associated with method
invocation and with the lifecycles of beans, but cannot perform any
business logic. Decorators, on the other hand, do perform business logic
by intercepting business methods of beans. This means that instead of
being reusable for different kinds of applications, as are interceptors,
their logic is specific to a particular application.

For example, instead of using an alternative `TestCoderImpl` class for
the `encoder` example, you could create a decorator as follows:

``` oac_no_warn
@Decorator
public abstract class CoderDecorator implements Coder {
    
    @Inject
    @Delegate
    @Any
    Coder coder;
    
    public String codeString(String s, int tval) {
        int len = s.length();

        return "\"" + s + "\" becomes " + "\"" + coder.codeString(s, tval)
                + "\", " + len + " characters in length";
    }
}
```

See [The decorators Example: Decorating a
Bean](cdi-adv-examples006.htm#GKPAX) for an example that uses this
decorator.

This simple decorator returns more detailed output than the encoded
string returned by the `CoderImpl.codeString` method. A more complex
decorator could store information in a database or perform some other
business logic.

A decorator can be declared as an abstract class so that it does not
have to implement all the business methods of the interface.

In order for a decorator to be invoked in a CDI application, it must,
like an interceptor or an alternative, be specified in the `beans.xml`
file. For example, the `CoderDecorator` class is specified as follows:

``` oac_no_warn
<decorators>
    <class>javaeetutorial.decorators.CoderDecorator</class>
</decorators>
```

If an application uses more than one decorator, the decorators are
invoked in the order in which they are specified in the `beans.xml`
file.

If an application has both interceptors and decorators, the interceptors
are invoked first. This means, in effect, that you cannot intercept a
decorator.

The decorators that you specify in the `beans.xml` file apply only to
classes in the same archive. Use the `@Priority` annotation to specify
decorators globally for an application that consists of multiple
modules, as in the following example:

``` oac_no_warn
@Decorator
@Priority(Interceptor.Priority.APPLICATION)
public abstract class CoderDecorator implements Coder { ... }
```

Decorators with lower priority values are called first. You do not need
to specify the decorator in the `beans.xml` when you use the `@Priority`
annotation.

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
<td><a href="cdi-adv006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
