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
<td><a href="jsf-custom010.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom012.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 15.11 Creating and Using a Custom Converter

A JavaServer Faces converter class converts strings to objects and
objects to strings as required. Several standard converters are provided
by JavaServer Faces for this purpose. See [Using the Standard
Converters](jsf-page-core001.htm#BNAST) for more information on these
included converters.

As explained in [Conversion Model](jsf-intro005.htm#BNAQI), if the
standard converters included with JavaServer Faces cannot perform the
data conversion that you need, you can create a custom converter to
perform this specialized conversion. This implementation, at a minimum,
must define how to convert data both ways between the two views of the
data described in [Conversion Model](jsf-intro005.htm#BNAQI).

All custom converters must implement the `javax.faces.convert.Converter`
interface. This section explains how to implement this interface to
perform a custom data conversion.

The Duke's Bookstore case study uses a custom `Converter`
implementation, located in
tut-install`/examples/case-studies/dukes-bookstore/src/java/dukesbookstore/converters/CreditCardConverter.java`,
to convert the data entered in the Credit Card Number field on the
`bookcashier.xhtml` page. It strips blanks and hyphens from the text
string and formats it so that a blank space separates every four
characters.

Another common use case for a custom converter is in a list for a
nonstandard object type. In the Duke's Tutoring case study, the
`Student` and `Guardian` entities require a custom converter so that
they can be converted to and from a `UISelectItems` input component.

## 15.11.1 Creating a Custom Converter

The `CreditCardConverter` custom converter class is created as follows:

``` oac_no_warn
@FacesConverter("ccno")
public class CreditCardConverter implements Converter {
    ...
}
```

The `@FacesConverter` annotation registers the custom converter class as
a converter with the name of `ccno` with the JavaServer Faces
implementation. Alternatively, you can register the converter with
entries in the application configuration resource file, as shown in
[Registering a Custom Converter](jsf-configure009.htm#BNAXE).

To define how the data is converted from the presentation view to the
model view, the `Converter` implementation must implement the
`getAsObject(FacesContext, UIComponent, String)` method from the
`Converter` interface. Here is the implementation of this method from
`CreditCardConverter`:

``` oac_no_warn
@Override
public Object getAsObject(FacesContext context,
        UIComponent component, String newValue)
        throws ConverterException {

    if (newValue.isEmpty()) {
        return null;
    }
    // Since this is only a String to String conversion,
    // this conversion does not throw ConverterException.
    
    String convertedValue = newValue.trim();
    if ( (convertedValue.contains("-")) || (convertedValue.contains(" "))) {
        char[] input = convertedValue.toCharArray();
        StringBuilder builder = new StringBuilder(input.length);
        for (int i = 0; i < input.length; ++i) {
            if ((input[i] == '-') || (input[i] == ' ')) {
            } else {
                builder.append(input[i]);
            }
        }
        convertedValue = builder.toString();
    }
    return convertedValue;
}
```

During the Apply Request Values phase, when the components' `decode`
methods are processed, the JavaServer Faces implementation looks up the
component's local value in the request and calls the `getAsObject`
method. When calling this method, the JavaServer Faces implementation
passes in the current `FacesContext` instance, the component whose data
needs conversion, and the local value as a `String`. The method then
writes the local value to a character array, trims the hyphens and
blanks, adds the rest of the characters to a `String`, and returns the
`String`.

To define how the data is converted from the model view to the
presentation view, the `Converter` implementation must implement the
`getAsString(FacesContext, UIComponent, Object)` method from the
`Converter` interface. Here is an implementation of this method:

``` oac_no_warn
@Override
public String getAsString(FacesContext context,
        UIComponent component, Object value)
        throws ConverterException {
    
    String inputVal = null;
    if ( value == null ) {
        return "";
    }
    // value must be of a type that can be cast to a String.
    try {
        inputVal = (String)value;
    } catch (ClassCastException ce) {
        FacesMessage errMsg = new FacesMessage(CONVERSION_ERROR_MESSAGE_ID);
        FacesContext.getCurrentInstance().addMessage(null, errMsg);
        throw new ConverterException(errMsg.getSummary());
    }
    // insert spaces after every four characters for better
    // readability if they are not already present.
    char[] input = inputVal.toCharArray();
    StringBuilder builder = new StringBuilder(input.length + 3);
    for (int i = 0; i < input.length; ++i) {
        if ((i % 4) == 0 && (i != 0)) {
            if ({input[i] != ' ') || (input[i] != '-')){
                builder.append(" ");
                // if there are any "-"'s convert them to blanks.
            } else if (input[i] == '-') {
                builder.append(" ");
            }
         }
         builder.append(input[i]);
    }
    String convertedValue = builder.toString();
    return convertedValue;
}
```

During the Render Response phase, in which the components' `encode`
methods are called, the JavaServer Faces implementation calls the
`getAsString` method in order to generate the appropriate output. When
the JavaServer Faces implementation calls this method, it passes in the
current `FacesContext`, the `UIComponent` whose value needs to be
converted, and the bean value to be converted. Because this converter
does a `String`-to-`String` conversion, this method can cast the bean
value to a `String`.

If the value cannot be converted to a `String`, the method throws an
exception, passing an error message from the resource bundle that is
registered with the application. [Registering Application
Messages](jsf-configure006.htm#BNAXB) explains how to register custom
error messages with the application.

If the value can be converted to a `String`, the method reads the
`String` to a character array and loops through the array, adding a
space after every four characters.

You can also create a custom converter with a `@FacesConverter`
annotation that specifies the `forClass` attribute, as shown in the
following example from the Duke's Tutoring case study:

``` oac_no_warn
@FacesConverter(forClass=Guardian.class, value="guardian")
public class GuardianConverter extends EntityConverter implements Converter { ...
```

The `forClass` attribute registers the converter as the default
converter for the `Guardian` class. Therefore, whenever that class is
specified by a `value` attribute of an input component, the converter is
invoked automatically.

A converter class can be a separate Java POJO class, as in the Duke's
Bookstore case study. If it needs to access objects defined in a managed
bean class, however, it can be a subclass of a JavaServer Faces managed
bean, as in the `address-book` persistence example, in which the
converters use an enterprise bean that is injected into the managed bean
class.

## 15.11.2 Using a Custom Converter

To apply the data conversion performed by a custom converter to a
particular component's value, you must do one of the following.

  - Reference the converter from the component tag's `converter`
    attribute.

  - Nest an `f:converter` tag inside the component's tag and reference
    the custom converter from one of the `f:converter` tag's attributes.

If you are using the component tag's `converter` attribute, this
attribute must reference the `Converter` implementation's identifier or
the fully-qualified class name of the converter. [Creating and Using a
Custom Converter](#BNAUS) explains how to implement a custom converter.

The identifier for the credit card converter class is `ccno`, the value
specified in the `@FacesConverter` annotation:

``` oac_no_warn
@FacesConverter("ccno")
public class CreditCardConverter implements Converter {
    ...
```

Therefore, the `CreditCardConverter` instance can be registered on the
`ccno` component as shown in the following example:

``` oac_no_warn
<h:inputText id="ccno"
             size="19"
             converter="ccno"
             value="#{cashierBean.creditCardNumber}"
             required="true"
             requiredMessage="#{bundle.ReqCreditCard}">
    ...
</h:inputText>
```

By setting the `converter` attribute of a component's tag to the
converter's identifier or its class name, you cause that component's
local value to be automatically converted according to the rules
specified in the `Converter` implementation.

Instead of referencing the converter from the component tag's
`converter` attribute, you can reference the converter from an
`f:converter` tag nested inside the component's tag. To reference the
custom converter using the `f:converter` tag, you do one of the
following.

  - Set the `f:converter` tag's `converterId` attribute to the
    `Converter` implementation's identifier defined in the
    `@FacesConverter` annotation or in the application configuration
    resource file. This method is shown in `bookcashier.xhtml`:
    
    ``` oac_no_warn
    <h:inputText id="ccno" 
                 size="19"
                 value="#{cashierBean.creditCardNumber}"
                 required="true"
                 requiredMessage="#{bundle.ReqCreditCard}">
        <f:converter converterId="ccno"/>
        <f:validateRegex 
           pattern="\d{16}|\d{4} \d{4} \d{4} \d{4}|\d{4}-\d{4}-\d{4}-\d{4}"/>
    </h:inputText>
    ```

  - Bind the `Converter` implementation to a managed bean property using
    the `f:converter` tag's `binding` attribute, as described in
    [Binding Converters, Listeners, and Validators to Managed Bean
    Properties](jsf-custom014.htm#BNATM).

The JavaServer Faces implementation calls the converter's `getAsObject`
method to strip spaces and hyphens from the input value. The
`getAsString` method is called when the `bookcashier.xhtml` page is
redisplayed; this happens if the user orders more than $100 worth of
books.

In the Duke's Tutoring case study, each converter is registered as the
converter for a particular class. The converter is automatically invoked
whenever that class is specified by a `value` attribute of an input
component. In the following example, the `itemValue` attribute
(highlighted in bold) calls the converter for the `Guardian` class:

``` oac_no_warn
<h:selectManyListbox id="selectGuardiansMenu"
                     title="#{bundle['action.add.guardian']}"
                     value="#{guardianManager.selectedGuardians}"
                     size="5"
                     converter="guardian">
    <f:selectItems value="#{guardianManager.allGuardians}"
                   var="selectedGuardian"
                   itemLabel="#{selectedGuardian.name}"
                   itemValue="#{selectedGuardian}" />
</h:selectManyListbox>
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
<td><a href="jsf-custom010.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom012.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
