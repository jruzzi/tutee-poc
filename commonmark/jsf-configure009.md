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
<td><a href="jsf-configure008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure010.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 16.9 Registering a Custom Converter

As is the case with a custom validator, if the application developer
creates a custom converter, you must register it with the application
either by using the `@FacesConverter` annotation, as described in
[Creating a Custom Converter](jsf-custom011.htm#GLPHB), or by using the
`converter` XML element in the application configuration resource file.
Here is a hypothetical `converter` configuration for
`CreditCardConverter` from the Duke's Bookstore case study:

``` oac_no_warn
<converter>
    <description>
        Converter for credit card numbers that normalizes
        the input to a standard format
    </description>
    <converter-id>CreditCardConverter</converter-id>
    <converter-class>
        dukesbookstore.converters.CreditCardConverter
    </converter-class>
</converter>
```

Attributes specified in a `converter` tag override any settings in the
`@FacesConverter` annotation.

The `converter` element represents a `javax.faces.convert.Converter`
implementation and contains required `converter-id` and
`converter-class` elements.

The `converter-id` element identifies an ID that is used by the
`converter` attribute of a UI component tag to apply the converter to
the component's data. [Using a Custom
Converter](jsf-custom011.htm#BNATU) includes an example of referencing
the custom converter from a component tag.

The `converter-class` element identifies the `Converter` implementation.

[Creating and Using a Custom Converter](jsf-custom011.htm#BNAUS)
explains how to create a custom converter.

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
<td><a href="jsf-configure008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure010.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
