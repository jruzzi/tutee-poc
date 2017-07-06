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
<td><a href="servlets003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 17.4 Creating and Initializing a Servlet

Use the `@WebServlet` annotation to define a servlet component in a web
application. This annotation is specified on a class and contains
metadata about the servlet being declared. The annotated servlet must
specify at least one URL pattern. This is done by using the
`urlPatterns` or `value` attribute on the annotation. All other
attributes are optional, with default settings. Use the `value`
attribute when the only attribute on the annotation is the URL pattern;
otherwise, use the `urlPatterns` attribute when other attributes are
also used.

Classes annotated with `@WebServlet` must extend the
`javax.servlet.http.HttpServlet` class. For example, the following code
snippet defines a servlet with the URL pattern `/report`:

``` oac_no_warn
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;

@WebServlet("/report")
public class MoodServlet extends HttpServlet {
    ...
```

The web container initializes a servlet after loading and instantiating
the servlet class and before delivering requests from clients. To
customize this process to allow the servlet to read persistent
configuration data, initialize resources, and perform any other one-time
activities, you can either override the `init` method of the `Servlet`
interface or specify the `initParams` attribute of the `@WebServlet`
annotation. The `initParams` attribute contains a `@WebInitParam`
annotation. If it cannot complete its initialization process, a servlet
throws an `UnavailableException`.

Use an initialization parameter to provide data needed by a particular
servlet. By contrast, a context parameter provides data that is
available to all components of a web application.

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
<td><a href="servlets003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="servlets005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
