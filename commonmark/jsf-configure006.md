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
<td><a href="jsf-configure005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 16.6 Registering Application Messages

Application messages can include any strings displayed to the user as
well as custom error messages (which are displayed by the `message` and
`messages` tags) for your custom converters or validators. To make
messages available at application startup time, do one of the following:

  - Queue an individual message onto the
    `javax.faces.context.FacesContext` instance programmatically, as
    described in [Using FacesMessage to Create a Message](#GKUHG)

  - Register all the messages with your application using the
    application configuration resource file

Here is the section of the `faces-config.xml` file that registers the
messages for the Duke's Bookstore case study application:

``` oac_no_warn
<application>
    <resource-bundle>
        <base-name>
            javaeetutorial.dukesbookstore.web.messages.Messages
        </base-name>
        <var>bundle</var>
    </resource-bundle>
    <locale-config>
        <default-locale>en</default-locale>
        <supported-locale>es</supported-locale>
        <supported-locale>de</supported-locale>
        <supported-locale>fr</supported-locale>
    </locale-config>
</application>
```

This set of elements causes the application to be populated with the
messages that are contained in the specified resource bundle.

The `resource-bundle` element represents a set of localized messages. It
must contain the fully qualified path to the resource bundle containing
the localized messages (in this case,
`dukesbookstore.web.messages.Messages`). The `var` element defines the
EL name by which page authors refer to the resource bundle.

The `locale-config` element lists the default locale and the other
supported locales. The `locale-config` element enables the system to
find the correct locale based on the browser's language settings.

The `supported-locale` and `default-locale` tags accept the lowercase,
two-character codes defined by ISO 639-1 (see
`http://www.loc.gov/standards/iso639-2/php/English_list.php`). Make sure
that your resource bundle actually contains the messages for the locales
you specify with these tags.

To access the localized message, the application developer merely
references the key of the message from the resource bundle.

You can pull localized text into an `alt` tag for a graphic image, as in
the following example:

``` oac_no_warn
<h:graphicImage id="mapImage" 
                name="book_all.jpg"
                library="images"
                alt="#{bundle.ChooseBook}"
                usemap="#bookMap" />
```

The `alt` attribute can accept value expressions. In this case, the
`alt` attribute refers to localized text that will be included in the
alternative text of the image rendered by this tag.

## 16.6.1 Using FacesMessage to Create a Message

Instead of registering messages in the application configuration
resource file, you can access the `java.util.ResourceBundle` directly
from managed bean code. The code snippet below locates an email error
message:

``` oac_no_warn
String message = "";
...
message = ExampleBean.loadErrorMessage(context,
    ExampleBean.EX_RESOURCE_BUNDLE_NAME,
         "EMailError");
context.addMessage(toValidate.getClientId(context),
    new FacesMessage(message));
```

These lines call the bean's `loadErrorMessage` method to get the message
from the `ResourceBundle`. Here is the `loadErrorMessage` method:

``` oac_no_warn
public static String loadErrorMessage(FacesContext context,
     String basename, String key) {
    if ( bundle == null ) {
         try {
            bundle = ResourceBundle.getBundle(basename,
                 context.getViewRoot().getLocale());
        } catch (Exception e) {
            return null;
        }
    }
    return bundle.getString(key);
}
```

## 16.6.2 Referencing Error Messages

A JavaServer Faces page uses the `message` or `messages` tags to access
error messages, as explained in [Displaying Error Messages with the
h:message and h:messages Tags](jsf-page002.htm#BNASO).

The error messages these tags access include

  - The standard error messages that accompany the standard converters
    and validators that ship with the API. (see Section 2.5.2.4 of the
    JavaServer Faces specification for a complete list of standard error
    messages)

  - Custom error messages contained in resource bundles registered with
    the application by the application architect using the
    `resource-bundle` element in the configuration file

When a converter or validator is registered on an input component, the
appropriate error message is automatically queued on the component.

A page author can override the error messages queued on a component by
using the following attributes of the component's tag:

  - `converterMessage`: References the error message to display when the
    data on the enclosing component cannot be converted by the converter
    registered on this component.

  - `requiredMessage`: References the error message to display when no
    value has been entered into the enclosing component.

  - `validatorMessage`: References the error message to display when the
    data on the enclosing component cannot be validated by the validator
    registered on this component.

All three attributes are enabled to take literal values and value
expressions. If an attribute uses a value expression, this expression
references the error message in a resource bundle. This resource bundle
must be made available to the application in one of the following ways:

  - By the application architect using the `resource-bundle` element in
    the configuration file

  - By the page author using the `f:loadBundle` tag

Conversely, the `resource-bundle` element must be used to make available
to the application those resource bundles containing custom error
messages that are queued on the component as a result of a custom
converter or validator being registered on the component.

The following tags show how to specify the `requiredMessage` attribute
using a value expression to reference an error message:

``` oac_no_warn
<h:inputText id="ccno" size="19"
    required="true"
    requiredMessage="#{customMessages.ReqMessage}">
    ...
</h:inputText>
<h:message styleClass="error-message" for="ccno"/>
```

The value expression used by `requiredMessage` in this example
references the error message with the `ReqMessage` key in the resource
bundle `customMessages`.

This message replaces the corresponding message queued on the component
and will display wherever the `message` or `messages` tag is placed on
the page.

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
<td><a href="jsf-configure005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
