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
<td><a href="toc.md"><img src="img/toc.gif" alt="Go To Table Of Contents" /><br />
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
<td><a href="title.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partintro.md"><img src="img/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>



# Preface

This tutorial is a guide to developing enterprise applications for the
Java Platform, Enterprise Edition 7 (Java EE 7), using GlassFish Server
Open Source Edition.

GlassFish Server Open Source Edition is the leading open-source and
open-community platform for building and deploying next-generation
applications and services. GlassFish Server Open Source Edition,
developed by the GlassFish project open-source community at
`https://glassfish.java.net/`, is the first compatible implementation of
the Java EE 7 platform specification. This lightweight, flexible, and
open-source application server enables organizations not only to
leverage the new capabilities introduced within the Java EE 7
specification, but also to add to their existing capabilities through a
faster and more streamlined development and deployment cycle. GlassFish
Server Open Source Edition is hereafter referred to as GlassFish Server.

The following topics are addressed here:

  - [Audience](#CIACGIBD)

  - [Documentation Accessibility](#CIAHFICG)

  - [Before You Read This Book](#BNAAC)

  - [Related Documentation](#GIPRL)

  - [Conventions](#GKVTF)

  - [Default Paths and File Names](#GFIRK)

## Audience

This tutorial is intended for programmers interested in developing and
deploying Java EE 7 applications. It covers the technologies comprising
the Java EE platform and describes how to develop Java EE components and
deploy them on the Java EE Software Development Kit (SDK).

## Documentation Accessibility

For information about Oracle's commitment to accessibility, visit the
Oracle Accessibility Program website at
`http://www.oracle.com/pls/topic/lookup?ctx=acc&id=docacc`.

Access to Oracle Support

Oracle customers that have purchased support have access to electronic
support through My Oracle Support. For information, visit
`http://www.oracle.com/pls/topic/lookup?ctx=acc&id=info` or visit
`http://www.oracle.com/pls/topic/lookup?ctx=acc&id=trs` if you are
hearing impaired.

## Before You Read This Book

Before proceeding with this tutorial, you should have a good knowledge
of the Java programming language. A good way to get to that point is to
work through the Java Tutorials
(`http://docs.oracle.com/javase/tutorial/index.mdl`).

## Related Documentation

The GlassFish Server documentation set describes deployment planning and
system installation. To obtain documentation for GlassFish Server Open
Source Edition, go to `https://glassfish.java.net/docs/`.

The Java EE 7 API specification can be viewed at
`http://docs.oracle.com/javaee/7/api/` and is also provided in the Java
EE 7 SDK.

Additionally, the Java EE Specifications at
`http://www.oracle.com/technetwork/java/javaee/tech/index.mdl` might be
useful.

For information about creating enterprise applications in the NetBeans
Integrated Development Environment (IDE), see
`https://netbeans.org/kb/`.

For information about the Java DB database for use with GlassFish
Server, see
`http://www.oracle.com/technetwork/java/javadb/overview/index.mdl`.

The GlassFish Samples project is a collection of sample applications
that demonstrate a broad range of Java EE technologies. The GlassFish
Samples are bundled with the Java EE Software Development Kit (SDK) and
are also available from the GlassFish Samples project page at
`https://glassfish-samples.java.net/`.

## Conventions

The following table describes the typographic conventions that are used
in this book.

<table style="width:55%;">
<colgroup>
<col width="15%" />
<col width="40%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Convention</th>
<th>Meaning</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span class="bold">Boldface</span></td>
<td>Boldface type indicates graphical user interface elements associated with an action or terms defined in text.</td>
<td>From the <span class="gui-object-action">File</span> menu, choose <span class="gui-object-action">Open Project</span>.
<p>A <span class="bold">cache</span> is a copy that is stored locally.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr">Monospace</code></td>
<td>Monospace type indicates the names of files and directories, commands within a paragraph, URLs, code in examples, text that appears on the screen, or text that you enter.</td>
<td>Edit your <code dir="ltr">.login</code> file.
<p>Use <code dir="ltr">ls</code> <code dir="ltr">-a</code> to list all files.</p>
<p><code dir="ltr">machine_name% you have mail.</code></p></td>
</tr>
<tr class="odd">
<td>Italic</td>
<td>Italic type indicates book titles, emphasis, or placeholder variables for which you supply particular values.</td>
<td>Read Chapter 6 in the <span class="italic">User's Guide</span>.
<p>Do <span class="italic">not</span> save the file.</p>
<p>The command to remove a file is <code dir="ltr">rm</code> <span class="variable">filename</span>.</p></td>
</tr>
</tbody>
</table>

  

## Default Paths and File Names

The following table describes the default paths and file names that are
used in this book.

<table style="width:51%;">
<colgroup>
<col width="19%" />
<col width="32%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Placeholder</th>
<th>Description</th>
<th>Default Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span class="variable">as-install</span></td>
<td>Represents the base installation directory for GlassFish Server or the SDK of which GlassFish Server is a part.</td>
<td>Installations on the Solaris operating system, Linux operating system, and Mac operating system:
<p><span class="variable">user's-home-directory</span><code dir="ltr">/glassfish4/glassfish</code></p>
<p>Windows, all installations:</p>
<p><span class="variable">SystemDrive</span><code dir="ltr">:\glassfish4\glassfish</code></p></td>
</tr>
<tr class="even">
<td><span class="variable">as-install-parent</span></td>
<td>Represents the parent of the base installation directory for GlassFish Server.</td>
<td>Installations on the Solaris operating system, Linux operating system, and Mac operating system:
<p><span class="variable">user's-home-directory</span><code dir="ltr">/glassfish4</code></p>
<p>Windows, all installations:</p>
<p><span class="variable">SystemDrive</span><code dir="ltr">:\glassfish4</code></p></td>
</tr>
<tr class="odd">
<td><span class="variable">tut-install</span></td>
<td>Represents the base installation directory for the <span class="italic">Java EE Tutorial</span> after you install GlassFish Server or the SDK and run the Update Tool.</td>
<td><span class="variable">as-install-parent</span><code dir="ltr">/docs/javaee-tutorial</code></td>
</tr>
<tr class="even">
<td><span class="variable">domain-dir</span></td>
<td>Represents the directory in which a domain's configuration is stored.</td>
<td><span class="variable">as-install</span><code dir="ltr">/domains/domain1</code></td>
</tr>
</tbody>
</table>

  

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
<td><a href="title.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partintro.md"><img src="img/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
</tr>
</tbody>
</table></td>
<td><img src="img/oracle.gif" alt="Oracle Logo" class="copyrightlogo" /> <a href="img/cpyr.htm"><br />
<span class="copyrightlogo">Copyright © 2014, Oracle and/or its affiliates. All rights reserved.</span></a></td>
<td><table>
<tbody>
<tr class="odd">
<td> </td>
<td><a href="toc.md"><img src="img/toc.gif" alt="Go To Table Of Contents" /><br />
<span class="icon">Contents</span></a></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>


