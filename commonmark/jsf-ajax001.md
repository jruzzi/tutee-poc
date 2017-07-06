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
<td><a href="jsf-ajax.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 13.1 Overview of Ajax

Early web applications were created mostly as static web pages. When a
static web page is updated by a client, the entire page has to reload to
reflect the update. In effect, every update needs a page reload to
reflect the change. Repetitive page reloads can result in excessive
network access and can impact application performance. Technologies such
as Ajax were created to overcome these deficiencies.

Ajax refers to JavaScript and XML, technologies that are widely used for
creating dynamic and asynchronous web content. While Ajax is not limited
to JavaScript and XML technologies, more often than not they are used
together by web applications. The focus of this tutorial is on using
JavaScript based Ajax functionality in JavaServer Faces web
applications.

JavaScript is a dynamic scripting language for web applications. It
allows users to add enhanced functionality to user interfaces and allows
web pages to interact with clients asynchronously. JavaScript runs
mainly on the client side (as in a browser) and thereby reduces server
access by clients.

When a JavaScript function sends an asynchronous request from the client
to the server, the server sends back a response that is used to update
the page's Document Object Model (DOM). This response is often in the
format of an XML document. The term Ajax refers to this interaction
between the client and server.

The server response need not be in XML only; it can also be in other
formats, such as JSON (see [Introduction to JSON](jsonp001.htm#BABEECIB)
and `http://www.json.org/`). This tutorial does not focus on the
response formats.

Ajax enables asynchronous and partial updating of web applications. Such
functionality allows for highly responsive web pages that are rendered
in near real time. Ajax-based web applications can access server and
process information and can also retrieve data without interfering with
the display and rendering of the current web page on a client (such as a
browser).

Some of the advantages of using Ajax are as follows:

  - Form data validation in real time, eliminating the need to submit
    the form for verification

  - Enhanced functionality for web pages, such as user name and password
    prompts

  - Partial update of the web content, avoiding complete page reloads

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
<td><a href="jsf-ajax.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
