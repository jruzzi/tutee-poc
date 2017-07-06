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
<td><a href="security-advanced004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-advanced006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 50.5 Securing Application Clients

The Java EE authentication requirements for application clients are the
same as for other Java EE components, and the same authentication
techniques can be used as for other Java EE application components. No
authentication is necessary when accessing unprotected web resources.

When accessing protected web resources, the usual varieties of
authentication can be used: HTTP basic authentication, HTTP login-form
authentication, or SSL client authentication. [Specifying an
Authentication Mechanism in the Deployment
Descriptor](security-webtier002.htm#BNCBN) describes how to specify HTTP
basic authentication and HTTP login-form authentication. [Client
Authentication](security-advanced002.htm#GLIEQ) describes how to specify
SSL client authentication.

Authentication is required when accessing protected enterprise beans.
The authentication mechanisms for enterprise beans are discussed in
[Securing Enterprise Beans](security-javaee002.htm#BNBYL).

An application client makes use of an authentication service provided by
the application client container for authenticating its users. The
container's service can be integrated with the native platform's
authentication system so that a single sign-on capability is used. The
container can authenticate the user either when the application is
started or when a protected resource is accessed.

An application client can provide a class, called a login module, to
gather authentication data. If so, the
`javax.security.auth.callback.CallbackHandler` interface must be
implemented, and the class name must be specified in its deployment
descriptor. The application's callback handler must fully support
`Callback` objects specified in the `javax.security.auth.callback`
package.

## 50.5.1 Using Login Modules

An application client can use the Java Authentication and Authorization
Service (JAAS) to create login modules for authentication. A JAAS-based
application implements the
`javax.security.auth.callback.CallbackHandler` interface so that it can
interact with users to enter specific authentication data, such as user
names or passwords, or to display error and warning messages.

Applications implement the `CallbackHandler` interface and pass it to
the login context, which forwards it directly to the underlying login
modules. A login module uses the callback handler both to gather input,
such as a password or smart card PIN, from users and to supply
information, such as status information, to users. Because the
application specifies the callback handler, an underlying login module
can remain independent of the various ways applications interact with
users.

For example, the implementation of a callback handler for a GUI
application might display a window to solicit user input, or the
implementation of a callback handler for a command-line tool might
simply prompt the user for input directly from the command line.

The login module passes an array of appropriate callbacks to the
callback handler's `handle` method, such as a `NameCallback` for the
user name and a `PasswordCallback` for the password; the callback
handler performs the requested user interaction and sets appropriate
values in the callbacks. For example, to process a `NameCallback`, the
`CallbackHandler` might prompt for a name, retrieve the value from the
user, and call the `setName` method of the `NameCallback` to store the
name.

For more information on using JAAS for authentication in login modules,
refer to the documentation listed in [Further Information about Advanced
Security Topics](security-advanced008.htm#BABBGBBF).

## 50.5.2 Using Programmatic Login

Programmatic login enables the client code to supply user credentials.
If you are using an EJB client, you can use the
`com.sun.appserv.security.ProgrammaticLogin` class with its convenient
`login` and `logout` methods. Programmatic login is specific to a
server.

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
<td><a href="security-advanced004.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-advanced006.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
