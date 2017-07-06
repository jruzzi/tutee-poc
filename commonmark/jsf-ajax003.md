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
<td><a href="jsf-ajax002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 13.3 Using Ajax with Facelets

As mentioned in the previous section, JavaServer Faces technology
supports Ajax by using a built-in JavaScript resource library that is
provided as part of the JavaServer Faces core libraries. This built-in
Ajax resource can be used in JavaServer Faces web applications in one of
the following ways.

  - By using the `f:ajax` tag along with another standard component in a
    Facelets application. This method adds Ajax functionality to any UI
    component without additional coding and configuration.

  - By using the JavaScript API method `jsf.ajax.request()` directly
    within the Facelets application. This method provides direct access
    to Ajax methods and allows customized control of component behavior.

## 13.3.1 Using the f:ajax Tag

The `f:ajax` tag is a JavaServer Faces core tag that provides Ajax
functionality to any regular UI component when used in conjunction with
that component. In the following example, Ajax behavior is added to an
input component by including the `f:ajax` core tag:

``` oac_no_warn
<h:inputText value="#{bean.message}">
    <f:ajax />
</h:inputText>
```

In this example, although Ajax is enabled, the other attributes of the
`f:ajax` tag are not defined. If an event is not defined, the default
action for the component is performed. For the `inputText` component,
when no `event` attribute is specified, the default event is
`valueChange`. [Table 13-1](#GKDER) lists the attributes of the `f:ajax`
tag and their default actions.

Table 13-1 Attributes of the f:ajax Tag

<table style="width:48%;">
<colgroup>
<col width="13%" />
<col width="35%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">disabled</code></p></td>
<td><p><code dir="ltr">javax.el.ValueExpression</code> that evaluates to a <code dir="ltr">Boolean</code></p></td>
<td><p>A <code dir="ltr">Boolean</code> value that identifies the tag status. A value of <code dir="ltr">true</code> indicates that the Ajax behavior should not be rendered. A value of <code dir="ltr">false</code> indicates that the Ajax behavior should be rendered. The default value is <code dir="ltr">false</code>.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">event</code></p></td>
<td><p><code dir="ltr">javax.el.ValueExpression</code> that evaluates to a <code dir="ltr">String</code></p></td>
<td><p>A <code dir="ltr">String</code> that identifies the type of event to which the Ajax action will apply. If specified, it must be one of the events supported by the component. If not specified, the default event (the event that triggers the Ajax request) is determined for the component. The default event is <code dir="ltr">action</code> for <code dir="ltr">javax.faces.component.ActionSource</code> components and <code dir="ltr">valueChange</code> for <code dir="ltr">javax.faces.component.EditableValueHolder</code> components.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">execute</code></p></td>
<td><p><code dir="ltr">javax.el.ValueExpression</code> that evaluates to an <code dir="ltr">Object</code></p></td>
<td><p>A <code dir="ltr">Collection</code> that identifies a list of components to be executed on the server. If a literal is specified, it must be a space-delimited <code dir="ltr">String</code> of component identifiers and/or one of the keywords. If a <code dir="ltr">ValueExpression</code> is specified, it must refer to a property that returns a <code dir="ltr">Collection</code> of <code dir="ltr">String</code> objects. If not specified, the default value is <code dir="ltr">@this</code>.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">immediate</code></p></td>
<td><p><code dir="ltr">javax.el.ValueExpression</code> that evaluates to a <code dir="ltr">Boolean</code></p></td>
<td><p>A <code dir="ltr">Boolean</code> value that indicates whether inputs are to be processed early in the lifecycle. If <code dir="ltr">true</code>, behavior events generated from this behavior are broadcast during the Apply Request Values phase. Otherwise, the events will be broadcast during the Invoke Application phase.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">listener</code></p></td>
<td><p><code dir="ltr">javax.el.MethodExpression</code></p></td>
<td><p>The name of the listener method that is called when a <code dir="ltr">javax.faces.event.AjaxBehaviorEvent</code> has been broadcast for the listener.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">onevent</code></p></td>
<td><p><code dir="ltr">javax.el.ValueExpression</code> that evaluates to a <code dir="ltr">String</code></p></td>
<td><p>The name of the JavaScript function that handles UI events.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">onerror</code></p></td>
<td><p><code dir="ltr">javax.el.ValueExpression</code> that evaluates to a <code dir="ltr">String</code></p></td>
<td><p>The name of the JavaScript function that handles errors.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">render</code></p></td>
<td><p><code dir="ltr">javax.el.ValueExpression</code> that evaluates to an <code dir="ltr">Object</code></p></td>
<td><p>A <code dir="ltr">Collection</code> that identifies a list of components to be rendered on the client. If a literal is specified, it must be a space-delimited <code dir="ltr">String</code> of component identifiers and/or one of the keywords. If a <code dir="ltr">ValueExpression</code> is specified, it must refer to a property that returns a <code dir="ltr">Collection</code> of <code dir="ltr">String</code> objects. If not specified, the default value is <code dir="ltr">@none</code>.</p></td>
</tr>
</tbody>
</table>

  

The keywords listed in [Table 13-2](#GKNLK) can be used with the
`execute` and `render` attributes of the `f:ajax` tag.

Table 13-2 Execute and Render Keywords

<table style="width:14%;">
<colgroup>
<col width="14%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Keyword</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">@all</code></p></td>
<td><p>All component identifiers</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@form</code></p></td>
<td><p>The form that encloses the component</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">@none</code></p></td>
<td><p>No component identifiers</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@this</code></p></td>
<td><p>The element that triggered the request</p></td>
</tr>
</tbody>
</table>

  

Note that when you use the `f:ajax` tag in a Facelets page, the
JavaScript resource library is loaded implicitly. This resource library
can also be loaded explicitly as described in [Loading JavaScript as a
Resource](jsf-ajax010.htm#GKAAM).

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
<td><a href="jsf-ajax002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
