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
<td><a href="jsf-facelets008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-el.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 8.9 HTML5-Friendly Markup

When you want to produce user interface features for which HTML does not
have its own elements, you can create a custom JavaServer Faces
component and insert it in your Facelets page. This mechanism can cause
a simple element to create complex web code. However, creating such a
component is a significant task (see [Chapter 15, "Creating Custom UI
Components and Other Custom Objects"](jsf-custom.htm#BNAVG)).

HTML5 offers new elements and attributes that can make it unnecessary to
write your own components. It also provides many new capabilities for
existing components. JavaServer Faces technology supports HTML5 not by
introducing new UI components that imitate HTML5 ones but by allowing
you to use HTML5 markup directly. It also allows you to use JavaServer
Faces attributes within HTML5 elements. JavaServer Faces technology
support for HTML5 falls into two categories:

  - Pass-through elements

  - Pass-through attributes

The effect of the HTML5-friendly markup feature is to offer the Facelets
page author almost complete control over the rendered page output,
rather than having to pass this control off to component authors. You
can mix and match JavaServer Faces and HTML5 components and elements as
you see fit.

## 8.9.1 Using Pass-Through Elements

Pass-through elements allow you to use HTML5 tags and attributes but to
treat them as equivalent to JavaServer Faces components associated with
a server-side `UIComponent` instance.

To make an element that is not a JavaServer Faces element a pass-through
element, specify at least one of its attributes using the
`http://xmlns.jcp.org/jsf` namespace. For example, the following code
declares the namespace with the short name `jsf`:

``` oac_no_warn
<html ... xmlns:jsf="http://xmlns.jcp.org/jsf"
...
    <input type="email" jsf:id="email" name="email"
           value="#{reservationBean.email}" required="required"/>
```

Here, the `jsf` prefix is placed on the `id` attribute so that the HTML5
input tag's attributes are treated as part of the Facelets page. This
means that, for example, you can use EL expressions to retrieve managed
bean properties.

[Table 8-4](#BABJADGH) shows how pass-through elements are rendered as
Facelets tags. The JSF implementation uses the element name and the
identifying attribute to determine the corresponding Facelets tag that
will be used in the server-side processing. The browser, however,
interprets the markup that the page author has written.

Table 8-4 How Facelets Renders HTML5 Elements

<table style="width:66%;">
<colgroup>
<col width="0%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>HTML5 Element Name</th>
<th>Identifying Attribute</th>
<th>Facelets Tag</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">a</code></p></td>
<td><p><code dir="ltr">jsf:action</code></p></td>
<td><p><code dir="ltr">h:commandLink</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">a</code></p></td>
<td><p><code dir="ltr">jsf:actionListener</code></p></td>
<td><p><code dir="ltr">h:commandLink</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">a</code></p></td>
<td><p><code dir="ltr">jsf:value</code></p></td>
<td><p><code dir="ltr">h:outputLink</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">a</code></p></td>
<td><p><code dir="ltr">jsf:outcome</code></p></td>
<td><p><code dir="ltr">h:link</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">body</code></p></td>
<td><br />
</td>
<td><p><code dir="ltr">h:body</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">button</code></p></td>
<td><br />
</td>
<td><p><code dir="ltr">h:commandButton</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">button</code></p></td>
<td><p><code dir="ltr">jsf:outcome</code></p></td>
<td><p><code dir="ltr">h:button</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">form</code></p></td>
<td><br />
</td>
<td><p><code dir="ltr">h:form</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">head</code></p></td>
<td><br />
</td>
<td><p><code dir="ltr">h:head</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">img</code></p></td>
<td><br />
</td>
<td><p><code dir="ltr">h:graphicImage</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;button&quot;</code></p></td>
<td><p><code dir="ltr">h:commandButton</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;checkbox&quot;</code></p></td>
<td><p><code dir="ltr">h:selectBooleanCheckbox</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;color&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;date&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;datetime&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;datetime-local&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;email&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;month&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;number&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;range&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;search&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;time&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;url&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;week&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;file&quot;</code></p></td>
<td><p><code dir="ltr">h:inputFile</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;hidden&quot;</code></p></td>
<td><p><code dir="ltr">h:inputHidden</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;password&quot;</code></p></td>
<td><p><code dir="ltr">h:inputSecret</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;reset&quot;</code></p></td>
<td><p><code dir="ltr">h:commandButton</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;submit&quot;</code></p></td>
<td><p><code dir="ltr">h:commandButton</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">input</code></p></td>
<td><p><code dir="ltr">type=&quot;*&quot;</code></p></td>
<td><p><code dir="ltr">h:inputText</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">label</code></p></td>
<td><br />
</td>
<td><p><code dir="ltr">h:outputLabel</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">link</code></p></td>
<td><br />
</td>
<td><p><code dir="ltr">h:outputStylesheet</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">script</code></p></td>
<td><br />
</td>
<td><p><code dir="ltr">h:outputScript</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">select</code></p></td>
<td><p><code dir="ltr">multiple=&quot;*&quot;</code></p></td>
<td><p><code dir="ltr">h:selectManyListbox</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">select</code></p></td>
<td><br />
</td>
<td><p><code dir="ltr">h:selectOneListbox</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">textarea</code></p></td>
<td><br />
</td>
<td><p><code dir="ltr">h:inputTextArea</code></p></td>
</tr>
</tbody>
</table>

  

## 8.9.2 Using Pass-Through Attributes

Pass-through attributes are the converse of pass-through elements. They
allow you to pass attributes that are not JavaServer Faces attributes
through to the browser without interpretation. If you specify a
pass-through attribute in a JavaServer Faces `UIComponent`, the
attribute name and value are passed straight through to the browser
without being interpreted by JavaServer Faces components or renderers.
There are several ways to specify pass-through attributes.

  - Use the JavaServer Faces namespace for pass-through attributes to
    prefix the attribute names within a JavaServer Faces component. For
    example, the following code declares the namespace with the short
    name `p`, then passes the `type`, `min`, `max`, `required`, and
    `title` attributes through to the HTML5 `input` component:
    
    ``` oac_no_warn
    <html ... xmlns:p="http://xmlns.jcp.org/jsf/passthrough"
    ...
        
    <h:form prependId="false">
    <h:inputText id="nights" p:type="number" value="#{bean.nights}" 
                 p:min="1" p:max="30" p:required="required" 
                 p:title="Enter a number between 1 and 30 inclusive.">
            ...
    ```
    
    This will cause the following markup to be rendered (assuming that
    `bean.nights` has a default value set to 1):
    
    ``` oac_no_warn
    <input id="nights" type="number" value="1" min="1" max="30"
           required="required" 
           title="Enter a number between 1 and 30 inclusive.">
    ```

  - To pass a single attribute, nest the `f:passThroughAttribute` tag
    within a component tag. For example:
    
    ``` oac_no_warn
    <h:inputText value="#{user.email}">
        <f:passThroughAttribute name="type" value="email" />
    </h:inputText>
    ```
    
    This code would be rendered similarly to the following:
    
    ``` oac_no_warn
    <input value="me@me.com" type="email" />
    ```

  - To pass a group of attributes, nest the `f:passThroughAttributes`
    tag within a component tag, specifying an EL value that must
    evaluate to a `Map<String, Object>`. For example:
    
    ``` oac_no_warn
    <h:inputText value="#{bean.nights">
        <f:passThroughAttributes value="#{bean.nameValuePairs}" />
    </h:inputText>
    ```
    
    If the bean used the following `Map` declaration and initialized the
    map in the constructor as follows, the markup would be similar to
    the output of the code that uses the pass-through attribute
    namespace:
    
    ``` oac_no_warn
    private Map<String, Object> nameValuePairs;
    ...
    public Bean() {
        this.nameValuePairs = new HashMap<>();
        this.nameValuePairs.put("type", "number");
        this.nameValuePairs.put("min", "1");
        this.nameValuePairs.put("max", "30");
        this.nameValuePairs.put("required", "required");
        this.nameValuePairs.put("title", 
                "Enter a number between 1 and 4 inclusive.");
    }
    ```

## 8.9.3 The reservation Example Application

The `reservation` example application provides a set of HTML5 `input`
elements of various types to simulate purchasing tickets for a
theatrical event. It consists of two Facelets pages, `reservation.xhtml`
and `confirmation.xhtml`, and a backing bean, `ReservationBean.java`.
The pages use both pass-through attributes and pass-through elements.

The source code for this application is in the
tut-install`/examples/web/jsf/reservation/` directory.

The following topics are addressed here:

  - [Section 8.9.3.1, "The Facelets Pages for the reservation
    Application"](#BABGCAHH)

  - [Section 8.9.3.2, "The Managed Bean for the reservation
    Application"](#BABHFCCG)

  - [Section 8.9.3.3, "To Build, Package, and Deploy the reservation
    Example Using NetBeans IDE"](#BABIHHGC)

### 8.9.3.1 The Facelets Pages for the reservation Application

The first important feature of the Facelets pages for the `reservation`
application is the `DOCTYPE` header. Most Facelets pages in JavaServer
Faces applications refer to the XHTML DTD. The facelets pages for this
application begin simply with the following `DOCTYPE` header, which
indicates an HTML5 page:

``` oac_no_warn
<!DOCTYPE html>
```

The namespace declarations in the `html` element of the
`reservation.xhtml` page specify both the `jsf` and the `passthrough`
namespaces:

``` oac_no_warn
<html lang="en"
      xmlns="http://www.w3.org/1999/xhtml"
      xmlns:f="http://xmlns.jcp.org/jsf/core"
      xmlns:h="http://xmlns.jcp.org/jsf/html"
      xmlns:p="http://xmlns.jcp.org/jsf/passthrough"
      xmlns:jsf="http://xmlns.jcp.org/jsf">
```

Next, an empty `h:head` tag followed by an `h:outputStylesheet` tag
within the `h:body` tag illustrates the use of a relocatable resource
(as described in [Relocatable Resources](jsf-facelets007.htm#BABHGBJI)):

``` oac_no_warn
<h:head>
</h:head>
<h:body>
    <h:outputStylesheet name="css/stylesheet.css" target="head"/>
```

The `reservation.xhtml` page uses pass-through elements for most of the
form fields on the page. This allows it to use some HTML5-specific
`input` element types, such as `date` and `email`. For example, the
following element renders both a date format and a calendar from which
you can choose a date. The `jsf` prefix on the `id` attribute makes the
element a pass-through one:

``` oac_no_warn
    <input type="date" jsf:id="date" name="date" 
           value="#{reservationBean.date}" required="required"
           title="Enter or choose a date."/>
```

The field for the number of tickets, however, uses the
`h:passThroughAttributes` tag to pass a `Map` defined in the managed
bean. It also recalculates the total in response to a change in the
field:

``` oac_no_warn
    <h:inputText id="tickets" value="#{reservationBean.tickets}">
        <f:passThroughAttributes value="#{reservationBean.ticketAttrs}"/>
        <f:ajax event="change" render="total" 
                listener="#{reservationBean.calculateTotal}"/>
    </h:inputText>
```

The field for the price specifies the `number` type as a pass-through
attribute of the `h:inputText` element, offering a range of four ticket
prices. Here, the `p` prefix on the HTML5 attributes passes them through
to the browser uninterpreted by the JavaServer Faces input component:

``` oac_no_warn
    <h:inputText id="price" p:type="number" 
                 value="#{reservationBean.price}" 
                 p:min="80" p:max="120"
                 p:step="20" p:required="required" 
                 p:title="Enter a price: 80, 100, 120, or 140.">
        <f:ajax event="change" render="total" 
                listener="#{reservationBean.calculateTotal}"/>
    </h:inputText>
```

The output of the `calculateTotal` method that is specified as the
listener for the Ajax event is rendered in the output element whose `id`
and `name` value is `total`. See [Chapter 13, "Using Ajax with
JavaServer Faces Technology"](jsf-ajax.htm#GKIOW), for more information.

The second Facelets page, `confirmation.xhtml`, uses a pass-through
`output` element to display the values entered by the user and provides
a Facelets `h:commandButton` tag to allow the user to return to the
`reservation.xhtml` page.

### 8.9.3.2 The Managed Bean for the reservation Application

The session-scoped managed bean for the reservation application,
`ReservationBean.java`, contains properties for all the elements on the
Facelets pages. It also contains two methods, `calculateTotal` and
`clear`, that act as listeners for Ajax events on the
`reservation.xhtml`
page.

### 8.9.3.3 To Build, Package, and Deploy the reservation Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsf
    ```

4.  Select the `reservation` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `reservation` project and
    select Build.
    
    This option builds the example application and deploys it to your
    GlassFish Server
instance.

### 8.9.3.4 To Build, Package, and Deploy the reservation Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsf/reservation/
    ```

3.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the application into a WAR file,
    `reservation.war`, that is located in the `target` directory. It
    then deploys the WAR file to your GlassFish Server instance.

### 8.9.3.5 To Run the reservation Example

At the time of the publication of this tutorial, the browser that most
fully implements HTML5 is Google Chrome, and it is recommended that you
use it to run this example. Other browsers are catching up, however, and
may work equally well by the time you read this.

1.  Enter the following URL in your web browser:
    
    ``` oac_no_warn
    http://localhost:8080/reservation
    ```

2.  Enter information in the fields of the `reservation.xhtml` page.
    
    The Performance Date field has a date field with up and down arrows
    that allow you to increment and decrement the month, day, and year
    as well as a larger down arrow that brings up a date editor in
    calendar form.
    
    The Number of Tickets and Ticket Price fields also have up and down
    arrows that allow you to increment and decrement the values within
    the allowed range and steps. The Estimated Total changes when you
    change either of these two fields.
    
    Email addresses and dates are checked for format, but not for
    validity (you can make a reservation for a past date, for instance).

3.  Click Make Reservation to complete the reservation or Clear to
    restore the fields to their default values.

4.  If you click Make Reservation, the `confirmation.xhtml` page
    appears, displaying the submitted values.
    
    Click Back to return to the `reservation.xhtml` page.

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
<td><a href="jsf-facelets008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-el.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
