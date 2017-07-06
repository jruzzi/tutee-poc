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
<td><a href="jaxrs-advanced.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 31.1 Annotations for Field and Bean Properties of Resource Classes

JAX-RS annotations for resource classes let you extract specific parts
or values from a Uniform Resource Identifier (URI) or request header.

JAX-RS provides the annotations listed in [Table 31-1](#GKOBO).

Table 31-1 Advanced JAX-RS Annotations

<table style="width:22%;">
<colgroup>
<col width="22%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Annotation</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">@Context</code></p></td>
<td><p>Injects information into a class field, bean property, or method parameter</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@CookieParam</code></p></td>
<td><p>Extracts information from cookies declared in the cookie request header</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">@FormParam</code></p></td>
<td><p>Extracts information from a request representation whose content type is <code dir="ltr">application/x-www-form-urlencoded</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@HeaderParam</code></p></td>
<td><p>Extracts the value of a header</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">@MatrixParam</code></p></td>
<td><p>Extracts the value of a URI matrix parameter</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@PathParam</code></p></td>
<td><p>Extracts the value of a URI template parameter</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">@QueryParam</code></p></td>
<td><p>Extracts the value of a URI query parameter</p></td>
</tr>
</tbody>
</table>

  

## 31.1.1 Extracting Path Parameters

URI path templates are URIs with variables embedded within the URI
syntax. The `@PathParam` annotation lets you use variable URI path
fragments when you call a method.

The following code snippet shows how to extract the last name of an
employee when the employee's email address is provided:

``` oac_no_warn
@Path("/employees/{firstname}.{lastname}@{domain}.com")
public class EmpResource {

    @GET
    @Produces("text/xml")
    public String getEmployeelastname(@PathParam("lastname") String lastName) {
      ...
    }
}
```

In this example, the `@Path` annotation defines the URI variables (or
path parameters) `{firstname}`, `{lastname}`, and `{domain}`. The
`@PathParam` in the method parameter of the request method extracts the
last name from the email address.

If your HTTP request is `GET` `/employees/john.doe@example.com`, the
value "`doe`" is injected into `{lastname}`.

You can specify several path parameters in one URI.

You can declare a regular expression with a URI variable. For example,
if it is required that the last name must consist only of lowercase and
uppercase characters, you can declare the following regular expression:

``` oac_no_warn
@Path("/employees/{firstname}.{lastname[a-zA-Z]*}@{domain}.com")
```

If the last name does not match the regular expression, a 404 response
is returned.

## 31.1.2 Extracting Query Parameters

Use the `@QueryParam` annotation to extract query parameters from the
query component of the request URI.

For instance, to query all employees who have joined within a specific
range of years, use a method signature like the following:

``` oac_no_warn
@Path("/employees/")
@GET
public Response getEmployees(
        @DefaultValue("2003") @QueryParam("minyear") int minyear,
        @DefaultValue("2013") @QueryParam("maxyear") int maxyear)
    {...}
```

This code snippet defines two query parameters, `minyear` and `maxyear`.
The following HTTP request would query for all employees who have joined
between 2003 and 2013:

``` oac_no_warn
GET /employees?maxyear=2013&minyear=2003
```

The `@DefaultValue` annotation defines a default value, which is to be
used if no values are provided for the query parameters. By default,
JAX-RS assigns a null value for `Object` values and zero for primitive
data types. You can use the `@DefaultValue` annotation to eliminate null
or zero values and define your own default values for a parameter.

## 31.1.3 Extracting Form Data

Use the `@FormParam` annotation to extract form parameters from HTML
forms. For example, the following form accepts the name, address, and
manager's name of an employee:

``` oac_no_warn
<FORM action="http://example.com/employees/" method="post">
  <p>
    <fieldset>
      Employee name: <INPUT type="text" name="empname" tabindex="1">  
      Employee address: <INPUT type="text" name="empaddress" tabindex="2"> 
      Manager name: <INPUT type="text" name="managername" tabindex="3"> 
    </fieldset>
  </p>
</FORM>
```

Use the following code snippet to extract the manager name from this
HTML form:

``` oac_no_warn
@POST
@Consumes("application/x-www-form-urlencoded")
public void post(@FormParam("managername") String managername) {
    // Store the value
    ...
}
```

To obtain a map of form parameter names to values, use a code snippet
like the following:

``` oac_no_warn
@POST
@Consumes("application/x-www-form-urlencoded")
public void post(MultivaluedMap<String, String> formParams) {
    // Store the message
}
```

## 31.1.4 Extracting the Java Type of a Request or Response

The `javax.ws.rs.core.Context` annotation retrieves the Java types
related to a request or response.

The `javax.ws.rs.core.UriInfo` interface provides information about the
components of a request URI. The following code snippet shows how to
obtain a map of query and path parameter names to values:

``` oac_no_warn
@GET
public String getParams(@Context UriInfo ui) {
    MultivaluedMap<String, String> queryParams = ui.getQueryParameters();
    MultivaluedMap<String, String> pathParams = ui.getPathParameters();
}
```

The `javax.ws.rs.core.HttpHeaders` interface provides information about
request headers and cookies. The following code snippet shows how to
obtain a map of header and cookie parameter names to values:

``` oac_no_warn
@GET
public String getHeaders(@Context HttpHeaders hh) {
    MultivaluedMap<String, String> headerParams = hh.getRequestHeaders();
    MultivaluedMap<String, Cookie> pathParams = hh.getCookies();
}
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
<td><a href="jaxrs-advanced.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
