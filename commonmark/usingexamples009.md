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
<td><a href="usingexamples008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partplatform.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 2.9 Debugging Java EE Applications

This section explains how to determine what is causing an error in your
application deployment or execution.

## 2.9.1 Using the Server Log

One way to debug applications is to look at the server log in
domain-dir`/logs/server.log`. The log contains output from GlassFish
Server and your applications. You can log messages from any Java class
in your application with `System.out.println` and the Java Logging APIs
(documented at
`http://docs.oracle.com/javase/7/docs/technotes/guides/logging/index.html`)
and from web components with the `ServletContext.log` method.

If you use NetBeans IDE, logging output appears in the Output window as
well as the server log.

If you start GlassFish Server with the `--verbose` flag, all logging and
debugging output will appear on the terminal window or command prompt
and the server log. If you start GlassFish Server in the background,
debugging information is available only in the log. You can view the
server log with a text editor or with the Administration Console log
viewer.

### 2.9.1.1 To Use the Administration Console Log Viewer

1.  Select the GlassFish Server node.

2.  Click View Log Files.
    
    The log viewer opens and displays the last 40 entries.

3.  To display other entries, follow these steps.
    
    1.  Click Modify Search.
    
    2.  Specify any constraints on the entries you want to see.
    
    3.  Click Search at the top of the log viewer.

## 2.9.2 Using a Debugger

GlassFish Server supports the Java Platform Debugger Architecture
(JPDA). With JPDA, you can configure GlassFish Server to communicate
debugging information using a socket.

### 2.9.2.1 To Debug an Application Using a Debugger

1.  Follow these steps to enable debugging in GlassFish Server using the
    Administration Console:
    
    1.  Expand the Configurations node, then expand the server-config
        node.
    
    2.  Select the JVM Settings node. The default debug options are set
        to:
        
        ``` oac_no_warn
        -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=9009
        ```
        
        As you can see, the default debugger socket port is 9009. You
        can change it to a port not in use by GlassFish Server or
        another service.
    
    3.  Select the Debug Enabled check box.
    
    4.  Click Save.

2.  Stop GlassFish Server and then restart it.

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
<td><a href="usingexamples008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partplatform.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
