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
<td><a href="jms-examples002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jms-examples004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 46.3 Writing Simple JMS Applications

This section shows how to create, package, and run simple JMS clients
that are packaged as application clients.

The following topics are addressed here:

  - [Section 46.3.1, "Overview of Writing Simple JMS
    Application"](#CHDCEFGA)

  - [Section 46.3.2, "Starting the JMS Provider"](#BNCFD)

  - [Section 46.3.3, "Creating JMS Administered Objects"](#GKTJS)

  - [Section 46.3.4, "Building All the Simple Examples"](#BABEEABE)

  - [Section 46.3.5, "Sending Messages"](#BABIHCAE)

  - [Section 46.3.6, "Receiving Messages Synchronously"](#BNCFB)

  - [Section 46.3.7, "Using a Message Listener for Asynchronous Message
    Delivery"](#BNCFH)

  - [Section 46.3.8, "Browsing Messages on a Queue"](#BNCFL)

  - [Section 46.3.9, "Running Multiple Consumers on the Same
    Destination"](#BABDDHHC)

  - [Section 46.3.10, "Acknowledging Messages"](#BNCFX)

## 46.3.1 Overview of Writing Simple JMS Application

The clients demonstrate the basic tasks a JMS application must perform:

  - Creating a `JMSContext`

  - Creating message producers and consumers

  - Sending and receiving messages

Each example uses two clients: one that sends messages and one that
receives them. You can run the clients in two terminal windows.

When you write a JMS client to run in an enterprise bean application,
you use many of the same methods in much the same sequence as for an
application client. However, there are some significant differences.
[Using the JMS API in Java EE Applications](jms-concepts005.htm#BNCGL)
describes these differences, and this chapter provides examples that
illustrate them.

The examples for this section are in the
tut-install`/examples/jms/simple/` directory, under the following
subdirectories:

  
`producer/`  
`synchconsumer/`  
`asynchconsumer/`  
`messagebrowser/`  
`clientackconsumer/`  

Before running the examples, you need to start GlassFish Server and
create administered objects.

## 46.3.2 Starting the JMS Provider

When you use GlassFish Server, your JMS provider is GlassFish Server.
Start the server as described in [Starting and Stopping GlassFish
Server](usingexamples002.htm#BNADI).

## 46.3.3 Creating JMS Administered Objects

This example uses the following JMS administered objects:

  - A connection factory

  - Two destination resources: a topic and a queue

Before you run the applications, you can use the `asadmin add-resources`
command to create needed JMS resources, specifying as the argument a
file named `glassfish-resources.xml`. This file can be created in any
project using NetBeans IDE, although you can also create it by hand. A
file for the needed resources is present in the
`jms/simple/producer/src/main/setup/` directory.

The JMS examples use a connection factory with the logical JNDI lookup
name `java:comp/DefaultJMSConnectionFactory`, which is preconfigured in
GlassFish Server.

You can also use the `asadmin create-jms-resource` command to create
resources, the `asadmin list-jms-resources` command to display their
names, and the `asadmin delete-jms-resource` command to remove them.

### 46.3.3.1 To Create Resources for the Simple Examples

A `glassfish-resources.xml` file in one of the Maven projects can create
all the resources needed for the simple examples.

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a command window, go to the `Producer` example.
    
    ``` oac_no_warn
    cd tut-install/jms/simple/producer
    ```

3.  Create the resources using the `asadmin add-resources` command:
    
    ``` oac_no_warn
    asadmin add-resources src/main/setup/glassfish-resources.xml
    ```

4.  Verify the creation of the resources:
    
    ``` oac_no_warn
    asadmin list-jms-resources
    ```
    
    The command lists the two destinations and connection factory
    specified in the `glassfish-resources.xml` file in addition to the
    platform default connection factory:
    
    ``` oac_no_warn
    jms/MyQueue
    jms/MyTopic
    jms/__defaultConnectionFactory
    Command list-jms-resources executed successfully.
    ```
    
    In GlassFish Server, the Java EE
    `java:comp/DefaultJMSConnectionFactory` resource is mapped to a
    connection factory named `jms/__defaultConnectionFactory`.

## 46.3.4 Building All the Simple Examples

To run the simple examples using GlassFish Server, package each example
in an application client JAR file. The application client JAR file
requires a manifest file, located in the `src/main/java/META-INF/`
directory for each example, along with the `.class` file.

The `pom.xml` file for each example specifies a plugin that creates an
application client JAR file. You can build the examples using either
NetBeans IDE or Maven.

The following topics are addressed here:

  - [Section 46.3.4.1, "To Build All the Simple Examples Using NetBeans
    IDE"](#CHDJEJCD)

  - [Section 46.3.4.2, "To Build All the Simple Examples Using
    Maven"](#CHDGHJAA)

### 46.3.4.1 To Build All the Simple Examples Using NetBeans IDE

1.  From the File menu, choose Open Project.

2.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/jms
    ```

3.  Expand the `jms` node and select the `simple` folder.

4.  Click Open Project to open all the simple examples.

5.  In the Projects tab, right-click the `simple` project and select
    Build to build all the examples.
    
    This command places the application client JAR files in the `target`
    directories for the examples.

### 46.3.4.2 To Build All the Simple Examples Using Maven

1.  In a terminal window, go to the `simple` directory:
    
    ``` oac_no_warn
    cd tut-install/jms/simple/
    ```

2.  Enter the following command to build all the projects:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command places the application client JAR files in the `target`
    directories for the examples.

## 46.3.5 Sending Messages

This section describes how to use a client to send messages. The
`Producer.java` client will send messages in all of these examples.

The following topics are addressed here:

  - [Section 46.3.5.1, "General Steps Performed in the
    Example"](#CHDGHJHH)

  - [Section 46.3.5.2, "The Producer.java Client"](#CHDFBABB)

  - [Section 46.3.5.3, "To Run the Producer Client"](#CHDHIIHE)

### 46.3.5.1 General Steps Performed in the Example

General steps this example performs are as follows.

1.  Inject resources for the administered objects used by the example.

2.  Accept and verify command-line arguments. You can use this example
    to send any number of messages to either a queue or a topic, so you
    specify the destination type and the number of messages on the
    command line when you run the program.

3.  Create a `JMSContext`, then send the specified number of text
    messages in the form of strings, as described in [Message
    Bodies](jms-concepts003.htm#BNCEW).

4.  Send a final message of type `Message` to indicate that the consumer
    should expect no more messages.

5.  Catch any exceptions.

### 46.3.5.2 The Producer.java Client

The sending client, `Producer.java`, performs the following steps.

1.  Injects resources for a connection factory, queue, and topic:
    
    ``` oac_no_warn
    @Resource(lookup = "java:comp/DefaultJMSConnectionFactory")
    private static ConnectionFactory connectionFactory;
    @Resource(lookup = "jms/MyQueue")
    private static Queue queue;
    @Resource(lookup = "jms/MyTopic")
    private static Topic topic;
    ```

2.  Retrieves and verifies command-line arguments that specify the
    destination type and the number of arguments:
    
    ``` oac_no_warn
    final int NUM_MSGS;
    String destType = args[0];
    System.out.println("Destination type is " + destType);
    if ( ! ( destType.equals("queue") || destType.equals("topic") ) ) { 
        System.err.println("Argument must be \"queue\" or " + "\"topic\"");
        System.exit(1);
    }
    if (args.length == 2){ 
        NUM_MSGS = (new Integer(args[1])).intValue();
    } else { 
        NUM_MSGS = 1;
    }
    ```

3.  Assigns either the queue or the topic to a destination object, based
    on the specified destination type:
    
    ``` oac_no_warn
    Destination dest = null;
    try { 
        if (destType.equals("queue")) { 
            dest = (Destination) queue; 
        } else { 
            dest = (Destination) topic; 
        }
    } catch (Exception e) {
        System.err.println("Error setting destination: " + e.toString()); 
        System.exit(1);
    }
    ```

4.  Within a `try`-with-resources block, creates a `JMSContext`:
    
    ``` oac_no_warn
    try (JMSContext context = connectionFactory.createContext();) {
    ```

5.  Sets the message count to zero, then creates a `JMSProducer` and
    sends one or more messages to the destination and increments the
    count. Messages in the form of strings are of the `TextMessage`
    message type:
    
    ``` oac_no_warn
        int count = 0;
        for (int i = 0; i < NUM_MSGS; i++) { 
            String message = "This is message " + (i + 1) 
                    + " from producer";
            // Comment out the following line to send many messages
            System.out.println("Sending message: " + message); 
            context.createProducer().send(dest, message);
            count += 1;
        }
        System.out.println("Text messages sent: " + count);
    ```

6.  Sends an empty control message to indicate the end of the message
    stream:
    
    ``` oac_no_warn
        context.createProducer().send(dest, context.createMessage());
    ```
    
    Sending an empty message of no specified type is a convenient way
    for an application to indicate to the consumer that the final
    message has arrived.

7.  Catches and handles any exceptions. The end of the
    `try`-with-resources block automatically causes the `JMSContext` to
    be closed:
    
    ``` oac_no_warn
    } catch (Exception e) {
        System.err.println("Exception occurred: " + e.toString());
        System.exit(1);
    }
    System.exit(0);
    ```

### 46.3.5.3 To Run the Producer Client

You can run the client using the `appclient` command. The `Producer`
client takes one or two command-line arguments: a destination type and,
optionally, a number of messages. If you do not specify a number of
messages, the client sends one message.

You will use the client to send three messages to a queue.

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)) and that you
    have created resources and built the simple JMS examples (see
    [Creating JMS Administered Objects](#GKTJS) and [Building All the
    Simple Examples](#BABEEABE)).

2.  In a terminal window, go to the `producer` directory:
    
    ``` oac_no_warn
    cd producer
    ```

3.  Run the `Producer` program, sending three messages to the queue:
    
    ``` oac_no_warn
    appclient -client target/producer.jar queue 3
    ```
    
    The output of the program looks like this (along with some
    additional output):
    
    ``` oac_no_warn
    Destination type is queue
    Sending message: This is message 1 from producer
    Sending message: This is message 2 from producer
    Sending message: This is message 3 from producer
    Text messages sent: 3
    ```
    
    The messages are now in the queue, waiting to be received.
    
      
    
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Note:</p>
    When you run an application client, the command may take a long time to complete.</td>
    </tr>
    </tbody>
    </table>
    
      

## 46.3.6 Receiving Messages Synchronously

This section describes the receiving client, which uses the `receive`
method to consume messages synchronously. This section then explains how
to run the clients using GlassFish Server.

The following topics are addressed here:

  - [Section 46.3.6.1, "The SynchConsumer.java Client"](#BNCFC)

  - [Section 46.3.6.2, "To Run the SynchConsumer and Producer
    Clients"](#BNCFG)

### 46.3.6.1 The SynchConsumer.java Client

The receiving client, `SynchConsumer.java`, performs the following
steps.

1.  Injects resources for a connection factory, queue, and topic.

2.  Assigns either the queue or the topic to a destination object, based
    on the specified destination type.

3.  Within a `try`-with-resources block, creates a `JMSContext`.

4.  Creates a `JMSConsumer`, starting message delivery:
    
    ``` oac_no_warn
    consumer = context.createConsumer(dest);
    ```

5.  Receives the messages sent to the destination until the
    end-of-message-stream control message is received:
    
    ``` oac_no_warn
    int count = 0;
    while (true) {
        Message m = consumer.receive(1000); 
        if (m != null) { 
            if (m instanceof TextMessage) { 
                System.out.println(
                        "Reading message: " + m.getBody(String.class));
                count += 1; 
            } else { 
                break; 
            } 
        }
    }
    System.out.println("Messages received: " + count);
    ```
    
    Because the control message is not a `TextMessage`, the receiving
    client terminates the `while` loop and stops receiving messages
    after the control message arrives.

6.  Catches and handles any exceptions. The end of the
    `try`-with-resources block automatically causes the `JMSContext` to
    be closed.

The `SynchConsumer` client uses an indefinite `while` loop to receive
messages, calling `receive` with a timeout argument.

### 46.3.6.2 To Run the SynchConsumer and Producer Clients

You can run the client using the `appclient` command. The
`SynchConsumer` client takes one command-line argument, the destination
type.

These steps show how to receive and send messages synchronously using
both a queue and a topic. The steps assume you already ran the
`Producer` client and have three messages waiting in the queue.

1.  In the same terminal window where you ran `Producer`, go to the
    `synchconsumer` directory:
    
    ``` oac_no_warn
    cd ../synchconsumer
    ```

2.  Run the `SynchConsumer` client, specifying the queue:
    
    ``` oac_no_warn
    appclient -client target/synchconsumer.jar queue
    ```
    
    The output of the client looks like this (along with some additional
    output):
    
    ``` oac_no_warn
    Destination type is queue
    Reading message: This is message 1 from producer
    Reading message: This is message 2 from producer
    Reading message: This is message 3 from producer
    Messages received: 3
    ```

3.  Now try running the clients in the opposite order. Run the
    `SynchConsumer` client:
    
    ``` oac_no_warn
    appclient -client target/synchconsumer.jar queue
    ```
    
    The client displays the destination type and then waits for
    messages.

4.  Open a new terminal window and run the `Producer` client:
    
    ``` oac_no_warn
    cd tut-install/jms/simple/producer
    appclient -client target/producer.jar queue 3
    ```
    
    When the messages have been sent, the `SynchConsumer` client
    receives them and exits.

5.  Now run the `Producer` client using a topic instead of a queue:
    
    ``` oac_no_warn
    appclient -client target/producer.jar topic 3
    ```
    
    The output of the client looks like this (along with some additional
    output):
    
    ``` oac_no_warn
    Destination type is topic
    Sending message: This is message 1 from producer
    Sending message: This is message 2 from producer
    Sending message: This is message 3 from producer
    Text messages sent: 3
    ```

6.  Now, in the other terminal window, run the `SynchConsumer` client
    using the topic:
    
    ``` oac_no_warn
    appclient -client target/synchconsumer.jar topic
    ```
    
    The result, however, is different. Because you are using a
    subscription on a topic, messages that were sent before you created
    the subscription on the topic will not be added to the subscription
    and delivered to the consumer. (See [Publish/Subscribe Messaging
    Style](jms-concepts002.htm#BNCED) and [Consuming Messages from
    Topics](jms-concepts003.htm#BABEEJJJ) for details.) Instead of
    receiving the messages, the client waits for messages to arrive.

7.  Leave the `SynchConsumer` client running and run the `Producer`
    client again:
    
    ``` oac_no_warn
    appclient -client target/producer.jar topic 3
    ```
    
    Now the `SynchConsumer` client receives the messages:
    
    ``` oac_no_warn
    Destination type is topic
    Reading message: This is message 1 from producer
    Reading message: This is message 2 from producer
    Reading message: This is message 3 from producer
    Messages received: 3
    ```
    
    Because these messages were sent after the consumer was started, the
    client receives them.

## 46.3.7 Using a Message Listener for Asynchronous Message Delivery

This section describes the receiving clients in an example that uses a
message listener for asynchronous message delivery. This section then
explains how to compile and run the clients using GlassFish Server.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
In the Java EE platform, message listeners can be used only in application clients, as in this example. To allow asynchronous message delivery in a web or enterprise bean application, you use a message-driven bean, shown in later examples in this chapter.</td>
</tr>
</tbody>
</table>

  

The following topics are addressed here:

  - [Section 46.3.7.1, "Writing the AsynchConsumer.java and
    TextListener.java Clients"](#BNCFI)

  - [Section 46.3.7.2, "To Run the AsynchConsumer and Producer
    Clients"](#BNCFK)

### 46.3.7.1 Writing the AsynchConsumer.java and TextListener.java Clients

The sending client is `Producer.java`, the same client used in [Sending
Messages](#BABIHCAE) and [Receiving Messages Synchronously](#BNCFB).

An asynchronous consumer normally runs indefinitely. This one runs until
the user types the character `q` or `Q` to stop the client.

1.  The client, `AsynchConsumer.java`, performs the following steps.
    
    1.  Injects resources for a connection factory, queue, and topic.
    
    2.  Assigns either the queue or the topic to a destination object,
        based on the specified destination type.
    
    3.  In a `try`-with-resources block, creates a `JMSContext`.
    
    4.  Creates a `JMSConsumer`.
    
    5.  Creates an instance of the `TextListener` class and registers it
        as the message listener for the `JMSConsumer`:
        
        ``` oac_no_warn
        listener = new TextListener();
        consumer.setMessageListener(listener);
        ```
    
    6.  Listens for the messages sent to the destination, stopping when
        the user types the character `q` or `Q` (it uses a
        `java.io.InputStreamReader` to do this).
    
    7.  Catches and handles any exceptions. The end of the
        `try`-with-resources block automatically causes the `JMSContext`
        to be closed, thus stopping delivery of messages to the message
        listener.

2.  The message listener, `TextListener.java`, follows these steps:
    
    1.  When a message arrives, the `onMessage` method is called
        automatically.
    
    2.  If the message is a `TextMessage`, the `onMessage` method
        displays its content as a string value. If the message is not a
        text message, it reports this fact:
        
        ``` oac_no_warn
        public void onMessage(Message m) { 
            try { 
                if (m instanceof TextMessage) { 
                    System.out.println(
                            "Reading message: " + m.getBody(String.class)); 
                } else { 
                     System.out.println("Message is not a TextMessage"); 
                } 
            } catch (JMSException | JMSRuntimeException e) {
                System.err.println("JMSException in onMessage(): " + e.toString());
            }
        }
        ```

For this example, you will use the same connection factory and
destinations you created in [To Create Resources for the Simple
Examples](#BABHEFCB).

The steps assume that you have already built and packaged all the
examples using NetBeans IDE or Maven.

### 46.3.7.2 To Run the AsynchConsumer and Producer Clients

You will need two terminal windows, as you did in [Receiving Messages
Synchronously](#BNCFB).

1.  In the terminal window where you ran the `SynchConsumer` client, go
    to the `asynchconsumer` example directory:
    
    ``` oac_no_warn
    cd tut-install/jms/simple/asynchconsumer
    ```

2.  Run the `AsynchConsumer` client, specifying the `topic` destination
    type:
    
    ``` oac_no_warn
    appclient -client target/asynchconsumer.jar topic
    ```
    
    The client displays the following lines (along with some additional
    output) and then waits for messages:
    
    ``` oac_no_warn
    Destination type is topic
    To end program, enter Q or q, then <return>
    ```

3.  In the terminal window where you ran the `Producer` client
    previously, run the client again, sending three messages:
    
    ``` oac_no_warn
    appclient -client target/producer.jar topic 3
    ```
    
    The output of the client looks like this (along with some additional
    output):
    
    ``` oac_no_warn
    Destination type is topic
    Sending message: This is message 1 from producer
    Sending message: This is message 2 from producer
    Sending message: This is message 3 from producer
    Text messages sent: 3
    ```
    
    In the other window, the `AsynchConsumer` client displays the
    following (along with some additional output):
    
    ``` oac_no_warn
    Destination type is topic
    To end program, enter Q or q, then <return>
    Reading message: This is message 1 from producer
    Reading message: This is message 2 from producer
    Reading message: This is message 3 from producer
    Message is not a TextMessage
    ```
    
    The last line appears because the client has received the non-text
    control message sent by the `Producer` client.

4.  Enter `Q` or `q` and press Return to stop the `AsynchConsumer`
    client.

5.  Now run the clients using a queue.
    
    In this case, as with the synchronous example, you can run the
    `Producer` client first, because there is no timing dependency
    between the sender and receiver:
    
    ``` oac_no_warn
    appclient -client target/producer.jar queue 3
    ```
    
    The output of the client looks like this:
    
    ``` oac_no_warn
    Destination type is queue
    Sending message: This is message 1 from producer
    Sending message: This is message 2 from producer
    Sending message: This is message 3 from producer
    Text messages sent: 3
    ```

6.  In the other window, run the `AsynchConsumer` client:
    
    ``` oac_no_warn
    appclient -client target/asynchconsumer.jar queue
    ```
    
    The output of the client looks like this (along with some additional
    output):
    
    ``` oac_no_warn
    Destination type is queue
    To end program, enter Q or q, then <return>
    Reading message: This is message 1 from producer
    Reading message: This is message 2 from producer
    Reading message: This is message 3 from producer
    Message is not a TextMessage
    ```

7.  Enter `Q` or `q` and press Return to stop the client.

## 46.3.8 Browsing Messages on a Queue

This section describes an example that creates a `QueueBrowser` object
to examine messages on a queue, as described in [JMS Queue
Browsers](jms-concepts003.htm#BNCEY). This section then explains how to
compile, package, and run the example using GlassFish Server.

The following topics are addressed here:

  - [Section 46.3.8.1, "The MessageBrowser.java Client"](#BNCFM)

  - [Section 46.3.8.2, "To Run the QueueBrowser Client"](#BNCFN)

### 46.3.8.1 The MessageBrowser.java Client

To create a `QueueBrowser` for a queue, you call the
`JMSContext.createBrowser` method with the queue as the argument. You
obtain the messages in the queue as an `Enumeration` object. You can
then iterate through the `Enumeration` object and display the contents
of each message.

The `MessageBrowser.java` client performs the following steps.

1.  Injects resources for a connection factory and a queue.

2.  In a `try`-with-resources block, creates a `JMSContext`.

3.  Creates a `QueueBrowser`:
    
    ``` oac_no_warn
    QueueBrowser browser = context.createBrowser(queue);
    ```

4.  Retrieves the `Enumeration` that contains the messages:
    
    ``` oac_no_warn
    Enumeration msgs = browser.getEnumeration();
    ```

5.  Verifies that the `Enumeration` contains messages, then displays the
    contents of the messages:
    
    ``` oac_no_warn
    if ( !msgs.hasMoreElements() ) { 
        System.out.println("No messages in queue");
    } else { 
        while (msgs.hasMoreElements()) { 
            Message tempMsg = (Message)msgs.nextElement(); 
            System.out.println("Message: " + tempMsg); 
        }
    }
    ```

6.  Catches and handles any exceptions. The end of the
    `try`-with-resources block automatically causes the `JMSContext` to
    be closed.

Dumping the message contents to standard output retrieves the message
body and properties in a format that depends on the implementation of
the `toString` method. In GlassFish Server, the message format looks
something like this:

``` oac_no_warn
Text:   This is message 3 from producer
Class:                  com.sun.messaging.jmq.jmsclient.TextMessageImpl
getJMSMessageID():      ID:8-10.152.23.26(bf:27:4:e:e7:ec)-55645-1363100335526
getJMSTimestamp():      1129061034355
getJMSCorrelationID():  null
JMSReplyTo:             null
JMSDestination:         PhysicalQueue
getJMSDeliveryMode():   PERSISTENT
getJMSRedelivered():    false
getJMSType():           null
getJMSExpiration():     0
getJMSPriority():       4
Properties:             {JMSXDeliveryCount=0}
```

Instead of displaying the message contents this way, you can call some
of the `Message` interface's getter methods to retrieve the parts of the
message you want to see.

For this example, you will use the connection factory and queue you
created for [Receiving Messages Synchronously](#BNCFB). It is assumed
that you have already built and packaged all the examples.

### 46.3.8.2 To Run the QueueBrowser Client

To run the `MessageBrowser` example using the `appclient` command,
follow these steps.

You also need the `Producer` example to send the message to the queue,
and one of the consumer clients to consume the messages after you
inspect them.

To run the clients, you need two terminal windows.

1.  In a terminal window, go to the `producer` directory:
    
    ``` oac_no_warn
    cd tut-install/examples/jms/simple/producer/
    ```

2.  Run the `Producer` client, sending one message to the queue, along
    with the non-text control message:
    
    ``` oac_no_warn
    appclient -client target/producer.jar queue
    ```
    
    The output of the client looks like this (along with some additional
    output):
    
    ``` oac_no_warn
    Destination type is queue
    Sending message: This is message 1 from producer
    Text messages sent: 1
    ```

3.  In another terminal window, go to the `messagebrowser` directory:
    
    ``` oac_no_warn
    cd tut-install/jms/simple/messagebrowser
    ```

4.  Run the `MessageBrowser` client using the following command:
    
    ``` oac_no_warn
    appclient -client target/messagebrowser.jar
    ```
    
    The output of the client looks something like this (along with some
    additional output):
    
    ``` oac_no_warn
    Message: 
    Text:   This is message 1 from producer
    Class:                  com.sun.messaging.jmq.jmsclient.TextMessageImpl
    getJMSMessageID():      ID:9-10.152.23.26(bf:27:4:e:e7:ec)-55645-1363100335526
    getJMSTimestamp():      1363100335526
    getJMSCorrelationID():  null
    JMSReplyTo:             null
    JMSDestination:         PhysicalQueue
    getJMSDeliveryMode():   PERSISTENT
    getJMSRedelivered():    false
    getJMSType():           null
    getJMSExpiration():     0
    getJMSPriority():       4
    Properties:             {JMSXDeliveryCount=0}
    
    Message: 
    Class:                  com.sun.messaging.jmq.jmsclient.MessageImpl
    getJMSMessageID():      ID:10-10.152.23.26(bf:27:4:e:e7:ec)-55645-1363100335526
    getJMSTimestamp():      1363100335526
    getJMSCorrelationID():  null
    JMSReplyTo:             null
    JMSDestination:         PhysicalQueue
    getJMSDeliveryMode():   PERSISTENT
    getJMSRedelivered():    false
    getJMSType():           null
    getJMSExpiration():     0
    getJMSPriority():       4
    Properties:             {JMSXDeliveryCount=0}
    ```
    
    The first message is the `TextMessage`, and the second is the
    non-text control message.

5.  Go to the `synchconsumer` directory.

6.  Run the `SynchConsumer` client to consume the messages:
    
    ``` oac_no_warn
    appclient -client target/synchconsumer.jar queue
    ```
    
    The output of the client looks like this (along with some additional
    output):
    
    ``` oac_no_warn
    Destination type is queue
    Reading message: This is message 1 from producer
    Messages received: 1
    ```

## 46.3.9 Running Multiple Consumers on the Same Destination

To illustrate further the way point-to-point and publish/subscribe
messaging works, you can use the `Producer` and `SynchConsumer` examples
to send messages that are then consumed by two clients running
simultaneously.

1.  Open three command windows. In one, go to the `producer` directory.
    In the other two, go to the `synchconsumer` directory.

2.  In each of the `synchconsumer` windows, start running the client,
    receiving messages from a queue:
    
    ``` oac_no_warn
    appclient -client target/synchconsumer.jar queue
    ```
    
    Wait until you see the "Destination type is queue" message in both
    windows.

3.  In the `producer` window, run the client, sending 20 or so messages
    to the queue:
    
    ``` oac_no_warn
    appclient -client target/producer.jar queue 20
    ```

4.  Look at the output in the `synchconsumer` windows. In point-to-point
    messaging, each message can have only one consumer. Therefore, each
    of the clients receives some of the messages. One of the clients
    receives the non-text control message, reports the number of
    messages received, and exits.

5.  In the window of the client that did not receive the non-text
    control message, enter Control-C to exit the program.

6.  Next, run the `synchconsumer` clients using a topic. In each window,
    run the following command:
    
    ``` oac_no_warn
    appclient -client target/synchconsumer.jar topic
    ```
    
    Wait until you see the "Destination type is topic" message in both
    windows.

7.  In the `producer` window, run the client, sending 20 or so messages
    to the topic:
    
    ``` oac_no_warn
    appclient -client target/producer.jar topic 20
    ```

8.  Again, look at the output in the `synchconsumer` windows. In
    publish/subscribe messaging, a copy of every message is sent to each
    subscription on the topic. Therefore, each of the clients receives
    all 20 text messages as well as the non-text control message.

## 46.3.10 Acknowledging Messages

JMS provides two alternative ways for a consuming client to ensure that
a message is not acknowledged until the application has finished
processing the message:

  - Using a synchronous consumer in a `JMSContext` that has been
    configured to use the `CLIENT_ACKNOWLEDGE` setting

  - Using a message listener for asynchronous message delivery in a
    `JMSContext` that has been configured to use the default
    `AUTO_ACKNOWLEDGE` setting

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
In the Java EE platform, <code dir="ltr">CLIENT_ACKNOWLEDGE</code> sessions can be used only in application clients, as in this example.</td>
</tr>
</tbody>
</table>

  

The `clientackconsumer` example demonstrates the first alternative, in
which a synchronous consumer uses client acknowledgment. The
`asynchconsumer` example described in [Using a Message Listener for
Asynchronous Message Delivery](#BNCFH) demonstrates the second
alternative.

For information about message acknowledgment, see [Controlling Message
Acknowledgment](jms-concepts004.htm#BNCFW).

The following table describes four possible interactions between types
of consumers and types of acknowledgment.

Table 46-3 Message Acknowledgment with Synchronous and Asynchronous
Consumers

<table style="width:50%;">
<colgroup>
<col width="21%" />
<col width="28%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Consumer Type</th>
<th>Acknowledgment Type</th>
<th>Behavior</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Synchronous</p></td>
<td><p>Client</p></td>
<td><p>Client acknowledges message after processing is complete</p></td>
</tr>
<tr class="even">
<td><p>Asynchronous</p></td>
<td><p>Client</p></td>
<td><p>Client acknowledges message after processing is complete</p></td>
</tr>
<tr class="odd">
<td><p>Synchronous</p></td>
<td><p>Auto</p></td>
<td><p>Acknowledgment happens immediately after <code dir="ltr">receive</code> call; message cannot be redelivered if any subsequent processing steps fail</p></td>
</tr>
<tr class="even">
<td><p>Asynchronous</p></td>
<td><p>Auto</p></td>
<td><p>Message is automatically acknowledged when <code dir="ltr">onMessage</code> method returns</p></td>
</tr>
</tbody>
</table>

  

The example is under the
tut-install`/examples/jms/simple/clientackconsumer/` directory.

The example client, `ClientAckConsumer.java`, creates a `JMSContext`
that specifies client acknowledgment:

``` oac_no_warn
try (JMSContext context =
      connectionFactory.createContext(JMSContext.CLIENT_ACKNOWLEDGE);) {
    ...
```

The client uses a `while` loop almost identical to that used by
`SynchConsumer.java`, with the exception that after processing each
message, it calls the `acknowledge` method on the `JMSContext`:

``` oac_no_warn
context.acknowledge();
```

The example uses the following objects:

  - The `jms/MyQueue` resource that you created for [Receiving Messages
    Synchronously](#BNCFB).

  - `java:comp/DefaultJMSConnectionFactory`, the platform default
    connection factory preconfigured with GlassFish Server

### 46.3.10.1 To Run the ClientAckConsumer Client

1.  In a terminal window, go to the following directory:
    
    ``` oac_no_warn
    tut-install/examples/jms/simple/producer/
    ```

2.  Run the `Producer` client, sending some messages to the queue:
    
    ``` oac_no_warn
    appclient -client target/producer.jar queue 3
    ```

3.  In another terminal window, go to the following directory:
    
    ``` oac_no_warn
    tut-install/examples/jms/simple/clientackconsumer/
    ```

4.  To run the client, use the following command:
    
    ``` oac_no_warn
    appclient -client target/clientackconsumer.jar
    ```
    
    The client output looks like this (along with some additional
    output):
    
    ``` oac_no_warn
    Created client-acknowledge JMSContext
    Reading message: This is message 1 from producer
    Acknowledging TextMessage
    Reading message: This is message 2 from producer
    Acknowledging TextMessage
    Reading message: This is message 3 from producer
    Acknowledging TextMessage
    Acknowledging non-text control message
    ```
    
    The client acknowledges each message explicitly after processing it,
    just as a `JMSContext` configured to use `AUTO_ACKNOWLEDGE` does
    automatically after a `MessageListener` returns successfully from
    processing a message received asynchronously.

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
<td><a href="jms-examples002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jms-examples004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
