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
<td><a href="connectorexample001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="connectorexample003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 53.2 The trading Example

The `trading` example demonstrates how to implement and use a simple
outbound resource adapter that submits requests to a legacy EIS using a
TCP socket. The example demonstrates the scenario in [Figure
53-1](#CHDHADIG) and consists of the following modules:

  - `trading-eis`: A Java SE program that simulates a legacy EIS

  - `trading-rar`: The outbound resource adapter implementation

  - `trading-war`: A web application that uses the resource adapter

  - `trading-ear`: An enterprise archive that contains the resource
    adapter and the web application

Figure 53-1 The trading Example

![Description of Figure 53-1 follows](img/jeett_dt_054.png)  
[Description of "Figure 53-1 The trading
Example"](img_text/jeett_dt_054.htm)  
  

The `trading-eis` module is an auxiliary project that resembles a legacy
stock trading execution platform. It contains a Java SE program that
listens for trading requests in plain text on a TCP socket. The program
replies to trading requests with a status value, a confirmation number,
and the dollar amounts for the requested shares and fees. For example, a
request-response pair would look like this:

``` oac_no_warn
>> BUY 1000 ZZZZ MARKET
<< EXECUTED #1234567 TOTAL 50400.00 FEE 252.00
```

The `trading-rar` module implements the outbound contract of the Java EE
Connector Architecture to submit requests and obtain responses from the
legacy stock trading execution platform. The `trading-rar` module
provides and implements a custom client interface for Java EE
applications to use. This interface is simpler than the Common Client
Interface (CCI).

The `trading-war` module is a web application with a JavaServer Faces
interface and a managed bean. This application enables clients to submit
trades to the EIS using the resource adapter provided by the
`trading-rar` module. The `trading-war` module uses the custom client
interface provided by the resource adapter to obtain connections to the
EIS.

## 53.2.1 Using the Outbound Resource Adapter

In most cases, Java EE application developers use outbound resource
adapters developed by a third party. Outbound resource adapters either
implement the Common Client Interface (CCI) or provide a custom
interface for applications to interact with the EIS. Outbound resource
adapters provide Java EE applications with the following elements:

  - Connection factories

  - Connection handles

  - Other interfaces and objects specific to the EIS domain

Java EE applications obtain an instance of the connection factory via
resource injection and then use the factory object to obtain connection
handles to the EIS. The connection handles enable the application to
make requests and obtain information from the EIS.

The `trading-rar` module provides a custom client interface that
consists of the classes listed in [Table 53-1](#CHDCHJAC).

Table 53-1 Classes and Interfaces in the javaeetutorial.trading.rar.api
Package

<table style="width:32%;">
<colgroup>
<col width="32%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>API Component</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">TradeOrder</code></p></td>
<td><p>Represents a trade order for the EIS</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">TradeResponse</code></p></td>
<td><p>Represents a response from the EIS to a trade request</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">TradeConnection</code></p></td>
<td><p>Represents a connection handle to the EIS</p>
<p>Provides a method for applications to submit trades to the EIS</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">TradeConnectionFactory</code></p></td>
<td><p>Enables applications to obtain connection handles to the EIS</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">TradeProcessingException</code></p></td>
<td><p>Indicates that a problem occurred processing a trade request</p></td>
</tr>
</tbody>
</table>

  

The `ResourceAccessBean` managed bean in the `trading-war` module
configures a connection factory for the `trading-rar` resource adapter
by using the `@ConnectionFactoryDefinition` annotation as follows:

``` oac_no_warn
@Named
@SessionScoped
@ConnectionFactoryDefinition(
    name = "java:comp/env/eis/TradeConnectionFactory",
    interfaceName = "javaeetutorial.trading.rar.api.TradeConnectionFactory",
    resourceAdapter = "#trading-rar",
    minPoolSize = 5,
    transactionSupport = 
            TransactionSupport.TransactionSupportLevel.NoTransaction
)
public class ResourceAccessBean implements Serializable { ... }
```

The `name` parameter specifies the JNDI name for the connection factory.
This example registers the connection factory in the `java:comp` scope.
You can use the `ConnectionFactoryDefinition` annotation to specify a
different scope, such as `java:global`, `java:app`, or `java:module`.
The `AdministeredObjectDefinition` annotation also enables you to
register administered connector objects in the JNDI namespace.

The `interfaceName` parameter specifies the interface implemented by the
connection factory included in the resource adapter. In this example,
this is a custom interface.

The `resourceAdapter` parameter specifies the name of the resource
adapter that contains the connection factory implementation. The `#`
prefix in `#trading-rar` indicates that `trading-rar` is an embedded
resource adapter that is bundled in the same EAR as this web
application.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
You can also configure a connection factory for a previously deployed outbound resource adapter using the administration commands from your application server. However, this is a vendor-specific procedure.</td>
</tr>
</tbody>
</table>

  

The managed bean obtains a connection factory object using resource
injection as follows:

``` oac_no_warn
...
public class ResourceAccessBean implements Serializable {
    @Resource(lookup = "java:comp/env/eis/TradeConnectionFactory")
    private TradeConnectionFactory connectionFactory;
    ...
}
```

The managed bean uses the connection factory to obtain connection
handles as follows:

``` oac_no_warn
TradeConnection connection = connectionFactory.getConnection();
```

The resource adapter returns a connection handle associated with a
physical connection to the EIS. Once a connection handle is available,
the managed bean submits a trade and obtains the response as follows:

``` oac_no_warn
TradeOrder order = new TradeOrder();
order.setNShares(1000);
order.setTicker(TradeOrder.Ticker.YYYY);
order.setOrderType(TradeOrder.OrderType.BUY);
order.setOrderClass(TradeOrder.OrderClass.MARKET);
...
try {
    TradeResponse response = connection.submitOrder(order);
    ...
} catch (TradeProcessingException ex) { ... }
```

## 53.2.2 Implementing the Outbound Resource Adapter

The `trading-rar` module implements the outbound contract and a custom
client interface for the simple legacy stock trading platform EIS used
in this example. The architecture of the outbound resource adapter is
shown in [Figure 53-2](#CHDIGAJE).

Figure 53-2 Architecture of the trading Example

![Description of Figure 53-2 follows](img/jeett_dt_055.png)  
[Description of "Figure 53-2 Architecture of the trading
Example"](img_text/jeett_dt_055.htm)  
  

The `trading-rar` module implements the interfaces listed in [Table
53-2](#CHDIBBIC).

Table 53-2 Interfaces Implemented in the trading-rar Module

<table style="width:58%;">
<colgroup>
<col width="26%" />
<col width="32%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Package</th>
<th>Interface</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">javax.resource.spi</code></p></td>
<td><p><code dir="ltr">ResourceAdapter</code></p></td>
<td><p>Defines the lifecycle methods of the resource adapter</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.resource.spi</code></p></td>
<td><p><code dir="ltr">ManagedConnectionFactory</code></p></td>
<td><p>Defines a connection factory that the connection manager from the application server uses to obtain physical connections to the EIS</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.resource.spi</code></p></td>
<td><p><code dir="ltr">ManagedConnection</code></p></td>
<td><p>Defines a physical connection to the EIS that can be managed by the connection manager</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">trading.rar.api</code></p></td>
<td><p><code dir="ltr">TradeConnectionFactory</code></p></td>
<td><p>Defines a connection factory that applications use to obtain connection handles</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">trading.rar.api</code></p></td>
<td><p><code dir="ltr">TradeConnection</code></p></td>
<td><p>Defines a connection handle that applications use to interact with the EIS</p></td>
</tr>
</tbody>
</table>

  

When the `trading-ear` archive is deployed and a connection pool
resource is configured as described in [Using the Outbound Resource
Adapter](#CHDFADJD), the application server creates
`TradeConnectionFactory` objects that applications can obtain using
resource injection. The `TradeConnectionFactory` implementation
delegates creating connections to the connection manager provided by the
application server.

The connection manager uses the `ManagedConnectionFactory`
implementation to obtain physical connections to the EIS and maintains a
pool of active physical connections. When an application requests a
connection handle, the connection manager associates a connection from
the pool with a new connection handle that the application can use.
Connection pooling improves application performance and simplifies
resource adapter development.

For more details, see the code and the comments in the `trading-rar`
module.

## 53.2.3 Running the trading Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `trading` example.

The following topics are addressed here:

  - [Section 53.2.3.1, "To Run the trading Example Using NetBeans
    IDE"](#BABCHDDC)

  - [Section 53.2.3.2, "To Run the trading Example Using
    Maven"](#BABFJAAG)

### 53.2.3.1 To Run the trading Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/connectors
    ```

4.  Select the `trading` folder.

5.  Click Open Project.

6.  In the Projects tab, expand the `trading` node.

7.  Right-click the `trading-eis` module and select Open Project.

8.  Right-click the `trading-eis` project and select Run.
    
    The messages from the EIS appear in the Output tab:
    
    ``` oac_no_warn
    Trade execution server listening on port 4004.
    ```

9.  Right-click the `trading-ear` project and select Build.
    
    This command packages the resource adapter and the web application
    in an EAR file and deploys it to GlassFish Server.

10. Open the following URL in a web browser:
    
    ``` oac_no_warn
    http://localhost:8080/trading/
    ```
    
    The web interface enables you to connect to the EIS and submit
    trades. The server log shows the requests from the web application
    and the call sequence that provides connection handles from the
    resource adapter.

11. Before undeploying the `trading-ear` application, close the
    `trading-eis` application from the status bar.

### 53.2.3.2 To Run the trading Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/connectors/trading/
    ```

3.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the resource adapter and the web
    application into an EAR archive and deploys it to GlassFish Server.

4.  In the same terminal window, go to the `trading-eis` directory:
    
    ``` oac_no_warn
    cd trading-eis
    ```

5.  Enter the following command to run the trade execution platform:
    
    ``` oac_no_warn
    mvn exec:java
    ```
    
    The messages from the EIS appear in the terminal window:
    
    ``` oac_no_warn
    Trade execution server listening on port 4004.
    ```

6.  Open the following URL in a web browser:
    
    ``` oac_no_warn
    http://localhost:8080/trading/
    ```
    
    The web interface enables you to connect to the EIS and submit
    trades. The server log shows the requests from the web application
    and the call sequence that provides connection handles from the
    resource adapter.

7.  Before undeploying the `trading-ear` application, press Ctrl+C on
    the terminal window to close the `trading-eis` application.

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
<td><a href="connectorexample001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="connectorexample003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
