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
<td><a href="jms-examples009.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partsecurity.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 46.10 Using NetBeans IDE to Create JMS Resources

When you write your own JMS applications, you will need to create
resources for them. This section explains how to use NetBeans IDE to
create `src/main/setup/glassfish-resources.xml` files similar to those
used in the examples in this chapter. It also explains how to use
NetBeans IDE to delete the resources.

You can also create, list, and delete JMS resources using the
Administration Console or the `asadmin create-jms-resource`, `asadmin
list-jms-resources`, and `asadmin delete-jms-resources` commands. For
information, consult the GlassFish Server documentation or enter
`asadmin help` command-name.

The following topics are addressed here:

  - [Section 46.10.1, "To Create JMS Resources Using NetBeans
    IDE"](#CHDFIJBJ)

  - [Section 46.10.2, "To Delete JMS Resources Using NetBeans
    IDE"](#CHDCFADI)

## 46.10.1 To Create JMS Resources Using NetBeans IDE

Follow these steps to create a JMS resource in GlassFish Server using
NetBeans IDE. Repeat these steps for each resource you need.

1.  Right-click the project for which you want to create resources and
    select New, then select Other.

2.  In the New File wizard, under Categories, select GlassFish.

3.  Under File Types, select JMS Resource.

4.  On the General Attributes - JMS Resource page, in the JNDI Name
    field, enter the name of the resource.
    
    By convention, JMS resource names begin with `jms/`.

5.  Select the option for the resource type.
    
    Normally, this is either `javax.jms.Queue`, `javax.jms.Topic`, or
    `javax.jms.ConnectionFactory`.

6.  Click Next.

7.  On the JMS Properties page, for a queue or topic, enter a name for a
    physical queue in the Value field for the Name property.
    
    You can enter any value for this required field.
    
    Connection factories have no required properties. In a few
    situations, you may need to specify a property.

8.  Click Finish.
    
    A file named `glassfish-resources.xml` is created in your Maven
    project, in a directory named `src/main/setup/`. In the Projects
    tab, you can find it under the Other Sources node. You will need to
    run the `asadmin add-resources` command to create the resources in
    GlassFish Server.

## 46.10.2 To Delete JMS Resources Using NetBeans IDE

1.  In the Services tab, expand the Servers node, then expand the
    GlassFish Server node.

2.  Expand the Resources node, then expand the Connector Resources node.

3.  Expand the Admin Object Resources node.

4.  Right-click any destination you want to remove and select
    Unregister.

5.  Expand the Connector Connection Pools node.

6.  Right-click the connection pool that corresponds to the connection
    factory you removed and select Unregister.
    
    When you remove a connector connection pool, the associated
    connector resource is also deleted. This action removes the
    connection factory.

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
<td><a href="jms-examples009.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partsecurity.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
