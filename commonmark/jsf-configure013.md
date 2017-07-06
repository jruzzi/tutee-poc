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
<td><a href="jsf-configure012.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 16.13 Basic Requirements of a JavaServer Faces Application

In addition to configuring your application, you must satisfy other
requirements of JavaServer Faces applications, including properly
packaging all the necessary files and providing a deployment descriptor.
This section describes how to perform these administrative tasks.

JavaServer Faces applications can be packaged in a WAR file, which must
conform to specific requirements to execute across different containers.
At a minimum, a WAR file for a JavaServer Faces application may contain
the following:

  - A web application deployment descriptor, called `web.xml`, to
    configure resources required by a web application (required)

  - A specific set of JAR files containing essential classes (optional)

  - A set of application classes, JavaServer Faces pages, and other
    required resources, such as image files

A WAR file may also contain:

  - An application configuration resource file, which configures
    application resources

  - A set of tag library descriptor files

For example, a Java Server Faces web application WAR file using Facelets
typically has the following directory structure:

``` oac_no_warn
$PROJECT_DIR
[Web Pages]
+- /[xhtml or html documents]
+- /resources
+- /WEB-INF
   +- /web.xml
   +- /beans.xml (optional)
   +- /classes (optional)
   +- /lib (optional)
   +- /faces-config.xml (optional)
   +- /*.taglib.xml (optional)
   +- /glassfish-web.xml (optional)
```

The `web.xml` file (or web deployment descriptor), the set of JAR files,
and the set of application files must be contained in the `WEB-INF`
directory of the WAR file.

## 16.13.1 Configuring an Application with a Web Deployment Descriptor

Web applications are commonly configured using elements contained in the
web application deployment descriptor, `web.xml`. The deployment
descriptor for a JavaServer Faces application must specify certain
configurations, including the following:

  - The servlet used to process JavaServer Faces requests

  - The servlet mapping for the processing servlet

  - The path to the configuration resource file, if it exists and is not
    located in a default location

The deployment descriptor can also include other, optional
configurations, such as those that

  - Specify where component state is saved

  - Encrypt state saved on the client

  - Compress state saved on the client

  - Restrict access to pages containing JavaServer Faces tags

  - Turn on XML validation

  - Specify the Project Stage

  - Verify custom objects

This section gives more details on these configurations. Where
appropriate, it also describes how you can make these configurations
using NetBeans IDE.

### 16.13.1.1 Identifying the Servlet for Lifecycle Processing

A requirement of a JavaServer Faces application is that all requests to
the application that reference previously saved JavaServer Faces
components must go through `javax.faces.webapp.FacesServlet`. A
`FacesServlet` instance manages the request-processing lifecycle for web
applications and initializes the resources required by JavaServer Faces
technology.

