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
<td><a href="jsf-facelets003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 8.4 Using Facelets Templates

JavaServer Faces technology provides the tools to implement user
interfaces that are easy to extend and reuse. Templating is a useful
Facelets feature that allows you to create a page that will act as the
base, or template, for the other pages in an application. By using
templates, you can reuse code and avoid recreating similarly constructed
pages. Templating also helps in maintaining a standard look and feel in
an application with a large number of pages.

[Table 8-2](#GJBFP) lists Facelets tags that are used for templating and
their respective functionality.

Table 8-2 Facelets Templating Tags

<table style="width:22%;">
<colgroup>
<col width="22%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">ui:component</code></p></td>
<td><p>Defines a component that is created and added to the component tree.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">ui:composition</code></p></td>
<td><p>Defines a page composition that optionally uses a template. Content outside of this tag is ignored.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ui:debug</code></p></td>
<td><p>Defines a debug component that is created and added to the component tree.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">ui:decorate</code></p></td>
<td><p>Similar to the composition tag but does not disregard content outside this tag.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ui:define</code></p></td>
<td><p>Defines content that is inserted into a page by a template.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">ui:fragment</code></p></td>
<td><p>Similar to the component tag but does not disregard content outside this tag.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ui:include</code></p></td>
<td><p>Encapsulates and reuses content for multiple pages.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">ui:insert</code></p></td>
<td><p>Inserts content into a template.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ui:param</code></p></td>
<td><p>Used to pass parameters to an included file.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">ui:repeat</code></p></td>
<td><p>Used as an alternative for loop tags, such as <code dir="ltr">c:forEach</code> or <code dir="ltr">h:dataTable.</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ui:remove</code></p></td>
<td><p>Removes content from a page.</p></td>
</tr>
</tbody>
</table>

  

For more information on Facelets templating tags, see the [JavaServer
Faces Facelets Tag Library documentation](olink:JSFTL).

The Facelets tag library includes the main templating tag `ui:insert`. A
template page that is created with this tag allows you to define a
default structure for a page. A template page is used as a template for
other pages, usually referred to as client pages.

Here is an example of a template saved as `template.xhtml`:

``` oac_no_warn
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" 
      "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:ui="http://xmlns.jcp.org/jsf/facelets"
      xmlns:h="http://xmlns.jcp.org/jsf/html">
    
    <h:head>
        <meta http-equiv="Content-Type" 
              content="text/html; charset=UTF-8" />
        <h:outputStylesheet library="css" name="default.css"/>
        <h:outputStylesheet library="css" name="cssLayout.css"/>
        <title>Facelets Template</title>
    </h:head>
    
    <h:body>
        <div id="top" class="top">
            <ui:insert name="top">Top Section</ui:insert>
        </div>
        <div>
        <div id="left">
             <ui:insert name="left">Left Section</ui:insert>
        </div>
        <div id="content" class="left_content">
             <ui:insert name="content">Main Content</ui:insert>
        </div>
        </div>
    </h:body>
</html>
```

The example page defines an XHTML page that is divided into three
sections: a top section, a left section, and a main section. The
sections have style sheets associated with them. The same structure can
be reused for the other pages of the application.

The client page invokes the template by using the `ui:composition` tag.
In the following example, a client page named `templateclient.xhtml`
invokes the template page named `template.xhtml` from the preceding
example. A client page allows content to be inserted with the help of
the `ui:define` tag.

``` oac_no_warn
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" 
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:ui="http://xmlns.jcp.org/jsf/facelets"
      xmlns:h="http://xmlns.jcp.org/jsf/html">
    
    <h:body>
        <ui:composition template="./template.xhtml">
            <ui:define name="top">
                Welcome to Template Client Page
            </ui:define>

            <ui:define name="left">
                <h:outputLabel value="You are in the Left Section"/>
            </ui:define>

            <ui:define name="content">
                <h:graphicImage value="#{resource['images:wave.med.gif']}"/>
                <h:outputText value="You are in the Main Content Section"/>
            </ui:define>
        </ui:composition>
    </h:body>
</html>
```

You can use NetBeans IDE to create Facelets template and client pages.
For more information on creating these pages, see
`https://netbeans.org/kb/docs/web/jsf20-intro.html`.

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
<td><a href="jsf-facelets003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
