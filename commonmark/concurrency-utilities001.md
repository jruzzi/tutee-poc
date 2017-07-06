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
<td><a href="concurrency-utilities.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="concurrency-utilities002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 56.1 Concurrency Basics

Concurrency is the concept of executing two or more tasks at the same
time (in parallel). Tasks may include methods (functions), parts of a
program, or even other programs. With current computer architectures,
support for multiple cores and multiple processors in a single CPU is
very common.

The Java Platform has always offered support for concurrent programming,
which was the basis for implementing many of the services offered by
Java EE containers. At Java SE 5, additional high-level API support for
concurrency was provided by the `java.util.concurrent` package.

Prior to Java EE 7, there were no specific APIs that allowed enterprise
developers to use concurrency utilities in a safely standard manner. The
Java EE web and EJB containers instantiate objects using
container-managed thread pools. Therefore, using Java SE concurrent APIs
to instantiate `Thread` objects was strongly discouraged. If a developer
creates a new (non-managed) `Thread` object, the container could not
guarantee that other Java EE platform services (for example,
transactions and security) would be part of this `Thread`.

## 56.1.1 Threads and Processes

The two main concurrency concepts are processes and threads.

Processes are primarily associated with applications running on the
operating system (OS). A process has specific runtime resources to
interact with the underlying OS and allocate other resources, such as
its own memory, just as the JVM process does. A JVM is in fact a
process.

The Java programming language and platform are primarily concerned with
threads.

Threads share some features with processes, since both consume resources
from the OS or the execution environment. But threads are easier to
create and consume many fewer resources than a process.

Because threads are so lightweight, any modern CPU that has a couple of
cores and a few gigabytes of RAM can handle thousands of threads in a
single JVM process. The precise number of threads will depend on the
combined output of the CPU, OS, and RAM available, as well as on correct
configuration (tuning) of the JVM.

Although concurrent programming solves many problems and can improve
performance for most applications, there are a number of situations
where multiple execution lines (threads or processes) can cause major
problems. These situations include the following:

  - Deadlocks

  - Thread starvation

  - Concurrent accessing of shared resources

  - Situations when the program generates incorrect data

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
<td><a href="concurrency-utilities.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="concurrency-utilities002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
