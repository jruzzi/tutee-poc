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
<td><a href="jaxrs-client002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 30.3 Advanced Features of the Client API

This section describes some of the advanced features of the JAX-RS
Client API.

The following topics are addressed here:

  - [Section 30.3.1, "Configuring the Client Request"](#CHDGBBCC)

  - [Section 30.3.2, "Asynchronous Invocations in the Client
    API"](#CHDEBIGG)

## 30.3.1 Configuring the Client Request

Additional configuration options may be added to the client request
after it is created but before it is invoked.

The following topics are addressed here:

  - [Section 30.3.1.1, "Setting Message Headers in the Client
    Request"](#CHDHAFBG)

  - [Section 30.3.1.2, "Setting Cookies in the Client
    Request"](#CHDHFFDJ)

  - [Section 30.3.1.3, "Adding Filters to the Client"](#CHDJEFID)

### 30.3.1.1 Setting Message Headers in the Client Request

You can set HTTP headers on the request by calling the
`Invocation.Builder.header` method.

``` oac_no_warn
Client client = ClientBuilder.newClient();
WebTarget myResource = client.target("http://example.com/webapi/read");
String response = myResource.request(MediaType.TEXT_PLAIN)
        .header("myHeader", "The header value")
        .get(String.class);
```

If you need to set multiple headers on the request, call the
`Invocation.Builder.headers` method and pass in a
`javax.ws.rs.core.MultivaluedMap` instance with the name-value pairs of
the HTTP headers. Calling the `headers` method replaces all the existing
headers with the headers supplied in the `MultivaluedMap` instance.

``` oac_no_warn
Client client = ClientBuilder.newClient();
WebTarget myResource = client.target("http://example.com/webapi/read");
MultivaluedMap<String, Object> myHeaders = 
    new MultivaluedMap<>("myHeader", "The header value");
myHeaders.add(...);
String response = myResource.request(MediaType.TEXT_PLAIN)
        .headers(myHeaders)
        .get(String.class);
```

The `MultivaluedMap` interface allows you to specify multiple values for
a given key.

``` oac_no_warn
MultivaluedMap<String, Object> myHeaders = 
    new MultivaluedMap<String, Object>();
List<String> values = new ArrayList<>();
values.add(...)
myHeaders.add("myHeader", values
```

### 30.3.1.2 Setting Cookies in the Client Request

You can add HTTP cookies to the request by calling the
`Invocation.Builder.cookie` method, which takes a name-value pair as
parameters.

``` oac_no_warn
Client client = ClientBuilder.newClient();
WebTarget myResource = client.target("http://example.com/webapi/read");
String response = myResource.request(MediaType.TEXT_PLAIN)
        .cookie("myCookie", "The cookie value")
        .get(String.class);
```

The `javax.ws.rs.core.Cookie` class encapsulates the attributes of an
HTTP cookie, including the name, value, path, domain, and RFC
specification version of the cookie. In the following example, the
`Cookie` object is configured with a name-value pair, a path, and a
domain.

``` oac_no_warn
Client client = ClientBuilder.newClient();
WebTarget myResource = client.target("http://example.com/webapi/read");
Cookie myCookie = new Cookie("myCookie", "The cookie value", 
    "/webapi/read", "example.com"); 
String response = myResource.request(MediaType.TEXT_PLAIN)
        .cookie(myCookie)
        .get(String.class);
```

### 30.3.1.3 Adding Filters to the Client

You can register custom filters with the client request or the response
received from the target resource. To register filter classes when the
`Client` instance is created, call the `Client.register`
method.

``` oac_no_warn
Client client = ClientBuilder.newClient().register(MyLoggingFilter.class);
```

In the preceding example, all invocations that use this `Client`
instance have the `MyLoggingFilter` filter registered with them.

You can also register the filter classes on the target by calling
`WebTarget.register`.

``` oac_no_warn
Client client = ClientBuilder.newClient().register(MyLoggingFilter.class);
WebTarget target = client.target("http://example.com/webapi/secure")
        .register(MyAuthenticationFilter.class);
```

In the preceding example, both the `MyLoggingFilter` and
`MyAuthenticationFilter` filters are attached to the invocation.

Request and response filter classes implement the
`javax.ws.rs.client.ClientRequestFilter` and
`javax.ws.rs.client.ClientResponseFilter` interfaces, respectively. Both
of these interfaces define a single method, `filter`. All filters must
be annotated with `javax.ws.rs.ext.Provider`.

The following class is a logging filter for both client requests and
client responses.

``` oac_no_warn
@Provider
public class MyLoggingFilter implements ClientRequestFilter, 
        ClientResponseFilter {
    static final Logger logger = Logger.getLogger(...);

    // implement the ClientRequestFilter.filter method
    @Override
    public void filter(ClientRequestContext requestContext) 
            throws IOException {
        logger.log(...);
        ...
    }

    // implement the ClientResponseFilter.filter method
    @Override
    public void filter(ClientRequestContext requestContext, 
           ClientResponseContext responseContext) throws IOException {
        logger.log(...);
        ...
    }
}
```

If the invocation must be stopped while the filter is active, call the
context object's `abortWith` method, and pass in a
`javax.ws.rs.core.Response` instance from within the filter.

``` oac_no_warn
@Override
public void filter(ClientRequestContext requestContext) throws IOException {
    ...
    Response response = new Response();
    response.status(500);
    requestContext.abortWith(response);
}
```

## 30.3.2 Asynchronous Invocations in the Client API

In networked applications, network issues can affect the perceived
performance of the application, particularly in long-running or
complicated network calls. Asynchronous processing helps prevent
blocking and makes better use of an application's resources.

In the JAX-RS Client API, the `Invocation.Builder.async` method is used
when constructing a client request to indicate that the call to the
service should be performed asynchronously. An asynchronous invocation
returns control to the caller immediately, with a return type of
[`java.util.concurrent.Future<T>`](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/Future.html?is-external=true)
(part of the Java SE concurrency API) and with the type set to the
return type of the service call. `Future<T>` objects have methods to
check if the asynchronous call has been completed, to retrieve the final
result, to cancel the invocation, and to check if the invocation has
been cancelled.

The following example shows how to invoke an asynchronous request on a
resource.

``` oac_no_warn
Client client = ClientBuilder.newClient();
WebTarget myResource = client.target("http://example.com/webapi/read");
Future<String> response = myResource.request(MediaType.TEXT_PLAIN)
        .async()
        .get(String.class);
```

### 30.3.2.1 Using Custom Callbacks in Asynchronous Invocations

The `InvocationCallback` interface defines two methods, `completed` and
`failed`, that are called when an asynchronous invocation either
completes successfully or fails, respectively. You may register an
`InvocationCallback` instance on your request by creating a new instance
when specifying the request method.

The following example shows how to register a callback object on an
asynchronous invocation.

``` oac_no_warn
Client client = ClientBuilder.newClient();
WebTarget myResource = client.target("http://example.com/webapi/read");
Future<Customer> fCustomer = myResource.request(MediaType.TEXT_PLAIN)
        .async()
        .get(new InvocationCallback<Customer>() {
            @Override
            public void completed(Customer customer) {
            // Do something with the customer object
            }
            @Override
             public void failed(Throwable throwable) {
            // handle the error
            }
    });
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
<td><a href="jaxrs-client002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs-advanced.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
