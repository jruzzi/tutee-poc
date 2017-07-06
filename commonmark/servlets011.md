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
<td><a href="servlets010.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets012.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.11 Uploading Files with Java Servlet Technology

Supporting file uploads is a very basic and common requirement for many
web applications. In prior versions of the Servlet specification,
implementing file upload required the use of external libraries or
complex input processing. The Java Servlet specification now helps to
provide a viable solution to the problem in a generic and portable way.
Java Servlet technology now supports file upload out of the box, so any
web container that implements the specification can parse multipart
requests and make mime attachments available through the
`HttpServletRequest` object.

A new annotation, `javax.servlet.annotation.MultipartConfig`, is used to
indicate that the servlet on which it is declared expects requests to be
made using the `multipart/form-data` MIME type. Servlets that are
annotated with `@MultipartConfig` can retrieve the `Part` components of
a given `multipart/form-data` request by calling the
`request.getPart(String name)` or `request.getParts()` method.

## 17.11.1 The @MultipartConfig Annotation

The `@MultipartConfig` annotation supports the following optional
attributes.

  - `location`: An absolute path to a directory on the file system. The
    `location` attribute does not support a path relative to the
    application context. This location is used to store files
    temporarily while the parts are processed or when the size of the
    file exceeds the specified `fileSizeThreshold` setting. The default
    location is `""`.

  - `fileSizeThreshold`: The file size in bytes after which the file
    will be temporarily stored on disk. The default size is 0 bytes.

  - `MaxFileSize`: The maximum size allowed for uploaded files, in
    bytes. If the size of any uploaded file is greater than this size,
    the web container will throw an exception (`IllegalStateException`).
    The default size is unlimited.

  - `maxRequestSize`: The maximum size allowed for a
    `multipart/form-data` request, in bytes. The web container will
    throw an exception if the overall size of all uploaded files exceeds
    this threshold. The default size is unlimited.

For, example, the `@MultipartConfig` annotation could be constructed as
follows:

``` oac_no_warn
@MultipartConfig(location="/tmp", fileSizeThreshold=1024*1024,
    maxFileSize=1024*1024*5, maxRequestSize=1024*1024*5*5)
```

Instead of using the `@MultipartConfig` annotation to hard-code these
attributes in your file upload servlet, you could add the following as a
child element of the servlet configuration element in the `web.xml`
file:

``` oac_no_warn
<multipart-config>
    <location>/tmp</location>
    <max-file-size>20848820</max-file-size>
    <max-request-size>418018841</max-request-size>
    <file-size-threshold>1048576</file-size-threshold>
</multipart-config>
```

## 17.11.2 The getParts and getPart Methods

The Servlet specification supports two additional `HttpServletRequest`
methods:

  - `Collection<Part> getParts()`

  - `Part getPart(String name)`

The `request.getParts()` method returns collections of all `Part`
objects. If you have more than one input of type file, multiple `Part`
objects are returned. Because `Part` objects are named, the
`getPart(String name)` method can be used to access a particular `Part`.
Alternatively, the `getParts()` method, which returns an
`Iterable<Part>`, can be used to get an `Iterator` over all the `Part`
objects.

The `javax.servlet.http.Part` interface is a simple one, providing
methods that allow introspection of each `Part`. The methods do the
following:

  - Retrieve the name, size, and content-type of the `Part`

  - Query the headers submitted with a `Part`

  - Delete a `Part`

  - Write a `Part` out to disk

For example, the `Part` interface provides the `write(String filename)`
method to write the file with the specified name. The file can then be
saved in the directory that is specified with the `location` attribute
of the `@MultipartConfig` annotation or, in the case of the `fileupload`
example, in the location specified by the Destination field in the form.

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
<td><a href="servlets010.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets012.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
