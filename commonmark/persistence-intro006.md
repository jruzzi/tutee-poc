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
<td><a href="persistence-intro005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-intro007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 37.6 Database Schema Creation

The persistence provider can be configured to automatically create the
database tables, load data into the tables, and remove the tables during
application deployment using standard properties in the application's
deployment descriptor. These tasks are typically used during the
development phase of a release, not against a production database.

The following is an example of a `persistence.xml` deployment descriptor
that specifies that the provider should drop all database artifacts
using a provided script, create the artifacts with a provided script,
and load data from a provided script when the application is deployed:

``` oac_no_warn
<?xml version="1.0" encoding="UTF-8"?>
<persistence version="2.1" xmlns="http://xmlns.jcp.org/xml/ns/persistence"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence
 http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1.xsd">
  <persistence-unit name="examplePU" transaction-type="JTA">
    <jta-data-source>java:global/ExampleDataSource</jta-data-source>
    <properties>
        <property name="javax.persistence.schema-generation.database.action"
                  value="drop-and-create"/>
        <property name="javax.persistence.schema-generation.create-source"
                  value="script"/>
        <property name="javax.persistence.schema-generation.create-script-source"
                  value="META-INF/sql/create.sql" />
        <property name="javax.persistence.sql-load-script-source"
                  value="META-INF/sql/data.sql" />
        <property name="javax.persistence.schema-generation.drop-source"
                  value="script" />
        <property name="javax.persistence.schema-generation.drop-script-source"
                  value="META-INF/sql/drop.sql" />
    </properties>
  </persistence-unit>
</persistence>
```

## 37.6.1 Configuring an Application to Create or Drop Database Tables

The `javax.persistence.schema-generation.database.action` property is
used to specify the action taken by the persistence provider when an
application is deployed. If the property is not set, the persistence
provider will not create or drop any database artifacts.

Table 37-3 Schema Creation Actions

<table style="width:31%;">
<colgroup>
<col width="31%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Setting</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">none</code></p></td>
<td><p>No schema creation or deletion will take place.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">create</code></p></td>
<td><p>The provider will create the database artifacts on application deployment. The artifacts will remain unchanged after application redeployment.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">drop-and-create</code></p></td>
<td><p>Any artifacts in the database will be deleted, and the provider will create the database artifacts on deployment.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">drop</code></p></td>
<td><p>Any artifacts in the database will be deleted on application deployment.</p></td>
</tr>
</tbody>
</table>

  

In this example, the persistence provider will delete any remaining
database artifacts and then create the artifacts when the application is
deployed:

``` oac_no_warn
<property name="javax.persistence.schema-generation.database.action"
           value="drop-and-create"/>
```

By default, the object/relational metadata in the persistence unit is
used to create the database artifacts. You may also supply scripts used
by the provider to create and delete the database artifacts. The
`javax.persistence.schema-generation.create-source` and
`javax.persistence.schema-generation.drop-source` properties control how
the provider will create or delete the database artifacts.

Table 37-4 Settings for Create and Delete Source Properties

<table style="width:31%;">
<colgroup>
<col width="31%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Setting</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">metadata</code></p></td>
<td><p>Use the object/relational metadata in the application to create or delete the database artifacts.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">script</code></p></td>
<td><p>Use a provided script for creating or deleting the database artifacts.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">metadata-then-script</code></p></td>
<td><p>Use a combination of object/relational metadata, then a user-provided script to create or delete the database artifacts.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">script-then-metadata</code></p></td>
<td><p>Use a combination of a user-provided script, then the object/relational metadata to create and delete the database artifacts.</p></td>
</tr>
</tbody>
</table>

  

In this example, the persistence provider will use a script packaged
within the application to create the database artifacts:

``` oac_no_warn
<property name="javax.persistence.schema-generation.create-source"
           value="script"/>
```

If you specify a script in `create-source` or `drop-source`, specify the
location of the script using the
`javax.persistence.schema-generation.create-script-source` or
`javax.persistence.schema-generation.drop-script-source` property. The
location of the script is relative to the root of the persistence
unit:

``` oac_no_warn
<property name="javax.persistence.schema-generation.create-script-source"
           value="META-INF/sql/create.sql" />
```

In the above example, the `create-script-source` is set to a SQL file
called `create.sql` in the `META-INF/sql` directory relative to root of
the persistence unit.

## 37.6.2 Loading Data Using SQL Scripts

If you want to populate the database tables with data before the
application loads, specify the location of a load script in the
`javax.persistence.sql-load-script-source property`. The location
specified in this property is relative to the root of the persistence
unit.

In this example, the load script is a file called `data.sql` in the
`META-INF/sql` directory relative to the root of the persistence unit:

``` oac_no_warn
<property name="javax.persistence.sql-load-script-source"
          value="META-INF/sql/data.sql" />
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
<td><a href="persistence-intro005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-intro007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
