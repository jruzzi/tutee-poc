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
<td><a href="jsf-page-core.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-page-core002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 11.1 Using the Standard Converters

The JavaServer Faces implementation provides a set of `Converter`
implementations that you can use to convert component data. The purpose
of conversion is to take the String-based data coming in from the
Servlet API and convert it to strongly typed Java objects suitable for
the business domain. For more information on the conceptual details of
the conversion model, see [Conversion Model](jsf-intro005.htm#BNAQI).

The standard `Converter` implementations are located in the
`javax.faces.convert` package. Normally, converters are implicitly
assigned based on the type of the EL expression pointed to by the value
of the component. However, these converters can also be accessed by a
converter ID. [Table 11-1](#CHDIHIIC) shows the converter classes and
their associated converter IDs.

Table 11-1 Converter Classes and Converter IDs

<table style="width:48%;">
<colgroup>
<col width="48%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Class in the javax.faces.convert Package</th>
<th>Converter ID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">BigDecimalConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.BigDecimal</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">BigIntegerConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.BigInteger</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">BooleanConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.Boolean</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">ByteConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.Byte</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">CharacterConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.Character</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">DateTimeConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.DateTime</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">DoubleConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.Double</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">EnumConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.Enum</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">FloatConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.Float</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">IntegerConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.Integer</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">LongConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.Long</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">NumberConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.Number</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ShortConverter</code></p></td>
<td><p><code dir="ltr">javax.faces.Short</code></p></td>
</tr>
</tbody>
</table>

  

A standard error message is associated with each of these converters. If
you have registered one of these converters onto a component on your
page and the converter is not able to convert the component's value, the
converter's error message will display on the page. For example, the
following error message appears if `BigIntegerConverter` fails to
convert a value:

``` oac_no_warn
{0} must be a number consisting of one or more digits
```

In this case, the `{0}` substitution parameter will be replaced with the
name of the input component on which the converter is registered.

Two of the standard converters (`DateTimeConverter` and
`NumberConverter`) have their own tags, which allow you to configure the
format of the component data using the tag attributes. For more
information about using `DateTimeConverter`, see [Using
DateTimeConverter](#BNASV). For more information about using
`NumberConverter`, see [Using NumberConverter](#BNASX). The following
section explains how to convert a component's value, including how to
register other standard converters with a component.

## 11.1.1 Converting a Component's Value

To use a particular converter to convert a component's value, you need
to register the converter onto the component. You can register any of
the standard converters in one of the following ways.

  - Nest one of the standard converter tags inside the component's tag.
    These tags are `f:convertDateTime` and `f:convertNumber`, which are
    described in [Using DateTimeConverter](#BNASV) and [Using
    NumberConverter](#BNASX), respectively.

  - Bind the value of the component to a managed bean property of the
    same type as the converter. This is the most common technique.

  - Refer to the converter from the component tag's `converter`
    attribute, specifying the ID of the converter class.

  - Nest an `f:converter` tag inside of the component tag, and use
    either the `f:converter` tag's `converterId` attribute or its
    `binding` attribute to refer to the converter.

As an example of the second technique, if you want a component's data to
be converted to an `Integer`, you can simply bind the component's value
to a managed bean property. Here is an example:

``` oac_no_warn
Integer age = 0;
public Integer getAge(){ return age;}
public void setAge(Integer age) {this.age = age;}
```

The data from the `h:inputText` tag in the this example will be
converted to a `java.lang.Integer` value. The `Integer` type is a
supported type of `NumberConverter`. If you don't need to specify any
formatting instructions using the `f:convertNumber` tag attributes, and
if one of the standard converters will suffice, you can simply reference
that converter by using the component tag's `converter` attribute.

You can also nest an `f:converter` tag within the component tag and use
either the converter tag's `converterId` attribute or its `binding`
attribute to reference the converter.

The `converterId` attribute must reference the converter's ID. Here is
an example that uses one of the converter IDs listed in [Table
11-1](#CHDIHIIC):

``` oac_no_warn
<h:inputText value="#{loginBean.age}">
    <f:converter converterId="javax.faces.Integer" />
</h:inputText>
```

Instead of using the `converterId` attribute, the `f:converter` tag can
use the `binding` attribute. The `binding` attribute must resolve to a
bean property that accepts and returns an appropriate `Converter`
instance.

You can also create custom converters and register them on components
using the `f:converter` tag. For details, see [Creating and Using a
Custom Converter](jsf-custom011.htm#BNAUS).

## 11.1.2 Using DateTimeConverter

You can convert a component's data to a `java.util.Date` by nesting the
`convertDateTime` tag inside the component tag. The `convertDateTime`
tag has several attributes that allow you to specify the format and type
of the data. [Table 11-2](#BNASW) lists the attributes.

Here is a simple example of a `convertDateTime` tag:

``` oac_no_warn
<h:outputText value="#{cashierBean.shipDate}">
    <f:convertDateTime type="date" dateStyle="full" />
</h:outputText>
```

When binding the `DateTimeConverter` to a component, ensure that the
managed bean property to which the component is bound is of type
`java.util.Date`. In the preceding example, `cashierBean.shipDate` must
be of type `java.util.Date`.

The example tag can display the following output:

``` oac_no_warn
Saturday, September 21, 2013
```

You can also display the same date and time by using the following tag
in which the date format is specified:

``` oac_no_warn
<h:outputText value="#{cashierBean.shipDate}">
    <f:convertDateTime pattern="EEEEEEEE, MMM dd, yyyy" />
</h:outputText>
```

If you want to display the example date in Spanish, you can use the
`locale` attribute:

``` oac_no_warn
<h:outputText value="#{cashierBean.shipDate}">
    <f:convertDateTime dateStyle="full"
                       locale="es"
                       timeStyle="long" type="both" />
</h:outputText>
```

This tag would display the following output:

``` oac_no_warn
jueves 24 de octubre de 2013 15:07:04 GMT
```

Refer to the "Customizing Formats" lesson of the Java Tutorial at
`http://docs.oracle.com/javase/tutorial/i18n/format/simpleDateFormat.html`
for more information on how to format the output using the `pattern`
attribute of the `convertDateTime` tag.

Table 11-2 Attributes for the f:convertDateTime Tag

<table style="width:36%;">
<colgroup>
<col width="13%" />
<col width="23%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">binding</code></p></td>
<td><p><code dir="ltr">DateTimeConverter</code></p></td>
<td><p>Used to bind a converter to a managed bean property.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">dateStyle</code></p></td>
<td><p><code dir="ltr">String</code></p></td>
<td><p>Defines the format, as specified by <code dir="ltr">java.text.DateFormat</code>, of a date or the date part of a <code dir="ltr">date</code> string. Applied only if <code dir="ltr">type</code> is <code dir="ltr">date</code> or <code dir="ltr">both</code> and if <code dir="ltr">pattern</code> is not defined. Valid values: <code dir="ltr">default</code>, <code dir="ltr">short</code>, <code dir="ltr">medium</code>, <code dir="ltr">long</code>, and <code dir="ltr">full</code>. If no value is specified, <code dir="ltr">default</code> is used.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">for</code></p></td>
<td><p><code dir="ltr">String</code></p></td>
<td><p>Used with composite components. Refers to one of the objects within the composite component inside which this tag is nested.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">locale</code></p></td>
<td><p><code dir="ltr">String</code> or <code dir="ltr">Locale</code></p></td>
<td><p><code dir="ltr">Locale</code> whose predefined styles for dates and times are used during formatting or parsing. If not specified, the <code dir="ltr">Locale</code> returned by <code dir="ltr">FacesContext.getLocale</code> will be used.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">pattern</code></p></td>
<td><p><code dir="ltr">String</code></p></td>
<td><p>Custom formatting pattern that determines how the date/time string should be formatted and parsed. If this attribute is specified, <code dir="ltr">dateStyle</code>, <code dir="ltr">timeStyle</code>, and <code dir="ltr">type</code> attributes are ignored.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">timeStyle</code></p></td>
<td><p><code dir="ltr">String</code></p></td>
<td><p>Defines the format, as specified by <code dir="ltr">java.text.DateFormat</code>, of a <code dir="ltr">time</code> or the time part of a <code dir="ltr">date</code> string. Applied only if <code dir="ltr">type</code> is time and <code dir="ltr">pattern</code> is not defined. Valid values: <code dir="ltr">default</code>, <code dir="ltr">short</code>, <code dir="ltr">medium</code>, <code dir="ltr">long</code>, and <code dir="ltr">full</code>. If no value is specified, <code dir="ltr">default</code> is used.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">timeZone</code></p></td>
<td><p><code dir="ltr">String</code> or <code dir="ltr">TimeZone</code></p></td>
<td><p>Time zone in which to interpret any time information in the <code dir="ltr">date</code> string.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">type</code></p></td>
<td><p><code dir="ltr">String</code></p></td>
<td><p>Specifies whether the string value will contain a date, a time, or both. Valid values are <code dir="ltr">date</code>, <code dir="ltr">time</code>, or <code dir="ltr">both</code>. If no value is specified, <code dir="ltr">date</code> is used.</p></td>
</tr>
</tbody>
</table>

  

## 11.1.3 Using NumberConverter

You can convert a component's data to a `java.lang.Number` by nesting
the `convertNumber` tag inside the component tag. The `convertNumber`
tag has several attributes that allow you to specify the format and type
of the data. [Table 11-3](#BNASY) lists the attributes.

The following example uses a `convertNumber` tag to display the total
prices of the contents of a shopping cart:

``` oac_no_warn
<h:outputText value="#{cart.total}">
    <f:convertNumber currencySymbol="$" type="currency"/>
</h:outputText>
```

When binding the `NumberConverter` to a component, ensure that the
managed bean property to which the component is bound is of a primitive
type or has a type of `java.lang.Number`. In the preceding example,
`cart.total` is of type `double`.

Here is an example of a number that this tag can display:

``` oac_no_warn
$934
```

This result can also be displayed by using the following tag in which
the currency pattern is specified:

``` oac_no_warn
<h:outputText id="cartTotal" value="#{cart.total}">
    <f:convertNumber pattern="$####" />
</h:outputText>
```

See the "Customizing Formats" lesson of the Java Tutorial at
`http://docs.oracle.com/javase/tutorial/i18n/format/decimalFormat.html`
for more information on how to format the output by using the `pattern`
attribute of the `convertNumber` tag.

Table 11-3 Attributes for the f:convertNumber Tag

<table style="width:46%;">
<colgroup>
<col width="25%" />
<col width="21%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">binding</code></p></td>
<td><p><code dir="ltr">NumberConverter</code></p></td>
<td><p>Used to bind a converter to a managed bean property.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">currencyCode</code></p></td>
<td><p><code dir="ltr">String</code></p></td>
<td><p>ISO 4217 currency code, used only when formatting currencies.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">currencySymbol</code></p></td>
<td><p><code dir="ltr">String</code></p></td>
<td><p>Currency symbol, applied only when formatting currencies.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">for</code></p></td>
<td><p><code dir="ltr">String</code></p></td>
<td><p>Used with composite components. Refers to one of the objects within the composite component inside which this tag is nested.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">groupingUsed</code></p></td>
<td><p><code dir="ltr">Boolean</code></p></td>
<td><p>Specifies whether formatted output contains grouping separators.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">integerOnly</code></p></td>
<td><p><code dir="ltr">Boolean</code></p></td>
<td><p>Specifies whether only the integer part of the value will be parsed.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">locale</code></p></td>
<td><p><code dir="ltr">String</code> or <code dir="ltr">Locale</code></p></td>
<td><p><code dir="ltr">Locale</code> whose number styles are used to format or parse data.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">maxFractionDigits</code></p></td>
<td><p><code dir="ltr">int</code></p></td>
<td><p>Maximum number of digits formatted in the fractional part of the output.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">maxIntegerDigits</code></p></td>
<td><p><code dir="ltr">int</code></p></td>
<td><p>Maximum number of digits formatted in the integer part of the output.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">minFractionDigits</code></p></td>
<td><p><code dir="ltr">int</code></p></td>
<td><p>Minimum number of digits formatted in the fractional part of the output.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">minIntegerDigits</code></p></td>
<td><p><code dir="ltr">int</code></p></td>
<td><p>Minimum number of digits formatted in the integer part of the output.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">pattern</code></p></td>
<td><p><code dir="ltr">String</code></p></td>
<td><p>Custom formatting pattern that determines how the number string is formatted and parsed.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">type</code></p></td>
<td><p><code dir="ltr">String</code></p></td>
<td><p>Specifies whether the string value is parsed and formatted as a <code dir="ltr">number</code>, <code dir="ltr">currency</code>, or <code dir="ltr">percentage</code>. If not specified, <code dir="ltr">number</code> is used.</p></td>
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
<td><a href="jsf-page-core.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-page-core002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
