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
<td><a href="jms-concepts004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jms-concepts006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 45.5 Using the JMS API in Java EE Applications

This section describes how using the JMS API in enterprise bean
applications or web applications differs from using it in application
clients.

The following topics are addressed here:

  - [Section 45.5.1, "Overview of Using the JMS API"](#CHDGICJB)

  - [Section 45.5.2, "Creating Resources for Java EE
    Applications"](#BABHFBDH)

  - [Section 45.5.3, "Using Resource Injection in Enterprise Bean or Web
    Components"](#BNCGM)

  - [Section 45.5.4, "Using Java EE Components to Produce and to
    Synchronously Receive Messages"](#BNCGN)

  - [Section 45.5.5, "Using Message-Driven Beans to Receive Messages
    Asynchronously"](#BNCGQ)

  - [Section 45.5.6, "Managing JTA Transactions"](#BNCGS)

## 45.5.1 Overview of Using the JMS API

A general rule in the Java EE platform specification applies to all Java
EE components that use the JMS API within EJB or web containers:
Application components in the web and EJB containers must not attempt to
create more than one active (not closed) `Session` object per
connection. Multiple `JMSContext` objects are permitted, however, since
they combine a single connection and a single session.

This rule does not apply to application clients. The application client
container supports the creation of multiple sessions for each
connection.

## 45.5.2 Creating Resources for Java EE Applications

You can use annotations to create application-specific connection
factories and destinations for Java EE enterprise bean or web
components. The resources you create in this way are visible only to the
application for which you create them.

You can also use deployment descriptor elements to create these
resources. Elements specified in the deployment descriptor override
elements specified in annotations. See [Packaging
Applications](packaging001.htm#BCGDJDFB) for basic information about
deployment descriptors. You must use a deployment descriptor to create
application-specific resources for application clients.

To create a destination, use a `@JMSDestinationDefinition` annotation
like the following on a class:

``` oac_no_warn
@JMSDestinationDefinition(
    name = "java:app/jms/myappTopic",
    interfaceName = "javax.jms.Topic",
    destinationName = "MyPhysicalAppTopic"
  )
```

The `name`, `interfaceName`, and `destinationName` elements are
required. You can optionally specify a `description` element. To create
multiple destinations, enclose them in a `@JMSDestinationDefinitions`
annotation, separated by commas.

To create a connection factory, use a `@JMSConnectionFactoryDefinition`
annotation like the following on a class:

``` oac_no_warn
@JMSConnectionFactoryDefinition(
    name="java:app/jms/MyConnectionFactory"
)
```

The `name` element is required. You can optionally specify a number of
other elements, such as `clientId` if you want to use the connection
factory for durable subscriptions, or `description`. If you do not
specify the `interfaceName` element, the default interface is
`javax.jms.ConnectionFactory`. To create multiple connection factories,
enclose them in a `@JMSConnectionFactoryDefinitions` annotation,
separated by commas.

You need to specify the annotation only once for a given application, in
any of the components.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
If your application contains one or more message-driven beans, you may want to place the annotation on one of the message-driven beans. If you place the annotation on a sending component such as an application client, you need to specify the <code dir="ltr">mappedName</code> element to look up the topic, instead of using the <code dir="ltr">destinationLookup</code> property of the activation configuration specification.</td>
</tr>
</tbody>
</table>

  

When you inject the resource into a component, use the value of the
`name` element in the definition annotation as the value of the `lookup`
element in the `@Resource` annotation:

``` oac_no_warn
@Resource(lookup = "java:app/jms/myappTopic")
private Topic topic;
```

The following portable JNDI namespaces are available. Which ones you can
use depends on how your application is packaged.

  - `java:global`: Makes the resource available to all deployed
    applications

  - `java:app`: Makes the resource available to all components in all
    modules in a single application

  - `java:module`: Makes the resource available to all components within
    a given module (for example, all enterprise beans within an EJB
    module)

  - `java:comp`: Makes the resource available to a single component only
    (except in a web application, where it is equivalent to
    `java:module`)

See the API documentation for details on these annotations. The examples
in [Sending and Receiving Messages Using a Simple Web
Application](jms-examples006.htm#BABBABFC), [Sending Messages from a
Session Bean to an MDB](jms-examples008.htm#BNCGW), and [Using an Entity
to Join Messages from Two MDBs](jms-examples009.htm#BNCHF) all use the
`@JMSDestinationDefinition` annotation. The other JMS examples do not
use these annotations. The examples that consist only of application
clients are not deployed in the application server and must therefore
communicate with each other using administratively created resources
that exist outside of individual applications.

## 45.5.3 Using Resource Injection in Enterprise Bean or Web Components

You may use resource injection to inject both administered objects and
`JMSContext` objects in Java EE applications.

The following topics are addressed here:

  - [Section 45.5.3.1, "Injecting a ConnectionFactory, Queue, or
    Topic"](#CHDCHDIJ)

  - [Section 45.5.3.2, "Injecting a JMSContext Object"](#BABCJBEE)

### 45.5.3.1 Injecting a ConnectionFactory, Queue, or Topic

Normally, you use the `@Resource` annotation to inject a
`ConnectionFactory`, `Queue`, or `Topic` into your Java EE application.
These objects must be created administratively before you deploy your
application. You may want to use the default connection factory, whose
JNDI name is `java:comp/DefaultJMSConnectionFactory`.

When you use resource injection in an application client component, you
normally declare the JMS resource static:

``` oac_no_warn
@Resource(lookup = "java:comp/DefaultJMSConnectionFactory")
private static ConnectionFactory connectionFactory;

@Resource(lookup = "jms/MyQueue")
private static Queue queue;
```

However, when you use this annotation in a session bean, a
message-driven bean, or a web component, do not declare the resource
static:

``` oac_no_warn
@Resource(lookup = "java:comp/DefaultJMSConnectionFactory")
private ConnectionFactory connectionFactory;

@Resource(lookup = "jms/MyTopic")
private Topic topic;
```

If you declare the resource static in these components, runtime errors
will result.

### 45.5.3.2 Injecting a JMSContext Object

To access a `JMSContext` object in an enterprise bean or web component,
instead of injecting the `ConnectionFactory` resource and then creating
a `JMSContext`, you can use the `@Inject` and `@JMSConnectionFactory`
annotations to inject a `JMSContext`. To use the default connection
factory, use code like the following:

``` oac_no_warn
@Inject
private JMSContext context1;
```

To use your own connection factory, use code like the following:

``` oac_no_warn
@Inject
@JMSConnectionFactory("jms/MyConnectionFactory")
private JMSContext context2;
```

## 45.5.4 Using Java EE Components to Produce and to Synchronously Receive Messages

An application that produces messages or synchronously receives them can
use a Java EE web or EJB component, such as a managed bean, a servlet,
or a session bean, to perform these operations. The example in [Sending
Messages from a Session Bean to an MDB](jms-examples008.htm#BNCGW) uses
a stateless session bean to send messages to a topic. The example in
[Sending and Receiving Messages Using a Simple Web
Application](jms-examples006.htm#BABBABFC) uses managed beans to produce
and to consume messages.

Because a synchronous receive with no specified timeout ties up server
resources, this mechanism usually is not the best application design for
a web or EJB component. Instead, use a synchronous receive that
specifies a timeout value, or use a message-driven bean to receive
messages asynchronously. For details about synchronous receives, see
[JMS Message Consumers](jms-concepts003.htm#BNCEP).

Using the JMS API in a Java EE component is in many ways similar to
using it in an application client. The main differences are the areas of
resource management and transactions.

### 45.5.4.1 Managing JMS Resources in Web and EJB Components

The JMS resources are a connection and a session, usually combined in a
`JMSContext` object. In general, it is important to release JMS
resources when they are no longer being used. Here are some useful
practices to follow.

  - If you wish to maintain a JMS resource only for the life span of a
    business method, use a `try`-with-resources statement to create the
    `JMSContext` so that it will be closed automatically at the end of
    the `try` block.

  - To maintain a JMS resource for the duration of a transaction or
    request, inject the `JMSContext` as described in [Injecting a
    JMSContext Object](#BABCJBEE). This will also cause the resource to
    be released when it is no longer needed.

  - If you would like to maintain a JMS resource for the life span of an
    enterprise bean instance, you can use a `@PostConstruct` callback
    method to create the resource and a `@PreDestroy` callback method to
    close the resource. However, there is normally no need to do this,
    since application servers usually maintain a pool of connections. If
    you use a stateful session bean and you wish to maintain the JMS
    resource in a cached state, you must close the resource in a
    `@PrePassivate` callback method and set its value to `null`, and you
    must create it again in a `@PostActivate` callback method.

### 45.5.4.2 Managing Transactions in Session Beans

Instead of using local transactions, you use JTA transactions. You can
use either container-managed transactions or bean-managed transactions.
Normally, you use container-managed transactions for bean methods that
perform sends or receives, allowing the EJB container to handle
transaction demarcation. Because container-managed transactions are the
default, you do not have to specify them.

You can use bean-managed transactions and the
`javax.transaction.UserTransaction` interface's transaction demarcation
methods, but you should do so only if your application has special
requirements and you are an expert in using transactions. Usually,
container-managed transactions produce the most efficient and correct
behavior. This tutorial does not provide any examples of bean-managed
transactions.

## 45.5.5 Using Message-Driven Beans to Receive Messages Asynchronously

The sections [What Is a Message-Driven Bean?](ejb-intro003.htm#GIPKO)
and [How Does the JMS API Work with the Java EE
Platform?](jms-concepts001.htm#BNCDW) describe how the Java EE platform
supports a special kind of enterprise bean, the message-driven bean,
which allows Java EE applications to process JMS messages
asynchronously. Other Java EE web and EJB components allow you to send
messages and to receive them synchronously but not asynchronously.

A message-driven bean is a message listener to which messages can be
delivered from either a queue or a topic. The messages can be sent by
any Java EE component (from an application client, another enterprise
bean, or a web component) or from an application or a system that does
not use Java EE technology.

A message-driven bean class has the following requirements.

  - It must be annotated with the `@MessageDriven` annotation if it does
    not use a deployment descriptor.

  - The class must be defined as `public`, but not as `abstract` or
    `final`.

  - It must contain a public constructor with no arguments.

It is recommended, but not required, that a message-driven bean class
implement the message listener interface for the message type it
supports. A bean that supports the JMS API implements the
`javax.jms.MessageListener` interface, which means that it must provide
an `onMessage` method with the following signature:

``` oac_no_warn
void onMessage(Message inMessage)
```

The `onMessage` method is called by the bean's container when a message
has arrived for the bean to service. This method contains the business
logic that handles the processing of the message. It is the
message-driven bean's responsibility to parse the message and perform
the necessary business logic.

A message-driven bean differs from an application client's message
listener in the following ways.

  - In an application client, you must create a `JMSContext`, then
    create a `JMSConsumer`, then call `setMessageListener` to activate
    the listener. For a message-driven bean, you need only define the
    class and annotate it, and the EJB container creates it for you.

  - The bean class uses the `@MessageDriven` annotation, which typically
    contains an `activationConfig` element containing
    `@ActivationConfigProperty` annotations that specify properties used
    by the bean or the connection factory. These properties can include
    the connection factory, a destination type, a durable subscription,
    a message selector, or an acknowledgment mode. Some of the examples
    in [Chapter 46, "Java Message Service
    Examples"](jms-examples.htm#BNCGV) set these properties. You can
    also set the properties in the deployment descriptor.

  - The application client container has only one instance of a
    `MessageListener`, which is called on a single thread at a time. A
    message-driven bean, however, may have multiple instances,
    configured by the container, which may be called concurrently by
    multiple threads (although each instance is called by only one
    thread at a time). Message-driven beans may therefore allow much
    faster processing of messages than message listeners.

  - You do not need to specify a message acknowledgment mode unless you
    use bean-managed transactions. The message is consumed in the
    transaction in which the `onMessage` method is invoked.

[Table 45-3](#GJKOH) lists the activation configuration properties
defined by the JMS specification.

Table 45-3 @ActivationConfigProperty Settings for Message-Driven Beans

<table style="width:33%;">
<colgroup>
<col width="33%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Property Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">acknowledgeMode</code></p></td>
<td><p>Acknowledgment mode, used only for bean-managed transactions; the default is <code dir="ltr">Auto-acknowledge</code> (<code dir="ltr">Dups-ok-acknowledge</code> is also permitted)</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">destinationLookup</code></p></td>
<td><p>The lookup name of the queue or topic from which the bean will receive messages</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">destinationType</code></p></td>
<td><p>Either <code dir="ltr">javax.jms.Queue</code> or <code dir="ltr">javax.jms.Topic</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">subscriptionDurability</code></p></td>
<td><p>For durable subscriptions, set the value to <code dir="ltr">Durable</code>; see <a href="jms-concepts003.htm#BNCGD">Creating Durable Subscriptions</a> for more information</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">clientId</code></p></td>
<td><p>For durable subscriptions, the client ID for the connection (optional)</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">subscriptionName</code></p></td>
<td><p>For durable subscriptions, the name of the subscription</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">messageSelector</code></p></td>
<td><p>A string that filters messages; see <a href="jms-concepts003.htm#BNCER">JMS Message Selectors</a> for information</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">connectionFactoryLookup</code></p></td>
<td><p>The lookup name of the connection factory to be used to connect to the JMS provider from which the bean will receive messages</p></td>
</tr>
</tbody>
</table>

  

For example, here is the message-driven bean used in [Receiving Messages
Asynchronously Using a Message-Driven Bean](jms-examples007.htm#BNBPK):

``` oac_no_warn
@MessageDriven(activationConfig = {
    @ActivationConfigProperty(propertyName = "destinationLookup",
            propertyValue = "jms/MyQueue"),
    @ActivationConfigProperty(propertyName = "destinationType",
            propertyValue = "javax.jms.Queue")
})
public class SimpleMessageBean implements MessageListener {

    @Resource
    private MessageDrivenContext mdc;
    static final Logger logger = Logger.getLogger("SimpleMessageBean");

    public SimpleMessageBean() {
    }

    @Override
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
}
```

If JMS is integrated with the application server using a resource
adapter, the JMS resource adapter handles these tasks for the EJB
container.

The bean class commonly injects a `MessageDrivenContext` resource, which
provides some additional methods you can use for transaction management
(`setRollbackOnly`, for example):

``` oac_no_warn
    @Resource
    private MessageDrivenContext mdc;
```

A message-driven bean never has a local or remote interface. Instead, it
has only a bean class.

A message-driven bean is similar in some ways to a stateless session
bean: Its instances are relatively short-lived and retain no state for a
specific client. The instance variables of the message-driven bean
instance can contain some state across the handling of client messages:
for example, an open database connection, or an object reference to an
enterprise bean object.

Like a stateless session bean, a message-driven bean can have many
interchangeable instances running at the same time. The container can
pool these instances to allow streams of messages to be processed
concurrently. The container attempts to deliver messages in
chronological order when that would not impair the concurrency of
message processing, but no guarantees are made as to the exact order in
which messages are delivered to the instances of the message-driven bean
class. If message order is essential to your application, you may want
to configure your application server to use just one instance of the
message-driven bean.

For details on the lifecycle of a message-driven bean, see [The
Lifecycle of a Message-Driven Bean](ejb-intro007.htm#GIPKW).

## 45.5.6 Managing JTA Transactions

Java EE application clients and Java SE clients use JMS local
transactions (described in [Using JMS Local
Transactions](jms-concepts004.htm#BNCGH)), which allow the grouping of
sends and receives within a specific JMS session. Java EE applications
that run in the web or EJB container commonly use JTA transactions to
ensure the integrity of accesses to external resources. The key
difference between a JTA transaction and a JMS local transaction is that
a JTA transaction is controlled by the application server's transaction
managers. JTA transactions may be distributed, which means that they can
encompass multiple resources in the same transaction, such as a JMS
provider and a database.

For example, distributed transactions allow multiple applications to
perform atomic updates on the same database, and they allow a single
application to perform atomic updates on multiple databases.

In a Java EE application that uses the JMS API, you can use transactions
to combine message sends or receives with database updates and other
resource manager operations. You can access resources from multiple
application components within a single transaction. For example, a
servlet can start a transaction, access multiple databases, invoke an
enterprise bean that sends a JMS message, invoke another enterprise bean
that modifies an EIS system using the Connector Architecture, and
finally commit the transaction. Your application cannot, however, both
send a JMS message and receive a reply to it within the same
transaction.

JTA transactions within the EJB and web containers can be either of two
kinds.

  - Container-managed transactions: The container controls the integrity
    of your transactions without your having to call `commit` or
    `rollback`. Container-managed transactions are easier to use than
    bean-managed transactions. You can specify appropriate transaction
    attributes for your enterprise bean methods.
    
    Use the `Required` transaction attribute (the default) to ensure
    that a method is always part of a transaction. If a transaction is
    in progress when the method is called, the method will be part of
    that transaction; if not, a new transaction will be started before
    the method is called and will be committed when the method returns.
    See [Transaction Attributes](transactions004.htm#BNCIK) for more
    information.

  - Bean-managed transactions: You can use these in conjunction with the
    `javax.transaction.UserTransaction` interface, which provides its
    own `commit` and `rollback` methods you can use to delimit
    transaction boundaries. Bean-managed transactions are recommended
    only for those who are experienced in programming transactions.

You can use either container-managed transactions or bean-managed
transactions with message-driven beans. To ensure that all messages are
received and handled within the context of a transaction, use
container-managed transactions and use the `Required` transaction
attribute (the default) for the `onMessage` method.

When you use container-managed transactions, you can call the following
`MessageDrivenContext` methods.

  - `setRollbackOnly`: Use this method for error handling. If an
    exception occurs, `setRollbackOnly` marks the current transaction so
    that the only possible outcome of the transaction is a rollback.

  - `getRollbackOnly`: Use this method to test whether the current
    transaction has been marked for rollback.

If you use bean-managed transactions, the delivery of a message to the
`onMessage` method takes place outside the JTA transaction context. The
transaction begins when you call the `UserTransaction.begin` method
within the `onMessage` method, and it ends when you call
`UserTransaction.commit` or `UserTransaction.rollback`. Any call to the
`Connection.createSession` method must take place within the
transaction.

Using bean-managed transactions allows you to process the message by
using more than one transaction or to have some parts of the message
processing take place outside a transaction context. However, if you use
container-managed transactions, the message is received by the MDB and
processed by the `onMessage` method within the same transaction. It is
not possible to achieve this behavior with bean-managed transactions.

When you create a `JMSContext` in a JTA transaction (in the web or EJB
container), the container ignores any arguments you specify, because it
manages all transactional properties. When you create a `JMSContext` in
the web or EJB container and there is no JTA transaction, the value (if
any) passed to the `createContext` method should be
`JMSContext.AUTO_ACKNOWLEDGE` or `JMSContext.DUPS_OK_ACKNOWLEDGE`.

When you use container-managed transactions, you normally use the
`Required` transaction attribute (the default) for your enterprise
bean's business methods.

You do not specify the activation configuration property
`acknowledgeMode` when you create a message-driven bean that uses
container-managed transactions. The container acknowledges the message
automatically when it commits the transaction.

If a message-driven bean uses bean-managed transactions, the message
receipt cannot be part of the bean-managed transaction. You can set the
activation configuration property `acknowledgeMode` to
`Auto-acknowledge` or `Dups-ok-acknowledge` to specify how you want the
message received by the message-driven bean to be acknowledged.

If the `onMessage` method throws a `RuntimeException`, the container
does not acknowledge processing the message. In that case, the JMS
provider will redeliver the unacknowledged message in the future.

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
<td><a href="jms-concepts004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jms-concepts006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
