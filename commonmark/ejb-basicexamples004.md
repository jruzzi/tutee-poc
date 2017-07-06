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
<td><a href="ejb-basicexamples003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-basicexamples005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 34.4 A Web Service Example: helloservice

This example demonstrates a simple web service that generates a response
based on information received from the client. `HelloServiceBean` is a
stateless session bean that implements a single method: `sayHello`. This
method matches the `sayHello` method invoked by the client described in
[A Simple JAX-WS Application Client](jaxws002.htm#BNAYX).

The following topics are addressed here:

  - [Section 34.4.1, "The Web Service Endpoint Implementation
    Class"](#BNBOS)

  - [Section 34.4.2, "Stateless Session Bean Implementation
    Class"](#BNBOT)

  - [Section 34.4.3, "Running the helloservice Example"](#BNBOU)

## 34.4.1 The Web Service Endpoint Implementation Class

`HelloServiceBean` is the endpoint implementation class, typically the
primary programming artifact for enterprise bean web service endpoints.
The web service endpoint implementation class has the following
requirements.

  - The class must be annotated with either the `javax.jws.WebService`
    or the `javax.jws.WebServiceProvider` annotation.

  - The implementing class may explicitly reference an SEI through the
    `endpointInterface` element of the `@WebService` annotation but is
    not required to do so. If no `endpointInterface` is specified in
    `@WebService`, an SEI is implicitly defined for the implementing
    class.

  - The business methods of the implementing class must be public and
    must not be declared `static` or `final`.

  - Business methods that are exposed to web service clients must be
    annotated with `javax.jws.WebMethod`.

  - Business methods that are exposed to web service clients must have
    JAXB-compatible parameters and return types. See the list of JAXB
    default data type bindings at [Types Supported by
    JAX-WS](jaxws003.htm#BNAZC).

  - The implementing class must not be declared `final` and must not be
    `abstract`.

  - The implementing class must have a default public constructor.

  - The endpoint class must be annotated `@Stateless`.

  - The implementing class must not define the `finalize` method.

  - The implementing class may use the `javax.annotation.PostConstruct`
    or `javax.annotation.PreDestroy` annotations on its methods for
    lifecycle event callbacks.
    
    The `@PostConstruct` method is called by the container before the
    implementing class begins responding to web service clients.
    
    The `@PreDestroy` method is called by the container before the
    endpoint is removed from operation.

## 34.4.2 Stateless Session Bean Implementation Class

The `HelloServiceBean` class implements the `sayHello` method, which is
annotated `@WebMethod`. The source code for the `HelloServiceBean` class
is as follows:

``` oac_no_warn
package javaeetutorial.helloservice.ejb;

import javax.ejb.Stateless;
import javax.jws.WebMethod;
import javax.jws.WebService;

@Stateless
@WebService
public class HelloServiceBean {
    private final String message = "Hello, ";

    public void HelloServiceBean() {}

    @WebMethod
    public String sayHello(String name) {
        return message + name + ".";
    }
}
```

## 34.4.3 Running the helloservice Example

You can use either NetBeans IDE or Maven to build, package, and deploy
the `helloservice` example. You can then use the Administration Console
to test the web service endpoint methods.

The following topics are addressed here:

  - [Section 34.4.3.1, "To Build, Package, and Deploy the helloservice
    Example Using NetBeans IDE"](#BNBOV)

  - [Section 34.4.3.2, "To Build, Package, and Deploy the helloservice
    Example Using Maven"](#BNBOW)

  - [Section 34.4.3.3, "To Test the Service without a
Client"](#BNBOX)

### 34.4.3.1 To Build, Package, and Deploy the helloservice Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/ejb
    ```

4.  Select the `helloservice` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `helloservice` project and
    select Build.
    
    This builds and packages the application into `helloservice.ear`,
    located in tut-install`/examples/ejb/helloservice/target/`, and
    deploys this EAR file to GlassFish
Server.

### 34.4.3.2 To Build, Package, and Deploy the helloservice Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/ejb/helloservice/
    ```

3.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This compiles the source files and packages the application into an
    EJB JAR file located at
    tut-install`/examples/ejb/helloservice/target/helloservice.jar`.
    Then the EJB JAR file is deployed to GlassFish Server.
    
    Upon deployment, GlassFish Server generates additional artifacts
    required for web service invocation, including the WSDL file.

### 34.4.3.3 To Test the Service without a Client

The GlassFish Server Administration Console allows you to test the
methods of a web service endpoint. To test the `sayHello` method of
`HelloServiceBean`, follow these steps.

1.  Open the Administration Console by opening the following URL in a
    web browser:
    
    ``` oac_no_warn
    http://localhost:4848/
    ```

2.  In the navigation tree, select the Applications node.

3.  In the Applications table, click the `helloservice` link.

4.  In the Modules and Components table, click the View Endpoint link.

5.  On the Web Service Endpoint Information page, click the Tester link:
    
    ``` oac_no_warn
    /HelloServiceBeanService/HelloServiceBean?Tester
    ```

6.  On the Web Service Test Links page, click the non-secure link (the
    one that specifies port 8080).

7.  On the HelloServiceBeanService Web Service Tester page, under
    Methods, enter a name as the parameter to the `sayHello` method.

8.  Click sayHello.
    
    The sayHello Method invocation page opens. Under Method returned,
    you'll see the response from the endpoint.

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
<td><a href="ejb-basicexamples003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-basicexamples005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
