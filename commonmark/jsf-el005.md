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
<td><a href="jsf-el004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-el006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 9.5 Operators

In addition to the `.` and `[]` operators discussed in [Value and Method
Expressions](jsf-el003.htm#BNAHU), the EL provides the following
operators, which can be used in rvalue expressions only.

  - Arithmetic: `+`, `-` (binary), `*`, `/` and `div`, `%` and `mod`,
    `-` (unary).

  - String concatenation: `+=`.

  - Logical: `and`, `&&`, `or`, `||`, `not`, `!`.

  - Relational: `==`, `eq`, `!=`, `ne`, `<`, `lt`, `>`, `gt`, `<=`,
    `ge`, `>=`, `le`. Comparisons can be made against other values or
    against Boolean, string, integer, or floating-point literals.

  - Empty: The `empty` operator is a prefix operation that can be used
    to determine whether a value is `null` or empty.

  - Conditional: `A ? B : C`. Evaluate `B` or `C`, depending on the
    result of the evaluation of `A`.

  - Lambda expression: `->`, the arrow token.

  - Assignment: `=`.

  - Semicolon: `;`.

The precedence of operators, highest to lowest, left to right, is as
follows:

  - `[] .`

  - `()` (used to change the precedence of operators)

  - `-` (unary) `not ! empty`

  - `* / div % mod`

  - `+ -` (binary)

  - `+=`

  - `<> <= >= lt gt le ge`

  - `== != eq ne`

  - `&& and`

  - `|| or`

  - `? :`

  - `->`

  - `=`

  - `;`

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
<td><a href="jsf-el004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-el006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
