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
<td><a href="jsf-custom003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 15.4 Steps for Creating a Custom Component

You can apply the following steps while developing your own custom
component.

1.  Create a custom component class that does the following:
    
    1.  Overrides the `getFamily` method to return the component family,
        which is used to look up renderers that can render the component
    
    2.  Includes the rendering code or delegates it to a renderer
        (explained in Step [2](#CDECBJAE))
    
    3.  Enables component attributes to accept expressions
    
    4.  Queues an event on the component if the component generates
        events
    
    5.  Saves and restores the component state

2.  Delegate rendering to a renderer if your component does not handle
    the rendering. To do this:
    
    1.  Create a custom renderer class by extending
        `javax.faces.render.Renderer`.
    
    2.  Register the renderer to a render kit.

3.  Register the component.

4.  Create an event handler if your component generates events.

5.  Create a tag library descriptor (TLD) that defines the custom tag.

See [Registering a Custom Component](jsf-configure012.htm#BNAXI) and
[Registering a Custom Renderer with a Render
Kit](jsf-configure011.htm#BNAXH) for information on registering the
custom component and the renderer. The section [Using a Custom
Component](jsf-custom010.htm#BNATT) discusses how to use the custom
component in a JavaServer Faces page.

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
<td><a href="jsf-custom003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
