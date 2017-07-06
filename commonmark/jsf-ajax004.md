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
<td><a href="jsf-ajax003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 13.4 Sending an Ajax Request

To activate Ajax functionality, the web application must create an Ajax
request and send it to the server. The server then processes the
request.

The application uses the attributes of the `f:ajax` tag listed in [Table
13-1](jsf-ajax003.htm#GKDER) to create the Ajax request. The following
sections explain the process of creating and sending an Ajax request
using some of these attributes.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
Behind the scenes, the <code dir="ltr">jsf.ajax.request()</code> method of the JavaScript resource library collects the data provided by the <code dir="ltr">f:ajax</code> tag and posts the request to the JavaServer Faces lifecycle.</td>
</tr>
</tbody>
</table>

  

The following topics are addressed here:

  - [Section 13.4.1, "Using the event Attribute"](#GKHVT)

  - [Section 13.4.2, "Using the execute Attribute"](#GKHUZ)

  - [Section 13.4.3, "Using the immediate Attribute"](#GKHWM)

  - [Section 13.4.4, "Using the listener Attribute"](#GKHZS)

## 13.4.1 Using the event Attribute

The `event` attribute defines the event that triggers the Ajax action.
Some of the possible values for this attribute are `click`, `keyup`,
`mouseover`, `focus`, and `blur`.

If not specified, a default event based on the parent component will be
applied. The default event is `action` for
`javax.faces.component.ActionSource` components, such as a
`commandButton`, and `valueChange` for
`javax.faces.component.EditableValueHolder` components, such as
`inputText`. In the following example, an Ajax tag is associated with
the button component, and the event that triggers the Ajax action is a
mouse click:

``` oac_no_warn
<h:commandButton id="submit" value="Submit"> 
    <f:ajax event="click" />
</h:commandButton>
<h:outputText id="result" value="#{userNumberBean.response}" />
```

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
You may have noticed that the listed events are very similar to JavaScript events. In fact, they are based on JavaScript events, but do not have the <code dir="ltr">on</code> prefix.</td>
</tr>
</tbody>
</table>

  

For a command button, the default event is `click`, so you do not
actually need to specify `event="click"` to obtain the desired behavior.

## 13.4.2 Using the execute Attribute

The `execute` attribute defines the component or components to be
executed on the server. The component is identified by its `id`
attribute. You can specify more than one executable component. If more
than one component is to be executed, specify a space-delimited list of
components.

When a component is executed, it participates in all phases of the
request-processing lifecycle except the Render Response phase.

The `execute` attribute value can also be a keyword, such as `@all`,
`@none`, `@this`, or `@form`. The default value is `@this`, which refers
to the component within which the `f:ajax` tag is nested.

The following code specifies that the `h:inputText` component with the
`id` value of `userNo` should be executed when the button is clicked:

``` oac_no_warn
<h:inputText id="userNo" 
             title="Type a number from 0 to 10:"
             value="#{userNumberBean.userNumber}">
    ...
</h:inputText>
<h:commandButton id="submit" value="Submit"> 
    <f:ajax event="click" execute="userNo" />
</h:commandButton>
```

## 13.4.3 Using the immediate Attribute

The `immediate` attribute indicates whether user inputs are to be
processed early in the application lifecycle or later. If the attribute
is set to `true`, events generated from this component are broadcast
during the Apply Request Values phase. Otherwise, the events will be
broadcast during the Invoke Application phase.

If not defined, the default value of this attribute is `false`.

## 13.4.4 Using the listener Attribute

The `listener` attribute refers to a method expression that is executed
on the server side in response to an Ajax action on the client. The
listener's `javax.faces.event.AjaxBehaviorListener.processAjaxBehavior`
method is called once during the Invoke Application phase of the
lifecycle. In the following code from the `reservation` example
application (see [The reservation Example
Application](jsf-facelets009.htm#BABGGIAA)), a `listener` attribute is
defined by an `f:ajax` tag, which refers to a method from the bean:

``` oac_no_warn
<f:ajax event="change" render="total" 
        listener="#{reservationBean.calculateTotal}"/>
```

Whenever either the price or the number of tickets ordered changes, the
`calculateTotal` method of `ReservationBean` recalculates the total cost
of the tickets and displays it in the output component named `total`.

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
<td><a href="jsf-ajax003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
