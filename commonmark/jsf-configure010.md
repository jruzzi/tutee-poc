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
<td><a href="jsf-configure009.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure011.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 16.10 Configuring Navigation Rules

Navigation between different pages of a JavaServer Faces application,
such as choosing the next page to be displayed after a button or link
component is clicked, is defined by a set of rules. Navigation rules can
be implicit, or they can be explicitly defined in the application
configuration resource file. For more information on implicit navigation
rules, see [Navigation Model](jsf-intro006.htm#BNAQL).

Each navigation rule specifies how to navigate from one page to another
page or set of pages. The JavaServer Faces implementation chooses the
proper navigation rule according to which page is currently displayed.

After the proper navigation rule is selected, the choice of which page
to access next from the current page depends on two factors:

  - The action method invoked when the component was clicked

  - The logical outcome referenced by the component's tag or returned
    from the action method

The outcome can be anything the developer chooses, but [Table
16-3](#BNAXG) lists some outcomes commonly used in web applications.

Table 16-3 Common Outcome Strings

<table style="width:17%;">
<colgroup>
<col width="17%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Outcome</th>
<th>What It Means</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">success</code></p></td>
<td><p>Everything worked. Go on to the next page.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">failure</code></p></td>
<td><p>Something is wrong. Go on to an error page.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">login</code></p></td>
<td><p>The user needs to log in first. Go on to the login page.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">no results</code></p></td>
<td><p>The search did not find anything. Go to the search page again.</p></td>
</tr>
</tbody>
</table>

  

Usually, the action method performs some processing on the form data of
the current page. For example, the method might check whether the user
name and password entered in the form match the user name and password
on file. If they match, the method returns the outcome `success`.
Otherwise, it returns the outcome `failure`. As this example
demonstrates, both the method used to process the action and the outcome
returned are necessary to determine the correct page to access.

Here is a navigation rule that could be used with the example just
described:

``` oac_no_warn
<navigation-rule>
    <from-view-id>/login.xhtml</from-view-id>
    <navigation-case>
        <from-action>#{LoginForm.login}</from-action>
        <from-outcome>success</from-outcome>
        <to-view-id>/storefront.xhtml</to-view-id>
    </navigation-case>
    <navigation-case>
        <from-action>#{LoginForm.logon}</from-action>
        <from-outcome>failure</from-outcome>
        <to-view-id>/logon.xhtml</to-view-id>
    </navigation-case>
</navigation-rule>
```

This navigation rule defines the possible ways to navigate from
`login.xhtml`. Each `navigation-case` element defines one possible
navigation path from `login.xhtml`. The first `navigation-case` says
that if `LoginForm.login` returns an outcome of `success`, then
`storefront.xhtml` will be accessed. The second `navigation-case` says
that `login.xhtml` will be re-rendered if `LoginForm.login` returns
`failure`.

The configuration of an application's page flow consists of a set of
navigation rules. Each rule is defined by the `navigation-rule` element
in the `faces-config.xml` file.

Each `navigation-rule` element corresponds to one component tree
identifier defined by the optional `from-view-id` element. This means
that each rule defines all the possible ways to navigate from one
particular page in the application. If there is no `from-view-id`
element, the navigation rules defined in the `navigation-rule` element
apply to all the pages in the application. The `from-view-id` element
also allows wildcard matching patterns. For example, this `from-view-id`
element says that the navigation rule applies to all the pages in the
`books` directory:

``` oac_no_warn
<from-view-id>/books/*</from-view-id>
```

A `navigation-rule` element can contain zero or more `navigation-case`
elements. The `navigation-case` element defines a set of matching
criteria. When these criteria are satisfied, the application will
navigate to the page defined by the `to-view-id` element contained in
the same `navigation-case` element.

The navigation criteria are defined by optional `from-outcome` and
`from-action` elements. The `from-outcome` element defines a logical
outcome, such as `success`. The `from-action` element uses a method
expression to refer to an action method that returns a `String`, which
is the logical outcome. The method performs some logic to determine the
outcome and returns the outcome.

The `navigation-case` elements are checked against the outcome and the
method expression in the following order.

1.  Cases specifying both a `from-outcome` value and a `from-action`
    value. Both of these elements can be used if the action method
    returns different outcomes depending on the result of the processing
    it performs.

2.  Cases specifying only a `from-outcome` value. The `from-outcome`
    element must match either the outcome defined by the `action`
    attribute of the `javax.faces.component.UICommand` component or the
    outcome returned by the method referred to by the `UICommand`
    component.

3.  Cases specifying only a `from-action` value. This value must match
    the `action` expression specified by the component tag.

When any of these cases is matched, the component tree defined by the
`to-view-id` element will be selected for rendering.

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
<td><a href="jsf-configure009.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-configure011.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
