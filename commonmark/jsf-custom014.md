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
<td><a href="jsf-custom013.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft:
2017-06-12

# 15.14 Binding Converters, Listeners, and Validators to Managed Bean Properties

As described in [Adding Components to a Page Using HTML Tag Library
Tags](jsf-page002.htm#BNARF), a page author can bind converter,
listener, and validator implementations to managed bean properties using
the `binding` attributes of the tags that are used to register the
implementations on components.

This technique has similar advantages to binding component instances to
managed bean properties, as described in [Binding Component Values and
Instances to Managed Bean Properties](jsf-custom013.htm#BNATG). In
particular, binding a converter, listener, or validator implementation
to a managed bean property yields the following benefits.

  - The managed bean can instantiate the implementation instead of
    allowing the page author to do so.

  - The managed bean can programmatically modify the attributes of the
    implementation. In the case of a custom implementation, the only
    other way to modify the attributes outside of the implementation
    class would be to create a custom tag for it and require the page
    author to set the attribute values from the page.

Whether you are binding a converter, listener, or validator to a managed
bean property, the process is the same for any of the implementations.

  - Nest the converter, listener, or validator tag within an appropriate
    component tag.

  - Make sure that the managed bean has a property that accepts and
    returns the converter, listener, or validator implementation class
    that you want to bind to the property.

  - Reference the managed bean property using a value expression from
    the `binding` attribute of the converter, listener, or validator
    tag.

For example, say that you want to bind the standard `DateTime` converter
to a managed bean property because you want to set the formatting
pattern of the user's input in the managed bean rather than on the
Facelets page. First, the page registers the converter onto the
component by nesting the `f:convertDateTime` tag within the component
tag. Then, the page references the property with the `binding` attribute
of the `f:convertDateTime` tag:

``` oac_no_warn
<h:inputText value="#{loginBean.birthDate}">
    <f:convertDateTime binding="#{loginBean.convertDate}" />
</h:inputText>
```

The `convertDate` property would look something like this:

``` oac_no_warn
private DateTimeConverter convertDate;
public DateTimeConverter getConvertDate() {
    ...
    return convertDate;
}
public void setConvertDate(DateTimeConverter convertDate) {
    convertDate.setPattern("EEEEEEEE, MMM dd, yyyy");
    this.convertDate = convertDate;
}
```

See [Writing Properties Bound to Converters, Listeners, or
Validators](jsf-develop002.htm#BNAUL) for more information on writing
managed bean properties for converter, listener, and validator
implementations.

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
<td><a href="jsf-custom013.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
