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
<td><a href="batch-processing001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="batch-processing003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 55.2 Batch Processing in Java EE

This section lists the components of the batch processing framework in
Java EE and provides an overview of the steps you have to follow to
create a batch application.

The following topics are addressed here:

  - [Section 55.2.1, "The Batch Processing Framework"](#BABEAFJI)

  - [Section 55.2.2, "Creating Batch Applications"](#BABCGDHJ)

  - [Section 55.2.3, "Elements of a Batch Job"](#BABDGDJB)

  - [Section 55.2.4, "Properties and Parameters"](#BABHJEJC)

  - [Section 55.2.5, "Job Instances and Job Executions"](#BABHJGDH)

  - [Section 55.2.6, "Batch and Exit Status"](#BABBFGEF)

## 55.2.1 The Batch Processing Framework

Java EE includes a batch processing framework that consists of the
following elements:

  - A batch runtime that manages the execution of jobs

  - A job specification language based on XML

  - A Java API to interact with the batch runtime

  - A Java API to implement steps, decision elements, and other batch
    artifacts

Batch applications in Java EE contain XML files and Java classes. The
XML files define the structure of a job in terms of batch artifacts and
the relationships between them. (A batch artifact is a part of a
chunk-oriented step, a task-oriented step, a decision element, or
another component of a batch application). The Java classes implement
the application logic of the batch artifacts defined in the XML files.
The batch runtime parses the XML files and loads the batch artifacts as
Java classes to run the jobs in a batch application.

## 55.2.2 Creating Batch Applications

The process for creating a batch application in Java EE is the
following.

1.  Design the batch application.
    
    1.  Identify the input sources, the format of the input data, the
        desired final result, and the required processing phases.
    
    2.  Organize the application as a job with chunk-oriented steps,
        task-oriented steps, and decision elements. Determine the
        dependencies between them.
    
    3.  Determine the order of execution in terms of transitions between
        steps.
    
    4.  Identify steps that can run in parallel and steps that can run
        in more than one thread.

2.  Create the batch artifacts as Java classes by implementing the
    interfaces specified by the framework for steps, decision elements,
    and so on. These Java classes contain the code to read data from
    input sources, format items, process items, and store results. Batch
    artifacts can access context objects from the batch runtime using
    dependency injection.

3.  Define jobs, steps, and their execution flow in XML files using the
    Job Specification Language. The elements in the XML files reference
    batch artifacts implemented as Java classes. The batch artifacts can
    access properties declared in the XML files, such as names of files
    and databases.

4.  Use the Java API provided by the batch runtime to launch the batch
    application.

The following sections describe in detail how to use the components of
the batch processing framework in Java EE to create batch applications.

## 55.2.3 Elements of a Batch Job

A batch job can contain one or more of the following elements:

  - Steps

  - Flows

  - Splits

  - Decision elements

Steps are described in [Introduction to Batch
Processing](batch-processing001.htm#BCGJDEEH), and can be chunk-oriented
or task-oriented. Chunk-oriented steps can be partitioned steps. In a
partitioned chunk step, the processing of one item does not depend on
other items, so these steps can run in more than one thread.

A flow is a sequence of steps that execute as a unit. A sequence of
related steps can be grouped together into a flow. The steps in a flow
cannot transition to steps outside the flow. The flow transitions to the
next element when its last step completes.

A split is a set of flows that execute in parallel; each flow runs on a
separate thread. The split transitions to the next element when all its
flows complete.

Decision elements use the exit status of the previous step to determine
the next step or to terminate the batch job.

## 55.2.4 Properties and Parameters

Jobs and steps can have a number of properties associated with them. You
define properties in the job definition file, and batch artifacts access
these properties using context objects from the batch runtime. Using
properties in this manner enables you to decouple static parameters of
the job from the business logic and to reuse batch artifacts in
different job definition files.

Specifying properties is described in [Using the Job Specification
Language](batch-processing004.htm#BCGDDBBG), and accessing properties in
batch artifacts is described in [Creating Batch
Artifacts](batch-processing005.htm#BCGHDHGH).

Java EE applications can also pass parameters to a job when they submit
it to the batch runtime. This enables you to specify dynamic parameters
that are only known at runtime. Parameters are also necessary for
partitioned steps, since each partition needs to know, for example, what
range of items to process.

Specifying parameters when submitting jobs is described in [Submitting
Jobs to the Batch Runtime](batch-processing006.htm#BCGCAHCB). Specifying
parameters for partitioned steps and accessing them in batch artifacts
is demonstrated in [The phonebilling Example
Application](batch-processing009.htm#BCGFCACD).

## 55.2.5 Job Instances and Job Executions

A job definition can have multiple instances, each with different
parameters. A job execution is an attempt to run a job instance. The
batch runtime maintains information about job instances and job
executions, as described in [Checking the Status of a
Job](batch-processing006.htm#BCGIBGFC).

## 55.2.6 Batch and Exit Status

The state of jobs, steps, splits, and flows is represented in the batch
runtime as a batch status value. Batch status values are listed [Table
55-1](#BCGJBGDF). They are represented as strings.

Table 55-1 Batch Status Values

<table style="width:28%;">
<colgroup>
<col width="28%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">STARTING</code></p></td>
<td><p>The job has been submitted to the batch runtime.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">STARTED</code></p></td>
<td><p>The job is running.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">STOPPING</code></p></td>
<td><p>The job has been requested to stop.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">STOPPED</code></p></td>
<td><p>The job has stopped.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">FAILED</code></p></td>
<td><p>The job finished executing because of an error.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">COMPLETED</code></p></td>
<td><p>The job finished executing successfully.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">ABANDONED</code></p></td>
<td><p>The job was marked abandoned.</p></td>
</tr>
</tbody>
</table>

  

Java EE applications can submit jobs and access the batch status of a
job using the `JobOperator` interface, as described in [Submitting Jobs
to the Batch Runtime](batch-processing006.htm#BCGCAHCB). Job definition
files can refer to batch status values using the Job Specification
Language (JSL), as described in [Using the Job Specification
Language](batch-processing004.htm#BCGDDBBG). Batch artifacts can access
batch status values using context objects, as described in [Using the
Context Objects from the Batch
Runtime](batch-processing005.htm#BCGCJEEF).

For flows, the batch status is that of its last step. For splits, the
batch status is the following:

  - `COMPLETED`: If all its flows have a batch status of `COMPLETED`

  - `FAILED`: If any flow has a batch status of `FAILED`

  - `STOPPED`: If any flow has a batch status of `STOPPED`, and no flows
    have a batch status of `FAILED`

The batch status for jobs, steps, splits, and flows is set by the batch
runtime. Jobs, steps, splits, and flows also have an exit status, which
is a user-defined value based on the batch status. You can set the exit
status inside batch artifacts or in the job definition file. You can
access the exit status in the same manner as the batch status, described
above. The default value for the exit status is the same as the batch
status.

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
<td><a href="batch-processing001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="batch-processing003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
