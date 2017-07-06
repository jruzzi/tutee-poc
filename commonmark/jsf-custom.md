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
<td><a href="jsf-advanced-cc004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 15 Creating Custom UI Components and Other Custom Objects

This chapter describes creating custom components for applications that
have additional functionality not provided by standard JavaServer Faces
components.

The following topics are addressed here:

  - [Introduction to Creating Custom
    Components](jsf-custom001.htm#A1350198)

  - [Determining Whether You Need a Custom Component or
    Renderer](jsf-custom002.htm#BNAVH)

  - [Understanding the Image Map Example](jsf-custom003.htm#GLPCB)

  - [Steps for Creating a Custom Component](jsf-custom004.htm#BNAVT)

  - [Creating Custom Component Classes](jsf-custom005.htm#BNAVU)

  - [Delegating Rendering to a Renderer](jsf-custom006.htm#BNAWA)

  - [Implementing an Event Listener](jsf-custom007.htm#BNAUT)

  - [Handling Events for Custom Components](jsf-custom008.htm#BNAWD)

  - [Defining the Custom Component Tag in a Tag Library
    Descriptor](jsf-custom009.htm#BNAWN)

  - [Using a Custom Component](jsf-custom010.htm#BNATT)

  - [Creating and Using a Custom Converter](jsf-custom011.htm#BNAUS)

  - [Creating and Using a Custom Validator](jsf-custom012.htm#BNAUW)

  - [Binding Component Values and Instances to Managed Bean
    Properties](jsf-custom013.htm#BNATG)

  - [Binding Converters, Listeners, and Validators to Managed Bean
    Properties](jsf-custom014.htm#BNATM)

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
<td><a href="jsf-advanced-cc004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
