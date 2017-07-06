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
<td><a href="cdi-basic013.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basic015.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft:
2017-06-12

# 23.14 Using the @PostConstruct and @PreDestroy Annotations with CDI Managed Bean Classes

CDI managed bean classes and their superclasses support the annotations
for initializing and for preparing for the destruction of a bean. These
annotations are defined in JSR 250: Common Annotations for the Java
platform (`http://jcp.org/en/jsr/detail?id=250`).

The following topics are addressed here:

  - [Section 23.14.1, "To Initialize a Managed Bean Using the
    @PostConstruct Annotation"](#CIHEHHCH)

  - [Section 23.14.2, "To Prepare for the Destruction of a Managed Bean
    Using the @PreDestroy
Annotation"](#CIHBAFAC)

## 23.14.1 To Initialize a Managed Bean Using the @PostConstruct Annotation

Initializing a managed bean specifies the lifecycle callback method that
the CDI framework should call after dependency injection but before the
class is put into service.

1.  In the managed bean class or any of its superclasses, define a
    method that performs the initialization that you require.

2.  Annotate the declaration of the method with the
    `javax.annotation.PostConstruct` annotation.

When the managed bean is injected into a component, CDI calls the method
after all injection has occurred and after all initializers have been
called.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
As mandated in JSR 250, if the annotated method is declared in a superclass, the method is called unless a subclass of the declaring class overrides the method.</td>
</tr>
</tbody>
</table>

  

The `UserNumberBean` managed bean in [The guessnumber-cdi CDI
Example](cdi-basicexamples003.htm#GJCXV) uses `@PostConstruct` to
annotate a method that resets all bean fields:

``` oac_no_warn
@PostConstruct
public void reset () {
    this.minimum = 0;
    this.userNumber = 0;
    this.remainingGuesses = 0;
    this.maximum = maxNumber;
    this.number = randomInt.get();
}
```

## 23.14.2 To Prepare for the Destruction of a Managed Bean Using the @PreDestroy Annotation

Preparing for the destruction of a managed bean specifies the lifecycle
call back method that signals that an application component is about to
be destroyed by the container.

1.  In the managed bean class or any of its superclasses, prepare for
    the destruction of the managed bean.
    
    In this method, perform any cleanup that is required before the bean
    is destroyed, such as releasing a resource that the bean has been
    holding.

2.  Annotate the declaration of the method with the
    `javax.annotation.PreDestroy` annotation.

CDI calls this method before starting to destroy the bean.

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
<td><a href="cdi-basic013.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basic015.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
