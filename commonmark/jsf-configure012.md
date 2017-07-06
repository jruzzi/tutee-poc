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
<td><a href="jsf-configure011.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure013.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 16.12 Registering a Custom Component

In addition to registering custom renderers (as explained in the
preceding section), you also must register the custom components that
are usually associated with the custom renderers. You use either a
`@FacesComponent` annotation, as described in [Creating Custom Component
Classes](jsf-custom005.htm#BNAVU), or the `component` element of the
application configuration resource file.

Here is a hypothetical `component` element from the application
configuration resource file that registers `AreaComponent`:

``` oac_no_warn
<component>
    <component-type>DemoArea</component-type>
    <component-class>
        dukesbookstore.components.AreaComponent
    </component-class>
    <property>
        <property-name>alt</property-name>
        <property-class>java.lang.String</property-class>
    </property>
    <property>
        <property-name>coords</property-name>
        <property-class>java.lang.String</property-class>
    </property>
    <property>
        <property-name>shape</property-name>
        <property-class>java.lang.String</property-class>
    </property>
</component>
```

Attributes specified in a `component` tag override any settings in the
`@FacesComponent` annotation.

The `component-type` element indicates the name under which the
component should be registered. Other objects referring to this
component use this name. For example, the `component-type` element in
the configuration for `AreaComponent` defines a value of `DemoArea`,
which matches the value returned by the `AreaTag` class's
`getComponentType` method.

The `component-class` element indicates the fully qualified class name
of the component. The `property` elements specify the component
properties and their types.

If the custom component can include facets, you can configure the facets
in the component configuration using `facet` elements, which are allowed
after the `component-class` elements. See [Registering a Custom Renderer
with a Render Kit](jsf-configure011.htm#BNAXH) for further details on
configuring facets.

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
<td><a href="jsf-configure011.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure013.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
