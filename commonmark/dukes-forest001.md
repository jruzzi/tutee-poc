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
<td><a href="dukes-forest.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-forest002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 59.1 Overview of the Duke's Forest Case Study Example

Duke's Forest is a simple e-commerce application that contains several
web applications and illustrates the use of the following Java EE 7
APIs:

  - JavaServer Faces technology, including Ajax

  - Contexts and Dependency Injection for Java EE (CDI)

  - Java API for RESTful Web Services (JAX-RS)

  - Java Persistence API (JPA)

  - Java API for JavaBeans Validation (Bean Validation)

  - Enterprise JavaBeans (EJB) technology

  - Java Message Service (JMS)

The application consists of the following projects.

  - Duke's Store: A web application that has a product catalog, customer
    self-registration, and a shopping cart. It also has an
    administration interface for product, category, and user management.
    The project name is `dukes-store`.

  - Duke's Shipment: A web application that provides an interface for
    order shipment management. The project name is `dukes-shipment`.

  - Duke's Payment: A web service application that has a RESTful web
    service for order payment. The project name is `dukes-payment`.

  - Duke's Resources: A simple Java archive project that contains all
    resources used by the web projects. It includes messages, CSS style
    sheets, images, JavaScript files, and JavaServer Faces composite
    components. The project name is `dukes-resources`.

  - Entities: A simple Java archive project that contains all JPA
    entities. This project is shared among other projects that use the
    entities. The project name is `entities`.

  - Events: A simple Java archive project that contains a POJO class
    that is used as a CDI event. The project name is `events`.

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
<td><a href="dukes-forest.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-forest002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
