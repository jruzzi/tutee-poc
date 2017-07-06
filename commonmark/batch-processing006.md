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
<td><a href="batch-processing005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="batch-processing007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 55.6 Submitting Jobs to the Batch Runtime

The `JobOperator` interface in the `javax.batch.operations` package
enables you to submit jobs to the batch runtime and obtain information
about existing jobs. This interface provides the following
functionality.

  - Obtain the names of all known jobs.

  - Start, stop, restart, and abandon jobs.

  - Obtain job instances and job executions.

The `BatchRuntime` class in the `javax.batch.runtime` package provides
the `getJobOperator` factory method to obtain `JobOperator` objects.

## 55.6.1 Starting a Job

The following example code demonstrates how to obtain a `JobOperator`
object and submit a batch job:

``` oac_no_warn
JobOperator jobOperator = BatchRuntime.getJobOperator();
Properties props = new Properties();
props.setProperty("parameter1", "value1");
...
long execID = jobOperator.start("simplejob", props);
```

The first argument of the `JobOperator.start` method is the name of the
job as specified in its job definition file. The second parameter is a
`Properties` object that represents the parameters for this job
execution. You can use job parameters to pass to a job information that
is only known at runtime.

## 55.6.2 Checking the Status of a Job

The `JobExecution` interface in the `javax.batch.runtime` package
provides methods to obtain information about submitted jobs. This
interface provides the following functionality.

  - Obtain the batch and exit status of a job execution.

  - Obtain the time the execution was started, updated, or ended.

  - Obtain the job name.

  - Obtain the execution ID.

The following example code demonstrates how to obtain the batch status
of a job using its execution ID:

``` oac_no_warn
JobExecution jobExec = jobOperator.getJobExecution(execID);
String status = jobExec.getBatchStatus().toString();
```

## 55.6.3 Invoking the Batch Runtime in Your Application

The component from which you invoke the batch runtime depends on the
architecture of your particular application. For example, you can invoke
the batch runtime from an enterprise bean, a servlet, a managed bean,
and so on.

See [The webserverlog Example
Application](batch-processing008.htm#BCGJHEHJ) and [The phonebilling
Example Application](batch-processing009.htm#BCGFCACD) for details on
how to invoke the batch runtime from a managed bean driven by a
JavaServer Faces user interface.

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
<td><a href="batch-processing005.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="batch-processing007.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
