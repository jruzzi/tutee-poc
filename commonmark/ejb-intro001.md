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
<td><a href="ejb-intro.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-intro002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 32.1 What Is an Enterprise Bean?

Written in the Java programming language, an enterprise bean is a
server-side component that encapsulates the business logic of an
application. The business logic is the code that fulfills the purpose of
the application. In an inventory control application, for example, the
enterprise beans might implement the business logic in methods called
`checkInventoryLevel` and `orderProduct`. By invoking these methods,
clients can access the inventory services provided by the application.

The following topics are addressed here:

  - [Section 32.1.1, "Benefits of Enterprise Beans"](#GIPLK)

  - [Section 32.1.2, "When to Use Enterprise Beans"](#GIPKN)

  - [Section 32.1.3, "Types of Enterprise Beans"](#GIPNM)

## 32.1.1 Benefits of Enterprise Beans

For several reasons, enterprise beans simplify the development of large,
distributed applications. First, because the EJB container provides
system-level services to enterprise beans, the bean developer can
concentrate on solving business problems. The EJB container, rather than
the bean developer, is responsible for system-level services, such as
transaction management and security authorization.

Second, because the beans rather than the clients contain the
application's business logic, the client developer can focus on the
presentation of the client. The client developer does not have to code
the routines that implement business rules or access databases. As a
result, the clients are thinner, a benefit that is particularly
important for clients that run on small devices.

Third, because enterprise beans are portable components, the application
assembler can build new applications from existing beans. Provided that
they use the standard APIs, these applications can run on any compliant
Java EE server.

## 32.1.2 When to Use Enterprise Beans

You should consider using enterprise beans if your application has any
of the following requirements.

  - The application must be scalable. To accommodate a growing number of
    users, you may need to distribute an application's components across
    multiple machines. Not only can the enterprise beans of an
    application run on different machines, but also their location will
    remain transparent to the clients.

  - Transactions must ensure data integrity. Enterprise beans support
    transactions, the mechanisms that manage the concurrent access of
    shared objects.

  - The application will have a variety of clients. With only a few
    lines of code, remote clients can easily locate enterprise beans.
    These clients can be thin, various, and numerous.

## 32.1.3 Types of Enterprise Beans

[Table 32-1](#GIPLZ) summarizes the two types of enterprise beans. The
following sections discuss each type in more detail.

Table 32-1 Enterprise Bean Types

<table style="width:30%;">
<colgroup>
<col width="30%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Enterprise Bean Type</th>
<th>Purpose</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Session</p></td>
<td><p>Performs a task for a client; optionally, may implement a web service</p></td>
</tr>
<tr class="even">
<td><p>Message-driven</p></td>
<td><p>Acts as a listener for a particular messaging type, such as the Java Message Service API</p></td>
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
<td><a href="ejb-intro.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-intro002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
