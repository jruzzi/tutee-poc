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
<td><a href="cdi-basicexamples002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 24.3 The guessnumber-cdi CDI Example

The `guessnumber-cdi` example, somewhat more complex than the
`simplegreeting` example, illustrates the use of producer methods and of
session and application scope. The example is a game in which you try to
guess a number in fewer than ten attempts. It is similar to the
`guessnumber-jsf` example described in [Chapter 8, "Introduction to
Facelets"](jsf-facelets.htm#GIEPX), except that you can keep guessing
until you get the right answer or until you use up your ten attempts.

The example includes four source files, a Facelets page and template,
and configuration files. The configuration files and the template are
the same as those used for the `simplegreeting` example.

The following topics are addressed here:

  - [Section 24.3.1, "The guessnumber-cdi Source Files"](#GJDJU)

  - [Section 24.3.2, "The Facelets Page"](#GJDON)

  - [Section 24.3.3, "Running the guessnumber-cdi Example"](#GJDPW)

## 24.3.1 The guessnumber-cdi Source Files

The four source files for the `guessnumber-cdi` example are

  - The `@MaxNumber` qualifier interface

  - The `@Random` qualifier interface

  - The `Generator` managed bean, which defines producer methods

  - The `UserNumberBean` managed bean

The source files are located in the
tut-install`/examples/cdi/guessnumber-cdi/src/main/java/javaeetutorial/guessnumber`
directory.

### 24.3.1.1 The @MaxNumber and @Random Qualifier Interfaces

The `@MaxNumber` qualifier interface is defined as follows:

``` oac_no_warn
package guessnumber;

import java.lang.annotation.Documented;
import static java.lang.annotation.ElementType.FIELD;
import static java.lang.annotation.ElementType.METHOD;
import static java.lang.annotation.ElementType.PARAMETER;
import static java.lang.annotation.ElementType.TYPE;
import java.lang.annotation.Retention;
import static java.lang.annotation.RetentionPolicy.RUNTIME;
import java.lang.annotation.Target;
import javax.inject.Qualifier;

@Target({TYPE, METHOD, PARAMETER, FIELD})
@Retention(RUNTIME)
@Documented
@Qualifier
public @interface MaxNumber {
}
```

The `@Random` qualifier interface is defined as follows:

``` oac_no_warn
package guessnumber;

import java.lang.annotation.Documented;
import static java.lang.annotation.ElementType.FIELD;
import static java.lang.annotation.ElementType.METHOD;
import static java.lang.annotation.ElementType.PARAMETER;
import static java.lang.annotation.ElementType.TYPE;
import java.lang.annotation.Retention;
import static java.lang.annotation.RetentionPolicy.RUNTIME;
import java.lang.annotation.Target;
import javax.inject.Qualifier;

@Target({TYPE, METHOD, PARAMETER, FIELD})
@Retention(RUNTIME)
@Documented
@Qualifier
public @interface Random {
}
```

### 24.3.1.2 The Generator Managed Bean

The `Generator` managed bean contains the two producer methods for the
application. The bean has the `@ApplicationScoped` annotation to specify
that its context extends for the duration of the user's interaction with
the application:

``` oac_no_warn
package guessnumber;

import java.io.Serializable;
import javax.enterprise.context.ApplicationScoped;
import javax.enterprise.inject.Produces;

@ApplicationScoped
public class Generator implements Serializable {

    private static final long serialVersionUID = -7213673465118041882L;

    private final java.util.Random random = 
        new java.util.Random( System.currentTimeMillis() );

    private final int maxNumber = 100;

    java.util.Random getRandom() {
        return random;
    }

    @Produces @Random int next() {
        return getRandom().nextInt(maxNumber + 1);
    }

    @Produces @MaxNumber int getMaxNumber() {
        return maxNumber;
    }

}
```

### 24.3.1.3 The UserNumberBean Managed Bean

The `UserNumberBean` managed bean, the managed bean for the JavaServer
Faces application, provides the basic logic for the game. This bean does
the following:

  - Implements setter and getter methods for the bean fields

  - Injects the two qualifier objects

  - Provides a `reset` method that allows you to begin a new game after
    you complete one

  - Provides a `check` method that determines whether the user has
    guessed the number

  - Provides a `validateNumberRange` method that determines whether the
    user's input is correct

The bean is defined as follows:

``` oac_no_warn
package guessnumber;

import java.io.Serializable;
import javax.annotation.PostConstruct;
import javax.enterprise.context.SessionScoped;
import javax.enterprise.inject.Instance;
import javax.faces.application.FacesMessage;
import javax.faces.component.UIComponent;
import javax.faces.component.UIInput;
import javax.faces.context.FacesContext;
import javax.inject.Inject;
import javax.inject.Named;

@Named
@SessionScoped
public class UserNumberBean implements Serializable {

    private static final long serialVersionUID = -7698506329160109476L;

    private int number;
    private Integer userNumber;
    private int minimum;
    private int remainingGuesses;

    @MaxNumber
    @Inject
    private int maxNumber;

    private int maximum;

    @Random
    @Inject
    Instance<Integer> randomInt;

    public UserNumberBean() {
    }

    public int getNumber() {
        return number;
    }

    public void setUserNumber(Integer user_number) {
        userNumber = user_number;
    }

    public Integer getUserNumber() {
        return userNumber;
    }

    public int getMaximum() {
        return (this.maximum);
    }

    public void setMaximum(int maximum) {
        this.maximum = maximum;
    }

    public int getMinimum() {
        return (this.minimum);
    }

    public void setMinimum(int minimum) {
        this.minimum = minimum;
    }

    public int getRemainingGuesses() {
        return remainingGuesses;
    }

    public String check() throws InterruptedException {
        if (userNumber > number) {
            maximum = userNumber - 1;
        }
        if (userNumber < number) {
            minimum = userNumber + 1;
        }
        if (userNumber == number) {
            FacesContext.getCurrentInstance().addMessage(null, 
                new FacesMessage("Correct!"));
        }
        remainingGuesses--;
        return null;
    }

    @PostConstruct
    public void reset() {
        this.minimum = 0;
        this.userNumber = 0;
        this.remainingGuesses = 10;
        this.maximum = maxNumber;
        this.number = randomInt.get();
    }

    public void validateNumberRange(FacesContext context, 
                                    UIComponent toValidate, 
                                    Object value) {
        int input = (Integer) value;

        if (input < minimum || input > maximum) {
            ((UIInput) toValidate).setValid(false);

            FacesMessage message = new FacesMessage("Invalid guess");
            context.addMessage(toValidate.getClientId(context), message);
        }
    }
}
```

## 24.3.2 The Facelets Page

This example uses the same template that the `simplegreeting` example
uses. The `index.xhtml` file, however, is more complex.

``` oac_no_warn
<?xml version='1.0' encoding='UTF-8' ?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" 
          "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html lang="en"
      xmlns="http://www.w3.org/1999/xhtml"
      xmlns:ui="http://xmlns.jcp.org/jsf/facelets"
      xmlns:h="http://xmlns.jcp.org/jsf/html">
    <ui:composition template="/template.xhtml">

        <ui:define name="title">Guess My Number</ui:define>
        <ui:define name="head">Guess My Number</ui:define>
        <ui:define name="content">
            <h:form id="GuessMain">
                <div style="color: black; font-size: 24px;">
                    <p>I'm thinking of a number from 
                    <span style="color: blue">#{userNumberBean.minimum}</span> 
                    to 
                    <span style="color: blue">#{userNumberBean.maximum}</span>. 
                    You have 
                    <span style="color: blue">
                        #{userNumberBean.remainingGuesses}
                    </span> 
                    guesses.</p>
                </div>
                <h:panelGrid border="0" columns="5" style="font-size: 18px;">
                    <h:outputLabel for="inputGuess">Number:</h:outputLabel>
                    <h:inputText id="inputGuess"
                                 value="#{userNumberBean.userNumber}"
                                 required="true" size="3"
disabled="#{userNumberBean.number eq userNumberBean.userNumber or userNumberBean.remainingGuesses le 0}"
                               validator="#{userNumberBean.validateNumberRange}">
                    </h:inputText>
                    <h:commandButton id="GuessButton" value="Guess"
                                     action="#{userNumberBean.check}"
disabled="#{userNumberBean.number eq userNumberBean.userNumber or userNumberBean.remainingGuesses le 0}"/>
                    <h:commandButton id="RestartButton" value="Reset"
                                     action="#{userNumberBean.reset}"
                                     immediate="true" />
                    <h:outputText id="Higher" value="Higher!"
rendered="#{userNumberBean.number gt userNumberBean.userNumber and userNumberBean.userNumber ne 0}"
                                  style="color: #d20005"/>
                    <h:outputText id="Lower" value="Lower!"
rendered="#{userNumberBean.number lt userNumberBean.userNumber and userNumberBean.userNumber ne 0}"
                                  style="color: #d20005"/>
                </h:panelGrid>
                <div style="color: #d20005; font-size: 14px;">
                    <h:messages id="messages" globalOnly="false"/>
                </div>
            </h:form>
        </ui:define>
        
    </ui:composition>
</html>
```

The Facelets page presents the user with the minimum and maximum values
and the number of guesses remaining. The user's interaction with the
game takes place within the `panelGrid` table, which contains an input
field, Guess and Reset buttons, and a field that appears if the guess is
higher or lower than the correct number. Every time the user clicks the
Guess button, the `userNumberBean.check` method is called to reset the
maximum or minimum value or, if the guess is correct, to generate a
`FacesMessage` to that effect. The method that determines whether each
guess is valid is `userNumberBean.validateNumberRange`.

## 24.3.3 Running the guessnumber-cdi Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `guessnumber-cdi` application.

The following topics are addressed here:

  - [Section 24.3.3.1, "To Build, Package, and Deploy the
    guessnumber-cdi Example Using NetBeans IDE"](#GJDPS)

  - [Section 24.3.3.2, "To Build, Package, and Deploy the
    guessnumber-cdi Example Using Maven"](#GJDPR)

  - [Section 24.3.3.3, "To Run the guessnumber
Example"](#GJDQB)

### 24.3.3.1 To Build, Package, and Deploy the guessnumber-cdi Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/cdi
    ```

4.  Select the `guessnumber-cdi` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `guessnumber-cdi` project and
    select Build.
    
    This command builds and packages the application into a WAR file,
    `guessnumber-cdi.war`, located in the `target` directory, and then
    deploys it to GlassFish
Server.

### 24.3.3.2 To Build, Package, and Deploy the guessnumber-cdi Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/cdi/guessnumber-cdi/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This command builds and packages the application into a WAR file,
    `guessnumber-cdi.war`, located in the `target` directory, and then
    deploys it to GlassFish Server.

### 24.3.3.3 To Run the guessnumber Example

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/guessnumber-cdi
    ```
    
    The Guess My Number page opens.

2.  On the Guess My Number page, enter a number in the Number field and
    click Guess.
    
    The minimum and maximum values are modified, along with the
    remaining number of guesses.

3.  Keep guessing numbers until you get the right answer or run out of
    guesses.
    
    If you get the right answer or run out of guesses, the input field
    and Guess button are grayed out.

4.  Click Reset to play the game again with a new random number.

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
<td><a href="cdi-basicexamples002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
