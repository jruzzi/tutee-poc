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
<td><a href="dukes-bookstore.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-bookstore002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 57.1 Design and Architecture of Duke's Bookstore

Duke's Bookstore is a simple web application that uses many features of
JavaServer Faces technology, in addition to other Java EE 7 features:

  - JavaServer Faces technology, as well as Contexts and Dependency
    Injection for Java EE (CDI)
    
      - A set of Facelets pages, along with a template, provides the
        user interface to the application.
    
      - CDI managed beans are associated with each of the Facelets
        pages.
    
      - A custom image map component on the front page allows you to
        select a book to enter the store. Each area of the map is
        represented by a JavaServer Faces managed bean. Text hyperlinks
        are also provided for accessibility.
    
      - Action listeners are registered on the image map and the text
        links. These listeners retrieve the ID value for the selected
        book and store it in the session map so it can be retrieved by
        the managed bean for the next page.
    
      - The `h:dataTable` tag is used to render the book catalog and
        shopping cart contents dynamically.
    
      - A custom converter is registered on the credit card field on the
        checkout page, `bookcashier.xhtml`, which also uses an
        `f:validateRegEx` tag to ensure that the input is correctly
        formatted.
    
      - A value-change listener is registered on the name field on
        `bookcashier.xhtml`. This listener saves the name in a parameter
        so the following page, `bookreceipt.xhtml`, can access it.

  - Enterprise beans: Local, no-interface-view stateless session bean
    and singleton bean

  - A Java Persistence API entity

The packages of the Duke's Bookstore application, located in the
tut-install`/examples/case-studies/dukes-bookstore/src/main/java/javaeetutorial/dukesbookstore/`
directory, are as follows:

  - `components`: Includes the custom UI component classes,
    `MapComponent` and `AreaComponent`

  - `converters`: Includes the custom converter class,
    `CreditCardConverter`

  - `ejb`: Includes two enterprise beans:
    
      - A singleton bean, `ConfigBean`, that initializes the data in the
        database
    
      - A stateless session bean, `BookRequestBean`, that contains the
        business logic to manage the entity

  - `entity`: Includes the `Book` entity class

  - `exceptions`: Includes three exception classes

  - `listeners`: Includes the event handler and event listener classes

  - `model`: Includes a model JavaBeans class

  - `renderers`: Includes the custom renderers for the custom UI
    component classes

  - `web.managedbeans`: Includes the managed beans for the Facelets
    pages

  - `web.messages`: Includes the resource bundle files for localized
    messages

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
<td><a href="dukes-bookstore.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-bookstore002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
