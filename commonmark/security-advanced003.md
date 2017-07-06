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
<td><a href="security-advanced002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-advanced004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 50.3 Using the JDBC Realm for User Authentication

An authentication realm, sometimes called a security policy domain or
security domain, is a scope over which an application server defines and
enforces a common security policy. A realm contains a collection of
users, who may or may not be assigned to a group. GlassFish Server comes
preconfigured with the file, certificate, and administration realms. An
administrator can also set up LDAP, JDBC, digest, or custom realms.

An application can specify in its deployment descriptor which realm to
use. If the application does not specify a realm, GlassFish Server uses
its default realm, the `file` realm. If an application specifies that a
JDBC realm is to be used for user authentication, GlassFish Server will
retrieve user credentials from a database. The application server uses
the database information and the enabled JDBC realm option in the
configuration file.

A database provides an easy way to add, edit, or delete users at runtime
and enables users to create their own accounts without any
administrative assistance. Using a database has an additional benefit:
providing a place to securely store any extra user information. A realm
can be thought of as a database of user names and passwords that
identify valid users of a web application or set of web applications
with an enumeration of the list of roles associated with each valid
user. Access to specific web application resources is granted to all
users in a particular role, instead of enumerating a list of associated
users. A user name can have any number of roles associated with it.

Two of the tutorial case studies, [Chapter 58, "Duke's Tutoring Case
Study Example,"](dukes-tutoring.htm#GKAEE) and [Chapter 59, "Duke's
Forest Case Study Example,"](dukes-forest.htm#GLNPW) use a JDBC realm
for user authentication.

## 50.3.1 To Configure a JDBC Authentication Realm

GlassFish Server enables administrators to specify a user's credentials
(user name and password) in the JDBC realm instead of in the connection
pool. This prevents other applications from browsing the database tables
for user credentials. By default, storing passwords as clear text is not
supported in the JDBC realm. Under normal circumstances, passwords
should not be stored as clear text.

1.  Create the database tables in which user credentials for the realm
    will be stored.

2.  Add user credentials to the database tables you created.

3.  Create a JDBC connection pool for the database.
    
    You can use the Administration Console or the command line to create
    a connection pool.

4.  Create a JDBC resource for the database.
    
    You can use the Administration Console or the command line to create
    a JDBC resource.

5.  Create a realm.
    
    This step needs to associate the resource with the realm, define the
    tables and columns for users and groups used for authentication, and
    define the digest algorithm that will be used for storing passwords
    in the database.
    
    You can use the Administration Console or the command line to create
    a realm.

6.  Modify the deployment descriptor for your application to specify the
    JDBC realm.
    
      - For an enterprise application in an EAR file, modify the
        `glassfish-application.xml` file.
    
      - For a web application in a WAR file, modify the `web.xml` file.
    
      - For an enterprise bean in an EJB JAR file, modify the
        `glassfish-ejb-jar.xml` file.
    
    For example, for a hypothetical application, the `web.xml` file
    could specify the `jdbcRealm` realm, as follows:
    
    ``` oac_no_warn
    <login-config>
        <auth-method>FORM</auth-method>
        <realm-name>jdbcRealm</realm-name>
        <form-login-config>
            <form-login-page>/login.xhtml</form-login-page>
            <form-error-page>/login.xhtml</form-error-page>
        </form-login-config>
    </login-config>
    <security-constraint>
        <web-resource-collection>
            <web-resource-name>Secure Pages</web-resource-name>
            <description/>
            <url-pattern>/admin/*</url-pattern>
        </web-resource-collection>
        <auth-constraint>
            <role-name>ADMINS</role-name>
        </auth-constraint>
    </security-constraint>
    ```
    
    Form-based login is specified for all web pages under `/admin`.
    Access to those pages will be allowed only to users in the `ADMINS`
    role.

7.  Assign security roles to users or groups of users in the realm.
    
    To assign a security role to a group or to a user, add a
    security-role-mapping element to the application server-specific
    deployment descriptor, in this case `glassfish-web.xml`:
    
    ``` oac_no_warn
    <security-role-mapping>
        <role-name>USERS</role-name>
        <group-name>USERS</group-name>
    </security-role-mapping>
    <security-role-mapping>
        <role-name>ADMINS</role-name>
        <group-name>ADMINS</group-name>
    </security-role-mapping>
    ```
    
    Since GlassFish Server users are assigned to groups during the user
    creation process, this is more efficient than mapping security roles
    to individual users.

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
<td><a href="security-advanced002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="security-advanced004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
