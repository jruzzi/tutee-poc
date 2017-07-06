++++
<table cellspacing="0" cellpadding="0" width="100%">
<tr>
<td align="left" valign="top"><b>Java Platform, Enterprise Edition The Java EE Tutorial</b><br />
<b>Release 7 Java Platform, Enterprise Edition</b><br />
E39031-02</td>
<td valign="bottom" align="right">
<table cellspacing="0" cellpadding="0" width="225">
<tr>
<td>&nbsp;</td>
<td align="center" valign="top"><a href="toc.md"><img src="img/toc.gif" alt="Go To Table Of Contents" /><br />
<span class="icon">Contents</span></a></td>
</tr>
</table>
</td>
</tr>
</table>
<hr />
<table cellspacing="0" cellpadding="0" width="100">
<tr>
<td align="center"><a href="overview005.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a>&nbsp;</td>
<td align="center"><a href="overview007.md"><img src="img/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td>&nbsp;</td>
</tr>
</table>
++++
[[BNABS]]

[[JEETT00310]]
[[web-services-support]]
1.6 Web Services Support
------------------------

Web services are web-based enterprise applications that use open,
XML-based standards and transport protocols to exchange data with
calling clients. The Java EE platform provides the XML APIs and tools
you need to quickly design, develop, test, and deploy web services and
clients that fully interoperate with other web services and clients
running on Java-based or non-Java-based platforms.

To write web services and clients with the Java EE XML APIs, all you
need to do is pass parameter data to the method calls and process the
data returned; for document-oriented web services, you send documents
containing the service data back and forth. No low-level programming is
needed because the XML API implementations do the work of translating
the application data to and from an XML-based data stream that is sent
over the standardized XML-based transport protocols. These XML-based
standards and protocols are introduced in the following sections.

The translation of data to a standardized XML-based data stream is what
makes web services and clients written with the Java EE XML APIs fully
interoperable. This does not necessarily mean that the data being
transported includes XML tags, because the transported data can itself
be plain text, XML data, or any kind of binary data, such as audio,
video, maps, program files, computer-aided design (CAD) documents, and
the like. The next section introduces XML and explains how parties doing
business can use XML tags and schemas to exchange data in a meaningful
way.

[[BNABT]]

[[JEETT00851]]
[[xml]]
1.6.1 XML
~~~~~~~~~

Extensible Markup Language (XML) is a cross-platform, extensible,
text-based standard for representing data. Parties that exchange XML
data can create their own tags to describe the data, set up schemas to
specify which tags can be used in a particular kind of XML document, and
use XML style sheets to manage the display and handling of the data.

For example, a web service can use XML and a schema to produce price
lists, and companies that receive the price lists and schema can have
their own style sheets to handle the data in a way that best suits their
needs. Here are examples.

* One company might put XML pricing information through a program to
translate the XML into HTML so that it can post the price lists to its
intranet.
* A partner company might put the XML pricing information through a tool
to create a marketing presentation.
* Another company might read the XML pricing information into an
application for processing.

[[BNABU]]

[[JEETT00852]]
[[soap-transport-protocol]]
1.6.2 SOAP Transport Protocol
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Client requests and web service responses are transmitted as Simple
Object Access Protocol (SOAP) messages over HTTP to enable a completely
interoperable exchange between clients and web services, all running on
different platforms and at various locations on the Internet. HTTP is a
familiar request-and-response standard for sending messages over the
Internet, and SOAP is an XML-based protocol that follows the HTTP
request-and-response model.

The SOAP portion of a transported message does the following:

* Defines an XML-based envelope to describe what is in the message and
explain how to process the message
* Includes XML-based encoding rules to express instances of
application-defined data types within the message
* Defines an XML-based convention for representing the request to the
remote service and the resulting response

[[BNABV]]

[[JEETT00853]]
[[wsdl-standard-format]]
1.6.3 WSDL Standard Format
~~~~~~~~~~~~~~~~~~~~~~~~~~

The Web Services Description Language (WSDL) is a standardized XML
format for describing network services. The description includes the
name of the service, the location of the service, and ways to
communicate with the service. WSDL service descriptions can be published
on the Web. GlassFish Server provides a tool for generating the WSDL
specification of a web service that uses remote procedure calls to
communicate with clients.

++++
<hr />
<table cellspacing="0" cellpadding="0" width="100%">
<col width="33%" />
<col width="*" />
<col width="33%" />
<tr>
<td valign="bottom">
<table cellspacing="0" cellpadding="0" width="100">
<col width="*" />
<col width="48%" />
<col width="48%" />
<tr>
<td>&nbsp;</td>
<td align="center"><a href="overview005.md"><img src="img/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a>&nbsp;</td>
<td align="center"><a href="overview007.md"><img src="img/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
</tr>
</table>
</td>
<td><img src="img/oracle.gif" alt="Oracle Logo" /> <a href="img/cpyr.md"><br />
<span>Copyright&nbsp;&copy;&nbsp;2014,&nbsp;Oracle&nbsp;and/or&nbsp;its&nbsp;affiliates.&nbsp;All&nbsp;rights&nbsp;reserved.</a><br>
ORACLE&nbsp;CONFIDENTIAL.&nbsp;For&nbsp;authorized&nbsp;use&nbsp;only.&nbsp;Do&nbsp;not&nbsp;distribute&nbsp;to&nbsp;third&nbsp;parties.</span></td>
<td valign="bottom" align="right">
<table cellspacing="0" cellpadding="0" width="225">
<tr>
<td>&nbsp;</td>
<td align="center" valign="top"><a href="toc.md"><img src="img/toc.gif" alt="Go To Table Of Contents" /><br />
<span>Contents</span></a></td>
</tr>
</table>
</td>
</tr>
</table>
<p align="center"></p>
++++