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
<td><a href="connectorexample002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="interceptors.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 53.3 The traffic Example

The `traffic` example demonstrates how to implement and use a simple
inbound resource adapter that receives data from a legacy EIS using a
TCP socket.

The example is in the tut-install`/examples/connectors/traffic`
directory. See [Chapter 2, "Using the Tutorial
Examples,"](usingexamples.htm#GFIUD) for basic information on building
and running sample applications.

The example demonstrates the scenario in [Figure 53-3](#CHDGFGHB) and
consists of the following modules:

  - `traffic-eis`: A Java SE program that simulates an EIS

  - `traffic-rar`: The inbound resource adapter implementation

  - `traffic-ejb`: A message-driven bean that is the endpoint for
    incoming messages

  - `traffic-war`: A web application that displays information from the
    message-driven bean

  - `traffic-ear`: An enterprise archive that contains the resource
    adapter, the message-driven bean, and the web application

Figure 53-3 The traffic Example

![Description of Figure 53-3 follows](img/jeett_dt_056.png)  
[Description of "Figure 53-3 The traffic
Example"](img_text/jeett_dt_056.htm)  
  

The `traffic-eis` module is an auxiliary project that resembles a legacy
traffic information system. It contains a Java SE program that sends
traffic status updates for several cities to any subscribed client. The
program sends the updates in JSON format over a TCP socket. For example,
a traffic update looks like this:

``` oac_no_warn
{"report":[
    {"city":"City1", "access":"AccessA", "status":"GOOD"},
    {"city":"City1", "access":"AccessB", "status":"CONGESTED"},
    ...
    {"city":"City5", "access":"AccessE", "status":"SLOW"}
 ]}
```

The `traffic-rar` module implements the inbound contract of the Java EE
Connector Architecture. This module subscribes to the traffic
information system using the TCP port indicated by the configuration
provided by the MDB and invokes the methods of the MDB to process
traffic information updates.

The `traffic-ejb` module contains a message-driven bean that activates
the resource adapter with a configuration parameter (the TCP port to
subscribe to the traffic information system). The MDB contains a method
to process the traffic information updates. This method filters the
updates for a particular city and publishes the results to a Java
Message Service (JMS) topic.

The `traffic-war` module contains a message-driven bean that receives
filtered traffic information updates from the JMS topic asynchronously
and sends them to the clients using a WebSocket endpoint.

## 53.3.1 Using the Inbound Resource Adapter

In most cases, Java EE application developers use inbound resource
adapters developed by a third party. To use an inbound resource adapter,
a Java EE application includes a message-driven bean with the following
characteristics.

  - The MDB implements the business interface defined by the resource
    adapter.

  - The MDB specifies configuration parameters to activate the resource
    adapter.

The business interface defined by the resource adapter is not specified
in the Java EE Connector Architecture; it is specific to the EIS.

The MDB in this example is defined as follows:

``` oac_no_warn
@MessageDriven(
    activationConfig = {
      @ActivationConfigProperty(propertyName = "port", 
                                propertyValue = "4008")
    }
)
public class TrafficMdb implements TrafficListener { ... }
```

The `TrafficListener` interface is defined in the API package of the
resource adapter. The resource adapter requires the MDB to provide the
`port` property.

When the MDB is deployed, it activates the `traffic-rar` resource
adapter, which invokes the methods of the MDB to process traffic
information updates. Then the MDB filters the updates for a particular
city and publishes the results to a JMS topic.

In this particular example, the `TrafficListener` interface is empty. In
addition to this interface, the resource adapter provides the
`TrafficCommand` annotation and uses reflection to discover which
methods in the MDB are decorated with this annotation:

``` oac_no_warn
@MessageDriven(...)
public class TrafficMdb implements TrafficListener {

    @TrafficCommand(name="report", info="Process report")
    public void processReport(String jsonReport) { ... }
    ...
}
```

This approach enables you to adapt the MDB to support new features in
the EIS without having to modify the `TrafficListener` interface or the
resource adapter module.

## 53.3.2 Implementing the Inbound Resource Adapter

The `traffic-rar` module implements the inbound resource adapter
contract from the Java EE Connector Architecture for the simple traffic
information system (EIS) used in this example. The architecture of the
inbound resource adapter is shown in [Figure 53-4](#CHDHADDC).

Figure 53-4 Architecture of the traffic Example

![Description of Figure 53-4 follows](img/jeett_dt_057.png)  
[Description of "Figure 53-4 Architecture of the traffic
Example"](img_text/jeett_dt_057.htm)  
  

The `traffic-rar` module implements the interfaces listed in [Table
53-3](#CHDEDEAF).

Table 53-3 Interfaces Implemented in the traffic-rar Module

<table style="width:49%;">
<colgroup>
<col width="26%" />
<col width="23%" />
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
<td><p>Defines the lifecycle methods of the resource adapter.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.resource.spi</code></p></td>
<td><p><code dir="ltr">ActivationSpec</code></p></td>
<td><p>Defines the configuration parameters that the MDB provides to activate the inbound resource adapter.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.resource.spi</code></p></td>
<td><p><code dir="ltr">Work</code></p></td>
<td><p>The traffic service subscriber implements this interface from the work management contract to wait for traffic updates on a separate thread.</p></td>
</tr>
</tbody>
</table>

  

When an MDB activates the inbound resource adapter, the container
invokes the `endpointActivation` method in the `TrafficResourceAdapter`
class:

``` oac_no_warn
@Connector(...)
public class TrafficResourceAdapter implements ResourceAdapter, Serializable {
    ...
    @Override
    public void endpointActivation(MessageEndpointFactory endpointFactory, 
                                   ActivationSpec spec) 
                                   throws ResourceException {
        Class endpointClass = endpointFactory.getEndpointClass();
        /* this method is called from a new thread in the example: 
        MessageEndpoint endpoint = endpointFactory.createEndpoint(null); */
    }
}
```

The `getEndpointClass` method returns the `Class` type of the MDB
performing the activation, which enables the resource adapter to use
reflection to find methods annotated with `@TrafficCommand` in the MDB.

The `createEndpoint` method returns an instance of the MDB. The resource
adapter uses this instance to invoke the methods of the MDB when it
receives requests from the EIS.

After obtaining the message endpoint instance (MDB), the resource
adapter uses the work management contract to create the traffic service
subscriber thread that receives traffic updates from the EIS. The
resource adapter obtains the `WorkManager` instance from the bootstrap
context as follows:

``` oac_no_warn
WorkManager workManager;
...
@Override
public void start(BootstrapContext ctx) ... {
    workManager = ctx.getWorkManager();
}
```

The resource adapter schedules the traffic service subscriber thread
using the work manager:

``` oac_no_warn
tSubscriber = new TrafficServiceSubscriber(tSpec, endpoint);
workManager.scheduleWork(tSubscriber);
```

The `TrafficServiceSubscriber` class implements the
`javax.resource.spi.Work` interface from the work management contract.

The traffic service subscriber thread uses reflection to invoke the
methods in the MDB:

``` oac_no_warn
private String callMdb(MessageEndpoint mdb, Method command, 
                       String... params) ... {
    String resp;
    /* this code contains proper exception handling in the sources */
    mdb.beforeDelivery(command);
    Object ret = command.invoke(mdb, (Object[]) params);
    resp = (String) ret;
    mdb.afterDelivery();
    return resp;
}

For more details, see the code and the comments in the traffic-rar module.
```

## 53.3.3 Running the traffic Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `traffic` example.

The following topics are addressed here:

  - [Section 53.3.3.1, "To Run the traffic Example Using NetBeans
    IDE"](#BABIJJEH)

  - [Section 53.3.3.2, "To Run the traffic Example Using
    Maven"](#BABBBGBA)

### 53.3.3.1 To Run the traffic Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/connectors
    ```

4.  Select the `traffic` folder.

5.  Click Open Project.

6.  In the Projects tab, expand the `traffic` node.

7.  Right-click the `traffic-eis` module and select Open Project.

8.  Right-click the `traffic-eis` project and select Run.
    
    The messages from the EIS appear on the Output tab:
    
    ``` oac_no_warn
    Traffic EIS accepting connections on port 4008
    ```

9.  In the Projects tab, right-click the `traffic` project and select
    Clean and Build.
    
    This command builds and packages the resource adapter, the MDB, and
    the web application into an EAR archive and deploys it. The server
    log shows the call sequence that activates the resource adapter and
    the filtered traffic updates for City1.

10. Open the following URL in a web browser:
    
    ``` oac_no_warn
    http://localhost:8080/traffic/
    ```
    
    The web interface shows filtered traffic updates for City1 every few
    seconds.

11. After undeploying the `traffic-ear` application, close the
    `traffic-eis` application from the status bar.

### 53.3.3.2 To Run the traffic Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/connectors/traffic/traffic-eis/
    ```

3.  Enter the following command in the terminal window:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the traffic EIS.

4.  Enter the following command in the terminal window:
    
    ``` oac_no_warn
    mvn exec:java
    ```
    
    The messages from the EIS appear in the terminal window:
    
    ``` oac_no_warn
    Traffic EIS accepting connections on port 4008
    ```
    
    Leave this terminal window open.

5.  Open a new terminal window and go to:
    
    ``` oac_no_warn
    tut-install/examples/connectors/traffic/
    ```

6.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the resource adapter, the MDB, and
    the web application into an EAR archive and deploys it. The server
    log shows the call sequence that activates the resource adapter and
    the filtered traffic updates for City1.

7.  Open the following URL in a web browser:
    
    ``` oac_no_warn
    http://localhost:8080/traffic/
    ```
    
    The web interface shows the filtered traffic updates for City1 every
    few seconds.

8.  After undeploying the `traffic-ear` application, press Ctrl+C in the
    first terminal window to close the `traffic-eis` application.

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
<td><a href="connectorexample002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="interceptors.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
