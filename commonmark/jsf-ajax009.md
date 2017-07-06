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
<td><a href="jsf-ajax008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax010.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 13.9 Grouping of Components

The previous sections describe how to associate a single UI component
with Ajax functionality. You can also associate Ajax with more than one
component at a time by grouping them together on a page. The following
example shows how a number of components can be grouped by using the
`f:ajax` tag:

``` oac_no_warn
<f:ajax>
    <h:form>
        <h:inputText id="input1" value="#{user.name}"/> 
        <h:commandButton id="Submit"/>
    </h:form>
</f:ajax>
```

In the example, neither component is associated with any Ajax `event` or
`render` attributes yet. Therefore, no action will take place in case of
user input. You can associate the above components with an `event` and a
`render` attribute as follows:

``` oac_no_warn
<f:ajax event="click" render="@all">
    <h:form>
        <h:inputText id="input1" value="#{user.name}"/> 
        <h:commandButton id="Submit"/> 
    </h:form>
</f:ajax>
```

In the updated example, when the user clicks either component, the
updated results will be displayed for all components. You can further
fine-tune the Ajax action by adding specific events to each of the
components, in which case Ajax functionality becomes cumulative.
Consider the following example:

``` oac_no_warn
<f:ajax event="click" render="@all">
    ...
    <h:commandButton id="Submit">
        <f:ajax event="mouseover"/>
    </h:commandButton>
    ...
</f:ajax>
```

Now the button component will fire an Ajax action in case of a
`mouseover` event as well as a mouse-click event.

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
<td><a href="jsf-ajax008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax010.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
