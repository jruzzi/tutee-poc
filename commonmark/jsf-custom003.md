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
<td><a href="jsf-custom002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 15.3 Understanding the Image Map Example

Duke's Bookstore includes a custom image map component on the
`index.xhtml` page. This image map displays a selection of six book
titles. When the user clicks one of the book titles in the image map,
the application goes to a page that displays the title of the selected
book as well as information about a featured book. The page allows the
user to add either book (or none) to the shopping cart.

The following topics are addressed here:

  - [Section 15.3.1, "Why Use JavaServer Faces Technology to Implement
    an Image Map?"](#GLPBD)

  - [Section 15.3.2, "Understanding the Rendered HTML"](#GLPEM)

  - [Section 15.3.3, "Understanding the Facelets Page"](#GLPCD)

  - [Section 15.3.4, "Configuring Model Data"](#GLPBO)

  - [Section 15.3.5, "Summary of the Image Map Application
    Classes"](#GLPEL)

## 15.3.1 Why Use JavaServer Faces Technology to Implement an Image Map?

JavaServer Faces technology is an ideal framework to use for
implementing this kind of image map because it can perform the work that
must be done on the server without requiring you to create a server-side
image map.

In general, client-side image maps are preferred over server-side image
maps for several reasons. One reason is that the client-side image map
allows the browser to provide immediate feedback when a user positions
the mouse over a hotspot. Another reason is that client-side image maps
perform better because they don't require round-trips to the server.
However, in some situations, your image map might need to access the
server to retrieve data or to change the appearance of nonform controls,
tasks that a client-side image map cannot do.

Because the image map custom component uses JavaServer Faces technology,
it has the best of both styles of image maps: It can handle the parts of
the application that need to be performed on the server while allowing
the other parts of the application to be performed on the client side.

## 15.3.2 Understanding the Rendered HTML

Here is an abbreviated version of the form part of the HTML page that
the application needs to render:

``` oac_no_warn
<form id="j_idt13" name="j_idt13" method="post"
        action="/dukesbookstore/index.xhtml" ...>
    ...
    <img id="j_idt13:mapImage"
         src="/dukesbookstore/javax.faces.resource/book_all.jpg?ln=images"
         alt="Choose a Book from our Catalog"
         usemap="#bookMap" />
    ...
    <map name="bookMap">
       <area alt="Duke"                        
          coords="67,23,212,268"
          shape="rect"
          onmouseout="document.forms[0]['j_idt13:mapImage'].src='resources/images/book_all.jpg'"
          onmouseover="document.forms[0]['j_idt13:mapImage'].src='resources/images/book_201.jpg'"
          onclick="document.forms[0]['bookMap_current'].value='Duke'; document.forms[0].submit()"
       />
    ...
       <input type="hidden" name="bookMap_current">
    </map>
    ...
</form>
```

The `img` tag associates an image (`book_all.jpg`) with the image map
referenced in the `usemap` attribute value.

The `map` tag specifies the image map and contains a set of `area` tags.

Each `area` tag specifies a region of the image map. The `onmouseover`,
`onmouseout`, and `onclick` attributes define which JavaScript code is
executed when these events occur. When the user moves the mouse over a
region, the `onmouseover` function associated with the region displays
the map with that region highlighted. When the user moves the mouse out
of a region, the `onmouseout` function redisplays the original image. If
the user clicks on a region, the `onclick` function sets the value of
the `input` tag to the ID of the selected area and submits the page.

The `input` tag represents a hidden control that stores the value of the
currently selected area between client-server exchanges so that the
server-side component classes can retrieve the value.

The server-side objects retrieve the value of `bookMap_current` and set
the locale in the `javax.faces.context.FacesContext` instance according
to the region that was selected.

## 15.3.3 Understanding the Facelets Page

Here is an abbreviated form of the Facelets page that the image map
component uses to generate the HTML page shown in the preceding section.
It uses custom `bookstore:map` and `bookstore:area` tags to represent
the custom components:

``` oac_no_warn
<h:form>
    ...
        <h:graphicImage id="mapImage" 
                        name="book_all.jpg"
                        library="images"
                        alt="#{bundle.ChooseBook}"
                        usemap="#bookMap" />
        <bookstore:map id="bookMap" 
                       current="map1"
                       immediate="true"
                       action="bookstore">
            <f:actionListener
                type="dukesbookstore.listeners.MapBookChangeListener" />
            <bookstore:area id="map1" value="#{Book201}"
                            onmouseover="resources/images/book_201.jpg"
                            onmouseout="resources/images/book_all.jpg"
                            targetImage="mapImage" />
            <bookstore:area id="map2" value="#{Book202}" 
                            onmouseover="resources/images/book_202.jpg"
                            onmouseout="resources/images/book_all.jpg" 
                            targetImage="mapImage"/>
            ...
        </bookstore:map>
    ...
</h:form>
```

The `alt` attribute of the `h:graphicImage` tag maps to the localized
string `"Choose a Book from our Catalog"`.

The `f:actionListener` tag within the `bookstore:map` tag points to a
listener class for an action event. The `processAction` method of the
listener places the book ID for the selected map area into the session
map. The way this event is handled is explained more in [Handling Events
for Custom Components](jsf-custom008.htm#BNAWD).

The `action` attribute of the `bookstore:map` tag specifies a logical
outcome `String`, `"bookstore"`, which by implicit navigation rules
sends the application to the page `bookstore.xhtml`. For more
information on navigation, see [Configuring Navigation
Rules](jsf-configure010.htm#BNAXF).

The `immediate` attribute of the `bookstore:map` tag is set to `true`,
which indicates that the default `javax.faces.event.ActionListener`
implementation should execute during the Apply Request Values phase of
the request-processing lifecycle, instead of waiting for the Invoke
Application phase. Because the request resulting from clicking the map
does not require any validation, data conversion, or server-side object
updates, it makes sense to skip directly to the Invoke Application
phase.

The `current` attribute of the `bookstore:map` tag is set to the default
area, which is `map1` (the book My Early Years: Growing Up on Star7, by
Duke).

Notice that the `bookstore:area` tags do not contain any of the
JavaScript, coordinate, or shape data that is displayed on the HTML
page. The JavaScript is generated by the
`dukesbookstore.renderers.AreaRenderer` class. The `onmouseover` and
`onmouseout` attribute values indicate the image to be loaded when these
events occur. How the JavaScript is generated is explained more in
[Performing Encoding](jsf-custom005.htm#BNAVW).

The coordinate, shape, and alternate text data are obtained through the
`value` attribute, whose value refers to an attribute in application
scope. The value of this attribute is a bean, which stores the `coords`,
`shape`, and `alt` data. How these beans are stored in the application
scope is explained more in the next section.

## 15.3.4 Configuring Model Data

In a JavaServer Faces application, data such as the coordinates of a
hotspot of an image map is retrieved from the `value` attribute through
a bean. However, the shape and coordinates of a hotspot should be
defined together because the coordinates are interpreted differently
depending on what shape the hotspot is. Because a component's value can
be bound only to one property, the `value` attribute cannot refer to
both the shape and the coordinates.

To solve this problem, the application encapsulates all of this
information in a set of `ImageArea` objects. These objects are
initialized into application scope by the managed bean creation facility
(see [Section 16.5.1, "Using the managed-bean
Element"](jsf-configure005.htm#BNAWR)). Here is part of the managed bean
declaration for the `ImageArea` bean corresponding to the South America
hotspot:

``` oac_no_warn
<managed-bean eager="true">
    ...
    <managed-bean-name>Book201</managed-bean-name>
    <managed-bean-class>
        javaeetutorial.dukesbookstore.model.ImageArea
    </managed-bean-class>
    <managed-bean-scope>application</managed-bean-scope>
    <managed-property>
        ...
        <property-name>shape</property-name>
        <value>rect</value>
    </managed-property>
    <managed-property>
        ...
        <property-name>alt</property-name>
        <value>Duke</value>
    </managed-property>
    <managed-property>
        ...
        <property-name>coords</property-name>
        <value>67,23,212,268</value>
    </managed-property>
</managed-bean>
```

For more information on initializing managed beans with the managed bean
creation facility, see the section [Application Configuration Resource
File](jsf-configure003.htm#BNAWP).

The `value` attributes of the `bookstore:area` tags refer to the beans
in the application scope, as shown in this `bookstore:area` tag from
`index.xhtml`:

``` oac_no_warn
<bookstore:area id="map1" value="#{Book201}"
                onmouseover="resources/images/book_201.jpg"
                onmouseout="resources/images/book_all.jpg"
                targetImage="mapImage" />
```

To reference the `ImageArea` model object bean values from the component
class, you implement a `getValue` method in the component class. This
method calls `super.getValue`. The superclass of
tut-install`/examples/case-studies/dukes-bookstore/src/java/dukesbookstore/components/AreaComponent.java`,
`UIOutput`, has a `getValue` method that does the work of finding the
`ImageArea` object associated with `AreaComponent`. The `AreaRenderer`
class, which needs to render the `alt`, `shape`, and `coords` values
from the `ImageArea` object, calls the `getValue` method of
`AreaComponent` to retrieve the `ImageArea` object.

``` oac_no_warn
ImageArea iarea = (ImageArea) area.getValue();
```

`ImageArea` is a simple bean, so you can access the shape, coordinates,
and alternative text values by calling the appropriate accessor methods
of `ImageArea`. [Creating the Renderer Class](jsf-custom006.htm#BNAWB)
explains how to do this in the `AreaRenderer` class.

## 15.3.5 Summary of the Image Map Application Classes

[Table 15-2](#GLPEK) summarizes all the classes needed to implement the
image map component.

Table 15-2 Image Map Classes

<table style="width:26%;">
<colgroup>
<col width="26%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Class</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">AreaSelectedEvent</code></p></td>
<td><p>The <code dir="ltr">javax.faces.event.ActionEvent</code> indicating that an <code dir="ltr">AreaComponent</code> from the <code dir="ltr">MapComponent</code> has been selected.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">AreaComponent</code></p></td>
<td><p>The class that defines <code dir="ltr">AreaComponent</code>, which corresponds to the <code dir="ltr">bookstore:area</code> custom tag.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">MapComponent</code></p></td>
<td><p>The class that defines <code dir="ltr">MapComponent</code>, which corresponds to the <code dir="ltr">bookstore:map</code> custom tag.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">AreaRenderer</code></p></td>
<td><p>This <code dir="ltr">javax.faces.render.Renderer</code> performs the delegated rendering for <code dir="ltr">AreaComponent</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ImageArea</code></p></td>
<td><p>The bean that stores the shape and coordinates of the hotspots.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">MapBookChangeListener</code></p></td>
<td><p>The action listener for the <code dir="ltr">MapComponent</code>.</p></td>
</tr>
</tbody>
</table>

  

The Duke's Bookstore source directory, called bookstore-dir, is
tut-install`/examples/case-studies/dukes-bookstore/src/java/dukesbookstore/`.
The event and listener classes are located in
bookstore-dir`/listeners/`. The component classes are located in
bookstore-dir`/components/`. The renderer classes are located in
bookstore-dir`/renderers/`. `ImageArea` is located in
bookstore-dir`/model/`.

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
<td><a href="jsf-custom002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
