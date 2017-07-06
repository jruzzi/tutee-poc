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
<td><a href="jaxrs-advanced002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 31.3 Subresources and Runtime Resource Resolution

You can use a resource class to process only a part of the URI request.
A root resource can then implement subresources that can process the
remainder of the URI path.

A resource class method that is annotated with `@Path` is either a
subresource method or a subresource locator.

  - A subresource method is used to handle requests on a subresource of
    the corresponding resource.

  - A subresource locator is used to locate subresources of the
    corresponding resource.

The following topics are addressed here:

  - [Section 31.3.1, "Subresource Methods"](#GKLAG)

  - [Section 31.3.2, "Subresource Locators"](#GKRHR)

## 31.3.1 Subresource Methods

A subresource method handles an HTTP request directly. The method must
be annotated with a request method designator, such as `@GET` or
`@POST`, in addition to `@Path`. The method is invoked for request URIs
that match a URI template created by concatenating the URI template of
the resource class with the URI template of the method.

The following code snippet shows how a subresource method can be used to
extract the last name of an employee when the employee's email address
is provided:

``` oac_no_warn
@Path("/employeeinfo")
public class EmployeeInfo {

    public employeeinfo() {}

    @GET
    @Path("/employees/{firstname}.{lastname}@{domain}.com")
    @Produces("text/xml")
    public String getEmployeeLastName(@PathParam("lastname") String lastName) {
       ...
    }
}
```

The `getEmployeeLastName` method returns `doe` for the following `GET`
request:

``` oac_no_warn
GET /employeeinfo/employees/john.doe@example.com
```

## 31.3.2 Subresource Locators

A subresource locator returns an object that will handle an HTTP
request. The method must not be annotated with a request method
designator. You must declare a subresource locator within a subresource
class, and only subresource locators are used for runtime resource
resolution.

The following code snippet shows a subresource locator:

``` oac_no_warn
// Root resource class
@Path("/employeeinfo")
public class EmployeeInfo {

    // Subresource locator: obtains the subresource Employee
    // from the path /employeeinfo/employees/{empid}
    @Path("/employees/{empid}")
    public Employee getEmployee(@PathParam("empid") String id) {
        // Find the Employee based on the id path parameter
        Employee emp = ...;
        ...
        return emp;
    }
}

// Subresource class
public class Employee {

    // Subresource method: returns the employee's last name
    @GET
    @Path("/lastname")
    public String getEmployeeLastName() {
        ...
        return lastName;
    }
}
```

In this code snippet, the `getEmployee` method is the subresource
locator that provides the `Employee` object, which services requests for
`lastname`.

If your HTTP request is `GET /employeeinfo/employees/as209/`, the
`getEmployee` method returns an `Employee` object whose id is `as209`.
At runtime, JAX-RS sends a `GET /employeeinfo/employees/as209/lastname`
request to the `getEmployeeLastName` method. The `getEmployeeLastName`
method retrieves and returns the last name of the employee whose id is
`as209`.

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
<td><a href="jaxrs-advanced002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
