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
<td><a href="jsf-custom005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 15.6 Delegating Rendering to a Renderer

Both `MapComponent` and `AreaComponent` delegate all of their rendering
to a separate renderer. The section [Performing
Encoding](jsf-custom005.htm#BNAVW) explains how `MapRenderer` performs
the encoding for `MapComponent`. This section explains in detail the
process of delegating rendering to a renderer using `AreaRenderer`,
which performs the rendering for `AreaComponent`.

To delegate rendering, you perform the tasks described in the following
topics:

  - [Section 15.6.1, "Creating the Renderer Class"](#BNAWB)

  - [Section 15.6.2, "Identifying the Renderer Type"](#BNAWC)

## 15.6.1 Creating the Renderer Class

When delegating rendering to a renderer, you can delegate all encoding
and decoding to the renderer, or you can choose to do part of it in the
component class. The `AreaComponent` class delegates encoding to the
`AreaRenderer` class.

The renderer class begins with a `@FacesRenderer` annotation:

``` oac_no_warn
@FacesRenderer(componentFamily = "Area", rendererType = "DemoArea")
public class AreaRenderer extends Renderer {
```

The `@FacesRenderer` annotation registers the renderer class with the
JavaServer Faces implementation as a renderer class. The annotation
identifies the component family as well as the renderer type.

To perform the rendering for `AreaComponent`, `AreaRenderer` must
implement an `encodeEnd` method. The `encodeEnd` method of
`AreaRenderer` retrieves the shape, coordinates, and alternative text
values stored in the `ImageArea` bean that is bound to `AreaComponent`.
Suppose that the `area` tag currently being rendered has a `value`
attribute value of `"book203"`. The following line from `encodeEnd` gets
the value of the attribute `"book203"` from the `FacesContext` instance:

``` oac_no_warn
ImageArea ia = (ImageArea)area.getValue();
```

The attribute value is the `ImageArea` bean instance, which contains the
`shape`, `coords`, and `alt` values associated with the `book203`
`AreaComponent` instance. [Configuring Model
Data](jsf-custom003.htm#GLPBO) describes how the application stores
these values.

After retrieving the `ImageArea` object, the method renders the values
for `shape`, `coords`, and `alt` by simply calling the associated
accessor methods and passing the returned values to the `ResponseWriter`
instance, as shown by these lines of code, which write out the shape and
coordinates:

``` oac_no_warn
writer.startElement("area", area);
writer.writeAttribute("alt", iarea.getAlt(), "alt");
writer.writeAttribute("coords", iarea.getCoords(), "coords");
writer.writeAttribute("shape", iarea.getShape(), "shape");
```

The `encodeEnd` method also renders the JavaScript for the `onmouseout`,
`onmouseover`, and `onclick` attributes. The Facelets page needs to
provide only the path to the images that are to be loaded during an
`onmouseover` or `onmouseout` action:

``` oac_no_warn
<bookstore:area id="map3" value="#{Book203}" 
                onmouseover="resources/images/book_203.jpg" 
                onmouseout="resources/images/book_all.jpg" 
                targetImage="mapImage"/>
```

The `AreaRenderer` class takes care of generating the JavaScript for
these actions, as shown in the following code from `encodeEnd`. The
JavaScript that `AreaRenderer` generates for the `onclick` action sets
the value of the hidden field to the value of the current area's
component ID and submits the page.

``` oac_no_warn
sb = new StringBuffer("document.forms[0]['").append(targetImageId).
        append("'].src='");
sb.append(
        getURI(context,
        (String) area.getAttributes().get("onmouseout")));
sb.append("'");
writer.writeAttribute("onmouseout", sb.toString(), "onmouseout");
sb = new StringBuffer("document.forms[0]['").append(targetImageId).
        append("'].src='");
sb.append(
        getURI(context,
        (String) area.getAttributes().get("onmouseover")));
sb.append("'");
writer.writeAttribute("onmouseover", sb.toString(), "onmouseover");
sb = new StringBuffer("document.forms[0]['");
sb.append(getName(context, area));
sb.append("'].value='");
sb.append(iarea.getAlt());
sb.append("'; document.forms[0].submit()");
writer.writeAttribute("onclick", sb.toString(), "value");
writer.endElement("area");
```

By submitting the page, this code causes the JavaServer Faces lifecycle
to return back to the Restore View phase. This phase saves any state
information, including the value of the hidden field, so that a new
request component tree is constructed. This value is retrieved by the
`decode` method of the `MapComponent` class. This decode method is
called by the JavaServer Faces implementation during the Apply Request
Values phase, which follows the Restore View phase.

In addition to the `encodeEnd` method, `AreaRenderer` contains an empty
constructor. This is used to create an instance of `AreaRenderer` so
that it can be added to the render kit.

The `@FacesRenderer` annotation registers the renderer class with the
JavaServer Faces implementation as a renderer class. The annotation
identifies the component family as well as the renderer type.

## 15.6.2 Identifying the Renderer Type

Register the renderer with a render kit by using the `@FacesRenderer`
annotation (or by using the application configuration resource file, as
explained in [Registering a Custom Renderer with a Render
Kit](jsf-configure011.htm#BNAXH)). During the Render Response phase, the
JavaServer Faces implementation calls the `getRendererType` method of
the component's tag handler to determine which renderer to invoke, if
there is one.

You identify the type associated with the renderer in the `rendererType`
element of the `@FacesRenderer` annotation for `AreaRenderer` as well as
in the `renderer-type` element of the tag library descriptor.

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
<td><a href="jsf-custom005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
