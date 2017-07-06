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
<td><a href="cdi-adv002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft:
2017-06-12

# 25.3 Using Producer Methods, Producer Fields, and Disposer Methods in CDI Applications

A producer method generates an object that can then be injected.
Typically, you use producer methods in the following situations:

  - When you want to inject an object that is not itself a bean

  - When the concrete type of the object to be injected may vary at
    runtime

  - When the object requires some custom initialization that the bean
    constructor does not perform

For more information on producer methods, see [Injecting Objects by
Using Producer Methods](cdi-basic012.htm#GJDID).

A producer field is a simpler alternative to a producer method; it is a
field of a bean that generates an object. It can be used instead of a
simple getter method. Producer fields are particularly useful for
declaring Java EE resources such as data sources, JMS resources, and web
service references.

A producer method or field is annotated with the
`javax.enterprise.inject.Produces` annotation.

## 25.3.1 Using Producer Methods

A producer method can allow you to select a bean implementation at
runtime instead of at development time or deployment time. For example,
in the example described in [The producermethods Example: Using a
Producer Method to Choose a Bean
Implementation](cdi-adv-examples003.htm#GKHPY), the managed bean defines
the following producer method:

``` oac_no_warn
@Produces
@Chosen
@RequestScoped
public Coder getCoder() {

    switch (coderType) {
        case TEST:
            return new TestCoderImpl();
        case SHIFT:
            return new CoderImpl();
        default:
            return null;
    }
}
```

Here, `getCoder` becomes in effect a getter method, and when the `coder`
property is injected with the same qualifier and other annotations as
the method, the selected version of the interface is used.

``` oac_no_warn
@Inject
@Chosen
@RequestScoped
Coder coder;
```

Specifying the qualifier is essential: It tells CDI which `Coder` to
inject. Without it, the CDI implementation would not be able to choose
between `CoderImpl`, `TestCoderImpl`, and the one returned by `getCoder`
and would cancel deployment, informing the user of the ambiguous
dependency.

## 25.3.2 Using Producer Fields to Generate Resources

A common use of a producer field is to generate an object such as a JDBC
`DataSource` or a Java Persistence API `EntityManager` (see [Chapter 37,
"Introduction to the Java Persistence
API,"](persistence-intro.htm#BNBPZ) for more information). The object
can then be managed by the container. For example, you could create a
`@UserDatabase` qualifier and then declare a producer field for an
entity manager as follows:

``` oac_no_warn
@Produces
@UserDatabase
@PersistenceContext
private EntityManager em;
```

The `@UserDatabase` qualifier can be used when you inject the object
into another bean, `RequestBean`, elsewhere in the application:

``` oac_no_warn
    @Inject
    @UserDatabase
    EntityManager em;
    ...
```

[The producerfields Example: Using Producer Fields to Generate
Resources](cdi-adv-examples004.htm#GKHRG) shows how to use producer
fields to generate an entity manager. You can use a similar mechanism to
inject `@Resource`, `@EJB`, or `@WebServiceRef` objects.

To minimize the reliance on resource injection, specify the producer
field for the resource in one place in the application, and then inject
the object wherever in the application you need it.

## 25.3.3 Using a Disposer Method

You can use a producer method or a producer field to generate an object
that needs to be removed when its work is completed. If you do, you need
a corresponding disposer method, annotated with a `@Disposes`
annotation. For example, you can close the entity manager as follows:

``` oac_no_warn
public void close(@Disposes @UserDatabase EntityManager em) {
    em.close();
}
```

The disposer method is called automatically when the context ends (in
this case, at the end of the conversation, because `RequestBean` has
conversation scope), and the parameter in the `close` method receives
the object produced by the producer field.

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
<td><a href="cdi-adv002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
