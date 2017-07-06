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
<td><a href="jaxrs-client.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-client002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 30.1 Overview of the Client API

The JAX-RS Client API provides a high-level API for accessing any REST
resources, not just JAX-RS services. The Client API is defined in the
`javax.ws.rs.client` package.

The following topics are addressed here:

  - [Section 30.1.1, "Creating a Basic Client Request Using the Client
    API"](#CHDFCABB)

  - [Section 30.1.2, "Obtaining the Client Instance"](#CHDHBFHJ)

  - [Section 30.1.3, "Setting the Client Target"](#CHDDCICC)

  - [Section 30.1.4, "Setting Path Parameters in Targets"](#CHDDBFCG)

  - [Section 30.1.5, "Invoking the Request"](#CHDEFCDB)

## 30.1.1 Creating a Basic Client Request Using the Client API

The following steps are needed to access a REST resource using the
Client API.

1.  Obtain an instance of the `javax.ws.rs.client.Client` interface.

2.  Configure the `Client` instance with a target.

3.  Create a request based on the target.

4.  Invoke the request.

The Client API is designed to be fluent, with method invocations chained
together to configure and submit a request to a REST resource in only a
few lines of code.

``` oac_no_warn
Client client = ClientBuilder.newClient();
String name = client.target("http://example.com/webapi/hello")
        .request(MediaType.TEXT_PLAIN)
        .get(String.class);
```

In this example, the client instance is first created by calling the
`javax.ws.rs.client.ClientBuilder.newClient` method. Then, the request
is configured and invoked by chaining method calls together in one line
of code. The `Client.target` method sets the target based on a URI. The
`javax.ws.rs.client.WebTarget.request` method sets the media type for
the returned entity. The `javax.ws.rs.client.Invocation.Builder.get`
method invokes the service using an HTTP `GET` request, setting the type
of the returned entity to `String`.

## 30.1.2 Obtaining the Client Instance

The `Client` interface defines the actions and infrastructure a REST
client requires to consume a RESTful web service. Instances of `Client`
are obtained by calling the `ClientBuilder.newClient` method.

``` oac_no_warn
Client client = ClientBuilder.newClient();
```

Use the `close` method to close `Client` instances after all the
invocations for the target resource have been performed:

``` oac_no_warn
Client client = ClientBuilder.newClient();
...
client.close();
```

`Client` instances are heavyweight objects. For performance reasons,
limit the number of `Client` instances in your application, as the
initialization and destruction of these instances may be expensive in
your runtime environment.

## 30.1.3 Setting the Client Target

The target of a client, the REST resource at a particular URI, is
represented by an instance of the `javax.ws.rs.client.WebTarget`
interface. You obtain a `WebTarget` instance by calling the
`Client.target` method and passing in the URI of the target REST
resource.

``` oac_no_warn
Client client = ClientBuilder.newClient();
WebTarget myResource = client.target("http://example.com/webapi");
```

For complex REST resources, it may be beneficial to create several
instances of `WebTarget`. In the following example, a base target is
used to construct several other targets that represent different
services provided by a REST resource.

``` oac_no_warn
Client client = ClientBuilder.newClient();
WebTarget base = client.target("http://example.com/webapi");
// WebTarget at http://example.com/webapi/read
WebTarget read = base.path("read");
// WebTarget at http://example.com/webapi/write
WebTarget write = base.path("write");
```

The `WebTarget.path` method creates a new `WebTarget` instance by
appending the current target URI with the path that was passed in.

## 30.1.4 Setting Path Parameters in Targets

Path parameters in client requests can be specified as URI template
parameters, similar to the template parameters used when defining a
resource URI in a JAX-RS service. Template parameters are specified by
surrounding the template variable with braces (`{}`). Call the
`resolveTemplate` method to substitute the `{username}`, and then call
the `queryParam` method to add another variable to pass.

``` oac_no_warn
WebTarget myResource = client.target("http://example.com/webapi/read")
        .path("{userName}")
        .resolveTemplate("userName", "janedoe")        .queryParam("chapter", "1");// http://example.com/webapi/read/janedoe?chapter=1Response response = myResource.request(...)        .get();
```

## 30.1.5 Invoking the Request

After setting and applying any configuration options to the target, call
one of the `WebTarget.request` methods to begin creating the request.
This is usually accomplished by passing to `WebTarget.request` the
accepted media response type for the request either as a string of the
MIME type or using one of the constants in `javax.ws.rs.core.MediaType`.
The `WebTarget.request` method returns an instance of
`javax.ws.rs.client.Invocation.Builder`, a helper object that provides
methods for preparing the client request.

``` oac_no_warn
Client client = ClientBuilder.newClient();
WebTarget myResource = client.target("http://example.com/webapi/read");
Invocation.Builder builder = myResource.request(MediaType.TEXT_PLAIN);
```

Using a `MediaType` constant is equivalent to using the string defining
the MIME type.

``` oac_no_warn
Invocation.Builder builder = myResource.request("text/plain");
```

After setting the media type, invoke the request by calling one of the
methods of the `Invocation.Builder` instance that corresponds to the
type of HTTP request the target REST resource expects. These methods
are:

  - `get()`

  - `post()`

  - `delete()`

  - `put()`

  - `head()`

  - `options()`

For example, if the target REST resource is for an HTTP GET request,
call the `Invocation.Builder.get` method. The return type should
correspond to the entity returned by the target REST resource.

``` oac_no_warn
Client client = ClientBuilder.newClient();
WebTarget myResource = client.target("http://example.com/webapi/read");
String response = myResource.request(MediaType.TEXT_PLAIN)
        .get(String.class);
```

If the target REST resource is expecting an HTTP POST request, call the
`Invocation.Builder.post` method.

``` oac_no_warn
Client client = ClientBuilder.newClient();
StoreOrder order = new StoreOrder(...);
WebTarget myResource = client.target("http://example.com/webapi/write");
TrackingNumber trackingNumber = myResource.request(MediaType.APPLICATION_XML)
                                   .post(Entity.xml(order), TrackingNumber.class);
```

In the preceding example, the return type is a custom class and is
retrieved by setting the type in the `Invocation.Builder.post(Entity<?>
entity, Class<T> responseType)` method as a parameter.

If the return type is a collection, use
`javax.ws.rs.core.GenericType<T>` as the response type parameter, where
`T` is the collection
type:

``` oac_no_warn
List<StoreOrder> orders = client.target("http://example.com/webapi/read")
        .path("allOrders")
        .request(MediaType.APPLICATION_XML)
        .get(new GenericType<List<StoreOrder>>() {});
```

This preceding example shows how methods are chained together in the
Client API to simplify how requests are configured and invoked.

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
<td><a href="jaxrs-client.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-client002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
