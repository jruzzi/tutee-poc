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
<td><a href="cdi-basic002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basic004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 23.3 About Beans

CDI redefines the concept of a bean beyond its use in other Java
technologies, such as the JavaBeans and Enterprise JavaBeans (EJB)
technologies. In CDI, a bean is a source of contextual objects that
define application state and/or logic. A Java EE component is a bean if
the lifecycle of its instances may be managed by the container according
to the lifecycle context model defined in the CDI specification.

More specifically, a bean has the following attributes:

  - A (nonempty) set of bean types

  - A (nonempty) set of qualifiers (see [Using
    Qualifiers](cdi-basic006.htm#GJBCK))

  - A scope (see [Using Scopes](cdi-basic008.htm#GJBBK))

  - Optionally, a bean EL name (see [Giving Beans EL
    Names](cdi-basic009.htm#GJBAK))

  - A set of interceptor bindings

  - A bean implementation

A bean type defines a client-visible type of the bean. Almost any Java
type may be a bean type of a bean.

  - A bean type may be an interface, a concrete class, or an abstract
    class and may be declared final or have final methods.

  - A bean type may be a parameterized type with type parameters and
    type variables.

  - A bean type may be an array type. Two array types are considered
    identical only if the element type is identical.

  - A bean type may be a primitive type. Primitive types are considered
    to be identical to their corresponding wrapper types in `java.lang`.

  - A bean type may be a raw type.

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
<td><a href="cdi-basic002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basic004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
