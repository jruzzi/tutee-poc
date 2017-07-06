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
<td><a href="dukes-bookstore001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-bookstore003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 57.2 The Duke's Bookstore Interface

This section provides additional detail regarding the components of the
Duke's Bookstore example and how they interact.

The following topics are addressed here:

  - [Section 57.2.1, "The Book Java Persistence API Entity"](#GLQER)

  - [Section 57.2.2, "Enterprise Beans Used in Duke's
    Bookstore"](#GLQEU)

  - [Section 57.2.3, "Facelets Pages and Managed Beans Used in Duke's
    Bookstore"](#GLQDP)

  - [Section 57.2.4, "Custom Components and Other Custom Objects Used in
    Duke's Bookstore"](#GLQDX)

  - [Section 57.2.5, "Properties Files Used in Duke's
    Bookstore"](#GLQDG)

  - [Section 57.2.6, "Deployment Descriptors Used in Duke's
    Bookstore"](#GLQED)

## 57.2.1 The Book Java Persistence API Entity

The `Book` entity, located in the `dukesbookstore.entity` package,
encapsulates the book data stored by Duke's Bookstore.

The `Book` entity defines attributes used in the example:

  - A book ID

  - The author's first name

  - The author's surname

  - The title

  - The price

  - Whether the book is on sale

  - The publication year

  - A description of the book

  - The number of copies in the inventory

The `Book` entity also defines a simple named query, `findBooks`.

## 57.2.2 Enterprise Beans Used in Duke's Bookstore

Two enterprise beans located in the `dukesbookstore.ejb` package provide
the business logic for Duke's Bookstore.

  - `BookRequestBean` is a stateful session bean that contains the
    business methods for the application. The methods create, retrieve,
    and purchase books, and update the inventory for a book. To retrieve
    the books, the `getBooks` method calls the `findBooks` named query
    defined in the `Book` entity.

  - `ConfigBean` is a singleton session bean used to create the books in
    the catalog when the application is initially deployed. It calls the
    `createBook` method defined in `BookRequestBean`.

## 57.2.3 Facelets Pages and Managed Beans Used in Duke's Bookstore

The Duke's Bookstore application uses Facelets and its templating
features to display the user interface. The Facelets pages interact with
a set of CDI managed beans that act as backing beans, providing the
underlying properties and methods for the user interface. The front page
also interacts with the custom components used by the application.

The application uses the following Facelets pages, which are located in
the tut-install`/examples/case-studies/dukes-bookstore/src/main/webapp/`
directory.

  - `bookstoreTemplate.xhtml`: The template file, which specifies a
    header used on every page as well as the style sheet used by all the
    pages. The template also retrieves the language set in the web
    browser.
    
    Uses the `LocaleBean` managed bean.

  - `index.xhtml`: Landing page, which lays out the custom map and area
    components using managed beans configured in the `faces-config.xml`
    file and allows the user to select a book and advance to the
    `bookstore.xhtml` page.

  - `bookstore.xhtml`: Page that allows the user to obtain details on
    the selected book or the featured book, to add either book to the
    shopping cart, and to advance to the `bookcatalog.xhtml` page.
    
    Uses the `BookstoreBean` managed bean.

  - `bookdetails.xhtml`: Page that shows details on a book selected from
    `bookstore.xhtml` or other pages and allows the user to add the book
    to the cart and/or advance to the `bookcatalog.xhtml` page.
    
    Uses the `BookDetailsBean` managed bean.

  - `bookcatalog.xhtml`: Page that displays the books in the catalog and
    allows the user to add books to the shopping cart, view the details
    for any book, view the shopping cart, empty the shopping cart, or
    purchase the books in the shopping cart.
    
    Uses the `BookstoreBean`, `CatalogBean`, and `ShoppingCart` managed
    beans.

  - `bookshowcart.xhtml`: Page that displays the contents of the
    shopping cart and allows the user to remove items, view the details
    for an item, empty the shopping cart, purchase the books in the
    shopping cart, or return to the catalog.
    
    Uses the `ShowCartBean` and `ShoppingCart` managed beans.

  - `bookcashier.xhtml`: Page that allows the user to purchase books,
    specify a shipping option, subscribe to newsletters, or join the
    Duke Fan Club with a purchase over a certain amount.
    
    Uses the `CashierBean` and `ShoppingCart` managed beans.

  - `bookreceipt.xhtml`: Page that confirms the user's purchase and
    allows the user to return to the catalog page to continue shopping.
    
    Uses the `CashierBean` managed bean.

  - `bookordererror.xhtml`: Page rendered by `CashierBean` if the
    bookstore has no more copies of a book that was ordered.

The application uses the following managed beans, which are located in
the
tut-install`/examples/case-studies/dukes-bookstore/src/main/java/javaeetutorial/dukesbookstore/web/managedbeans/`
directory.

  - `AbstractBean`: Contains utility methods called by other managed
    beans.

  - `BookDetailsBean`: Backing bean for the `bookdetails.xhtml` page.
    Specifies the name `details`.

  - `BookstoreBean`: Backing bean for the `bookstore.xhtml` page.
    Specifies the name `store`.

  - `CashierBean`: Backing bean for the `bookcashier.xhtml` and
    `bookreceipt.xhtml` pages.

  - `CatalogBean`: Backing bean for the `bookcatalog.xhtml` page.
    Specifies the name `catalog`.

  - `LocaleBean`: Managed bean that retrieves the current locale; used
    on each page.

  - `ShoppingCart`: Backing bean used by the `bookcashier.xhtml`,
    `bookcatalog.xhtml`, and `bookshowcart.xhtml` pages. Specifies the
    name `cart`.

  - `ShoppingCartItem`: Contains methods called by `ShoppingCart`,
    `CatalogBean`, and `ShowCartBean`.

  - `ShowCartBean`: Backing bean for the `bookshowcart.xhtml` page.
    Specifies the name
`showcart`.

## 57.2.4 Custom Components and Other Custom Objects Used in Duke's Bookstore

The map and area custom components for Duke's Bookstore, along with
associated renderer, listener, and model classes, are defined in the
following packages in the
tut-install`/examples/case-studies/dukes-bookstore/src/main/java/javaeetutorial/dukesbookstore/`
directory.

  - `components`: Contains the `MapComponent` and `AreaComponent`
    classes. See [Creating Custom Component
    Classes](jsf-custom005.htm#BNAVU).

  - `listeners`: Contains the `AreaSelectedEvent` class, along with
    other listener classes. See [Handling Events for Custom
    Components](jsf-custom008.htm#BNAWD).

  - `model`: Contains the `ImageArea` class. See [Configuring Model
    Data](jsf-custom003.htm#GLPBO) for more information.

  - `renderers`: Contains the `MapRenderer` and `AreaRenderer` classes.
    See [Delegating Rendering to a Renderer](jsf-custom006.htm#BNAWA).

The
tut-install`/examples/case-studies/dukes-bookstore/src/java/dukesbookstore/`
directory also contains a custom converter and other custom listeners
not specifically tied to the custom components.

  - `converters`: Contains the `CreditCardConverter` class. See
    [Creating and Using a Custom Converter](jsf-custom011.htm#BNAUS).

  - `listeners`: Contains the `LinkBookChangeListener`,
    `MapBookChangeListener`, and `NameChanged` classes. See
    [Implementing an Event Listener](jsf-custom007.htm#BNAUT).

## 57.2.5 Properties Files Used in Duke's Bookstore

The strings used in the Duke's Bookstore application are encapsulated
into resource bundles to allow the display of localized strings in
multiple locales. The properties files, located in the
tut-install`/examples/case-studies/dukes-bookstore/src/main/java/javaeetutorial/dukesbookstore/web/messages/`
directory, consist of a default file containing English strings and
three additional files for other locales. The files are as follows:

  - `Messages.properties`: Default file, containing English strings

  - `Messages_de.properties`: File containing German strings

  - `Messages_es.properties`: File containing Spanish strings

  - `Messages_fr.properties`: File containing French strings

The language setting in the user's web browser determines which locale
is used. The `html` tag in `bookstoreTemplate.xhtml` retrieves the
language setting from the `language` property of `LocaleBean`:

``` oac_no_warn
<html lang="#{localeBean.language}"
...
```

For more information about resource bundles, see [Chapter 20,
"Internationalizing and Localizing Web
Applications."](webi18n.htm#BNAXU)

The resource bundle is configured as follows in the `faces-config.xml`
file:

``` oac_no_warn
<application>
    <resource-bundle>
        <base-name>
            javaeetutorial.dukesbookstore.web.messages.Messages
        </base-name>
        <var>bundle</var>
    </resource-bundle>
    <locale-config>
        <default-locale>en</default-locale>
        <supported-locale>de</supported-locale>
        <supported-locale>es</supported-locale>
        <supported-locale>fr</supported-locale>
    </locale-config>
</application>
```

This configuration means that in the Facelets pages, messages are
retrieved using the prefix `bundle` with the key found in the
`Messages_`locale`.properties` file, as in the following example from
the `index.xhtml` page:

``` oac_no_warn
<h:outputText style="font-weight:bold" 
              value="#{bundle.ChooseBook}" />
```

In `Messages.properties`, the key string is defined as follows:

``` oac_no_warn
ChooseBook=Choose a Book from our Catalog
```

## 57.2.6 Deployment Descriptors Used in Duke's Bookstore

The following deployment descriptors are used in Duke's Bookstore:

  - `src/main/resources/META-INF/persistence.xml`: The Java Persistence
    API configuration file

  - `src/main/webapp/WEB-INF/bookstore.taglib.xml`: The tag library
    descriptor file for the custom components

  - `src/main/webapp/WEB-INF/faces-config.xml`: The JavaServer Faces
    configuration file, which configures the managed beans for the map
    component as well as the resource bundles for the application

  - `src/main/webapp/WEB-INF/web.xml`: The web application configuration
    file

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
<td><a href="dukes-bookstore001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="dukes-bookstore003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
