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
<td><a href="cdi-adv-examples002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv-examples004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft:
2017-06-12

# 26.3 The producermethods Example: Using a Producer Method to Choose a Bean Implementation

The `producermethods` example shows how to use a producer method to
choose between two beans at runtime, as described in [Using Producer
Methods, Producer Fields, and Disposer Methods in CDI
Applications](cdi-adv003.htm#GKGKV). It is very similar to the `encoder`
example described in [The encoder Example: Using
Alternatives](cdi-adv-examples002.htm#GKHPU). The example includes the
same interface and two implementations of it, a managed bean, a Facelets
page, and configuration files. It also contains a qualifier type. When
you run it, you do not need to edit the `beans.xml` file and redeploy
the application to change its behavior.

The following topics are addressed here:

  - [Section 26.3.1, "Components of the producermethods
    Example"](#GKHRO)

  - [Section 26.3.2, "Running the producermethods Example"](#GKHQE)

## 26.3.1 Components of the producermethods Example

The components of `producermethods` are very much like those for
`encoder`, with some significant differences.

Neither implementation of the `Coder` bean is annotated `@Alternative`,
and there is no `beans.xml` file, because it is not needed.

The Facelets page and the managed bean, `CoderBean`, have an additional
property, `coderType`, that allows the user to specify at runtime which
implementation to use. In addition, the managed bean has a producer
method that selects the implementation using a qualifier type,
`@Chosen`.

The bean declares two constants that specify whether the coder type is
the test implementation or the implementation that actually shifts
letters:

``` oac_no_warn
    private final static int TEST = 1;
    private final static int SHIFT = 2;
    private int coderType = SHIFT; // default value
```

The producer method, annotated with `@Produces` and `@Chosen` as well as
`@RequestScoped` (so that it lasts only for the duration of a single
request and response), returns one of the two implementations based on
the `coderType` supplied by the user.

``` oac_no_warn
    @Produces
    @Chosen
    @RequestScoped
    public Coder getCoder() {

        switch (coderType) {
            case TEST:
                return new TestCoderImpl();
            case SHIFT:
                return new CoderImpl();
            default:
                return null;
        }
    }
```

Finally, the managed bean injects the chosen implementation, specifying
the same qualifier as that returned by the producer method to resolve
ambiguities:

``` oac_no_warn
    @Inject
    @Chosen
    @RequestScoped
    Coder coder;
```

The Facelets page contains modified instructions and a pair of options
whose selected value is assigned to the property `coderBean.coderType`:

``` oac_no_warn
    <h2>String Encoder</h2>
        <p>Select Test or Shift, type a string and an integer, then click
            Encode.</p>
        <p>If you select Test, the TestCoderImpl bean will display the
            argument values.</p>
        <p>If you select Shift, the CoderImpl bean will return a string that
            shifts the letters in the original string by the value you specify.
            The value must be between 0 and 26.</p>
        <h:form id="encodeit">
            <h:selectOneRadio id="coderType"
                              required="true"
                              value="#{coderBean.coderType}">
                <f:selectItem
                    itemValue="1"
                    itemLabel="Test"/>
                <f:selectItem
                    itemValue="2"
                    itemLabel="Shift Letters"/>
            </h:selectOneRadio>
            ...
```

## 26.3.2 Running the producermethods Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `producermethods` application.

The following topics are addressed here:

  - [Section 26.3.2.1, "To Build, Package, and Deploy the
    producermethods Example Using NetBeans IDE"](#GKHPE)

  - [Section 26.3.2.2, "To Build, Package, and Deploy the
    producermethods Example Using Maven"](#GKHPS)

  - [Section 26.3.2.3, "To Run the producermethods
Example"](#GKHQG)

### 26.3.2.1 To Build, Package, and Deploy the producermethods Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/cdi
    ```

4.  Select the `producermethods` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `producermethods` project and
    select Build.
    
    This command builds and packages the application into a WAR file,
    `producermethods.war`, located in the `target` directory, and then
    deploys it to GlassFish
Server.

### 26.3.2.2 To Build, Package, and Deploy the producermethods Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/cdi/producermethods/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the application into a WAR file,
    `producermethods.war`, located in the `target` directory, and then
    deploys it to GlassFish Server.

### 26.3.2.3 To Run the producermethods Example

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/producermethods
    ```

2.  On the String Encoder page, select either the Test or Shift Letters
    option, enter a string and the number of letters to shift by, and
    then click Encode.
    
    Depending on your selection, the Result line displays either the
    encoded string or the input values you specified.

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
<td><a href="cdi-adv-examples002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv-examples004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
