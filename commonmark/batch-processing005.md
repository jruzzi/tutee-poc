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
<td><a href="batch-processing004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="batch-processing006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 55.5 Creating Batch Artifacts

After you define a job in terms of its batch artifacts using the Job
Specification Language (JSL), you create these artifacts as Java classes
that implement the interfaces in the `javax.batch.api` package and its
subpackages.

This section lists the main batch artifact interfaces, demonstrates how
to access context objects from the batch runtime, and provides some
examples.

The following topics are addressed here:

  - [Section 55.5.1, "Batch Artifact Interfaces"](#BABDAIBI)

  - [Section 55.5.2, "Dependency Injection in Batch
    Artifacts"](#BCGIFJBB)

  - [Section 55.5.3, "Using the Context Objects from the Batch
    Runtime"](#BCGCJEEF)

## 55.5.1 Batch Artifact Interfaces

The following tables list the interfaces that you implement to create
batch artifacts. The interface implementations are referenced from the
elements described in [Using the Job Specification
Language](batch-processing004.htm#BCGDDBBG).

[Table 55-3](#BCGGCIDC) lists the interfaces to implement batch
artifacts for chunk steps, task steps, and decision elements.

[Table 55-4](#BCGEAAEA) lists the interfaces to implement batch
artifacts for partitioned steps.

[Table 55-5](#BCGCAEDI) lists the interfaces to implement batch
artifacts for job and step listeners.

Table 55-3 Main Batch Artifact Interfaces

<table style="width:56%;">
<colgroup>
<col width="28%" />
<col width="27%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Package</th>
<th>Interface</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api</code></p></td>
<td><p><code dir="ltr">Batchlet</code></p></td>
<td><p>Implements the business logic of a task-oriented step. It is referenced from the <code dir="ltr">batchlet</code> element.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api</code></p></td>
<td><p><code dir="ltr">Decider</code></p></td>
<td><p>Decides the next step, flow, or split to execute based on information from the execution of the previous step, flow, or split. It is referenced from the <code dir="ltr">decision</code> element.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.chunk</code></p></td>
<td><p><code dir="ltr">CheckPointAlgorithm</code></p></td>
<td><p>Implements a custom checkpoint policy for chunk steps. It is referenced from the <code dir="ltr">checkpoint-algorithm</code> element inside the <code dir="ltr">chunk</code> element.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api.chunk</code></p></td>
<td><p><code dir="ltr">ItemReader</code></p></td>
<td><p>Reads items from an input source in a chunk step. It is referenced from the <code dir="ltr">reader</code> element inside the <code dir="ltr">chunk</code> element.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.chunk</code></p></td>
<td><p><code dir="ltr">ItemProcessor</code></p></td>
<td><p>Processes input items to obtain output items in chunk steps. It is referenced from the <code dir="ltr">processor</code> element inside the <code dir="ltr">chunk</code> element.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api.chunk</code></p></td>
<td><p><code dir="ltr">ItemWriter</code></p></td>
<td><p>Writes output items in chunk steps. It is referenced from the <code dir="ltr">writer</code> element inside the <code dir="ltr">chunk</code> element.</p></td>
</tr>
</tbody>
</table>

  

Table 55-4 Partition Batch Artifact Interfaces

<table style="width:58%;">
<colgroup>
<col width="33%" />
<col width="25%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Package</th>
<th>Interface</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.partition</code></p></td>
<td><p><code dir="ltr">PartitionPlan</code></p></td>
<td><p>Provides details on how to execute a partitioned step, such as the number of partitions, the number of threads, and the parameters for each partition. This artifact is not referenced directly from the job definition file.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api.partition</code></p></td>
<td><p><code dir="ltr">PartitionMapper</code></p></td>
<td><p>Provides a <code dir="ltr">PartitionPlan</code> object. It is referenced from the <code dir="ltr">mapper</code> element inside the <code dir="ltr">partition</code> element.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.partition</code></p></td>
<td><p><code dir="ltr">PartitionReducer</code></p></td>
<td><p>Receives control when a partitioned step begins, ends, or rolls back. It is referenced from the <code dir="ltr">reducer</code> element inside the <code dir="ltr">partition</code> element.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api.partition</code></p></td>
<td><p><code dir="ltr">PartitionCollector</code></p></td>
<td><p>Sends intermediary results from each partition to a partition analyzer. It is referenced from the <code dir="ltr">collector</code> element inside the <code dir="ltr">partition</code> element.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.partition</code></p></td>
<td><p><code dir="ltr">PartitionAnalyzer</code></p></td>
<td><p>Processes data and final results from each partition. It is referenced from the <code dir="ltr">analyzer</code> element inside the <code dir="ltr">partition</code> element.</p></td>
</tr>
</tbody>
</table>

  

Table 55-5 Listener Batch Artifact Interfaces

<table style="width:61%;">
<colgroup>
<col width="0%" />
<col width="27%" />
<col width="34%" />
</colgroup>
<thead>
<tr class="header">
<th>Package</th>
<th>Interface</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.listener</code></p></td>
<td><p><code dir="ltr">JobListener</code></p></td>
<td><p>Intercepts job execution before and after running a job. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">job</code> element.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api.listener</code></p></td>
<td><p><code dir="ltr">StepListener</code></p></td>
<td><p>Intercepts step execution before and after running a step. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.chunk.listener</code></p></td>
<td><p><code dir="ltr">ChunkListener</code></p></td>
<td><p>Intercepts chunk processing in chunk steps before and after processing each chunk, and on errors. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api.chunk.listener</code></p></td>
<td><p><code dir="ltr">ItemReadListener</code></p></td>
<td><p>Intercepts item reading in chunk steps before and after reading each item, and on errors. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.chunk.listener</code></p></td>
<td><p><code dir="ltr">ItemProcessListener</code></p></td>
<td><p>Intercepts item processing in chunk steps before and after processing each item, and on errors. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api.chunk.listener</code></p></td>
<td><p><code dir="ltr">ItemWriteListener</code></p></td>
<td><p>Intercepts item writing in chunk steps before and after writing each item, and on errors. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.chunk.listener</code></p></td>
<td><p><code dir="ltr">RetryReadListener</code></p></td>
<td><p>Intercepts retry item reading in chunk steps when an exception occurs. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api.chunk.listener</code></p></td>
<td><p><code dir="ltr">RetryProcessListener</code></p></td>
<td><p>Intercepts retry item processing in chunk steps when an exception occurs. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.chunk.listener</code></p></td>
<td><p><code dir="ltr">RetryWriteListener</code></p></td>
<td><p>Intercepts retry item writing in chunk steps when an exception occurs. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api.chunk.listener</code></p></td>
<td><p><code dir="ltr">SkipReadListener</code></p></td>
<td><p>Intercepts skippable exception handling for item readers in chunk steps. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">javax.batch.api.chunk.listener</code></p></td>
<td><p><code dir="ltr">SkipProcessListener</code></p></td>
<td><p>Intercepts skippable exception handling for item processors in chunk steps. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">javax.batch.api.chunk.listener</code></p></td>
<td><p><code dir="ltr">SkipWriteListener</code></p></td>
<td><p>Intercepts skippable exception handling for item writers in chunk steps. It is referenced from the <code dir="ltr">listener</code> element inside the <code dir="ltr">step</code> element.</p></td>
</tr>
</tbody>
</table>

  

## 55.5.2 Dependency Injection in Batch Artifacts

To ensure that Contexts and Dependency Injection (CDI) works in your
batch artifacts, follow these steps.

1.  Define your batch artifact implementations as CDI named beans using
    the `Named` annotation.
    
    For example, define an item reader implementation in a chunk step as
    follows:
    
    ``` oac_no_warn
    @Named("MyItemReaderImpl")
    public class MyItemReaderImpl implements ItemReader {
        /* ... Override the ItemReader interface methods ... */
    }
    ```

2.  Provide a public, empty, no-argument constructor for your batch
    artifacts.
    
    For example, provide the following constructor for the artifact
    above:
    
    ``` oac_no_warn
    public MyItemReaderImpl() {}
    ```

3.  Specify the CDI name for the batch artifacts in the job definition
    file, instead of using the fully qualified name of the class.
    
    For example, define the step for the artifact above as follows:
    
    ``` oac_no_warn
    <step id="stepA" next="stepB">
      <chunk>
        <reader ref="MyItemReaderImpl"></reader>
        ...
      </chunk>
    </step>
    ```
    
    This example uses the CDI name (`MyItemReaderImpl`) instead of the
    fully qualified name of the class
    (`com.example.pkg.MyItemReaderImpl`) to specify a batch artifact.

4.  Ensure that your module is a CDI bean archive by annotating your
    batch artifacts with the `javax.enterprise.context.Dependent`
    annotation or by including an empty `beans.xml` deployment
    description with your application. For example, the following batch
    artifact is annotated with `@Dependent`:
    
    ``` oac_no_warn
    @Dependent
    @Named("MyItemReaderImpl")
    public class MyItemReaderImpl implements ItemReader { ... }
    ```
    
    For more information on bean archives, see [Packaging CDI
    Applications](cdi-adv001.htm#CACDCFDE) in [Chapter 25, "Contexts and
    Dependency Injection for Java EE: Advanced
    Topics"](cdi-adv.htm#GJEHI).

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
Contexts and Dependency Injection (CDI) is required in order to access context objects from the batch runtime in batch artifacts.</td>
</tr>
</tbody>
</table>

  

You may encounter the following errors if you do not follow this
procedure.

  - The batch runtime cannot locate some batch artifacts.

  - The batch artifacts throw null pointer exceptions when accessing
    injected objects.

## 55.5.3 Using the Context Objects from the Batch Runtime

The batch runtime provides context objects that implement the
`JobContext` and `StepContext` interfaces in the
`javax.batch.runtime.context` package. These objects are associated with
the current job and step, respectively, and enable you to do the
following:

  - Get information from the current job or step, such as its name,
    instance ID, execution ID, batch status, and exit status

  - Set the user-defined exit status

  - Store user data

  - Get property values from the job or step definition

You can inject context objects from the batch runtime inside batch
artifact implementations like item readers, item processors, item
writers, batchlets, listeners, and so on. The following example
demonstrates how to access property values from the job definition file
in an item reader implementation:

``` oac_no_warn
@Dependent
@Named("MyItemReaderImpl")
public class MyItemReaderImpl implements ItemReader {
    @Inject
    JobContext jobCtx;

    public MyItemReaderImpl() {}

    @Override
    public void open(Serializable checkpoint) throws Exception {
        String fileName = jobCtx.getProperties()
                                .getProperty("log_file_name");
        ...
    }
    ...
}
```

See [Dependency Injection in Batch Artifacts](#BCGIFJBB) for
instructions on how to define your batch artifacts to use dependency
injection.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
Do <span class="italic">not</span> access batch context objects inside artifact constructors.
<p>Because the job does not run until you submit it to the batch runtime, the batch context objects are not available when CDI instantiates your artifacts upon loading your application. The instantiation of these beans fails and the batch runtime cannot find your batch artifacts when your application submits the job.</p></td>
</tr>
</tbody>
</table>

  

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
<td><a href="batch-processing004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="batch-processing006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
