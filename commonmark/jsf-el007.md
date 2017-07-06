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
<td><a href="jsf-el006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-el008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 9.7 Examples of EL Expressions

[Table 9-1](#BNAIN) contains example EL expressions and the result of
evaluating them.

Table 9-1 Example Expressions

<table style="width:45%;">
<colgroup>
<col width="0%" />
<col width="45%" />
</colgroup>
<thead>
<tr class="header">
<th>EL Expression</th>
<th>Result</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">${1&gt; (4/2)}</code></p></td>
<td><p><code dir="ltr">false</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">${4.0&gt;= 3}</code></p></td>
<td><p><code dir="ltr">true</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">${100.0 == 100}</code></p></td>
<td><p><code dir="ltr">true</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">${(10*10) ne 100}</code></p></td>
<td><p><code dir="ltr">false</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">${'a' &gt; 'b'}</code></p></td>
<td><p><code dir="ltr">false</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">${'hip' lt 'hit'}</code></p></td>
<td><p><code dir="ltr">true</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">${4&gt; 3}</code></p></td>
<td><p><code dir="ltr">true</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">${1.2E4 + 1.4}</code></p></td>
<td><p><code dir="ltr">12001.4</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">${3 div 4}</code></p></td>
<td><p><code dir="ltr">0.75</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">${10 mod 4}</code></p></td>
<td><p><code dir="ltr">2</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">${((x, y) -&gt; x + y)(3, 5.5)}</code></p></td>
<td><p><code dir="ltr">8.5</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">[1,2,3,4].stream().sum()</code></p></td>
<td><p><code dir="ltr">10</code></p></td>
</tr>
<tr class="odd">
<td><p>[1,3,5,2].stream().sorted().toList()</p></td>
<td><p><code dir="ltr">[1, 2, 3, 5]</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">${!empty param.Add}</code></p></td>
<td><p><code dir="ltr">False</code> if the request parameter named <code dir="ltr">Add</code> is <code dir="ltr">null</code> or an empty string</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">${pageContext.request.contextPath}</code></p></td>
<td><p>The context path</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">${sessionScope.cart.numberOfItems}</code></p></td>
<td><p>The value of the <code dir="ltr">numberOfItems</code> property of the session-scoped attribute named <code dir="ltr">cart</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">${param['mycom.productId']}</code></p></td>
<td><p>The value of the request parameter named <code dir="ltr">mycom.productId</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">${header[&quot;host&quot;]}</code></p></td>
<td><p>The host</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">${departments[deptName]}</code></p></td>
<td><p>The value of the entry named <code dir="ltr">deptName</code> in the <code dir="ltr">departments</code> map</p></td>
</tr>
<tr class="even">
<td><pre class="oac_no_warn" space="preserve" dir="ltr"><code>${requestScope[&#39;javax.servlet.forward.servlet_path&#39;]}</code></pre></td>
<td><p>The value of the request-scoped attribute named <code dir="ltr">javax.servlet.forward.servlet_path</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">#{customer.lName}</code></p></td>
<td><p>Gets the value of the property <code dir="ltr">lName</code> from the <code dir="ltr">customer</code> bean during an initial request; sets the value of <code dir="ltr">lName</code> during a postback</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">#{customer.calcTotal}</code></p></td>
<td><p>The return value of the method <code dir="ltr">calcTotal</code> of the <code dir="ltr">customer</code> bean</p></td>
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
<td><a href="jsf-el006.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-el008.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
