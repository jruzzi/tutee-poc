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
<td><a href="bean-validation001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="bean-validation003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 21.2 Using Bean Validation Constraints

The Bean Validation model is supported by constraints in the form of
annotations placed on a field, method, or class of a JavaBeans
component, such as a managed bean.

Constraints can be built in or user defined. User-defined constraints
are called custom constraints. Several built-in constraints are
available in the `javax.validation.constraints` package. [Table
21-1](#GKAGK) lists all the built-in constraints. See [Creating Custom
Constraints](bean-validation-advanced001.htm#GKFGX) for information on
creating custom constraints.

Table 21-1 Built-In Bean Validation Constraints

<table style="width:45%;">
<colgroup>
<col width="16%" />
<col width="28%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Constraint</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">@AssertFalse</code></p></td>
<td><p>The value of the field or property must be <code dir="ltr">false</code>.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@AssertFalse
boolean isUnsupported;</code></pre></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@AssertTrue</code></p></td>
<td><p>The value of the field or property must be <code dir="ltr">true</code>.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@AssertTrue
boolean isActive;</code></pre></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">@DecimalMax</code></p></td>
<td><p>The value of the field or property must be a decimal value lower than or equal to the number in the value element.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@DecimalMax(&quot;30.00&quot;)
BigDecimal discount;</code></pre></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@DecimalMin</code></p></td>
<td><p>The value of the field or property must be a decimal value greater than or equal to the number in the value element.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@DecimalMin(&quot;5.00&quot;)
BigDecimal discount;</code></pre></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">@Digits</code></p></td>
<td><p>The value of the field or property must be a number within a specified range. The <code dir="ltr">integer</code> element specifies the maximum integral digits for the number, and the <code dir="ltr">fraction</code> element specifies the maximum fractional digits for the number.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@Digits(integer=6, fraction=2)
BigDecimal price;</code></pre></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@Future</code></p></td>
<td><p>The value of the field or property must be a date in the future.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@Future
Date eventDate;</code></pre></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">@Max</code></p></td>
<td><p>The value of the field or property must be an integer value lower than or equal to the number in the value element.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@Max(10)
int quantity;</code></pre></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@Min</code></p></td>
<td><p>The value of the field or property must be an integer value greater than or equal to the number in the value element.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@Min(5)
int quantity;</code></pre></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">@NotNull</code></p></td>
<td><p>The value of the field or property must not be null.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@NotNull
String username;</code></pre></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@Null</code></p></td>
<td><p>The value of the field or property must be null.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@Null
String unusedString;</code></pre></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">@Past</code></p></td>
<td><p>The value of the field or property must be a date in the past.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@Past
Date birthday;</code></pre></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">@Pattern</code></p></td>
<td><p>The value of the field or property must match the regular expression defined in the <code dir="ltr">regexp</code> element.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@Pattern(regexp=&quot;\\(\\d{3}\\)\\d{3}-\\d{4}&quot;)
String phoneNumber;</code></pre></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">@Size</code></p></td>
<td><p>The size of the field or property is evaluated and must match the specified boundaries. If the field or property is a <code dir="ltr">String</code>, the size of the string is evaluated. If the field or property is a <code dir="ltr">Collection</code>, the size of the <code dir="ltr">Collection</code> is evaluated. If the field or property is a <code dir="ltr">Map</code>, the size of the <code dir="ltr">Map</code> is evaluated. If the field or property is an array, the size of the array is evaluated. Use one of the optional <code dir="ltr">max</code> or <code dir="ltr">min</code> elements to specify the boundaries.</p></td>
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>@Size(min=2, max=240)
String briefMessage;</code></pre></td>
</tr>
</tbody>
</table>

  

In the following example, a constraint is placed on a field using the
built-in `@NotNull` constraint:

``` oac_no_warn
public class Name {
    @NotNull 
    private String firstname;

    @NotNull 
    private String lastname;
    ...
}
```

You can also place more than one constraint on a single JavaBeans
component object. For example, you can place an additional constraint
for size of field on the `firstname` and the `lastname` fields:

``` oac_no_warn
public class Name {
    @NotNull
    @Size(min=1, max=16)
    private String firstname;

    @NotNull 
    @Size(min=1, max=16)
    private String lastname;
    ...
}
```

The following example shows a method with a user-defined constraint that
checks for a predefined email address pattern, such as a corporate email
account:

``` oac_no_warn
@ValidEmail 
public String getEmailAddress() {
    return emailAddress;
}
```

For a built-in constraint, a default implementation is available. A
user-defined or custom constraint needs a validation implementation. In
the preceding example, the `@ValidEmail` custom constraint needs an
implementation class.

Any validation failures are gracefully handled and can be displayed by
the `h:messages` tag.

Any managed bean that contains Bean Validation annotations automatically
gets validation constraints placed on the fields on a JavaServer Faces
application's web pages.

For more information on using validation constraints, see the following:

  - [Chapter 22, "Bean Validation: Advanced
    Topics"](bean-validation-advanced.htm#GKAHP)

  - [Validating Resource Data with Bean
    Validation](jaxrs-advanced002.htm#BABCJEDF)

  - [Validating Persistent Fields and
    Properties](persistence-intro002.htm#GKAHQ)

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
<td><a href="bean-validation001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="bean-validation003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
