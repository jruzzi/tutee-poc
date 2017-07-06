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
<td><a href="resources002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="resources004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 52.3 Common Client Interface

This section explains how components use the Connector Architecture
Common Client Interface (CCI) API and a resource adapter to access data
from an EIS. The CCI API defines a set of interfaces and classes whose
methods allow a client to perform typical data access operations. The
CCI interfaces and classes are as follows.

  - `ConnectionFactory`: Provides an application component with a
    `Connection` instance to an EIS.

  - `Connection`: Represents the connection to the underlying EIS.

  - `ConnectionSpec`: Provides a means for an application component to
    pass connection-request-specific properties to the
    `ConnectionFactory` when making a connection request.

  - `Interaction`: Provides a means for an application component to
    execute EIS functions, such as database stored procedures.

  - `InteractionSpec`: Holds properties pertaining to an application
    component's interaction with an EIS.

  - `Record`: The superinterface for the various kinds of record
    instances. Record instances can be `MappedRecord`, `IndexedRecord`,
    or `ResultSet` instances, all of which inherit from the `Record`
    interface.

  - `RecordFactory`: Provides an application component with a `Record`
    instance.

  - `IndexedRecord`: Represents an ordered collection of `Record`
    instances based on the `java.util.List` interface.

A client or application component that uses the CCI to interact with an
underlying EIS does so in a prescribed manner. The component must
establish a connection to the EIS's resource manager, and it does so
using the `ConnectionFactory`. The `Connection` object represents the
connection to the EIS and is used for subsequent interactions with the
EIS.

The component performs its interactions with the EIS, such as accessing
data from a specific table, using an `Interaction` object. The
application component defines the Interaction object by using an
`InteractionSpec` object. When it reads data from the EIS, such as from
database tables, or writes to those tables, the application component
does so by using a particular type of `Record` instance: a
`MappedRecord`, an `IndexedRecord`, or a `ResultSet` instance.

Note, too, that a client application that relies on a CCI resource
adapter is very much like any other Java EE client that uses enterprise
bean methods.

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
<td><a href="resources002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="resources004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
