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
<td><a href="resources003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="resources005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft:
2017-06-12

# 52.4 Using Resource Adapters with Contexts and Dependency Injection for Java EE (CDI)

For details about CDI, see [Chapter 23, "Introduction to Contexts and
Dependency Injection for Java EE"](cdi-basic.htm#GIWHB) and [Chapter 25,
"Contexts and Dependency Injection for Java EE: Advanced
Topics."](cdi-adv.htm#GJEHI)

Do not specify the following classes in the resource adapter as CDI
managed beans (that is, do not inject them), because the behavior of
these classes as CDI managed beans has not been portably defined.

  - Resource adapter beans: These beans are classes that are annotated
    with the `javax.resource.spi.Connector` annotation or are declared
    as corresponding elements in the resource adapter deployment
    descriptor, `ra.xml`.

  - Managed connection factory beans: These beans are classes that are
    annotated with the `javax.resource.spi.ConnectorDefinition`
    annotation or the `javax.resource.spi.ConnectorDefinitions`
    annotation or are declared as corresponding elements in `ra.xml`.

  - Activation specification beans: These beans are classes that are
    annotated with the `javax.resource.spi.Activation` annotation or are
    declared as corresponding elements in `ra.xml`.

  - Administered object beans: These beans are classes that are
    annotated with the `javax.resource.spi.AdministeredObject`
    annotation or are declared as corresponding elements in `ra.xml`.

Other types of classes in the resource adapter can be CDI managed beans
and will behave in a portable manner.

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
<td><a href="resources003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="resources005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
