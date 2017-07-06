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
<td><a href="concurrency-utilities004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="concurrency-utilities006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 56.5 The jobs Concurrency Example

This section describes a very basic example that shows how to use some
of the basic concurrency features in an enterprise application.
Specifically, this example uses one of the main components of
Concurrency Utilities for Java EE, a Managed Executor Service.

The example demonstrates a scenario where a RESTful web service, exposed
as a public API, is used to submit generic jobs for execution. These
jobs are processed in the background. Each job prints a "Starting" and a
"Finished" message at the beginning and end of the execution. Also, to
simulate background processing, each job takes 10 seconds to execute.

The RESTful service exposes two methods:

  - `/token`: Exposed as a GET method that registers and returns valid
    API tokens

  - `/process`: Exposed as a POST method that receives a `jobID` query
    parameter, which is the identifier for the job to be executed, and a
    custom HTTP header named `X-REST-API-Key,` which will be used
    internally to validate requests with tokens

The token is used to differentiate the Quality of Service (QoS) offered
by the API. Users that provide a token in a service request can process
multiple concurrent jobs. However, users that do not provide a token can
process only one job at a time. Since every job takes 10 seconds to
execute, users that provide no token will be able to execute only one
call to the service every 10 seconds. For users that provide a token,
processing will be much faster.

This differentiation is made possible by the use of two different
Managed Executor Services, one for each type of request.

## 56.5.1 Running the jobs Example

After configuring GlassFish Server by adding two Managed Executor
Services, you can use either NetBeans IDE or Maven to build, package,
deploy, and run the `jobs` example.

The following topics are addressed here:

  - [Section 56.5.1.1, "To Configure GlassFish Server for the Basic
    Concurrency Example"](#CHDCIBBD)

  - [Section 56.5.1.2, "To Build, Package, and Deploy the jobs Example
    Using NetBeans IDE"](#CHDFBAHJ)

  - [Section 56.5.1.3, "To Build, Package, and Deploy the jobs Example
    Using Maven"](#CHDECFFF)

  - [Section 56.5.1.4, "To Run the jobs Example and Submit Jobs with Low
    Priority"](#CHDFHHAF)

  - [Section 56.5.1.5, "To Run the jobs Example and Submit Jobs with
    High
Priority"](#CHDHEABJ)

### 56.5.1.1 To Configure GlassFish Server for the Basic Concurrency Example

To configure GlassFish Server, follow these steps.

1.  Open the Administration Console at `http://localhost:4848`.

2.  Expand the Resources node.

3.  Expand the Concurrent Resources node.

4.  Click Managed Executor Services.

5.  On the Managed Executor Services page, click New to open the New
    Managed Executor Services page.

6.  In the JNDI Name field, enter `MES_High` to create the high-priority
    Managed Executor Service. Use the following settings (keep the
    default values for other settings):
    
      - Thread Priority: 10
    
      - Core Size: 2
    
      - Maximum Pool Size: 5
    
      - Task Queue Capacity: 2

7.  Click OK.

8.  On the On the Managed Executor Services page, click New again.

9.  In the JNDI Name field, enter `MES_Low` to create the low-priority
    Managed Executor Service. Use the following settings (keep the
    default values for other settings):
    
      - Thread Priority: 1
    
      - Core Size: 1
    
      - Maximum Pool Size: 1
    
      - Task Queue Capacity: 0

10. Click
OK.

### 56.5.1.2 To Build, Package, and Deploy the jobs Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/concurrency
    ```

4.  Select the `jobs` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `jobs` project and select
    Build.
    
    This command builds and deploys the application.

### 56.5.1.3 To Build, Package, and Deploy the jobs Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/concurrency/jobs
    ```

3.  Enter the following command to build and deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```

### 56.5.1.4 To Run the jobs Example and Submit Jobs with Low Priority

To run the example as a user who submits jobs with low priority, follow
these steps:

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/jobs
    ```

2.  In the Jobs Client page, enter the value 1 in the Enter a JobID
    field, enter nothing in the Enter a Token field, then click Submit
    Job.
    
    The following message should be displayed at the bottom of the page:
    
    ``` oac_no_warn
    Job 1 successfully submitted
    ```
    
    The server log includes the following messages:
    
    ``` oac_no_warn
    INFO:   Invalid or missing token! 
    INFO:   Task started LOW-1
    INFO:   Job 1 successfully submitted
    INFO:   Task finished LOW-1
    ```
    
    You submitted a job with low priority. This means that you cannot
    submit another job for 10 seconds. If you try to do so, the RESTful
    API will return a service unavailable (HTTP 503) response and the
    following message will be displayed at the bottom of the page:
    
    ``` oac_no_warn
    Job 2 was NOT submitted
    ```
    
    The server log will include the following messages:
    
    ``` oac_no_warn
    INFO:   Invalid or missing token! 
    INFO:   Job 1 successfully submitted
    INFO:   Task started LOW-1
    INFO:   Invalid or missing token! 
    INFO:   Job 2 was NOT submitted
    INFO:   Task finished LOW-1
    ```

### 56.5.1.5 To Run the jobs Example and Submit Jobs with High Priority

To run the example as a user who submits jobs with high priority, follow
these steps:

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/jobs
    ```

2.  In the Jobs Client page, enter a value of one to ten digits in the
    Enter a JobID field.

3.  Click the here link on the line "Get a token here" to get a token.
    The page that displays the token will open in a new tab.

4.  Copy the token and return to the Jobs Client page.

5.  Paste the token in the Enter a Token field, then click Submit Job.
    
    A message like the following should be displayed at the bottom of
    the page:
    
    ``` oac_no_warn
    Job 11 successfully submitted
    ```
    
    The server log includes the following messages:
    
    ``` oac_no_warn
    INFO:   Token accepted. Execution with high priority.
    INFO:   Task started HIGH-11
    INFO:   Job 11 successfully submitted
    INFO:   Task finished HIGH-11
    ```
    
    You submitted a job with high priority. This means that you can
    submit multiple jobs, each with a token, and not face the 10 second
    per job restriction that the low priority submitters face. If you
    submit 3 jobs with tokens in rapid succession, messages like the
    following will be displayed at the bottom of the page:
    
    ``` oac_no_warn
    Job 1 was submitted
    Job 2 was submitted
    Job 3 was submitted
    ```
    
    The server log will include the following messages:
    
    ``` oac_no_warn
    INFO:   Token accepted. Execution with high priority.
    INFO:   Task started HIGH-1
    INFO:   Job 1 successfully submitted
    INFO:   Token accepted. Execution with high priority.
    INFO:   Task started HIGH-2
    INFO:   Job 2 successfully submitted
    INFO:   Task finished HIGH-1
    INFO:   Token accepted. Execution with high priority.
    INFO:   Task started HIGH-3
    INFO:   Job 3 successfully submitted
    INFO:   Task finished HIGH-2
    INFO:   Task finished HIGH-3
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
<td><a href="concurrency-utilities004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="concurrency-utilities006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
