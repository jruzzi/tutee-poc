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
<td><a href="usingexamples001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="usingexamples003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 2.2 Starting and Stopping GlassFish Server

You can start and stop GlassFish Server using either NetBeans IDE or the
command line.

## 2.2.1 To Start GlassFish Server Using NetBeans IDE

1.  Click the Services tab.

2.  Expand Servers.

3.  Right-click the GlassFish Server instance and select Start.

## 2.2.2 To Stop GlassFish Server Using NetBeans IDE

To stop GlassFish Server using NetBeans IDE, right-click the GlassFish
Server instance and select Stop.

## 2.2.3 To Start GlassFish Server Using the Command Line

To start GlassFish Server from the command line, open a terminal window
or command prompt and execute the following:

``` oac_no_warn
asadmin start-domain --verbose
```

A domain is a set of one or more GlassFish Server instances managed by
one administration server. The following elements are associated with a
domain:

  - The GlassFish Server port number: The default is 8080.

  - The administration server's port number: The default is 4848.

  - An administration user name and password: The default user name is
    `admin`, and by default no password is required.

You specify these values when you install GlassFish Server. The examples
in this tutorial assume that you chose the default ports as well as the
default user name and lack of password.

With no arguments, the `start-domain` command initiates the default
domain, which is `domain1`. The `--verbose` flag causes all logging and
debugging output to appear on the terminal window or command prompt. The
output also goes into the server log, which is located in
domain-dir`/logs/server.log`.

## 2.2.4 To Stop GlassFish Server Using the Command Line

To stop GlassFish Server, open a terminal window or command prompt and
execute:

``` oac_no_warn
asadmin stop-domain domain1
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
<td><a href="usingexamples001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="usingexamples003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
