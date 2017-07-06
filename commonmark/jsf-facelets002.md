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
<td><a href="jsf-facelets001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 8.2 The Lifecycle of a Facelets Application

The JavaServer Faces specification defines the lifecycle of a JavaServer
Faces application. For more information on this lifecycle, see [The
Lifecycle of a JavaServer Faces Application](jsf-intro007.htm#BNAQQ).
The following steps describe that process as applied to a Facelets-based
application.

1.  When a client, such as a browser, makes a new request to a page that
    is created using Facelets, a new component tree or
    `javax.faces.component.UIViewRoot` is created and placed in the
    `FacesContext`.

2.  The `UIViewRoot` is applied to the Facelets, and the view is
    populated with components for rendering.

3.  The newly built view is rendered back as a response to the client.

4.  On rendering, the state of this view is stored for the next request.
    The state of input components and form data is stored.

5.  The client may interact with the view and request another view or
    change from the JavaServer Faces application. At this time, the
    saved view is restored from the stored state.

6.  The restored view is once again passed through the JavaServer Faces
    lifecycle, which eventually will either generate a new view or
    re-render the current view if there were no validation problems and
    no action was triggered.

7.  If the same view is requested, the stored view is rendered once
    again.

8.  If a new view is requested, then the process described in Step
    [2](#BABGCBAJ) is continued.

9.  The new view is then rendered back as a response to the client.

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
<td><a href="jsf-facelets001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
