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
<td><a href="jsf-advanced-cc003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 14.4 The compositecomponentexample Example Application

The `compositecomponentexample` application creates a composite
component that accepts a name (or any other string). The component
interacts with a managed bean that calculates whether the letters in the
name, if converted to numeric values, add up to a prime number. The
component displays the sum of the letter values and reports whether it
is or is not prime.

The `compositecomponentexample` application has a composite component
file, a using page, and a managed bean.

The source code for this application is in the
tut-install`/examples/web/jsf/compositecomponentexample/` directory.

The following topics are addressed here:

  - [Section 14.4.1, "The Composite Component File"](#GKHUU)

  - [Section 14.4.2, "The Using Page"](#GKHVX)

  - [Section 14.4.3, "The Managed Bean"](#GKHVQ)

  - [Section 14.4.4, "Running the compositecomponentexample
    Example"](#GLECV)

## 14.4.1 The Composite Component File

The composite component file is an XHTML file,
`/web/resources/ezcomp/PrimePanel.xhtml`. It has a `composite:interface`
section that declares the labels for the name and a command button. It
also declares a managed bean, which defines properties for the name.

``` oac_no_warn
<composite:interface>
    <composite:attribute name="namePrompt" 
                         default="Name, word, or phrase: "/>
    <composite:attribute name="calcButtonText" default="Calculate"/>
    <composite:attribute name="calcAction"
                         method-signature="java.lang.String action()"/>
    <composite:attribute name="primeBean"/>
    <composite:editableValueHolder name="nameVal" targets="form:name"/>
</composite:interface>
```

The composite component implementation accepts the input value for the
`name` property of the managed bean. The `h:outputStylesheet` tag
specifies the stylesheet as a relocatable resource. The implementation
then specifies the format of the output, using properties of the managed
bean, as well as the format of error messages. The sum value is rendered
only after it has been calculated, and the report of whether the sum is
prime or not is rendered only if the input value is validated.

``` oac_no_warn
<composite:implementation>
    <h:form id="form">
        <h:outputStylesheet library="css" name="default.css" 
                            target="head"/>
        <h:panelGrid columns="2" role="presentation">
            <h:outputLabel for="name"
                           value="#{cc.attrs.namePrompt}"/>
            <h:inputText id="name"
                         size="45"
                         value="#{cc.attrs.primeBean.name}" 
                         required="true"/>
        </h:panelGrid>        
        <p>
            <h:commandButton id="calcButton" 
                             value="#{cc.attrs.calcButtonText}"
                             action="#{cc.attrs.calcAction}">
                <f:ajax execute="name" render="outputGroup"/>
            </h:commandButton>
        </p>
       
       <h:panelGroup id="outputGroup" layout="block">
            <p>
                <h:outputText id="result" style="color:blue"
                              rendered="#{cc.attrs.primeBean.totalSum gt 0}"
                              value="Sum is #{cc.attrs.primeBean.totalSum}" />
            </p>
            <p>
                <h:outputText id="response" style="color:blue"
                              value="#{cc.attrs.primeBean.response}"
                              rendered="#{!facesContext.validationFailed}"/>
                <h:message id="errors1" 
                           showSummary="true" 
                           showDetail="false"
                           style="color: #d20005;
                           font-family: 'New Century Schoolbook', serif;
                           font-style: oblique;
                           text-decoration: overline" 
                           for="name"/>
            </p>
        </h:panelGroup>
    </h:form>
</composite:implementation>
```

## 14.4.2 The Using Page

The using page in this example application, `web/index.xhtml`, is an
XHTML file that invokes the `PrimePanel.xhtml` composite component file
along with the managed bean. It validates the user's input.

``` oac_no_warn
<div id="compositecomponent">
    <ez:PrimePanel primeBean="#{primeBean}"  
                   calcAction="#{primeBean.calculate}">
    </ez:PrimePanel>
</div>
```

## 14.4.3 The Managed Bean

The managed bean, `PrimeBean.java`, defines a method called `calculate`,
which performs the calculations on the input string and sets properties
accordingly. The bean first creates an array of prime numbers. It
calculates the sum of the letters in the string, with `'a'` equal to 1
and `'z'` equal to 26, and determines whether the value can be found in
the array of primes. An uppercase letter in the input string has the
same value as its lowercase equivalent.

The bean specifies the minimum and maximum size of the `name` string,
which is enforced by the Bean Validation `@Size` constraint. The bean
uses the `@Model` annotation, a shortcut for `@Named` and
`@RequestScoped`, as described in Step [7](webapp003.htm#CHDCABHC) of
[To View the hello1 Web Module Using NetBeans IDE](webapp003.htm#GJWTV).

``` oac_no_warn
@Model
public class PrimeBean implements Serializable {
    ...
    @Size(min=1, max=45)
    private String name;
    ...

    public String calculate() {
        ...
    }
}
```

## 14.4.4 Running the compositecomponentexample Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `compositecomponentexample` example.

The following topics are addressed here:

  - [Section 14.4.4.1, "To Build, Package, and Deploy the
    compositecomponentexample Example Using NetBeans IDE"](#GKHVC)

  - [Section 14.4.4.2, "To Build, Package, and Deploy the
    compositecomponentexample Example Using Maven"](#GLEAE)

  - [Section 14.4.4.3, "To Run the compositecomponentexample
    Example"](#GLEEU)

### 14.4.4.1 To Build, Package, and Deploy the compositecomponentexample Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsf
    ```

4.  Select the `compositecomponentexample` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `compositecomponentexample`
    project and select Build.
    
    This command builds and deploys the
application.

### 14.4.4.2 To Build, Package, and Deploy the compositecomponentexample Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/web/jsf/compositecomponentexample/
    ```

3.  Enter the following command to build and deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```

### 14.4.4.3 To Run the compositecomponentexample Example

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/compositecomponentexample
    ```

2.  On the page that appears, enter a string in the Name, word, or
    phrase field, then click Calculate.
    
    The page reports the sum of the letters and whether the sum is
    prime. A validation error is reported if no value is entered or if
    the string contains more than 45 characters.

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
<td><a href="jsf-advanced-cc003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-custom.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
