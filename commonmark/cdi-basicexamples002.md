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
<td><a href="cdi-basicexamples001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basicexamples003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 24.2 The simplegreeting CDI Example

The `simplegreeting` example illustrates some of the most basic features
of CDI: scopes, qualifiers, bean injection, and accessing a managed bean
in a JavaServer Faces application. When you run the example, you click a
button that presents either a formal or an informal greeting, depending
on how you edited one of the classes. The example includes four source
files, a Facelets page and template, and configuration files.

The following topics are addressed here:

  - [Section 24.2.1, "The simplegreeting Source Files"](#GJCQS)

  - [Section 24.2.2, "The Facelets Template and Page"](#GJDOJ)

  - [Section 24.2.3, "Running the simplegreeting Example"](#GJCYM)

## 24.2.1 The simplegreeting Source Files

The four source files for the `simplegreeting` example are

  - The default `Greeting` class, shown in [Beans as Injectable
    Objects](cdi-basic005.htm#GIZKS)

  - The `@Informal` qualifier interface definition and the
    `InformalGreeting` class that implements the interface, both shown
    in [Using Qualifiers](cdi-basic006.htm#GJBCK)

  - The `Printer` managed bean class, which injects one of the two
    interfaces, shown in full in [Adding Setter and Getter
    Methods](cdi-basic010.htm#GJBBP)

The source files are located in the
tut-install`/examples/cdi/simplegreeting/src/main/java/javaeetutorial/simplegreeting`
directory.

## 24.2.2 The Facelets Template and Page

To use the managed bean in a simple Facelets application:

1.  Use a very simple template file and `index.xhtml` page.
    
    The template page, `template.xhtml`, looks like this:
    
    ``` oac_no_warn
    <?xml version='1.0' encoding='UTF-8' ?>
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" 
              "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html lang="en"
          xmlns="http://www.w3.org/1999/xhtml"
          xmlns:h="http://xmlns.jcp.org/jsf/html"
          xmlns:ui="http://xmlns.jcp.org/jsf/facelets">
        <h:head>
            <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
            <h:outputStylesheet library="css" name="default.css"/>
            <title><ui:insert name="title">Default Title</ui:insert></title>
        </h:head>
    
        <body>
            <div id="container">
                <div id="header">
                    <h2><ui:insert name="head">Head</ui:insert></h2>
                </div>
    
                <div id="space">
                    <p></p>
                </div>
    
                <div id="content">
                    <ui:insert name="content"/>
                </div>
            </div>
        </body>
    </html>
    ```

2.  To create the Facelets page, redefine the title and head, then add a
    small form to the content:
    
    ``` oac_no_warn
    <?xml version='1.0' encoding='UTF-8' ?>
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" 
              "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html lang="en"
          xmlns="http://www.w3.org/1999/xhtml"
          xmlns:ui="http://xmlns.jcp.org/jsf/facelets"
          xmlns:h="http://xmlns.jcp.org/jsf/html">
        <ui:composition template="/template.xhtml">
    
            <ui:define name="title">Simple Greeting</ui:define>
            <ui:define name="head">Simple Greeting</ui:define>
            <ui:define name="content">
                <h:form id="greetme">
                   <p><h:outputLabel value="Enter your name: " for="name"/>
                      <h:inputText id="name" value="#{printer.name}"/></p>
                   <p><h:commandButton value="Say Hello" 
                                       action="#{printer.createSalutation}"/></p>
                   <p><h:outputText value="#{printer.salutation}"/> </p>
                </h:form>
            </ui:define>
    
        </ui:composition>
    </html>
    ```
    
    The form asks the user to enter a name. The button is labeled Say
    Hello, and the action defined for it is to call the
    `createSalutation` method of the `Printer` managed bean. This method
    in turn calls the `greet` method of the defined `Greeting` class.
    
    The output text for the form is the value of the greeting returned
    by the setter method. Depending on whether the default or the
    `@Informal` version of the greeting is injected, this is one of the
    following, where name is the name entered by the user:
    
    ``` oac_no_warn
    Hello, name.
    
    Hi, name!
    ```
    
    The Facelets page and template are located in the
    tut-install`/examples/cdi/simplegreeting/src/main/webapp/`
    directory.
    
    The simple CSS file that is used by the Facelets page is in the
    following
    location:
    
    ``` oac_no_warn
    tut-install/examples/cdi/simplegreeting/src/main/webapp/resources/css/default.css
    ```

## 24.2.3 Running the simplegreeting Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `simplegreeting` application.

The following topics are addressed here:

  - [Section 24.2.3.1, "To Build, Package, and Run the simplegreeting
    Example Using NetBeans IDE"](#GJCXP)

  - [Section 24.2.3.2, "To Build, Package, and Deploy the simplegreeting
    Example Using Maven"](#GJCZT)

  - [Section 24.2.3.3, "To Run the simplegreeting
Example"](#GJCZE)

### 24.2.3.1 To Build, Package, and Run the simplegreeting Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/cdi
    ```

4.  Select the `simplegreeting` folder.

5.  Click Open Project.

6.  To modify the `Printer.java` file, perform these steps:
    
    1.  Expand the Source Packages node.
    
    2.  Expand the `greetings` node.
    
    3.  Double-click the `Printer.java` file.
    
    4.  In the editor, comment out the `@Informal` annotation:
        
        ``` oac_no_warn
        @Inject
        //@Informal
        Greeting greeting;
        ```
    
    5.  Save the file.

7.  In the Projects tab, right-click the `simplegreeting` project and
    select Build.
    
    This command builds and packages the application into a WAR file,
    `simplegreeting.war`, located in the `target` directory, and then
    deploys it to GlassFish
Server.

### 24.2.3.2 To Build, Package, and Deploy the simplegreeting Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/cdi/simplegreeting/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the application into a WAR file,
    `simplegreeting.war`, located in the `target` directory, and then
    deploys it to GlassFish Server.

### 24.2.3.3 To Run the simplegreeting Example

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/simplegreeting
    ```
    
    The Simple Greeting page opens.

2.  Enter a name in the field.
    
    For example, suppose that you enter `Duke`.

3.  Click Say Hello.
    
    If you did not modify the `Printer.java` file, the following text
    string appears below the button:
    
    ``` oac_no_warn
    Hi, Duke!
    ```
    
    If you commented out the `@Informal` annotation in the
    `Printer.java` file, the following text string appears below the
    button:
    
    ``` oac_no_warn
    Hello, Duke.
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
<td><a href="cdi-basicexamples001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-basicexamples003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
