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
<td><a href="persistence-entitygraphs002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-entitygraphs004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 43.3 Using Named Entity Graphs

Named entity graphs are created using annotations applied to entity
classes or the `named-entity-graph` element and its sub-elements in the
application's deployment descriptor. The persistence provider will scan
for all named entity graphs, defined in both annotations and in XML,
within an application. A named entity graph set using an annotation may
be overridden using `named-entity-graph`.

## 43.3.1 Applying Named Entity Graph Annotations to Entity Classes

The `javax.persistence.NamedEntityGraph` annotation defines a single
named entity graph and is applied at the class level. Multiple
`@NamedEntityGraph` annotations may be defined for a class by adding
them within a `javax.persistence.NamedEntityGraphs` class-level
annotation.

The `@NamedEntityGraph` annotation must be applied on the root of the
graph of entities. That is, if the `EntityManager.find` or query
operation has as its root entity the `EmailMessage` class, the named
entity graph used in the operation must be defined in the `EmailMessage`
class:

``` oac_no_warn
@NamedEntityGraph
@Entity
public class EmailMessage {
    @Id
    String messageId;
    String subject;
    String body;
    String sender;
}
```

In this example, the `EmailMessage` class has a `@NamedEntityGraph`
annotation to define a named entity graph that defaults to the name of
the class, `EmailMessage`. No fields are included in the
`@NamedEntityGraph` annotation as attribute nodes, and the fields are
not annotated with metadata to set the fetch type, so the only field
that will be eagerly fetched in either a load graph or fetch graph is
`messageId`.

The attributes of a named entity graph are the fields of the entity that
should be included in the entity graph. Add the fields to the entity
graph by specifying them in the `attributeNodes` element of
`@NamedEntityGraph` with a `javax.persistence.NamedAttributeNode`
annotation:

``` oac_no_warn
@NamedEntityGraph(name="emailEntityGraph", attributeNodes={
    @NamedAttributeNode("subject"),
    @NamedAttributeNode("sender")
})
@Entity
public class EmailMessage { ... }
```

In this example, the name of the named entity graph is
`emailEntityGraph` and includes the `subject` and `sender` fields.

Multiple `@NamedEntityGraph` definitions may be applied to a class by
grouping them within a `@NamedEntityGraphs` annotation.

In the following example, two entity graphs are defined on the
`EmailMessage` class. One is for a preview pane, which fetches only the
sender, subject, and body of the message. The other is for a full view
of the message, including any message attachments:

``` oac_no_warn
@NamedEntityGraphs({
    @NamedEntityGraph(name="previewEmailEntityGraph", attributeNodes={
        @NamedAttributeNode("subject"),
        @NamedAttributeNode("sender"),
        @NamedAttributeNode("body")
    }),
    @NamedEntityGraph(name="fullEmailEntityGraph", attributeNodes={
        @NamedAttributeNode("sender"),
        @NamedAttributeNode("subject"),
        @NamedAttributeNode("body"),
        @NamedAttributeNode("attachments")
    })
})
@Entity
public class EmailMessage { ... }
```

## 43.3.2 Obtaining EntityGraph Instances from Named Entity Graphs

Use the `EntityManager.getEntityGraph` method, passing in the named
entity graph name, to obtain `EntityGraph` instances for a named entity
graph:

``` oac_no_warn
EntityGraph<EmailMessage> eg = em.getEntityGraph("emailEntityGraph");
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
<td><a href="persistence-entitygraphs002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-entitygraphs004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
