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
<td><a href="jsf-page-core002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-page-core004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 11.3 Using the Standard Validators

JavaServer Faces technology provides a set of standard classes and
associated tags that page authors and application developers can use to
validate a component's data. [Table 11-5](#BNATD) lists all the standard
validator classes and the tags that allow you to use the validators from
the page.

Table 11-5 The Validator Classes

<table style="width:53%;">
<colgroup>
<col width="27%" />
<col width="26%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Validator Class</th>
<th>Tag</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">BeanValidator</code></p></td>
<td><p><code dir="ltr">validateBean</code></p></td>
<td><p>Registers a bean validator for the component.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">DoubleRangeValidator</code></p></td>
<td><p><code dir="ltr">validateDoubleRange</code></p></td>
<td><p>Checks whether the local value of a component is within a certain range. The value must be floating-point or convertible to floating-point.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">LengthValidator</code></p></td>
<td><p><code dir="ltr">validateLength</code></p></td>
<td><p>Checks whether the length of a component's local value is within a certain range. The value must be a <code dir="ltr">java.lang.String</code>.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">LongRangeValidator</code></p></td>
<td><p><code dir="ltr">validateLongRange</code></p></td>
<td><p>Checks whether the local value of a component is within a certain range. The value must be any numeric type or <code dir="ltr">String</code> that can be converted to a <code dir="ltr">long</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">RegexValidator</code></p></td>
<td><p><code dir="ltr">validateRegex</code></p></td>
<td><p>Checks whether the local value of a component is a match against a regular expression from the <code dir="ltr">java.util.regex</code> package.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">RequiredValidator</code></p></td>
<td><p><code dir="ltr">validateRequired</code></p></td>
<td><p>Ensures that the local value is not empty on an <code dir="ltr">EditableValueHolder</code> component.</p></td>
</tr>
</tbody>
</table>

  

All of these validator classes implement the `Validator` interface.
Component writers and application developers can also implement this
interface to define their own set of constraints for a component's
value.

Similar to the standard converters, each of these validators has one or
more standard error messages associated with it. If you have registered
one of these validators onto a component on your page and the validator
is unable to validate the component's value, the validator's error
message will display on the page. For example, the error message that
displays when the component's value exceeds the maximum value allowed by
`LongRangeValidator` is as follows:

``` oac_no_warn
{1}: Validation Error: Value is greater than allowable maximum of "{0}"
```

In this case, the `{1}` substitution parameter is replaced by the
component's label or `id`, and the `{0}` substitution parameter is
replaced with the maximum value allowed by the validator.

See [Displaying Error Messages with the h:message and h:messages
Tags](jsf-page002.htm#BNASO) for information on how to display
validation error messages on the page when validation fails.

Instead of using the standard validators, you can use Bean Validation to
validate data. If you specify bean validation constraints on your
managed bean properties, the constraints are automatically placed on the
corresponding fields on your applications web pages. See [Chapter 21,
"Introduction to Bean Validation"](bean-validation.htm#CHDGJIIA) for
more information. You do not need to specify the `validateBean` tag to
use Bean Validation, but the tag allows you to use more advanced Bean
Validation features. For example, you can use the `validationGroups`
attribute of the tag to specify constraint groups.

You can also create and register custom validators, although Bean
Validation has made this feature less useful. For details, see [Creating
and Using a Custom Validator](jsf-custom012.htm#BNAUW).

## 11.3.1 Validating a Component's Value

To validate a component's value using a particular validator, you need
to register that validator on the component. You can do this in one of
the following ways.

  - Nest the validator's corresponding tag (shown in [Table
    11-5](#BNATD)) inside the component's tag. [Using Validator
    Tags](#BNATF) explains how to use the `validateLongRange` tag. You
    can use the other standard tags in the same way.

  - Refer to a method that performs the validation from the component
    tag's `validator` attribute.

  - Nest a validator tag inside the component tag, and use either the
    validator tag's `validatorId` attribute or its `binding` attribute
    to refer to the validator.

See [Referencing a Method That Performs
Validation](jsf-page-core004.htm#BNATR) for more information on using
the `validator` attribute.

The `validatorId` attribute works similarly to the `converterId`
attribute of the `converter` tag, as described in [Converting a
Component's Value](jsf-page-core001.htm#BNASU).

Keep in mind that validation can be performed only on components that
implement `EditableValueHolder`, because these components accept values
that can be validated.

## 11.3.2 Using Validator Tags

The following example shows how to use the `f:validateLongRange`
validator tag on an input component named `quantity`:

``` oac_no_warn
<h:inputText id="quantity" size="4" value="#{item.quantity}">
    <f:validateLongRange minimum="1"/>
</h:inputText>
<h:message for="quantity"/>
```

This tag requires the user to enter a number that is at least 1. The
`validateLongRange` tag also has a `maximum` attribute, which sets a
maximum value for the input.

The attributes of all the standard validator tags accept EL value
expressions. This means that the attributes can reference managed bean
properties rather than specify literal values. For example, the
`f:validateLongRange` tag in the preceding example can reference managed
bean properties called `minimum` and `maximum` to get the minimum and
maximum values acceptable to the validator implementation, as shown in
this snippet from the `guessnumber-jsf` example:

``` oac_no_warn
<h:inputText id="userNo"
             title="Type a number from 0 to 10:"
             value="#{userNumberBean.userNumber}">
    <f:validateLongRange minimum="#{userNumberBean.minimum}"
                         maximum="#{userNumberBean.maximum}"/>
</h:inputText>
```

The following `f:validateRegex` tag shows how you might ensure that a
password is from 4 to 10 characters long and contains at least one
digit, at least one lowercase letter, and at least one uppercase letter:

``` oac_no_warn
<f:validateRegex pattern="((?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{4,10})"
                 for="passwordVal"/>
```

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
<td><a href="jsf-page-core002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-page-core004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
