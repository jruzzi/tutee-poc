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
<td><a href="cdi-adv-examples005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partwebsvcs.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 26.6 The decorators Example: Decorating a Bean

The `decorators` example, which is yet another variation on the
`encoder` example, shows how to use a decorator to implement additional
business logic for a bean.

The source files are located in the
tut-install`/examples/cdi/decorators/src/main/java/javaeetutorial/decorators/`
directory.

The following topics are addressed here:

  - [Section 26.6.1, "Overview of the decorators Example"](#CHDDDFCI)

  - [Section 26.6.2, "Components of the decorators Example"](#GKPAQ)

  - [Section 26.6.3, "Running the decorators Example"](#GKPBK)

## 26.6.1 Overview of the decorators Example

Instead of having the user choose between two alternative
implementations of an interface at deployment time or runtime, a
decorator adds some additional logic to a single implementation of the
interface.

The example includes an interface, an implementation of it, a decorator,
an interceptor, a managed bean, a Facelets page, and configuration
files.

## 26.6.2 Components of the decorators Example

The `decorators` example is very similar to the `encoder` example
described in [The encoder Example: Using
Alternatives](cdi-adv-examples002.htm#GKHPU). Instead of providing two
implementations of the `Coder` interface, however, this example provides
only the `CoderImpl` class. The decorator class, `CoderDecorator`,
rather than simply return the coded string, displays the input and
output strings' values and length.

The `CoderDecorator` class, like `CoderImpl`, implements the business
method of the `Coder` interface, `codeString`:

``` oac_no_warn
@Decorator
public abstract class CoderDecorator implements Coder {

    @Inject
    @Delegate
    @Any
    Coder coder;

    public String codeString(String s, int tval) {
        int len = s.length();

        return "\"" + s + "\" becomes " + "\"" + coder.codeString(s, tval) 
                + "\", " + len + " characters in length";
    }
}
```

The decorator's `codeString` method calls the delegate object's
`codeString` method to perform the actual encoding.

The `decorators` example includes the `Logged` interceptor binding and
`LoggedInterceptor` class from the `billpayment` example. For this
example, the interceptor is set on the `CoderBean.encodeString` method
and the `CoderImpl.codeString` method. The interceptor code is
unchanged; interceptors are usually reusable for different applications.

Except for the interceptor annotations, the `CoderBean` and `CoderImpl`
classes are identical to the versions in the `encoder` example.

The `beans.xml` file specifies both the decorator and the interceptor:

``` oac_no_warn
    <decorators>
        <class>javaeetutorial.decorators.CoderDecorator</class>
    </decorators>
    <interceptors>
        <class>javaeetutorial.decorators.LoggedInterceptor</class>
    </interceptors>
```

## 26.6.3 Running the decorators Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `decorators` application.

The following topics are addressed here:

  - [Section 26.6.3.1, "To Build, Package, and Deploy the decorators
    Example Using NetBeans IDE"](#GKPAG)

  - [Section 26.6.3.2, "To Build, Package, and Deploy the decorators
    Example Using Maven"](#GKPAJ)

  - [Section 26.6.3.3, "To Run the decorators
Example"](#GKPAN)

### 26.6.3.1 To Build, Package, and Deploy the decorators Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/cdi
    ```

4.  Select the `decorators` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `decorators` project and select
    Build.
    
    This command builds and packages the application into a WAR file,
    `decorators.war`, located in the `target` directory, and then
    deploys it to GlassFish
Server.

### 26.6.3.2 To Build, Package, and Deploy the decorators Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/cdi/decorators/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the application into a WAR file,
    `decorators.war`, located in the `target` directory, and then
    deploys it to GlassFish Server.

### 26.6.3.3 To Run the decorators Example

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/decorators
    ```

2.  On the Decorated String Encoder page, enter a string and the number
    of letters to shift by, and then click Encode.
    
    The output from the decorator method appears in blue on the Result
    line. For example, if you entered `Java` and `4`, you would see the
    following:
    
    ``` oac_no_warn
    "Java" becomes "Neze", 4 characters in length
    ```

3.  Examine the server log output.
    
    In NetBeans IDE, the output is visible in the GlassFish Server
    Output tab. Otherwise, view domain-dir`/logs/server.log`.
    
    The output from the interceptors
    appears:
    
    ``` oac_no_warn
    INFO: Entering method: encodeString in class javaeetutorial.decorators.CoderBean
    INFO: Entering method: codeString in class javaeetutorial.decorators.CoderImpl
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
<td><a href="cdi-adv-examples005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partwebsvcs.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
