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
<td><a href="ejb-async001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partpersist.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 36.2 The async Example Application

The `async` example demonstrates how to define an asynchronous business
method on a session bean and call it from a web client. This example
contains two modules.

  - A web application (`async-war`) that contains a stateless session
    bean and a JavaServer Faces interface. The `MailerBean` stateless
    session bean defines an asynchronous method, `sendMessage`, which
    uses the JavaMail API to send an email to an specified email
    address.

  - An auxiliary Java SE program (`async-smtpd`) that simulates an SMTP
    server. This program listens on TCP port 3025 for SMTP requests and
    prints the email messages to the standard output (instead of
    delivering them).

The following section describes the architecture of the `async-war`
module.

## 36.2.1 Architecture of the async-war Module

The `async-war` module consists of a single stateless session bean,
`MailerBean`, and a JavaServer Faces web application front end that uses
Facelets tags in XHTML files to display a form for users to enter the
email address for the recipient of an email. The status of the email is
updated when the email is finally sent.

The `MailerBean` session bean injects a JavaMail resource used to send
an email message to an address specified by the user. The message is
created, modified, and sent using the JavaMail API. The session bean
looks like this:

``` oac_no_warn
@Named
@Stateless
public class MailerBean {
    @Resource(name="mail/myExampleSession")
    private Session session;
    private static final Logger logger = 
            Logger.getLogger(MailerBean.class.getName());

    @Asynchronous
    public Future<String> sendMessage(String email) {
        String status;
        try {
            Properties properties = new Properties();            properties.put("mail.smtp.port", "3025");            session = Session.getInstance(properties);                        Message message = new MimeMessage(session);
            message.setFrom();
            message.setRecipients(Message.RecipientType.TO,
                    InternetAddress.parse(email, false));
            message.setSubject("Test message from async example");
            message.setHeader("X-Mailer", "JavaMail");
            DateFormat dateFormatter = DateFormat
                    .getDateTimeInstance(DateFormat.LONG, DateFormat.SHORT);
            Date timeStamp = new Date();
            String messageBody = "This is a test message from the async "
                    + "example of the Java EE Tutorial. It was sent on "
                    + dateFormatter.format(timeStamp)
                    + ".";
            message.setText(messageBody);
            message.setSentDate(timeStamp);
            Transport.send(message);
            status = "Sent";
            logger.log(Level.INFO, "Mail sent to {0}", email);
        } catch (MessagingException ex) {
            logger.severe("Error in sending message.");
            status = "Encountered an error: " + ex.getMessage();
            logger.severe(ex.getMessage());
        }
        return new AsyncResult<>(status);
    }
}
```

The injected JavaMail resource can be configured through the GlassFish
Server Administration Console, through a GlassFish Server administrative
command, or through a resource configuration file packaged with the
application. The resource configuration can be modified at runtime by
the GlassFish Server administrator to use a different mail server or
transport protocol.

The web client consists of a Facelets template, `template.xhtml`; two
Facelets clients, `index.xhtml` and `response.xhtml`; and a JavaServer
Faces managed bean, `MailerManagedBean`. The `index.xhtml` file contains
a form for the target email address. When the user submits the form, the
`MailerManagedBean.send` method is called. This method uses an injected
instance of the `MailerBean` session bean to call
`MailerBean.sendMessage`. The result is sent to the `response.xhtml`
Facelets view.

## 36.2.2 Running the async Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `async` example.

The following topics are addressed here:

  - [Section 36.2.2.1, "To Run the async Example Application Using
    NetBeans IDE"](#GKINW)

  - [Section 36.2.2.2, "To Run the async Example Application Using
    Maven"](#GKRFB)

### 36.2.2.1 To Run the async Example Application Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/ejb
    ```

4.  Select the `async` folder, select Open Required Projects, and click
    Open Project.

5.  In the Projects tab, right-click the `async-smtpd` project and
    select Run.
    
    The SMTP server simulator starts accepting connections. The
    async-smptd output tab shows the following message:
    
    ``` oac_no_warn
    [Test SMTP server listening on port 3025]
    ```

6.  In the Projects tab, right-click the `async-war` project and select
    Build.
    
    This command configures the JavaMail resource using a GlassFish
    Server administrative command and builds, packages, and deploys the
    `async-war` module.

7.  Open the following URL in a web browser window:
    
    ``` oac_no_warn
    http://localhost:8080/async-war
    ```

8.  In the web browser window, enter an email address and click Send
    email.
    
    The `MailerBean` stateless bean uses the JavaMail API to deliver an
    email to the SMTP server simulator. The async-smptd output window in
    NetBeans IDE shows the resulting email message, including its
    headers.

9.  To stop the SMTP server simulator, click the X button on the right
    side of the status bar in NetBeans IDE.

10. Delete the JavaMail session resource.
    
    1.  In the Services tab, expand the Servers node, then expand the
        GlassFish Server server node.
    
    2.  Expand the Resources node, then expand the JavaMail Sessions
        node.
    
    3.  Right-click mail/myExampleSession and select Unregister.

### 36.2.2.2 To Run the async Example Application Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/ejb/async/async-smtpd/
    ```

3.  Enter the following command to build and package the SMTP server
    simulator:
    
    ``` oac_no_warn
    mvn install
    ```

4.  Enter the following command to start the STMP server simulator:
    
    ``` oac_no_warn
    mvn exec:java
    ```
    
    The following message appears:
    
    ``` oac_no_warn
    [Test SMTP server listening on port 3025]
    ```
    
    Keep this terminal window open.

5.  In a new terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/ejb/async/async-war
    ```

6.  Enter the following command to configure the JavaMail resource and
    to build, package, and deploy the `async-war` module:
    
    ``` oac_no_warn
    mvn install
    ```

7.  Open the following URL in a web browser window:
    
    ``` oac_no_warn
    http://localhost:8080/async-war
    ```

8.  In the web browser window, enter an email address and click Send
    email.
    
    The `MailerBean` stateless bean uses the JavaMail API to deliver an
    email to the SMTP server simulator. The resulting email message
    appears on the first terminal window, including its headers.

9.  To stop the SMTP server simulator, close the terminal window in
    which you issued the command to start the STMP server simulator.

10. To delete the JavaMail session resource, type the following command:
    
    ``` oac_no_warn
    asadmin delete-javamail-resource mail/myExampleSession
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
<td><a href="ejb-async001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partpersist.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
