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
<td><a href="bean-validation003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="bean-validation005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 21.4 Validating Constructors and Methods

Bean Validation constraints may be placed on the parameters of nonstatic
methods and constructors and on the return values of nonstatic methods.
Static methods and constructors will not be validated.

``` oac_no_warn
public class Employee {
...
  public Employee (@NotNull String name) { ... }

  public void setSalary(
      @NotNull 
      @Digits(integer=6, fraction=2) BigDecimal salary,
      @NotNull
      @ValidCurrency
      String currencyType) {
    ...
  }
...
}
```

In this example, the `Employee` class has a constructor constraint
requiring a name and has two sets of method parameter constraints. The
amount of the salary for the employee must not be null, cannot be
greater than six digits to the left of the decimal point, and cannot
have more than two digits to the right of the decimal place. The
currency type must not be null and is validated using a custom
constraint.

If you add method constraints to classes in an object hierarchy, special
care must be taken to avoid unintended behavior by subtypes. See [Using
Method Constraints in Type
Hierarchies](bean-validation-advanced004.htm#CIHGJBGI) for more
information.

## 21.4.1 Cross-Parameter Constraints

Constraints that apply to multiple parameters are called cross-parameter
constraints, and may be applied at the method or constructor level.

``` oac_no_warn
@ConsistentPhoneParameters
@NotNull
public Employee (String name, String officePhone, String mobilePhone) {
  ...
}
```

In this example, a custom cross-parameter constraint,
`@ConsistentPhoneParameters`, validates that the format of the phone
numbers passed into the constructor match. The `@NotNull` constraint
applies to all the parameters in the constructor.

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Tip:</p>
Cross-parameter constraint annotations are applied directly to the method or constructor. Return value constraints are also applied directly to the method or constructor. To avoid confusion as to where the constraint applies, parameter or return value, choose a name for any custom constraints that identifies where the constraint applies. For instance, the preceding example applies a custom constraint, <code dir="ltr">@ConsistentPhoneParameters</code>, that indicates that it applies to the parameters of the method or constructor.
<p>When you create a custom constraint that applies to both method parameters and return values, the <code dir="ltr">validationAppliesTo</code> element of the constraint annotation may be set to <code dir="ltr">ConstraintTarget.RETURN_VALUE</code> or <code dir="ltr">ConstraintTarget.PARAMETERS</code> to explicitly set the target of the validation constraint.</p></td>
</tr>
</tbody>
</table>

  

## 21.4.2 Identifying Parameter Constraint Violations

If a `ConstraintViolationException` occurs during a method call, the
Bean Validation runtime returns a parameter index to identify which
parameter caused the constraint violation. The parameter index is in the
form `arg`PARAMETER\_INDEX, where PARAMETER\_INDEX is an integer that
starts at 0 for the first parameter of the method or constructor.

## 21.4.3 Adding Constraints to Method Return Values

To validate the return value for a method, you can apply constraints
directly to the method or constructor declaration.

``` oac_no_warn
@NotNull
public Employee getEmployee() { ... }
```

Cross-parameter constraints are also applied at the method level. Custom
constraints that could be applied to both the return value and the
method parameters have an ambiguous constraint target. To avoid this
ambiguity, add a `validationAppliesTo` element to the constraint
annotation definition with the default set to either
`ConstraintTarget.RETURN_VALUE` or `ConstraintTarget.PARAMETERS` to
explicitly set the target of the validation constraint.

``` oac_no_warn
@Manager(validationAppliesTo=ConstraintTarget.RETURN_VALUE)
public Employee getManager(Employee employee) { ... }
```

See [Removing Ambiguity in Constraint
Targets](bean-validation-advanced001.htm#CIHCICAI) for more information.

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
<td><a href="bean-validation003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="bean-validation005.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
