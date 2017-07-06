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
<td><a href="resources001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="resources003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 52.2 Metadata Annotations

Java EE Connector Architecture provides a set of annotations to minimize
the need for deployment descriptors.

  - The `@Connector` annotation can be used by the resource adapter
    developer to specify that the JavaBeans component is a resource
    adapter JavaBeans component. This annotation is used for providing
    metadata about the capabilities of the resource adapter. Optionally,
    you can provide a JavaBeans component implementing the
    `ResourceAdapter` interface, as in the following example:
    
    ``` oac_no_warn
    @Connector(
        displayName = "TrafficResourceAdapter",
        vendorName = "Java EE Tutorial", 
        version = "7.0"
    )
    public class TrafficResourceAdapter implements ResourceAdapter, 
                                                   Serializable {
        ...
    }
    ```

  - The `@ConnectionDefinition` annotation defines a set of connection
    interfaces and classes pertaining to a particular connection type,
    as in the following example:
    
    ``` oac_no_warn
    @ConnectionDefinition(
        connectionFactory = ConnectionFactory.class,
        connectionFactoryImpl = TradeConnectionFactory.class,
        connection = Connection.class,
        connectionImpl = TradeConnection.class
    )
    public class TradeManagedConnectionFactory ... {
        ...
    }
    ```

  - The `@AdministeredObject` annotation designates a JavaBeans
    component as an administered object.

  - The `@Activation` annotation contains configuration information
    pertaining to inbound connectivity from an EIS instance, as in the
    following example:
    
    ``` oac_no_warn
    @Activation(
            messageListeners = { TrafficListener.class }
    )
    public class TrafficActivationSpec implements ActivationSpec, 
                                                  Serializable {
        ...
        @ConfigProperty()
        /* port to listen to requests from the EIS */
        private String port;
        ...
    }
    ```

  - The `@ConfigProperty` annotation can be used on JavaBeans components
    to provide additional configuration information that may be used by
    the deployer and resource adapter provider. The preceding example
    code shows several `@ConfigProperty` annotations.

  - The `@ConnectionFactoryDefinition` annotation is a resource
    definition annotation that is used to define a connector connection
    factory and register it in JNDI under the name specified in the
    mandatory `name` annotation element. The mandatory `interfaceName`
    annotation element specifies the fully qualified name of the
    connection factory interface class. The `transactionSupport`
    annotation element specifies the level of transaction support the
    connection factory needs to support. The `minPoolSize` and
    `maxPoolSize` annotation elements specify the minimum or maximum
    number of connections that should be allocated for a connection pool
    that backs this connection factory resource. Additional properties
    associated with the connection factory being defined can be
    specified through the `properties` element.
    
    Since repeated annotations are not allowed, the
    `@ConnectionFactoryDefinitions` annotation acts as a container for
    multiple connector connection factory definitions. The `value`
    annotation element contains the multiple connector connection
    factory definitions.

  - The `@AdministeredObjectDefinition` annotation is a resource
    definition annotation that is used to define an administered object
    and register it in JNDI under the name specified in the mandatory
    `name` annotation element. The mandatory fully qualified name of the
    administered object's class must be indicated by the `className`
    element. Additional properties that must be configured in the
    administered object can be specified through the `properties`
    element.
    
    Since repeated annotations are not allowed, the
    `@AdministeredObjectDefinitions` annotation acts as a container for
    multiple administered object definitions. The `value` annotation
    element contains the multiple administered object definitions.

The specification allows a resource adapter to be developed in
mixed-mode form, that is the ability for a resource adapter developer to
use both metadata annotations and deployment descriptors in
applications. An application assembler or deployer may use the
deployment descriptor to override the metadata annotations specified by
the resource adapter developer.

The deployment descriptor for a resource adapter, if present, is named
`ra.xml`. The `metadata-complete` attribute defines whether the
deployment descriptor for the resource adapter module is complete or
whether the class files available to the module and packaged with the
resource adapter need to be examined for annotations that specify
deployment information.

For the complete list of annotations and JavaBeans components provided
in the Java EE 7 platform, see the Java EE Connector Architecture 1.7
specification.

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
<td><a href="resources001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="resources003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
