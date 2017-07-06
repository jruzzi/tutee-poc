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
<td><a href="jsf-facelets007.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets009.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 8.8 Resource Library Contracts

Resource library contracts allow you to define a different look and feel
for different parts of one or more applications, instead of either
having to use the same look and feel for all or having to specify a
different look on a page-by-page basis.

To do this, you create a `contracts` section of your web application.
Within the `contracts` section, you can specify any number of named
areas, each of which is called a contract. Within each contract you can
specify resources such as template files, stylesheets, JavaScript files,
and images.

For example, you could specify two contracts named `c1` and `c2`, each
of which uses a template and other files:

``` oac_no_warn
src/main/webapp
    WEB-INF/
    contracts
        c1
            template.xhtml
            style.css
            myImg.gif
            myJS.js
        c2
            template.xhtml
            style2.css
            img2.gif
            JS2.js
    index.xhtml
    ...
```

One part of the application can use `c1`, while another can use `c2`.

Another way to use contracts is to specify a single contract that
contains multiple templates:

``` oac_no_warn
src/main/webapp
    contracts
        myContract
            template1.xhtml
            template2.xhtml
            style.css
            img.png
            img2.png
```

You can package a resource library contract in a JAR file for reuse in
different applications. If you do so, the contracts must be located
under `META-INF/contracts`. You can then place the JAR file in the
`WEB-INF/lib` directory of an application. This means that the
application would be organized as follows:

``` oac_no_warn
src/main/webapp/
    WEB-INF/lib/myContract.jar
    ...
```

You can specify the contract usage within an application's
`faces-config.xml` file, under the `resource-library-contracts` element.
You need to use this element only if your application uses more than one
contract, however.

## 8.8.1 The hello1-rlc Example Application

The `hello1-rlc` example modifies the simple `hello1` example from [A
Web Module That Uses JavaServer Faces Technology: The hello1
Example](webapp003.htm#BNADX) to use two resource library contracts.
Each of the two pages in the application uses a different contract.

The managed bean for `hello1-rlc`, `Hello.java`, is identical to the one
for `hello1` (except that it replaces the `@Named` and `@RequestScoped`
annotations with `@Model`).

The source code for this application is in the
tut-install`/examples/web/jsf/hello1-rlc/` directory.

The following topics are addressed here:

  - [Section 8.8.1.1, "Configuring the hello1-rlc Example"](#BABGEDEB)

  - [Section 8.8.1.2, "The Facelets Pages for the hello1-rlc
    Example"](#BABDHCFG)

  - [Section 8.8.1.3, "To Build, Package, and Deploy the hello1-rlc
    Example Using NetBeans IDE"](#BABBGFFF)

  - [Section 8.8.1.4, "To Build, Package, and Deploy the hello1-rlc
    Example Using Maven"](#BABJAGFB)

  - [Section 8.8.1.5, "To Run the hello1-rlc Example"](#BABFCHEB)

### 8.8.1.1 Configuring the hello1-rlc Example

The `faces-config.xml` file for the `hello1-rlc` example contains the
following elements:

``` oac_no_warn
<resource-library-contracts>
    <contract-mapping>
        <url-pattern>/reply/*</url-pattern>
        <contracts>reply</contracts>
    </contract-mapping>
    <contract-mapping>
        <url-pattern>*</url-pattern>
        <contracts>hello</contracts>
    </contract-mapping>
</resource-library-contracts>
```

The `contract-mapping` elements within the `resource-library-contracts`
element map each contract to a different set of pages within the
application. One contract, named `reply`, is used for all pages under
the `reply` area of the application (`/reply/*`). The other contract,
`hello`, is used for all other pages in the application (`*`).

The application is organized as follows:

``` oac_no_warn
hello1-rlc
    pom.xml
    src/main/java/javaeetutorial/hello1rlc/Hello.java
    src/main/webapp
        WEB-INF
            faces-config.xml
            web.xml
        contracts
            hello
                default.css
                duke.handsOnHips.gif
                template.xhtml
            reply
                default.css
                duke.thumbsup.gif
                template.xhtml
        reply
            response.xhtml
        greeting.xhtml
```

The `web.xml` file specifies the `welcome-file` as `greeting.xhtml`.
Because it is not located under `src/main/webapp/reply`, this Facelets
page uses the `hello` contract, whereas
`src/main/webapp/reply/response.xhtml` uses the `reply` contract.

### 8.8.1.2 The Facelets Pages for the hello1-rlc Example

The `greeting.xhtml` and `response.xhtml` pages have identical code
calling in their templates:

``` oac_no_warn
<ui:composition template="/template.xhtml">
```

The `template.xhtml` files in the `hello` and `reply` contracts differ
only in two respects: the placeholder text for the `title` element
("Hello Template" and "Reply Template") and the graphic that each
specifies.

The `default.css` stylesheets in the two contracts differ in only one
respect: the background color specified for the `body`
element.

### 8.8.1.3 To Build, Package, and Deploy the hello1-rlc Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsf
    ```

4.  Select the `hello1-rlc` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `hello1-rlc` project and select
    Build.
    
    This option builds the example application and deploys it to your
    GlassFish Server
instance.

### 8.8.1.4 To Build, Package, and Deploy the hello1-rlc Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsf/hello1-rlc/
    ```

3.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the application into a WAR file,
    `hello1-rlc.war`, that is located in the `target` directory. It then
    deploys it to your GlassFish Server instance.

### 8.8.1.5 To Run the hello1-rlc Example

1.  Enter the following URL in your web browser:
    
    ``` oac_no_warn
    http://localhost:8080/hello1-rlc
    ```

2.  The `greeting.xhtml` page looks just like the one from `hello1`
    except for its background color and graphic.

3.  In the text field, enter your name and click Submit.

4.  The response page also looks just like the one from `hello1` except
    for its background color and graphic.
    
    The page displays the name you submitted. Click Back to return to
    the `greeting.xhtml` page.

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
<td><a href="jsf-facelets007.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-facelets009.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
