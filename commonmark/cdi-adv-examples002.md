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
<td><a href="cdi-adv-examples001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv-examples003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 26.2 The encoder Example: Using Alternatives

The `encoder` example shows how to use alternatives to choose between
two beans at deployment time, as described in [Using Alternatives in CDI
Applications](cdi-adv002.htm#GJSDF). The example includes an interface
and two implementations of it, a managed bean, a Facelets page, and
configuration files.

The source files are located in the
tut-install`/examples/cdi/encoder/src/main/java/javaeetutorial/encoder/`
directory.

The following topics are addressed here:

  - [Section 26.2.1, "The Coder Interface and Implementations"](#GKHQA)

  - [Section 26.2.2, "The encoder Facelets Page and Managed
    Bean"](#GKHPM)

  - [Section 26.2.3, "Running the encoder Example"](#GKHQQ)

## 26.2.1 The Coder Interface and Implementations

The `Coder` interface contains just one method, `codeString`, that takes
two arguments: a string, and an integer value that specifies how the
letters in the string should be transposed.

``` oac_no_warn
public interface Coder {

    public String codeString(String s, int tval);
}
```

The interface has two implementation classes, `CoderImpl` and
`TestCoderImpl`. The implementation of `codeString` in `CoderImpl`
shifts the string argument forward in the alphabet by the number of
letters specified in the second argument; any characters that are not
letters are left unchanged. (This simple shift code is known as a Caesar
cipher because Julius Caesar reportedly used it to communicate with his
generals.) The implementation in `TestCoderImpl` merely displays the
values of the arguments. The `TestCoderImpl` implementation is annotated
`@Alternative`:

``` oac_no_warn
import javax.enterprise.inject.Alternative;

@Alternative
public class TestCoderImpl implements Coder {

    @Override
    public String codeString(String s, int tval) {
        return ("input string is " + s + ", shift value is " + tval);
    }
}
```

The `beans.xml` file for the `encoder` example contains an
`alternatives` element for the `TestCoderImpl` class, but by default the
element is commented out:

``` oac_no_warn
<beans ...>
    <!--<alternatives>
        <class>javaeetutorial.encoder.TestCoderImpl</class>
    </alternatives>-->
</beans>
```

This means that by default, the `TestCoderImpl` class, annotated
`@Alternative`, will not be used. Instead, the `CoderImpl` class will be
used.

## 26.2.2 The encoder Facelets Page and Managed Bean

The simple Facelets page for the `encoder` example, `index.xhtml`, asks
the user to enter the string and integer values and passes them to the
managed bean, `CoderBean`, as `coderBean.inputString` and
`coderBean.transVal`:

``` oac_no_warn
<html lang="en"
      xmlns="http://www.w3.org/1999/xhtml"
      xmlns:h="http://java.sun.com/jsf/html">
    <h:head>
        <h:outputStylesheet library="css" name="default.css"/>
        <title>String Encoder</title>
    </h:head>
    <h:body>
        <h2>String Encoder</h2>
        <p>Type a string and an integer, then click Encode.</p>
        <p>Depending on which alternative is enabled, the coder bean
            will either display the argument values or return a string that
            shifts the letters in the original string by the value you
            specify. The value must be between 0 and 26.</p>
        <h:form id="encodeit">
            <p><h:outputLabel value="Enter a string: " for="inputString"/>
                <h:inputText id="inputString"
                             value="#{coderBean.inputString}"/>
                <h:outputLabel value="Enter the number of letters to shift by: "
                               for="transVal"/>
                <h:inputText id="transVal" value="#{coderBean.transVal}"/></p>
            <p><h:commandButton value="Encode"
                                action="#{coderBean.encodeString()}"/></p>
            <p><h:outputLabel value="Result: " for="outputString"/>
                <h:outputText id="outputString"
                              value="#{coderBean.codedString}"
                              style="color:blue"/></p>
            <p><h:commandButton value="Reset"
                                action="#{coderBean.reset}"/></p>
        </h:form>
        ...
    </h:body>
</html>
```

When the user clicks the Encode button, the page invokes the managed
bean's `encodeString` method and displays the result,
`coderBean.codedString`, in blue. The page also has a Reset button that
clears the fields.

The managed bean, `CoderBean`, is a `@RequestScoped` bean that declares
its input and output properties. The `transVal` property has three Bean
Validation constraints that enforce limits on the integer value, so that
if the user enters an invalid value, a default error message appears on
the Facelets page. The bean also injects an instance of the `Coder`
interface:

``` oac_no_warn
@Named
@RequestScoped
public class CoderBean {

    private String inputString;
    private String codedString;
    @Max(26)
    @Min(0)
    @NotNull
    private int transVal;

    @Inject
    Coder coder;
    ...
```

In addition to simple getter and setter methods for the three
properties, the bean defines the `encodeString` action method called by
the Facelets page. This method sets the `codedString` property to the
value returned by a call to the `codeString` method of the `Coder`
implementation:

``` oac_no_warn
    public void encodeString() {
        setCodedString(coder.codeString(inputString, transVal));
    }
```

Finally, the bean defines the `reset` method to empty the fields of the
Facelets page:

``` oac_no_warn
    public void reset() {
        setInputString("");
        setTransVal(0);
    }
```

## 26.2.3 Running the encoder Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `encoder`
application.

### 26.2.3.1 To Build, Package, and Deploy the encoder Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/cdi
    ```

4.  Select the `encoder` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `encoder` project and select
    Build.
    
    This command builds and packages the application into a WAR file,
    `encoder.war`, located in the `target` directory, and then deploys
    it to GlassFish Server.

### 26.2.3.2 To Run the encoder Example Using NetBeans IDE

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/encoder
    ```

2.  On the String Encoder page, enter a string and the number of letters
    to shift by, and then click Encode.
    
    The encoded string appears in blue on the Result line. For example,
    if you enter `Java` and `4`, the result is `Neze`.

3.  Now, edit the `beans.xml` file to enable the alternative
    implementation of `Coder`.
    
    1.  In the Projects tab, under the `encoder` project, expand the Web
        Pages node, then expand the WEB-INF node.
    
    2.  Double-click the `beans.xml` file to open it.
    
    3.  Remove the comment characters that surround the `alternatives`
        element, so that it looks like this:
        
        ``` oac_no_warn
        <alternatives>
            <class>javaeetutorial.encoder.TestCoderImpl</class>
        </alternatives>
        ```
    
    4.  Save the file.

4.  Right-click the `encoder` project and select Clean and Build.

5.  In the web browser, reenter the URL to show the String Encoder page
    for the redeployed project:
    
    ``` oac_no_warn
    http://localhost:8080/encoder/
    ```

6.  Enter a string and the number of letters to shift by, and then click
    Encode.
    
    This time, the Result line displays your arguments. For example, if
    you enter `Java` and `4`, the result
is:
    
    ``` oac_no_warn
    Result: input string is Java, shift value is 4
    ```

### 26.2.3.3 To Build, Package, and Deploy the encoder Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/cdi/encoder/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the application into a WAR file,
    `encoder.war`, located in the `target` directory, and then deploys
    it to GlassFish Server.

### 26.2.3.4 To Run the encoder Example Using Maven

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/encoder/
    ```
    
    The String Encoder page opens.

2.  Enter a string and the number of letters to shift by, and then click
    Encode.
    
    The encoded string appears in blue on the Result line. For example,
    if you enter `Java` and `4`, the result is `Neze`.

3.  Now, edit the `beans.xml` file to enable the alternative
    implementation of `Coder`.
    
    1.  In a text editor, open the following
        file:
        
        ``` oac_no_warn
        tut-install/examples/cdi/encoder/src/main/webapp/WEB-INF/beans.xml
        ```
    
    2.  Remove the comment characters that surround the `alternatives`
        element, so that it looks like this:
        
        ``` oac_no_warn
        <alternatives>
            <class>javaeetutorial.encoder.TestCoderImpl</class>
        </alternatives>
        ```
    
    3.  Save and close the file.

4.  Enter the following command:
    
    ``` oac_no_warn
    mvn clean install
    ```

5.  In the web browser, reenter the URL to show the String Encoder page
    for the redeployed project:
    
    ``` oac_no_warn
    http://localhost:8080/encoder
    ```

6.  Enter a string and the number of letters to shift by, and then click
    Encode.
    
    This time, the Result line displays your arguments. For example, if
    you enter `Java` and `4`, the result is:
    
    ``` oac_no_warn
    Result: input string is Java, shift value is 4
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
<td><a href="cdi-adv-examples001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv-examples003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
