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
<td><a href="dukes-tutoring001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-tutoring003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 58.2 Main Interface

The main interface allows students and staff to check students in and
out, and record when students are outside at the playground.

The following topics are addressed here:

  - [Section 58.2.1, "Java Persistence API Entities Used in the Main
    Interface"](#GKAFJ)

  - [Section 58.2.2, "Enterprise Beans Used in the Main
    Interface"](#GKAFC)

  - [Section 58.2.3, "WebSocket Endpoint Used in the Main
    Interface"](#BCGHHCDA)

  - [Section 58.2.4, "Facelets Files Used in the Main
    Interface"](#GKAET)

  - [Section 58.2.5, "Helper Classes Used in the Main
    Interface"](#GKADH)

  - [Section 58.2.6, "Properties Files"](#GKADA)

  - [Section 58.2.7, "Deployment Descriptors Used in Duke's
    Tutoring"](#GKAEV)

## 58.2.1 Java Persistence API Entities Used in the Main Interface

The following entities used in the main interface encapsulate data
stored and manipulated by Duke's Tutoring, and are located in the
`dukestutoring.entity` package in the `dukes-tutoring-common` project.

  - `Person`: The `Person` entity defines attributes common to students
    and guardians tracked by the application. These attributes are the
    person's name and contact information, including phone numbers and
    email address. This entity has two subclasses, `Student` and
    `Guardian`.

  - `PersonDetails`: The `PersonDetails` entity is used to store
    additional data common to all people, such as attributes like
    pictures and the person's birthday, which aren't included in the
    `Person` entity for performance reasons.

  - `Student` and `Guardian`: The `Student` entity stores attributes
    specific to the students who come to tutoring. This includes
    information like the student's grade level and school. The
    `Guardian` entity's attributes are specific to the parents or
    guardians of a `Student`. Students and guardians have a many-to-many
    relationship. That is, a student may have one or more guardians, and
    a guardian may have one or more students.

  - `Address`: The `Address` entity represents a mailing address and is
    associated with `Person` entities. Addresses and people have a
    many-to-one relationship. That is, one person may have many
    addresses.

  - `TutoringSession`: The `TutoringSession` entity represents a
    particular day at the tutoring center. A particular tutoring session
    tracks which students attended that day, and which students went to
    the park.

  - `StatusEntry`: The `StatusEntry` entity, which logs when a student's
    status changes, is associated with the `TutoringSession` entity.
    Students' statuses change when they check in to a tutoring session,
    when they go to the park, and when they check out. The status entry
    allows the tutoring center staff to track exactly which students
    attended a tutoring session, when they checked in and out, which
    students went to the park while they were at the tutoring center,
    and when they went to and came back from the park.

For information on creating Java Persistence API entities, see [Chapter
37, "Introduction to the Java Persistence
API."](persistence-intro.htm#BNBPZ) For information on validating entity
data, see [Validating Persistent Fields and
Properties](persistence-intro002.htm#GKAHQ) and [Chapter 22, "Bean
Validation: Advanced Topics."](bean-validation-advanced.htm#GKAHP)

## 58.2.2 Enterprise Beans Used in the Main Interface

The following enterprise beans used in the main interface provide the
business logic for Duke's Tutoring, and are located in the
`dukestutoring.ejb` package in the `dukes-tutoring-war` project:

  - `ConfigBean` is a singleton session bean used to create the default
    students when the application is initially deployed, and to create
    an automatic EJB timer that creates tutoring session entities every
    weekday.

  - `RequestBean` is a stateless session bean containing the business
    methods for the main interface. The bean also has business methods
    for retrieving lists of students. These business methods use
    strongly typed Criteria API queries to retrieve data from the
    database. `RequestBean` also injects a CDI event instance,
    `StatusEvent`. This event is fired from the business methods when
    the status of a student changes.

For information on creating and using enterprise beans, see [Enterprise
Beans](partentbeans.htm#BNBLR). For information on creating strongly
typed Criteria API queries, see [Chapter 40, "Using the Criteria API to
Create Queries."](persistence-criteria.htm#GJITV) For information on CDI
events, see [Using Events in CDI Applications](cdi-adv005.htm#GKHIC).

## 58.2.3 WebSocket Endpoint Used in the Main Interface

The `javaeetutorial.dukestutoring.web.websocket.StatusEndpoint` class is
a WebSocket server endpoint that returns students and their status to
client endpoints. The `StatusEndpoint.updateStatus` method is a CDI
observer method for the `StatusEvent` event. When a student's status
changes in the main interface, a `StatusEvent` is fired. The
`updateStatus` observer method is called by the container, and pushes
out the status change to all the client endpoints registered with
`StatusEndpoint`.

The `index.xhtml` JavaServer Faces page contains JavaScript code to
connect to the WebSocket endpoint. The `onMessage` method on this page
clicks a JavaServer Faces button, which makes an Ajax request to refresh
the table that shows the current status of the students.

For more information on WebSocket endpoints, see [Chapter 18, "Java API
for WebSocket."](websocket.htm#GKJIQ5) For information on CDI events,
see [Using Events in CDI Applications](cdi-adv005.htm#GKHIC).

## 58.2.4 Facelets Files Used in the Main Interface

The Duke's Tutoring application uses Facelets to display the user
interface, making extensive use of the templating features of Facelets.
Facelets, the default display technology for JavaServer Faces
technology, consists of XHTML files located in the
tut-install`/examples/case-studies/dukes-tutoring-war/src/main/webapp/`
directory.

The following Facelets files are used in the main interface:

  - `template.xhtml`: Template file for the main interface

  - `error.xhtml`: Error file if something goes wrong

  - `index.xhtml`: Landing page for the main interface

  - `park.xhtml`: Page showing who is currently at the park

  - `current.xhtml`: Page showing who is currently in today's tutoring
    session

  - `statusEntries.xhtml`: Page showing the detailed status entry log
    for today's session

  - `resources/components/allStudentsTable.xhtml`: A composite component
    for a table displaying all active students

  - `resources/components/allInactiveStudentsTable.xhtml`: A composite
    component for a table displaying all inactive students

  - `resources/components/currentSessionTable.xhtml`: A composite
    component for a table displaying all students in today's session

  - `resources/components/parkTable.xhtml`: A composite component for a
    table displaying all students currently at the park

  - `WEB-INF/includes/mainNav.xhtml`: XHTML fragment for the main
    interface's navigation bar

For information on using Facelets, see [Chapter 8, "Introduction to
Facelets."](jsf-facelets.htm#GIEPX)

## 58.2.5 Helper Classes Used in the Main Interface

The following helper classes, found in the `dukes-tutoring-common`
project's `dukestutoring.util` package, are used in the main interface.

  - `CalendarUtil`: A class that provides a method to strip the
    unnecessary time data from `java.util.Calendar` instances.

  - `Email`: A custom Bean Validation annotation class for validating
    email addresses in the `Person` entity.

  - `StatusType`: An enumerated type defining the different statuses
    that a student can have. Possible values are `IN`, `OUT`, and
    `PARK`. `StatusType` is used throughout the application, including
    in the `StatusEntry` entity, and throughout the main interface.
    `StatusType` also defines a `toString` method that returns a
    localized translation of the status based on the locale.

## 58.2.6 Properties Files

The strings used in the main interface are encapsulated into resource
bundles to allow the display of localized strings in multiple locales.
Each of the properties files has locale-specific files appended with
locale codes, containing the translated strings for each locale. For
example, `Messages_es.properties` contains the localized strings for
Spanish locales.

The `dukes-tutoring-common` project has the following resource bundle
under `src/main/resources/`.

  - `javaeetutorial/dukestutoring/util/StatusMessages.properties`:
    Strings for each of the status types defined in the `StatusType`
    enumerated type for the default locale. Each supported locale has a
    property file of the form `StatusMessages_`locale
    prefix`.properties` containing the localized strings. For example,
    the strings for Spanish-speaking locales are located in
    `StatusMessages_es.properties`.

The `dukes-tutoring-war` project has the following resource bundles
under `src/main/resources/`.

  - `ValidationMessages.properties`: Strings for the default locale used
    by the Bean Validation runtime to display validation messages. This
    file must be named `ValidationMessages.properties` and located in
    the default package as required by the Bean Validation
    specification. Each supported locale has a property file of the form
    `ValidationMessages_`locale prefix`.properties` containing the
    localized strings. For example, the strings for German-speaking
    locales are located in `ValidationMessages_de.properties`.

  - `javaeetutorial/dukestutoring/web/messages/Messages.properties`:
    Strings for the default locale for the main and administration
    Facelets interface. Each supported locale has a property file of the
    form `Messages_`locale prefix`.properties` containing the localized
    strings. For example, the strings for simplified Chinese-speaking
    locales are located in `Messages_zh.properties`.

For information on localizing web applications, see [Registering
Application Messages](jsf-configure006.htm#BNAXB).

## 58.2.7 Deployment Descriptors Used in Duke's Tutoring

Duke's Tutoring uses these deployment descriptors in the
`src/main/webapp/WEB-INF` directory of the `dukes-tutoring-war` project:

  - `faces-config.xml`: The JavaServer Faces configuration file

  - `glassfish-web.xml`: The configuration file specific to GlassFish
    Server, which defines security role mapping

  - `web.xml`: The web application configuration file

Duke's Tutoring also uses the following deployment descriptor in the
`src/main/resources/META-INF` directory of the `dukes-tutoring-common`
project:

  - `persistence.xml`: The Java Persistence API configuration file

No enterprise bean deployment descriptor is used in Duke's Tutoring.
Annotations in the enterprise bean class files are used for the
configuration of enterprise beans in this application.

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
<td><a href="dukes-tutoring001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-tutoring003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
