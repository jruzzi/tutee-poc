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
<td><a href="security-intro.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-intro002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 47.1 Overview of Java EE Security

Every enterprise that has either sensitive resources that can be
accessed by many users or resources that traverse unprotected, open
networks, such as the Internet, needs to be protected.

Enterprise tier and web tier applications are made up of components that
are deployed into various containers. These components are combined to
build a multitier enterprise application. Security for components is
provided by their containers. A container provides two kinds of
security: declarative and programmatic.

  - Declarative security expresses an application component's security
    requirements by using either deployment descriptors or annotations.
    
    A deployment descriptor is an XML file that is external to the
    application and that expresses an application's security structure,
    including security roles, access control, and authentication
    requirements. For more information about deployment descriptors,
    read [Using Deployment Descriptors for Declarative
    Security](security-intro003.htm#BNBXF).
    
    Annotations, also called metadata, are used to specify information
    about security within a class file. When the application is
    deployed, this information can be either used by or overridden by
    the application deployment descriptor. Annotations save you from
    having to write declarative information inside XML descriptors.
    Instead, you simply put annotations on the code, and the required
    information gets generated. For this tutorial, annotations are used
    for securing applications wherever possible. For more information
    about annotations, see [Using Annotations to Specify Security
    Information](security-intro003.htm#BNBXG).

  - Programmatic security is embedded in an application and is used to
    make security decisions. Programmatic security is useful when
    declarative security alone is not sufficient to express the security
    model of an application. For more information about programmatic
    security, read [Using Programmatic
    Security](security-intro003.htm#BNBXH).

More information on these concepts and mechanisms can be found in the
chapter on security in the Java EE 7 specification.

Other chapters in this Part discuss security requirements in web tier
and enterprise tier applications.

  - [Chapter 48, "Getting Started Securing Web
    Applications"](security-webtier.htm#BNCAS) explains how to add
    security to web components, such as servlets.

  - [Chapter 49, "Getting Started Securing Enterprise
    Applications"](security-javaee.htm#BNBYK) explains how to add
    security to Java EE components, such as enterprise beans and
    application clients.

## 47.1.1 A Simple Application Security Walkthrough

The security behavior of a Java EE environment may be better understood
by examining what happens in a simple application with a web client, a
user interface, and enterprise bean business logic.

In the following example, which is taken from the Java EE 7
Specification, the web client relies on the web server to act as its
authentication proxy by collecting user authentication data from the
client and using it to establish an authenticated session.

### 47.1.1.1 Step 1: Initial Request

In the first step of this example, the web client requests the main
application URL. This action is shown in [Figure 47-1](#BNBWN).

Figure 47-1 Initial Request

![Description of Figure 47-1 follows](img/jeett_dt_039.png)  
[Description of "Figure 47-1 Initial
Request"](img_text/jeett_dt_039.htm)  
  

Since the client has not yet authenticated itself to the application
environment, the server responsible for delivering the web portion of
the application, hereafter referred to as the web server, detects this
and invokes the appropriate authentication mechanism for this resource.
For more information on these mechanisms, see [Security
Mechanisms](security-intro002.htm#BNBWY).

### 47.1.1.2 Step 2: Initial Authentication

The web server returns a form that the web client uses to collect
authentication data, such as user name and password, from the user. The
web client forwards the authentication data to the web server, where it
is validated by the web server, as shown in [Figure 47-2](#BNBWP). The
validation mechanism may be local to a server or may leverage the
underlying security services. On the basis of the validation, the web
server sets a credential for the user.

Figure 47-2 Initial Authentication

![Description of Figure 47-2 follows](img/jeett_dt_040.png)  
[Description of "Figure 47-2 Initial
Authentication"](img_text/jeett_dt_040.htm)  
  

### 47.1.1.3 Step 3: URL Authorization

The credential is used for future determinations of whether the user is
authorized to access restricted resources it may request. The web server
consults the security policy associated with the web resource to
determine the security roles that are permitted access to the resource.
The security policy is derived from annotations or from the deployment
descriptor. The web container then tests the user's credential against
each role to determine whether it can map the user to the role. [Figure
47-3](#BNBWR) shows this process.

Figure 47-3 URL Authorization

![Description of Figure 47-3 follows](img/jeett_dt_041.png)  
[Description of "Figure 47-3 URL
Authorization"](img_text/jeett_dt_041.htm)  
  

The web server's evaluation stops with an "is authorized" outcome when
the web server is able to map the user to a role. A "not authorized"
outcome is reached if the web server is unable to map the user to any of
the permitted roles.

### 47.1.1.4 Step 4: Fulfilling the Original Request

If the user is authorized, the web server returns the result of the
original URL request, as shown in [Figure 47-4](#BNBWT).

Figure 47-4 Fulfilling the Original Request

![Description of Figure 47-4 follows](img/jeett_dt_042.png)  
[Description of "Figure 47-4 Fulfilling the Original
Request"](img_text/jeett_dt_042.htm)  
  

In our example, the response URL of a web page is returned, enabling the
user to post form data that needs to be handled by the business-logic
component of the application. See [Chapter 48, "Getting Started Securing
Web Applications"](security-webtier.htm#BNCAS) for more information on
protecting web applications.

### 47.1.1.5 Step 5: Invoking Enterprise Bean Business Methods

The web page performs the remote method call to the enterprise bean,
using the user's credential to establish a secure association between
the web page and the enterprise bean, as shown in [Figure 47-5](#BNBWV).
The association is implemented as two related security contexts: one in
the web server and one in the EJB container.

Figure 47-5 Invoking an Enterprise Bean Business Method

![Description of Figure 47-5 follows](img/jeett_dt_043.png)  
[Description of "Figure 47-5 Invoking an Enterprise Bean Business
Method"](img_text/jeett_dt_043.htm)  
  

The EJB container is responsible for enforcing access control on the
enterprise bean method. The container consults the security policy
associated with the enterprise bean to determine the security roles that
are permitted access to the method. The security policy is derived from
annotations or from the deployment descriptor. For each role, the EJB
container determines whether it can map the caller to the role by using
the security context associated with the call.

The container's evaluation stops with an "is authorized" outcome when
the container is able to map the caller's credential to a role. A "not
authorized" outcome is reached if the container is unable to map the
caller to any of the permitted roles. A "not authorized" result causes
an exception to be thrown by the container and propagated back to the
calling web page.

If the call is authorized, the container dispatches control to the
enterprise bean method. The result of the bean's execution of the call
is returned to the web page and ultimately to the user by the web server
and the web client.

## 47.1.2 Features of a Security Mechanism

A properly implemented security mechanism will provide the following
functionality:

  - Prevent unauthorized access to application functions and business or
    personal data (authentication)

  - Hold system users accountable for operations they perform
    (non-repudiation)

  - Protect a system from service interruptions and other breaches that
    affect quality of service

Ideally, properly implemented security mechanisms will also be

  - Easy to administer

  - Transparent to system users

  - Interoperable across application and enterprise boundaries

## 47.1.3 Characteristics of Application Security

Java EE applications consist of components that can contain both
protected and unprotected resources. Often, you need to protect
resources to ensure that only authorized users have access.
Authorization provides controlled access to protected resources.
Authorization is based on identification and authentication.
Identification is a process that enables recognition of an entity by a
system, and authentication is a process that verifies the identity of a
user, device, or other entity in a computer system, usually as a
prerequisite to allowing access to resources in a system.

Authorization and authentication are not required for an entity to
access unprotected resources. Accessing a resource without
authentication is referred to as unauthenticated, or anonymous, access.

The characteristics of application security that, when properly
addressed, help to minimize the security threats faced by an enterprise
include the following.

  - Authentication: The means by which communicating entities, such as
    client and server, prove to each other that they are acting on
    behalf of specific identities that are authorized for access. This
    ensures that users are who they say they are.

  - Authorization, or access control: The means by which interactions
    with resources are limited to collections of users or programs for
    the purpose of enforcing integrity, confidentiality, or availability
    constraints. This ensures that users have permission to perform
    operations or access data.

  - Data integrity: The means used to prove that information has not
    been modified by a third party, an entity other than the source of
    the information. For example, a recipient of data sent over an open
    network must be able to detect and discard messages that were
    modified after they were sent. This ensures that only authorized
    users can modify data.

  - Confidentiality, or data privacy: The means used to ensure that
    information is made available only to users who are authorized to
    access it. This ensures that only authorized users can view
    sensitive data.

  - Non-repudiation: The means used to prove that a user who performed
    some action cannot reasonably deny having done so. This ensures that
    transactions can be proved to have happened.

  - Quality of Service: The means used to provide better service to
    selected network traffic over various technologies.

  - Auditing: The means used to capture a tamper-resistant record of
    security-related events for the purpose of being able to evaluate
    the effectiveness of security policies and mechanisms. To enable
    this, the system maintains a record of transactions and security
    information.

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
<td><a href="security-intro.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-intro002.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
