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
<td><a href="ejb-intro006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-intro008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 32.7 The Lifecycles of Enterprise Beans

An enterprise bean goes through various stages during its lifetime, or
lifecycle. Each type of enterprise bean (stateful session, stateless
session, singleton session, or message-driven) has a different
lifecycle.

The descriptions that follow refer to methods that are explained along
with the code examples in the next two chapters. If you are new to
enterprise beans, you should skip this section and run the code examples
first.

The following topics are addressed here:

  - [Section 32.7.1, "The Lifecycle of a Stateful Session Bean"](#GIPLN)

  - [Section 32.7.2, "The Lifecycle of a Stateless Session
    Bean"](#GIPLM)

  - [Section 32.7.3, "The Lifecycle of a Singleton Session
    Bean"](#GIPRX)

  - [Section 32.7.4, "The Lifecycle of a Message-Driven Bean"](#GIPKW)

## 32.7.1 The Lifecycle of a Stateful Session Bean

[Figure 32-2](#GIPMI) illustrates the stages that a stateful session
bean passes through during its lifetime. The client initiates the
lifecycle by obtaining a reference to a stateful session bean. The
container performs any dependency injection and then invokes the method
annotated with `@PostConstruct`, if any. The bean is now ready to have
its business methods invoked by the client.

Figure 32-2 Lifecycle of a Stateful Session Bean

![Description of Figure 32-2 follows](img/jeett_dt_021.png)  
[Description of "Figure 32-2 Lifecycle of a Stateful Session
Bean"](img_text/jeett_dt_021.htm)  
  

While in the ready stage, the EJB container may decide to deactivate, or
passivate, the bean by moving it from memory to secondary storage.
(Typically, the EJB container uses a least-recently-used algorithm to
select a bean for passivation.) The EJB container invokes the method
annotated `@PrePassivate`, if any, immediately before passivating it. If
a client invokes a business method on the bean while it is in the
passive stage, the EJB container activates the bean, calls the method
annotated `@PostActivate`, if any, and then moves it to the ready stage.

At the end of the lifecycle, the client invokes a method annotated
`@Remove`, and the EJB container calls the method annotated
`@PreDestroy`, if any. The bean's instance is then ready for garbage
collection.

Your code controls the invocation of only one lifecycle method: the
method annotated `@Remove`. All other methods in [Figure 32-2](#GIPMI)
are invoked by the EJB container. See [Chapter 52, "Resource Adapters
and Contracts"](resources.htm#BNCJH) for more information.

## 32.7.2 The Lifecycle of a Stateless Session Bean

Because a stateless session bean is never passivated, its lifecycle has
only two stages: nonexistent and ready for the invocation of business
methods. [Figure 32-3](#GIPNI) illustrates the stages of a stateless
session bean.

Figure 32-3 Lifecycle of a Stateless or Singleton Session Bean

![Description of Figure 32-3 follows](img/jeett_dt_022.png)  
[Description of "Figure 32-3 Lifecycle of a Stateless or Singleton
Session Bean"](img_text/jeett_dt_022.htm)  
  

The EJB container typically creates and maintains a pool of stateless
session beans, beginning the stateless session bean's lifecycle. The
container performs any dependency injection and then invokes the method
annotated `@PostConstruct`, if it exists. The bean is now ready to have
its business methods invoked by a client.

At the end of the lifecycle, the EJB container calls the method
annotated `@PreDestroy`, if it exists. The bean's instance is then ready
for garbage collection.

## 32.7.3 The Lifecycle of a Singleton Session Bean

Like a stateless session bean, a singleton session bean is never
passivated and has only two stages, nonexistent and ready for the
invocation of business methods, as shown in [Figure 32-3](#GIPNI).

The EJB container initiates the singleton session bean lifecycle by
creating the singleton instance. This occurs upon application deployment
if the singleton is annotated with the `@Startup` annotation. The
container performs any dependency injection and then invokes the method
annotated `@PostConstruct`, if it exists. The singleton session bean is
now ready to have its business methods invoked by the client.

At the end of the lifecycle, the EJB container calls the method
annotated `@PreDestroy`, if it exists. The singleton session bean is now
ready for garbage collection.

## 32.7.4 The Lifecycle of a Message-Driven Bean

[Figure 32-4](#GIPLR) illustrates the stages in the lifecycle of a
message-driven bean.

Figure 32-4 Lifecycle of a Message-Driven Bean

![Description of Figure 32-4 follows](img/jeett_dt_023.png)  
[Description of "Figure 32-4 Lifecycle of a Message-Driven
Bean"](img_text/jeett_dt_023.htm)  
  

The EJB container usually creates a pool of message-driven bean
instances. For each instance, the EJB container performs these tasks.

1.  If the message-driven bean uses dependency injection, the container
    injects these references before instantiating the instance.

2.  The container calls the method annotated `@PostConstruct`, if any.

Like a stateless session bean, a message-driven bean is never passivated
and has only two states: nonexistent and ready to receive messages.

At the end of the lifecycle, the container calls the method annotated
`@PreDestroy`, if any. The bean's instance is then ready for garbage
collection.

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
<td><a href="ejb-intro006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-intro008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
