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
<td><a href="jsf-facelets005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 8.6 Web Resources

Web resources are any software artifacts that the web application
requires for proper rendering, including images, script files, and any
user-created component libraries. Resources must be collected in a
standard location, which can be one of the following.

  - A resource packaged in the web application root must be in a
    subdirectory of a `resources` directory at the web application root:
    `resources/`resource-identifier.

  - A resource packaged in the web application's classpath must be in a
    subdirectory of the `META-INF/resources` directory within a web
    application: `META-INF/resources/`resource-identifier. You can use
    this file structure to package resources in a JAR file bundled in
    the web application.

The JavaServer Faces runtime will look for the resources in the
preceding listed locations, in that order.

Resource identifiers are unique strings that conform to the following
format (all on one
line):

``` oac_no_warn
[locale-prefix/][library-name/][library-version/]resource-name[/resource-version]
```

Elements of the resource identifier in brackets (`[]`) are optional,
indicating that only a resource-name, which is usually a file name, is a
required element. For example, the most common way to specify a style
sheet, image, or script is to use the `library` and `name` attributes,
as in the following tag from the `guessnumber-jsf` example:

``` oac_no_warn
<h:outputStylesheet library="css" name="default.css"/>
```

This tag specifies that the `default.css` style sheet is in the
directory `web/resources/css`.

You can also specify the location of an image using the following
syntax, also from the `guessnumber-jsf` example:

``` oac_no_warn
<h:graphicImage value="#{resource['images:wave.med.gif']}"/>
```

This tag specifies that the image named `wave.med.gif` is in the
directory `web/resources/images`.

Resources can be considered as a library location. Any artifact, such as
a composite component or a template that is stored in the `resources`
directory, becomes accessible to the other application components, which
can use it to create a resource instance.

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
<td><a href="jsf-facelets005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
