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
<td><a href="batch-processing008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="batch-processing010.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 55.9 The phonebilling Example Application

The `phonebilling` example application, located in the
tut-install`/examples/batch/phonebilling/` directory, demonstrates how
to use the batch framework in Java EE to implement a phone billing
system. This example application processes a log file of phone calls and
creates a bill for each customer.

The following topics are addressed here:

  - [Section 55.9.1, "Architecture of the phonebilling Example
    Application"](#BABDEIFG)

  - [Section 55.9.2, "Running the phonebilling Example
    Application"](#BABBGDAA)

## 55.9.1 Architecture of the phonebilling Example Application

The `phonebilling` example application consists of the following
elements.

  - A job definition file (`phonebilling.xml`) that uses the Job
    Specification Language (JSL) to define a batch job with two chunk
    steps. The first step reads call records from a log file and
    associates them with a bill. The second step computes the amount due
    and writes each bill to a text file.

  - A Java class (`CallRecordLogCreator`) that creates the log file for
    the batch job. This is an auxiliary component that does not
    demonstrate any key functionality in this example.

  - Two Java Persistence API (JPA) entities (`CallRecord` and
    `PhoneBill`) that represent call records and customer bills. The
    application uses a JPA entity manager to store instances of these
    entities in a database.

  - Three batch artifacts (`CallRecordReader`, `CallRecordProcessor`,
    and `CallRecordWriter`) that implement the first step of the
    application. This step reads call records from the log file,
    associates them with a bill, and stores them in a database.

  - Four batch artifacts (`BillReader`, `BillProcessor`, `BillWriter`,
    and `BillPartitionMapper`) that implement the second step of the
    application. This step is a partitioned step that gets each bill
    from the database, calculates the amount due, and writes it to a
    text file.

  - Two Facelets pages (`index.xhtml` and `jobstarted.xhtml`) that
    provide the front end of the batch application. The first page shows
    the log file that will be processed by the batch job, and the second
    page enables the user to check on the status of the job and shows
    the resulting bill for each customer.

  - A managed bean (`JsfBean`) that is accessed from the Facelets pages.
    The bean submits the job to the batch runtime, checks on the status
    of the job, and reads the text files for each bill.

### 55.9.1.1 The Job Definition File

The `phonebilling.xml` job definition file is located in the
`WEB-INF/classes/META-INF/batch-jobs/` directory. The file specifies
three job-level properties and two steps:

``` oac_no_warn
<?xml version="1.0" encoding="UTF-8"?>
<job id="phonebilling" xmlns="http://xmlns.jcp.org/xml/ns/javaee" 
     version="1.0">
    <properties>
        <property name="log_file_name" value="log1.txt"/>
        <property name="airtime_price" value="0.08"/>
        <property name="tax_rate" value="0.07"/>
    </properties>
    <step id="callrecords" next="bills"> ... </step>
    <step id="bills"> ... </step>
</job>
```

The first step is defined as follows:

``` oac_no_warn
<step id="callrecords" next="bills">
    <chunk checkpoint-policy="item" item-count="10">
        <reader ref="CallRecordReader"></reader>
        <processor ref="CallRecordProcessor"></processor>
        <writer ref="CallRecordWriter"></writer>
    </chunk>
</step>
```

This step is a normal chunk step that specifies the batch artifacts that
implement each phase of the step. The batch artifact names are not fully
qualified class names, so the batch artifacts are CDI beans annotated
with `@Named`.

The second step is defined as follows:

``` oac_no_warn
<step id="bills">
    <chunk checkpoint-policy="item" item-count="2">
        <reader ref="BillReader">
            <properties>                <property name="firstItem" value="#{partitionPlan['firstItem']}"/>                <property name="numItems" value="#{partitionPlan['numItems']}"/>            </properties>        </reader>
        <processor ref="BillProcessor"></processor>
        <writer ref="BillWriter"></writer>
    </chunk>
    <partition>
        <mapper ref="BillPartitionMapper"/>
    </partition>
    <end on="COMPLETED"/>
</step>
```

This step is a partitioned chunk step. The partition plan is specified
through the `BillPartitionMapper` artifact instead of using the `plan`
element.

### 55.9.1.2 The CallRecord and PhoneBill Entities

The `CallRecord` entity is defined as follows:

``` oac_no_warn
@Entity
public class CallRecord implements Serializable {
    @Id @GeneratedValue
    private Long id;
    @Temporal(TemporalType.DATE)
    private Date datetime;
    private String fromNumber;
    private String toNumber;
    private int minutes;
    private int seconds;
    private BigDecimal price;

    public CallRecord() { }

    public CallRecord(String datetime, String from, 
            String to, int min, int sec)             throws ParseException { ... }

    public CallRecord(String jsonData) throws ParseException { ... }

    /* ... Getters and setters ... */
}
```

The `id` field is generated automatically by the JPA implementation to
store and retrieve `CallRecord` objects to and from a database.

The second constructor creates a `CallRecord` object from an entry of
JSON data in the log file using the JSON Processing API. Log entries
look as follows:

``` oac_no_warn
{"datetime":"03/01/2013 04:03","from":"555-0101",
"to":"555-0114","length":"03:39"}
```

The `PhoneBill` entity is defined as follows:

``` oac_no_warn
@Entity
public class PhoneBill implements Serializable {
    @Id
    private String phoneNumber;
    @OneToMany(fetch = FetchType.EAGER, cascade = CascadeType.PERSIST)
    @OrderBy("datetime ASC")
    private List<CallRecord> calls;
    private BigDecimal amountBase;
    private BigDecimal taxRate;
    private BigDecimal tax;
    private BigDecimal amountTotal;
 
    public PhoneBill() { }
    
    public PhoneBill(String number) {
        this.phoneNumber = number;
        calls = new ArrayList<>();
    }
    
    public void addCall(CallRecord call) {
        calls.add(call);
    }
    
    public void calculate(BigDecimal taxRate) { ... }

    /* ... Getters and setters ... *
}
```

The `OneToMany` annotation defines the relationship between a bill and
its call records. The `FetchType.EAGER` attribute specifies that the
collection should be retrieved eagerly. The `CascadeType.PERSIST`
attribute indicates that the elements in the call list should be
automatically persisted when the phone bill is persisted. The `OrderBy`
annotation defines an order for retrieving the elements of the call list
from the database.

The batch artifacts use instances of these two entities as items to
read, process, and write.

For more information on the Java Persistence API, see [Chapter 37,
"Introduction to the Java Persistence
API"](persistence-intro.htm#BNBPZ). For more information on the JSON
Processing API, see [Chapter 19, "JSON Processing"](jsonp.htm#GLRBB).

### 55.9.1.3 The Call Records Chunk Step

The first step is composed of the `CallRecordReader`,
`CallRecordProcessor`, and `CallRecordWriter` batch artifacts.

The `CallRecordReader` artifact reads call records from the log file:

``` oac_no_warn
@Dependent
@Named("CallRecordReader")
public class CallRecordReader implements ItemReader {
    private ItemNumberCheckpoint checkpoint;
    private String fileName;
    private BufferedReader breader;
    @Inject
    JobContext jobCtx;

    /* ... Override the open, close, readItem, 
     *     and checkpointInfo methods ... */
}
```

The `open` method reads the `log_filename` property and opens the log
file with a buffered reader:

``` oac_no_warn
fileName = jobCtx.getProperties().getProperty("log_file_name");
breader = new BufferedReader(new FileReader(fileName));
```

If a checkpoint object is provided, the `open` method advances the
reader up to the last checkpoint. Otherwise, this method creates a new
checkpoint object. The checkpoint object keeps track of the line number
from the last committed chunk.

The `readItem` method returns a new `CallRecord` object or null at the
end of the log file:

``` oac_no_warn
@Override
public Object readItem() throws Exception {
    /* Read a line from the log file and 
     * create a CallRecord from JSON */
    String callEntryJson = breader.readLine();
    if (callEntryJson != null) {
        checkpoint.nextItem();
        return new CallRecord(callEntryJson);
    } else
        return null;
}
```

The `CallRecordProcessor` artifact obtains the airtime price from the
job properties, calculates the price of each call, and returns the call
object. This artifact overrides only the `processItem` method.

The `CallRecordWriter` artifact associates each call record with a bill
and stores the bill in the database. This artifact overrides the `open`,
`close`, `writeItems`, and `checkpointInfo` methods. The `writeItems`
method looks like this:

``` oac_no_warn
@Override
public void writeItems(List<Object> callList) throws Exception {
    
    for (Object callObject : callList) {
        CallRecord call = (CallRecord) callObject;
        PhoneBill bill = em.find(PhoneBill.class, call.getFromNumber());
        if (bill == null) {
            /* No bill for this customer yet, create one */
            bill = new PhoneBill(call.getFromNumber());
            bill.addCall(call);
            em.persist(bill);
        } else {
            /* Add call to existing bill */
            bill.addCall(call);
        }
    }
}
```

### 55.9.1.4 The Phone Billing Chunk Step

The second step is composed of the `BillReader`, `BillProcessor`,
`BillWriter`, and `BillPartitionMapper` batch artifacts. This step gets
the phone bills from the database, computes the tax and total amount
due, and writes each bill to a text file. Since the processing of each
bill is independent of the others, this step can be partitioned and run
in more than one thread.

The `BillPartitionMapper` artifact specifies the number of partitions
and the parameters for each partition. In this example, the parameters
represent the range of items each partition should process. The artifact
obtains the number of bills in the database to calculate these ranges.
It provides a partition plan object that overrides the `getPartitions`
and `getPartitionProperties` methods of the `PartitionPlan` interface.
The `getPartitions` method looks like this:

``` oac_no_warn
@Override
public Properties[] getPartitionProperties() {
    /* Assign an (approximately) equal number of elements
     * to each partition. */
    long totalItems = getBillCount();
    long partItems = (long) totalItems / getPartitions();
    long remItems = totalItems % getPartitions();
 
    /* Populate a Properties array. Each Properties element
     * in the array corresponds to a partition. */
    Properties[] props = new Properties[getPartitions()];

    for (int i = 0; i < getPartitions(); i++) {
        props[i] = new Properties();
        props[i].setProperty("firstItem", 
                String.valueOf(i * partItems));
        /* Last partition gets the remainder elements */
        if (i == getPartitions() - 1) {
            props[i].setProperty("numItems", 
                    String.valueOf(partItems + remItems));
        } else {
            props[i].setProperty("numItems", 
                    String.valueOf(partItems));
    }
    return props;
}
```

The `BillReader` artifact obtains the partition parameters as follows:

``` oac_no_warn
@Dependent
@Named("BillReader")
public class BillReader implements ItemReader {
    @Inject    @BatchProperty(name = "firstItem")    private String firstItemValue;    @Inject    @BatchProperty(name = "numItems")    private String numItemsValue;
    private ItemNumberCheckpoint checkpoint;    @PersistenceContext    private EntityManager em;    private Iterator iterator;

    @Override
    public void open(Serializable ckpt) throws Exception {
        /* Get the range of items to work on in this partition */
        long firstItem0 = Long.parseLong(firstItemValue);
        long numItems0 = Long.parseLong(numItemsValue);
 
        if (ckpt == null) {
            /* Create a checkpoint object for this partition */
            checkpoint = new ItemNumberCheckpoint();
            checkpoint.setItemNumber(firstItem0);
            checkpoint.setNumItems(numItems0);
        } else {
            checkpoint = (ItemNumberCheckpoint) ckpt;
        }
 
        /* Adjust range for this partition from the checkpoint */
        long firstItem = checkpoint.getItemNumber();
        long numItems = numItems0 - (firstItem - firstItem0);
        ...
    }
    ...
}
```

This artifact also obtains an iterator to read items from the JPA entity
manager:

``` oac_no_warn
/* Obtain an iterator for the bills in this partition */
String query = "SELECT b FROM PhoneBill b ORDER BY b.phoneNumber";
Query q = em.createQuery(query).setFirstResult((int) firstItem)
        .setMaxResults((int) numItems);
iterator = q.getResultList().iterator();
```

The `BillProcessor` artifact iterates over the list of call records in a
bill and calculates the tax and total amount due for each bill.

The `BillWriter` artifact writes each bill to a plain text file.

### 55.9.1.5 The JavaServer Faces Pages

The `index.xhtml` page contains a text area that shows the log file of
call records. The page provides a button for the user to submit the
batch job and navigate to the next page:

``` oac_no_warn
<body>
    <h1>The Phone Billing Example Application</h1>
    <h2>Log file</h2>
    <p>The batch job analyzes the following log file:</p>
    <textarea cols="90" rows="25" 
              readonly="true">#{jsfBean.createAndShowLog()}</textarea>
    <p> </p>
    <h:form>
        <h:commandButton value="Start Batch Job" 
                         action="#{jsfBean.startBatchJob()}" />
    </h:form>
</body>
```

This page calls the methods of the managed bean to show the log file and
submit the batch job.

The `jobstarted.xhtml` page provides a button to check the current
status of the batch job and displays the bills when the job finishes:

``` oac_no_warn
<p>Current Status of the Job: <b>#{jsfBean.jobStatus}</b></p>
<h:dataTable var="_row" value="#{jsfBean.rowList}" 
             border="1" rendered="#{jsfBean.completed}">
    <!-- ... show results from jsfBean.rowList ... -->
</h:dataTable>
<!-- Render the check status button if the job has not finished -->
<h:form>
    <h:commandButton value="Check Status" 
                     rendered="#{jsfBean.completed==false}"
                     action="jobstarted" />
</h:form>
```

### 55.9.1.6 The Managed Bean

The `JsfBean` managed bean submits the job to the batch runtime, checks
on the status of the job, and reads the text files for each bill.

The `startBatchJob` method of the bean submits the job to the batch
runtime:

``` oac_no_warn
/* Submit the batch job to the batch runtime.
 * JSF Navigation method (return the name of the next page) */
public String startBatchJob() {
    jobOperator = BatchRuntime.getJobOperator();
    execID = jobOperator.start("phonebilling", null);
    return "jobstarted";
}
```

The `getJobStatus` method of the bean checks the status of the job:

``` oac_no_warn
/* Get the status of the job from the batch runtime */
public String getJobStatus() {
    return jobOperator.getJobExecution(execID).getBatchStatus().toString();
}
```

The `getRowList` method of the bean creates a list of bills to be
displayed on the `jobstarted.xhtml` JSF page using a table.

## 55.9.2 Running the phonebilling Example Application

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `phonebilling` example application.

The following topics are addressed here:

  - [Section 55.9.2.1, "To Run the phonebilling Example Application
    Using NetBeans IDE"](#BABIBBBG)

  - [Section 55.9.2.2, "To Run the phonebilling Example Application
    Using
Maven"](#BABFHIIB)

### 55.9.2.1 To Run the phonebilling Example Application Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  From the File menu, choose Open Project.

3.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/batch
    ```

4.  Select the `phonebilling` folder.

5.  Click Open Project.

6.  In the Projects tab, right-click the `phonebilling` project and
    select Run.
    
    This command builds and packages the application into a WAR file,
    `phonebilling.war`, located in the `target/` directory; deploys it
    to the server; and launches a web browser window at the following
    URL:
    
    ``` oac_no_warn
    http://localhost:8080/phonebilling/
    ```

### 55.9.2.2 To Run the phonebilling Example Application Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/batch/phonebilling/
    ```

3.  Enter the following command to deploy the application:
    
    ``` oac_no_warn
    mvn install
    ```

4.  Open a web browser window at the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/phonebilling/
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
<td><a href="batch-processing008.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="batch-processing010.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
