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
<td><a href="jsf-custom.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 15.1 Introduction to Creating Custom Components

JavaServer Faces technology offers a basic set of standard, reusable UI
components that enable quick and easy construction of user interfaces
for web applications. These components mostly map one-to-one to the
elements in HTML 4. But often an application requires a component that
has additional functionality or requires a completely new component.
JavaServer Faces technology allows extension of standard components to
enhance their functionality or to create custom components. A rich
ecosystem of third-party component libraries is built on this extension
capability, but it is beyond the scope of this tutorial to examine them.
A web search for "JSF Component Libraries" is a good starting point to
learn more about this important aspect of using JavaServer Faces
technology.

In addition to extending the functionality of standard components, a
component writer might want to give a page author the ability to change
the appearance of the component on the page or to alter listener
behavior. Alternatively, the component writer might want to render a
component to a different kind of client device type, such as a
smartphone or a tablet instead of a desktop computer. Enabled by the
flexible JavaServer Faces architecture, a component writer can separate
the definition of the component behavior from its appearance by
delegating the rendering of the component to a separate renderer. In
this way, a component writer can define the behavior of a custom
component once but create multiple renderers, each of which defines a
different way to render the component to a particular kind of client
device.

A `javax.faces.component.UIComponent` is a Java class that is
responsible for representing a self-contained piece of the user
interface during the request-processing lifecycle. It is intended to
represent the meaning of the component; the visual representation of the
component is the responsibility of the `javax.faces.render.Renderer`.
There can be multiple instances of the same `UIComponent` class in any
given JavaServer Faces view, just as there can be multiple instances of
any Java class in any given Java program.

JavaServer Faces technology provides the ability to create custom
components by extending the `UIComponent` class, the base class for all
standard UI components. A custom component can be used anywhere an
ordinary component can be used, such as within a composite component. A
`UIComponent` is identified by two names: `component-family` specifies
the general purpose of the component (input or output, for instance),
and `component-type` indicates the specific purpose of a component, such
as a text input field or a command button.

A `Renderer` is a helper to the `UIComponent` that deals with how that
specific `UIComponent` class should appear in a specific kind of client
device. Renderers are identified by two names: `render-kit-id` and
`renderer-type`. A render kit is just a bucket into which a particular
group of renderers is placed, and the `render-kit-id` identifies the
group. Most JavaServer Faces component libraries provide their own
render kits.

A `javax.faces.view.facelets.Tag` object is a helper to the
`UIComponent` and `Renderer` that allows the page author to include an
instance of a `UIComponent` in a JavaServer Faces view. A tag represents
a specific combination of `component-type` and `renderer-type`.

See [Component, Renderer, and Tag Combinations](jsf-custom002.htm#BNAVK)
for information on how components, renderers, and tags interact.

This chapter uses the image map component from the Duke's Bookstore case
study example to explain how you can create simple custom components,
custom renderers, and associated custom tags, and take care of all the
other details associated with using the components and renderers in an
application. See [Chapter 57, "Duke's Bookstore Case Study
Example"](dukes-bookstore.htm#GLNVI) for more information about this
example.

The chapter also describes how to create other custom objects: custom
converters, custom listeners, and custom validators. It also describes
how to bind component values and instances to data objects and how to
bind custom objects to managed bean properties.

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
<td><a href="jsf-custom.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
