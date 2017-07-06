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
<td><a href="jaxrs-advanced001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 31.2 Validating Resource Data with Bean Validation

JAX-RS supports the Bean Validation to verify JAX-RS resource classes.
This support consists of:

  - Adding constraint annotations to resource method parameters

  - Ensuring entity data is valid when the entity is passed in as a
    parameter

The following topics are addressed here:

  - [Section 31.2.1, "Using Constraint Annotations on Resource
    Methods"](#CIHJAFGI)

  - [Section 31.2.2, "Validating Entity Data"](#CIHFDCBI)

  - [Section 31.2.3, "Validation Exception Handling and Response
    Codes"](#CIHCHEFH)

## 31.2.1 Using Constraint Annotations on Resource Methods

Bean Validation constraint annotations may be applied to parameters for
a resource. The server will validate the parameters and either pass or
throw a `javax.validation.ValidationException`.

``` oac_no_warn
@POST
@Path("/createUser")
@Consumes(MediaType.APPLICATION_FORM_URLENCODED)
public void createUser(@NotNull @FormParam("username") String username,
                       @NotNull @FormParam("firstName") String firstName,
                       @NotNull @FormParam("lastName") String lastName,
                       @Email @FormParam("email") String email) {
    ...
}
```

In the preceding example, the built-in constraint `@NotNull` is applied
to the `username`, `firstName`, and `lastName` form fields. The
user-defined `@Email` constraint validates that the email address
supplied by the `email` form field is correctly formatted.

The constraints may also be applied to fields within a resource class.

``` oac_no_warn
@Path("/createUser")
public class CreateUserResource {
  @NotNull
  @FormParam("username")
  private String username;

  @NotNull
  @FormParam("firstName")
  private String firstName;

  @NotNull
  @FormParam("lastName")
  private String lastName;

  @Email
  @FormParam("email")
  private String email;

  ...
}
```

In the preceding example, the same constraints that were applied to the
method parameters in the previous example are applied to the class
fields. The behavior is the same in both examples.

Constraints may also be applied to a resource class's JavaBeans
properties by adding the constraint annotations to the getter method.

``` oac_no_warn
@Path("/createuser")
public class CreateUserResource {
  private String username;

  @FormParam("username")
  public void setUsername(String username) {
    this.username = username;
  }

  @NotNull
  public String getUsername() {
    return username;
  }
  ...
}
```

Constraints may also be applied at the resource class level. In the
following example, `@PhoneRequired` is a user-defined constraint that
ensures that a user enters at least one phone number. That is, either
`homePhone` or `mobilePhone` can be null, but not both.

``` oac_no_warn
@Path("/createUser")
@PhoneRequired
public class CreateUserResource {
  @FormParam("homePhone")
  private Phone homePhone;

  @FormParam("mobilePhone")
  private Phone mobilePhone;
  ...
}
```

## 31.2.2 Validating Entity Data

Classes that contain validation constraint annotations may be used in
method parameters in a resource class. To validate these entity classes,
use the `@Valid` annotation on the method parameter. For example, the
following class is a user-defined class containing both standard and
user-defined validation constraints.

``` oac_no_warn
@PhoneRequired
public class User {
  @NotNull
  private String username;

  private Phone homePhone;

  private Phone mobilePhone;
  ...
}
```

This entity class is used as a parameter to a resource method.

``` oac_no_warn
@Path("/createUser")
public class CreateUserResource {
  ...
  @POST
  @Consumers(MediaType.APPLICATION_XML)
  public void createUser(@Valid User user) {
    ...
  }
  ...
}
```

The `@Valid` annotation ensures that the entity class is validated at
runtime. Additional user-defined constraints can also trigger validation
of an entity.

``` oac_no_warn
@Path("/createUser")
public class CreateUserResource {
  ...
  @POST
  @Consumers(MediaType.APPLICATION_XML)
  public void createUser(@ActiveUser User user) {
    ...
  }
  ...
}
```

In the preceding example, the user-defined `@ActiveUser` constraint is
applied to the `User` class in addition to the `@PhoneRequired` and
`@NotNull` constraints defined within the entity class.

If a resource method returns an entity class, validation may be
triggered by applying the `@Valid` or any other user-defined constraint
annotation to the resource method.

``` oac_no_warn
@Path("/getUser")
public class GetUserResource {
  ...
  @GET
  @Path("{username}")
  @Produces(MediaType.APPLICATION_XML)
  @ActiveUser
  @Valid
  public User getUser(@PathParam("username") String username) {
    // find the User
    return user;
  }
  ...
}
```

As in the previous example, the `@ActiveUser` constraint is applied to
the returned entity class as well as the `@PhoneRequired` and `@NotNull`
constraints defined within the entity class.

## 31.2.3 Validation Exception Handling and Response Codes

If a `javax.validation.ValidationException` or any subclass of
`ValidationException` except `ConstraintValidationException` is thrown,
the JAX-RS runtime will respond to the client request with a 500
(Internal Server Error) HTTP status code.

If a `ConstraintValidationException` is thrown, the JAX-RS runtime will
respond to the client with one of the following HTTP status codes:

  - 500 (Internal Server Error) if the exception was thrown while
    validating a method return type

  - 400 (Bad Request) in all other cases

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
<td><a href="jaxrs-advanced001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
