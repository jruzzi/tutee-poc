++++
<table cellspacing="0" cellpadding="0" width="100%">
<tr>
<td align="left" valign="top"><b>Java Platform, Enterprise Edition The Java EE Tutorial</b><br />
<b>Release 7 Java Platform, Enterprise Edition</b><br />
E39031-02</td>
<td valign="bottom" align="right">
<table cellspacing="0" cellpadding="0" width="225">
<tr>
<td>&nbsp;</td>
<td align="center" valign="top"><a href="toc.md"><img src="img/toc.gif" alt="Go To Table Of Contents" /><br />
<span class="icon">Contents</span></a></td>
</tr>
</table>
</td>
</tr>
</table>
<hr />
<table cellspacing="0" cellpadding="0" width="100">
<tr>
<td align="center"><a href="title.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a>&nbsp;</td>
<td align="center"><a href="partintro.md"><img src="img/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td>&nbsp;</td>
</tr>
</table>
++++

[[JEETT00063]]
[[GEXAF]]

[[preface]]
Preface
-------

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

* link:#CIACGIBD[Audience]
* link:#CIAHFICG[Documentation Accessibility]
* link:#BNAAC[Before You Read This Book]
* link:#GIPRL[Related Documentation]
* link:#GKVTF[Conventions]
* link:#GFIRK[Default Paths and File Names]

[[JEETT1336]]

[[CIACGIBD]]
[[audience]]
Audience
~~~~~~~~

This tutorial is intended for programmers interested in developing and
deploying Java EE 7 applications. It covers the technologies comprising
the Java EE platform and describes how to develop Java EE components and
deploy them on the Java EE Software Development Kit (SDK).

[[JEETT1337]]
[[CIAHFICG]]

[[documentation-accessibility]]
Documentation Accessibility
~~~~~~~~~~~~~~~~~~~~~~~~~~~

For information about Oracle's commitment to accessibility, visit the
Oracle Accessibility Program website at
`http://www.oracle.com/pls/topic/lookup?ctx=acc&id=docacc`.

[[sthref2]]

Access to Oracle Support

Oracle customers that have purchased support have access to electronic
support through My Oracle Support. For information, visit
`http://www.oracle.com/pls/topic/lookup?ctx=acc&id=info` or visit
`http://www.oracle.com/pls/topic/lookup?ctx=acc&id=trs` if you are
hearing impaired.

[[JEETT00301]]
[[BNAAC]]

[[before-you-read-this-book]]
Before You Read This Book
~~~~~~~~~~~~~~~~~~~~~~~~~

Before proceeding with this tutorial, you should have a good knowledge
of the Java programming language. A good way to get to that point is to
work through the Java Tutorials
(`http://docs.oracle.com/javase/tutorial/index.md`).

[[JEETT00302]]
[[GIPRL]]

[[related-documentation]]
Related Documentation
~~~~~~~~~~~~~~~~~~~~~

The GlassFish Server documentation set describes deployment planning and
system installation. To obtain documentation for GlassFish Server Open
Source Edition, go to `https://glassfish.java.net/docs/`.

The Java EE 7 API specification can be viewed at
`http://docs.oracle.com/javaee/7/api/` and is also provided in the Java
EE 7 SDK.

Additionally, the Java EE Specifications at
`http://www.oracle.com/technetwork/java/javaee/tech/index.md` might be
useful.

For information about creating enterprise applications in the NetBeans
Integrated Development Environment (IDE), see
`https://netbeans.org/kb/`.

For information about the Java DB database for use with GlassFish
Server, see
`http://www.oracle.com/technetwork/java/javadb/overview/index.md`.

The GlassFish Samples project is a collection of sample applications
that demonstrate a broad range of Java EE technologies. The GlassFish
Samples are bundled with the Java EE Software Development Kit (SDK) and
are also available from the GlassFish Samples project page at
`https://glassfish-samples.java.net/`.

[[JEETT00303]]
[[GKVTF]]

[[conventions]]
Conventions
~~~~~~~~~~~

The following table describes the typographic conventions that are used
in this book.

[width="55%", options="header",]
|=======================================================================
|Convention |Meaning |Example
|Boldface |Boldface type indicates graphical user interface elements
associated with an action or terms defined in text. a|
From the File menu, choose Open Project.

A cache is a copy that is stored locally.

|`Monospace` |Monospace type indicates the names of files and
directories, commands within a paragraph, URLs, code in examples, text
that appears on the screen, or text that you enter. a|
Edit your `.login` file.

Use `ls` `-a` to list all files.

`machine_name% you have mail.`

|Italic |Italic type indicates book titles, emphasis, or placeholder
variables for which you supply particular values. a|
Read Chapter 6 in the User's Guide.

Do not save the file.

The command to remove a file is `rm` filename.

|=======================================================================



[[JEETT00304]]
[[GFIRK]]

[[default-paths-and-file-names]]
Default Paths and File Names
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following table describes the default paths and file names that are
used in this book.

[width="50%",options="header",]
|=======================================================================
|Placeholder |Description |Default Value
|as-install |Represents the base installation directory for GlassFish
Server or the SDK of which GlassFish Server is a part. a|
Installations on the Solaris operating system, Linux operating system,
and Mac operating system:

user's-home-directory`/glassfish4/glassfish`

Windows, all installations:

SystemDrive`:\glassfish4\glassfish`

|as-install-parent |Represents the parent of the base installation
directory for GlassFish Server. a|
Installations on the Solaris operating system, Linux operating system,
and Mac operating system:

user's-home-directory`/glassfish4`

Windows, all installations:

SystemDrive`:\glassfish4`

|tut-install |Represents the base installation directory for the Java EE
Tutorial after you install GlassFish Server or the SDK and run the
Update Tool. |as-install-parent`/docs/javaee-tutorial`

|domain-dir |Represents the directory in which a domain's configuration
is stored. |as-install`/domains/domain1`
|=======================================================================

 
++++
<hr />
<table cellspacing="0" cellpadding="0" width="100%">
<col width="33%" />
<col width="*" />
<col width="33%" />
<tr>
<td valign="bottom">
<table cellspacing="0" cellpadding="0" width="100">
<col width="*" />
<col width="48%" />
<col width="48%" />
<tr>
<td>&nbsp;</td>
<td align="center"><a href="title.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a>&nbsp;</td>
<td align="center"><a href="partintro.md"><img src="img/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
</tr>
</table>
</td>
<td><img src="img/oracle.gif" alt="Oracle Logo" /> <a href="img/cpyr.md"><br />
<span>Copyright&nbsp;&copy;&nbsp;2014,&nbsp;Oracle&nbsp;and/or&nbsp;its&nbsp;affiliates.&nbsp;All&nbsp;rights&nbsp;reserved.</a><br>
ORACLE&nbsp;CONFIDENTIAL.&nbsp;For&nbsp;authorized&nbsp;use&nbsp;only.&nbsp;Do&nbsp;not&nbsp;distribute&nbsp;to&nbsp;third&nbsp;parties.</span></td>
<td valign="bottom" align="right">
<table cellspacing="0" cellpadding="0" width="225">
<tr>
<td>&nbsp;</td>
<td align="center" valign="top"><a href="toc.md"><img src="img/toc.gif" alt="Go To Table Of Contents" /><br />
<span>Contents</span></a></td>
</tr>
</table>
</td>
</tr>
</table>
<p align="center"></p>
++++