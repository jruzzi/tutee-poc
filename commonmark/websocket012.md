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
<td><a href="websocket011.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket013.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 18.12 The websocketbot Example Application

The `websocketbot` example application, located in the
tut-install`/examples/web/websocket/websocketbot/` directory,
demonstrates how to use a WebSocket endpoint to implement a chat. The
example resembles a chat room in which many users can join and have a
conversation. Users can ask simple questions to a bot agent that is
always available in the chat room.

The following topics are addressed here:

  - [Section 18.12.1, "Architecture of the websocketbot Example
    Application"](#CIHICIDE)

  - [Section 18.12.2, "Running the websocketbot Example
    Application"](#CIHHJHDB)

## 18.12.1 Architecture of the websocketbot Example Application

The `websocketbot` example application consists of the following
elements:

  - [Section 18.12.1.1, "The CDI Bean"](#CIHDAEHF) – A CDI bean
    (`BotBean`) that contains the logic for the bot agent to reply to
    messages

  - [Section 18.12.1.2, "The WebSocket Endpoint"](#CIHJJJHG) – A
    WebSocket endpoint (`BotEndpoint`) that implements the chat room

  - [Section 18.12.1.3, "The Application Messages"](#CIHFDGHG) – A set
    of classes (`Message`, `ChatMessage`, `InfoMessage`, `JoinMessage`,
    and `UsersMessage`) that represent application messages

  - [Section 18.12.1.4, "The Encoder Classes"](#CIHGHHBD) – A set of
    classes (`ChatMessageEncoder`, `InfoMessageEncoder`,
    `JoinMessageEncoder`, and `UsersMessageEncoder`) that encode
    application messages into WebSocket text messages as JSON data

  - [Section 18.12.1.5, "The Message Decoder"](#CIHHFICG) – A class
    (`MessageDecoder`) the parses WebSocket text messages as JSON data
    and decodes them into `JoinMessage` or `ChatMessage` objects

  - [Section 18.11.1.3, "The HTML Page"](websocket011.htm#CIHHIEFH) – An
    HTML page (`index.html`) that uses JavaScript code to implement the
    client for the chat room

### 18.12.1.1 The CDI Bean

The CDI bean (`BotBean`) is a Java class that contains the `respond`
method. This method compares the incoming chat message with a set of
predefined questions and returns a chat response.

``` oac_no_warn
@Named
public class BotBean {
    public String respond(String msg) { ... }
}
```

### 18.12.1.2 The WebSocket Endpoint

The WebSocket endpoint (`BotEndpoint`) is an annotated endpoint that
performs the following functions:

  - Receives messages from clients

  - Forwards messages to clients

  - Maintains a list of connected clients

  - Invokes the bot agent functionality

The endpoint specifies its deployment URI and the message encoders and
decoders using the `ServerEndpoint` annotation. The endpoint obtains an
instance of the `BotBean` class and a managed executor service resource
through dependency injection:

``` oac_no_warn
@ServerEndpoint(
   value = "/websocketbot",
   decoders = { MessageDecoder.class }, 
   encoders = { JoinMessageEncoder.class, ChatMessageEncoder.class, 
                InfoMessageEncoder.class, UsersMessageEncoder.class }
)
/* There is a BotEndpoint instance per connection */
public class BotEndpoint {
   private static final Logger logger = Logger.getLogger("BotEndpoint");
   /* Bot functionality bean */
   @Inject private BotBean botbean;
   /* Executor service for asynchronous processing */
   @Resource(name="comp/DefaultManagedExecutorService")
   private ManagedExecutorService mes;
   
   @OnOpen
   public void openConnection(Session session) {
       logger.log(Level.INFO, "Connection opened.");
   }
   ...
}
```

The `message` method processes incoming messages from clients. The
decoder converts incoming text messages into `JoinMessage` or
`ChatMessage` objects, which inherit from the `Message` class. The
`message` method receives a `Message` object as a parameter:

``` oac_no_warn
@OnMessage
public void message(Session session, Message msg) {
   logger.log(Level.INFO, "Received: {0}", msg.toString());
   
   if (msg instanceof JoinMessage) {
      /* Add the new user and notify everybody */
      JoinMessage jmsg = (JoinMessage) msg;
      session.getUserProperties().put("name", jmsg.getName());
      session.getUserProperties().put("active", true);
      logger.log(Level.INFO, "Received: {0}", jmsg.toString());
      sendAll(session, new InfoMessage(jmsg.getName() + 
              " has joined the chat"));
      sendAll(session, new ChatMessage("Duke", jmsg.getName(), 
              "Hi there!!"));
      sendAll(session, new UsersMessage(this.getUserList(session)));
      
   } else if (msg instanceof ChatMessage) {
      /* Forward the message to everybody */
      ChatMessage cmsg = (ChatMessage) msg;
      logger.log(Level.INFO, "Received: {0}", cmsg.toString());
      sendAll(session, cmsg);
      if (cmsg.getTarget().compareTo("Duke") == 0) {
         /* The bot replies to the message */
         mes.submit(new Runnable() {
            @Override
            public void run() {
               String resp = botbean.respond(cmsg.getMessage());
               sendAll(session, new ChatMessage("Duke",
                       cmsg.getName(), resp));
            }
         });
      }
   }
}
```

If the message is a join message, the endpoint adds the new user to the
list and notifies all connected clients. If the message is a chat
message, the endpoint forwards it to all connected clients.

If a chat message is for the bot agent, the endpoint obtains a response
using the `BotBean` instance and sends it to all connected clients. The
`sendAll` method is similar to the example in [Sending Messages to All
Peers Connected to an Endpoint](websocket005.htm#BABIFBCG).

Asynchronous Processing and Concurrency Considerations

The WebSocket endpoint calls the `BotBean.respond` method to obtain a
response from the bot. In this example, this is a blocking operation;
the user that sent the associated message would not be able to send or
receive other chat messages until the operation completes. To avoid this
problem, the endpoint obtains an executor service from the container and
executes the blocking operation in a different thread using the
`ManagedExecutorService.submit` method from Concurrency Utilities for
Java EE.

The Java API for WebSocket specification requires that Java EE
implementations instantiate endpoint classes once per connection. This
facilitates the development of WebSocket endpoints, because you are
guaranteed that only one thread is executing the code in a WebSocket
endpoint class at any given time. When you introduce a new thread in an
endpoint, as in this example, you must ensure that variables and methods
accessed by more than one thread are thread safe. In this example, the
code in `BotBean` is thread safe, and the `BotEndpoint.sendAll` method
has been declared `synchronized`.

Refer to [Chapter 56, "Concurrency Utilities for Java
EE"](concurrency-utilities.htm#GKJIQ8) for more information on the
managed executor service and Concurrency Utilities for Java EE.

### 18.12.1.3 The Application Messages

The classes that represent application messages (`Message`,
`ChatMessage`, `InfoMessage`, `JoinMessage`, and `UsersMessage`) contain
only properties and getter and setter methods. For example, the
`ChatMessage` class looks like this:

``` oac_no_warn
public class ChatMessage extends Message {
    private String name;
    private String target;
    private String message;
    /* ... Constructor, getters, and setters ... */
}
```

### 18.12.1.4 The Encoder Classes

The encoder classes convert application message objects into JSON text
using the Java API for JSON Processing. For example, the
`ChatMessageEncoder` class is implemented as follows:

``` oac_no_warn
/* Encode a ChatMessage as JSON.
 * For example, (new ChatMessage("Peter","Duke","How are you?"))
 * is encoded as follows:
 * {"type":"chat","target":"Duke","message":"How are you?"}
 */
public class ChatMessageEncoder implements Encoder.Text<ChatMessage> {
   @Override
   public void init(EndpointConfig ec) { }
   @Override
   public void destroy() { }
   @Override
   public String encode(ChatMessage chatMessage) throws EncodeException {
      // Access properties in chatMessage and write JSON text...
   }
}
```

See [Chapter 19](jsonp.htm#GLRBB), [JSON Processing](jsonp.htm#GLRBB)
for more information on the Java API for JSON Processing.

### 18.12.1.5 The Message Decoder

The message decoder (`MessageDecoder`) class converts WebSocket text
messages into application messages by parsing JSON text. It is
implemented as follows:

``` oac_no_warn
/* Decode a JSON message into a JoinMessage or a ChatMessage.
 * For example, the incoming message
 * {"type":"chat","name":"Peter","target":"Duke","message":"How are you?"}
 * is decoded as (new ChatMessage("Peter", "Duke", "How are you?"))
 */
public class MessageDecoder implements Decoder.Text<Message> {
    /* Stores the name-value pairs from a JSON message as a Map */
    private Map<String,String> messageMap;

    @Override
    public void init(EndpointConfig ec) { }
    @Override
    public void destroy() { }

    /* Create a new Message object if the message can be decoded */
    @Override
    public Message decode(String string) throws DecodeException {
       Message msg = null;
       if (willDecode(string)) {
          switch (messageMap.get("type")) {
             case "join":
                msg = new JoinMessage(messageMap.get("name"));
                break;
             case "chat":
                msg = new ChatMessage(messageMap.get("name"),
                                      messageMap.get("target"),
                                      messageMap.get("message"));
          }
       } else {
          throw new DecodeException(string, "[Message] Can't decode.");
       }
       return msg;
   }
   
   /* Decode a JSON message into a Map and check if it contains
    * all the required fields according to its type. */
   @Override
   public boolean willDecode(String string) {
      // Convert JSON data from the message into a name-value map...
      // Check if the message has all the fields for its message type...
   }
}
```

### 18.12.1.6 The HTML Page

The HTML page (`index.html`) contains a field for the user name. After
the user types a name and clicks Join, three text areas are available:
one to type and send messages, one for the chat room, and one with the
list of users. The page also contains a WebSocket console that shows the
messages sent and received as JSON text.

The JavaScript code on the page uses the WebSocket API to connect to the
endpoint, send messages, and designate callback methods. The WebSocket
API is supported by most modern browsers and is widely used for web
client development with HTML5.

## 18.12.2 Running the websocketbot Example Application

This section describes how to run the `websocketbot` example application
using NetBeans IDE and from the command line.

The following topics are addressed here:

  - [Section 18.12.2.1, "To Run the websocketbot Example Application
    Using NetBeans IDE"](#CIHFDDGE)

  - [Section 18.12.2.2, "To Run the websocketbot Example Application
    Using Maven"](#CIHEDEHB)

  - [Section 18.12.2.3, "To Test the websocketbot Example
    Application"](#BABDDAAG)

### 18.12.2.1 To Run the websocketbot Example Application Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/websocket
    ```

4.  Select the `websocketbot` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `websocketbot` project and
    select Run.
    
    This command builds and packages the application into a WAR file,
    `websocketbot.war`, located in the `target/` directory; deploys it
    to the server; and launches a web browser window with the following
    URL:
    
    ``` oac_no_warn
    http://localhost:8080/websocketbot/
    ```
    
    See [To Test the websocketbot Example Application](#BABDDAAG) for
    more information.

### 18.12.2.2 To Run the websocketbot Example Application Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/websocket/websocketbot/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```

4.  Open a web browser window and type the following address:
    
    ``` oac_no_warn
    http://localhost:8080/websocketbot/
    ```
    
    See [To Test the websocketbot Example Application](#BABDDAAG) for
    more information.

### 18.12.2.3 To Test the websocketbot Example Application

1.  On the main page, type your name on the first text field and press
    the Enter key.
    
    The list of connected users appears on the text area on the right.
    The text area on the left is the chat room.

2.  Type a message on the text area below the login button. For example,
    type the messages in bold and press enter to obtain responses
    similar to the following:
    
    ``` oac_no_warn
    [--Peter has joined the chat--]
    Duke: @Peter Hi there!!
    Peter: @Duke how are you?
    Duke: @Peter I'm doing great, thank you!
    Peter: @Duke when is your birthday?
    Duke: @Peter My birthday is on May 23rd. Thanks for asking!
    ```

3.  Join the chat from another browser window by copying and pasting the
    URI on the address bar and joining with a different name.
    
    The new user name appears in the list of users in both browser
    windows. You can send messages from either window and see how they
    appear in the other.

4.  Click Show WebSocket Console.
    
    The console shows the messages sent and received as JSON text.

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
<td><a href="websocket011.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="websocket013.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
