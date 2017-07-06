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
<td><a href="persistence-entitygraphs001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-entitygraphs003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 43.2 Entity Graph Basics

You can create entity graphs statically by using annotations or a
deployment descriptor, or dynamically by using standard interfaces.

You can use an entity graph with the `EntityManager.find` method or as
part of a JPQL or Criteria API query by specifying the entity graph as a
hint to the operation or query.

Entity graphs have attributes that correspond to the fields that will be
eagerly fetched during a `find` or query operation. The primary key and
version fields of the entity class are always fetched and do not need to
be explicitly added to an entity graph.

## 43.2.1 The Default Entity Graph

By default, all fields in an entity are fetched lazily unless the
`fetch` attribute of the entity metadata is set to
`javax.persistence.FetchType.EAGER`. The default entity graph consists
of all the fields of an entity whose fields are set to be eagerly
fetched.

For example, the following `EmailMessage` entity specifies that some
fields will be fetched eagerly:

``` oac_no_warn
@Entity
public class EmailMessage implements Serializable {
    @Id
    String messageId;
    @Basic(fetch=EAGER)
    String subject;
    String body;
    @Basic(fetch=EAGER)
    String sender;
    @OneToMany(mappedBy="message", fetch=LAZY)
    Set<EmailAttachment> attachments;
    ...
}
```

The default entity graph for this entity would contain the `messageId`,
`subject`, and `sender` fields, but not the `body` or `attachments`
fields.

## 43.2.2 Using Entity Graphs in Persistence Operations

Entity graphs are used by creating an instance of the
`javax.persistence.EntityGraph` interface by calling either
`EntityManager.getEntityGraph` for named entity graphs or
`EntityManager.createEntityGraph` for creating dynamic entity graphs.

A named entity graph is an entity graph specified by the
`@NamedEntityGraph` annotation applied to entity classes, or the
`named-entity-graph` element in the application's deployment
descriptors. Named entity graphs defined within the deployment
descriptor override any annotation-based entity graphs with the same
name.

The created entity graph can be either a fetch graph or a load graph.

The following topics are addressed here:

  - [Section 43.2.2.1, "Fetch Graphs"](#BABGEFCG)

  - [Section 43.2.2.2, "Load Graphs"](#BABHJBHG)

### 43.2.2.1 Fetch Graphs

To specify a fetch graph, set the `javax.persistence.fetchgraph`
property when you execute an `EntityManager.find` or query operation. A
fetch graph consists of only the fields explicitly specified in the
`EntityGraph` instance, and ignores the default entity graph settings.

In the following example, the default entity graph is ignored, and only
the `body` field is included in the dynamically created fetch graph:

``` oac_no_warn
EntityGraph<EmailMessage> eg = em.createEntityGraph(EmailMessage.class);
eg.addAttributeNodes("body");
...
Properties props = new Properties();
props.put("javax.persistence.fetchgraph", eg);
EmailMessage message = em.find(EmailMessage.class, id, props);
```

### 43.2.2.2 Load Graphs

To specify a load graph, set the `javax.persistence.loadgraph` property
when you execute an `EntityManager.find` or query operation. A load
graph consists of the fields explicitly specified in the `EntityGraph`
instance plus any fields in the default entity graph.

In the following example, the dynamically created load graph contains
all the fields in the default entity graph plus the `body` field:

``` oac_no_warn
EntityGraph<EmailMessage> eg = em.createEntityGraph(EmailMessage.class);
eg.addAttributeNodes("body");
...
Properties props = new Properties();
props.put("javax.persistence.loadgraph", eg);
EmailMessage message = em.find(EmailMessage.class, id, props);
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
<td><a href="persistence-entitygraphs001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-entitygraphs003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
