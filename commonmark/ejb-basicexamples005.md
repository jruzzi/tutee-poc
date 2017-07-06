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
<td><a href="ejb-basicexamples004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-basicexamples006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 34.5 Using the Timer Service

Applications that model business work flows often rely on timed
notifications. The timer service of the enterprise bean container
enables you to schedule timed notifications for all types of enterprise
beans except for stateful session beans. You can schedule a timed
notification to occur according to a calendar schedule, at a specific
time, after a duration of time, or at timed intervals. For example, you
could set timers to go off at 10:30 a.m. on May 23, in 30 days, or every
12 hours.

Enterprise bean timers are either programmatic timers or automatic
timers. Programmatic timers are set by explicitly calling one of the
timer creation methods of the `TimerService` interface. Automatic timers
are created upon the successful deployment of an enterprise bean that
contains a method annotated with the `javax.ejb.Schedule` or
`javax.ejb.Schedules` annotations.

## 34.5.1 Creating Calendar-Based Timer Expressions

Timers can be set according to a calendar-based schedule, expressed
using a syntax similar to the UNIX `cron` utility. Both programmatic and
automatic timers can use calendar-based timer expressions. [Table
34-1](#GIQLY) shows the calendar-based timer attributes.

Table 34-1 Calendar-Based Timer Attributes

<table style="width:51%;">
<colgroup>
<col width="15%" />
<col width="23%" />
<col width="13%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Description</th>
<th>Default Value</th>
<th>Allowable Values and Examples</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">second</code></p></td>
<td><p>One or more seconds within a minute</p></td>
<td><p><code dir="ltr">0</code></p></td>
<td><p><code dir="ltr">0</code> to <code dir="ltr">59</code>. For example: <code dir="ltr">second=&quot;30&quot;</code>.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">minute</code></p></td>
<td><p>One or more minutes within an hour</p></td>
<td><p><code dir="ltr">0</code></p></td>
<td><p><code dir="ltr">0</code> to <code dir="ltr">59</code>. For example: <code dir="ltr">minute=&quot;15&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">hour</code></p></td>
<td><p>One or more hours within a day</p></td>
<td><p><code dir="ltr">0</code></p></td>
<td><p><code dir="ltr">0</code> to <code dir="ltr">23</code>. For example: <code dir="ltr">hour=&quot;13&quot;</code>.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">dayOfWeek</code></p></td>
<td><p>One or more days within a week</p></td>
<td><p><code dir="ltr">*</code></p>
<br />
</td>
<td><p><code dir="ltr">0</code> to <code dir="ltr">7</code> (both 0 and 7 refer to Sunday). For example: <code dir="ltr">dayOfWeek=&quot;3&quot;</code>.</p>
<p><code dir="ltr">Sun</code>, <code dir="ltr">Mon</code>, <code dir="ltr">Tue</code>, <code dir="ltr">Wed</code>, <code dir="ltr">Thu</code>, <code dir="ltr">Fri</code>, <code dir="ltr">Sat</code>. For example: <code dir="ltr">dayOfWeek=&quot;Mon&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">dayOfMonth</code></p></td>
<td><p>One or more days within a month</p></td>
<td><p><code dir="ltr">*</code></p>
<br />
</td>
<td><p><code dir="ltr">1</code> to <code dir="ltr">31</code>. For example: <code dir="ltr">dayOfMonth=&quot;15&quot;</code>.</p>
<p><code dir="ltr">–7</code> to <code dir="ltr">–1</code> (a negative number means the <span class="variable">n</span>th day or days before the end of the month). For example: <code dir="ltr">dayOfMonth=&quot;–3&quot;</code>.</p>
<p><code dir="ltr">Last</code>. For example: <code dir="ltr">dayOfMonth=&quot;Last&quot;</code>.</p>
<p>[<code dir="ltr">1st</code>, <code dir="ltr">2nd</code>, <code dir="ltr">3rd</code>, <code dir="ltr">4th</code>, <code dir="ltr">5th</code>, <code dir="ltr">Last</code>] [<code dir="ltr">Sun</code>, <code dir="ltr">Mon</code>, <code dir="ltr">Tue</code>, <code dir="ltr">Wed</code>, <code dir="ltr">Thu</code>, <code dir="ltr">Fri</code>, <code dir="ltr">Sat</code>]. For example: <code dir="ltr">dayOfMonth=&quot;2nd Fri&quot;</code>.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">month</code></p></td>
<td><p>One or more months within a year</p></td>
<td><p><code dir="ltr">*</code></p>
<br />
</td>
<td><p><code dir="ltr">1</code> to <code dir="ltr">12</code>. For example: <code dir="ltr">month=&quot;7&quot;</code>.</p>
<p><code dir="ltr">Jan</code>, <code dir="ltr">Feb</code>, <code dir="ltr">Mar</code>, <code dir="ltr">Apr</code>, <code dir="ltr">May</code>, <code dir="ltr">Jun</code>, <code dir="ltr">Jul</code>, <code dir="ltr">Aug</code>, <code dir="ltr">Sep</code>, <code dir="ltr">Oct</code>, <code dir="ltr">Nov</code>, <code dir="ltr">Dec</code>. For example: <code dir="ltr">month=&quot;July&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">year</code></p></td>
<td><p>A particular calendar year</p></td>
<td><p><code dir="ltr">*</code></p>
<br />
</td>
<td><p>A four-digit calendar year. For example: <code dir="ltr">year=&quot;2011&quot;</code>.</p></td>
</tr>
</tbody>
</table>

  

### 34.5.1.1 Specifying Multiple Values in Calendar Expressions

You can specify multiple values in calendar expressions, as described in
the following sections.

Using Wildcards in Calendar Expressions

Setting an attribute to an asterisk symbol (`*`) represents all
allowable values for the attribute.

The following expression represents every minute:

``` oac_no_warn
minute="*"
```

The following expression represents every day of the week:

``` oac_no_warn
dayOfWeek="*"
```

Specifying a List of Values

To specify two or more values for an attribute, use a comma (`,`) to
separate the values. A range of values is allowed as part of a list.
Wildcards and intervals, however, are not allowed.

Duplicates within a list are ignored.

The following expression sets the day of the week to Tuesday and
Thursday:

``` oac_no_warn
dayOfWeek="Tue, Thu"
```

The following expression represents 4:00 a.m., every hour from 9:00 a.m.
to 5:00 p.m. using a range, and 10:00 p.m.:

``` oac_no_warn
hour="4,9-17,22"
```

Specifying a Range of Values

Use a dash character (`-`) to specify an inclusive range of values for
an attribute. Members of a range cannot be wildcards, lists, or
intervals. A range of the form `x-x`, is equivalent to the single-valued
expression `x`. A range of the form `x-y` where `x` is greater than `y`
is equivalent to the expression `x-`maximumvalue`,` minimumvalue`-y`.
That is, the expression begins at `x`, rolls over to the beginning of
the allowable values, and continues up to `y`.

The following expression represents 9:00 a.m. to 5:00 p.m.:

``` oac_no_warn
hour="9-17"
```

The following expression represents Friday through Monday:

``` oac_no_warn
dayOfWeek="5-1"
```

The following expression represents the twenty-fifth day of the month to
the end of the month, and the beginning of the month to the fifth day of
the month:

``` oac_no_warn
dayOfMonth="25-5"
```

It is equivalent to the following expression:

``` oac_no_warn
dayOfMonth="25-Last,1-5"
```

Specifying Intervals

The forward slash (`/`) constrains an attribute to a starting point and
an interval and is used to specify every `N` seconds, minutes, or hours
within the minute, hour, or day. For an expression of the form `x/y`,
`x` represents the starting point and `y` represents the interval. The
wildcard character may be used in the `x` position of an interval and is
equivalent to setting `x` to `0`.

Intervals may be set only for `second`, `minute`, and `hour` attributes.

The following expression represents every 10 minutes within the hour:

``` oac_no_warn
minute="*/10"
```

It is equivalent to:

``` oac_no_warn
minute="0,10,20,30,40,50"
```

The following expression represents every 2 hours starting at noon:

``` oac_no_warn
hour="12/2"
```

## 34.5.2 Programmatic Timers

When a programmatic timer expires (goes off), the container calls the
method annotated `@Timeout` in the bean's implementation class. The
`@Timeout` method contains the business logic that handles the timed
event.

### 34.5.2.1 The @Timeout Method

Methods annotated `@Timeout` in the enterprise bean class must return
`void` and optionally take a `javax.ejb.Timer` object as the only
parameter. They may not throw application exceptions:

``` oac_no_warn
@Timeout
public void timeout(Timer timer) {
    System.out.println("TimerBean: timeout occurred");
}
```

### 34.5.2.2 Creating Programmatic Timers

To create a timer, the bean invokes one of the `create` methods of the
`TimerService` interface. These methods allow single-action, interval,
or calendar-based timers to be created.

For single-action or interval timers, the expiration of the timer can be
expressed as either a duration or an absolute time. The duration is
expressed as a the number of milliseconds before a timeout event is
triggered. To specify an absolute time, create a `java.util.Date` object
and pass it to the `TimerService.createSingleActionTimer` or the
`TimerService.createTimer` method.

The following code sets a programmatic timer that will expire in 1
minute (60,000 milliseconds):

``` oac_no_warn
long duration = 60000;
Timer timer =
    timerService.createSingleActionTimer(duration, new TimerConfig());
```

The following code sets a programmatic timer that will expire at 12:05
p.m. on May 1, 2015, specified as a `java.util.Date`:

``` oac_no_warn
SimpleDateFormatter formatter = 
    new SimpleDateFormatter("MM/dd/yyyy 'at' HH:mm");
Date date = formatter.parse("05/01/2015 at 12:05");
Timer timer = timerService.createSingleActionTimer(date, new TimerConfig());
```

For calendar-based timers, the expiration of the timer is expressed as a
`javax.ejb.ScheduleExpression` object, passed as a parameter to the
`TimerService.createCalendarTimer` method. The `ScheduleExpression`
class represents calendar-based timer expressions and has methods that
correspond to the attributes described in [Creating Calendar-Based Timer
Expressions](#GIQLK).

The following code creates a programmatic timer using the
`ScheduleExpression` helper class:

``` oac_no_warn
ScheduleExpression schedule = new ScheduleExpression();
schedule.dayOfWeek("Mon");
schedule.hour("12-17, 23");
Timer timer = timerService.createCalendarTimer(schedule);
```

For details on the method signatures, see the `TimerService` API
documentation at
`http://docs.oracle.com/javaee/7/api/javax/ejb/TimerService.html`.

The bean described in [The timersession Example](#BNBPE) creates a timer
as follows:

``` oac_no_warn
Timer timer = timerService.createTimer(intervalDuration,
        "Created new programmatic timer");
```

In the `timersession` example, the method that calls `createTimer` is
invoked in a business method, which is called by a client.

Timers are persistent by default. If the server is shut down or crashes,
persistent timers are saved and will become active again when the server
is restarted. If a persistent timer expires while the server is down,
the container will call the `@Timeout` method when the server is
restarted.

Nonpersistent programmatic timers are created by calling
`TimerConfig.setPersistent(false)` and passing the `TimerConfig` object
to one of the timer-creation methods.

The `Date` and `long` parameters of the `createTimer` methods represent
time with the resolution of milliseconds. However, because the timer
service is not intended for real-time applications, a callback to the
`@Timeout` method might not occur with millisecond precision. The timer
service is for business applications, which typically measure time in
hours, days, or longer durations.

## 34.5.3 Automatic Timers

Automatic timers are created by the EJB container when an enterprise
bean that contains methods annotated with the `@Schedule` or
`@Schedules` annotations is deployed. An enterprise bean can have
multiple automatic timeout methods, unlike a programmatic timer, which
allows only one method annotated with the `@Timeout` annotation in the
enterprise bean class.

Automatic timers can be configured through annotations or through the
`ejb-jar.xml` deployment descriptor.

Adding a `@Schedule` annotation on an enterprise bean marks that method
as a timeout method according to the calendar schedule specified in the
attributes of `@Schedule`.

The `@Schedule` annotation has elements that correspond to the calendar
expressions detailed in [Creating Calendar-Based Timer
Expressions](#GIQLK) and the `persistent`, `info`, and `timezone`
elements.

The optional `persistent` element takes a Boolean value and is used to
specify whether the automatic timer should survive a server restart or
crash. By default, all automatic timers are persistent.

The optional `timezone` element is used to specify that the automatic
timer is associated with a particular time zone. If set, this element
will evaluate all timer expressions in relation to the specified time
zone, regardless of the time zone in which the EJB container is running.
By default, all automatic timers set are in relation to the default time
zone of the server.

The optional `info` element is used to set an informational description
of the timer. A timer's information can be retrieved later by using
`Timer.getInfo`.

The following timeout method uses `@Schedule` to set a timer that will
expire every Sunday at midnight:

``` oac_no_warn
@Schedule(dayOfWeek="Sun", hour="0")
public void cleanupWeekData() { ... }
```

The `@Schedules` annotation is used to specify multiple calendar-based
timer expressions for a given timeout method.

The following timeout method uses the `@Schedules` annotation to set
multiple calendar-based timer expressions. The first expression sets a
timer to expire on the last day of every month. The second expression
sets a timer to expire every Friday at 11:00 p.m.:

``` oac_no_warn
@Schedules ({
    @Schedule(dayOfMonth="Last"),
    @Schedule(dayOfWeek="Fri", hour="23")
})
public void doPeriodicCleanup() { ... }
```

## 34.5.4 Canceling and Saving Timers

Timers can be cancelled by the following events.

  - When a single-event timer expires, the EJB container calls the
    associated timeout method and then cancels the timer.

  - When the bean invokes the `cancel` method of the `Timer` interface,
    the container cancels the timer.

If a method is invoked on a cancelled timer, the container throws the
`javax.ejb.NoSuchObjectLocalException`.

To save a `Timer` object for future reference, invoke its `getHandle`
method and store the `TimerHandle` object in a database. (A
`TimerHandle` object is serializable.) To reinstantiate the `Timer`
object, retrieve the handle from the database and invoke `getTimer` on
the handle. A `TimerHandle` object cannot be passed as an argument of a
method defined in a remote or web service interface. In other words,
remote clients and web service clients cannot access a bean's
`TimerHandle` object. Local clients, however, do not have this
restriction.

## 34.5.5 Getting Timer Information

In addition to defining the `cancel` and `getHandle` methods, the
`Timer` interface defines methods for obtaining information about
timers:

``` oac_no_warn
public long getTimeRemaining();
public java.util.Date getNextTimeout();
public java.io.Serializable getInfo();
```

The `getInfo` method returns the object that was the last parameter of
the `createTimer` invocation. For example, in the `createTimer` code
snippet of the preceding section, this information parameter is a
`String` object with the value `created timer`.

To retrieve all of a bean's active timers, call the `getTimers` method
of the `TimerService` interface. The `getTimers` method returns a
collection of `Timer` objects.

## 34.5.6 Transactions and Timers

An enterprise bean usually creates a timer within a transaction. If this
transaction is rolled back, the timer creation also is rolled back.
Similarly, if a bean cancels a timer within a transaction that gets
rolled back, the timer cancellation is rolled back. In this case, the
timer's duration is reset as if the cancellation had never occurred.

In beans that use container-managed transactions, the `@Timeout` method
usually has the `Required` or `RequiresNew` transaction attribute to
preserve transaction integrity. With these attributes, the EJB container
begins the new transaction before calling the `@Timeout` method. If the
transaction is rolled back, the container will call the `@Timeout`
method at least one more time.

## 34.5.7 The timersession Example

The source code for this example is in the
tut-install`/examples/ejb/timersession/src/main/java/` directory.

`TimerSessionBean` is a singleton session bean that shows how to set
both an automatic timer and a programmatic timer. In the source code
listing of `TimerSessionBean` that follows, the `setTimer` and
`@Timeout` methods are used to set a programmatic timer. A
`TimerService` instance is injected by the container when the bean is
created. Because it's a business method, `setTimer` is exposed to the
local, no-interface view of `TimerSessionBean` and can be invoked by the
client. In this example, the client invokes `setTimer` with an interval
duration of 8,000 milliseconds, or 8 seconds. The `setTimer` method
creates a new timer by invoking the `createTimer` method of
`TimerService`. Now that the timer is set, the EJB container will invoke
the `programmaticTimeout` method of `TimerSessionBean` when the timer
expires, in about 8 seconds:

``` oac_no_warn
...
    public void setTimer(long intervalDuration) {
        logger.log(Level.INFO, 
                "Setting a programmatic timeout for {0} milliseconds from now.",
                intervalDuration);
        Timer timer = timerService.createTimer(intervalDuration, 
                "Created new programmatic timer");
    }
    
    @Timeout
    public void programmaticTimeout(Timer timer) {
        this.setLastProgrammaticTimeout(new Date());
        logger.info("Programmatic timeout occurred.");
    }
...
```

`TimerSessionBean` also has an automatic timer and timeout method,
`automaticTimeout`. The automatic timer is set to expire every 1 minute
and is set by using a calendar-based timer expression in the `@Schedule`
annotation:

``` oac_no_warn
...
    @Schedule(minute = "*/1", hour = "*", persistent = false)
    public void automaticTimeout() {
        this.setLastAutomaticTimeout(new Date());
        logger.info("Automatic timeout occured");
    }
...
```

`TimerSessionBean` also has two business methods:
`getLastProgrammaticTimeout` and `getLastAutomaticTimeout`. Clients call
these methods to get the date and time of the last timeout for the
programmatic timer and automatic timer, respectively.

Here's the source code for the `TimerSessionBean` class:

``` oac_no_warn
package javaeetutorial.timersession.ejb;

import java.util.Date;
import java.util.logging.Level;
import java.util.logging.Logger;
import javax.annotation.Resource;
import javax.ejb.Schedule;
import javax.ejb.Singleton;
import javax.ejb.Startup;
import javax.ejb.Timeout;
import javax.ejb.Timer;
import javax.ejb.TimerService;

@Singleton
@Startup
public class TimerSessionBean {
    @Resource
    TimerService timerService;

    private Date lastProgrammaticTimeout;
    private Date lastAutomaticTimeout;
    
    private static final Logger logger = 
            Logger.getLogger("timersession.ejb.TimerSessionBean");
    
    public void setTimer(long intervalDuration) {
        logger.log(Level.INFO,
                "Setting a programmatic timeout for {0} milliseconds from now.",
                intervalDuration);
        Timer timer = timerService.createTimer(intervalDuration, 
                "Created new programmatic timer");
    }
    
    @Timeout
    public void programmaticTimeout(Timer timer) {
        this.setLastProgrammaticTimeout(new Date());
        logger.info("Programmatic timeout occurred.");
    }

    @Schedule(minute = "*/1", hour = "*", persistent = false)
    public void automaticTimeout() {
        this.setLastAutomaticTimeout(new Date());
        logger.info("Automatic timeout occured");
    }

    public String getLastProgrammaticTimeout() {
        if (lastProgrammaticTimeout != null) {
            return lastProgrammaticTimeout.toString();
        } else {
            return "never";
        }
    }

    public void setLastProgrammaticTimeout(Date lastTimeout) {
        this.lastProgrammaticTimeout = lastTimeout;
    }

    public String getLastAutomaticTimeout() {
        if (lastAutomaticTimeout != null) {
            return lastAutomaticTimeout.toString();
        } else {
            return "never";
        }
    }

    public void setLastAutomaticTimeout(Date lastAutomaticTimeout) {
        this.lastAutomaticTimeout = lastAutomaticTimeout;
    }
}
```

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
GlassFish Server has a default minimum timeout value of 1,000 milliseconds, or 1 second. If you need to set the timeout value lower than 1,000 milliseconds, change the value of the Minimum Delivery Interval setting in the Administration Console. To modify the minimum timeout value, in the Administration Console expand <span class="gui-object-action">Configurations</span>, then expand <span class="gui-object-action">server-config</span>, select <span class="gui-object-action">EJB Container</span>, and click the <span class="gui-object-action">EJB Timer Service</span> tab. Enter a new timeout value under <span class="gui-object-action">Minimum Delivery Interval</span> and click <span class="gui-object-action">Save</span>. The lowest practical value for <code dir="ltr">minimum-delivery-interval-in-millis</code> is around 10 milliseconds, owing to virtual machine constraints.</td>
</tr>
</tbody>
</table>

  

## 34.5.8 Running the timersession Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `timersession` example.

The following topics are addressed here:

  - [Section 34.5.8.1, "To Run the timersession Example Using NetBeans
    IDE"](#GIQNI)

  - [Section 34.5.8.2, "To Build, Package, and Deploy the timersession
    Example Using Maven"](#GIQNQ)

  - [Section 34.5.8.3, "To Run the Web Client"](#GIQOP)

### 34.5.8.1 To Run the timersession Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/ejb
    ```

4.  Select the `timersession` folder.

5.  Click Open Project.

6.  From the Run menu, choose Run Project.
    
    This builds and packages the application into a WAR file located at
    tut-install`/examples/ejb/timersession/target/timersession.war`,
    deploys this WAR file to your GlassFish Server instance, and then
    runs the web
client.

### 34.5.8.2 To Build, Package, and Deploy the timersession Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/ejb/timersession/
    ```

3.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This builds and packages the application into a WAR file located at
    tut-install`/examples/ejb/timersession/target/timersession.war` and
    deploys this WAR file to your GlassFish Server instance.

### 34.5.8.3 To Run the Web Client

1.  Open a web browser to the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/timersession
    ```

2.  Click Set Timer to set a programmatic timer.

3.  Wait for a while and click the browser's Refresh button.
    
    You will see the date and time of the last programmatic and
    automatic timeouts.
    
    To see the messages that are logged when a timeout occurs, open the
    `server.log` file located in domain-dir`/logs/`.

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
<td><a href="ejb-basicexamples004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="ejb-basicexamples006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
