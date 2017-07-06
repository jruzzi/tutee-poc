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
<td><a href="jaxrs002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 29.3 Example Applications for JAX-RS

This section provides an introduction to creating, deploying, and
running your own JAX-RS applications. This section demonstrates the
steps that are needed to create, build, deploy, and test a very simple
web application that uses JAX-RS annotations.

The following topics are addressed here:

  - [Section 29.3.1, "Creating a Simple RESTful Web Service"](#GIPYZ)

  - [Section 29.3.2, "The rsvp Example Application"](#GJVBC)

  - [Section 29.3.3, "Real-World Examples"](#GIRCI)

## 29.3.1 Creating a Simple RESTful Web Service

This section explains how to use NetBeans IDE to create a RESTful web
service using a Maven archetype. The archetype generates a skeleton for
the application, and you simply need to implement the appropriate
method.

You can find a version of this application at
tut-install`/examples/jaxrs/hello/`.

The following topics are addressed here:

  - [Section 29.3.1.1, "To Create a RESTful Web Service Using NetBeans
    IDE"](#GIQAA)

### 29.3.1.1 To Create a RESTful Web Service Using NetBeans IDE

1.  Ensure you have installed the tutorial archetypes as described in
    [Installing the Tutorial Archetypes](usingexamples007.htm#CHDJGCCA).

2.  In NetBeans IDE, create a simple web application using the
    `jaxrs-service-archetype` Maven archetype. This archetype creates a
    very simple "Hello, World" web application.
    
    1.  From the File menu, choose New Project.
    
    2.  From Categories, select Maven. From Projects, select Project
        From Archetype. Click Next.
    
    3.  Under Search enter `jaxrs-service`, select the
        `jaxrs-service-archetype`, and click Next.
    
    4.  Under Project Name enter `HelloWorldApplication`, set the
        Project Location, and set the Package name to
        `javaeetutorial.hello`, and click Finish.
    
    The project is created.

3.  In `HelloWorld.java`, find the `getHtml()` method. Replace the
    `//TODO` comment with the following text, so that the finished
    product resembles the following method:
    
    ``` oac_no_warn
    @GET
    @Produces("text/html")
    public String getHtml() {
        return "<html lang=\"en\"><body><h1>Hello, World!!</body></h1></html>";
    }
    ```
    
      
    
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Note:</p>
    Because the MIME type produced is HTML, you can use HTML tags in your return statement.</td>
    </tr>
    </tbody>
    </table>
    
      

4.  Right-click the `HelloWorldApplication` project in the Projects pane
    and select Run.
    
    This will build and deploy the application to GlassFish Server.

5.  In a browser, open the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/HelloWorldApplication/HelloWorldApplication
    ```
    
    A browser window opens and displays the return value of `Hello,
    World!!`

For other sample applications that demonstrate deploying and running
JAX-RS applications using NetBeans IDE, see [The rsvp Example
Application](#GJVBC) and Your First Cup: An Introduction to the Java EE
Platform at `http://docs.oracle.com/javaee/7/firstcup/doc/`. You may
also look at the tutorials on the NetBeans IDE tutorial site, such as
the one titled "Getting Started with RESTful Web Services" at
`https://netbeans.org/kb/docs/websvc/rest.html`. This tutorial includes
a section on creating a CRUD application from a database. Create, read,
update, and delete (CRUD) are the four basic functions of persistent
storage and relational databases.

## 29.3.2 The rsvp Example Application

The `rsvp` example application, located in the
tut-install`/examples/jaxrs/rsvp/` directory, allows invitees to an
event to indicate whether they will attend. The events, people invited
to the event, and the responses to the invite are stored in a Java DB
database using the Java Persistence API. The JAX-RS resources in `rsvp`
are exposed in a stateless session enterprise bean.

The following topics are addressed here:

  - [Section 29.3.2.1, "Components of the rsvp Example
    Application"](#GJVAW)

  - [Section 29.3.2.2, "Running the rsvp Example Application"](#GKCCA)

### 29.3.2.1 Components of the rsvp Example Application

The three enterprise beans in the `rsvp` example application are
`rsvp.ejb.ConfigBean`, `rsvp.ejb.StatusBean`, and
`rsvp.ejb.ResponseBean`.

`ConfigBean` is a singleton session bean that initializes the data in
the database.

`StatusBean` exposes a JAX-RS resource for displaying the current status
of all invitees to an event. The URI path template is declared first on
the class and then on the `getEvent` method:

``` oac_no_warn
@Stateless
@Named
@Path("/status")
public class StatusBean {
    ...
    @GET
    @Produces({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
    @Path("{eventId}/")
    public Event getEvent(@PathParam("eventId") Long eventId) {
         ...
```

The combination of the two `@Path` annotations results in the following
URI path template:

``` oac_no_warn
@Path("/status/{eventId}/")
```

The URI path variable `eventId` is a `@PathParam` variable in the
`getEvent` method, which responds to HTTP GET requests and has been
annotated with `@GET`. The `eventId` variable is used to look up all the
current responses in the database for that particular event.

`ResponseBean` exposes a JAX-RS resource for setting an invitee's
response to a particular event. The URI path template for `ResponseBean`
is declared as follows:

``` oac_no_warn
@Path("/{eventId}/{inviteId}")
```

Two URI path variables are declared in the path template: `eventId` and
`inviteId`. As in `StatusBean`, `eventId` is the unique ID for a
particular event. Each invitee to that event has a unique ID for the
invitation, and that is the `inviteId`. Both of these path variables are
used in two JAX-RS methods in `ResponseBean`: `getResponse` and
`putResponse`. The `getResponse` method responds to HTTP GET requests
and displays the invitee's current response and a form to change the
response.

The `javaeetutorial.rsvp.rest.RsvpApplication` class defines the root
application path for the resources by applying the
`javax.ws.rs.ApplicationPath` annotation at the class level.

``` oac_no_warn
@ApplicationPath("/webapi")
public class RsvpApplication extends Application {
}
```

An invitee who wants to change his or her response selects the new
response and submits the form data, which is processed as an HTTP POST
request by the `putResponse` method. The new response is extracted from
the HTTP POST request and stored as the `userResponse` string. The
`putResponse` method uses `userResponse`, `eventId`, and `inviteId` to
update the invitee's response in the database.

The events, people, and responses in `rsvp` are encapsulated in Java
Persistence API entities. The `rsvp.entity.Event`, `rsvp.entity.Person`,
and `rsvp.entity.Response` entities respectively represent events,
invitees, and responses to an event.

The `rsvp.util.ResponseEnum` class declares an enumerated type that
represents all the possible response statuses an invitee may have.

The web application also includes two CDI managed beans, `StatusManager`
and `EventManager`, which use the JAX-RS Client API to call the
resources exposed in `StatusBean` and `ResponseBean`. For information on
how the Client API is used in `rsvp`, see ["The Client API in the rsvp
Example Application"](jaxrs-client002.htm#BABEDFIG).

### 29.3.2.2 Running the rsvp Example Application

Both NetBeans IDE and Maven can be used to deploy and run the `rsvp`
example application.

The following topics are addressed here:

  - [Section 29.3.2.2.1, "To Run the rsvp Example Application Using
    NetBeans IDE"](#CIHEFEHA)

  - [Section 29.3.2.2.2, "To Run the rsvp Example Application Using
    Maven"](#CIHHHIEI)

#### 29.3.2.2.1 To Run the rsvp Example Application Using NetBeans IDE

1.  If the database server is not already running, start it by following
    the instructions in [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK).

2.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

3.  From the File menu, choose Open Project.

4.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/jaxrs
    ```

5.  Select the `rsvp` folder.

6.  Click Open Project.

7.  In the Projects tab, right-click the `rsvp` project and select Run.
    
    The project will be compiled, assembled, and deployed to GlassFish
    Server. A web browser window will open to the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/rsvp/index.xhtml
    ```

8.  In the web browser window, click the Event status link for the
    Duke's Birthday event.
    
    You'll see the current invitees and their responses.

9.  Click the current response of one of the invitees in the Status
    column of the table, select a new response, and click Update your
    status.
    
    The invitee's new status should now be displayed in the table of
    invitees and their response statuses.

#### 29.3.2.2.2 To Run the rsvp Example Application Using Maven

1.  If the database server is not already running, start it by following
    the instructions in [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK).

2.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

3.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/jaxrs/rsvp/
    ```

4.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds, assembles, and deploys `rsvp` to GlassFish
    Server.

5.  Open a web browser window to the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/rsvp/
    ```

6.  In the web browser window, click the Event status link for the
    Duke's Birthday event.
    
    You'll see the current invitees and their responses.

7.  Click the current response of one of the invitees in the Status
    column of the table, select a new response, and click Update your
    status.
    
    The invitee's new status should now be displayed in the table of
    invitees and their response statuses.

## 29.3.3 Real-World Examples

Most blog sites use RESTful web services. These sites involve
downloading XML files, in RSS or Atom format, that contain lists of
links to other resources. Other websites and web applications that use
REST-like developer interfaces to data include Twitter and Amazon S3
(Simple Storage Service). With Amazon S3, buckets and objects can be
created, listed, and retrieved using either a REST-style HTTP interface
or a SOAP interface. The examples that ship with Jersey include a
storage service example with a RESTful interface.

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
<td><a href="jaxrs002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jaxrs004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
