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
<td><a href="dukes-tutoring003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-forest.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 58.4 Running the Duke's Tutoring Case Study Application

This section describes how to build, package, deploy, and run the Duke's
Tutoring application.

The following topics are addressed here:

  - [Section 58.4.1, "Running Duke's Tutoring"](#GKJOA)

## 58.4.1 Running Duke's Tutoring

You can use either NetBeans IDE or Maven to build, package, deploy, and
run Duke's Tutoring.

The following topics are addressed here:

  - [Section 58.4.1.1, "To Build and Deploy Duke's Tutoring Using
    NetBeans IDE"](#GKJNR)

  - [Section 58.4.1.2, "To Build and Deploy Duke's Tutoring Using
    Maven"](#GKJOG)

  - [Section 58.4.1.3, "Using Duke's Tutoring"](#GKJOC)

### 58.4.1.1 To Build and Deploy Duke's Tutoring Using NetBeans IDE

Before You Begin

You must have already configured GlassFish Server as a Java EE server in
NetBeans IDE, as described in [To Add GlassFish Server as a Server Using
NetBeans IDE](usingexamples001.htm#GIQZL).

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  If the database server is not already running, start it as described
    in [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK).

3.  From the File menu, choose Open Project.

4.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/case-studies
    ```

5.  Select the `dukes-tutoring` folder.

6.  Select the Open Required Projects check box and click Open Project.
    
      
    
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Note:</p>
    The first time you open Duke's Tutoring in NetBeans, you will see error glyphs in the <span class="gui-object-action">Projects</span> tab. This is expected, as the metamodel files used by the enterprise beans for Criteria API queries have not yet been generated.</td>
    </tr>
    </tbody>
    </table>
    
      

7.  In the Projects tab, right-click the `dukes-tutoring` project and
    select Build.
    
    This command creates a JDBC security realm named tutoringRealm,
    builds and packages the `dukes-tutoring-common` and
    `dukes-tutoring-war` projects, and deploys `dukes-tutoring-war` to
    GlassFish Server, starting the Java DB database and GlassFish Server
    if they have not already been started.

### 58.4.1.2 To Build and Deploy Duke's Tutoring Using Maven

1.  Make sure that GlassFish Server has started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  If the database server is not already running, start it as described
    in [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK).

3.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/case-studies/dukes-tutoring/
    ```

4.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command creates a JDBC security realm named tutoringRealm,
    builds and packages the `dukes-tutoring-common` and
    `dukes-tutoring-war` projects, and deploys `dukes-tutoring-war` to
    GlassFish Server.

### 58.4.1.3 Using Duke's Tutoring

Once Duke's Tutoring is running on GlassFish Server, use the main
interface to experiment with checking students in and out or sending
them to the park.

To Use the Main Interface of Duke's Tutoring

1.  In a web browser, open the main interface at the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/dukes-tutoring-war/
    ```

2.  Use the main interface to check students in and out, and to log when
    the students go to the park.

To Use the Administration Interface of Duke's Tutoring

Follow these instructions to log in to the administration interface of
Duke's Tutoring and add new students, guardians, and addresses.

1.  From the main interface, open the administration interface by
    clicking Administration main page in the left menu.
    
    This redirects you to the login page at the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/dukes-tutoring-war/admin/index.xhtml
    ```

2.  On the login page, enter `admin@example.com` in the User name field,
    and enter `javaee` in the Password field.

3.  Use the administration interface to add or modify students, add
    guardians, or add addresses.
    
      - To add a new student, click Create new student in the left menu,
        fill in the fields (two are required) in the form that opens,
        and click Submit. The Email, Home phone, and Mobile phone fields
        have formatting requirements enforced by HTML5 pass-through or
        by Bean Validation constraints.
    
      - To modify a student, click Edit next to the student's name,
        modify the fields in the form that opens, and click Submit. To
        edit another student, choose the student from the drop-down menu
        at the top of the page and click Change student.
    
      - To remove a student, click Remove next to the student's name,
        then click Confirm in the page that appears. This action removes
        the student from the tutoring session but does not remove the
        student from the database. To add the student to the tutoring
        session again, click Activate student in the left menu, then
        click Activate next to the student's name in the page that
        appears.
    
      - To add a guardian for a student, click Add guardian next to the
        student's name. The page that appears shows the student's name,
        the available guardians, and the current guardians for the
        student, if any. To add an existing guardian for that student,
        select the guardian from the list and click Add guardian. To
        create a new guardian for the student, fill in the fields and
        click Submit. To remove a guardian from a student, select one of
        the student's current guardians from the list and click Remove
        guardian.
    
      - To add an address for a student, click Add address next to the
        student's name. In the page that appears, fill in the
        appropriate fields in the form that appears, and click Submit.
        Four fields are required.

The administration interface is not fully implemented. It is not
possible to edit a guardian or to view or edit an address, although
Facelets pages exist for these features. The application also makes no
use of the properties in the `PersonDetails` entity. Feel free to modify
the application to add these features.

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
<td><a href="dukes-tutoring003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-forest.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
