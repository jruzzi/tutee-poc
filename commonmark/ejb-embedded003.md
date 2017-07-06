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
<td><a href="ejb-embedded002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-async.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 35.3 The standalone Example Application

The `standalone` example application demonstrates how to create an
instance of the embedded enterprise bean container in a JUnit test class
and call a session bean business method.

The following topics are addressed here:

  - [Section 35.3.1, "Overview of the standalone Example
    Application"](#BEIDAJAC)

  - [Section 35.3.2, "To Run the standalone Example Application Using
    NetBeans IDE"](#GKCQP)

  - [Section 35.3.3, "To Run the standalone Example Application Using
    Maven"](#BEIGHEHJ)

## 35.3.1 Overview of the standalone Example Application

Testing the business methods of an enterprise bean in a unit test allows
developers to exercise the business logic of an application separately
from the other application layers, such as the presentation layer, and
without having to deploy the application to a Java EE server.

The `standalone` example has two main components: `StandaloneBean`, a
stateless session bean, and `StandaloneBeanTest`, a JUnit test class
that acts as a client to `StandaloneBean` using the embedded container.

`StandaloneBean` is a simple session bean exposing a local, no-interface
view with a single business method, `returnMessage`, which returns
"Greetings\!" as a `String`:

``` oac_no_warn
@Stateless
public class StandaloneBean {

    private static final String message = "Greetings!";

    public String returnMessage() {
        return message;
    }
    
}
```

`StandaloneBeanTest` calls `StandaloneBean.returnMessage` and tests that
the returned message is correct. First, an embedded container instance
and initial context are created within the `setUp` method, which is
annotated with `org.junit.Before` to indicate that the method should be
executed before the test methods:

``` oac_no_warn
@Before
public void setUp() {
    ec = EJBContainer.createEJBContainer();
    ctx = ec.getContext();
}
```

The `testReturnMessage` method, annotated with `org.junit.Test` to
indicate that the method includes a unit test, obtains a reference to
`StandaloneBean` through the `Context` instance, and calls
`StandaloneBean.returnMessage`. The result is compared with the expected
result using a JUnit assertion, `assertEquals`. If the string returned
from `StandaloneBean.returnMessage` is equal to "Greetings\!" the test
passes:

``` oac_no_warn
@Test
public void testReturnMessage() throws Exception {
    logger.info("Testing standalone.ejb.StandaloneBean.returnMessage()");
    StandaloneBean instance = (StandaloneBean)
            ctx.lookup("java:global/classes/StandaloneBean");
    String expResult = "Greetings!";
    String result = instance.returnMessage();
    assertEquals(expResult, result);
}
```

Finally, the `tearDown` method, annotated with `org.junit.After` to
indicate that the method should be executed after all the unit tests
have run, closes the embedded container instance:

``` oac_no_warn
@After
public void tearDown() {
    if (ec != null) {
        ec.close();
    }
}
```

## 35.3.2 To Run the standalone Example Application Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/ejb
    ```

4.  Select the `standalone` folder and click Open Project.

5.  In the Projects tab, right-click `standalone` and select Test.
    
    This will execute the JUnit test class `StandaloneBeanTest`. The
    Output tab shows the progress of the test and the output log.

## 35.3.3 To Run the standalone Example Application Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/ejb/standalone/
    ```

3.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command compiles and packages the application into an JAR file,
    and executes the JUnit test class `StandaloneBeanTest`.

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
<td><a href="ejb-embedded002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-async.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
