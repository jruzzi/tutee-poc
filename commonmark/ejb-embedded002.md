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
<td><a href="ejb-embedded001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-embedded003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 35.2 Developing Embeddable Enterprise Bean Applications

All embeddable enterprise bean containers support the features listed in
[Table 35-1](#GKCQC).

Table 35-1 Required Enterprise Bean Features in the Embeddable Container

<table style="width:32%;">
<colgroup>
<col width="32%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Enterprise Bean Feature</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Local session beans</p></td>
<td><p>Local and no-interface view stateless, stateful, and singleton session beans. All method access is synchronous. Session beans must not be web service endpoints.</p></td>
</tr>
<tr class="even">
<td><p>Transactions</p></td>
<td><p>Container-managed and bean-managed transactions.</p></td>
</tr>
<tr class="odd">
<td><p>Security</p></td>
<td><p>Declarative and programmatic security.</p></td>
</tr>
<tr class="even">
<td><p>Interceptors</p></td>
<td><p>Class-level and method-level interceptors for session beans.</p></td>
</tr>
<tr class="odd">
<td><p>Deployment descriptor</p></td>
<td><p>The optional <code dir="ltr">ejb-jar.xml</code> deployment descriptor, with the same overriding rules for the enterprise bean container in Java EE servers.</p></td>
</tr>
</tbody>
</table>

  

Container providers are allowed to support the full set of features in
enterprise beans, but applications that use the embedded container will
not be portable if they use enterprise bean features not listed in
[Table 35-1](#GKCQC), such as the timer service, session beans as web
service endpoints, or remote business interfaces.

## 35.2.1 Running Embedded Applications

The embedded container, the enterprise bean components, and the client
all are executed in the same virtual machine using the same classpath.
As a result, developers can run an application that uses the embedded
container just like a typical Java SE application, as
follows:

``` oac_no_warn
java -classpath mySessionBean.jar:containerProviderRuntime.jar:myClient.jar \                                                                                            
com.example.ejb.client.Main
```

In the above example, `mySessionBean.jar` is an EJB JAR containing a
local stateless session bean, `containerProviderRuntime.jar` is a JAR
file supplied by the enterprise bean provider that contains the needed
runtime classes for the embedded container, and `myClient.jar` is a JAR
file containing a Java SE application that calls the business methods in
the session bean through the embedded container.

In GlassFish Server, the runtime JAR that includes the classes for the
embedded container is `glassfish-embedded-all.jar`.

## 35.2.2 Creating the Enterprise Bean Container

The `javax.ejb.embedded.EJBContainer` abstract class represents an
instance of the enterprise bean container and includes factory methods
for creating a container instance. The `EJBContainer.createEJBContainer`
method is used to create and initialize an embedded container instance.

The following code snippet shows how to create an embedded container
that is initialized with the container provider's default settings:

``` oac_no_warn
EJBContainer ec = EJBContainer.createEJBContainer();
```

By default, the embedded container will search the virtual machine
classpath for enterprise bean modules: directories containing a
`META-INF/ejb-jar.xml` deployment descriptor, directories containing a
class file with one of the enterprise bean component annotations (such
as `@Stateless`), or JAR files containing an `ejb-jar.xml` deployment
descriptor or class file with an enterprise bean annotation. Any
matching entries are considered enterprise bean modules within the same
application. Once all the valid enterprise bean modules have been found
in the classpath, the container will begin initializing the modules.
When the `createEJBContainer` method successfully returns, the client
application can obtain references to the client view of any enterprise
bean module found by the embedded container.

An alternate version of the `EJBContainer.createEJBContainer` method
takes a `Map` of properties and settings for customizing the embeddable
container instance:

``` oac_no_warn
Properties props = new Properties();
props.setProperty(...);
...
EJBContainer ec = EJBContainer.createEJBContainer(props);
```

### 35.2.2.1 Explicitly Specifying Enterprise Bean Modules to Be Initialized

Developers can specify exactly which enterprise bean modules the
embedded container will initialize. To explicitly specify the enterprise
bean modules initialized by the embedded container, set the
`EJBContainer.MODULES` property.

The modules may be located either in the virtual machine classpath in
which the embedded container and client code run, or alternately outside
the virtual machine classpath.

To specify modules in the virtual machine classpath, set
`EJBContainer.MODULES` to a `String` to specify a single module name, or
a `String` array containing the module names. The embedded container
searches the virtual machine classpath for enterprise bean modules
matching the specified names:

``` oac_no_warn
Properties props = new Properties();
props.setProperty(EJBContainer.MODULES, "mySessionBean");
EJBContainer ec = EJBContainer.createEJBContainer(props);
```

To specify enterprise bean modules outside the virtual machine
classpath, set `EJBContainer.MODULES` to a `java.io.File` object or an
array of `File` objects. Each `File` object refers to an EJB JAR file,
or a directory containing an expanded EJB JAR file:

``` oac_no_warn
Properties props = new Properties();
File ejbJarFile = new File(...);
props.setProperty(EJBContainer.MODULES, ejbJarFile);
EJBContainer ec = EJBContainer.createEJBContainer(props);
```

## 35.2.3 Looking Up Session Bean References

To look up session bean references in an application using the embedded
container:

1.  Use an instance of `EJBContainer` to retrieve a
    `javax.naming.Context` object.
    
    Call the `EJBContainer.getContext` method to retrieve the `Context`
    object:
    
    ``` oac_no_warn
    EJBContainer ec = EJBContainer.createEJBContainer();
    Context ctx = ec.getContext();
    ```
    
    References to session beans can then be obtained using the portable
    JNDI syntax detailed in [Portable JNDI
    Syntax](ejb-intro004.htm#GIRGN). For example, to obtain a reference
    to `MySessionBean`, a local session bean with a no-interface view,
    use the following code:
    
    ``` oac_no_warn
    MySessionBean msb = (MySessionBean) 
                ctx.lookup("java:global/mySessionBean/MySessionBean");
    ```

## 35.2.4 Shutting Down the Enterprise Bean Container

To shut down the embedded container:

1.  From the client, call the `close` method of the instance of
    `EJBContainer`.
    
    ``` oac_no_warn
    EJBContainer ec = EJBContainer.createEJBContainer();
    ...
    ec.close();
    ```
    
    While clients are not required to shut down `EJBContainer`
    instances, doing so frees resources consumed by the embedded
    container. This is particularly important when the virtual machine
    under which the client application is running has a longer lifetime
    than the client application.

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
<td><a href="ejb-embedded001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-embedded003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
