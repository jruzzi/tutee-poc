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
<td><a href="jsf-facelets004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 8.5 Composite Components

JavaServer Faces technology offers the concept of composite components
with Facelets. A composite component is a special type of template that
acts as a component.

Any component is essentially a piece of reusable code that behaves in a
particular way. For example, an input component accepts user input. A
component can also have validators, converters, and listeners attached
to it to perform certain defined actions.

A composite component consists of a collection of markup tags and other
existing components. This reusable, user-created component has a
customized, defined functionality and can have validators, converters,
and listeners attached to it like any other component.

With Facelets, any XHTML page that contains markup tags and other
components can be converted into a composite component. Using the
resources facility, the composite component can be stored in a library
that is available to the application from the defined resources
location.

[Table 8-3](#GJCWC) lists the most commonly used composite tags and
their functions.

Table 8-3 Composite Component Tags

<table style="width:39%;">
<colgroup>
<col width="39%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">composite:interface</code></p></td>
<td><p>Declares the usage contract for a composite component. The composite component can be used as a single component whose feature set is the union of the features declared in the usage contract.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">composite:implementation</code></p></td>
<td><p>Defines the implementation of the composite component. If a <code dir="ltr">composite:interface</code> element appears, there must be a corresponding <code dir="ltr">composite:implementation</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">composite:attribute</code></p></td>
<td><p>Declares an attribute that may be given to an instance of the composite component in which this tag is declared.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">composite:insertChildren</code></p></td>
<td><p>Any child components or template text within the composite component tag in the using page will be reparented into the composite component at the point indicated by this tag's placement within the <code dir="ltr">composite:implementation</code> section.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">composite:valueHolder</code></p></td>
<td><p>Declares that the composite component whose contract is declared by the <code dir="ltr">composite:interface</code> in which this element is nested exposes an implementation of <code dir="ltr">ValueHolder</code> suitable for use as the target of attached objects in the using page.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">composite:editableValueHolder</code></p></td>
<td><p>Declares that the composite component whose contract is declared by the <code dir="ltr">composite:interface</code> in which this element is nested exposes an implementation of <code dir="ltr">EditableValueHolder</code> suitable for use as the target of attached objects in the using page.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">composite:actionSource</code></p></td>
<td><p>Declares that the composite component whose contract is declared by the <code dir="ltr">composite:interface</code> in which this element is nested exposes an implementation of <code dir="ltr">ActionSource2</code> suitable for use as the target of attached objects in the using page.</p></td>
</tr>
</tbody>
</table>

  

For more information and a complete list of Facelets composite tags, see
the [JavaServer Faces Facelets Tag Library documentation](olink:JSFTL).

The following example shows a composite component that accepts an email
address as input:

``` oac_no_warn
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
  xmlns:composite="http://xmlns.jcp.org/jsf/composite"
  xmlns:h="http://xmlns.jcp.org/jsf/html">

    <h:head>
        <title>This content will not be displayed</title>
    </h:head>
    <h:body>
        <composite:interface>
            <composite:attribute name="value" required="false"/>
        </composite:interface>

        <composite:implementation>
            <h:outputLabel value="Email id: "></h:outputLabel>
            <h:inputText value="#{cc.attrs.value}"></h:inputText>
        </composite:implementation>
    </h:body>
</html>
```

Note the use of `cc.attrs.value` when defining the value of the
`inputText` component. The word `cc` in JavaServer Faces is a reserved
word for composite components. The `#{cc.attrs.`attribute-name`}`
expression is used to access the attributes defined for the composite
component's interface, which in this case happens to be `value`.

The preceding example content is stored as a file named `email.xhtml` in
a folder named `resources/emcomp`, under the application web root
directory. This directory is considered a library by JavaServer Faces,
and a component can be accessed from such a library. For more
information on resources, see [Web
Resources](jsf-facelets006.htm#GIRGM).

The web page that uses this composite component is generally called a
using page. The using page includes a reference to the composite
component, in the `xml` namespace declarations:

``` oac_no_warn
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
  xmlns:h="http://xmlns.jcp.org/jsf/html"
  xmlns:em="http://xmlns.jcp.org/jsf/composite/emcomp">

    <h:head>
        <title>Using a sample composite component</title>
    </h:head>

    <body>
        <h:form>
            <em:email value="Enter your email id" />
        </h:form>
    </body>
</html>
```

The local composite component library is defined in the `xmlns`
namespace with the declaration
`xmlns:em="http://xmlns.jcp.org/jsf/composite/emcomp"`. The component
itself is accessed through the `em:email` tag. The preceding example
content can be stored as a web page named `emuserpage.xhtml` under the
web root directory. When compiled and deployed on a server, it can be
accessed with the following URL:

``` oac_no_warn
http://localhost:8080/application-name/emuserpage.xhtml
```

See [Chapter 14, "Composite Components: Advanced Topics and an
Example,"](jsf-advanced-cc.htm#GKHXA) for more information and an
example.

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
<td><a href="jsf-facelets004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
