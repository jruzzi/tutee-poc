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
<td><a href="ejb-gettingstarted001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-gettingstarted003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 33.2 Creating the Enterprise Bean

The enterprise bean in our example is a stateless session bean called
`ConverterBean`. The source code for `ConverterBean` is in the
tut-install`/examples/ejb/converter/src/main/java/` directory.

Creating `ConverterBean` requires these steps:

1.  Coding the bean's implementation class (the source code is provided)

2.  Compiling the source code

## 33.2.1 Coding the Enterprise Bean Class

The enterprise bean class for this example is called `ConverterBean`.
This class implements two business methods: `dollarToYen` and
`yenToEuro`. Because the enterprise bean class doesn't implement a
business interface, the enterprise bean exposes a local, no-interface
view. The public methods in the enterprise bean class are available to
clients that obtain a reference to `ConverterBean`. The source code for
the `ConverterBean` class is as follows:

``` oac_no_warn
package javaeetutorial.converter.ejb;

import java.math.BigDecimal;
import javax.ejb.*;

@Stateless
public class ConverterBean {
    private BigDecimal yenRate = new BigDecimal("83.0602");
    private BigDecimal euroRate = new BigDecimal("0.0093016");

    public BigDecimal dollarToYen(BigDecimal dollars) {
        BigDecimal result = dollars.multiply(yenRate);
        return result.setScale(2, BigDecimal.ROUND_UP);
    }

    public BigDecimal yenToEuro(BigDecimal yen) {
        BigDecimal result = yen.multiply(euroRate);
        return result.setScale(2, BigDecimal.ROUND_UP);
    }
}
```

Note the `@Stateless` annotation decorating the enterprise bean class.
This annotation lets the container know that `ConverterBean` is a
stateless session bean.

## 33.2.2 Creating the converter Web Client

The web client is contained in the following servlet class under the
tut-install`/examples/ejb/converter/src/main/java/` directory:

``` oac_no_warn
converter/web/ConverterServlet.java
```

A Java servlet is a web component that responds to HTTP requests.

The `ConverterServlet` class uses dependency injection to obtain a
reference to `ConverterBean`. The `javax.ejb.EJB` annotation is added to
the declaration of the private member variable `converter`, which is of
type `ConverterBean`. `ConverterBean` exposes a local, no-interface
view, so the enterprise bean implementation class is the variable type:

``` oac_no_warn
@WebServlet(urlPatterns="/")
public class ConverterServlet extends HttpServlet {
  @EJB
  ConverterBean converter;
  ...
}
```

When the user enters an amount to be converted to yen and euro, the
amount is retrieved from the request parameters; then the
`ConverterBean.dollarToYen` and the `ConverterBean.yenToEuro` methods
are called:

``` oac_no_warn
...
try {
  String amount = request.getParameter("amount");
  if (amount != null && amount.length()> 0) {
    // convert the amount to a BigDecimal from the request parameter
    BigDecimal d = new BigDecimal(amount);
    // call the ConverterBean.dollarToYen() method to get the amount
    // in Yen
    BigDecimal yenAmount = converter.dollarToYen(d);

    // call the ConverterBean.yenToEuro() method to get the amount
    // in Euros
    BigDecimal euroAmount = converter.yenToEuro(yenAmount);
    ...
  }
  ...
}
```

The results are displayed to the user.

## 33.2.3 Running the converter Example

Now you are ready to compile the enterprise bean class
(`ConverterBean.java`) and the servlet class (`ConverterServlet.java`)
and to package the compiled classes into a WAR file. You can use either
NetBeans IDE or Maven to build, package, deploy, and run the `converter`
example.

The following topics are addressed here:

  - [Section 33.2.3.1, "To Run the converter Example Using NetBeans
    IDE"](#GIPUM)

  - [Section 33.2.3.2, "To Run the converter Example Using
    Maven"](#GIPVQ)

### 33.2.3.1 To Run the converter Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/ejb
    ```

4.  Select the `converter` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `converter` project and select
    Build.

7.  Open a web browser to the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/converter
    ```

8.  On the Servlet ConverterServlet page, enter `100` in the field and
    click Submit.
    
    A second page opens, showing the converted values.

### 33.2.3.2 To Run the converter Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/ejb/converter/
    ```

3.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command compiles the source files for the enterprise bean and
    the servlet, packages the project into a WAR module
    (`converter.war`), and deploys the WAR to the server. For more
    information about Maven, see [Building the
    Examples](usingexamples005.htm#BNAAN).

4.  Open a web browser to the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/converter
    ```

5.  On the Servlet ConverterServlet page, enter `100` in the field and
    click Submit.
    
    A second page opens, showing the converted values.

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
<td><a href="ejb-gettingstarted001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-gettingstarted003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
