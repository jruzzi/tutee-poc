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
<td><a href="jsf-custom001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 15.2 Determining Whether You Need a Custom Component or Renderer

The JavaServer Faces implementation supports a very basic set of
components and associated renderers. This section helps you to decide
whether you can use standard components and renderers in your
application or need a custom component or custom renderer.

The following topics are addressed here:

  - [Section 15.2.1, "When to Use a Custom Component"](#BNAVI)

  - [Section 15.2.2, "When to Use a Custom Renderer"](#BNAVJ)

  - [Section 15.2.3, "Component, Renderer, and Tag
    Combinations"](#BNAVK)

## 15.2.1 When to Use a Custom Component

A component class defines the state and behavior of a UI component. This
behavior includes converting the value of a component to the appropriate
markup, queuing events on components, performing validation, and any
other behavior related to how the component interacts with the browser
and the request-processing lifecycle.

You need to create a custom component in the following situations.

  - You need to add new behavior to a standard component, such as
    generating an additional type of event (for example, notifying
    another part of the page that something changed in this component as
    a result of user interaction).

  - You need to take a different action in the request processing of the
    value of a component from what is available in any of the existing
    standard components.

  - You want to take advantage of an HTML capability offered by your
    target browser, but none of the standard JavaServer Faces components
    take advantage of the capability in the way you want, if at all. The
    current release does not contain standard components for complex
    HTML components, such as frames; however, because of the
    extensibility of the component architecture, you can use JavaServer
    Faces technology to create components like these. The Duke's
    Bookstore case study creates custom components that correspond to
    the HTML `map` and `area` tags.

  - You need to render to a non-HTML client that requires extra
    components not supported by HTML. Eventually, the standard HTML
    render kit will provide support for all standard HTML components.
    However, if you are rendering to a different client, such as a
    phone, you might need to create custom components to represent the
    controls uniquely supported by the client. For example, some
    component architectures for wireless clients include support for
    tickers and progress bars, which are not available on an HTML
    client. In this case, you might also need a custom renderer along
    with the component, or you might need only a custom renderer.

You do not need to create a custom component in the following cases.

  - You need to aggregate components to create a new component that has
    its own unique behavior. In this situation, you can use a composite
    component to combine existing standard components. For more
    information on composite components, see [Composite
    Components](jsf-facelets005.htm#GIQZR) and [Chapter 14, "Composite
    Components: Advanced Topics and an
    Example"](jsf-advanced-cc.htm#GKHXA).

  - You simply need to manipulate data on the component or add
    application-specific functionality to it. In this situation, you
    should create a managed bean for this purpose and bind it to the
    standard component rather than create a custom component. See
    [Managed Beans in JavaServer Faces
    Technology](jsf-develop001.htm#BNAQM) for more information on
    managed beans.

  - You need to convert a component's data to a type not supported by
    its renderer. See [Using the Standard
    Converters](jsf-page-core001.htm#BNAST) for more information about
    converting a component's data.

  - You need to perform validation on the component data. Standard
    validators and custom validators can be added to a component by
    using the validator tags from the page. See [Using the Standard
    Validators](jsf-page-core003.htm#BNATC) and [Creating and Using a
    Custom Validator](jsf-custom012.htm#BNAUW) for more information
    about validating a component's data.

  - You need to register event listeners on components. You can either
    register event listeners on components using the
    `f:valueChangeListener` and `f:actionListener` tags, or you can
    point at an event-processing method on a managed bean using the
    component's `actionListener` or `valueChangeListener` attributes.
    See [Implementing an Event Listener](jsf-custom007.htm#BNAUT) and
    [Writing Managed Bean Methods](jsf-develop003.htm#BNAVB) for more
    information.

## 15.2.2 When to Use a Custom Renderer

A renderer, which generates the markup to display a component on a web
page, allows you to separate the semantics of a component from its
appearance. By keeping this separation, you can support different kinds
of client devices with the same kind of authoring experience. You can
think of a renderer as a "client adapter." It produces output suitable
for consumption and display by the client and accepts input from the
client when the user interacts with that component.

If you are creating a custom component, you need to ensure, among other
things, that your component class performs these operations that are
central to rendering the component:

  - Decoding: Converting the incoming request parameters to the local
    value of the component

  - Encoding: Converting the current local value of the component into
    the corresponding markup that represents it in the response

The JavaServer Faces specification supports two programming models for
handling encoding and decoding.

  - Direct implementation: The component class itself implements the
    decoding and encoding.

  - Delegated implementation: The component class delegates the
    implementation of encoding and decoding to a separate renderer.

By delegating the operations to the renderer, you have the option of
associating your custom component with different renderers so that you
can render the component on different clients. If you don't plan to
render a particular component on different clients, it may be simpler to
let the component class handle the rendering. However, a separate
renderer enables you to preserve the separation of semantics from
appearance. The Duke's Bookstore application separates the renderers
from the components, although it renders only to HTML 4 web browsers.

If you aren't sure whether you will need the flexibility offered by
separate renderers but you want to use the simpler direct-implementation
approach, you can actually use both models. Your component class can
include some default rendering code, but it can delegate rendering to a
renderer if there is one.

## 15.2.3 Component, Renderer, and Tag Combinations

When you create a custom component, you can create a custom renderer to
go with it. To associate the component with the renderer and to
reference the component from the page, you will also need a custom tag.

Although you need to write the custom component and renderer, there is
no need to write code for a custom tag (called a tag handler). If you
specify the component and renderer combination, Facelets creates the tag
handler automatically.

In rare situations, you might use a custom renderer with a standard
component rather than a custom component. Or you might use a custom tag
without a renderer or a component. This section gives examples of these
situations and summarizes what is required for a custom component,
renderer, and tag.

You would use a custom renderer without a custom component if you wanted
to add some client-side validation on a standard component. You would
implement the validation code with a client-side scripting language,
such as JavaScript, and then render the JavaScript with the custom
renderer. In this situation, you need a custom tag to go with the
renderer so that its tag handler can register the renderer on the
standard component.

Custom components as well as custom renderers need custom tags
associated with them. However, you can have a custom tag without a
custom renderer or custom component. For example, suppose that you need
to create a custom validator that requires extra attributes on the
validator tag. In this case, the custom tag corresponds to a custom
validator and not to a custom component or custom renderer. In any case,
you still need to associate the custom tag with a server-side object.

[Table 15-1](#BNAVL) summarizes what you must or can associate with a
custom component, custom renderer, or custom tag.

Table 15-1 Requirements for Custom Components, Custom Renderers, and
Custom Tags

<table style="width:60%;">
<colgroup>
<col width="20%" />
<col width="0%" />
<col width="40%" />
</colgroup>
<thead>
<tr class="header">
<th>Custom Item</th>
<th>Must Have</th>
<th>Can Have</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Custom component</p></td>
<td><p>Custom tag</p></td>
<td><p>Custom renderer or standard renderer</p></td>
</tr>
<tr class="even">
<td><p>Custom renderer</p></td>
<td><p>Custom tag</p></td>
<td><p>Custom component or standard component</p></td>
</tr>
<tr class="odd">
<td><p>Custom JavaServer Faces tag</p></td>
<td><p>Some server-side object, like a component, a custom renderer, or custom validator</p></td>
<td><p>Custom component or standard component associated with a custom renderer</p></td>
</tr>
</tbody>
</table>

  

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
<td><a href="jsf-custom001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
