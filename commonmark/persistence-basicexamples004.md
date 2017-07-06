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
<td><a href="persistence-basicexamples003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-querylanguage.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 38.4 The address-book Application

The `address-book` example application is a simple web application that
stores contact data. It uses a single entity class, `Contact`, that uses
the Java API for JavaBeans Validation (Bean Validation) to validate the
data stored in the persistent attributes of the entity, as described in
[Validating Persistent Fields and
Properties](persistence-intro002.htm#GKAHQ).

The following topics are addressed here:

  - [Section 38.4.1, "Bean Validation Constraints in
    address-book"](#GKAOJ)

  - [Section 38.4.2, "Specifying Error Messages for Constraints in
    address-book"](#GKANL)

  - [Section 38.4.3, "Validating Contact Input from a JavaServer Faces
    Application"](#GKAON)

  - [Section 38.4.4, "Running the address-book Example"](#GKAOP)

## 38.4.1 Bean Validation Constraints in address-book

The `Contact` entity uses the `@NotNull`, `@Pattern`, and `@Past`
constraints on the persistent attributes.

The `@NotNull` constraint marks the attribute as a required field. The
attribute must be set to a non-null value before the entity can be
persisted or modified. Bean Validation will throw a validation error if
the attribute is null when the entity is persisted or modified.

The `@Pattern` constraint defines a regular expression that the value of
the attribute must match before the entity can be persisted or modified.
This constraint has two different uses in `address-book`.

  - The regular expression declared in the `@Pattern` annotation on the
    `email` field matches email addresses of the form name`@`domain
    name`.`top level domain, allowing only valid characters for email
    addresses. For example, `username@example.com` will pass validation,
    as will `firstname.lastname@mail.example.com`. However,
    `firstname,lastname@example.com`, which contains an illegal comma
    character in the local name, will fail validation.

  - The `mobilePhone` and `homePhone` fields are annotated with a
    `@Pattern` constraint that defines a regular expression to match
    phone numbers of the form `(`xxx`)` xxx`-`xxxx.

The `@Past` constraint is applied to the birthday field, which must be a
`java.util.Date` in the past.

Here are the relevant parts of the `Contact` entity class:

``` oac_no_warn
@Entity
public class Contact implements Serializable {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    @NotNull
    protected String firstName;
    @NotNull
    protected String lastName;
    @Pattern(regexp = "[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\\."
            + "[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*@"
            + "(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\\.)+[a-z0-9]"
            + "(?:[a-z0-9-]*[a-z0-9])?",
            message = "{invalid.email}")
    protected String email;
    @Pattern(regexp = "^\\(?(\\d{3})\\)?[- ]?(\\d{3})[- ]?(\\d{4})$",
            message = "{invalid.phonenumber}")
    protected String mobilePhone;
    @Pattern(regexp = "^\\(?(\\d{3})\\)?[- ]?(\\d{3})[- ]?(\\d{4})$",
            message = "{invalid.phonenumber}")
    protected String homePhone;
    @Temporal(javax.persistence.TemporalType.DATE)
    @Past
    protected Date birthday;
    ...
}
```

## 38.4.2 Specifying Error Messages for Constraints in address-book

Some of the constraints in the `Contact` entity specify an optional
message:

``` oac_no_warn
@Pattern(regexp = "^\\(?(\\d{3})\\)?[- ]?(\\d{3})[- ]?(\\d{4})$",
        message = "{invalid.phonenumber}")
protected String homePhone;
```

The optional message element in the `@Pattern` constraint overrides the
default validation message. The message can be specified directly:

``` oac_no_warn
@Pattern(regexp = "^\\(?(\\d{3})\\)?[- ]?(\\d{3})[- ]?(\\d{4})$",
        message = "Invalid phone number!")
protected String homePhone;
```

The constraints in `Contact`, however, are strings in the resource
bundle `ValidationMessages.properties`, under
tut-install`/examples/persistence/address-book/src/java/`. This allows
the validation messages to be located in one single properties file and
the messages to be easily localized. Overridden Bean Validation messages
must be placed in a resource bundle properties file named
`ValidationMessages.properties` in the default package, with localized
resource bundles taking the form
`ValidationMessages_`locale-prefix`.properties`. For example,
`ValidationMessages_es.properties` is the resource bundle used in
Spanish-speaking locales.

## 38.4.3 Validating Contact Input from a JavaServer Faces Application

The `address-book` application uses a JavaServer Faces web front end to
allow users to enter contacts. While JavaServer Faces has a form input
validation mechanism using tags in Facelets XHTML files, `address-book`
doesn't use these validation tags. Bean Validation constraints in
JavaServer Faces managed beans, in this case in the `Contact` entity,
automatically trigger validation when the forms are submitted.

The following code snippet from the `Create.xhtml` Facelets file shows
some of the input form for creating new `Contact` instances:

``` oac_no_warn
<h:form>
    <table columns="3" role="presentation">
        <tr>
            <td><h:outputLabel value="#{bundle.CreateContactLabel_firstName}" 
                               for="firstName" /></td>
            <td><h:inputText id="firstName" 
                             value="#{contactController.selected.firstName}" 
                             title="#{bundle.CreateContactTitle_firstName}"/>
            </td>
            <td><h:message for="firstName" /></td>
        </tr>
        <tr>
            <td><h:outputLabel value="#{bundle.CreateContactLabel_lastName}" 
                               for="lastName" /></td>
            <td><h:inputText id="lastName" 
                             value="#{contactController.selected.lastName}" 
                             title="#{bundle.CreateContactTitle_lastName}" />
            </td>
            <td><h:message for="lastName" /></td>
        </tr>
        ...
    </table>
</h:form>
```

The `<h:inputText>` tags `firstName` and `lastName` are bound to the
attributes in the `Contact` entity instance `selected` in the
`ContactController` stateless session bean. Each `<h:inputText>` tag has
an associated `<h:message>` tag that will display validation error
messages. The form doesn't require any JavaServer Faces validation tags,
however.

## 38.4.4 Running the address-book Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `address-book` application.

The following topics are addressed here:

  - [Section 38.4.4.1, "To Run the address-book Example Using NetBeans
    IDE"](#GKAOD)

  - [Section 38.4.4.2, "To Run the address-book Example Using
    Maven"](#GKANZ)

### 38.4.4.1 To Run the address-book Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  If the database server is not already running, start it by following
    the instructions in [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK).

3.  From the File menu, choose Open Project.

4.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/persistence
    ```

5.  Select the `address-book` folder.

6.  Click Open Project.

7.  In the Projects tab, right-click the `address-book` project and
    select Run.
    
    After the application has been deployed, a web browser window
    appears at the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/address-book/
    ```

8.  Click Show All Contact Items, then Create New Contact. Enter values
    in the fields; then click Save.
    
    If any of the values entered violate the constraints in `Contact`,
    an error message will appear in red beside the field with the
    incorrect values.

### 38.4.4.2 To Run the address-book Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  If the database server is not already running, start it by following
    the instructions in [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK).

3.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/persistence/address-book/
    ```

4.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This will compile and assemble the `address-book` application into a
    WAR. The WAR file is then deployed to GlassFish Server.

5.  Open a web browser window and enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/address-book/
    ```

6.  Click Show All Contact Items, then Create New Contact. Enter values
    in the fields; then click Save.
    
    If any of the values entered violate the constraints in `Contact`,
    an error message will appear in red beside the field with the
    incorrect values.

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
<td><a href="persistence-basicexamples003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-querylanguage.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
