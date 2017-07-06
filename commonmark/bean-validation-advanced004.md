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
<td><a href="bean-validation-advanced003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partcdi.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 22.4 Using Method Constraints in Type Hierarchies

If you add validation constraints to objects in an inheritance
hierarchy, take special care to avoid unintended errors when using
subtypes.

For a given type, subtypes should be able to be substituted without
encountering errors. For example, if you have a `Person` class and an
`Employee` subclass that extends `Person`, you should be able to use
`Employee` instances wherever you might use `Person` instances. If
`Employee` overrides a method in `Person` by adding method parameter
constraints, code that works correctly with `Person` objects may throw
validation exceptions with `Employee` objects.

The following code shows an incorrect use of method parameter
constraints within a class hierarchy:

``` oac_no_warn
public class Person {
...
  public void setEmail(String email) { ... }
}

public class Employee extends Person {
...
  @Override
  public void setEmail(@Verified String email) { ... }
}
```

By adding the `@Verified` constraint to `Employee.setEmail`, parameters
that were valid with `Person.setEmail` will not be valid with
`Employee.setEmail`. This is called strengthening the preconditions
(that is, the method parameters) of a subtype's method. You may not
strengthen the preconditions of subtype method calls.

Similarly, the return values from method calls should not be weakened in
subtypes. The following code shows an incorrect use of constraints on
method return values in a class hierarchy:

``` oac_no_warn
public class Person {
...
  @Verified
  public Email getEmail() { ... }
}

public class Employee extends Person {
...
  @Override
  public Email getEmail() { ... }
}
```

In this example, the `Employee.getEmail` method removes the `@Verified`
constraint on the return value. Return values that would be not pass
validation when calling `Person.getEmail` are allowed when calling
`Employee.getEmail`. This is called weakening the postconditions (that
is, return values) of a subtype. You may not weaken the postconditions
of a subtype method call.

If your type hierarchy strengthens the preconditions or weakens the
postconditions of subtype method calls, a
`javax.validation.ConstraintDeclarationException` will be thrown by the
Bean Validation runtime.

Classes that implement several interfaces that each have the same method
signature, known as parallel types, need to be aware of the constraints
applied to the interfaces that they implement to avoid strengthening the
preconditions. For example:

``` oac_no_warn
public interface PaymentService {
  void processOrder(Order order, double amount);
...
}

public interface CreditCardPaymentService {
  void processOrder(@NotNull Order order, @NotNull double amount);
...
}

public class MyPaymentService implements PaymentService,
        CreditCardPaymentService {

  @Override
  public void processOrder(Order order, double amount) { ... }
...
}
```

In this case, `MyPaymentService` has the constraints from the
`processOrder` method in `CreditCardPaymentService`, but client code
that calls `PaymentService.processOrder` doesn't expect these
constraints. This is another example of strengthening the preconditions
of a subtype and will result in a `ConstraintDeclarationException`.

## 22.4.1 Rules for Using Method Constraints in Type Hierarchies

The following rules define how method validation constraints should be
used in type hierarchies.

  - Do not add method parameter constraints to overridden or implemented
    methods in a subtype.

  - Do not add method parameter constraints to overridden or implemented
    methods in a subtype that was originally declared in several
    parallel types.

  - You may add return value constraints to an overridden or implemented
    method in a subtype.

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
<td><a href="bean-validation-advanced003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="partcdi.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
