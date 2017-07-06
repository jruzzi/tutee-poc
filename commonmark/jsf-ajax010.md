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
<td><a href="jsf-ajax009.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax011.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 13.10 Loading JavaScript as a Resource

The JavaScript resource file bundled with JavaServer Faces technology is
named `jsf.js` and is available in the `javax.faces` library. This
resource library supports Ajax functionality in JavaServer Faces
applications.

If you use the `f:ajax` tag on a page, the `jsf.js` resource is
automatically delivered to the client. It is not necessary to use the
`h:outputScript` tag to specify this resource. You may want to use the
`h:outputScript` tag to specify other JavaScript libraries.

To use a JavaScript resource directly with a `UIComponent`, you must
explicitly load the resource as described in either of the following
topics:

  - [Section 13.10.1, "Using JavaScript API in a Facelets
    Application"](#GKAFI) – Uses the `h:outputScript` tag directly in a
    Facelets page

  - [Section 13.10.2, "Using the @ResourceDependency Annotation in a
    Bean Class"](#GKIPX) – Uses the
    `javax.faces.application.ResourceDependency` annotation on a
    `UIComponent` Java class

## 13.10.1 Using JavaScript API in a Facelets Application

To use the JavaScript resource API directly in a web application, such
as a Facelets page:

1.  Identify the default JavaScript resource for the page with the help
    of the `h:outputScript` tag.
    
    For example, consider the following section of a Facelets page:
    
    ``` oac_no_warn
    <h:form>
        <h:outputScript name="jsf.js" library="javax.faces" target="head"/>
    </h:form>
    ```
    
    Specifying the target as `head` causes the script resource to be
    rendered within the `head` element on the HTML page.

2.  Identify the component to which you would like to attach the Ajax
    functionality.

3.  Add the Ajax functionality to the component by using the JavaScript
    API. For example, consider the following:
    
    ``` oac_no_warn
    <h:form>
        <h:outputScript name="jsf.js" library="javax.faces" target="head">
        <h:inputText id="inputname" value="#{userBean.name}"/>
        <h:outputText id="outputname" value="#{userBean.name}"/>
        <h:commandButton id="submit" value="Submit"
                         onclick="jsf.ajax.request(this, event, 
                                  {execute:'inputname',render:'outputname'});
                                  return false;" />
    </h:form>
    ```
    
    The `jsf.ajax.request` method takes up to three parameters that
    specify source, event, and options. The source parameter identifies
    the DOM element that triggered the Ajax request, typically `this`.
    The optional event parameter identifies the DOM event that triggered
    this request. The optional options parameter contains a set of
    name/value pairs from [Table 13-5](#GKAIW).
    
    Table 13-5 Possible Values for the Options Parameter
    
    <table style="width:14%;">
    <colgroup>
    <col width="14%" />
    <col width="0%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Name</th>
    <th>Value</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><code dir="ltr">execute</code></p></td>
    <td><p>A space-delimited list of client identifiers or one of the keywords listed in <a href="jsf-ajax003.htm#GKNLK">Table 13-2</a>. The identifiers reference the components that will be processed during the Execute phase of the lifecycle.</p></td>
    </tr>
    <tr class="even">
    <td><p><code dir="ltr">render</code></p></td>
    <td><p>A space-delimited list of client identifiers or one of the keywords listed in <a href="jsf-ajax003.htm#GKNLK">Table 13-2</a>. The identifiers reference the components that will be processed during the render phase of the lifecycle.</p></td>
    </tr>
    <tr class="odd">
    <td><p><code dir="ltr">onevent</code></p></td>
    <td><p>A <code dir="ltr">String</code> that is the name of the JavaScript function to call when an event occurs.</p></td>
    </tr>
    <tr class="even">
    <td><p><code dir="ltr">onerror</code></p></td>
    <td><p>A <code dir="ltr">String</code> that is the name of the JavaScript function to call when an error occurs.</p></td>
    </tr>
    <tr class="odd">
    <td><p><code dir="ltr">params</code></p></td>
    <td><p>An object that may include additional parameters to include in the request.</p></td>
    </tr>
    </tbody>
    </table>
    
      
    
    If no identifier is specified, the default assumed keyword for the
    `execute` attribute is `@this`, and for the `render` attribute it is
    `@none`.
    
    You can also place the JavaScript method in a file and include it as
    a resource.

## 13.10.2 Using the @ResourceDependency Annotation in a Bean Class

Use the `javax.faces.application.ResourceDependency` annotation to cause
the bean class to load the default `jsf.js` library.

To load the Ajax resource from the server side:

1.  Use the `jsf.ajax.request` method within the bean class.
    
      
    
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Note:</p>
    This method is usually used when creating a custom component or a custom renderer for a component.</td>
    </tr>
    </tbody>
    </table>
    
      
    
    The following example shows how the resource is loaded in a bean
    class:
    
    ``` oac_no_warn
    @ResourceDependency(name="jsf.js" library="javax.faces" target="head")
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
<td><a href="jsf-ajax009.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax011.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
