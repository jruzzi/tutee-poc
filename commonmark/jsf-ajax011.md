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
<td><a href="jsf-ajax010.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax012.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 13.11 The ajaxguessnumber Example Application

To demonstrate the advantages of using Ajax, revisit the `guessnumber`
example from [Chapter 8, "Introduction to
Facelets"](jsf-facelets.htm#GIEPX). If you modify this example to use
Ajax, the response need not be displayed on the `response.xhtml` page.
Instead, an asynchronous call is made to the bean on the server side,
and the response is displayed on the originating page by executing just
the input component rather than by form submission.

The source code for this application is in the
tut-install`/examples/web/jsf/ajaxguessnumber/` directory.

The following topics are addressed here:

  - [Section 13.11.1, "The ajaxguessnumber Source Files"](#GKOIJ)

  - [Section 13.11.2, "Running the ajaxguessnumber Example"](#GKOKE)

## 13.11.1 The ajaxguessnumber Source Files

The changes to the `guessnumber` application occur in two source files.

The following topics are addressed here:

  - [Section 13.11.1.1, "The ajaxgreeting.xhtml Facelets Page"](#GKOFW)

  - [Section 13.11.1.2, "The UserNumberBean Backing Bean"](#GKOHN)

  - [Section 13.11.1.3, "The DukesNumberBean CDI Managed
    Bean"](#CHDGAIGJ)

### 13.11.1.1 The ajaxgreeting.xhtml Facelets Page

The Facelets page for `ajaxguessnumber`, `ajaxgreeting.xhtml`, is almost
the same as the `greeting.xhtml` page for the `guessnumber` application:

``` oac_no_warn
<h:head>
    <h:outputStylesheet library="css" name="default.css"/>
    <title>Ajax Guess Number Facelets Application</title>
</h:head>
<h:body>
    <h:form id="AjaxGuess">
        <h:graphicImage value="#{resource['images:wave.med.gif']}"
                        alt="Duke waving his hand"/>
        <h2>
            Hi, my name is Duke. I am thinking of a number from
            #{dukesNumberBean.minimum} to #{dukesNumberBean.maximum}.
            Can you guess it?
        </h2>
        <p>
            <h:inputText id="userNo" 
                         title="Enter a number from 0 to 10:"
                         value="#{userNumberBean.userNumber}">
                <f:validateLongRange minimum="#{dukesNumberBean.minimum}"
                                     maximum="#{dukesNumberBean.maximum}"/>
            </h:inputText>

            <h:commandButton id="submit" value="Submit">
                <f:ajax execute="userNo" render="outputGroup" />
            </h:commandButton>
        </p>
        <p>
            <h:panelGroup layout="block" id="outputGroup">
                <h:outputText id="result" style="color:blue"
                              value="#{userNumberBean.response}"
                              rendered="#{!facesContext.validationFailed}"/>
                <h:message id="errors1" 
                           showSummary="true" 
                           showDetail="false"
                           style="color: #d20005;
                           font-family: 'New Century Schoolbook', serif;
                           font-style: oblique;
                           text-decoration: overline" 
                           for="userNo"/>
            </h:panelGroup>
        </p>
    </h:form>
</h:body>
```

The most important change is in the `h:commandButton` tag. The `action`
attribute is removed from the tag, and an `f:ajax` tag is added.

The `f:ajax` tag specifies that when the button is clicked the
`h:inputText` component with the `id` value `userNo` is executed. The
components within the `outputGroup` panel group are then rendered. If a
validation error occurs, the managed bean is not executed, and the
validation error message is displayed in the message pane. Otherwise,
the result of the guess is rendered in the `result` component.

### 13.11.1.2 The UserNumberBean Backing Bean

A small change is also made in the `UserNumberBean` code so that the
output component does not display any message for the default (null)
value of the property `response`. Here is the modified bean code:

``` oac_no_warn
public String getResponse() {
    if ((userNumber != null)
            && (userNumber.compareTo(dukesNumberBean.getRandomInt()) == 0)) {
        return "Yay! You got it!";
    }
    if (userNumber == null) {
        return null;
    } else {
        return "Sorry, " + userNumber + " is incorrect.";
    }
}
```

### 13.11.1.3 The DukesNumberBean CDI Managed Bean

The `DukesNumberBean` session-scoped CDI managed bean stores the range
of guessable numbers and the randomly chosen number from that range. It
is injected into `UserNumberBean` with the CDI `@Inject` annotation so
that the value of the random number can be compared to the number the
user submitted:

``` oac_no_warn
@Inject
DukesNumberBean dukesNumberBean;
```

You will learn more about CDI in [Chapter 23, "Introduction to Contexts
and Dependency Injection for Java EE"](cdi-basic.htm#GIWHB).

## 13.11.2 Running the ajaxguessnumber Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `ajaxguessnumber` application.

The following topics are addressed here:

  - [Section 13.11.2.1, "To Build, Package, and Deploy the
    ajaxguessnumber Example Using NetBeans IDE"](#GLHVU)

  - [Section 13.11.2.2, "To Build, Package, and Deploy the
    ajaxguessnumber Example Using Maven"](#GLHVQ)

  - [Section 13.11.2.3, "To Run the ajaxguessnumber
Example"](#GLHWE)

### 13.11.2.1 To Build, Package, and Deploy the ajaxguessnumber Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsf
    ```

4.  Select the `ajaxguessnumber` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `ajaxguessnumber` project and
    select Build.
    
    This command builds and deploys the
project.

### 13.11.2.2 To Build, Package, and Deploy the ajaxguessnumber Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsf/ajaxguessnumber/
    ```

3.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the application into a WAR file,
    `ajaxguessnumber.war`, located in the `target` directory. It then
    deploys the application.

### 13.11.2.3 To Run the ajaxguessnumber Example

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/ajaxguessnumber
    ```

2.  Enter a value in the field and click Submit.
    
    If the value is in the range of 0 to 10, a message states whether
    the guess is correct or incorrect. If the value is outside that
    range or if the value is not a number, an error message appears in
    red.

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
<td><a href="jsf-ajax010.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-ajax012.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
