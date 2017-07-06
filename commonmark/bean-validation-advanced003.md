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
<td><a href="bean-validation-advanced002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="bean-validation-advanced004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 22.3 Grouping Constraints

Constraints may be added to one or more groups. Constraint groups are
used to create subsets of constraints so that only certain constraints
will be validated for a particular object. By default, all constraints
are included in the `Default` constraint group.

Constraint groups are represented by interfaces.

``` oac_no_warn
public interface Employee {}

public interface Contractor {}
```

Constraint groups can inherit from other groups.

``` oac_no_warn
public interface Manager extends Employee {}
```

When a constraint is added to an element, the constraint declares the
groups to which that constraint belongs by specifying the class name of
the group interface name in the `groups` element of the constraint.

``` oac_no_warn
@NotNull(groups=Employee.class)
Phone workPhone;
```

Multiple groups can be declared by surrounding the groups with braces
(`{` and `}`) and separating the groups' class names with commas.

``` oac_no_warn
@NotNull(groups={ Employee.class, Contractor.class })
Phone workPhone;
```

If a group inherits from another group, validating that group results in
validating all constraints declared as part of the supergroup. For
example, validating the `Manager` group results in the `workPhone` field
being validated, because `Employee` is a superinterface of `Manager`.

## 22.3.1 Customizing Group Validation Order

By default, constraint groups are validated in no particular order.
There are cases in which some groups should be validated before others.
For example, in a particular class, basic data should be validated
before more advanced data.

To set the validation order for a group, add a
`javax.validation.GroupSequence` annotation to the interface definition,
listing the order in which the validation should occur.

``` oac_no_warn
@GroupSequence({Default.class, ExpensiveValidationGroup.class})
public interface FullValidationGroup {}
```

When validating `FullValidationGroup`, first the `Default` group is
validated. If all the data passes validation, then the
`ExpensiveValidationGroup` group is validated. If a constraint is part
of both the `Default` and the `ExpensiveValidationGroup` groups, the
constraint is validated as part of the `Default` group and will not be
validated on the subsequent `ExpensiveValidationGroup` pass.

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
<td><a href="bean-validation-advanced002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="bean-validation-advanced004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
