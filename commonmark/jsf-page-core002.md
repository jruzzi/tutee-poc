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
<td><a href="jsf-page-core001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-page-core003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 11.2 Registering Listeners on Components

An application developer can implement listeners as classes or as
managed bean methods. If a listener is a managed bean method, the page
author references the method from either the component's
`valueChangeListener` attribute or its `actionListener` attribute. If
the listener is a class, the page author can reference the listener from
either an `f:valueChangeListener` tag or an `f:actionListener` tag and
nest the tag inside the component tag to register the listener on the
component.

[Referencing a Method That Handles an Action
Event](jsf-page-core004.htm#BNATQ) and [Referencing a Method That
Handles a Value-Change Event](jsf-page-core004.htm#BNATS) explain how a
page author uses the `valueChangeListener` and `actionListener`
attributes to reference managed bean methods that handle events.

This section explains how to register a `NameChanged` value-change
listener and a `BookChange` action listener implementation on
components. The Duke's Bookstore case study includes both of these
listeners.

## 11.2.1 Registering a Value-Change Listener on a Component

A page author can register a `ValueChangeListener` implementation on a
component that implements `EditableValueHolder` by nesting an
`f:valueChangeListener` tag within the component's tag on the page. The
`f:valueChangeListener` tag supports the attributes shown in [Table
11-4](#GKCLY), one of which must be used.

Table 11-4 Attributes for the f:valueChangeListener Tag

<table style="width:21%;">
<colgroup>
<col width="21%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">type</code></p></td>
<td><p>References the fully qualified class name of a <code dir="ltr">ValueChangeListener</code> implementation. Can accept a literal or a value expression.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">binding</code></p></td>
<td><p>References an object that implements <code dir="ltr">ValueChangeListener</code>. Can accept only a value expression, which must point to a managed bean property that accepts and returns a <code dir="ltr">ValueChangeListener</code> implementation.</p></td>
</tr>
</tbody>
</table>

  

The following example shows a value-change listener registered on a
component:

``` oac_no_warn
<h:inputText id="name"
             size="30"
             value="#{cashierBean.name}"
             required="true"
             requiredMessage="#{bundle.ReqCustomerName}">
    <f:valueChangeListener
        type="javaeetutorial.dukesbookstore.listeners.NameChanged" />
</h:inputText>
```

In the example, the core tag `type` attribute specifies the custom
`NameChanged` listener as the `ValueChangeListener` implementation
registered on the `name` component.

After this component tag is processed and local values have been
validated, its corresponding component instance will queue the
`ValueChangeEvent` associated with the specified `ValueChangeListener`
to the component.

The `binding` attribute is used to bind a `ValueChangeListener`
implementation to a managed bean property. This attribute works in a
similar way to the `binding` attribute supported by the standard
converter tags. See [Binding Component Values and Instances to Managed
Bean Properties](jsf-custom013.htm#BNATG) for more information.

## 11.2.2 Registering an Action Listener on a Component

A page author can register an `ActionListener` implementation on a
command component by nesting an `f:actionListener` tag within the
component's tag on the page. Similarly to the `f:valueChangeListener`
tag, the `f:actionListener` tag supports both the `type` and `binding`
attributes. One of these attributes must be used to reference the action
listener.

Here is an example of an `h:commandLink` tag that references an
`ActionListener` implementation:

``` oac_no_warn
<h:commandLink id="Duke" action="bookstore">
    <f:actionListener 
        type="javaeetutorial.dukesbookstore.listeners.LinkBookChangeListener" />
    <h:outputText value="#{bundle.Book201}"/>
</h:commandLink>
```

The `type` attribute of the `f:actionListener` tag specifies the fully
qualified class name of the `ActionListener` implementation. Similarly
to the `f:valueChangeListener` tag, the `f:actionListener` tag also
supports the `binding` attribute. See [Binding Converters, Listeners,
and Validators to Managed Bean Properties](jsf-custom014.htm#BNATM) for
more information about binding listeners to managed bean properties.

In addition to the `actionListener` tag that allows you register a
custom listener onto a component, the core tag library includes the
`f:setPropertyActionListener` tag. You use this tag to register a
special action listener onto the `ActionSource` instance associated with
a component. When the component is activated, the listener will store
the object referenced by the tag's `value` attribute into the object
referenced by the tag's `target` attribute.

The `bookcatalog.xhtml` page of the Duke's Bookstore application uses
`f:setPropertyActionListener` with two components: the `h:commandLink`
component used to link to the `bookdetails.xhtml` page and the
`h:commandButton` component used to add a book to the cart:

``` oac_no_warn
<h:dataTable id="books"
    value="#{store.books}"
    var="book"
    headerClass="list-header"
    styleClass="list-background"
    rowClasses="list-row-even, list-row-odd"
    border="1"
    summary="#{bundle.BookCatalog}" >
    ...
    <h:column>
        <f:facet name="header">
            <h:outputText value="#{bundle.ItemTitle}"/>
        </f:facet>
        <h:commandLink action="#{catalog.details}"
                       value="#{book.title}">
            <f:setPropertyActionListener target="#{requestScope.book}"
                                         value="#{book}"/>
        </h:commandLink>
    </h:column>
    ...
    <h:column>
        <f:facet name="header">
            <h:outputText value="#{bundle.CartAdd}"/>
        </f:facet>
        <h:commandButton id="add"
                         action="#{catalog.add}"
                         value="#{bundle.CartAdd}">
            <f:setPropertyActionListener target="#{requestScope.book}"
                                         value="#{book}"/>
        </h:commandButton>
    </h:column>
```

The `h:commandLink` and `h:commandButton` tags are within an
`h:dataTable` tag, which iterates over the list of books. The `var`
attribute refers to a single book in the list of books.

The object referenced by the `var` attribute of an `h:dataTable` tag is
in page scope. However, in this case you need to put this object into
request scope so that when the user activates the `commandLink`
component to go to `bookdetails.xhtml` or activates the `commandButton`
component to go to `bookcatalog.xhtml`, the book data is available to
those pages. Therefore, the `f:setPropertyActionListener` tag is used to
set the current book object into request scope when the `commandLink` or
`commandButton` component is activated.

In the preceding example, the `f:setPropertyActionListener` tag's
`value` attribute references the `book` object. The
`f:setPropertyActionListener` tag's `target` attribute references the
value expression `requestScope.book`, which is where the `book` object
referenced by the `value` attribute is stored when the `commandLink` or
the `commandButton` component is activated.

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
<td><a href="jsf-page-core001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-page-core003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
