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
<td><a href="cdi-adv004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 25.5 Using Events in CDI Applications

Events allow beans to communicate without any compile-time dependency.
One bean can define an event, another bean can fire the event, and yet
another bean can handle the event. The beans can be in separate packages
and even in separate tiers of the application.

## 25.5.1 Defining Events

An event consists of the following:

  - The event object, a Java object

  - Zero or more qualifier types, the event qualifiers

For example, in the `billpayment` example described in [The billpayment
Example: Using Events and Interceptors](cdi-adv-examples005.htm#GKHPA),
a `PaymentEvent` bean defines an event using three properties, which
have setter and getter methods:

``` oac_no_warn
    public String paymentType;
    public BigDecimal value;
    public Date datetime;

    public PaymentEvent() {
    }
```

The example also defines qualifiers that distinguish between two kinds
of `PaymentEvent`. Every event also has the default qualifier `@Any`.

## 25.5.2 Using Observer Methods to Handle Events

An event handler uses an observer method to consume events.

Each observer method takes as a parameter an event of a specific event
type that is annotated with the `@Observes` annotation and with any
qualifiers for that event type. The observer method is notified of an
event if the event object matches the event type and if all the
qualifiers of the event match the observer method event qualifiers.

The observer method can take other parameters in addition to the event
parameter. The additional parameters are injection points and can
declare qualifiers.

The event handler for the `billpayment` example, `PaymentHandler`,
defines two observer methods, one for each type of `PaymentEvent`:

``` oac_no_warn
public void creditPayment(@Observes @Credit PaymentEvent event) {
    ...
}

public void debitPayment(@Observes @Debit PaymentEvent event) {
    ...
}
```

Observer methods can also be conditional or transactional:

  - A conditional observer method is notified of an event only if an
    instance of the bean that defines the observer method already exists
    in the current context. To declare a conditional observer method,
    specify `notifyObserver=IF_EXISTS` as an argument to `@Observes`:
    
    ``` oac_no_warn
    @Observes(notifyObserver=IF_EXISTS)
    ```
    
    To obtain the default unconditional behavior, you can specify
    `@Observes(notifyObserver=ALWAYS)`.

  - A transactional observer method is notified of an event during the
    before-completion or after-completion phase of the transaction in
    which the event was fired. You can also specify that the
    notification is to occur only after the transaction has completed
    successfully or unsuccessfully. To specify a transactional observer
    method, use any of the following arguments to `@Observes`:
    
    ``` oac_no_warn
    @Observes(during=BEFORE_COMPLETION)
    
    @Observes(during=AFTER_COMPLETION)
    
    @Observes(during=AFTER_SUCCESS)
    
    @Observes(during=AFTER_FAILURE)
    ```
    
    To obtain the default nontransactional behavior, specify
    `@Observes(during=IN_PROGRESS)`.
    
    An observer method that is called before completion of a transaction
    may call the `setRollbackOnly` method on the transaction instance to
    force a transaction rollback.

Observer methods may throw exceptions. If a transactional observer
method throws an exception, the exception is caught by the container. If
the observer method is nontransactional, the exception terminates
processing of the event, and no other observer methods for the event are
called.

## 25.5.3 Firing Events

To activate an event, call the `javax.enterprise.event.Event.fire`
method. This method fires an event and notifies any observer methods.

In the `billpayment` example, a managed bean called `PaymentBean` fires
the appropriate event by using information it receives from the user
interface. There are actually four event beans, two for the event object
and two for the payload. The managed bean injects the two event beans.
The `pay` method uses a `switch` statement to choose which event to
fire, using `new` to create the payload.

``` oac_no_warn
    @Inject
    @Credit
    Event<PaymentEvent> creditEvent;

    @Inject
    @Debit
    Event<PaymentEvent> debitEvent;

    private static final int DEBIT = 1;
    private static final int CREDIT = 2;
    private int paymentOption = DEBIT;
    ...

    @Logged
    public String pay() {
        ...
        switch (paymentOption) {
            case DEBIT:
                PaymentEvent debitPayload = new PaymentEvent();
                // populate payload ... 
                debitEvent.fire(debitPayload);
                break;
            case CREDIT:
                PaymentEvent creditPayload = new PaymentEvent();
                // populate payload ... 
                creditEvent.fire(creditPayload);
                break;
            default:
                logger.severe("Invalid payment option!");
        }
        ...
    }
```

The argument to the `fire` method is a `PaymentEvent` that contains the
payload. The fired event is then consumed by the observer methods.

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
<td><a href="cdi-adv004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="cdi-adv006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
