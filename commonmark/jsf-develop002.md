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
<td><a href="jsf-develop001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-develop003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 12.2 Writing Bean Properties

As explained in [Managed Beans in JavaServer Faces
Technology](jsf-develop001.htm#BNAQM), a managed bean property can be
bound to one of the following items:

  - A component value

  - A component instance

  - A converter implementation

  - A listener implementation

  - A validator implementation

These properties follow the conventions of JavaBeans components (also
called beans). For more information on JavaBeans components, see the
JavaBeans Tutorial at
`http://docs.oracle.com/javase/tutorial/javabeans/index.html`.

The component's tag binds the component's value to a managed bean
property by using its `value` attribute and binds the component's
instance to a managed bean property by using its `binding` attribute.
Likewise, all the converter, listener, and validator tags use their
`binding` attributes to bind their associated implementations to managed
bean properties. See [Binding Component Values and Instances to Managed
Bean Properties](jsf-custom013.htm#BNATG) and [Binding Converters,
Listeners, and Validators to Managed Bean
Properties](jsf-custom014.htm#BNATM) for more information.

To bind a component's value to a managed bean property, the type of the
property must match the type of the component's value to which it is
bound. For example, if a managed bean property is bound to a
`UISelectBoolean` component's value, the property should accept and
return a `boolean` value or a `Boolean` wrapper `Object` instance.

To bind a component instance to a managed bean property, the property
must match the type of component. For example, if a managed bean
property is bound to a `UISelectBoolean` instance, the property should
accept and return a `UISelectBoolean` value.

Similarly, to bind a converter, listener, or validator implementation to
a managed bean property, the property must accept and return the same
type of converter, listener, or validator object. For example, if you
are using the `convertDateTime` tag to bind a
`javax.faces.convert.DateTimeConverter` to a property, that property
must accept and return a `DateTimeConverter` instance.

The rest of this section explains how to write properties that can be
bound to component values, to component instances for the component
objects described in [Adding Components to a Page Using HTML Tag Library
Tags](jsf-page002.htm#BNARF), and to converter, listener, and validator
implementations.

## 12.2.1 Writing Properties Bound to Component Values

To write a managed bean property that is bound to a component's value,
you must match the property type to the component's value.

[Table 12-1](#BNAUA) lists the `javax.faces.component` classes and the
acceptable types of their values.

Table 12-1 Acceptable Types of Component Values

<table style="width:32%;">
<colgroup>
<col width="32%" />
<col width="0%" />
</colgroup>
<thead>
<tr class="header">
<th>Component Class</th>
<th>Acceptable Types of Component Values</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr">UIInput</code>, <code dir="ltr">UIOutput</code>, <code dir="ltr">UISelectItem</code>, <code dir="ltr">UISelectOne</code></p></td>
<td><p>Any of the basic primitive and numeric types or any Java programming language object type for which an appropriate <code dir="ltr">javax.faces.convert.Converter</code> implementation is available</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">UIData</code></p></td>
<td><p><code dir="ltr">array</code> of beans, <code dir="ltr">List</code> of beans, single bean, <code dir="ltr">java.sql.ResultSet</code>, <code dir="ltr">javax.servlet.jsp.jstl.sql.Result</code>, <code dir="ltr">javax.sql.RowSet</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">UISelectBoolean</code></p></td>
<td><p><code dir="ltr">boolean</code> or <code dir="ltr">Boolean</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr">UISelectItems</code></p></td>
<td><p><code dir="ltr">java.lang.String</code>, <code dir="ltr">Collection</code>, <code dir="ltr">Array</code>, <code dir="ltr">Map</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr">UISelectMany</code></p></td>
<td><p><code dir="ltr">array</code> or <code dir="ltr">List</code>, although elements of the <code dir="ltr">array</code> or <code dir="ltr">List</code> can be any of the standard types</p></td>
</tr>
</tbody>
</table>

  

When they bind components to properties by using the `value` attributes
of the component tags, page authors need to ensure that the
corresponding properties match the types of the components' values.

### 12.2.1.1 UIInput and UIOutput Properties

The `UIInput` and `UIOutput` component classes are represented by the
component tags that begin with `h:input` and `h:output`, respectively
(for example, `h:inputText` and `h:outputText`).

In the following example, an `h:inputText` tag binds the `name`
component to the `name` property of a managed bean called `CashierBean`.

``` oac_no_warn
<h:inputText id="name" 
             size="30"
             value="#{cashierBean.name}"
    ...>
</h:inputText>
```

The following code snippet from the managed bean `CashierBean` shows the
bean property type bound by the preceding component tag:

``` oac_no_warn
protected String name = null;

public void setName(String name) {
    this.name = name;
}
public String getName() {
    return this.name;
}
```

As described in [Using the Standard
Converters](jsf-page-core001.htm#BNAST), to convert the value of an
input or output component you can either apply a converter or create the
bean property bound to the component with the matching type. Here is the
example tag, from [Using DateTimeConverter](jsf-page-core001.htm#BNASV),
that displays the date on which items will be shipped.

``` oac_no_warn
<h:outputText value="#{cashierBean.shipDate}">
    <f:convertDateTime type="date" dateStyle="full" />
</h:outputText>
```

The bean property represented by this tag must have a type of
`java.util.Date`. The following code snippet shows the `shipDate`
property, from the managed bean `CashierBean`, that is bound by the
tag's value in the preceding example:

``` oac_no_warn
private Date shipDate;

public Date getShipDate() {
    return this.shipDate;
}
public void setShipDate(Date shipDate) {
    this.shipDate = shipDate;
}
```

### 12.2.1.2 UIData Properties

The `UIData` component class is represented by the `h:dataTable`
component tag.

`UIData` components must be bound to one of the managed bean property
types listed in [Table 12-1](#BNAUA). Data components are discussed in
[Using Data-Bound Table Components](jsf-page002.htm#BNARZ). Here is part
of the start tag of `dataTable` from that section:

``` oac_no_warn
<h:dataTable id="items"
    ...
    value="#{cart.items}"
    ...
    var="item">
```

The value expression points to the `items` property of a shopping cart
bean named `cart`. The `cart` bean maintains a map of `ShoppingCartItem`
beans.

The `getItems` method from the `cart` bean populates a `List` with
`ShoppingCartItem` instances that are saved in the `items` map when the
customer adds books to the cart, as shown in the following code segment:

``` oac_no_warn
public synchronized List<ShoppingCartItem> getItems() {
    List<ShoppingCartItem> results = new ArrayList<ShoppingCartItem>();
    results.addAll(this.items.values());
    return results;
}
```

All the components contained in the `UIData` component are bound to the
properties of the `cart` bean that is bound to the entire `UIData`
component. For example, here is the `h:outputText` tag that displays the
book title in the table:

``` oac_no_warn
<h:commandLink action="#{showcart.details}">
    <h:outputText value="#{item.item.title}"/>
</h:commandLink>
```

The title is actually a link to the `bookdetails.xhtml` page. The
`h:outputText` tag uses the value expression `#{item.item.title}` to
bind its `UIOutput` component to the `title` property of the `Book`
entity. The first item in the expression is the `ShoppingCartItem`
instance that the `h:dataTable` tag is referencing while rendering the
current row. The second item in expression refers to the `item` property
of `ShoppingCartItem`, which returns an `Object` (in this case, a
`Book`). The `title` part of the expression refers to the `title`
property of `Book`. The value of the `UIOutput` component corresponding
to this tag is bound to the `title` property of the `Book` entity:

``` oac_no_warn
private String title;
...
public String getTitle() {
    return title;
}

public void setTitle(String title) {
    this.title = title;
}
```

### 12.2.1.3 UISelectBoolean Properties

The `UISelectBoolean` component class is represented by the component
tag `h:selectBooleanCheckbox`.

Managed bean properties that hold a `UISelectBoolean` component's data
must be of `boolean` or `Boolean` type. The example
`selectBooleanCheckbox` tag from the section [Displaying Components for
Selecting One Value](jsf-page002.htm#BNASE) binds a component to a
property. The following example shows a tag that binds a component value
to a `boolean` property:

``` oac_no_warn
<h:selectBooleanCheckbox title="#{bundle.receiveEmails}"
                         value="#{custFormBean.receiveEmails}">
</h:selectBooleanCheckbox>
<h:outputText value="#{bundle.receiveEmails}">
```

Here is an example property that can be bound to the component
represented by the example tag:

``` oac_no_warn
private boolean receiveEmails = false;
...
public void setReceiveEmails(boolean receiveEmails) {
    this.receiveEmails = receiveEmails;
}
public boolean getReceiveEmails() {
    return receiveEmails;
}
```

### 12.2.1.4 UISelectMany Properties

The `UISelectMany` component class is represented by the component tags
that begin with `h:selectMany` (for example, `h:selectManyCheckbox` and
`h:selectManyListbox`).

Because a `UISelectMany` component allows a user to select one or more
items from a list of items, this component must map to a bean property
of type `List` or `array`. This bean property represents the set of
currently selected items from the list of available items.

The following example of the `selectManyCheckbox` tag comes from
[Displaying Components for Selecting Multiple
Values](jsf-page002.htm#BNASI):

``` oac_no_warn
<h:selectManyCheckbox id="newslettercheckbox"
                      layout="pageDirection"
                      value="#{cashierBean.newsletters}">
    <f:selectItems value="#{cashierBean.newsletterItems}"/>
</h:selectManyCheckbox>
```

Here is the bean property that maps to the `value` of the
`selectManyCheckbox` tag from the preceding example:

``` oac_no_warn
private String[] newsletters;

public void setNewsletters(String[] newsletters) {
    this.newsletters = newsletters;
}
public String[] getNewsletters() {
    return this.newsletters;
}
```

The `UISelectItem` and `UISelectItems` components are used to represent
all the values in a `UISelectMany` component. See [UISelectItem
Properties](#BNAUG) and [UISelectItems Properties](#BNAUH) for
information on writing the bean properties for the `UISelectItem` and
`UISelectItems` components.

### 12.2.1.5 UISelectOne Properties

The `UISelectOne` component class is represented by the component tags
that begin with `h:selectOne` (for example, `h:selectOneRadio` and
`h:selectOneListbox`).

`UISelectOne` properties accept the same types as `UIInput` and
`UIOutput` properties, because a `UISelectOne` component represents the
single selected item from a set of items. This item can be any of the
primitive types and anything else for which you can apply a converter.

Here is an example of the `h:selectOneMenu` tag from [Displaying a Menu
Using the h:selectOneMenu Tag](jsf-page002.htm#BNASH):

``` oac_no_warn
<h:selectOneMenu id="shippingOption"
                 required="true"
                 value="#{cashierBean.shippingOption}">
    <f:selectItem itemValue="2"
                  itemLabel="#{bundle.QuickShip}"/>
    <f:selectItem itemValue="5"
                  itemLabel="#{bundle.NormalShip}"/>
    <f:selectItem itemValue="7"
                  itemLabel="#{bundle.SaverShip}"/>
 </h:selectOneMenu>
```

Here is the bean property corresponding to this tag:

``` oac_no_warn
private String shippingOption = "2";

public void setShippingOption(String shippingOption) {
    this.shippingOption = shippingOption;
}
public String getShippingOption() {
    return this.shippingOption;
}
```

Note that `shippingOption` represents the currently selected item from
the list of items in the `UISelectOne` component.

The `UISelectItem` and `UISelectItems` components are used to represent
all the values in a `UISelectOne` component. This is explained in
[Displaying a Menu Using the h:selectOneMenu
Tag](jsf-page002.htm#BNASH).

For information on how to write the managed bean properties for the
`UISelectItem` and `UISelectItems` components, see [UISelectItem
Properties](#BNAUG) and [UISelectItems Properties](#BNAUH).

### 12.2.1.6 UISelectItem Properties

A `UISelectItem` component represents a single value in a set of values
in a `UISelectMany` or a `UISelectOne` component. A `UISelectItem`
component must be bound to a managed bean property of type
`javax.faces.model.SelectItem`. A `SelectItem` object is composed of an
`Object` representing the value along with two `Strings` representing
the label and the description of the `UISelectItem` object.

The example `selectOneMenu` tag from [UISelectOne Properties](#BNAUF)
contains `selectItem` tags that set the values of the list of items in
the page. Here is an example of a bean property that can set the values
for this list in the bean:

``` oac_no_warn
SelectItem itemOne = null;

SelectItem getItemOne(){
    return itemOne;
}
void setItemOne(SelectItem item) {
    itemOne = item;
}
```

### 12.2.1.7 UISelectItems Properties

`UISelectItems` components are children of `UISelectMany` and
`UISelectOne` components. Each `UISelectItems` component is composed of
a set of either `UISelectItem` instances or any collection of objects,
such as an array, a list, or even POJOs.

The following code snippet from `CashierBean` shows how to write the
properties for `selectItems` tags containing `SelectItem` instances.

``` oac_no_warn
private String[] newsletters;
private static final SelectItem[] newsletterItems = {
    new SelectItem("Duke's Quarterly"),
    new SelectItem("Innovator's Almanac"),
    new SelectItem("Duke's Diet and Exercise Journal"),
    new SelectItem("Random Ramblings")
};
...
public void setNewsletters(String[] newsletters) {
    this.newsletters = newsletters;
}

public String[] getNewsletters() {
    return this.newsletters;
}

public SelectItem[] getNewsletterItems() {
    return newsletterItems;
}
```

Here, the `newsletters` property represents the `SelectItems` object,
whereas the `newsletterItems` property represents a static array of
`SelectItem` objects. The `SelectItem` class has several constructors;
in this example, the first argument is an `Object` representing the
value of the item, whereas the second argument is a `String`
representing the label that appears in the `UISelectMany` component on
the page.

## 12.2.2 Writing Properties Bound to Component Instances

A property bound to a component instance returns and accepts a component
instance rather than a component value. The following components bind a
component instance to a managed bean property:

``` oac_no_warn
<h:selectBooleanCheckbox id="fanClub"
                         rendered="false"
                         binding="#{cashierBean.specialOffer}" />
<h:outputLabel for="fanClub"
               rendered="false"
               binding="#{cashierBean.specialOfferText}"
               value="#{bundle.DukeFanClub}" />
</h:outputLabel>
```

The `selectBooleanCheckbox` tag renders a check box and binds the
`fanClub` `UISelectBoolean` component to the `specialOffer` property of
`CashierBean`. The `outputLabel` tag binds the value of the `value`
attribute, which represents the check box's label, to the
`specialOfferText` property of `CashierBean`. If the user orders more
than $100 worth of books and clicks the Submit button, the `submit`
method of `CashierBean` sets both components' `rendered` properties to
`true`, causing the check box and label to display when the page is
re-rendered.

Because the components corresponding to the example tags are bound to
the managed bean properties, these properties must match the components'
types. This means that the `specialOfferText` property must be of type
`UIOutput`, and the `specialOffer` property must be of type
`UISelectBoolean`:

``` oac_no_warn
UIOutput specialOfferText = null;
UISelectBoolean specialOffer = null;

public UIOutput getSpecialOfferText() {
    return this.specialOfferText;
}
public void setSpecialOfferText(UIOutput specialOfferText) {
    this.specialOfferText = specialOfferText;
}

public UISelectBoolean getSpecialOffer() {
    return this.specialOffer;
}
public void setSpecialOffer(UISelectBoolean specialOffer) {
    this.specialOffer = specialOffer;
}
```

For more general information on component binding, see [Managed Beans in
JavaServer Faces Technology](jsf-develop001.htm#BNAQM).

For information on how to reference a managed bean method that performs
navigation when a button is clicked, see [Referencing a Method That
Performs Navigation](jsf-page-core004.htm#BNATP).

For more information on writing managed bean methods that handle
navigation, see [Writing a Method to Handle
Navigation](jsf-develop003.htm#BNAVC).

## 12.2.3 Writing Properties Bound to Converters, Listeners, or Validators

All the standard converter, listener, and validator tags included with
JavaServer Faces technology support binding attributes that allow you to
bind converter, listener, or validator implementations to managed bean
properties.

The following example shows a standard `convertDateTime` tag using a
value expression with its `binding` attribute to bind the
`javax.faces.convert.DateTimeConverter` instance to the `convertDate`
property of `LoginBean`:

``` oac_no_warn
<h:inputText value="#{loginBean.birthDate}">
    <f:convertDateTime binding="#{loginBean.convertDate}" />
</h:inputText>
```

The `convertDate` property must therefore accept and return a
`DateTimeConverter` object, as shown here:

``` oac_no_warn
private DateTimeConverter convertDate;
public DateTimeConverter getConvertDate() {
       ...
    return convertDate;
}
public void setConvertDate(DateTimeConverter convertDate) {
    convertDate.setPattern("EEEEEEEE, MMM dd, yyyy");
    this.convertDate = convertDate;
}
```

Because the converter is bound to a managed bean property, the managed
bean property can modify the attributes of the converter or add new
functionality to it. In the case of the preceding example, the property
sets the date pattern that the converter uses to parse the user's input
into a `Date` object.

The managed bean properties that are bound to validator or listener
implementations are written in the same way and have the same general
purpose.

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
<td><a href="jsf-develop001.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="jsf-develop003.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
