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
<td><a href="concurrency-utilities001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="concurrency-utilities003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 56.2 Main Components of the Concurrency Utilities

Concurrent resources are managed objects that provide concurrency
capabilities to Java EE applications. In GlassFish Server, you configure
concurrent resources and then make them available for use by application
components such as servlets and enterprise beans. Concurrent resources
are accessed through JNDI lookup or resource injection.

The primary components of the concurrency utilities are as follows.

  - `ManagedExecutorService`: A managed executor service is used by
    applications to execute submitted tasks asynchronously. Tasks are
    executed on threads that are started and managed by the container.
    The context of the container is propagated to the thread executing
    the task.
    
    For example, by using an `ManagedExecutorService.submit()` call, a
    task, such as the GenerateReportTask, could be submitted to execute
    at a later time and then, by using the `Future` object callback,
    retrieve the result when it becomes available.

  - `ManagedScheduledExecutorService`: A managed scheduled executor
    service is used by applications to execute submitted tasks
    asynchronously at specific times. Tasks are executed on threads that
    are started and managed by the container. The context of the
    container is propagated to the thread executing the task. The API
    provides the scheduling functionality that allows users to set a
    specific date/time for the Task execution programmatically in the
    application.

  - `ContextService`: A context service is used to create dynamic proxy
    objects that capture the context of a container and enable
    applications to run within that context at a later time or be
    submitted to a Managed Executor Service. The context of the
    container is propagated to the thread executing the task.

  - `ManagedThreadFactory`: A managed thread factory is used by
    applications to create managed threads. The threads are started and
    managed by the container. The context of the container is propagated
    to the thread executing the task. This object can also be used to
    provide custom factories for specific use cases (with custom
    Threads) and, for example, set specific/proprietary properties to
    these objects.

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
<td><a href="concurrency-utilities001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="concurrency-utilities003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
