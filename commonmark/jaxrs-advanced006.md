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
<td><a href="jaxrs-advanced005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 31.6 Runtime Content Negotiation

The `@Produces` and `@Consumes` annotations handle static content
negotiation in JAX-RS. These annotations specify the content preferences
of the server. HTTP headers such as `Accept`, `Content-Type`, and
`Accept-Language` define the content negotiation preferences of the
client.

For more details on the HTTP headers for content negotiation, see HTTP
/1.1 - Content Negotiation
(`http://www.w3.org/Protocols/rfc2616/rfc2616-sec12.html`).

The following code snippet shows the server content preferences:

``` oac_no_warn
@Produces("text/plain")
@Path("/employee")
public class Employee {

    @GET
    public String getEmployeeAddressText(String address) {...}

    @Produces("text/xml")
    @GET
    public String getEmployeeAddressXml(Address address) {...}
}
```

The `getEmployeeAddressText` method is called for an HTTP request that
looks like the following:

``` oac_no_warn
GET /employee
Accept: text/plain
```

This will produce the following response:

``` oac_no_warn
500 Oracle Parkway, Redwood Shores, CA
```

The `getEmployeeAddressXml` method is called for an HTTP request that
looks like the following:

``` oac_no_warn
GET /employee
Accept: text/xml
```

This will produce the following response:

``` oac_no_warn
<address street="500 Oracle Parkway, Redwood Shores, CA" country="USA"/>
```

With static content negotiation, you can also define multiple content
and media types for the client and server.

``` oac_no_warn
@Produces("text/plain", "text/xml")
```

In addition to supporting static content negotiation, JAX-RS also
supports runtime content negotiation using the
`javax.ws.rs.core.Variant` class and `Request` objects. The `Variant`
class specifies the resource representation of content negotiation. Each
instance of the `Variant` class may contain a media type, a language,
and an encoding. The `Variant` object defines the resource
representation that is supported by the server. The
`Variant.VariantListBuilder` class is used to build a list of
representation variants.

The following code snippet shows how to create a list of resource
representation
variants:

``` oac_no_warn
List<Variant> vs = Variant.mediatypes("application/xml", "application/json")
        .languages("en", "fr").build();
```

This code snippet calls the `build` method of the `VariantListBuilder`
class. The `VariantListBuilder` class is invoked when you call the
`mediatypes`, `languages`, or `encodings` methods. The `build` method
builds a series of resource representations. The `Variant` list created
by the `build` method has all possible combinations of items specified
in the `mediatypes`, `languages`, and `encodings` methods.

In this example, the size of the `vs` object as defined in this code
snippet is 4, and the contents are as follows:

``` oac_no_warn
[["application/xml","en"], ["application/json","en"],
    ["application/xml","fr"],["application/json","fr"]]
```

The `javax.ws.rs.core.Request.selectVariant` method accepts a list of
`Variant` objects and chooses the `Variant` object that matches the HTTP
request. This method compares its list of `Variant` objects with the
`Accept`, `Accept-Encoding`, `Accept-Language`, and `Accept-Charset`
headers of the HTTP request.

The following code snippet shows how to use the `selectVariant` method
to select the most acceptable `Variant` from the values in the client
request:

``` oac_no_warn
@GET
public Response get(@Context Request r) { 
    List<Variant> vs = ...;
    Variant v = r.selectVariant(vs);
    if (v == null) {
        return Response.notAcceptable(vs).build();
    } else {
        Object rep = selectRepresentation(v);
        return Response.ok(rep, v);
    }
}
```

The `selectVariant` method returns the `Variant` object that matches the
request or null if no matches are found. In this code snippet, if the
method returns null, a `Response` object for a nonacceptable response is
built. Otherwise, a `Response` object with an OK status and containing a
representation in the form of an `Object` entity and a `Variant` is
returned.

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
<td><a href="jaxrs-advanced005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
