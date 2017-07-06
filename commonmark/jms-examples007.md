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
<td><a href="jms-examples006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jms-examples008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 46.7 Receiving Messages Asynchronously Using a Message-Driven Bean

If you are writing an application to run in the Java EE application
client container or on the Java SE platform, and you want to receive
messages asynchronously, you need to define a class that implements the
`MessageListener` interface, create a `JMSConsumer`, and call the method
`setMessageListener`.

If you're writing an application to run in the Java EE web or EJB
container and want it to receive messages asynchronously, you also need
to need to define a class that implements the `MessageListener`
interface. However, instead of creating a `JMSConsumer` and calling the
method `setMessageListener`, you must configure your message listener
class to be a message-driven bean. The application server will then take
care of the rest.

Message-driven beans can implement any messaging type. Most commonly,
however, they implement the Java Message Service (JMS) technology.

This section describes a simple message-driven bean example. Before
proceeding, you should read the basic conceptual information in the
section [What Is a Message-Driven Bean?](ejb-intro003.htm#GIPKO) as well
as [Using Message-Driven Beans to Receive Messages
Asynchronously](jms-concepts005.htm#BNCGQ).

## 46.7.1 Overview of the simplemessage Example

The `simplemessage` application has the following components:

  - `SimpleMessageClient`: An application client that sends several
    messages to a queue

  - `SimpleMessageBean`: A message-driven bean that asynchronously
    processes the messages that are sent to the queue

[Figure 46-3](#BNBPM) illustrates the structure of this application. The
application client sends messages to the queue, which was created
administratively using the Administration Console. The JMS provider (in
this case, GlassFish Server) delivers the messages to the instances of
the message-driven bean, which then processes the messages.

Figure 46-3 The simplemessage Application

![Description of Figure 46-3 follows](img/jeett_dt_036.png)  
[Description of "Figure 46-3 The simplemessage
Application"](img_text/jeett_dt_036.htm)  
  

The source code for this application is in the
tut-install`/examples/jms/simplemessage/` directory.

## 46.7.2 The simplemessage Application Client

The `SimpleMessageClient` sends messages to the queue that the
`SimpleMessageBean` listens to. The client starts by injecting the
connection factory and queue resources:

``` oac_no_warn
@Resource(lookup = "java:comp/DefaultJMSConnectionFactory")
private static ConnectionFactory connectionFactory;

@Resource(lookup = "jms/MyQueue")
private static Queue queue;
```

Next, the client creates the `JMSContext` in a `try`-with-resources
block:

``` oac_no_warn
String text;
final int NUM_MSGS = 3;

try (JMSContext context = connectionFactory.createContext();) {
```

Finally, the client sends several text messages to the queue:

``` oac_no_warn
for (int i = 0; i < NUM_MSGS; i++) {
    text = "This is message " + (i + 1);
    System.out.println("Sending message: " + text);
    context.createProducer().send(queue, text);
}
```

## 46.7.3 The simplemessage Message-Driven Bean Class

The code for the `SimpleMessageBean` class illustrates the requirements
of a message-driven bean class described in [Using Message-Driven Beans
to Receive Messages Asynchronously](jms-concepts005.htm#BNCGQ).

The first few lines of the `SimpleMessageBean` class use the
`@MessageDriven` annotation's `activationConfig` attribute to specify
configuration properties:

``` oac_no_warn
@MessageDriven(activationConfig = {
    @ActivationConfigProperty(propertyName = "destinationLookup",
            propertyValue = "jms/MyQueue"),
    @ActivationConfigProperty(propertyName = "destinationType",
            propertyValue = "javax.jms.Queue")
})
```

See [Table 45-3](jms-concepts005.htm#GJKOH) for a list of the available
properties.

See [Sending Messages from a Session Bean to an
MDB](jms-examples008.htm#BNCGW) for examples of the
`subscriptionDurability`, `clientId`, `subscriptionName`, and
`messageSelector` properties.

### 46.7.3.1 The onMessage Method

When the queue receives a message, the EJB container invokes the message
listener method or methods. For a bean that uses JMS, this is the
`onMessage` method of the `MessageListener` interface.

In the `SimpleMessageBean` class, the `onMessage` method casts the
incoming message to a `TextMessage` and displays the text:

``` oac_no_warn
public void onMessage(Message inMessage) {

    try {
        if (inMessage instanceof TextMessage) {
            logger.log(Level.INFO,
                    "MESSAGE BEAN: Message received: {0}",
                    inMessage.getBody(String.class));
        } else {
            logger.log(Level.WARNING,
                    "Message of wrong type: {0}",
                    inMessage.getClass().getName());
        }
    } catch (JMSException e) {
        logger.log(Level.SEVERE,
                "SimpleMessageBean.onMessage: JMSException: {0}",
                e.toString());
        mdc.setRollbackOnly();
    }
}
```

## 46.7.4 Running the simplemessage Example

You can use either NetBeans IDE or Maven to build, deploy, and run the
`simplemessage` example.

The following topics are addressed here:

  - [Section 46.7.4.1, "Creating Resources for the simplemessage
    Example"](#BNBPR)

  - [Section 46.7.4.2, "To Run the simplemessage Example Using NetBeans
    IDE"](#CHDFBDDA)

  - [Section 46.7.4.3, "To Run the simplemessage Example Using
    Maven"](#BNBPT)

### 46.7.4.1 Creating Resources for the simplemessage Example

This example uses the queue named `jms/MyQueue` and the preconfigured
default connection factory `java:comp/DefaultJMSConnectionFactory`.

If you have run the simple JMS examples in [Writing Simple JMS
Applications](jms-examples003.htm#BNCFA) and have not deleted the
resources, you already have the queue. Otherwise, follow the
instructions in [To Create Resources for the Simple
Examples](jms-examples003.htm#BABHEFCB) to create it.

For more information on creating JMS resources, see [Creating JMS
Administered Objects](jms-examples003.htm#GKTJS).

### 46.7.4.2 To Run the simplemessage Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/jms/simplemessage
    ```

4.  Select the `simplemessage` folder.

5.  Make sure that the Open Required Projects check box is selected,
    then click Open Project.

6.  In the Projects tab, right-click the `simplemessage` project and
    select Build. (If NetBeans IDE suggests that you run a priming
    build, click the box to do so.)
    
    This command packages the application client and the message-driven
    bean, then creates a file named `simplemessage.ear` in the
    `simplemessage-ear/target/` directory. It then deploys the
    `simplemessage-ear` module, retrieves the client stubs, and runs the
    application client.
    
    The output in the output window looks like this (preceded by
    application client container output):
    
    ``` oac_no_warn
    Sending message: This is message 1
    Sending message: This is message 2
    Sending message: This is message 3
    To see if the bean received the messages,
     check <install_dir>/domains/domain1/logs/server.log.
    ```
    
    In the server log file, lines similar to the following appear:
    
    ``` oac_no_warn
    MESSAGE BEAN: Message received: This is message 1
    MESSAGE BEAN: Message received: This is message 2
    MESSAGE BEAN: Message received: This is message 3
    ```
    
    The received messages may appear in a different order from the order
    in which they were sent.

7.  After you have finished running the application, undeploy it using
    the Services tab.

### 46.7.4.3 To Run the simplemessage Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/jms/simplemessage/
    ```

3.  To compile the source files and package the application, use the
    following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This target packages the application client and the message-driven
    bean, then creates a file named `simplemessage.ear` in the
    `simplemessage-ear/target/` directory. It then deploys the
    `simplemessage-ear` module, retrieves the client stubs, and runs the
    application client.
    
    The output in the terminal window looks like this (preceded by
    application client container output):
    
    ``` oac_no_warn
    Sending message: This is message 1
    Sending message: This is message 2
    Sending message: This is message 3
    To see if the bean received the messages,
     check <install_dir>/domains/domain1/logs/server.log.
    ```
    
    In the server log file, lines similar to the following appear:
    
    ``` oac_no_warn
    MESSAGE BEAN: Message received: This is message 1
    MESSAGE BEAN: Message received: This is message 2
    MESSAGE BEAN: Message received: This is message 3
    ```
    
    The received messages may appear in a different order from the order
    in which they were sent.

4.  After you have finished running the application, undeploy it using
    the `mvn cargo:undeploy` command.

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
<td><a href="jms-examples006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jms-examples008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
