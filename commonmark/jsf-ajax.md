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
<td><a href="jsf-develop003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 13 Using Ajax with JavaServer Faces Technology

This chapter describes using Ajax functionality in JavaServer Faces web
applications. Ajax is an acronym for Asynchronous JavaScript and XML, a
group of web technologies that enable creation of dynamic and highly
responsive web applications. Using Ajax, web applications can retrieve
content from the server without interfering with the display on the
client. In the Java EE 7 platform, JavaServer Faces technology provides
built-in support for Ajax.

The following topics are addressed here:

  - [Overview of Ajax](jsf-ajax001.htm#GKIGR)

  - [Using Ajax Functionality with JavaServer Faces
    Technology](jsf-ajax002.htm#GKINL)

  - [Using Ajax with Facelets](jsf-ajax003.htm#GKABR)

  - [Sending an Ajax Request](jsf-ajax004.htm#GKACE)

  - [Monitoring Events on the Client](jsf-ajax005.htm#GKDDF)

  - [Handling Errors](jsf-ajax006.htm#GKDCB)

  - [Receiving an Ajax Response](jsf-ajax007.htm#GKDBR)

  - [Ajax Request Lifecycle](jsf-ajax008.htm#GKUAR)

  - [Grouping of Components](jsf-ajax009.htm#GKHYH)

  - [Loading JavaScript as a Resource](jsf-ajax010.htm#GKAAM)

  - [The ajaxguessnumber Example Application](jsf-ajax011.htm#GKOKB)

  - [Further Information about Ajax in JavaServer Faces
    Technology](jsf-ajax012.htm#GKSDK)

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
<td><a href="jsf-develop003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
