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
<td><a href="interceptors003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="batch-processing001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 55 Batch Processing

This chapter describes Batch Applications for the Java Platform (JSR
352), which provides support for defining, implementing, and running
batch jobs. Batch jobs are tasks that can be executed without user
interaction. The batch framework is composed of a job specification
language based on XML, a Java API, and a batch runtime.

The following topics are addressed here:

  - [Introduction to Batch Processing](batch-processing001.htm#BCGJDEEH)

  - [Batch Processing in Java EE](batch-processing002.htm#BCGGIBHA)

  - [Simple Use Case](batch-processing003.htm#BCGHBJIG)

  - [Using the Job Specification
    Language](batch-processing004.htm#BCGDDBBG)

  - [Creating Batch Artifacts](batch-processing005.htm#BCGHDHGH)

  - [Submitting Jobs to the Batch
    Runtime](batch-processing006.htm#BCGCAHCB)

  - [Packaging Batch Applications](batch-processing007.htm#BCGBBGJI)

  - [The webserverlog Example
    Application](batch-processing008.htm#BCGJHEHJ)

  - [The phonebilling Example
    Application](batch-processing009.htm#BCGFCACD)

  - [Further Information about Batch
    Processing](batch-processing010.htm#BCGHCHAJ)

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
<td><a href="interceptors003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="batch-processing001.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
