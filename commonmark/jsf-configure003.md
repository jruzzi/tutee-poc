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
<td><a href="jsf-configure002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 16.3 Application Configuration Resource File

JavaServer Faces technology provides a portable configuration format (as
an XML document) for configuring application resources. One or more XML
documents, called application configuration resource files, may use this
format to register and configure objects and resources and to define
navigation rules for applications. An application configuration resource
file is usually named `faces-config.xml`.

You need an application configuration resource file in the following
cases:

  - To specify configuration elements for your application that are not
    available through managed bean annotations, such as localized
    messages and navigation rules

  - To override managed bean annotations when the application is
    deployed

The application configuration resource file must be valid against the
XML schema located at
`http://xmlns.jcp.org/xml/ns/javaee/web-facesconfig_2_2.xsd`.

In addition, each file must include the following information, in the
following order:

  - The XML version number, usually with an `encoding` attribute:
    
    ``` oac_no_warn
    <?xml version="1.0" encoding='UTF-8'?>
    ```

  - A `faces-config` tag enclosing all the other
    declarations:
    
    ``` oac_no_warn
    <faces-config version="2.2" xmlns="http://xmlns.jcp.org/xml/ns/javaee" 
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee 
                  http://xmlns.jcp.org/xml/ns/javaee/web-facesconfig_2_2.xsd"> 
        ...
    </faces-config>
    ```

You can have more than one application configuration resource file for
an application. The JavaServer Faces implementation finds the
configuration file or files by looking for the following.

  - A resource named `/META-INF/faces-config.xml` in any of the JAR
    files in the web application's `/WEB-INF/lib/` directory and in
    parent class loaders. If a resource with this name exists, it is
    loaded as a configuration resource. This method is practical for a
    packaged library containing some components and renderers. In
    addition, any file with a name that ends in `faces-config.xml` is
    also considered a configuration resource and is loaded as such.

  - A context initialization parameter,
    `javax.faces.application.CONFIG_FILES`, in your web deployment
    descriptor file that specifies one or more (comma-delimited) paths
    to multiple configuration files for your web application. This
    method is most often used for enterprise-scale applications that
    delegate to separate groups the responsibility for maintaining the
    file for each portion of a big application.

  - A resource named `faces-config.xml` in the `/WEB-INF/` directory of
    your application. Simple web applications make their configuration
    files available in this way.

To access the resources registered with the application, an application
developer can use an instance of the
`javax.faces.application.Application` class, which is automatically
created for each application. The `Application` instance acts as a
centralized factory for resources that are defined in the XML file.

When an application starts up, the JavaServer Faces implementation
creates a single instance of the `Application` class and configures it
with the information you provided in the application configuration
resource file.

## 16.3.1 Configuring Eager Application-Scoped Managed Beans

JavaServer Faces managed beans (either specified in the
f`aces-config.xml` file or annotated with
`javax.faces.bean.ManagedBean`) are lazily instantiated. That is, that
they are instantiated when a request is made from the application.

To force an application-scoped bean to be instantiated and placed in the
application scope as soon as the application is started and before any
request is made, the `eager` attribute of the managed bean should be set
to `true`, as shown in the following examples.

The `faces-config.xml` file declaration is as follows:

``` oac_no_warn
<managed-bean eager="true">
```

The annotation is as follows:

``` oac_no_warn
@ManagedBean(eager=true)
@ApplicationScoped
```

## 16.3.2 Ordering of Application Configuration Resource Files

Because JavaServer Faces technology allows the use of multiple
application configuration resource files stored in different locations,
the order in which they are loaded by the implementation becomes
important in certain situations (for example, when using
application-level objects). This order can be defined through an
`ordering` element and its subelements in the application configuration
resource file itself. The ordering of application configuration resource
files can be absolute or relative.

Absolute ordering is defined by an `absolute-ordering` element in the
file. With absolute ordering, the user specifies the order in which
application configuration resource files will be loaded. The following
example shows an entry for absolute ordering.

File `my-faces-config.xml` contains the following elements:

``` oac_no_warn
<faces-config>
    <name>myJSF</name>
    <absolute-ordering>
        <name>A</name>
        <name>B</name>
        <name>C</name>
    </absolute-ordering>
</faces-config>
```

In this example, A, B, and C are different application configuration
resource files and are to be loaded in the listed order.

If there is an `absolute-ordering` element in the file, only the files
listed by the subelement `name` are processed. To process any other
application configuration resource files, an `others` subelement is
required. In the absence of the `others` subelement, all other unlisted
files will be ignored at load time.

Relative ordering is defined by an `ordering` element and its
subelements `before` and `after`. With relative ordering, the order in
which application configuration resource files will be loaded is
calculated by considering ordering entries from the different files. The
following example shows some of these considerations. In the following
example, `config-A`, `config-B`, and `config-C` are different
application configuration resource files.

File `config-A` contains the following elements:

``` oac_no_warn
<faces-config>
    <name>config-A</name>
    <ordering>
        <before>
            <name>config-B</name>
        </before>
    </ordering>
</faces-config>
```

File `config-B` (not shown here) does not contain any `ordering`
elements.

File `config-C` contains the following elements:

``` oac_no_warn
<faces-config>
    <name>config-C</name>
    <ordering>
        <after>
            <name>config-B</name>
        </after>
    </ordering>
</faces-config>
```

Based on the `before` subelement entry, file `config-A` will be loaded
before the `config-B` file. Based on the `after` subelement entry, file
`config-C` will be loaded after the `config-B` file.

In addition, a subelement `others` can also be nested within the
`before` and `after` subelements. If the `others` element is present,
the specified file may receive highest or lowest preference among both
listed and unlisted configuration files.

If an `ordering` element is not present in an application configuration
file, then that file will be loaded after all the files that contain
`ordering` elements.

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
<td><a href="jsf-configure002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
