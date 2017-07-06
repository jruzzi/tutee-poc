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
<td><a href="resource-creation001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="resource-creation003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 3.2 DataSource Objects and Connection Pools

To store, organize, and retrieve data, most applications use a
relational database. Java EE 7 components may access relational
databases through the JDBC API. For information on this API, see
`http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/`.

In the JDBC API, databases are accessed by using `DataSource` objects. A
`DataSource` has a set of properties that identify and describe the
real-world data source that it represents. These properties include such
information as the location of the database server, the name of the
database, the network protocol to use to communicate with the server,
and so on. In GlassFish Server, a data source is called a JDBC resource.

Applications access a data source by using a connection, and a
`DataSource` object can be thought of as a factory for connections to
the particular data source that the `DataSource` instance represents. In
a basic `DataSource` implementation, a call to the `getConnection`
method returns a connection object that is a physical connection to the
data source.

A `DataSource` object may be registered with a JNDI naming service. If
so, an application can use the JNDI API to access that `DataSource`
object, which can then be used to connect to the data source it
represents.

`DataSource` objects that implement connection pooling also produce a
connection to the particular data source that the `DataSource` class
represents. The connection object that the `getConnection` method
returns is a handle to a `PooledConnection` object rather than a
physical connection. An application uses the connection object in the
same way that it uses a connection. Connection pooling has no effect on
application code except that a pooled connection, like all connections,
should always be explicitly closed. When an application closes a
connection that is pooled, the connection is returned to a pool of
reusable connections. The next time `getConnection` is called, a handle
to one of these pooled connections will be returned if one is available.
Because connection pooling avoids creating a new physical connection
every time one is requested, applications can run significantly faster.

A JDBC connection pool is a group of reusable connections for a
particular database. Because creating each new physical connection is
time consuming, the server maintains a pool of available connections to
increase performance. When it requests a connection, an application
obtains one from the pool. When an application closes a connection, the
connection is returned to the pool.

Applications that use the Persistence API specify the `DataSource`
object they are using in the `jta-data-source` element of the
`persistence.xml` file:

``` oac_no_warn
<jta-data-source>jdbc/MyOrderDB</jta-data-source>
```

This is typically the only reference to a JDBC object for a persistence
unit. The application code does not refer to any JDBC objects.

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
<td><a href="resource-creation001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="resource-creation003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
