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
<td><a href="jsf-page002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-page-core.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 10.3 Using Core Tags

The tags included in the JavaServer Faces core tag library are used to
perform core actions that are not performed by HTML tags.

[Table 10-8](#GKVYB) lists the event-handling core tags.

Table 10-8 Event-Handling Core Tags

<table style="width:36%;">
<colgroup>
<col width="36%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">f:actionListener</code></p></td>
<td><p>Adds an action listener to a parent component</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:phaseListener</code></p></td>
<td><p>Adds a <code dir="ltr">PhaseListener</code> to a page</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">f:setPropertyActionListener</code></p></td>
<td><p>Registers a special action listener whose sole purpose is to push a value into a managed bean when a form is submitted</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:valueChangeListener</code></p></td>
<td><p>Adds a value-change listener to a parent component</p></td>
</tr>
</tbody>
</table>

  

[Table 10-9](#GKVYY) lists the data-conversion core tags.

Table 10-9 Data-Conversion Core Tags

<table style="width:30%;">
<colgroup>
<col width="30%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">f:converter</code></p></td>
<td><p>Adds an arbitrary converter to the parent component</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:convertDateTime</code></p></td>
<td><p>Adds a <code dir="ltr">DateTimeConverter</code> instance to the parent component</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">f:convertNumber</code></p></td>
<td><p>Adds a <code dir="ltr">NumberConverter</code> instance to the parent component</p></td>
</tr>
</tbody>
</table>

  

[Table 10-10](#GKVZG) lists the facet core tags.

Table 10-10 Facet Core Tags

<table style="width:30%;">
<colgroup>
<col width="30%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">f:facet</code></p></td>
<td><p>Adds a nested component that has a special relationship to its enclosing tag</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:metadata</code></p></td>
<td><p>Registers a <code dir="ltr">facet</code> on a parent component</p></td>
</tr>
</tbody>
</table>

  

[Table 10-11](#GKVZA) lists the core tags that represent items in a
list.

Table 10-11 Core Tags That Represent Items in a List

<table style="width:30%;">
<colgroup>
<col width="30%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">f:selectItem</code></p></td>
<td><p>Represents one item in a list of items</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:selectItems</code></p></td>
<td><p>Represents a set of items</p></td>
</tr>
</tbody>
</table>

  

[Table 10-12](#GKVYV) lists the validator core tags.

Table 10-12 Validator Core Tags

<table style="width:30%;">
<colgroup>
<col width="30%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">f:validateDoubleRange</code></p></td>
<td><p>Adds a <code dir="ltr">DoubleRangeValidator</code> to a component</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:validateLength</code></p></td>
<td><p>Adds a <code dir="ltr">LengthValidator</code> to a component</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">f:validateLongRange</code></p></td>
<td><p>Adds a <code dir="ltr">LongRangeValidator</code> to a component</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:validator</code></p></td>
<td><p>Adds a custom validator to a component</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">f:validateRegEx</code></p></td>
<td><p>Adds a <code dir="ltr">RegExValidator</code> to a component</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:validateBean</code></p></td>
<td><p>Delegates the validation of a local value to a <code dir="ltr">BeanValidator</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">f:validateRequired</code></p></td>
<td><p>Enforces the presence of a value in a component</p></td>
</tr>
</tbody>
</table>

  

[Table 10-13](#GKVYU) lists the core tags that fall into other
categories.

Table 10-13 Miscellaneous Core Tags

<table style="width:47%;">
<colgroup>
<col width="28%" />
<col width="19%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag Category</th>
<th>Tag</th>
<th>Function</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attribute configuration</p></td>
<td><p><code dir="ltr">f:attribute</code></p></td>
<td><p>Adds configurable attributes to a parent component</p></td>
</tr>
<tr class="even">
<td><p>Localization</p></td>
<td><p><code dir="ltr">f:loadBundle</code></p></td>
<td><p>Specifies a <code dir="ltr">ResourceBundle</code> that is exposed as a <code dir="ltr">Map</code></p></td>
</tr>
<tr class="odd">
<td><p>Parameter substitution</p></td>
<td><p><code dir="ltr">f:param</code></p></td>
<td><p>Substitutes parameters into a <code dir="ltr">MessageFormat</code> instance and adds query string name-value pairs to a URL</p></td>
</tr>
<tr class="even">
<td><p>Ajax</p></td>
<td><p><code dir="ltr">f:ajax</code></p></td>
<td><p>Associates an Ajax action with a single component or a group of components based on placement</p></td>
</tr>
<tr class="odd">
<td><p>Event</p></td>
<td><p><code dir="ltr">f:event</code></p></td>
<td><p>Allows installing a <code dir="ltr">ComponentSystemEventListener</code> on a component</p></td>
</tr>
</tbody>
</table>

  

These tags, which are used in conjunction with component tags, are
explained in other sections of this tutorial.

[Table 10-14](#BNARE) lists the sections that explain how to use
specific core tags.

Table 10-14 Where the Core Tags Are Explained

<table style="width:28%;">
<colgroup>
<col width="28%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Tags</th>
<th>Where Explained</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Event-handling tags</p></td>
<td><p><a href="jsf-page-core002.htm#BNASZ">Registering Listeners on Components</a></p>
<br />
</td>
</tr>
<tr class="even">
<td><p>Data-conversion tags</p></td>
<td><p><a href="jsf-page-core001.htm#BNAST">Using the Standard Converters</a></p>
<br />
</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">f:facet</code></p></td>
<td><p><a href="jsf-page002.htm#BNARZ">Using Data-Bound Table Components</a> and <a href="jsf-page002.htm#BNASC">Laying Out Components with the h:panelGrid and h:panelGroup Tags</a></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:loadBundle</code></p></td>
<td><p><a href="webi18n002.htm#BNAXY">Setting the Resource Bundle</a></p>
<br />
</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">f:metadata</code></p></td>
<td><p><a href="jsf-page002.htm#GIQWQ">Using View Parameters to Configure Bookmarkable URLs</a></p>
<br />
</td>
</tr>
<tr class="even">
<td><p><code dir="ltr">f:param</code></p></td>
<td><p><a href="jsf-page002.htm#BNARU">Displaying a Formatted Message with the h:outputFormat Tag</a></p>
<br />
</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">f:selectItem</code> and <code dir="ltr">f:selectItems</code></p></td>
<td><p><a href="jsf-page002.htm#BNASK">Using the f:selectItem and f:selectItems Tags</a></p>
<br />
</td>
</tr>
<tr class="even">
<td><p>Validator tags</p></td>
<td><p><a href="jsf-page-core003.htm#BNATC">Using the Standard Validators</a></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">f:ajax</code></p></td>
<td><p><a href="jsf-ajax.htm#GKIOW">Chapter 13, &quot;Using Ajax with JavaServer Faces Technology&quot;</a></p>
<br />
</td>
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
<td><a href="jsf-page002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-page-core.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
