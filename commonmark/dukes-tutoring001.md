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
<td><a href="dukes-tutoring.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-tutoring002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 58.1 Design and Architecture of Duke's Tutoring

Duke's Tutoring is a web application that incorporates several Java EE
technologies. It exposes both a main interface (for students, guardians,
and tutoring center staff) and an administration interface (for staff to
maintain the system). The business logic for both interfaces is provided
by enterprise beans. The enterprise beans use the Java Persistence API
to create and store the application's data in the database. [Figure
58-1](#CHDDJDCH) illustrates the architecture of the application.

Figure 58-1 Architecture of the Duke's Tutoring Example Application

![Description of Figure 58-1 follows](img/jeett_dt_061.png)  
[Description of "Figure 58-1 Architecture of the Duke's Tutoring Example
Application"](img_text/jeett_dt_061.htm)  
  

The Duke's Tutoring application is organized into two main projects: the
`dukes-tutoring-common` library and the `dukes-tutoring-war` web
application. The `dukes-tutoring-common` library project contains the
entity classes and helper classes used by the `dukes-tutoring-war` web
application, and `dukes-tutoring-common` is packaged and deployed with
`dukes-tutoring-war`. The library JAR file is useful for allowing the
entity classes and helper classes to be reused by other applications,
such as a JavaFX client application.

Duke's Tutoring uses the following Java EE 7 platform features:

  - Java Persistence API entities
    
      - A custom Bean Validation annotation, `@Email`, for validating
        email addresses
    
      - A standard `jta-data-source` definition that will create the
        JDBC resource on deployment
    
      - A standard property in the `persistence.xml` deployment
        descriptor to automatically and portably create and delete the
        tables in the `jta-data-source`

  - Enterprise beans
    
      - Local, no-interface view session and singleton beans
    
      - JAX-RS resources in a session bean
    
      - Java EE security constraints on the administrative interface
        business methods
    
      - All enterprise beans packaged within the WAR

  - WebSocket
    
      - A WebSocket server endpoint that automatically publishes the
        status of students to client endpoints

  - Contexts and Dependency Injection
    
      - A CDI event that is fired when the status of a student changes
    
      - Handler methods for updating the application once the status
        event is fired
    
      - CDI managed beans for Facelets pages
    
      - Bean Validation annotations in the CDI managed beans

  - JavaServer Faces technology, using Facelets for the web front end
    
      - Templating
    
      - Composite components
    
      - A custom formatter, `PhoneNumberFormatter`
    
      - Security constraints on the administrative interface
    
      - Ajax-enabled Facelets components

The Duke's Tutoring application has two main user interfaces, both
packaged within a single WAR file:

  - The main interface, for students, guardians, and staff

  - The administrative interface used by the staff to manage the
    students and guardians, and to generate attendance reports

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
<td><a href="dukes-tutoring.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-tutoring002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
