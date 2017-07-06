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
<td><a href="webapp004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="webapp006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 6.5 Configuring Web Applications

This section describes the following tasks involved with configuring web
applications:

  - Setting context parameters

  - Declaring welcome files

  - Mapping errors to error screens

  - Declaring resource references

## 6.5.1 Setting Context Parameters

The web components in a web module share an object that represents their
application context. You can pass context parameters to the context, or
you can pass initialization parameters to a servlet. Context parameters
are available to the entire application. For information on
initialization parameters, see [Creating and Initializing a
Servlet](servlets004.htm#BNAFU).

### 6.5.1.1 To Add a Context Parameter Using NetBeans IDE

These steps apply generally to web applications but do not apply
specifically to the examples in this chapter.

To add a context parameter using NetBeans IDE:

1.  Open the project.

2.  Expand the project's node in the Projects tree.

3.  Expand the Web Pages node and then the WEB-INF node.

4.  Double-click `web.xml`.
    
    If the project does not have a `web.xml` file, create one by
    following the steps in [To Create a web.xml File Using NetBeans
    IDE](#GKIHH).

5.  Click General at the top of the editor window.

6.  Expand the Context Parameters node.

7.  Click Add.

8.  In the Add Context Parameter dialog box, in the Parameter Name
    field, enter the name that specifies the context object.

9.  In the Parameter Value field, enter the parameter to pass to the
    context object.

10. Click OK.

### 6.5.1.2 To Create a web.xml File Using NetBeans IDE

To create a `web.xml` file using NetBeans IDE:

1.  From the File menu, choose New File.

2.  In the New File wizard, select the Web category, then select
    Standard Deployment Descriptor under File Types.

3.  Click Next.

4.  Click Finish.
    
    A basic `web.xml` file appears in `web/WEB-INF/`.

## 6.5.2 Declaring Welcome Files

The welcome files mechanism allows you to specify a list of files that
the web container can append to a request for a URL (called a valid
partial request) that is not mapped to a web component. For example,
suppose that you define a welcome file `welcome.html`. When a client
requests a URL such as host`:`port`/`webapp`/`directory, where directory
is not mapped to a servlet or XHTML page, the file
host`:`port`/`webapp`/`directory`/welcome.html` is returned to the
client.

If a web container receives a valid partial request, the web container
examines the welcome file list, appends to the partial request each
welcome file in the order specified, and checks whether a static
resource or servlet in the WAR is mapped to that request URL. The web
container then sends the request to the first resource that matches in
the WAR.

If no welcome file is specified, GlassFish Server will use a file named
`index.html` as the default welcome file. If there is no welcome file
and no file named `index.html`, GlassFish Server returns a directory
listing.

You specify welcome files in the `web.xml` file. The welcome file
specification for the `hello1` example looks like this:

``` oac_no_warn
<welcome-file-list>
    <welcome-file>index.xhtml</welcome-file>
</welcome-file-list>
```

A specified welcome file must not have a leading or trailing slash
(`/`).

The `hello2` example does not specify a welcome file, because the URL
request is mapped to the `GreetingServlet` web component through the URL
pattern `/greeting`.

## 6.5.3 Mapping Errors to Error Screens

When an error occurs during execution of a web application, you can have
the application display a specific error screen according to the type of
error. In particular, you can specify a mapping between the status code
returned in an HTTP response or a Java programming language exception
returned by any web component and any type of error screen.

You can have multiple `error-page` elements in your deployment
descriptor. Each element identifies a different error that causes an
error page to open. This error page can be the same for any number of
`error-page` elements.

### 6.5.3.1 To Set Up Error Mapping Using NetBeans IDE

These steps apply generally to web applications but do not apply
specifically to the examples in this chapter.

To set up error mapping using NetBeans IDE:

1.  Open the project.

2.  Expand the project's node in the Projects tab.

3.  Expand the Web Pages node and then the WEB-INF node.

4.  Double-click `web.xml`.
    
    If the project does not have a `web.xml` file, create one by
    following the steps in [To Create a web.xml File Using NetBeans
    IDE](#GKIHH).

5.  Click Pages at the top of the editor window.

6.  Expand the Error Pages node.

7.  Click Add.

8.  In the Add Error Page dialog box, click Browse to locate the page
    that you want to act as the error page.

9.  Specify either an error code or an exception type.
    
      - To specify an error code, in the Error Code field enter the HTTP
        status code that will cause the error page to be opened, or
        leave the field blank to include all error codes.
    
      - To specify an exception type, in the Exception Type field enter
        the exception that will cause the error page to load. To specify
        all throwable errors and exceptions, enter
        `java.lang.Throwable`.

10. Click OK.

## 6.5.4 Declaring Resource References

If your web component uses such objects as enterprise beans, data
sources, or web services, you use Java EE annotations to inject these
resources into your application. Annotations eliminate a lot of the
boilerplate lookup code and configuration elements that previous
versions of Java EE required.

Although resource injection using annotations can be more convenient for
the developer, there are some restrictions on using it in web
applications. First, you can inject resources only into
container-managed objects, because a container must have control over
the creation of a component so that it can perform the injection into a
component. As a result, you cannot inject resources into such objects as
simple JavaBeans components. However, managed beans are managed by the
container; therefore, they can accept resource injections.

Components that can accept resource injections are listed in [Table
6-1](#BNAEV).

This section explains how to use a couple of the annotations supported
by a web container to inject resources. [Chapter 38, "Running the
Persistence Examples"](persistence-basicexamples.htm#GIJST), explains
how web applications use annotations supported by the Java Persistence
API. [Chapter 48, "Getting Started Securing Web
Applications"](security-webtier.htm#BNCAS), explains how to use
annotations to specify information about securing web applications. See
[Chapter 52, "Resource Adapters and Contracts"](resources.htm#BNCJH),
for more information on resources.

Table 6-1 Web Components That Accept Resource Injections

<table style="width:23%;">
<colgroup>
<col width="23%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>Interface/Class</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servlets</p></td>
<td><p><code dir="ltr">javax.servlet.Servlet</code></p></td>
</tr>
<tr class="even">
<td><p>Servlet filters</p></td>
<td><p><code dir="ltr">javax.servlet.ServletFilter</code></p></td>
</tr>
<tr class="odd">
<td><p>Event listeners</p></td>
<td><p><code dir="ltr">javax.servlet.ServletContextListener</code></p>
<p><code dir="ltr">javax.servlet.ServletContextAttributeListener</code></p>
<p><code dir="ltr">javax.servlet.ServletRequestListener</code></p>
<p><code dir="ltr">javax.servlet.ServletRequestAttributeListener</code></p>
<p><code dir="ltr">javax.servlet.http.HttpSessionListener</code></p>
<p><code dir="ltr">javax.servlet.http.HttpSessionAttributeListener</code></p>
<p><code dir="ltr">javax.servlet.http.HttpSessionBindingListener</code></p></td>
</tr>
<tr class="even">
<td><p>Managed beans</p></td>
<td><p>Plain Old Java Objects</p></td>
</tr>
</tbody>
</table>

  

### 6.5.4.1 Declaring a Reference to a Resource

The `@Resource` annotation is used to declare a reference to a resource,
such as a data source, an enterprise bean, or an environment entry.

The `@Resource` annotation is specified on a class, a method, or a
field. The container is responsible for injecting references to
resources declared by the `@Resource` annotation and mapping it to the
proper JNDI resources.

In the following example, the `@Resource` annotation is used to inject a
data source into a component that needs to make a connection to the data
source, as is done when using JDBC technology to access a relational
database:

``` oac_no_warn
@Resource javax.sql.DataSource catalogDS;
public getProductsByCategory() {
    // get a connection and execute the query
    Connection conn = catalogDS.getConnection();
    ...
}
```

The container injects this data source prior to the component's being
made available to the application. The data source JNDI mapping is
inferred from the field name, `catalogDS`, and the type,
`javax.sql.DataSource`.

If you have multiple resources that you need to inject into one
component, you need to use the `@Resources` annotation to contain them,
as shown by the following example:

``` oac_no_warn
@Resources ({
    @Resource(name="myDB" type=javax.sql.DataSource.class),
    @Resource(name="myMQ" type=javax.jms.ConnectionFactory.class)
})
```

The web application examples in this tutorial use the Java Persistence
API to access relational databases. This API does not require you to
explicitly create a connection to a data source. Therefore, the examples
do not use the `@Resource` annotation to inject a data source. However,
this API supports the `@PersistenceUnit` and `@PersistenceContext`
annotations for injecting `EntityManagerFactory` and `EntityManager`
instances, respectively. [Chapter 38, "Running the Persistence
Examples"](persistence-basicexamples.htm#GIJST) describes these
annotations and the use of the Java Persistence API in web applications.

### 6.5.4.2 Declaring a Reference to a Web Service

The `@WebServiceRef` annotation provides a reference to a web service.
The following example shows uses the `@WebServiceRef` annotation to
declare a reference to a web service. `WebServiceRef` uses the
`wsdlLocation` element to specify the URI of the deployed service's WSDL
file:

``` oac_no_warn
...
import javax.xml.ws.WebServiceRef;
...
public class ResponseServlet extends HTTPServlet {
@WebServiceRef(wsdlLocation="http://localhost:8080/helloservice/hello?wsdl")
static HelloService service;
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
<td><a href="webapp004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="webapp006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
