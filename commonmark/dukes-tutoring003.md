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
<td><a href="dukes-tutoring002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-tutoring004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 58.3 Administration Interface

The administration interface of Duke's Tutoring is used by the tutoring
center staff to manage the data employed by the main interface: the
students, the students' guardians, and the addresses. The administration
interface uses many of the same components as the main interface.
Additional components that are only used in the administration interface
are described here.

The following topics are addressed here:

  - [Section 58.3.1, "Enterprise Beans Used in the Administration
    Interface"](#GKAEN)

  - [Section 58.3.2, "Facelets Files Used in the Administration
    Interface"](#GKACB)

  - [Section 58.3.3, "CDI Managed Beans Used in the Administration
    Interface"](#BCGHIDEG)

  - [Section 58.3.4, "Helper Classes Used in the Administration
    Interface"](#BCGFFFCA)

## 58.3.1 Enterprise Beans Used in the Administration Interface

The following enterprise bean, in the `dukestutoring.ejb` package of the
`dukes-tutoring-war` project, is used in the administration interface.

  - `AdminBean`: A stateless session bean for all the business logic
    used in the administration interface. Calls security methods to
    allow invocation of the business methods only by authorized users.

## 58.3.2 Facelets Files Used in the Administration Interface

The following Facelets files, under `src/main/webapp/`, are used in the
administration interface:

  - `admin/adminTemplate.xhtml`: Template for the administration
    interface

  - `admin/index.xhtml`: Landing page for the administration interface

  - `login.xhtml`: Login page for the security-constrained
    administration interface

  - `loginError.xhtml`: Page displayed if there are errors
    authenticating the administration user

  - `admin/address` directory: Pages that allow you to create, edit, and
    delete `Address` entities

  - `admin/guardian` directory: Pages that allow you to create, edit,
    and delete `Guardian` entities

  - `admin/student` directory: Pages that allow you to create, edit, and
    delete `Student` entities

  - `resources/components/formLogin.xhtml`: Composite component for a
    login form using Java EE security

  - `WEB-INF/includes/adminNav.xhtml`: XHTML fragment for the
    administration interface's navigation bar

## 58.3.3 CDI Managed Beans Used in the Administration Interface

The CDI managed beans used in the administration interface are located
in the `dukestutoring.web` package in the `dukes-tutoring-war` project.

  - `StudentBean.java`: A managed bean for the Facelets pages used to
    create and edit students. The first and last names have Bean
    Validation annotations that require the fields to be filled in. The
    phone numbers have Bean Validation annotations to ensure that the
    submitted data is well-formed.

  - `GuardianBean.java`: A managed bean for the Facelets pages used to
    create guardians for and assign guardians to students. The first and
    last names have Bean Validation annotations that require the fields
    to be filled in. The phone numbers have Bean Validation annotations
    to ensure that the submitted data is well-formed.

  - `AddressBean.java`: A managed bean for the Facelets pages used to
    create addresses for students. The street, city, province, and
    postal code attributes have Bean Validation annotations that require
    the fields to be filled in, and the postal code attribute has an
    additional annotation to ensure that the data is properly formed.

## 58.3.4 Helper Classes Used in the Administration Interface

The following helper classes, found in the `dukes-tutoring-war`
project's `dukestutoring.web.util` package, are used in the
administration interface.

  - `EntityConverter`: A parent class to `StudentConverter` and
    `GuardianConverter` that defines a cache to store the entity classes
    when converting the entities for use in JavaServer Faces user
    interface components. The cache helps increase performance. The
    cache is stored in the JavaServer Faces context.

  - `StudentConverter`: A JavaServer Faces converter for the `Student`
    entity class. This class contains methods to convert `Student`
    instances to strings and back again, so they can be used in the user
    interface components of the application.

  - `GuardianConverter`: Similar to `StudentConverter`, this class is a
    converter for the `Guardian` entity class.

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
<td><a href="dukes-tutoring002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-tutoring004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
