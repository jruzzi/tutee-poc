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
<td><a href="interceptors.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="interceptors002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 54.1 Overview of Interceptors

Interceptors are used in conjunction with Java EE managed classes to
allow developers to invoke interceptor methods on an associated target
class, in conjunction with method invocations or lifecycle events.
Common uses of interceptors are logging, auditing, and profiling.

Although interceptors are part of Enterprise JavaBeans 3.2 and Contexts
and Dependency Injection for Java EE 1.1, the Interceptors 1.2
specification is downloadable as part of a maintenance release of JSR
318, Enterprise JavaBeans 3.1, available from
`http://jcp.org/en/jsr/detail?id=318`. You can use interceptors with
session beans, message-driven beans, and CDI managed beans. In all of
these cases, the interceptor target class is the bean class.

An interceptor can be defined within a target class as an interceptor
method, or in an associated class called an interceptor class.
Interceptor classes contain methods that are invoked in conjunction with
the methods or lifecycle events of the target class.

Interceptor classes and methods are defined using metadata annotations,
or in the deployment descriptor of the application that contains the
interceptors and target classes.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
Applications that use the deployment descriptor to define interceptors are not portable across Java EE servers.</td>
</tr>
</tbody>
</table>

  

Interceptor methods within the target class or in an interceptor class
are annotated with one of the metadata annotations defined in [Table
54-1](#GKECC).

Table 54-1 Interceptor Metadata Annotations

<table style="width:44%;">
<colgroup>
<col width="44%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Interceptor Metadata Annotation</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">javax.interceptor.AroundConstruct</code></p></td>
<td><p>Designates the method as an interceptor method that receives a callback after the target class is constructed</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.interceptor.AroundInvoke</code></p></td>
<td><p>Designates the method as an interceptor method</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.interceptor.AroundTimeout</code></p></td>
<td><p>Designates the method as a timeout interceptor for interposing on timeout methods for enterprise bean timers</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.annotation.PostConstruct</code></p></td>
<td><p>Designates the method as an interceptor method for post-construct lifecycle events</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.annotation.PreDestroy</code></p></td>
<td><p>Designates the method as an interceptor method for pre-destroy lifecycle events</p></td>
</tr>
</tbody>
</table>

  

## 54.1.1 Interceptor Classes

Interceptor classes may be designated with the optional
`javax.interceptor.Interceptor` annotation, but interceptor classes are
not required to be so annotated. An interceptor class must have a
public, no-argument constructor.

The target class can have any number of interceptor classes associated
with it. The order in which the interceptor classes are invoked is
determined by the order in which the interceptor classes are defined in
the `javax.interceptor.Interceptors` annotation. However, this order can
be overridden in the deployment descriptor.

Interceptor classes may be targets of dependency injection. Dependency
injection occurs when the interceptor class instance is created, using
the naming context of the associated target class, and before any
`@PostConstruct` callbacks are invoked.

## 54.1.2 Interceptor Lifecycle

Interceptor classes have the same lifecycle as their associated target
class. When a target class instance is created, an interceptor class
instance is also created for each declared interceptor class in the
target class. That is, if the target class declares multiple interceptor
classes, an instance of each class is created when the target class
instance is created. The target class instance and all interceptor class
instances are fully instantiated before any `@PostConstruct` callbacks
are invoked, and any `@PreDestroy` callbacks are invoked before the
target class and interceptor class instances are destroyed.

## 54.1.3 Interceptors and CDI

Contexts and Dependency Injection for Java EE (CDI) builds on the basic
functionality of Java EE interceptors. For information on CDI
interceptors, including a discussion of interceptor binding types, see
[Using Interceptors in CDI Applications](cdi-adv006.htm#GKHJX).

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
<td><a href="interceptors.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="interceptors002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