Before a JavaServer Faces application can launch its first web page, the
web container must invoke the `FacesServlet` instance in order for the
application lifecycle process to start. See [The Lifecycle of a
JavaServer Faces Application](jsf-intro007.htm#BNAQQ) for more
information.

The following example shows the default configuration of the
`FacesServlet`:

``` oac_no_warn
<servlet>
    <servlet-name>Faces Servlet</servlet-name>
    <servlet-class>javax.faces.webapp.FacesServlet</servlet-class>
</servlet>
```

You will provide a mapping configuration entry to make sure that the
`FacesServlet` instance is invoked. The mapping to `FacesServlet` can be
a prefix mapping, such as `/faces/*`, or an extension mapping, such as
`*.xhtml`. The mapping is used to identify a page as having JavaServer
Faces content. Because of this, the URL to the first page of the
application must include the URL pattern mapping.

The following elements specify a prefix mapping:

``` oac_no_warn
<servlet-mapping>
    <servlet-name>Faces Servlet</servlet-name>
    <url-pattern>/faces/*</url-pattern>
</servlet-mapping>
...
<welcome-file-list>
    <welcome-file>faces/greeting.xhtml</welcome-file>
</welcome-file-list>
```

The following elements, used in the tutorial examples, specify an
extension mapping:

``` oac_no_warn
<servlet-mapping>
    <servlet-name>Faces Servlet</servlet-name>
    <url-pattern>*.xhtml</url-pattern>
</servlet-mapping>
...
<welcome-file-list>
    <welcome-file>index.xhtml</welcome-file>
</welcome-file-list>
```

When you use this mechanism, users access the application as shown in
the following example:

``` oac_no_warn
http://localhost:8080/guessNumber
```

In the case of extension mapping, if a request comes to the server for a
page with an `.xhtml` extension, the container will send the request to
the `FacesServlet` instance, which will expect a corresponding page of
the same name containing the content to exist.

If you are using NetBeans IDE to create your application, a web
deployment descriptor is automatically created for you with default
configurations. If you created your application without an IDE, you can
create a web deployment
descriptor.

### 16.13.1.2 To Specify a Path to an Application Configuration Resource File

As explained in [Application Configuration Resource
File](jsf-configure003.htm#BNAWP), an application can have multiple
application configuration resource files. If these files are not located
in the directories that the implementation searches by default or the
files are not named `faces-config.xml`, you need to specify paths to
these files.

To specify these paths using NetBeans IDE, do the following.

1.  Expand the node of your project in the Projects tab.

2.  Expand the Web Pages and WEB-INF nodes that are under the project
    node.

3.  Double-click `web.xml`.

4.  After the `web.xml` file appears in the editor, click General at the
    top of the editor window.

5.  Expand the Context Parameters node.

6.  Click Add.

7.  In the Add Context Parameter dialog box:
    
    1.  Enter `javax.faces.CONFIG_FILES` in the Parameter Name field.
    
    2.  Enter the path to your configuration file in the Parameter Value
        field.
    
    3.  Click OK.

8.  Repeat steps 1 through 7 for each configuration file.

### 16.13.1.3 To Specify Where State Is Saved

For all the components in a web application, you can specify in your
deployment descriptor where you want the state to be saved, on either
client or server. You do this by setting a context parameter in your
deployment descriptor. By default, state is saved on the server, so you
need to specify this context parameter only if you want to save state on
the client. See [Saving and Restoring State](jsf-custom005.htm#BNAVZ)
for information on the advantages and disadvantages of each location.

To specify where state is saved using NetBeans IDE, do the following.

1.  Expand the node of your project in the Projects tab.

2.  Expand the Web Pages and WEB-INF nodes under the project node.

3.  Double-click `web.xml`.

4.  After the `web.xml` file appears in the editor window, click General
    at the top of the editor window.

5.  Expand the Context Parameters node.

6.  Click Add.

7.  In the Add Context Parameter dialog box:
    
    1.  Enter `javax.faces.STATE_SAVING_METHOD` in the Parameter Name
        field.
    
    2.  Enter `client` or `server` in the Parameter Value field.
    
    3.  Click OK.

If state is saved on the client, the state of the entire view is
rendered to a hidden field on the page. The JavaServer Faces
implementation saves the state on the server by default. Duke's Forest
saves its state on the client.

## 16.13.2 Configuring Project Stage

Project Stage is a context parameter identifying the status of a
JavaServer Faces application in the software lifecycle. The stage of an
application can affect the behavior of the application. For example,
error messages can be displayed during the Development stage but
suppressed during the Production stage.

The possible Project Stage values are as follows:

  - `Development`

  - `UnitTest`

  - `SystemTest`

  - `Production`

Project Stage is configured through a context parameter in the web
deployment descriptor file. Here is an example:

``` oac_no_warn
<context-param>
    <param-name>javax.faces.PROJECT_STAGE</param-name>
    <param-value>Development</param-value>
</context-param>
```

If no Project Stage is defined, the default stage is `Production`. You
can also add custom stages according to your requirements.

## 16.13.3 Including the Classes, Pages, and Other Resources

When packaging web applications using the included build scripts, you'll
notice that the scripts package resources in the following ways.

  - All web pages are placed at the top level of the WAR file.

  - The `faces-config.xml` file and the `web.xml` file are packaged in
    the `WEB-INF` directory.

  - All packages are stored in the `WEB-INF/classes/` directory.

  - All application JAR files are packaged in the `WEB-INF/lib/`
    directory.

  - All resource files are either under the root of the web application
    `/resources` directory or in the web application's classpath, the
    `META-INF/resources/`resourceIdentifier directory. For more
    information on resources, see [Web
    Resources](jsf-facelets006.htm#GIRGM).

When packaging your own applications, you can use NetBeans IDE or you
can use XML files such as those created for Maven. You can modify the
XML files to fit your situation. However, you can continue to package
your WAR files by using the directory structure described in this
section, because this technique complies with the commonly accepted
practice for packaging web applications.

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
<td><a href="jsf-configure012.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
