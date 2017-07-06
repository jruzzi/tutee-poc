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
<td><a href="dukes-forest003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 59.4 Running the Duke's Forest Application

Running the Duke's Forest application involves several tasks:

  - Registering as a customer of Duke's Store

  - As a customer, purchasing products

  - As an administrator, approving or denying shipment of a product

  - As an administrator, creating a new product, customer, group, or
    category

The following topics are addressed here:

  - [Section 59.4.1, "To Register as a Duke's Store
    Customer"](#CHDBDEHH)

  - [Section 59.4.2, "To Purchase Products"](#CHDCEJIC)

  - [Section 59.4.3, "To Approve Shipment of a Product"](#CHDICAIJ)

  - [Section 59.4.4, "To Create a New Product"](#CHDIFEGC)

## 59.4.1 To Register as a Duke's Store Customer

1.  In a web browser, enter the following URL:
    
    ``` oac_no_warn
    http://localhost:8080/dukes-store
    ```
    
    The Duke's Forest - Store page opens.

2.  Click Sign Up at the top of the page.

3.  Fill in the form fields, then click Save.
    
    All fields are required, and the Password value must be at least 7
    characters in length.

## 59.4.2 To Purchase Products

1.  To log in as the user you created, or as one of two users already in
    the database, enter the user name and password and click Log In.
    
    The preexisting users have the user names `jack@example.com` and
    `robert@example.com`, and they both have the same password, `1234`.

2.  Click Products in the left sidebar.

3.  On the page that appears, click one of the categories (Plants, Food,
    Services, or Tools).

4.  Choose a product and click Add to Cart.
    
    You can order only one of any one product, but you can order
    multiple different products in multiple categories. The products and
    a running total appear in the Shopping Cart in the left sidebar.

5.  When you have finished choosing products, click Checkout.
    
    A message appears: "Your order is being processed. Check the Orders
    page to see the status of your order."

6.  Click Orders in the left sidebar to verify your order.
    
    If the total of the order exceeds $1,000, the status of the order is
    "Order cancelled," because the Payment web service denies orders
    over that limit. Otherwise, the status is "Ready to ship."

7.  When you have finished placing orders, click Logout at the top of
    the page.

## 59.4.3 To Approve Shipment of a Product

1.  Log in to Duke's Store as an administrator.
    
    Your user name is `admin@example.com`, and your password is `1234`.
    
    The main administration page allows you to view categories,
    customers, administrators, groups, products, and orders, and to
    create new objects of all types except orders.

2.  At the bottom of the page, click Approve Shipment.
    
    This action takes you to Duke's Shipment, retaining your
    administrator login.

3.  On the Pending list, click Approve to approve an order and move it
    to the Shipped area of the page.
    
    If you click Deny, the order disappears from the page. If you log in
    to Duke's Store again as the customer, it will appear in the Orders
    list as "Order cancelled."

To return to Duke's Store from Duke's Shipment, click Return to Duke's
Store.

## 59.4.4 To Create a New Product

You can create other kinds of objects as well as products. Creating
products is more complex than the other creation processes, so it is
described here.

1.  Log in to Duke's Store as an administrator.

2.  On the main administration page, click Create New Product.

3.  Enter values in the Name, Price, and Description fields.

4.  Select a category, then click Next.

5.  On the Upload the Product Image page, click Browse to locate an
    image on your file system using a file chooser.

6.  Click Next.

7.  On the next page, view the product fields, then click Done.

8.  Click Products in the left sidebar, then click the category to
    verify that the product has been added.

9.  Click Administration at the top of the page to return to the main
    administration page, or click Logout to log out.

-----

<table style="width:66%;">
<colgroup>
<col width="33%" />
<col width="0%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><table style="width:48%;">
<colgroup>
<col width="0%" />
<col width="48%" />
</colgroup>
<tbody>
<tr class="odd">
<td> </td>
<td><a href="dukes-forest003.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
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
