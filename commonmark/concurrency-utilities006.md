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
<td><a href="concurrency-utilities005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="concurrency-utilities007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 56.6 The taskcreator Concurrency Example

The `taskcreator` example demonstrates how to use Concurrency Utilities
for Java EE to run tasks immediately, periodically, or after a fixed
delay. This example provides a JavaServer Faces interface that enables
users to submit tasks to be executed and displays information messages
for each task. The example uses the Managed Executor Service to run
tasks immediately and the Managed Scheduled Executor Service to run
tasks periodically or after a fixed delay. (See [Main Components of the
Concurrency Utilities](concurrency-utilities002.htm#CIHFBCFH) for
information about these services.)

The `taskcreator` example consists of the following components.

  - A JavaServer Faces page (`index.xhtml`) that contains three
    elements: a form to submit tasks, a task execution log, and a form
    to cancel periodic tasks. This page submits Ajax requests to create
    and cancel tasks. This page also receives WebSocket messages, using
    JavaScript code to update the task execution log.

  - A CDI managed bean (`TaskCreatorBean`) that processes the requests
    from the JavaServer Faces page. This bean invokes the methods in
    `TaskEJB` to submit new tasks and to cancel periodic tasks.

  - An enterprise bean (`TaskEJB`) that obtains executor service
    instances using resource injection and submits tasks for execution.
    This bean is also a JAX-RS web service endpoint. The tasks send
    information messages to this endpoint.

  - A WebSocket endpoint (`InfoEndpoint`) that the enterprise bean uses
    to send information messages to the clients.

  - A task class (`Task`) that implements the `Runnable` interface. The
    `run` method in this class sends information messages to the web
    service endpoint in `TaskEJB` and sleeps for 1.5 seconds.

[Figure 56-1](#CIHHACFF) shows the architecture of the `taskcreator`
example.

Figure 56-1 Architecture of the taskcreator Example

![Description of Figure 56-1 follows](img/jeett_dt_060.png)  
[Description of "Figure 56-1 Architecture of the taskcreator
Example"](img_text/jeett_dt_060.htm)  
  

The `TaskEJB` class obtains the default executor service objects from
the application server as follows:

``` oac_no_warn
@Resource(name="java:comp/DefaultManagedExecutorService")
ManagedExecutorService mExecService;

@Resource(name="java:comp/DefaultManagedScheduledExecutorService")
ManagedScheduledExecutorService sExecService;
```

The `submitTask` method in `TaskEJB` uses these objects to submit tasks
for execution as follows:

``` oac_no_warn
public void submitTask(Task task, String type) {
    /* Use the managed executor objects from the app server */
    switch (type) {
        case "IMMEDIATE":
            mExecService.submit(task);
            break;
        case "DELAYED":
            sExecService.schedule(task, 3, TimeUnit.SECONDS);
            break;
        case "PERIODIC":
            ScheduledFuture<?> fut;
            fut = sExecService.scheduleAtFixedRate(task, 0, 8, 
                    TimeUnit.SECONDS);
            periodicTasks.put(task.getName(), fut);
            break;
    }
}
```

For periodic tasks, `TaskEJB` keeps a reference to the `ScheduledFuture`
object, so that the user can cancel the task at any time.

## 56.6.1 Running the taskcreator Example

This section describes how to build, package, deploy, and run the
`taskcreator` example using NetBeans IDE or Maven.

The following topics are addressed here:

  - [Section 56.6.1.1, "To Build, Package, and Deploy the taskcreator
    Example Using NetBeans IDE"](#CHDCCJHB)

  - [Section 56.6.1.2, "To Build, Package, and Deploy the taskcreator
    Example Using Maven"](#CHDHJBDD)

  - [Section 56.6.1.3, "To Run the taskcreator
Example"](#CHDBJGID)

### 56.6.1.1 To Build, Package, and Deploy the taskcreator Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/concurrency
    ```

4.  Select the `taskcreator` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `taskcreator` project and
    select Build.
    
    This command builds and deploys the
application.

### 56.6.1.2 To Build, Package, and Deploy the taskcreator Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/concurrency/taskcreator
    ```

3.  Enter the following command to build and deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```

### 56.6.1.3 To Run the taskcreator Example

1.  Open the following URL in a web browser:
    
    ``` oac_no_warn
    http://localhost:8080/taskcreator/
    ```
    
    The page contains a form to submit tasks, a task execution log, and
    a form to cancel periodic tasks.

2.  Select the Immediate task type, enter a task name, and click the
    Submit button. Messages like the following appear in the task
    execution log:
    
    ``` oac_no_warn
    12:40:47 - IMMEDIATE Task TaskA finished
    12:40:45 - IMMEDIATE Task TaskA started
    ```

3.  Select the Delayed (3 sec) task type, enter a task name, and click
    the Submit button. Messages like the following appear in the task
    execution log:
    
    ``` oac_no_warn
    12:43:26 - DELAYED Task TaskB finished
    12:43:25 - DELAYED Task TaskB started
    12:43:22 - DELAYED Task TaskB submitted
    ```

4.  Select the Periodic (8 sec) task type, enter a task name, and click
    the Submit button. Messages like the following appear in the task
    execution log:
    
    ``` oac_no_warn
    12:45:25 - PERIODIC Task TaskC finished run #2
    12:45:23 - PERIODIC Task TaskC started run #2
    12:45:17 - PERIODIC Task TaskC finished run #1
    12:45:15 - PERIODIC Task TaskC started run #1
    ```
    
    You can add more than one periodic task. To cancel a periodic task,
    select it from the form and click Cancel Task.

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
<td><a href="concurrency-utilities005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="concurrency-utilities007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
