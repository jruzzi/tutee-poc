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
<td><a href="title.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

# Contents

Beta Draft: 2017-06-12

## [Title and Copyright Information](title.htm)

## [Preface](preface.htm#GEXAF)

  - [Audience](preface.htm#CIACGIBD)
  - [Documentation Accessibility](preface.htm#CIAHFICG)
  - [Before You Read This Book](preface.htm#BNAAC)
  - [Related Documentation](preface.htm#GIPRL)
  - [Conventions](preface.htm#GKVTF)
  - [Default Paths and File Names](preface.htm#GFIRK)

## [Part I Introduction](partintro.htm#GFIRP)

## [1 Overview](overview.htm#BNAAW)

  - [1.1 Introduction to Java EE](overview001.htm#A1046550)
  - [1.2 Java EE 7 Platform Highlights](overview002.htm#GIQVH)
  - [1.3 Java EE Application Model](overview003.htm#BNAAX)
  - [1.4 Distributed Multitiered Applications](overview004.htm#BNAAY)
      - [1.4.1 Security](overview004.htm#BNABA)
      - [1.4.2 Java EE Components](overview004.htm#BNABB)
      - [1.4.3 Java EE Clients](overview004.htm#BNABC)
          - [1.4.3.1 Web Clients](overview004.htm#BNABD)
          - [1.4.3.2 Application Clients](overview004.htm#BNABF)
          - [1.4.3.3 Applets](overview004.htm#BNABE)
          - [1.4.3.4 The JavaBeans Component
            Architecture](overview004.htm#BNABG)
          - [1.4.3.5 Java EE Server
            Communications](overview004.htm#BNABH)
      - [1.4.4 Web Components](overview004.htm#BNABJ)
      - [1.4.5 Business Components](overview004.htm#BNABK)
      - [1.4.6 Enterprise Information System
        Tier](overview004.htm#BNABL)
  - [1.5 Java EE Containers](overview005.htm#BNABO)
      - [1.5.1 Container Services](overview005.htm#BNABP)
      - [1.5.2 Container Types](overview005.htm#BNABQ)
  - [1.6 Web Services Support](overview006.htm#BNABS)
      - [1.6.1 XML](overview006.htm#BNABT)
      - [1.6.2 SOAP Transport Protocol](overview006.htm#BNABU)
      - [1.6.3 WSDL Standard Format](overview006.htm#BNABV)
  - [1.7 Java EE Application Assembly and
    Deployment](overview007.htm#BNABX)
  - [1.8 Java EE 7 APIs](overview008.htm#BNACJ)
      - [1.8.1 Enterprise JavaBeans Technology](overview008.htm#BNACL)
      - [1.8.2 Java Servlet Technology](overview008.htm#BNACM)
      - [1.8.3 JavaServer Faces Technology](overview008.htm#BNACP)
      - [1.8.4 JavaServer Pages Technology](overview008.htm#BNACN)
      - [1.8.5 JavaServer Pages Standard Tag
        Library](overview008.htm#BNACO)
      - [1.8.6 Java Persistence API](overview008.htm#BNADB)
      - [1.8.7 Java Transaction API](overview008.htm#BNACR)
      - [1.8.8 Java API for RESTful Web Services](overview008.htm#GIRBT)
      - [1.8.9 Managed Beans](overview008.htm#GJXSD)
      - [1.8.10 Contexts and Dependency Injection for Java
        EE](overview008.htm#GJXVO)
      - [1.8.11 Dependency Injection for Java](overview008.htm#GJXVG)
      - [1.8.12 Bean Validation](overview008.htm#GJXTY)
      - [1.8.13 Java Message Service API](overview008.htm#BNACQ)
      - [1.8.14 Java EE Connector Architecture](overview008.htm#BNACZ)
      - [1.8.15 JavaMail API](overview008.htm#BNACS)
      - [1.8.16 Java Authorization Contract for
        Containers](overview008.htm#GIRBE)
      - [1.8.17 Java Authentication Service Provider Interface for
        Containers](overview008.htm#GIRGP)
      - [1.8.18 Java API for WebSocket](overview008.htm#CJAHDJBJ)
      - [1.8.19 Java API for JSON Processing](overview008.htm#CJAGIEEI)
      - [1.8.20 Concurrency Utilities for Java
        EE](overview008.htm#CJAFGFCJ)
      - [1.8.21 Batch Applications for the Java
        Platform](overview008.htm#CJAJHGIH)
  - [1.9 Java EE 7 APIs in the Java Platform, Standard Edition
    7](overview009.htm#GIRDR)
      - [1.9.1 Java Database Connectivity API](overview009.htm#BNADA)
      - [1.9.2 Java Naming and Directory Interface
        API](overview009.htm#BNADC)
      - [1.9.3 JavaBeans Activation Framework](overview009.htm#BNACT)
      - [1.9.4 Java API for XML Processing](overview009.htm#BNACU)
      - [1.9.5 Java Architecture for XML Binding](overview009.htm#BNACW)
      - [1.9.6 Java API for XML Web Services](overview009.htm#BNACV)
      - [1.9.7 SOAP with Attachments API for
        Java](overview009.htm#BNACX)
      - [1.9.8 Java Authentication and Authorization
        Service](overview009.htm#BNADD)
      - [1.9.9 Common Annotations for the Java
        Platform](overview009.htm#sthref12)
  - [1.10 GlassFish Server Tools](overview010.htm#BNADF)

## [2 Using the Tutorial Examples](usingexamples.htm#GFIUD)

  - [2.1 Required Software](usingexamples001.htm#GEXAJ)
      - [2.1.1 Java Platform, Standard
        Edition](usingexamples001.htm#GEXAE)
      - [2.1.2 Java EE 7 Software Development
        Kit](usingexamples001.htm#GEXAB)
          - [2.1.2.1 SDK Installation Tips](usingexamples001.htm#GEXBC)
      - [2.1.3 Java EE 7 Tutorial Component](usingexamples001.htm#GEXBA)
      - [2.1.4 NetBeans IDE](usingexamples001.htm#GEXAZ)
          - [2.1.4.1 To Install NetBeans IDE without GlassFish
            Server](usingexamples001.htm#GJSEQ)
          - [2.1.4.2 To Add GlassFish Server as a Server Using NetBeans
            IDE](usingexamples001.htm#GIQZL)
      - [2.1.5 Apache Maven](usingexamples001.htm#GEXAA)
  - [2.2 Starting and Stopping GlassFish
    Server](usingexamples002.htm#BNADI)
      - [2.2.1 To Start GlassFish Server Using NetBeans
        IDE](usingexamples002.htm#CHDCACDI)
      - [2.2.2 To Stop GlassFish Server Using NetBeans
        IDE](usingexamples002.htm#sthref14)
      - [2.2.3 To Start GlassFish Server Using the Command
        Line](usingexamples002.htm#CHDBDDAF)
      - [2.2.4 To Stop GlassFish Server Using the Command
        Line](usingexamples002.htm#sthref15)
  - [2.3 Starting the Administration
    Console](usingexamples003.htm#BNADJ)
      - [2.3.1 To Start the Administration Console Using NetBeans
        IDE](usingexamples003.htm#GJKST)
  - [2.4 Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK)
      - [2.4.1 To Start the Database Server Using NetBeans
        IDE](usingexamples004.htm#GJSFS)
  - [2.5 Building the Examples](usingexamples005.htm#BNAAN)
  - [2.6 Tutorial Example Directory
    Structure](usingexamples006.htm#GEXAP)
  - [2.7 Java EE 7 Maven Archetypes in the
    Tutorial](usingexamples007.htm#CIHBHEFF)
      - [2.7.1 Installing the Tutorial
        Archetypes](usingexamples007.htm#CHDJGCCA)
          - [2.7.1.1 Installing the Tutorial Archetypes Using NetBeans
            IDE](usingexamples007.htm#sthref16)
          - [2.7.1.2 Installing the Tutorial Archetypes Using
            Maven](usingexamples007.htm#sthref17)
  - [2.8 Getting the Latest Updates to the
    Tutorial](usingexamples008.htm#GIQWR)
      - [2.8.1 To Update the Tutorial Using NetBeans
        IDE](usingexamples008.htm#GIQYK)
      - [2.8.2 To Update the Tutorial Using the Command
        Line](usingexamples008.htm#sthref18)
  - [2.9 Debugging Java EE Applications](usingexamples009.htm#BNADL)
      - [2.9.1 Using the Server Log](usingexamples009.htm#BNADM)
          - [2.9.1.1 To Use the Administration Console Log
            Viewer](usingexamples009.htm#GJSGH)
      - [2.9.2 Using a Debugger](usingexamples009.htm#BNADN)
          - [2.9.2.1 To Debug an Application Using a
            Debugger](usingexamples009.htm#GJQWL)

## [Part II Platform Basics](partplatform.htm#GFIRP2)

## [3 Resource Creation](resource-creation.htm#GKJIQ2)

  - [3.1 Resources and JNDI Naming](resource-creation001.htm#BNCJI)
  - [3.2 DataSource Objects and Connection
    Pools](resource-creation002.htm#BNCJJ)
  - [3.3 Creating Resources
    Administratively](resource-creation003.htm#CACFBGBE)

## [4 Injection](injection.htm#GKJIQ3)

  - [4.1 Resource Injection](injection001.htm#BABHDCAI)
  - [4.2 Dependency Injection](injection002.htm#BABDJGIE)
  - [4.3 The Main Differences between Resource Injection and Dependency
    Injection](injection003.htm#BABHFECJ)

## [5 Packaging](packaging.htm#GKJIQ4)

  - [5.1 Packaging Applications](packaging001.htm#BCGDJDFB)
  - [5.2 Packaging Enterprise Beans](packaging002.htm#BCGECBIJ)
      - [5.2.1 Packaging Enterprise Beans in EJB JAR
        Modules](packaging002.htm#CHDFCDBG)
      - [5.2.2 Packaging Enterprise Beans in WAR
        Modules](packaging002.htm#CHDJABEJ)
  - [5.3 Packaging Web Archives](packaging003.htm#BCGHAHGD)
  - [5.4 Packaging Resource Adapter Archives](packaging004.htm#BCGDHBHJ)

## [Part III The Web Tier](partwebtier.htm#BNADP)

## [6 Getting Started with Web Applications](webapp.htm#BNADR)

  - [6.1 Web Applications](webapp001.htm#GEYSJ)
  - [6.2 Web Application Lifecycle](webapp002.htm#BNADU)
  - [6.3 A Web Module That Uses JavaServer Faces Technology: The hello1
    Example](webapp003.htm#BNADX)
      - [6.3.1 To View the hello1 Web Module Using NetBeans
        IDE](webapp003.htm#GJWTV)
          - [6.3.1.1 Introduction to Scopes](webapp003.htm#GLQLK)
      - [6.3.2 Packaging and Deploying the hello1 Web
        Module](webapp003.htm#BNADZ)
          - [6.3.2.1 To Build and Package the hello1 Web Module Using
            NetBeans IDE](webapp003.htm#GJRGN)
          - [6.3.2.2 To Build and Package the hello1 Web Module Using
            Maven](webapp003.htm#GJRKN)
      - [6.3.3 Viewing Deployed Web Modules](webapp003.htm#BNAEI)
          - [6.3.3.1 To View Deployed Web Modules Using the
            Administration Console](webapp003.htm#GJSGR)
          - [6.3.3.2 To View Deployed Web Modules Using the asadmin
            Command](webapp003.htm#GJSEW)
          - [6.3.3.3 To View Deployed Web Modules Using NetBeans
            IDE](webapp003.htm#sthref24)
      - [6.3.4 Running the Deployed hello1 Web
        Module](webapp003.htm#BCEBEGED)
          - [6.3.4.1 Dynamic Reloading of Deployed
            Modules](webapp003.htm#BNAEM)
      - [6.3.5 Undeploying the hello1 Web Module](webapp003.htm#BNAEN)
          - [6.3.5.1 To Undeploy the hello1 Web Module Using NetBeans
            IDE](webapp003.htm#GJSEJ)
          - [6.3.5.2 To Undeploy the hello1 Web Module Using
            Maven](webapp003.htm#GJSHH)
  - [6.4 A Web Module That Uses Java Servlet Technology: The hello2
    Example](webapp004.htm#BNAEO)
      - [6.4.1 Mapping URLs to Web Components](webapp004.htm#BNAEP)
      - [6.4.2 Examining the hello2 Web Module](webapp004.htm#GJWWG)
          - [6.4.2.1 To View the hello2 Web Module Using NetBeans
            IDE](webapp004.htm#GJWWA)
      - [6.4.3 Running the hello2 Example](webapp004.htm#GKBLH)
          - [6.4.3.1 To Run the hello2 Example Using NetBeans
            IDE](webapp004.htm#GJSED)
          - [6.4.3.2 To Run the hello2 Example Using
            Maven](webapp004.htm#GJSHX)
  - [6.5 Configuring Web Applications](webapp005.htm#CHDHGJIA)
      - [6.5.1 Setting Context Parameters](webapp005.htm#BNAES)
          - [6.5.1.1 To Add a Context Parameter Using NetBeans
            IDE](webapp005.htm#GJSFJ)
          - [6.5.1.2 To Create a web.xml File Using NetBeans
            IDE](webapp005.htm#GKIHH)
      - [6.5.2 Declaring Welcome Files](webapp005.htm#BNAER)
      - [6.5.3 Mapping Errors to Error Screens](webapp005.htm#GKBKW)
          - [6.5.3.1 To Set Up Error Mapping Using NetBeans
            IDE](webapp005.htm#BNAET)
      - [6.5.4 Declaring Resource References](webapp005.htm#BNAEU)
          - [6.5.4.1 Declaring a Reference to a
            Resource](webapp005.htm#BNAEW)
          - [6.5.4.2 Declaring a Reference to a Web
            Service](webapp005.htm#BNAEX)
  - [6.6 Further Information about Web
    Applications](webapp006.htm#BNAFC)

## [7 JavaServer Faces Technology](jsf-intro.htm#BNAPH)

  - [7.1 Introduction to JavaServer Faces
    Technology](jsf-intro001.htm#A1073698)
  - [7.2 What Is a JavaServer Faces
    Application?](jsf-intro002.htm#BNAPK)
  - [7.3 JavaServer Faces Technology Benefits](jsf-intro003.htm#BNAPJ)
  - [7.4 A Simple JavaServer Faces Application](jsf-intro004.htm#GJAAM)
  - [7.5 User Interface Component Model](jsf-intro005.htm#BNAQD)
      - [7.5.1 User Interface Component Classes](jsf-intro005.htm#BNAQE)
      - [7.5.2 Component Rendering Model](jsf-intro005.htm#BNAQF)
      - [7.5.3 Conversion Model](jsf-intro005.htm#BNAQI)
      - [7.5.4 Event and Listener Model](jsf-intro005.htm#GIREH)
      - [7.5.5 Validation Model](jsf-intro005.htm#BNAQK)
  - [7.6 Navigation Model](jsf-intro006.htm#BNAQL)
  - [7.7 The Lifecycle of a JavaServer Faces
    Application](jsf-intro007.htm#BNAQQ)
      - [7.7.1 Overview of the JavaServer Faces
        Lifecycle](jsf-intro007.htm#GLPRC)
      - [7.7.2 Restore View Phase](jsf-intro007.htm#BNAQS)
      - [7.7.3 Apply Request Values Phase](jsf-intro007.htm#BNAQT)
      - [7.7.4 Process Validations Phase](jsf-intro007.htm#GJSBP)
      - [7.7.5 Update Model Values Phase](jsf-intro007.htm#BNAQV)
      - [7.7.6 Invoke Application Phase](jsf-intro007.htm#BNAQW)
      - [7.7.7 Render Response Phase](jsf-intro007.htm#BNAQX)
  - [7.8 Partial Processing and Partial
    Rendering](jsf-intro008.htm#GKNOJ)
  - [7.9 Further Information about JavaServer Faces
    Technology](jsf-intro009.htm#BNAQY)

## [8 Introduction to Facelets](jsf-facelets.htm#GIEPX)

  - [8.1 What Is Facelets?](jsf-facelets001.htm#GIJTU)
  - [8.2 The Lifecycle of a Facelets
    Application](jsf-facelets002.htm#GIPRR)
  - [8.3 Developing a Simple Facelets Application: The guessnumber-jsf
    Example Application](jsf-facelets003.htm#GIPOB)
      - [8.3.1 Creating a Facelets
        Application](jsf-facelets003.htm#GIQTE)
          - [8.3.1.1 Developing a Managed
            Bean](jsf-facelets003.htm#GIQQZ)
          - [8.3.1.2 Creating Facelets Views](jsf-facelets003.htm#GJZPV)
      - [8.3.2 Configuring the Application](jsf-facelets003.htm#GJJKC)
      - [8.3.3 Running the guessnumber-jsf Facelets
        Example](jsf-facelets003.htm#GIRGF)
          - [8.3.3.1 To Build, Package, and Deploy the guessnumber-jsf
            Example Using NetBeans IDE](jsf-facelets003.htm#GJQZL)
          - [8.3.3.2 To Build, Package, and Deploy the guessnumber-jsf
            Example Using Maven](jsf-facelets003.htm#GJQYU)
          - [8.3.3.3 To Run the guessnumber-jsf
            Example](jsf-facelets003.htm#GJQYX)
  - [8.4 Using Facelets Templates](jsf-facelets004.htm#GIQXP)
  - [8.5 Composite Components](jsf-facelets005.htm#GIQZR)
  - [8.6 Web Resources](jsf-facelets006.htm#GIRGM)
  - [8.7 Relocatable Resources](jsf-facelets007.htm#BABHGBJI)
  - [8.8 Resource Library Contracts](jsf-facelets008.htm#BABHAHDF)
      - [8.8.1 The hello1-rlc Example
        Application](jsf-facelets008.htm#sthref32)
          - [8.8.1.1 Configuring the hello1-rlc
            Example](jsf-facelets008.htm#BABGEDEB)
          - [8.8.1.2 The Facelets Pages for the hello1-rlc
            Example](jsf-facelets008.htm#BABDHCFG)
          - [8.8.1.3 To Build, Package, and Deploy the hello1-rlc
            Example Using NetBeans IDE](jsf-facelets008.htm#BABBGFFF)
          - [8.8.1.4 To Build, Package, and Deploy the hello1-rlc
            Example Using Maven](jsf-facelets008.htm#BABJAGFB)
          - [8.8.1.5 To Run the hello1-rlc
            Example](jsf-facelets008.htm#BABFCHEB)
  - [8.9 HTML5-Friendly Markup](jsf-facelets009.htm#BABGECCJ)
      - [8.9.1 Using Pass-Through
        Elements](jsf-facelets009.htm#sthref33)
      - [8.9.2 Using Pass-Through
        Attributes](jsf-facelets009.htm#sthref35)
      - [8.9.3 The reservation Example
        Application](jsf-facelets009.htm#BABGGIAA)
          - [8.9.3.1 The Facelets Pages for the reservation
            Application](jsf-facelets009.htm#BABGCAHH)
          - [8.9.3.2 The Managed Bean for the reservation
            Application](jsf-facelets009.htm#BABHFCCG)
          - [8.9.3.3 To Build, Package, and Deploy the reservation
            Example Using NetBeans IDE](jsf-facelets009.htm#BABIHHGC)
          - [8.9.3.4 To Build, Package, and Deploy the reservation
            Example Using Maven](jsf-facelets009.htm#sthref36)
          - [8.9.3.5 To Run the reservation
            Example](jsf-facelets009.htm#sthref37)

## [9 Expression Language](jsf-el.htm#GJDDD)

  - [9.1 Overview of the EL](jsf-el001.htm#BNAHQ)
  - [9.2 Immediate and Deferred Evaluation Syntax](jsf-el002.htm#BNAHR)
      - [9.2.1 Immediate Evaluation](jsf-el002.htm#BNAHS)
      - [9.2.2 Deferred Evaluation](jsf-el002.htm#BNAHT)
  - [9.3 Value and Method Expressions](jsf-el003.htm#BNAHU)
      - [9.3.1 Value Expressions](jsf-el003.htm#BNAHV)
          - [9.3.1.1 Referencing Objects](jsf-el003.htm#BNAHW)
          - [9.3.1.2 Referencing Object Properties or Collection
            Elements](jsf-el003.htm#BNAHX)
          - [9.3.1.3 Referencing Literals](jsf-el003.htm#sthref38)
          - [9.3.1.4 Parameterized Method Calls](jsf-el003.htm#GJHBZ)
          - [9.3.1.5 Where Value Expressions Can Be
            Used](jsf-el003.htm#BNAHY)
      - [9.3.2 Method Expressions](jsf-el003.htm#BNAHZ)
      - [9.3.3 Lambda Expressions](jsf-el003.htm#BEIHCBAH)
  - [9.4 Operations on Collection Objects](jsf-el004.htm#CIHGABHD)
  - [9.5 Operators](jsf-el005.htm#BNAIK)
  - [9.6 Reserved Words](jsf-el006.htm#BNAIL)
  - [9.7 Examples of EL Expressions](jsf-el007.htm#BNAIM)
  - [9.8 Further Information about the Expression
    Language](jsf-el008.htm#CIHGBBHA)

## [10 Using JavaServer Faces Technology in Web Pages](jsf-page.htm#BNAQZ)

  - [10.1 Setting Up a Page](jsf-page001.htm#BNARB)
  - [10.2 Adding Components to a Page Using HTML Tag Library
    Tags](jsf-page002.htm#BNARF)
      - [10.2.1 Common Component Tag Attributes](jsf-page002.htm#BNARG)
          - [10.2.1.1 The id Attribute](jsf-page002.htm#BNARH)
          - [10.2.1.2 The immediate Attribute](jsf-page002.htm#BNARI)
          - [10.2.1.3 The rendered Attribute](jsf-page002.htm#BNARJ)
          - [10.2.1.4 The style and styleClass
            Attributes](jsf-page002.htm#BNARK)
          - [10.2.1.5 The value and binding
            Attributes](jsf-page002.htm#BNARL)
      - [10.2.2 Adding HTML Head and Body Tags](jsf-page002.htm#GJDGQ)
      - [10.2.3 Adding a Form Component](jsf-page002.htm#BNARM)
      - [10.2.4 Using Text Components](jsf-page002.htm#BNARO)
          - [10.2.4.1 Rendering a Field with the h:inputText
            Tag](jsf-page002.htm#BNARR)
          - [10.2.4.2 Rendering a Password Field with the h:inputSecret
            Tag](jsf-page002.htm#BNARV)
          - [10.2.4.3 Rendering a Label with the h:outputLabel
            Tag](jsf-page002.htm#BNARS)
          - [10.2.4.4 Rendering a Link with the h:outputLink
            Tag](jsf-page002.htm#BNART)
          - [10.2.4.5 Displaying a Formatted Message with the
            h:outputFormat Tag](jsf-page002.htm#BNARU)
      - [10.2.5 Using Command Component Tags for Performing Actions and
        Navigation](jsf-page002.htm#BNARW)
          - [10.2.5.1 Rendering a Button with the h:commandButton
            Tag](jsf-page002.htm#BNARX)
          - [10.2.5.2 Rendering a Link with the h:commandLink
            Tag](jsf-page002.htm#GKBUJ)
      - [10.2.6 Adding Graphics and Images with the h:graphicImage
        Tag](jsf-page002.htm#BNASB)
      - [10.2.7 Laying Out Components with the h:panelGrid and
        h:panelGroup Tags](jsf-page002.htm#BNASC)
      - [10.2.8 Displaying Components for Selecting One
        Value](jsf-page002.htm#BNASE)
          - [10.2.8.1 Displaying a Check Box Using the
            h:selectBooleanCheckbox Tag](jsf-page002.htm#BNASG)
          - [10.2.8.2 Displaying a Menu Using the h:selectOneMenu
            Tag](jsf-page002.htm#BNASH)
      - [10.2.9 Displaying Components for Selecting Multiple
        Values](jsf-page002.htm#BNASI)
      - [10.2.10 Using the f:selectItem and f:selectItems
        Tags](jsf-page002.htm#BNASK)
          - [10.2.10.1 Using the f:selectItems
            Tag](jsf-page002.htm#BNASM)
          - [10.2.10.2 Using the f:selectItem
            Tag](jsf-page002.htm#BNASN)
      - [10.2.11 Displaying the Results from Selection
        Components](jsf-page002.htm#sthref50)
      - [10.2.12 Using Data-Bound Table
        Components](jsf-page002.htm#BNARZ)
      - [10.2.13 Displaying Error Messages with the h:message and
        h:messages Tags](jsf-page002.htm#BNASO)
      - [10.2.14 Creating Bookmarkable URLs with the h:button and h:link
        Tags](jsf-page002.htm#GIQZD)
      - [10.2.15 Using View Parameters to Configure Bookmarkable
        URLs](jsf-page002.htm#GIQWQ)
      - [10.2.16 The bookmarks Example
        Application](jsf-page002.htm#sthref52)
          - [10.2.16.1 To Build, Package, and Deploy the bookmarks
            Example Using NetBeans IDE](jsf-page002.htm#CHDIEHEB)
          - [10.2.16.2 To Build, Package, and Deploy the bookmarks
            Example Using Maven](jsf-page002.htm#CHDEFJEF)
          - [10.2.16.3 To Run the bookmarks
            Example](jsf-page002.htm#CHDGEBCB)
      - [10.2.17 Resource Relocation Using h:outputScript and
        h:outputStylesheet Tags](jsf-page002.htm#GJGEP)
  - [10.3 Using Core
Tags](jsf-page003.htm#BNARC)

## [11 Using Converters, Listeners, and Validators](jsf-page-core.htm#GJCUT)

  - [11.1 Using the Standard Converters](jsf-page-core001.htm#BNAST)
      - [11.1.1 Converting a Component's
        Value](jsf-page-core001.htm#BNASU)
      - [11.1.2 Using DateTimeConverter](jsf-page-core001.htm#BNASV)
      - [11.1.3 Using NumberConverter](jsf-page-core001.htm#BNASX)
  - [11.2 Registering Listeners on
    Components](jsf-page-core002.htm#BNASZ)
      - [11.2.1 Registering a Value-Change Listener on a
        Component](jsf-page-core002.htm#BNATA)
      - [11.2.2 Registering an Action Listener on a
        Component](jsf-page-core002.htm#BNATB)
  - [11.3 Using the Standard Validators](jsf-page-core003.htm#BNATC)
      - [11.3.1 Validating a Component's
        Value](jsf-page-core003.htm#BNATE)
      - [11.3.2 Using Validator Tags](jsf-page-core003.htm#BNATF)
  - [11.4 Referencing a Managed Bean Method](jsf-page-core004.htm#BNATN)
      - [11.4.1 Referencing a Method That Performs
        Navigation](jsf-page-core004.htm#BNATP)
      - [11.4.2 Referencing a Method That Handles an Action
        Event](jsf-page-core004.htm#BNATQ)
      - [11.4.3 Referencing a Method That Performs
        Validation](jsf-page-core004.htm#BNATR)
      - [11.4.4 Referencing a Method That Handles a Value-Change
        Event](jsf-page-core004.htm#BNATS)

## [12 Developing with JavaServer Faces Technology](jsf-develop.htm#BNATX)

  - [12.1 Managed Beans in JavaServer Faces
    Technology](jsf-develop001.htm#BNAQM)
      - [12.1.1 Creating a Managed Bean](jsf-develop001.htm#BNAQN)
      - [12.1.2 Using the EL to Reference Managed
        Beans](jsf-develop001.htm#BNAQP)
  - [12.2 Writing Bean Properties](jsf-develop002.htm#BNATY)
      - [12.2.1 Writing Properties Bound to Component
        Values](jsf-develop002.htm#BNATZ)
          - [12.2.1.1 UIInput and UIOutput
            Properties](jsf-develop002.htm#BNAUB)
          - [12.2.1.2 UIData Properties](jsf-develop002.htm#BNAUC)
          - [12.2.1.3 UISelectBoolean
            Properties](jsf-develop002.htm#BNAUD)
          - [12.2.1.4 UISelectMany Properties](jsf-develop002.htm#BNAUE)
          - [12.2.1.5 UISelectOne Properties](jsf-develop002.htm#BNAUF)
          - [12.2.1.6 UISelectItem Properties](jsf-develop002.htm#BNAUG)
          - [12.2.1.7 UISelectItems
            Properties](jsf-develop002.htm#BNAUH)
      - [12.2.2 Writing Properties Bound to Component
        Instances](jsf-develop002.htm#BNAUK)
      - [12.2.3 Writing Properties Bound to Converters, Listeners, or
        Validators](jsf-develop002.htm#BNAUL)
  - [12.3 Writing Managed Bean Methods](jsf-develop003.htm#BNAVB)
      - [12.3.1 Why Use Managed Beans](jsf-develop003.htm#sthref67)
      - [12.3.2 Writing a Method to Handle
        Navigation](jsf-develop003.htm#BNAVC)
      - [12.3.3 Writing a Method to Handle an Action
        Event](jsf-develop003.htm#BNAVD)
      - [12.3.4 Writing a Method to Perform
        Validation](jsf-develop003.htm#BNAVE)
      - [12.3.5 Writing a Method to Handle a Value-Change
        Event](jsf-develop003.htm#BNAVF)

## [13 Using Ajax with JavaServer Faces Technology](jsf-ajax.htm#GKIOW)

  - [13.1 Overview of Ajax](jsf-ajax001.htm#GKIGR)
  - [13.2 Using Ajax Functionality with JavaServer Faces
    Technology](jsf-ajax002.htm#GKINL)
  - [13.3 Using Ajax with Facelets](jsf-ajax003.htm#GKABR)
      - [13.3.1 Using the f:ajax Tag](jsf-ajax003.htm#GKAFN)
  - [13.4 Sending an Ajax Request](jsf-ajax004.htm#GKACE)
      - [13.4.1 Using the event Attribute](jsf-ajax004.htm#GKHVT)
      - [13.4.2 Using the execute Attribute](jsf-ajax004.htm#GKHUZ)
      - [13.4.3 Using the immediate Attribute](jsf-ajax004.htm#GKHWM)
      - [13.4.4 Using the listener Attribute](jsf-ajax004.htm#GKHZS)
  - [13.5 Monitoring Events on the Client](jsf-ajax005.htm#GKDDF)
  - [13.6 Handling Errors](jsf-ajax006.htm#GKDCB)
  - [13.7 Receiving an Ajax Response](jsf-ajax007.htm#GKDBR)
  - [13.8 Ajax Request Lifecycle](jsf-ajax008.htm#GKUAR)
  - [13.9 Grouping of Components](jsf-ajax009.htm#GKHYH)
  - [13.10 Loading JavaScript as a Resource](jsf-ajax010.htm#GKAAM)
      - [13.10.1 Using JavaScript API in a Facelets
        Application](jsf-ajax010.htm#GKAFI)
      - [13.10.2 Using the @ResourceDependency Annotation in a Bean
        Class](jsf-ajax010.htm#GKIPX)
  - [13.11 The ajaxguessnumber Example
    Application](jsf-ajax011.htm#GKOKB)
      - [13.11.1 The ajaxguessnumber Source
        Files](jsf-ajax011.htm#GKOIJ)
          - [13.11.1.1 The ajaxgreeting.xhtml Facelets
            Page](jsf-ajax011.htm#GKOFW)
          - [13.11.1.2 The UserNumberBean Backing
            Bean](jsf-ajax011.htm#GKOHN)
          - [13.11.1.3 The DukesNumberBean CDI Managed
            Bean](jsf-ajax011.htm#CHDGAIGJ)
      - [13.11.2 Running the ajaxguessnumber
        Example](jsf-ajax011.htm#GKOKE)
          - [13.11.2.1 To Build, Package, and Deploy the ajaxguessnumber
            Example Using NetBeans IDE](jsf-ajax011.htm#GLHVU)
          - [13.11.2.2 To Build, Package, and Deploy the ajaxguessnumber
            Example Using Maven](jsf-ajax011.htm#GLHVQ)
          - [13.11.2.3 To Run the ajaxguessnumber
            Example](jsf-ajax011.htm#GLHWE)
  - [13.12 Further Information about Ajax in JavaServer Faces
    Technology](jsf-ajax012.htm#GKSDK)

## [14 Composite Components: Advanced Topics and an Example](jsf-advanced-cc.htm#GKHXA)

  - [14.1 Attributes of a Composite
    Component](jsf-advanced-cc001.htm#GKHWV)
  - [14.2 Invoking a Managed Bean](jsf-advanced-cc002.htm#GKHUO)
  - [14.3 Validating Composite Component
    Values](jsf-advanced-cc003.htm#GKHWO)
  - [14.4 The compositecomponentexample Example
    Application](jsf-advanced-cc004.htm#GKHVN)
      - [14.4.1 The Composite Component
        File](jsf-advanced-cc004.htm#GKHUU)
      - [14.4.2 The Using Page](jsf-advanced-cc004.htm#GKHVX)
      - [14.4.3 The Managed Bean](jsf-advanced-cc004.htm#GKHVQ)
      - [14.4.4 Running the compositecomponentexample
        Example](jsf-advanced-cc004.htm#GLECV)
          - [14.4.4.1 To Build, Package, and Deploy the
            compositecomponentexample Example Using NetBeans
            IDE](jsf-advanced-cc004.htm#GKHVC)
          - [14.4.4.2 To Build, Package, and Deploy the
            compositecomponentexample Example Using
            Maven](jsf-advanced-cc004.htm#GLEAE)
          - [14.4.4.3 To Run the compositecomponentexample
            Example](jsf-advanced-cc004.htm#GLEEU)

## [15 Creating Custom UI Components and Other Custom Objects](jsf-custom.htm#BNAVG)

  - [15.1 Introduction to Creating Custom
    Components](jsf-custom001.htm#A1350198)
  - [15.2 Determining Whether You Need a Custom Component or
    Renderer](jsf-custom002.htm#BNAVH)
      - [15.2.1 When to Use a Custom Component](jsf-custom002.htm#BNAVI)
      - [15.2.2 When to Use a Custom Renderer](jsf-custom002.htm#BNAVJ)
      - [15.2.3 Component, Renderer, and Tag
        Combinations](jsf-custom002.htm#BNAVK)
  - [15.3 Understanding the Image Map Example](jsf-custom003.htm#GLPCB)
      - [15.3.1 Why Use JavaServer Faces Technology to Implement an
        Image Map?](jsf-custom003.htm#GLPBD)
      - [15.3.2 Understanding the Rendered
        HTML](jsf-custom003.htm#GLPEM)
      - [15.3.3 Understanding the Facelets
        Page](jsf-custom003.htm#GLPCD)
      - [15.3.4 Configuring Model Data](jsf-custom003.htm#GLPBO)
      - [15.3.5 Summary of the Image Map Application
        Classes](jsf-custom003.htm#GLPEL)
  - [15.4 Steps for Creating a Custom
    Component](jsf-custom004.htm#BNAVT)
  - [15.5 Creating Custom Component Classes](jsf-custom005.htm#BNAVU)
      - [15.5.1 Specifying the Component
        Family](jsf-custom005.htm#BNAVV)
      - [15.5.2 Performing Encoding](jsf-custom005.htm#BNAVW)
      - [15.5.3 Performing Decoding](jsf-custom005.htm#BNAVX)
      - [15.5.4 Enabling Component Properties to Accept
        Expressions](jsf-custom005.htm#BNAVY)
      - [15.5.5 Saving and Restoring State](jsf-custom005.htm#BNAVZ)
  - [15.6 Delegating Rendering to a Renderer](jsf-custom006.htm#BNAWA)
      - [15.6.1 Creating the Renderer Class](jsf-custom006.htm#BNAWB)
      - [15.6.2 Identifying the Renderer Type](jsf-custom006.htm#BNAWC)
  - [15.7 Implementing an Event Listener](jsf-custom007.htm#BNAUT)
      - [15.7.1 Implementing Value-Change
        Listeners](jsf-custom007.htm#BNAUU)
      - [15.7.2 Implementing Action Listeners](jsf-custom007.htm#BNAUV)
  - [15.8 Handling Events for Custom
    Components](jsf-custom008.htm#BNAWD)
  - [15.9 Defining the Custom Component Tag in a Tag Library
    Descriptor](jsf-custom009.htm#BNAWN)
  - [15.10 Using a Custom Component](jsf-custom010.htm#BNATT)
  - [15.11 Creating and Using a Custom
    Converter](jsf-custom011.htm#BNAUS)
      - [15.11.1 Creating a Custom Converter](jsf-custom011.htm#GLPHB)
      - [15.11.2 Using a Custom Converter](jsf-custom011.htm#BNATU)
  - [15.12 Creating and Using a Custom
    Validator](jsf-custom012.htm#BNAUW)
      - [15.12.1 Implementing the Validator
        Interface](jsf-custom012.htm#BNAUX)
      - [15.12.2 Specifying a Custom Tag](jsf-custom012.htm#BNAUY)
      - [15.12.3 Using a Custom Validator](jsf-custom012.htm#BNATV)
  - [15.13 Binding Component Values and Instances to Managed Bean
    Properties](jsf-custom013.htm#BNATG)
      - [15.13.1 Binding a Component Value to a
        Property](jsf-custom013.htm#BNATI)
      - [15.13.2 Binding a Component Value to an Implicit
        Object](jsf-custom013.htm#BNATJ)
      - [15.13.3 Binding a Component Instance to a Bean
        Property](jsf-custom013.htm#BNATL)
  - [15.14 Binding Converters, Listeners, and Validators to Managed Bean
    Properties](jsf-custom014.htm#BNATM)

## [16 Configuring JavaServer Faces Applications](jsf-configure.htm#BNAWO)

  - [16.1 Introduction to Configuring JavaServer Faces
    Applications](jsf-configure001.htm#A1352824)
  - [16.2 Using Annotations to Configure Managed
    Beans](jsf-configure002.htm#GIRCH)
      - [16.2.1 Using Managed Bean Scopes](jsf-configure002.htm#GIRCR)
  - [16.3 Application Configuration Resource
    File](jsf-configure003.htm#BNAWP)
      - [16.3.1 Configuring Eager Application-Scoped Managed
        Beans](jsf-configure003.htm#GIREP)
      - [16.3.2 Ordering of Application Configuration Resource
        Files](jsf-configure003.htm#GIQCK)
  - [16.4 Using Faces Flows](jsf-configure004.htm#CHDGFCJF)
      - [16.4.1 Packaging Flows in an
        Application](jsf-configure004.htm#sthref80)
      - [16.4.2 The Simplest Possible Flow: The simple-flow Example
        Application](jsf-configure004.htm#sthref81)
          - [16.4.2.1 To Build, Package, and Deploy the simple-flow
            Example Using NetBeans IDE](jsf-configure004.htm#sthref82)
          - [16.4.2.2 To Build, Package, and Deploy the simple-flow
            Example Using Maven](jsf-configure004.htm#sthref83)
          - [16.4.2.3 To Run the simple-flow
            Example](jsf-configure004.htm#sthref84)
      - [16.4.3 The checkout-module Example
        Application](jsf-configure004.htm#sthref85)
          - [16.4.3.1 The Facelets Pages for the checkout-module
            Example](jsf-configure004.htm#sthref86)
          - [16.4.3.2 Using a Configuration File to Configure a
            Flow](jsf-configure004.htm#sthref87)
          - [16.4.3.3 Using a Java Class to Configure a
            Flow](jsf-configure004.htm#sthref88)
          - [16.4.3.4 The Flow-Scoped Managed
            Beans](jsf-configure004.htm#sthref89)
          - [16.4.3.5 To Build, Package, and Deploy the checkout-module
            Example Using NetBeans IDE](jsf-configure004.htm#sthref90)
          - [16.4.3.6 To Build, Package, and Deploy the checkout-module
            Example Using Maven](jsf-configure004.htm#sthref91)
          - [16.4.3.7 To Run the checkout-module
            Example](jsf-configure004.htm#sthref92)
  - [16.5 Configuring Managed Beans](jsf-configure005.htm#BNAWQ)
      - [16.5.1 Using the managed-bean
        Element](jsf-configure005.htm#BNAWR)
      - [16.5.2 Initializing Properties Using the managed-property
        Element](jsf-configure005.htm#BNAWS)
          - [16.5.2.1 Referencing a Java Enum
            Type](jsf-configure005.htm#BNAWU)
          - [16.5.2.2 Referencing a Context Initialization
            Parameter](jsf-configure005.htm#BNAWV)
          - [16.5.2.3 Initializing Map
            Properties](jsf-configure005.htm#BNAWW)
          - [16.5.2.4 Initializing Array and List
            Properties](jsf-configure005.htm#BNAWX)
          - [16.5.2.5 Initializing Managed Bean
            Properties](jsf-configure005.htm#BNAWY)
      - [16.5.3 Initializing Maps and Lists](jsf-configure005.htm#BNAXA)
  - [16.6 Registering Application Messages](jsf-configure006.htm#BNAXB)
      - [16.6.1 Using FacesMessage to Create a
        Message](jsf-configure006.htm#GKUHG)
      - [16.6.2 Referencing Error Messages](jsf-configure006.htm#BNASS)
  - [16.7 Using Default Validators](jsf-configure007.htm#GIREB)
  - [16.8 Registering a Custom Validator](jsf-configure008.htm#BNAXD)
  - [16.9 Registering a Custom Converter](jsf-configure009.htm#BNAXE)
  - [16.10 Configuring Navigation Rules](jsf-configure010.htm#BNAXF)
  - [16.11 Registering a Custom Renderer with a Render
    Kit](jsf-configure011.htm#BNAXH)
  - [16.12 Registering a Custom Component](jsf-configure012.htm#BNAXI)
  - [16.13 Basic Requirements of a JavaServer Faces
    Application](jsf-configure013.htm#BNAXJ)
      - [16.13.1 Configuring an Application with a Web Deployment
        Descriptor](jsf-configure013.htm#BNAXK)
          - [16.13.1.1 Identifying the Servlet for Lifecycle
            Processing](jsf-configure013.htm#GLPOO)
          - [16.13.1.2 To Specify a Path to an Application Configuration
            Resource File](jsf-configure013.htm#BNAXM)
          - [16.13.1.3 To Specify Where State Is
            Saved](jsf-configure013.htm#BNAXN)
      - [16.13.2 Configuring Project Stage](jsf-configure013.htm#GIQXL)
      - [16.13.3 Including the Classes, Pages, and Other
        Resources](jsf-configure013.htm#BNAXT)

## [17 Java Servlet Technology](servlets.htm#BNAFD)

  - [17.1 What Is a Servlet?](servlets001.htm#BNAFE)
  - [17.2 Servlet Lifecycle](servlets002.htm#BNAFI)
      - [17.2.1 Handling Servlet Lifecycle
        Events](servlets002.htm#BNAFJ)
          - [17.2.1.1 Defining the Listener
            Class](servlets002.htm#BNAFK)
      - [17.2.2 Handling Servlet Errors](servlets002.htm#BNAFN)
  - [17.3 Sharing Information](servlets003.htm#BNAFO)
      - [17.3.1 Using Scope Objects](servlets003.htm#BNAFP)
      - [17.3.2 Controlling Concurrent Access to Shared
        Resources](servlets003.htm#BNAFS)
  - [17.4 Creating and Initializing a Servlet](servlets004.htm#BNAFU)
  - [17.5 Writing Service Methods](servlets005.htm#BNAFV)
      - [17.5.1 Getting Information from
        Requests](servlets005.htm#BNAFW)
      - [17.5.2 Constructing Responses](servlets005.htm#BNAFZ)
  - [17.6 Filtering Requests and Responses](servlets006.htm#BNAGB)
      - [17.6.1 Programming Filters](servlets006.htm#BNAGC)
      - [17.6.2 Programming Customized Requests and
        Responses](servlets006.htm#BNAGD)
      - [17.6.3 Specifying Filter Mappings](servlets006.htm#BNAGF)
          - [17.6.3.1 To Specify Filter Mappings Using NetBeans
            IDE](servlets006.htm#GJSLC)
  - [17.7 Invoking Other Web Resources](servlets007.htm#BNAGI)
      - [17.7.1 Including Other Resources in the
        Response](servlets007.htm#BNAGJ)
      - [17.7.2 Transferring Control to Another Web
        Component](servlets007.htm#BNAGK)
  - [17.8 Accessing the Web Context](servlets008.htm#BNAGL)
  - [17.9 Maintaining Client State](servlets009.htm#BNAGM)
      - [17.9.1 Accessing a Session](servlets009.htm#BNAGN)
      - [17.9.2 Associating Objects with a
        Session](servlets009.htm#BNAGO)
      - [17.9.3 Session Management](servlets009.htm#BNAGQ)
          - [17.9.3.1 To Set the Timeout Period Using NetBeans
            IDE](servlets009.htm#sthref99)
      - [17.9.4 Session Tracking](servlets009.htm#BNAGR)
  - [17.10 Finalizing a Servlet](servlets010.htm#BNAGS)
      - [17.10.1 Tracking Service Requests](servlets010.htm#BNAGT)
      - [17.10.2 Notifying Methods to Shut Down](servlets010.htm#BNAGU)
      - [17.10.3 Creating Polite Long-Running
        Methods](servlets010.htm#BNAGV)
  - [17.11 Uploading Files with Java Servlet
    Technology](servlets011.htm#BABFGCHB)
      - [17.11.1 The @MultipartConfig
        Annotation](servlets011.htm#sthref100)
      - [17.11.2 The getParts and getPart
        Methods](servlets011.htm#sthref101)
  - [17.12 Asynchronous Processing](servlets012.htm#BEIGCFDF)
      - [17.12.1 Asynchronous Processing in
        Servlets](servlets012.htm#sthref102)
      - [17.12.2 Waiting for a Resource](servlets012.htm#sthref104)
  - [17.13 Nonblocking I/O](servlets013.htm#BEIHICDH)
      - [17.13.1 Reading a Large HTTP POST Request Using Nonblocking
        I/O](servlets013.htm#sthref108)
  - [17.14 Protocol Upgrade Processing](servlets014.htm#BEIJHCDJ)
  - [17.15 The mood Example Application](servlets015.htm#GKCPG)
      - [17.15.1 Components of the mood Example
        Application](servlets015.htm#CHDEBFCB)
      - [17.15.2 Running the mood Example](servlets015.htm#GKCOJ)
          - [17.15.2.1 To Run the mood Example Using NetBeans
            IDE](servlets015.htm#GKCOB)
          - [17.15.2.2 To Run the mood Example Using
            Maven](servlets015.htm#GKCPJ)
  - [17.16 The fileupload Example Application](servlets016.htm#BABDGFJJ)
      - [17.16.1 Architecture of the fileupload Example
        Application](servlets016.htm#CHDFGBGI)
      - [17.16.2 Running the fileupload
        Example](servlets016.htm#CHDIHJCI)
          - [17.16.2.1 To Build, Package, and Deploy the fileupload
            Example Using NetBeans IDE](servlets016.htm#CHDGDJCI)
          - [17.16.2.2 To Build, Package, and Deploy the fileupload
            Example Using Maven](servlets016.htm#CHDCFADG)
          - [17.16.2.3 To Run the fileupload
            Example](servlets016.htm#CHDDDAAJ)
  - [17.17 The dukeetf Example Application](servlets017.htm#BEIFAIFF)
      - [17.17.1 Architecture of the dukeetf Example
        Application](servlets017.htm#CHDBBEDA)
          - [17.17.1.1 The Servlet](servlets017.htm#sthref110)
          - [17.17.1.2 The Enterprise Bean](servlets017.htm#sthref111)
          - [17.17.1.3 The HTML Page](servlets017.htm#sthref112)
      - [17.17.2 Running the dukeetf Example
        Application](servlets017.htm#CHDHBBBI)
          - [17.17.2.1 To Run the dukeetf Example Application Using
            NetBeans IDE](servlets017.htm#CHDCGCJD)
          - [17.17.2.2 To Run the dukeetf Example Application Using
            Maven](servlets017.htm#CHDHHAFG)
  - [17.18 Further Information about Java Servlet
    Technology](servlets018.htm#BNAGW)

## [18 Java API for WebSocket](websocket.htm#GKJIQ5)

  - [18.1 Introduction to WebSocket](websocket001.htm#BABDABHF)
  - [18.2 Creating WebSocket Applications in the Java EE
    Platform](websocket002.htm#BABEAEFC)
      - [18.2.1 Creating and Deploying a WebSocket
        Endpoint](websocket002.htm#sthref113)
  - [18.3 Programmatic Endpoints](websocket003.htm#BABGJEIG)
  - [18.4 Annotated Endpoints](websocket004.htm#BABFEBGA)
  - [18.5 Sending and Receiving Messages](websocket005.htm#BABFCGBJ)
      - [18.5.1 Sending Messages](websocket005.htm#CIHEHFCB)
          - [18.5.1.1 Sending Messages to All Peers Connected to an
            Endpoint](websocket005.htm#BABIFBCG)
      - [18.5.2 Receiving Messages](websocket005.htm#CIHIDFHD)
  - [18.6 Maintaining Client State](websocket006.htm#BABGJCAD)
  - [18.7 Using Encoders and Decoders](websocket007.htm#BABGADFG)
      - [18.7.1 Implementing Encoders to Convert Java Objects into
        WebSocket Messages](websocket007.htm#CIHBIGBI)
      - [18.7.2 Implementing Decoders to Convert WebSocket Messages into
        Java Objects](websocket007.htm#CIHGDJFG)
  - [18.8 Path Parameters](websocket008.htm#BABEJIJI)
  - [18.9 Handling Errors](websocket009.htm#BABDEJHB)
  - [18.10 Specifying an Endpoint Configurator
    Class](websocket010.htm#BABJAIGH)
  - [18.11 The dukeetf2 Example Application](websocket011.htm#BABGCEHE)
      - [18.11.1 Architecture of the dukeetf2 Sample
        Application](websocket011.htm#CIHJHJCD)
          - [18.11.1.1 The Endpoint](websocket011.htm#sthref115)
          - [18.11.1.2 The Enterprise Bean](websocket011.htm#sthref116)
          - [18.11.1.3 The HTML Page](websocket011.htm#CIHHIEFH)
      - [18.11.2 Running the dukeetf2 Example
        Application](websocket011.htm#CIHHBAIC)
          - [18.11.2.1 To Run the dukeetf2 Example Application Using
            NetBeans IDE](websocket011.htm#CIHEBIAH)
          - [18.11.2.2 To Run the dukeetf2 Example Application Using
            Maven](websocket011.htm#CIHDJCGJ)
  - [18.12 The websocketbot Example
    Application](websocket012.htm#BABCDBBC)
      - [18.12.1 Architecture of the websocketbot Example
        Application](websocket012.htm#CIHICIDE)
          - [18.12.1.1 The CDI Bean](websocket012.htm#CIHDAEHF)
          - [18.12.1.2 The WebSocket
            Endpoint](websocket012.htm#CIHJJJHG)
          - [18.12.1.3 The Application
            Messages](websocket012.htm#CIHFDGHG)
          - [18.12.1.4 The Encoder Classes](websocket012.htm#CIHGHHBD)
          - [18.12.1.5 The Message Decoder](websocket012.htm#CIHHFICG)
          - [18.12.1.6 The HTML Page](websocket012.htm#CIHGDBGF)
      - [18.12.2 Running the websocketbot Example
        Application](websocket012.htm#CIHHJHDB)
          - [18.12.2.1 To Run the websocketbot Example Application Using
            NetBeans IDE](websocket012.htm#CIHFDDGE)
          - [18.12.2.2 To Run the websocketbot Example Application Using
            Maven](websocket012.htm#CIHEDEHB)
          - [18.12.2.3 To Test the websocketbot Example
            Application](websocket012.htm#BABDDAAG)
  - [18.13 Further Information about
    WebSocket](websocket013.htm#BABDFIFD)

## [19 JSON Processing](jsonp.htm#GLRBB)

  - [19.1 Introduction to JSON](jsonp001.htm#BABEECIB)
      - [19.1.1 JSON Syntax](jsonp001.htm#BABGHEHG)
      - [19.1.2 Uses of JSON](jsonp001.htm#CEGJHJAB)
      - [19.1.3 Generating and Parsing JSON Data](jsonp001.htm#BABJJACI)
  - [19.2 JSON Processing in the Java EE
    Platform](jsonp002.htm#BABDFHHD)
  - [19.3 Using the Object Model API](jsonp003.htm#BABHAHIA)
      - [19.3.1 Creating an Object Model from JSON
        Data](jsonp003.htm#BABBHEBA)
      - [19.3.2 Creating an Object Model from Application
        Code](jsonp003.htm#BABIGIAF)
      - [19.3.3 Navigating an Object Model](jsonp003.htm#BABJHEHG)
      - [19.3.4 Writing an Object Model to a
        Stream](jsonp003.htm#BABHEJFF)
  - [19.4 Using the Streaming API](jsonp004.htm#BABDBHIA)
      - [19.4.1 Reading JSON Data Using a Parser](jsonp004.htm#BABGCHIG)
      - [19.4.2 Writing JSON Data Using a
        Generator](jsonp004.htm#BABGJEEF)
  - [19.5 JSON in Java EE RESTful Web Services](jsonp005.htm#BABCFABH)
  - [19.6 The jsonpmodel Example Application](jsonp006.htm#BABEDFCG)
      - [19.6.1 Components of the jsonpmodel Example
        Application](jsonp006.htm#CEGHHCCC)
      - [19.6.2 Running the jsonpmodel Example
        Application](jsonp006.htm#CEGEFHFH)
          - [19.6.2.1 To Run the jsonpmodel Example Application Using
            NetBeans IDE](jsonp006.htm#CEGFECCB)
          - [19.6.2.2 To Run the jsonpmodel Example Application Using
            Maven](jsonp006.htm#CEGGJBFA)
  - [19.7 The jsonpstreaming Example Application](jsonp007.htm#BABBJDAC)
      - [19.7.1 Components of the jsonpstreaming Example
        Application](jsonp007.htm#CEGDBIID)
      - [19.7.2 Running the jsonpstreaming Example
        Application](jsonp007.htm#CEGGHFIG)
          - [19.7.2.1 To Run the jsonpstreaming Example Application
            Using NetBeans IDE](jsonp007.htm#CEGJCBCG)
          - [19.7.2.2 To Run the jsonpstreaming Example Application
            Using Maven](jsonp007.htm#CEGCGDDJ)
  - [19.8 Further Information about the Java API for JSON
    Processing](jsonp008.htm#BABGAAGB)

## [20 Internationalizing and Localizing Web Applications](webi18n.htm#BNAXU)

  - [20.1 Java Platform Localization Classes](webi18n001.htm#BNAXV)
  - [20.2 Providing Localized Messages and Labels](webi18n002.htm#BNAXW)
      - [20.2.1 Establishing the Locale](webi18n002.htm#GKUIA)
      - [20.2.2 Setting the Resource Bundle](webi18n002.htm#BNAXY)
      - [20.2.3 Retrieving Localized Messages](webi18n002.htm#GKUFC)
  - [20.3 Date and Number Formatting](webi18n003.htm#BNAYA)
  - [20.4 Character Sets and Encodings](webi18n004.htm#BNAYB)
      - [20.4.1 Character Sets](webi18n004.htm#BNAYC)
      - [20.4.2 Character Encoding](webi18n004.htm#BNAYD)

## [Part IV Bean Validation](partbeanvalidation.htm#sthref1322)

## [21 Introduction to Bean Validation](bean-validation.htm#CHDGJIIA)

  - [21.1 Overview of Bean Validation](bean-validation001.htm#A1101988)
  - [21.2 Using Bean Validation
    Constraints](bean-validation002.htm#GIRCZ)
  - [21.3 Validating Null and Empty
    Strings](bean-validation003.htm#GKCRG)
  - [21.4 Validating Constructors and
    Methods](bean-validation004.htm#CACJIBEJ)
      - [21.4.1 Cross-Parameter
        Constraints](bean-validation004.htm#sthref120)
      - [21.4.2 Identifying Parameter Constraint
        Violations](bean-validation004.htm#sthref121)
      - [21.4.3 Adding Constraints to Method Return
        Values](bean-validation004.htm#sthref122)
  - [21.5 Further Information about Bean
    Validation](bean-validation005.htm#CACDECFE)

## [22 Bean Validation: Advanced Topics](bean-validation-advanced.htm#GKAHP)

  - [22.1 Creating Custom
    Constraints](bean-validation-advanced001.htm#GKFGX)
      - [22.1.1 Using the Built-In Constraints to Make a New
        Constraint](bean-validation-advanced001.htm#GKAIA)
      - [22.1.2 Removing Ambiguity in Constraint
        Targets](bean-validation-advanced001.htm#CIHCICAI)
  - [22.2 Customizing Validator
    Messages](bean-validation-advanced002.htm#GKAHI)
      - [22.2.1 The ValidationMessages Resource
        Bundle](bean-validation-advanced002.htm#GKAGY)
          - [22.2.1.1 Localizing Validation
            Messages](bean-validation-advanced002.htm#GKAIQ)
  - [22.3 Grouping Constraints](bean-validation-advanced003.htm#GKAGV)
      - [22.3.1 Customizing Group Validation
        Order](bean-validation-advanced003.htm#GKAGU)
  - [22.4 Using Method Constraints in Type
    Hierarchies](bean-validation-advanced004.htm#CIHGJBGI)
      - [22.4.1 Rules for Using Method Constraints in Type
        Hierarchies](bean-validation-advanced004.htm#sthref123)

## [Part V Contexts and Dependency Injection for Java EE](partcdi.htm#GJBNR)

## [23 Introduction to Contexts and Dependency Injection for Java EE](cdi-basic.htm#GIWHB)

  - [23.1 Getting Started](cdi-basic001.htm#BABJDJGA)
  - [23.2 Overview of CDI](cdi-basic002.htm#GIWHL)
  - [23.3 About Beans](cdi-basic003.htm#GJEBJ)
  - [23.4 About CDI Managed Beans](cdi-basic004.htm#GJFZI)
  - [23.5 Beans as Injectable Objects](cdi-basic005.htm#GIZKS)
  - [23.6 Using Qualifiers](cdi-basic006.htm#GJBCK)
  - [23.7 Injecting Beans](cdi-basic007.htm#GJBAN)
  - [23.8 Using Scopes](cdi-basic008.htm#GJBBK)
  - [23.9 Giving Beans EL Names](cdi-basic009.htm#GJBAK)
  - [23.10 Adding Setter and Getter Methods](cdi-basic010.htm#GJBBP)
  - [23.11 Using a Managed Bean in a Facelets
    Page](cdi-basic011.htm#GJBBU)
  - [23.12 Injecting Objects by Using Producer
    Methods](cdi-basic012.htm#GJDID)
  - [23.13 Configuring a CDI Application](cdi-basic013.htm#GJBNZ)
  - [23.14 Using the @PostConstruct and @PreDestroy Annotations with CDI
    Managed Bean Classes](cdi-basic014.htm#BABJFEAI)
      - [23.14.1 To Initialize a Managed Bean Using the @PostConstruct
        Annotation](cdi-basic014.htm#CIHEHHCH)
      - [23.14.2 To Prepare for the Destruction of a Managed Bean Using
        the @PreDestroy Annotation](cdi-basic014.htm#CIHBAFAC)
  - [23.15 Further Information about
CDI](cdi-basic015.htm#GIWEL)

## [24 Running the Basic Contexts and Dependency Injection Examples](cdi-basicexamples.htm#GJBLS)

  - [24.1 Building and Running the CDI
    Samples](cdi-basicexamples001.htm#A1250045)
  - [24.2 The simplegreeting CDI
    Example](cdi-basicexamples002.htm#GJBJU)
      - [24.2.1 The simplegreeting Source
        Files](cdi-basicexamples002.htm#GJCQS)
      - [24.2.2 The Facelets Template and
        Page](cdi-basicexamples002.htm#GJDOJ)
      - [24.2.3 Running the simplegreeting
        Example](cdi-basicexamples002.htm#GJCYM)
          - [24.2.3.1 To Build, Package, and Run the simplegreeting
            Example Using NetBeans IDE](cdi-basicexamples002.htm#GJCXP)
          - [24.2.3.2 To Build, Package, and Deploy the simplegreeting
            Example Using Maven](cdi-basicexamples002.htm#GJCZT)
          - [24.2.3.3 To Run the simplegreeting
            Example](cdi-basicexamples002.htm#GJCZE)
  - [24.3 The guessnumber-cdi CDI
    Example](cdi-basicexamples003.htm#GJCXV)
      - [24.3.1 The guessnumber-cdi Source
        Files](cdi-basicexamples003.htm#GJDJU)
          - [24.3.1.1 The @MaxNumber and @Random Qualifier
            Interfaces](cdi-basicexamples003.htm#GJDJP)
          - [24.3.1.2 The Generator Managed
            Bean](cdi-basicexamples003.htm#GJDJN)
          - [24.3.1.3 The UserNumberBean Managed
            Bean](cdi-basicexamples003.htm#GJDHY)
      - [24.3.2 The Facelets Page](cdi-basicexamples003.htm#GJDON)
      - [24.3.3 Running the guessnumber-cdi
        Example](cdi-basicexamples003.htm#GJDPW)
          - [24.3.3.1 To Build, Package, and Deploy the guessnumber-cdi
            Example Using NetBeans IDE](cdi-basicexamples003.htm#GJDPS)
          - [24.3.3.2 To Build, Package, and Deploy the guessnumber-cdi
            Example Using Maven](cdi-basicexamples003.htm#GJDPR)
          - [24.3.3.3 To Run the guessnumber
            Example](cdi-basicexamples003.htm#GJDQB)

## [25 Contexts and Dependency Injection for Java EE: Advanced Topics](cdi-adv.htm#GJEHI)

  - [25.1 Packaging CDI Applications](cdi-adv001.htm#CACDCFDE)
  - [25.2 Using Alternatives in CDI Applications](cdi-adv002.htm#GJSDF)
      - [25.2.1 Using Specialization](cdi-adv002.htm#GKHPO)
  - [25.3 Using Producer Methods, Producer Fields, and Disposer Methods
    in CDI Applications](cdi-adv003.htm#GKGKV)
      - [25.3.1 Using Producer Methods](cdi-adv003.htm#sthref125)
      - [25.3.2 Using Producer Fields to Generate
        Resources](cdi-adv003.htm#sthref126)
      - [25.3.3 Using a Disposer Method](cdi-adv003.htm#sthref127)
  - [25.4 Using Predefined Beans in CDI
    Applications](cdi-adv004.htm#CJGHGDBA)
  - [25.5 Using Events in CDI Applications](cdi-adv005.htm#GKHIC)
      - [25.5.1 Defining Events](cdi-adv005.htm#GKHHY)
      - [25.5.2 Using Observer Methods to Handle
        Events](cdi-adv005.htm#GKHNF)
      - [25.5.3 Firing Events](cdi-adv005.htm#GKHIH)
  - [25.6 Using Interceptors in CDI Applications](cdi-adv006.htm#GKHJX)
  - [25.7 Using Decorators in CDI Applications](cdi-adv007.htm#GKHQF)
  - [25.8 Using Stereotypes in CDI
Applications](cdi-adv008.htm#GKHQC)

## [26 Running the Advanced Contexts and Dependency Injection Examples](cdi-adv-examples.htm#GKHRE)

  - [26.1 Building and Running the CDI Advanced
    Examples](cdi-adv-examples001.htm#A1251406)
  - [26.2 The encoder Example: Using
    Alternatives](cdi-adv-examples002.htm#GKHPU)
      - [26.2.1 The Coder Interface and
        Implementations](cdi-adv-examples002.htm#GKHQA)
      - [26.2.2 The encoder Facelets Page and Managed
        Bean](cdi-adv-examples002.htm#GKHPM)
      - [26.2.3 Running the encoder
        Example](cdi-adv-examples002.htm#GKHQQ)
          - [26.2.3.1 To Build, Package, and Deploy the encoder Example
            Using NetBeans IDE](cdi-adv-examples002.htm#GKHOW)
          - [26.2.3.2 To Run the encoder Example Using NetBeans
            IDE](cdi-adv-examples002.htm#GKHQU)
          - [26.2.3.3 To Build, Package, and Deploy the encoder Example
            Using Maven](cdi-adv-examples002.htm#GKHQL)
          - [26.2.3.4 To Run the encoder Example Using
            Maven](cdi-adv-examples002.htm#GKHOL)
  - [26.3 The producermethods Example: Using a Producer Method to Choose
    a Bean Implementation](cdi-adv-examples003.htm#GKHPY)
      - [26.3.1 Components of the producermethods
        Example](cdi-adv-examples003.htm#GKHRO)
      - [26.3.2 Running the producermethods
        Example](cdi-adv-examples003.htm#GKHQE)
          - [26.3.2.1 To Build, Package, and Deploy the producermethods
            Example Using NetBeans IDE](cdi-adv-examples003.htm#GKHPE)
          - [26.3.2.2 To Build, Package, and Deploy the producermethods
            Example Using Maven](cdi-adv-examples003.htm#GKHPS)
          - [26.3.2.3 To Run the producermethods
            Example](cdi-adv-examples003.htm#GKHQG)
  - [26.4 The producerfields Example: Using Producer Fields to Generate
    Resources](cdi-adv-examples004.htm#GKHRG)
      - [26.4.1 The Producer Field for the producerfields
        Example](cdi-adv-examples004.htm#GKHPP)
      - [26.4.2 The producerfields Entity and Session
        Bean](cdi-adv-examples004.htm#GKHPD)
      - [26.4.3 The producerfields Facelets Pages and Managed
        Bean](cdi-adv-examples004.htm#GKHPF)
      - [26.4.4 Running the producerfields
        Example](cdi-adv-examples004.htm#GKHRH)
          - [26.4.4.1 To Build, Package, and Deploy the producerfields
            Example Using NetBeans IDE](cdi-adv-examples004.htm#GKHPB)
          - [26.4.4.2 To Build, Package, and Deploy the producerfields
            Example Using Maven](cdi-adv-examples004.htm#GKHRM)
          - [26.4.4.3 To Run the producerfields
            Example](cdi-adv-examples004.htm#GKHRR)
  - [26.5 The billpayment Example: Using Events and
    Interceptors](cdi-adv-examples005.htm#GKHPA)
      - [26.5.1 Overview of the billpayment
        Example](cdi-adv-examples005.htm#CHDIBGDF)
      - [26.5.2 The PaymentEvent Event
        Class](cdi-adv-examples005.htm#GKHOK)
      - [26.5.3 The PaymentHandler Event
        Listener](cdi-adv-examples005.htm#GKHRB)
      - [26.5.4 The billpayment Facelets Pages and Managed
        Bean](cdi-adv-examples005.htm#GKHRJ)
      - [26.5.5 The LoggedInterceptor Interceptor
        Class](cdi-adv-examples005.htm#GKHRQ)
      - [26.5.6 Running the billpayment
        Example](cdi-adv-examples005.htm#GKHPK)
          - [26.5.6.1 To Build, Package, and Deploy the billpayment
            Example Using NetBeans IDE](cdi-adv-examples005.htm#GKHQS)
          - [26.5.6.2 To Build, Package, and Deploy the billpayment
            Example Using Maven](cdi-adv-examples005.htm#GKHPX)
          - [26.5.6.3 To Run the billpayment
            Example](cdi-adv-examples005.htm#GKHPT)
  - [26.6 The decorators Example: Decorating a
    Bean](cdi-adv-examples006.htm#GKPAX)
      - [26.6.1 Overview of the decorators
        Example](cdi-adv-examples006.htm#CHDDDFCI)
      - [26.6.2 Components of the decorators
        Example](cdi-adv-examples006.htm#GKPAQ)
      - [26.6.3 Running the decorators
        Example](cdi-adv-examples006.htm#GKPBK)
          - [26.6.3.1 To Build, Package, and Deploy the decorators
            Example Using NetBeans IDE](cdi-adv-examples006.htm#GKPAG)
          - [26.6.3.2 To Build, Package, and Deploy the decorators
            Example Using Maven](cdi-adv-examples006.htm#GKPAJ)
          - [26.6.3.3 To Run the decorators
            Example](cdi-adv-examples006.htm#GKPAN)

## [Part VI Web Services](partwebsvcs.htm#BNAYK)

## [27 Introduction to Web Services](webservices-intro.htm#GIJTI)

  - [27.1 What Are Web Services?](webservices-intro001.htm#GIJVH)
  - [27.2 Types of Web Services](webservices-intro002.htm#GIQSX)
      - [27.2.1 "Big" Web Services](webservices-intro002.htm#GKCDG)
      - [27.2.2 RESTful Web Services](webservices-intro002.htm#GKCAW)
  - [27.3 Deciding Which Type of Web Service to
    Use](webservices-intro003.htm#GJBJI)

## [28 Building Web Services with JAX-WS](jaxws.htm#BNAYL)

  - [28.1 Overview of Java API for XML Web
    Services](jaxws001.htm#A1250966)
  - [28.2 Creating a Simple Web Service and Clients with
    JAX-WS](jaxws002.htm#BNAYN)
      - [28.2.1 Basic Steps for Creating a Web Service and
        Client](jaxws002.htm#sthref131)
      - [28.2.2 Requirements of a JAX-WS Endpoint](jaxws002.htm#BNAYP)
      - [28.2.3 Coding the Service Endpoint Implementation
        Class](jaxws002.htm#BNAYQ)
      - [28.2.4 Building, Packaging, and Deploying the
        Service](jaxws002.htm#BNAYR)
          - [28.2.4.1 To Build, Package, and Deploy the Service Using
            NetBeans IDE](jaxws002.htm#BNAYS)
          - [28.2.4.2 To Build, Package, and Deploy the Service Using
            Maven](jaxws002.htm#BNAYT)
      - [28.2.5 Testing the Methods of a Web Service
        Endpoint](jaxws002.htm#GKAJL)
          - [28.2.5.1 To Test the Service without a
            Client](jaxws002.htm#BNAYW)
      - [28.2.6 A Simple JAX-WS Application Client](jaxws002.htm#BNAYX)
          - [28.2.6.1 Coding the Application Client](jaxws002.htm#BNAYY)
          - [28.2.6.2 Running the Application
            Client](jaxws002.htm#BNAYZ)
      - [28.2.7 A Simple JAX-WS Web Client](jaxws002.htm#GJYGB)
          - [28.2.7.1 Coding the Servlet](jaxws002.htm#GJYFL)
          - [28.2.7.2 Running the Web Client](jaxws002.htm#GJYGE)
  - [28.3 Types Supported by JAX-WS](jaxws003.htm#BNAZC)
      - [28.3.1 Schema-to-Java Mapping](jaxws003.htm#BNAZT)
      - [28.3.2 Java-to-Schema Mapping](jaxws003.htm#BNAZW)
  - [28.4 Web Services Interoperability and JAX-WS](jaxws004.htm#BNAZD)
  - [28.5 Further Information about JAX-WS](jaxws005.htm#BNAZE)

## [29 Building RESTful Web Services with JAX-RS](jaxrs.htm#GIEPU)

  - [29.1 What Are RESTful Web Services?](jaxrs001.htm#GIJQY)
  - [29.2 Creating a RESTful Root Resource Class](jaxrs002.htm#GILIK)
      - [29.2.1 Developing RESTful Web Services with
        JAX-RS](jaxrs002.htm#GILRU)
      - [29.2.2 Overview of a JAX-RS Application](jaxrs002.htm#GILQB)
      - [29.2.3 The @Path Annotation and URI Path
        Templates](jaxrs002.htm#GINPW)
      - [29.2.4 Responding to HTTP Methods and
        Requests](jaxrs002.htm#GIPYS)
          - [29.2.4.1 The Request Method Designator
            Annotations](jaxrs002.htm#GIPXS)
          - [29.2.4.2 Using Entity Providers to Map HTTP Response and
            Request Entity Bodies](jaxrs002.htm#GIPZE)
      - [29.2.5 Using @Consumes and @Produces to Customize Requests and
        Responses](jaxrs002.htm#GIPZH)
          - [29.2.5.1 The @Produces Annotation](jaxrs002.htm#GIPXF)
          - [29.2.5.2 The @Consumes Annotation](jaxrs002.htm#GIPYT)
      - [29.2.6 Extracting Request Parameters](jaxrs002.htm#GIPYW)
      - [29.2.7 Configuring JAX-RS Applications](jaxrs002.htm#CIHEGAGI)
          - [29.2.7.1 Configuring a JAX-RS Application Using a Subclass
            of Application](jaxrs002.htm#CIHFEBJF)
          - [29.2.7.2 Configuring the Base URI in
            web.xml](jaxrs002.htm#CIHDHAIJ)
  - [29.3 Example Applications for JAX-RS](jaxrs003.htm#GIPZZ)
      - [29.3.1 Creating a Simple RESTful Web
        Service](jaxrs003.htm#GIPYZ)
          - [29.3.1.1 To Create a RESTful Web Service Using NetBeans
            IDE](jaxrs003.htm#GIQAA)
      - [29.3.2 The rsvp Example Application](jaxrs003.htm#GJVBC)
          - [29.3.2.1 Components of the rsvp Example
            Application](jaxrs003.htm#GJVAW)
          - [29.3.2.2 Running the rsvp Example
            Application](jaxrs003.htm#GKCCA)
      - [29.3.3 Real-World Examples](jaxrs003.htm#GIRCI)
  - [29.4 Further Information about
JAX-RS](jaxrs004.htm#GILIZ)

## [30 Accessing REST Resources with the JAX-RS Client API](jaxrs-client.htm#BABEIGIH)

  - [30.1 Overview of the Client API](jaxrs-client001.htm#BABBIHEJ)
      - [30.1.1 Creating a Basic Client Request Using the Client
        API](jaxrs-client001.htm#CHDFCABB)
      - [30.1.2 Obtaining the Client
        Instance](jaxrs-client001.htm#CHDHBFHJ)
      - [30.1.3 Setting the Client Target](jaxrs-client001.htm#CHDDCICC)
      - [30.1.4 Setting Path Parameters in
        Targets](jaxrs-client001.htm#CHDDBFCG)
      - [30.1.5 Invoking the Request](jaxrs-client001.htm#CHDEFCDB)
  - [30.2 Using the Client API in the JAX-RS Example
    Applications](jaxrs-client002.htm#BABJCIJC)
      - [30.2.1 The Client API in the rsvp Example
        Application](jaxrs-client002.htm#BABEDFIG)
      - [30.2.2 The Client API in the customer Example
        Application](jaxrs-client002.htm#CHDGBGID)
  - [30.3 Advanced Features of the Client
    API](jaxrs-client003.htm#BABCDDGH)
      - [30.3.1 Configuring the Client
        Request](jaxrs-client003.htm#CHDGBBCC)
          - [30.3.1.1 Setting Message Headers in the Client
            Request](jaxrs-client003.htm#CHDHAFBG)
          - [30.3.1.2 Setting Cookies in the Client
            Request](jaxrs-client003.htm#CHDHFFDJ)
          - [30.3.1.3 Adding Filters to the
            Client](jaxrs-client003.htm#CHDJEFID)
      - [30.3.2 Asynchronous Invocations in the Client
        API](jaxrs-client003.htm#CHDEBIGG)
          - [30.3.2.1 Using Custom Callbacks in Asynchronous
            Invocations](jaxrs-client003.htm#sthref138)

## [31 JAX-RS: Advanced Topics and an Example](jaxrs-advanced.htm#GJJXE)

  - [31.1 Annotations for Field and Bean Properties of Resource
    Classes](jaxrs-advanced001.htm#GKKRB)
      - [31.1.1 Extracting Path Parameters](jaxrs-advanced001.htm#GKKYA)
      - [31.1.2 Extracting Query
        Parameters](jaxrs-advanced001.htm#GKKXJ)
      - [31.1.3 Extracting Form Data](jaxrs-advanced001.htm#GKKYC)
      - [31.1.4 Extracting the Java Type of a Request or
        Response](jaxrs-advanced001.htm#GKLCQ)
  - [31.2 Validating Resource Data with Bean
    Validation](jaxrs-advanced002.htm#BABCJEDF)
      - [31.2.1 Using Constraint Annotations on Resource
        Methods](jaxrs-advanced002.htm#CIHJAFGI)
      - [31.2.2 Validating Entity Data](jaxrs-advanced002.htm#CIHFDCBI)
      - [31.2.3 Validation Exception Handling and Response
        Codes](jaxrs-advanced002.htm#CIHCHEFH)
  - [31.3 Subresources and Runtime Resource
    Resolution](jaxrs-advanced003.htm#GKNAV)
      - [31.3.1 Subresource Methods](jaxrs-advanced003.htm#GKLAG)
      - [31.3.2 Subresource Locators](jaxrs-advanced003.htm#GKRHR)
  - [31.4 Integrating JAX-RS with EJB Technology and
    CDI](jaxrs-advanced004.htm#GKNCY)
  - [31.5 Conditional HTTP Requests](jaxrs-advanced005.htm#GKQDA)
  - [31.6 Runtime Content Negotiation](jaxrs-advanced006.htm#GKQBQ)
  - [31.7 Using JAX-RS with JAXB](jaxrs-advanced007.htm#GKKNJ)
      - [31.7.1 Using Java Objects to Model Your
        Data](jaxrs-advanced007.htm#sthref140)
      - [31.7.2 Starting from an Existing XML Schema
        Definition](jaxrs-advanced007.htm#sthref141)
      - [31.7.3 Using JSON with JAX-RS and
        JAXB](jaxrs-advanced007.htm#sthref142)
  - [31.8 The customer Example Application](jaxrs-advanced008.htm#GKOIB)
      - [31.8.1 Overview of the customer Example
        Application](jaxrs-advanced008.htm#GKOFO)
      - [31.8.2 The Customer and Address Entity
        Classes](jaxrs-advanced008.htm#CIHJFEJI)
      - [31.8.3 The CustomerService Class](jaxrs-advanced008.htm#GKLGT)
      - [31.8.4 Using the JAX-RS Client in the CustomerBean
        Classes](jaxrs-advanced008.htm#GKQJQ)
      - [31.8.5 Running the customer
        Example](jaxrs-advanced008.htm#GKQKV)
          - [31.8.5.1 To Build, Package, and Deploy the customer Example
            Using NetBeans IDE](jaxrs-advanced008.htm#GKQLY)
          - [31.8.5.2 To Build, Package, and Deploy the customer Example
            Using Maven](jaxrs-advanced008.htm#GKQJV)

## [Part VII Enterprise Beans](partentbeans.htm#BNBLR)

## [32 Enterprise Beans](ejb-intro.htm#GIJSZ)

  - [32.1 What Is an Enterprise Bean?](ejb-intro001.htm#GIPMB)
      - [32.1.1 Benefits of Enterprise Beans](ejb-intro001.htm#GIPLK)
      - [32.1.2 When to Use Enterprise Beans](ejb-intro001.htm#GIPKN)
      - [32.1.3 Types of Enterprise Beans](ejb-intro001.htm#GIPNM)
  - [32.2 What Is a Session Bean?](ejb-intro002.htm#GIPJG)
      - [32.2.1 Types of Session Beans](ejb-intro002.htm#GIPKR)
          - [32.2.1.1 Stateful Session Beans](ejb-intro002.htm#GIPNL)
          - [32.2.1.2 Stateless Session Beans](ejb-intro002.htm#GIPIN)
          - [32.2.1.3 Singleton Session Beans](ejb-intro002.htm#GIPIM)
      - [32.2.2 When to Use Session Beans](ejb-intro002.htm#GIPMT)
  - [32.3 What Is a Message-Driven Bean?](ejb-intro003.htm#GIPKO)
      - [32.3.1 What Makes Message-Driven Beans Different from Session
        Beans?](ejb-intro003.htm#GIPMJ)
      - [32.3.2 When to Use Message-Driven
        Beans](ejb-intro003.htm#GIPJX)
  - [32.4 Accessing Enterprise Beans](ejb-intro004.htm#GIPJF)
      - [32.4.1 Using Enterprise Beans in
        Clients](ejb-intro004.htm#GIRFL)
          - [32.4.1.1 Portable JNDI Syntax](ejb-intro004.htm#GIRGN)
      - [32.4.2 Deciding on Remote or Local
        Access](ejb-intro004.htm#GIPIZ)
      - [32.4.3 Local Clients](ejb-intro004.htm#GIPMZ)
          - [32.4.3.1 Accessing Local Enterprise Beans Using the
            No-Interface View](ejb-intro004.htm#GIPSC)
          - [32.4.3.2 Accessing Local Enterprise Beans That Implement
            Business Interfaces](ejb-intro004.htm#GIPSE)
      - [32.4.4 Remote Clients](ejb-intro004.htm#GIPIU)
      - [32.4.5 Web Service Clients](ejb-intro004.htm#GIPKD)
      - [32.4.6 Method Parameters and Access](ejb-intro004.htm#GIPLY)
          - [32.4.6.1 Isolation](ejb-intro004.htm#GIPLX)
          - [32.4.6.2 Granularity of Accessed
            Data](ejb-intro004.htm#GIPKV)
  - [32.5 The Contents of an Enterprise Bean](ejb-intro005.htm#GIPIO)
  - [32.6 Naming Conventions for Enterprise
    Beans](ejb-intro006.htm#GIPKS)
  - [32.7 The Lifecycles of Enterprise Beans](ejb-intro007.htm#GIPLJ)
      - [32.7.1 The Lifecycle of a Stateful Session
        Bean](ejb-intro007.htm#GIPLN)
      - [32.7.2 The Lifecycle of a Stateless Session
        Bean](ejb-intro007.htm#GIPLM)
      - [32.7.3 The Lifecycle of a Singleton Session
        Bean](ejb-intro007.htm#GIPRX)
      - [32.7.4 The Lifecycle of a Message-Driven
        Bean](ejb-intro007.htm#GIPKW)
  - [32.8 Further Information about Enterprise
    Beans](ejb-intro008.htm#GIPLG)

## [33 Getting Started with Enterprise Beans](ejb-gettingstarted.htm#GIJRE)

  - [33.1 Starting With Enterprise
    Beans](ejb-gettingstarted001.htm#A1249349)
  - [33.2 Creating the Enterprise Bean](ejb-gettingstarted002.htm#GIPSS)
      - [33.2.1 Coding the Enterprise Bean
        Class](ejb-gettingstarted002.htm#GIPSX)
      - [33.2.2 Creating the converter Web
        Client](ejb-gettingstarted002.htm#GIPSI)
      - [33.2.3 Running the converter
        Example](ejb-gettingstarted002.htm#GIPVV)
          - [33.2.3.1 To Run the converter Example Using NetBeans
            IDE](ejb-gettingstarted002.htm#GIPUM)
          - [33.2.3.2 To Run the converter Example Using
            Maven](ejb-gettingstarted002.htm#GIPVQ)
  - [33.3 Modifying the Java EE
    Application](ejb-gettingstarted003.htm#GIPTI)
      - [33.3.1 To Modify a Class
File](ejb-gettingstarted003.htm#GIPUK)

## [34 Running the Enterprise Bean Examples](ejb-basicexamples.htm#GIJRB)

  - [34.1 Overview of the EJB
    Examples](ejb-basicexamples001.htm#A1250776)
  - [34.2 The cart Example](ejb-basicexamples002.htm#BNBOD)
      - [34.2.1 The Business Interface](ejb-basicexamples002.htm#BNBOE)
      - [34.2.2 Session Bean Class](ejb-basicexamples002.htm#BNBOF)
          - [34.2.2.1 Lifecycle Callback
            Methods](ejb-basicexamples002.htm#BNBOG)
          - [34.2.2.2 Business Methods](ejb-basicexamples002.htm#BNBOH)
      - [34.2.3 The @Remove Method](ejb-basicexamples002.htm#BNBOI)
      - [34.2.4 Helper Classes](ejb-basicexamples002.htm#BNBOJ)
      - [34.2.5 Running the cart
        Example](ejb-basicexamples002.htm#BNBOK)
          - [34.2.5.1 To Run the cart Example Using NetBeans
            IDE](ejb-basicexamples002.htm#BNBOL)
          - [34.2.5.2 To Run the cart Example Using
            Maven](ejb-basicexamples002.htm#BNBON)
  - [34.3 A Singleton Session Bean Example:
    counter](ejb-basicexamples003.htm#GIPVI)
      - [34.3.1 Creating a Singleton Session
        Bean](ejb-basicexamples003.htm#GIPVC)
          - [34.3.1.1 Initializing Singleton Session
            Beans](ejb-basicexamples003.htm#GIPPQ)
          - [34.3.1.2 Managing Concurrent Access in a Singleton Session
            Bean](ejb-basicexamples003.htm#GIPSZ)
          - [34.3.1.3 Handling Errors in a Singleton Session
            Bean](ejb-basicexamples003.htm#GIPVD)
      - [34.3.2 The Architecture of the counter
        Example](ejb-basicexamples003.htm#GIPXL)
      - [34.3.3 Running the counter
        Example](ejb-basicexamples003.htm#GIPVL)
          - [34.3.3.1 To Run the counter Example Using NetBeans
            IDE](ejb-basicexamples003.htm#GIPXT)
          - [34.3.3.2 To Run the counter Example Using
            Maven](ejb-basicexamples003.htm#GIPZW)
  - [34.4 A Web Service Example:
    helloservice](ejb-basicexamples004.htm#BNBOR)
      - [34.4.1 The Web Service Endpoint Implementation
        Class](ejb-basicexamples004.htm#BNBOS)
      - [34.4.2 Stateless Session Bean Implementation
        Class](ejb-basicexamples004.htm#BNBOT)
      - [34.4.3 Running the helloservice
        Example](ejb-basicexamples004.htm#BNBOU)
          - [34.4.3.1 To Build, Package, and Deploy the helloservice
            Example Using NetBeans IDE](ejb-basicexamples004.htm#BNBOV)
          - [34.4.3.2 To Build, Package, and Deploy the helloservice
            Example Using Maven](ejb-basicexamples004.htm#BNBOW)
          - [34.4.3.3 To Test the Service without a
            Client](ejb-basicexamples004.htm#BNBOX)
  - [34.5 Using the Timer Service](ejb-basicexamples005.htm#BNBOY)
      - [34.5.1 Creating Calendar-Based Timer
        Expressions](ejb-basicexamples005.htm#GIQLK)
          - [34.5.1.1 Specifying Multiple Values in Calendar
            Expressions](ejb-basicexamples005.htm#GIQMX)
      - [34.5.2 Programmatic Timers](ejb-basicexamples005.htm#GIQLT)
          - [34.5.2.1 The @Timeout
            Method](ejb-basicexamples005.htm#BNBOZ)
          - [34.5.2.2 Creating Programmatic
            Timers](ejb-basicexamples005.htm#BNBPA)
      - [34.5.3 Automatic Timers](ejb-basicexamples005.htm#GIQMB)
      - [34.5.4 Canceling and Saving
        Timers](ejb-basicexamples005.htm#BNBPB)
      - [34.5.5 Getting Timer
        Information](ejb-basicexamples005.htm#BNBPC)
      - [34.5.6 Transactions and Timers](ejb-basicexamples005.htm#BNBPD)
      - [34.5.7 The timersession
        Example](ejb-basicexamples005.htm#BNBPE)
      - [34.5.8 Running the timersession
        Example](ejb-basicexamples005.htm#BNBPF)
          - [34.5.8.1 To Run the timersession Example Using NetBeans
            IDE](ejb-basicexamples005.htm#GIQNI)
          - [34.5.8.2 To Build, Package, and Deploy the timersession
            Example Using Maven](ejb-basicexamples005.htm#GIQNQ)
          - [34.5.8.3 To Run the Web
            Client](ejb-basicexamples005.htm#GIQOP)
  - [34.6 Handling
Exceptions](ejb-basicexamples006.htm#BNBPJ)

## [35 Using the Embedded Enterprise Bean Container](ejb-embedded.htm#GKCQZ)

  - [35.1 Overview of the Embedded Enterprise Bean
    Container](ejb-embedded001.htm#GKFAE)
  - [35.2 Developing Embeddable Enterprise Bean
    Applications](ejb-embedded002.htm#GKCRR)
      - [35.2.1 Running Embedded
        Applications](ejb-embedded002.htm#GKCQI)
      - [35.2.2 Creating the Enterprise Bean
        Container](ejb-embedded002.htm#GKCOV)
          - [35.2.2.1 Explicitly Specifying Enterprise Bean Modules to
            Be Initialized](ejb-embedded002.htm#GKCRP)
      - [35.2.3 Looking Up Session Bean
        References](ejb-embedded002.htm#GLHUR)
      - [35.2.4 Shutting Down the Enterprise Bean
        Container](ejb-embedded002.htm#GKCRE)
  - [35.3 The standalone Example Application](ejb-embedded003.htm#GKCPV)
      - [35.3.1 Overview of the standalone Example
        Application](ejb-embedded003.htm#BEIDAJAC)
      - [35.3.2 To Run the standalone Example Application Using NetBeans
        IDE](ejb-embedded003.htm#GKCQP)
      - [35.3.3 To Run the standalone Example Application Using
        Maven](ejb-embedded003.htm#BEIGHEHJ)

## [36 Using Asynchronous Method Invocation in Session Beans](ejb-async.htm#GKIDZ)

  - [36.1 Asynchronous Method Invocation](ejb-async001.htm#GKKQG)
      - [36.1.1 Creating an Asynchronous Business
        Method](ejb-async001.htm#GKIFJ)
      - [36.1.2 Calling Asynchronous Methods from Enterprise Bean
        Clients](ejb-async001.htm#GKIEM)
          - [36.1.2.1 Retrieving the Final Result from an Asynchronous
            Method Invocation](ejb-async001.htm#GKICM)
          - [36.1.2.2 Cancelling an Asynchronous Method
            Invocation](ejb-async001.htm#GKIDB)
          - [36.1.2.3 Checking the Status of an Asynchronous Method
            Invocation](ejb-async001.htm#GKIEV)
  - [36.2 The async Example Application](ejb-async002.htm#GKIEZ)
      - [36.2.1 Architecture of the async-war
        Module](ejb-async002.htm#GKIQJ)
      - [36.2.2 Running the async Example](ejb-async002.htm#sthref151)
          - [36.2.2.1 To Run the async Example Application Using
            NetBeans IDE](ejb-async002.htm#GKINW)
          - [36.2.2.2 To Run the async Example Application Using
            Maven](ejb-async002.htm#GKRFB)

## [Part VIII Persistence](partpersist.htm#BNBPY)

## [37 Introduction to the Java Persistence API](persistence-intro.htm#BNBPZ)

  - [37.1 Overview of the Java Persistence
    API](persistence-intro001.htm#A1019685)
  - [37.2 Entities](persistence-intro002.htm#BNBQA)
      - [37.2.1 Requirements for Entity
        Classes](persistence-intro002.htm#BNBQB)
      - [37.2.2 Persistent Fields and Properties in Entity
        Classes](persistence-intro002.htm#BNBQC)
          - [37.2.2.1 Persistent Fields](persistence-intro002.htm#BNBQD)
          - [37.2.2.2 Persistent
            Properties](persistence-intro002.htm#BNBQE)
          - [37.2.2.3 Using Collections in Entity Fields and
            Properties](persistence-intro002.htm#GIQVN)
          - [37.2.2.4 Validating Persistent Fields and
            Properties](persistence-intro002.htm#GKAHQ)
      - [37.2.3 Primary Keys in
        Entities](persistence-intro002.htm#BNBQF)
      - [37.2.4 Multiplicity in Entity
        Relationships](persistence-intro002.htm#BNBQH)
      - [37.2.5 Direction in Entity
        Relationships](persistence-intro002.htm#BNBQI)
          - [37.2.5.1 Bidirectional
            Relationships](persistence-intro002.htm#BNBQJ)
          - [37.2.5.2 Unidirectional
            Relationships](persistence-intro002.htm#BNBQK)
          - [37.2.5.3 Queries and Relationship
            Direction](persistence-intro002.htm#BNBQL)
          - [37.2.5.4 Cascade Operations and
            Relationships](persistence-intro002.htm#BNBQM)
          - [37.2.5.5 Orphan Removal in
            Relationships](persistence-intro002.htm#GIQXY)
      - [37.2.6 Embeddable Classes in
        Entities](persistence-intro002.htm#GJIWZ)
  - [37.3 Entity Inheritance](persistence-intro003.htm#BNBQN)
      - [37.3.1 Abstract Entities](persistence-intro003.htm#BNBQO)
      - [37.3.2 Mapped Superclasses](persistence-intro003.htm#BNBQP)
      - [37.3.3 Non-Entity Superclasses](persistence-intro003.htm#BNBQQ)
      - [37.3.4 Entity Inheritance Mapping
        Strategies](persistence-intro003.htm#BNBQR)
          - [37.3.4.1 The Single Table per Class Hierarchy
            Strategy](persistence-intro003.htm#BNBQS)
          - [37.3.4.2 The Table per Concrete Class
            Strategy](persistence-intro003.htm#BNBQU)
          - [37.3.4.3 The Joined Subclass
            Strategy](persistence-intro003.htm#BNBQV)
  - [37.4 Managing Entities](persistence-intro004.htm#BNBQW)
      - [37.4.1 The EntityManager
        Interface](persistence-intro004.htm#BNBQY)
          - [37.4.1.1 Container-Managed Entity
            Managers](persistence-intro004.htm#BNBQZ)
          - [37.4.1.2 Application-Managed Entity
            Managers](persistence-intro004.htm#BNBRA)
          - [37.4.1.3 Finding Entities Using the
            EntityManager](persistence-intro004.htm#BNBRB)
          - [37.4.1.4 Managing an Entity Instance's
            Lifecycle](persistence-intro004.htm#BNBRC)
          - [37.4.1.5 Persisting Entity
            Instances](persistence-intro004.htm#BNBRD)
          - [37.4.1.6 Removing Entity
            Instances](persistence-intro004.htm#BNBRE)
          - [37.4.1.7 Synchronizing Entity Data to the
            Database](persistence-intro004.htm#BNBRF)
      - [37.4.2 Persistence Units](persistence-intro004.htm#BNBRJ)
  - [37.5 Querying Entities](persistence-intro005.htm#GJISE)
  - [37.6 Database Schema Creation](persistence-intro006.htm#CHDBEGIC)
      - [37.6.1 Configuring an Application to Create or Drop Database
        Tables](persistence-intro006.htm#sthref154)
      - [37.6.2 Loading Data Using SQL
        Scripts](persistence-intro006.htm#sthref159)
  - [37.7 Further Information about
    Persistence](persistence-intro007.htm#GKCLC)

## [38 Running the Persistence Examples](persistence-basicexamples.htm#GIJST)

  - [38.1 Overview of the Persistence
    Examples](persistence-basicexamples001.htm#A1023268)
  - [38.2 The order Application](persistence-basicexamples002.htm#GIQST)
      - [38.2.1 Entity Relationships in the order
        Application](persistence-basicexamples002.htm#GIQRH)
          - [38.2.1.1 Self-Referential
            Relationships](persistence-basicexamples002.htm#GIQQR)
          - [38.2.1.2 One-to-One
            Relationships](persistence-basicexamples002.htm#GIQSR)
          - [38.2.1.3 One-to-Many Relationship Mapped to Overlapping
            Primary and Foreign
            Keys](persistence-basicexamples002.htm#GIQTJ)
          - [38.2.1.4 Unidirectional
            Relationships](persistence-basicexamples002.htm#GIQUD)
      - [38.2.2 Primary Keys in the order
        Application](persistence-basicexamples002.htm#GIQQY)
          - [38.2.2.1 Generated Primary
            Keys](persistence-basicexamples002.htm#GIQUV)
          - [38.2.2.2 Compound Primary
            Keys](persistence-basicexamples002.htm#GIQUF)
      - [38.2.3 Entity Mapped to More Than One Database
        Table](persistence-basicexamples002.htm#GIQTL)
      - [38.2.4 Cascade Operations in the order
        Application](persistence-basicexamples002.htm#GIQUE)
      - [38.2.5 BLOB and CLOB Database Types in the order
        Application](persistence-basicexamples002.htm#GIQSC)
      - [38.2.6 Temporal Types in the order
        Application](persistence-basicexamples002.htm#GIQUM)
      - [38.2.7 Managing the order Application's
        Entities](persistence-basicexamples002.htm#GIQQV)
          - [38.2.7.1 Creating
            Entities](persistence-basicexamples002.htm#GIQRR)
          - [38.2.7.2 Finding
            Entities](persistence-basicexamples002.htm#GIQQC)
          - [38.2.7.3 Setting Entity
            Relationships](persistence-basicexamples002.htm#GIQUK)
          - [38.2.7.4 Using
            Queries](persistence-basicexamples002.htm#GIQSV)
          - [38.2.7.5 Removing
            Entities](persistence-basicexamples002.htm#GIQTW)
      - [38.2.8 Running the order
        Example](persistence-basicexamples002.htm#GIQUP)
          - [38.2.8.1 To Run the order Example Using NetBeans
            IDE](persistence-basicexamples002.htm#GIQSG)
          - [38.2.8.2 To Run the order Example Using
            Maven](persistence-basicexamples002.htm#GIQTY)
  - [38.3 The roster
    Application](persistence-basicexamples003.htm#GIQSQ)
      - [38.3.1 Relationships in the roster
        Application](persistence-basicexamples003.htm#GIQSO)
          - [38.3.1.1 The Many-To-Many Relationship in
            roster](persistence-basicexamples003.htm#GIQQK)
      - [38.3.2 Entity Inheritance in the roster
        Application](persistence-basicexamples003.htm#GIQRF)
      - [38.3.3 Criteria Queries in the roster
        Application](persistence-basicexamples003.htm#GJJFL)
          - [38.3.3.1 Metamodel Classes in the roster
            Application](persistence-basicexamples003.htm#GJJEX)
          - [38.3.3.2 Obtaining a CriteriaBuilder Instance in
            RequestBean](persistence-basicexamples003.htm#GJJFN)
          - [38.3.3.3 Creating Criteria Queries in RequestBean's
            Business Methods](persistence-basicexamples003.htm#GJJFF)
      - [38.3.4 Automatic Table Generation in the roster
        Application](persistence-basicexamples003.htm#GIQRX)
      - [38.3.5 Running the roster
        Example](persistence-basicexamples003.htm#GIQUZ)
          - [38.3.5.1 To Run the roster Example Using NetBeans
            IDE](persistence-basicexamples003.htm#GIQUG)
          - [38.3.5.2 To Run the roster Example Using
            Maven](persistence-basicexamples003.htm#GIQSJ)
  - [38.4 The address-book
    Application](persistence-basicexamples004.htm#GKANQ)
      - [38.4.1 Bean Validation Constraints in
        address-book](persistence-basicexamples004.htm#GKAOJ)
      - [38.4.2 Specifying Error Messages for Constraints in
        address-book](persistence-basicexamples004.htm#GKANL)
      - [38.4.3 Validating Contact Input from a JavaServer Faces
        Application](persistence-basicexamples004.htm#GKAON)
      - [38.4.4 Running the address-book
        Example](persistence-basicexamples004.htm#GKAOP)
          - [38.4.4.1 To Run the address-book Example Using NetBeans
            IDE](persistence-basicexamples004.htm#GKAOD)
          - [38.4.4.2 To Run the address-book Example Using
            Maven](persistence-basicexamples004.htm#GKANZ)

## [39 The Java Persistence Query Language](persistence-querylanguage.htm#BNBTG)

  - [39.1 Overview of the Java Persistence Query
    Language](persistence-querylanguage001.htm#A1073303)
  - [39.2 Query Language
    Terminology](persistence-querylanguage002.htm#BNBTH)
  - [39.3 Creating Queries Using the Java Persistence Query
    Language](persistence-querylanguage003.htm#BNBRG)
      - [39.3.1 Named Parameters in
        Queries](persistence-querylanguage003.htm#BNBRH)
      - [39.3.2 Positional Parameters in
        Queries](persistence-querylanguage003.htm#BNBRI)
  - [39.4 Simplified Query Language
    Syntax](persistence-querylanguage004.htm#BNBTI)
      - [39.4.1 Select
        Statements](persistence-querylanguage004.htm#BNBTJ)
      - [39.4.2 Update and Delete
        Statements](persistence-querylanguage004.htm#BNBTK)
  - [39.5 Example Queries](persistence-querylanguage005.htm#BNBTL)
      - [39.5.1 Simple Queries](persistence-querylanguage005.htm#BNBTM)
          - [39.5.1.1 A Basic Select
            Query](persistence-querylanguage005.htm#BNBTN)
          - [39.5.1.2 Eliminating Duplicate
            Values](persistence-querylanguage005.htm#BNBTO)
          - [39.5.1.3 Using Named
            Parameters](persistence-querylanguage005.htm#BNBTP)
      - [39.5.2 Queries That Navigate to Related
        Entities](persistence-querylanguage005.htm#BNBTQ)
          - [39.5.2.1 A Simple Query with
            Relationships](persistence-querylanguage005.htm#BNBTR)
          - [39.5.2.2 Navigating to Single-Valued Relationship
            Fields](persistence-querylanguage005.htm#BNBTS)
          - [39.5.2.3 Traversing Relationships with an Input
            Parameter](persistence-querylanguage005.htm#BNBTT)
          - [39.5.2.4 Traversing Multiple
            Relationships](persistence-querylanguage005.htm#BNBTU)
          - [39.5.2.5 Navigating According to Related
            Fields](persistence-querylanguage005.htm#BNBTV)
      - [39.5.3 Queries with Other Conditional
        Expressions](persistence-querylanguage005.htm#BNBTW)
          - [39.5.3.1 The LIKE
            Expression](persistence-querylanguage005.htm#BNBTX)
          - [39.5.3.2 The IS NULL
            Expression](persistence-querylanguage005.htm#BNBTY)
          - [39.5.3.3 The IS EMPTY
            Expression](persistence-querylanguage005.htm#BNBTZ)
          - [39.5.3.4 The BETWEEN
            Expression](persistence-querylanguage005.htm#BNBUA)
          - [39.5.3.5 Comparison
            Operators](persistence-querylanguage005.htm#BNBUB)
      - [39.5.4 Bulk Updates and
        Deletes](persistence-querylanguage005.htm#BNBUC)
          - [39.5.4.1 Update
            Queries](persistence-querylanguage005.htm#BNBUD)
          - [39.5.4.2 Delete
            Queries](persistence-querylanguage005.htm#BNBUE)
  - [39.6 Full Query Language
    Syntax](persistence-querylanguage006.htm#BNBUF)
      - [39.6.1 BNF Symbols](persistence-querylanguage006.htm#BNBUG)
      - [39.6.2 BNF Grammar of the Java Persistence Query
        Language](persistence-querylanguage006.htm#BNBUI)
      - [39.6.3 FROM Clause](persistence-querylanguage006.htm#BNBUJ)
          - [39.6.3.1
            Identifiers](persistence-querylanguage006.htm#BNBUK)
          - [39.6.3.2 Identification
            Variables](persistence-querylanguage006.htm#BNBUM)
          - [39.6.3.3 Range Variable
            Declarations](persistence-querylanguage006.htm#BNBUN)
          - [39.6.3.4 Collection Member
            Declarations](persistence-querylanguage006.htm#BNBUO)
          - [39.6.3.5 Joins](persistence-querylanguage006.htm#BNBUP)
      - [39.6.4 Path
        Expressions](persistence-querylanguage006.htm#BNBUQ)
          - [39.6.4.1 Examples of Path
            Expressions](persistence-querylanguage006.htm#BNBUR)
          - [39.6.4.2 Expression
            Types](persistence-querylanguage006.htm#BNBUS)
          - [39.6.4.3
            Navigation](persistence-querylanguage006.htm#BNBUT)
      - [39.6.5 WHERE Clause](persistence-querylanguage006.htm#BNBUU)
          - [39.6.5.1 Literals](persistence-querylanguage006.htm#BNBUV)
          - [39.6.5.2 Input
            Parameters](persistence-querylanguage006.htm#BNBVA)
          - [39.6.5.3 Conditional
            Expressions](persistence-querylanguage006.htm#BNBVB)
          - [39.6.5.4 Operators and Their
            Precedence](persistence-querylanguage006.htm#BNBVC)
          - [39.6.5.5 BETWEEN
            Expressions](persistence-querylanguage006.htm#BNBVE)
          - [39.6.5.6 IN
            Expressions](persistence-querylanguage006.htm#BNBVF)
          - [39.6.5.7 LIKE
            Expressions](persistence-querylanguage006.htm#BNBVG)
          - [39.6.5.8 NULL Comparison
            Expressions](persistence-querylanguage006.htm#BNBVI)
          - [39.6.5.9 Empty Collection Comparison
            Expressions](persistence-querylanguage006.htm#BNBVJ)
          - [39.6.5.10 Collection Member
            Expressions](persistence-querylanguage006.htm#BNBVK)
          - [39.6.5.11
            Subqueries](persistence-querylanguage006.htm#BNBVL)
          - [39.6.5.12 Functional
            Expressions](persistence-querylanguage006.htm#BNBVO)
          - [39.6.5.13 Case
            Expressions](persistence-querylanguage006.htm#GJJND)
          - [39.6.5.14 NULL
            Values](persistence-querylanguage006.htm#BNBVR)
          - [39.6.5.15 Equality
            Semantics](persistence-querylanguage006.htm#BNBVU)
      - [39.6.6 SELECT Clause](persistence-querylanguage006.htm#BNBVX)
          - [39.6.6.1 Return
            Types](persistence-querylanguage006.htm#BNBVY)
          - [39.6.6.2 The DISTINCT
            Keyword](persistence-querylanguage006.htm#BNBWB)
          - [39.6.6.3 Constructor
            Expressions](persistence-querylanguage006.htm#BNBWC)
      - [39.6.7 ORDER BY Clause](persistence-querylanguage006.htm#BNBWD)
      - [39.6.8 GROUP BY and HAVING
        Clauses](persistence-querylanguage006.htm#BNBWE)

## [40 Using the Criteria API to Create Queries](persistence-criteria.htm#GJITV)

  - [40.1 Overview of the Criteria and Metamodel
    APIs](persistence-criteria001.htm#GJRIJ)
  - [40.2 Using the Metamodel API to Model Entity
    Classes](persistence-criteria002.htm#GJIUP)
      - [40.2.1 Using Metamodel
        Classes](persistence-criteria002.htm#GJIVL)
  - [40.3 Using the Criteria API and Metamodel API to Create Basic
    Typesafe Queries](persistence-criteria003.htm#GJIVM)
      - [40.3.1 Creating a Criteria
        Query](persistence-criteria003.htm#GJIVS)
      - [40.3.2 Query Roots](persistence-criteria003.htm#GJIVQ)
      - [40.3.3 Querying Relationships Using
        Joins](persistence-criteria003.htm#GJIUV)
      - [40.3.4 Path Navigation in Criteria
        Queries](persistence-criteria003.htm#GJIVE)
      - [40.3.5 Restricting Criteria Query
        Results](persistence-criteria003.htm#GJIVI)
          - [40.3.5.1 The Expression Interface
            Methods](persistence-criteria003.htm#GJIWN)
          - [40.3.5.2 Expression Methods in the CriteriaBuilder
            Interface](persistence-criteria003.htm#GJIXA)
      - [40.3.6 Managing Criteria Query
        Results](persistence-criteria003.htm#GJIXE)
          - [40.3.6.1 Ordering
            Results](persistence-criteria003.htm#GJIWO)
          - [40.3.6.2 Grouping
            Results](persistence-criteria003.htm#GJIXG)
      - [40.3.7 Executing Queries](persistence-criteria003.htm#GJIVY)
          - [40.3.7.1 Single-Valued Query
            Results](persistence-criteria003.htm#GJIUR)
          - [40.3.7.2 Collection-Valued Query
            Results](persistence-criteria003.htm#GJIVP)

## [41 Creating and Using String-Based Criteria Queries](persistence-string-queries.htm#GKJIQ)

  - [41.1 Overview of String-Based Criteria API
    Queries](persistence-string-queries001.htm#GKJIV)
  - [41.2 Creating String-Based
    Queries](persistence-string-queries002.htm#GKJBQ)
  - [41.3 Executing String-Based
    Queries](persistence-string-queries003.htm#GKJDB)

## [42 Controlling Concurrent Access to Entity Data with Locking](persistence-locking.htm#GKJJF)

  - [42.1 Overview of Entity Locking and
    Concurrency](persistence-locking001.htm#GKJHZ)
      - [42.1.1 Using Optimistic
        Locking](persistence-locking001.htm#GKJJC)
  - [42.2 Lock Modes](persistence-locking002.htm#GKJIU)
      - [42.2.1 Setting the Lock Mode](persistence-locking002.htm#GKJIK)
      - [42.2.2 Using Pessimistic
        Locking](persistence-locking002.htm#GKJIL)
          - [42.2.2.1 Pessimistic Locking
            Timeouts](persistence-locking002.htm#GKJLQ)

## [43 Creating Fetch Plans with Entity Graphs](persistence-entitygraphs.htm#BABIJIAC)

  - [43.1 Overview of Using Fetch Plans and Entity
    Graphs](persistence-entitygraphs001.htm#A1153411)
  - [43.2 Entity Graph Basics](persistence-entitygraphs002.htm#BABCJBCG)
      - [43.2.1 The Default Entity
        Graph](persistence-entitygraphs002.htm#sthref177)
      - [43.2.2 Using Entity Graphs in Persistence
        Operations](persistence-entitygraphs002.htm#sthref178)
          - [43.2.2.1 Fetch
            Graphs](persistence-entitygraphs002.htm#BABGEFCG)
          - [43.2.2.2 Load
            Graphs](persistence-entitygraphs002.htm#BABHJBHG)
  - [43.3 Using Named Entity
    Graphs](persistence-entitygraphs003.htm#BABFIGEI)
      - [43.3.1 Applying Named Entity Graph Annotations to Entity
        Classes](persistence-entitygraphs003.htm#sthref179)
      - [43.3.2 Obtaining EntityGraph Instances from Named Entity
        Graphs](persistence-entitygraphs003.htm#sthref180)
  - [43.4 Using Entity Graphs in Query
    Operations](persistence-entitygraphs004.htm#BABGJDAJ)

## [44 Using a Second-Level Cache with Java Persistence API Applications](persistence-cache.htm#GKJIA)

  - [44.1 Overview of the Second-Level
    Cache](persistence-cache001.htm#GKJIO)
      - [44.1.1 Controlling whether Entities May Be
        Cached](persistence-cache001.htm#GKJIW)
  - [44.2 Specifying the Cache Mode Settings to Improve
    Performance](persistence-cache002.htm#GKJJJ)
      - [44.2.1 Setting the Cache Retrieval and Store
        Modes](persistence-cache002.htm#GKJDK)
          - [44.2.1.1 Cache Retrieval
            Mode](persistence-cache002.htm#GKJDR)
          - [44.2.1.2 Cache Store Mode](persistence-cache002.htm#GKJDD)
          - [44.2.1.3 Setting the Cache Retrieval or Store
            Mode](persistence-cache002.htm#GKJDS)
      - [44.2.2 Controlling the Second-Level Cache
        Programmatically](persistence-cache002.htm#GKJEB)
          - [44.2.2.1 Overview of the javax.persistence.Cache
            Interface](persistence-cache002.htm#CHDEECCF)
          - [44.2.2.2 Checking whether an Entity's Data Is
            Cached](persistence-cache002.htm#GKJDZ)
          - [44.2.2.3 Removing an Entity from the
            Cache](persistence-cache002.htm#GKJDQ)
          - [44.2.2.4 Removing All Data from the
            Cache](persistence-cache002.htm#GKJDA)

## [Part IX Messaging](partmessaging.htm#GFIRP3)

## [45 Java Message Service Concepts](jms-concepts.htm#BNCDQ)

  - [45.1 Overview of the JMS API](jms-concepts001.htm#BNCDR)
      - [45.1.1 What Is Messaging?](jms-concepts001.htm#BNCDS)
      - [45.1.2 What Is the JMS API?](jms-concepts001.htm#BNCDT)
      - [45.1.3 When Can You Use the JMS
        API?](jms-concepts001.htm#BNCDU)
      - [45.1.4 How Does the JMS API Work with the Java EE
        Platform?](jms-concepts001.htm#BNCDW)
  - [45.2 Basic JMS API Concepts](jms-concepts002.htm#BNCDX)
      - [45.2.1 JMS API Architecture](jms-concepts002.htm#BNCDY)
      - [45.2.2 Messaging Styles](jms-concepts002.htm#BNCEA)
          - [45.2.2.1 Point-to-Point Messaging
            Style](jms-concepts002.htm#BNCEB)
          - [45.2.2.2 Publish/Subscribe Messaging
            Style](jms-concepts002.htm#BNCED)
      - [45.2.3 Message Consumption](jms-concepts002.htm#BNCEG)
  - [45.3 The JMS API Programming Model](jms-concepts003.htm#BNCEH)
      - [45.3.1 JMS Administered Objects](jms-concepts003.htm#BNCEJ)
          - [45.3.1.1 JMS Connection
            Factories](jms-concepts003.htm#BNCEK)
          - [45.3.1.2 JMS Destinations](jms-concepts003.htm#BNCEL)
      - [45.3.2 Connections](jms-concepts003.htm#BNCEM)
      - [45.3.3 Sessions](jms-concepts003.htm#BNCEN)
      - [45.3.4 JMSContext Objects](jms-concepts003.htm#BABGDFEA)
      - [45.3.5 JMS Message Producers](jms-concepts003.htm#BNCEO)
      - [45.3.6 JMS Message Consumers](jms-concepts003.htm#BNCEP)
          - [45.3.6.1 JMS Message Listeners](jms-concepts003.htm#BNCEQ)
          - [45.3.6.2 JMS Message Selectors](jms-concepts003.htm#BNCER)
          - [45.3.6.3 Consuming Messages from
            Topics](jms-concepts003.htm#BABEEJJJ)
          - [45.3.6.4 Creating Durable
            Subscriptions](jms-concepts003.htm#BNCGD)
          - [45.3.6.5 Creating Shared
            Subscriptions](jms-concepts003.htm#BABJCIGJ)
      - [45.3.7 JMS Messages](jms-concepts003.htm#BNCES)
          - [45.3.7.1 Message Headers](jms-concepts003.htm#BNCET)
          - [45.3.7.2 Message Properties](jms-concepts003.htm#BNCEV)
          - [45.3.7.3 Message Bodies](jms-concepts003.htm#BNCEW)
      - [45.3.8 JMS Queue Browsers](jms-concepts003.htm#BNCEY)
      - [45.3.9 JMS Exception Handling](jms-concepts003.htm#BNCEZ)
  - [45.4 Using Advanced JMS Features](jms-concepts004.htm#BNCFU)
      - [45.4.1 Controlling Message
        Acknowledgment](jms-concepts004.htm#BNCFW)
      - [45.4.2 Specifying Options for Sending
        Messages](jms-concepts004.htm#BNCFV)
          - [45.4.2.1 Specifying Message
            Persistence](jms-concepts004.htm#BNCFY)
          - [45.4.2.2 Setting Message Priority
            Levels](jms-concepts004.htm#BNCFZ)
          - [45.4.2.3 Allowing Messages to
            Expire](jms-concepts004.htm#BNCGA)
          - [45.4.2.4 Specifying a Delivery
            Delay](jms-concepts004.htm#BABGEADH)
          - [45.4.2.5 Using JMSProducer Method
            Chaining](jms-concepts004.htm#BABJFIAD)
      - [45.4.3 Creating Temporary
        Destinations](jms-concepts004.htm#BNCGB)
      - [45.4.4 Using JMS Local Transactions](jms-concepts004.htm#BNCGH)
      - [45.4.5 Sending Messages
        Asynchronously](jms-concepts004.htm#BABFIFAJ)
  - [45.5 Using the JMS API in Java EE
    Applications](jms-concepts005.htm#BNCGL)
      - [45.5.1 Overview of Using the JMS
        API](jms-concepts005.htm#CHDGICJB)
      - [45.5.2 Creating Resources for Java EE
        Applications](jms-concepts005.htm#BABHFBDH)
      - [45.5.3 Using Resource Injection in Enterprise Bean or Web
        Components](jms-concepts005.htm#BNCGM)
          - [45.5.3.1 Injecting a ConnectionFactory, Queue, or
            Topic](jms-concepts005.htm#CHDCHDIJ)
          - [45.5.3.2 Injecting a JMSContext
            Object](jms-concepts005.htm#BABCJBEE)
      - [45.5.4 Using Java EE Components to Produce and to Synchronously
        Receive Messages](jms-concepts005.htm#BNCGN)
          - [45.5.4.1 Managing JMS Resources in Web and EJB
            Components](jms-concepts005.htm#BNCGO)
          - [45.5.4.2 Managing Transactions in Session
            Beans](jms-concepts005.htm#BNCGP)
      - [45.5.5 Using Message-Driven Beans to Receive Messages
        Asynchronously](jms-concepts005.htm#BNCGQ)
      - [45.5.6 Managing JTA Transactions](jms-concepts005.htm#BNCGS)
  - [45.6 Further Information about JMS](jms-concepts006.htm#BNCGU)

## [46 Java Message Service Examples](jms-examples.htm#BNCGV)

  - [46.1 Building and Running Java Message Service
    Examples](jms-examples001.htm#A1251921)
  - [46.2 Overview of the JMS Examples](jms-examples002.htm#BABEFBHJ)
  - [46.3 Writing Simple JMS Applications](jms-examples003.htm#BNCFA)
      - [46.3.1 Overview of Writing Simple JMS
        Application](jms-examples003.htm#CHDCEFGA)
      - [46.3.2 Starting the JMS Provider](jms-examples003.htm#BNCFD)
      - [46.3.3 Creating JMS Administered
        Objects](jms-examples003.htm#GKTJS)
          - [46.3.3.1 To Create Resources for the Simple
            Examples](jms-examples003.htm#BABHEFCB)
      - [46.3.4 Building All the Simple
        Examples](jms-examples003.htm#BABEEABE)
          - [46.3.4.1 To Build All the Simple Examples Using NetBeans
            IDE](jms-examples003.htm#CHDJEJCD)
          - [46.3.4.2 To Build All the Simple Examples Using
            Maven](jms-examples003.htm#CHDGHJAA)
      - [46.3.5 Sending Messages](jms-examples003.htm#BABIHCAE)
          - [46.3.5.1 General Steps Performed in the
            Example](jms-examples003.htm#CHDGHJHH)
          - [46.3.5.2 The Producer.java
            Client](jms-examples003.htm#CHDFBABB)
          - [46.3.5.3 To Run the Producer
            Client](jms-examples003.htm#CHDHIIHE)
      - [46.3.6 Receiving Messages
        Synchronously](jms-examples003.htm#BNCFB)
          - [46.3.6.1 The SynchConsumer.java
            Client](jms-examples003.htm#BNCFC)
          - [46.3.6.2 To Run the SynchConsumer and Producer
            Clients](jms-examples003.htm#BNCFG)
      - [46.3.7 Using a Message Listener for Asynchronous Message
        Delivery](jms-examples003.htm#BNCFH)
          - [46.3.7.1 Writing the AsynchConsumer.java and
            TextListener.java Clients](jms-examples003.htm#BNCFI)
          - [46.3.7.2 To Run the AsynchConsumer and Producer
            Clients](jms-examples003.htm#BNCFK)
      - [46.3.8 Browsing Messages on a Queue](jms-examples003.htm#BNCFL)
          - [46.3.8.1 The MessageBrowser.java
            Client](jms-examples003.htm#BNCFM)
          - [46.3.8.2 To Run the QueueBrowser
            Client](jms-examples003.htm#BNCFN)
      - [46.3.9 Running Multiple Consumers on the Same
        Destination](jms-examples003.htm#BABDDHHC)
      - [46.3.10 Acknowledging Messages](jms-examples003.htm#BNCFX)
          - [46.3.10.1 To Run the ClientAckConsumer
            Client](jms-examples003.htm#GJSCG)
  - [46.4 Writing More Advanced JMS
    Applications](jms-examples004.htm#GIWFH)
      - [46.4.1 Using Durable Subscriptions](jms-examples004.htm#BNCGG)
          - [46.4.1.1 To Create Resources for the Durable Subscription
            Example](jms-examples004.htm#sthref199)
          - [46.4.1.2 To Run the Durable Subscription
            Example](jms-examples004.htm#GJSCI)
          - [46.4.1.3 To Run the unsubscriber
            Example](jms-examples004.htm#sthref200)
      - [46.4.2 Using Local Transactions](jms-examples004.htm#BNCGJ)
          - [46.4.2.1 To Create Resources for the transactedexample
            Example](jms-examples004.htm#sthref202)
          - [46.4.2.2 To Run the transactedexample
            Clients](jms-examples004.htm#GJSHA)
  - [46.5 Writing High Performance and Scalable JMS
    Applications](jms-examples005.htm#BABGEFHC)
      - [46.5.1 Using Shared Nondurable
        Subscriptions](jms-examples005.htm#BABIBEAC)
          - [46.5.1.1 Writing the Clients for the Shared Consumer
            Example](jms-examples005.htm#sthref203)
          - [46.5.1.2 To Run the SharedConsumer and Producer
            Clients](jms-examples005.htm#sthref204)
      - [46.5.2 Using Shared Durable
        Subscriptions](jms-examples005.htm#BABEJBHA)
          - [46.5.2.1 To Run the SharedDurableConsumer and Producer
            Clients](jms-examples005.htm#sthref205)
  - [46.6 Sending and Receiving Messages Using a Simple Web
    Application](jms-examples006.htm#BABBABFC)
      - [46.6.1 The websimplemessage Facelets
        Pages](jms-examples006.htm#sthref208)
      - [46.6.2 The websimplemessage Managed
        Beans](jms-examples006.htm#sthref209)
      - [46.6.3 Running the websimplemessage
        Example](jms-examples006.htm#sthref210)
          - [46.6.3.1 Creating Resources for the websimplemessage
            Example](jms-examples006.htm#CHDHEHAB)
          - [46.6.3.2 To Package and Deploy websimplemessage Using
            NetBeans IDE](jms-examples006.htm#CHDBADGA)
          - [46.6.3.3 To Package and Deploy websimplemessage Using
            Maven](jms-examples006.htm#CHDBBBEI)
          - [46.6.3.4 To Run the websimplemessage
            Example](jms-examples006.htm#CHDIFEHC)
  - [46.7 Receiving Messages Asynchronously Using a Message-Driven
    Bean](jms-examples007.htm#BNBPK)
      - [46.7.1 Overview of the simplemessage
        Example](jms-examples007.htm#BNBPL)
      - [46.7.2 The simplemessage Application
        Client](jms-examples007.htm#BNBPN)
      - [46.7.3 The simplemessage Message-Driven Bean
        Class](jms-examples007.htm#BNBPO)
          - [46.7.3.1 The onMessage Method](jms-examples007.htm#BNBPP)
      - [46.7.4 Running the simplemessage
        Example](jms-examples007.htm#BNBPQ)
          - [46.7.4.1 Creating Resources for the simplemessage
            Example](jms-examples007.htm#BNBPR)
          - [46.7.4.2 To Run the simplemessage Example Using NetBeans
            IDE](jms-examples007.htm#CHDFBDDA)
          - [46.7.4.3 To Run the simplemessage Example Using
            Maven](jms-examples007.htm#BNBPT)
  - [46.8 Sending Messages from a Session Bean to an
    MDB](jms-examples008.htm#BNCGW)
      - [46.8.1 Writing the Application Components for the
        clientsessionmdb Example](jms-examples008.htm#BNCGX)
          - [46.8.1.1 Coding the Application Client:
            MyAppClient.java](jms-examples008.htm#BNCGZ)
          - [46.8.1.2 Coding the Publisher Session
            Bean](jms-examples008.htm#BNCHA)
          - [46.8.1.3 Coding the Message-Driven Bean:
            MessageBean.java](jms-examples008.htm#BNCHB)
      - [46.8.2 Running the clientsessionmdb
        Example](jms-examples008.htm#CHDDFAHA)
          - [46.8.2.1 To Run clientsessionmdb Using NetBeans
            IDE](jms-examples008.htm#CHDGGAIB)
          - [46.8.2.2 To Run clientsessionmdb Using
            Maven](jms-examples008.htm#CHDDDHBE)
  - [46.9 Using an Entity to Join Messages from Two
    MDBs](jms-examples009.htm#BNCHF)
      - [46.9.1 Overview of the clientmdbentity Example
        Application](jms-examples009.htm#BNCHG)
      - [46.9.2 Writing the Application Components for the
        clientmdbentity Example](jms-examples009.htm#BNCHI)
          - [46.9.2.1 Coding the Application Client:
            HumanResourceClient.java](jms-examples009.htm#BNCHJ)
          - [46.9.2.2 Coding the Message-Driven Beans for the
            clientmdbentity Example](jms-examples009.htm#BNCHK)
          - [46.9.2.3 Coding the Entity Class for the clientmdbentity
            Example](jms-examples009.htm#BNCHL)
      - [46.9.3 Running the clientmdbentity
        Example](jms-examples009.htm#CHDEEDJH)
          - [46.9.3.1 To Run clientmdbentity Using NetBeans
            IDE](jms-examples009.htm#CHDIJDEE)
          - [46.9.3.2 To Run clientmdbentity Using
            Maven](jms-examples009.htm#CHDICHGH)
          - [46.9.3.3 Viewing the Application
            Output](jms-examples009.htm#CHDCDEEF)
  - [46.10 Using NetBeans IDE to Create JMS
    Resources](jms-examples010.htm#BABDFDJC)
      - [46.10.1 To Create JMS Resources Using NetBeans
        IDE](jms-examples010.htm#CHDFIJBJ)
      - [46.10.2 To Delete JMS Resources Using NetBeans
        IDE](jms-examples010.htm#CHDCFADI)

## [Part X Security](partsecurity.htm#GIJRP)

## [47 Introduction to Security in the Java EE Platform](security-intro.htm#BNBWJ)

  - [47.1 Overview of Java EE Security](security-intro001.htm#BNBWK)
      - [47.1.1 A Simple Application Security
        Walkthrough](security-intro001.htm#BNBWL)
          - [47.1.1.1 Step 1: Initial
            Request](security-intro001.htm#BNBWM)
          - [47.1.1.2 Step 2: Initial
            Authentication](security-intro001.htm#BNBWO)
          - [47.1.1.3 Step 3: URL
            Authorization](security-intro001.htm#BNBWQ)
          - [47.1.1.4 Step 4: Fulfilling the Original
            Request](security-intro001.htm#BNBWS)
          - [47.1.1.5 Step 5: Invoking Enterprise Bean Business
            Methods](security-intro001.htm#BNBWU)
      - [47.1.2 Features of a Security
        Mechanism](security-intro001.htm#BNBWW)
      - [47.1.3 Characteristics of Application
        Security](security-intro001.htm#BNBWX)
  - [47.2 Security Mechanisms](security-intro002.htm#BNBWY)
      - [47.2.1 Java SE Security
        Mechanisms](security-intro002.htm#BNBWZ)
      - [47.2.2 Java EE Security
        Mechanisms](security-intro002.htm#BNBXA)
          - [47.2.2.1 Application-Layer
            Security](security-intro002.htm#BNBXB)
          - [47.2.2.2 Transport-Layer
            Security](security-intro002.htm#BNBXC)
          - [47.2.2.3 Message-Layer
            Security](security-intro002.htm#BNBXD)
  - [47.3 Securing Containers](security-intro003.htm#BNBXE)
      - [47.3.1 Using Annotations to Specify Security
        Information](security-intro003.htm#BNBXG)
      - [47.3.2 Using Deployment Descriptors for Declarative
        Security](security-intro003.htm#BNBXF)
      - [47.3.3 Using Programmatic
        Security](security-intro003.htm#BNBXH)
  - [47.4 Securing GlassFish Server](security-intro004.htm#BNBXI)
  - [47.5 Working with Realms, Users, Groups, and
    Roles](security-intro005.htm#BNBXJ)
      - [47.5.1 What Are Realms, Users, Groups, and
        Roles?](security-intro005.htm#BNBXK)
          - [47.5.1.1 What Is a Realm?](security-intro005.htm#BNBXM)
          - [47.5.1.2 What Is a User?](security-intro005.htm#BNBXN)
          - [47.5.1.3 What Is a Group?](security-intro005.htm#BNBXO)
          - [47.5.1.4 What Is a Role?](security-intro005.htm#BNBXP)
          - [47.5.1.5 Some Other
            Terminology](security-intro005.htm#BNBXQ)
      - [47.5.2 Managing Users and Groups in GlassFish
        Server](security-intro005.htm#BNBXR)
          - [47.5.2.1 To Add Users to GlassFish
            Server](security-intro005.htm#BNBXS)
      - [47.5.3 Setting Up Security Roles](security-intro005.htm#BNBXU)
      - [47.5.4 Mapping Roles to Users and
        Groups](security-intro005.htm#BNBXV)
  - [47.6 Establishing a Secure Connection Using
    SSL](security-intro006.htm#BNBXW)
      - [47.6.1 Verifying and Configuring SSL
        Support](security-intro006.htm#BNBXX)
  - [47.7 Further Information about
    Security](security-intro007.htm#BNBYJ)

## [48 Getting Started Securing Web Applications](security-webtier.htm#BNCAS)

  - [48.1 Overview of Web Application
    Security](security-webtier001.htm#BNCAT)
  - [48.2 Securing Web Applications](security-webtier002.htm#GKBAA)
      - [48.2.1 Overview of Securing Web
        Applications](security-webtier002.htm#CHDBIBHI)
      - [48.2.2 Specifying Security
        Constraints](security-webtier002.htm#BNCBK)
          - [48.2.2.1 Specifying a Web Resource
            Collection](security-webtier002.htm#GJJCD)
          - [48.2.2.2 Specifying an Authorization
            Constraint](security-webtier002.htm#GJJCG)
          - [48.2.2.3 Specifying a Secure
            Connection](security-webtier002.htm#BNCBM)
          - [48.2.2.4 Specifying Security Constraints for
            Resources](security-webtier002.htm#BNCBL)
      - [48.2.3 Specifying Authentication
        Mechanisms](security-webtier002.htm#GKBSA)
          - [48.2.3.1 HTTP Basic
            Authentication](security-webtier002.htm#BNCBO)
          - [48.2.3.2 Form-Based
            Authentication](security-webtier002.htm#BNCBQ)
          - [48.2.3.3 Digest
            Authentication](security-webtier002.htm#BNCBW)
      - [48.2.4 Specifying an Authentication Mechanism in the Deployment
        Descriptor](security-webtier002.htm#BNCBN)
      - [48.2.5 Declaring Security Roles](security-webtier002.htm#BNCAV)
  - [48.3 Using Programmatic Security with Web
    Applications](security-webtier003.htm#GJIIE)
      - [48.3.1 Authenticating Users
        Programmatically](security-webtier003.htm#GIRCJ)
      - [48.3.2 Checking Caller Identity
        Programmatically](security-webtier003.htm#BNCBA)
      - [48.3.3 Example Code for Programmatic
        Security](security-webtier003.htm#GJJLQ)
      - [48.3.4 Declaring and Linking Role
        References](security-webtier003.htm#BNCBB)
  - [48.4 Examples: Securing Web
    Applications](security-webtier004.htm#BNCBX)
      - [48.4.1 Overview of Examples of Securing Web
        Applications](security-webtier004.htm#CHDEBCHG)
      - [48.4.2 To Set Up Your System for Running the Security
        Examples](security-webtier004.htm#GJJLK)
      - [48.4.3 The hello2-basicauth Example: Basic Authentication with
        a Servlet](security-webtier004.htm#BNCCK)
          - [48.4.3.1 Specifying Security for Basic Authentication Using
            Annotations](security-webtier004.htm#GJRMH)
          - [48.4.3.2 To Build, Package, and Deploy the hello2-basicauth
            Example Using NetBeans IDE](security-webtier004.htm#GJQYS)
          - [48.4.3.3 To Build, Package, and Deploy the hello2-basicauth
            Example Using Maven](security-webtier004.htm#GJQZH)
          - [48.4.3.4 To Run the hello2-basicauth
            Example](security-webtier004.htm#GJQZF)
      - [48.4.4 The hello1-formauth Example: Form-Based Authentication
        with a JavaServer Faces
        Application](security-webtier004.htm#BNCBY)
          - [48.4.4.1 Creating the Login Form and the Error
            Page](security-webtier004.htm#BNCCA)
          - [48.4.4.2 Specifying Security for the Form-Based
            Authentication Example](security-webtier004.htm#BNCCB)
          - [48.4.4.3 To Build, Package, and Deploy the hello1-formauth
            Example Using NetBeans IDE](security-webtier004.htm#GJRBA)
          - [48.4.4.4 To Build, Package, and Deploy the hello1-formauth
            Example Using Maven and the asadmin
            Command](security-webtier004.htm#GJRAZ)
          - [48.4.4.5 To Run the hello1-formauth
            Example](security-webtier004.htm#GJRAL)

## [49 Getting Started Securing Enterprise Applications](security-javaee.htm#BNBYK)

  - [49.1 Basic Security Tasks for Enterprise
    Applications](security-javaee001.htm#CACGIFHJ)
  - [49.2 Securing Enterprise Beans](security-javaee002.htm#BNBYL)
      - [49.2.1 Securing an Enterprise Bean Using Declarative
        Security](security-javaee002.htm#GJGDI)
          - [49.2.1.1 Specifying Authorized Users by Declaring Security
            Roles](security-javaee002.htm#GJGCQ)
          - [49.2.1.2 Specifying an Authentication Mechanism and Secure
            Connection](security-javaee002.htm#BNBYU)
      - [49.2.2 Securing an Enterprise Bean
        Programmatically](security-javaee002.htm#GJGCS)
          - [49.2.2.1 Accessing an Enterprise Bean Caller's Security
            Context](security-javaee002.htm#GJGCR)
      - [49.2.3 Propagating a Security Identity
        (Run-As)](security-javaee002.htm#BNBYR)
          - [49.2.3.1 Configuring a Component's Propagated Security
            Identity](security-javaee002.htm#BNBZB)
          - [49.2.3.2 Trust between
            Containers](security-javaee002.htm#BNBZC)
      - [49.2.4 Deploying Secure Enterprise
        Beans](security-javaee002.htm#BNBZG)
  - [49.3 Examples: Securing Enterprise
    Beans](security-javaee003.htm#GKBSZ)
      - [49.3.1 The cart-secure Example: Securing an Enterprise Bean
        with Declarative Security](security-javaee003.htm#BNBZK)
          - [49.3.1.1 Annotating the Bean](security-javaee003.htm#BNBZL)
          - [49.3.1.2 To Run the cart-secure Example Using NetBeans
            IDE](security-javaee003.htm#BNBZN)
          - [49.3.1.3 To Run the cart-secure Example Using
            Maven](security-javaee003.htm#BNBZO)
      - [49.3.2 The converter-secure Example: Securing an Enterprise
        Bean with Programmatic Security](security-javaee003.htm#BNCAA)
          - [49.3.2.1 Modifying
            ConverterBean](security-javaee003.htm#BNCAB)
          - [49.3.2.2 Modifying
            ConverterServlet](security-javaee003.htm#GKBSI)
          - [49.3.2.3 To Run the converter-secure Example Using NetBeans
            IDE](security-javaee003.htm#BNCAD)
          - [49.3.2.4 To Run the converter-secure Example Using
            Maven](security-javaee003.htm#BNCAE)
          - [49.3.2.5 To Run the converter-secure
            Example](security-javaee003.htm#GJTDP)

## [50 Java EE Security: Advanced Topics](security-advanced.htm#GJJWX)

  - [50.1 Working with Digital
    Certificates](security-advanced001.htm#BNBYB)
      - [50.1.1 Creating a Server
        Certificate](security-advanced001.htm#BNBYC)
          - [50.1.1.1 To Use keytool to Create a Server
            Certificate](security-advanced001.htm#GJRGY)
      - [50.1.2 Adding Users to the Certificate
        Realm](security-advanced001.htm#GLIFW)
      - [50.1.3 Using a Different Server Certificate with GlassFish
        Server](security-advanced001.htm#BNBYF)
          - [50.1.3.1 To Specify a Different Server
            Certificate](security-advanced001.htm#sthref223)
  - [50.2 Authentication Mechanisms](security-advanced002.htm#GLIEN)
      - [50.2.1 Client Authentication](security-advanced002.htm#GLIEQ)
      - [50.2.2 Mutual Authentication](security-advanced002.htm#GLIEL)
          - [50.2.2.1 Enabling Mutual Authentication over
            SSL](security-advanced002.htm#BNBYH)
          - [50.2.2.2 Creating a Client Certificate for Mutual
            Authentication](security-advanced002.htm#BNBYI)
  - [50.3 Using the JDBC Realm for User
    Authentication](security-advanced003.htm#BABEJJDE)
      - [50.3.1 To Configure a JDBC Authentication
        Realm](security-advanced003.htm#sthref226)
  - [50.4 Securing HTTP Resources](security-advanced004.htm#BABGEJJJ)
  - [50.5 Securing Application Clients](security-advanced005.htm#GLIGC)
      - [50.5.1 Using Login Modules](security-advanced005.htm#GLIDW)
      - [50.5.2 Using Programmatic
        Login](security-advanced005.htm#GLIHQ)
  - [50.6 Securing Enterprise Information Systems
    Applications](security-advanced006.htm#GLIFD)
      - [50.6.1 Overview of Securing Enterprise Information Systems
        Applications](security-advanced006.htm#BABBJHIC)
      - [50.6.2 Container-Managed
        Sign-On](security-advanced006.htm#GLIHL)
      - [50.6.3 Component-Managed
        Sign-On](security-advanced006.htm#GLIDP)
      - [50.6.4 Configuring Resource Adapter
        Security](security-advanced006.htm#GLIGS)
      - [50.6.5 Mapping an Application Principal to EIS
        Principals](security-advanced006.htm#GLIGW)
  - [50.7 Configuring Security Using Deployment
    Descriptors](security-advanced007.htm#GKHRL)
      - [50.7.1 Specifying Security for Basic Authentication in the
        Deployment Descriptor](security-advanced007.htm#BNCCM)
      - [50.7.2 Specifying Non-Default Principal-to-Role Mapping in the
        Deployment Descriptor](security-advanced007.htm#GKAFQ)
  - [50.8 Further Information about Advanced Security
    Topics](security-advanced008.htm#BABBGBBF)

## [Part XI Java EE Supporting Technologies](partsupporttechs.htm#GIJUE)

## [51 Transactions](transactions.htm#BNCIH)

  - [51.1 Overview of Transactions](transactions001.htm#A1024277)
  - [51.2 Transactions in Java EE
    Applications](transactions002.htm#GIJRG)
  - [51.3 What Is a Transaction?](transactions003.htm#BNCII)
  - [51.4 Container-Managed Transactions](transactions004.htm#BNCIJ)
      - [51.4.1 Transaction Attributes](transactions004.htm#BNCIK)
          - [51.4.1.1 Required Attribute](transactions004.htm#BNCIM)
          - [51.4.1.2 RequiresNew Attribute](transactions004.htm#BNCIN)
          - [51.4.1.3 Mandatory Attribute](transactions004.htm#BNCIO)
          - [51.4.1.4 NotSupported Attribute](transactions004.htm#BNCIP)
          - [51.4.1.5 Supports Attribute](transactions004.htm#BNCIQ)
          - [51.4.1.6 Never Attribute](transactions004.htm#BNCIR)
          - [51.4.1.7 Summary of Transaction
            Attributes](transactions004.htm#BNCIS)
          - [51.4.1.8 Setting Transaction
            Attributes](transactions004.htm#BNCIU)
      - [51.4.2 Rolling Back a Container-Managed
        Transaction](transactions004.htm#BNCIV)
      - [51.4.3 Synchronizing a Session Bean's Instance
        Variables](transactions004.htm#BNCIW)
      - [51.4.4 Methods Not Allowed in Container-Managed
        Transactions](transactions004.htm#BNCIX)
  - [51.5 Bean-Managed Transactions](transactions005.htm#BNCIY)
      - [51.5.1 JTA Transactions](transactions005.htm#BNCIZ)
      - [51.5.2 Returning without Committing](transactions005.htm#BNCJA)
      - [51.5.3 Methods Not Allowed in Bean-Managed
        Transactions](transactions005.htm#BNCJB)
  - [51.6 Transaction Timeouts](transactions006.htm#BNCJC)
      - [51.6.1 To Set a Transaction
        Timeout](transactions006.htm#sthref230)
  - [51.7 Updating Multiple Databases](transactions007.htm#BNCJD)
  - [51.8 Transactions in Web Components](transactions008.htm#BNCJG)
  - [51.9 Further Information about
    Transactions](transactions009.htm#GKCMI)

## [52 Resource Adapters and Contracts](resources.htm#BNCJH)

  - [52.1 What Is a Resource Adapter?](resources001.htm#GIPGL)
      - [52.1.1 Management Contracts](resources001.htm#GIPGY)
          - [52.1.1.1 Lifecycle Management](resources001.htm#GIPHT)
          - [52.1.1.2 Work Management Contract](resources001.htm#GIPIG)
      - [52.1.2 Generic Work Context Contract](resources001.htm#GIPMK)
      - [52.1.3 Outbound and Inbound Contracts](resources001.htm#GKCKI)
  - [52.2 Metadata Annotations](resources002.htm#GIRDD)
  - [52.3 Common Client Interface](resources003.htm#GIPJU)
  - [52.4 Using Resource Adapters with Contexts and Dependency Injection
    for Java EE (CDI)](resources004.htm#CHDJFIGB)
  - [52.5 Further Information about Resource
    Adapters](resources005.htm#BNCJW)

## [53 The Resource Adapter Examples](connectorexample.htm#GLODB)

  - [53.1 Overview of the Resource Adapter
    Examples](connectorexample001.htm#A1253757)
  - [53.2 The trading Example](connectorexample002.htm#CHDFHAID)
      - [53.2.1 Using the Outbound Resource
        Adapter](connectorexample002.htm#CHDFADJD)
      - [53.2.2 Implementing the Outbound Resource
        Adapter](connectorexample002.htm#sthref236)
      - [53.2.3 Running the trading
        Example](connectorexample002.htm#sthref239)
          - [53.2.3.1 To Run the trading Example Using NetBeans
            IDE](connectorexample002.htm#BABCHDDC)
          - [53.2.3.2 To Run the trading Example Using
            Maven](connectorexample002.htm#BABFJAAG)
  - [53.3 The traffic Example](connectorexample003.htm#CHDJEADB)
      - [53.3.1 Using the Inbound Resource
        Adapter](connectorexample003.htm#sthref241)
      - [53.3.2 Implementing the Inbound Resource
        Adapter](connectorexample003.htm#sthref242)
      - [53.3.3 Running the traffic
        Example](connectorexample003.htm#sthref245)
          - [53.3.3.1 To Run the traffic Example Using NetBeans
            IDE](connectorexample003.htm#BABIJJEH)
          - [53.3.3.2 To Run the traffic Example Using
            Maven](connectorexample003.htm#BABBBGBA)

## [54 Using Java EE Interceptors](interceptors.htm#GKEED)

  - [54.1 Overview of Interceptors](interceptors001.htm#GKIGQ)
      - [54.1.1 Interceptor Classes](interceptors001.htm#GKECK)
      - [54.1.2 Interceptor Lifecycle](interceptors001.htm#GKEDY)
      - [54.1.3 Interceptors and CDI](interceptors001.htm#GKHSN)
  - [54.2 Using Interceptors](interceptors002.htm#GKEDM)
      - [54.2.1 Intercepting Method
        Invocations](interceptors002.htm#GKECY)
          - [54.2.1.1 Using Multiple Method
            Interceptors](interceptors002.htm#GKHMH)
          - [54.2.1.2 Accessing Target Method Parameters from an
            Interceptor Class](interceptors002.htm#GKHOV)
      - [54.2.2 Intercepting Lifecycle Callback
        Events](interceptors002.htm#GKECR)
          - [54.2.2.1 Using AroundConstruct Interceptor
            Methods](interceptors002.htm#sthref247)
          - [54.2.2.2 Using Multiple Lifecycle Callback
            Interceptors](interceptors002.htm#GKHNI)
      - [54.2.3 Intercepting Timeout Events](interceptors002.htm#GKEDU)
          - [54.2.3.1 Using Multiple Timeout
            Interceptors](interceptors002.htm#GKHLA)
      - [54.2.4 Binding Interceptors to
        Components](interceptors002.htm#sthref248)
          - [54.2.4.1 Declaring the Interceptor Bindings on an
            Interceptor Class](interceptors002.htm#sthref249)
          - [54.2.4.2 Binding a Component to an
            Interceptor](interceptors002.htm#sthref250)
      - [54.2.5 Ordering Interceptors](interceptors002.htm#sthref251)
  - [54.3 The interceptor Example
    Application](interceptors003.htm#GKECI)
      - [54.3.1 Running the interceptor
        Example](interceptors003.htm#sthref253)
          - [54.3.1.1 To Run the interceptor Example Using NetBeans
            IDE](interceptors003.htm#GKEDF)
          - [54.3.1.2 To Run the interceptor Example Using
            Maven](interceptors003.htm#GKECT)

## [55 Batch Processing](batch-processing.htm#GKJIQ6)

  - [55.1 Introduction to Batch
    Processing](batch-processing001.htm#BCGJDEEH)
      - [55.1.1 Steps in Batch Jobs](batch-processing001.htm#sthref254)
      - [55.1.2 Parallel Processing](batch-processing001.htm#sthref256)
      - [55.1.3 Status and Decision
        Elements](batch-processing001.htm#sthref257)
      - [55.1.4 Batch Framework
        Functionality](batch-processing001.htm#sthref259)
  - [55.2 Batch Processing in Java EE](batch-processing002.htm#BCGGIBHA)
      - [55.2.1 The Batch Processing
        Framework](batch-processing002.htm#BABEAFJI)
      - [55.2.2 Creating Batch
        Applications](batch-processing002.htm#BABCGDHJ)
      - [55.2.3 Elements of a Batch
        Job](batch-processing002.htm#BABDGDJB)
      - [55.2.4 Properties and
        Parameters](batch-processing002.htm#BABHJEJC)
      - [55.2.5 Job Instances and Job
        Executions](batch-processing002.htm#BABHJGDH)
      - [55.2.6 Batch and Exit Status](batch-processing002.htm#BABBFGEF)
  - [55.3 Simple Use Case](batch-processing003.htm#BCGHBJIG)
      - [55.3.1 Chunk Step](batch-processing003.htm#sthref261)
      - [55.3.2 Task Step](batch-processing003.htm#sthref262)
  - [55.4 Using the Job Specification
    Language](batch-processing004.htm#BCGDDBBG)
      - [55.4.1 The job Element](batch-processing004.htm#sthref263)
      - [55.4.2 The step Element](batch-processing004.htm#sthref264)
          - [55.4.2.1 The chunk
            Element](batch-processing004.htm#sthref265)
          - [55.4.2.2 The batchlet
            Element](batch-processing004.htm#sthref267)
          - [55.4.2.3 The partition
            Element](batch-processing004.htm#sthref268)
      - [55.4.3 The flow Element](batch-processing004.htm#sthref269)
      - [55.4.4 The split Element](batch-processing004.htm#sthref270)
      - [55.4.5 The decision Element](batch-processing004.htm#sthref271)
  - [55.5 Creating Batch Artifacts](batch-processing005.htm#BCGHDHGH)
      - [55.5.1 Batch Artifact
        Interfaces](batch-processing005.htm#BABDAIBI)
      - [55.5.2 Dependency Injection in Batch
        Artifacts](batch-processing005.htm#BCGIFJBB)
      - [55.5.3 Using the Context Objects from the Batch
        Runtime](batch-processing005.htm#BCGCJEEF)
  - [55.6 Submitting Jobs to the Batch
    Runtime](batch-processing006.htm#BCGCAHCB)
      - [55.6.1 Starting a Job](batch-processing006.htm#sthref275)
      - [55.6.2 Checking the Status of a
        Job](batch-processing006.htm#BCGIBGFC)
      - [55.6.3 Invoking the Batch Runtime in Your
        Application](batch-processing006.htm#sthref276)
  - [55.7 Packaging Batch
    Applications](batch-processing007.htm#BCGBBGJI)
  - [55.8 The webserverlog Example
    Application](batch-processing008.htm#BCGJHEHJ)
      - [55.8.1 Architecture of the webserverlog Example
        Application](batch-processing008.htm#BABCHDFB)
          - [55.8.1.1 The Job Definition
            File](batch-processing008.htm#BABFGCEC)
          - [55.8.1.2 The LogLine and LogFilteredLine
            Items](batch-processing008.htm#BABIHBFF)
          - [55.8.1.3 The Chunk Step Batch
            Artifacts](batch-processing008.htm#sthref277)
          - [55.8.1.4 The Listener Batch
            Artifacts](batch-processing008.htm#BCGCCFAC)
          - [55.8.1.5 The Task Step Batch
            Artifact](batch-processing008.htm#sthref278)
          - [55.8.1.6 The JavaServer Faces
            Pages](batch-processing008.htm#sthref279)
          - [55.8.1.7 The Managed
            Bean](batch-processing008.htm#sthref280)
      - [55.8.2 Running the webserverlog Example
        Application](batch-processing008.htm#BABFIHJA)
          - [55.8.2.1 To Run the webserverlog Example Application Using
            NetBeans IDE](batch-processing008.htm#BABHIJBE)
          - [55.8.2.2 To Run the webserverlog Example Application Using
            Maven](batch-processing008.htm#BABGACCD)
  - [55.9 The phonebilling Example
    Application](batch-processing009.htm#BCGFCACD)
      - [55.9.1 Architecture of the phonebilling Example
        Application](batch-processing009.htm#BABDEIFG)
          - [55.9.1.1 The Job Definition
            File](batch-processing009.htm#sthref281)
          - [55.9.1.2 The CallRecord and PhoneBill
            Entities](batch-processing009.htm#sthref282)
          - [55.9.1.3 The Call Records Chunk
            Step](batch-processing009.htm#sthref283)
          - [55.9.1.4 The Phone Billing Chunk
            Step](batch-processing009.htm#BCGGGAHB)
          - [55.9.1.5 The JavaServer Faces
            Pages](batch-processing009.htm#sthref284)
          - [55.9.1.6 The Managed
            Bean](batch-processing009.htm#sthref285)
      - [55.9.2 Running the phonebilling Example
        Application](batch-processing009.htm#BABBGDAA)
          - [55.9.2.1 To Run the phonebilling Example Application Using
            NetBeans IDE](batch-processing009.htm#BABIBBBG)
          - [55.9.2.2 To Run the phonebilling Example Application Using
            Maven](batch-processing009.htm#BABFHIIB)
  - [55.10 Further Information about Batch
    Processing](batch-processing010.htm#BCGHCHAJ)

## [56 Concurrency Utilities for Java EE](concurrency-utilities.htm#GKJIQ8)

  - [56.1 Concurrency Basics](concurrency-utilities001.htm#CIHDFGGG)
      - [56.1.1 Threads and
        Processes](concurrency-utilities001.htm#sthref286)
  - [56.2 Main Components of the Concurrency
    Utilities](concurrency-utilities002.htm#CIHFBCFH)
  - [56.3 Concurrency and
    Transactions](concurrency-utilities003.htm#CIHIDBDG)
  - [56.4 Concurrency and
    Security](concurrency-utilities004.htm#CIHCACAA)
  - [56.5 The jobs Concurrency
    Example](concurrency-utilities005.htm#CIHCGGEG)
      - [56.5.1 Running the jobs
        Example](concurrency-utilities005.htm#sthref287)
          - [56.5.1.1 To Configure GlassFish Server for the Basic
            Concurrency Example](concurrency-utilities005.htm#CHDCIBBD)
          - [56.5.1.2 To Build, Package, and Deploy the jobs Example
            Using NetBeans IDE](concurrency-utilities005.htm#CHDFBAHJ)
          - [56.5.1.3 To Build, Package, and Deploy the jobs Example
            Using Maven](concurrency-utilities005.htm#CHDECFFF)
          - [56.5.1.4 To Run the jobs Example and Submit Jobs with Low
            Priority](concurrency-utilities005.htm#CHDFHHAF)
          - [56.5.1.5 To Run the jobs Example and Submit Jobs with High
            Priority](concurrency-utilities005.htm#CHDHEABJ)
  - [56.6 The taskcreator Concurrency
    Example](concurrency-utilities006.htm#CIHBFEAE)
      - [56.6.1 Running the taskcreator
        Example](concurrency-utilities006.htm#sthref289)
          - [56.6.1.1 To Build, Package, and Deploy the taskcreator
            Example Using NetBeans
            IDE](concurrency-utilities006.htm#CHDCCJHB)
          - [56.6.1.2 To Build, Package, and Deploy the taskcreator
            Example Using Maven](concurrency-utilities006.htm#CHDHJBDD)
          - [56.6.1.3 To Run the taskcreator
            Example](concurrency-utilities006.htm#CHDBJGID)
  - [56.7 Further Information about the Concurrency
    Utilities](concurrency-utilities007.htm#CHDBIHAA)

## [Part XII Case Studies](partcasestudies.htm#GKGJW)

## [57 Duke's Bookstore Case Study Example](dukes-bookstore.htm#GLNVI)

  - [57.1 Design and Architecture of Duke's
    Bookstore](dukes-bookstore001.htm#GLOAW)
  - [57.2 The Duke's Bookstore Interface](dukes-bookstore002.htm#GLQFD)
      - [57.2.1 The Book Java Persistence API
        Entity](dukes-bookstore002.htm#GLQER)
      - [57.2.2 Enterprise Beans Used in Duke's
        Bookstore](dukes-bookstore002.htm#GLQEU)
      - [57.2.3 Facelets Pages and Managed Beans Used in Duke's
        Bookstore](dukes-bookstore002.htm#GLQDP)
      - [57.2.4 Custom Components and Other Custom Objects Used in
        Duke's Bookstore](dukes-bookstore002.htm#GLQDX)
      - [57.2.5 Properties Files Used in Duke's
        Bookstore](dukes-bookstore002.htm#GLQDG)
      - [57.2.6 Deployment Descriptors Used in Duke's
        Bookstore](dukes-bookstore002.htm#GLQED)
  - [57.3 Running the Duke's Bookstore Case Study
    Application](dukes-bookstore003.htm#GLPPQ)
      - [57.3.1 To Build and Deploy Duke's Bookstore Using NetBeans
        IDE](dukes-bookstore003.htm#GLPQG)
      - [57.3.2 To Build and Deploy Duke's Bookstore Using
        Maven](dukes-bookstore003.htm#GLPQN)
      - [57.3.3 To Run Duke's
        Bookstore](dukes-bookstore003.htm#BABEHDEG)

## [58 Duke's Tutoring Case Study Example](dukes-tutoring.htm#GKAEE)

  - [58.1 Design and Architecture of Duke's
    Tutoring](dukes-tutoring001.htm#GKAEI)
  - [58.2 Main Interface](dukes-tutoring002.htm#GKAFH)
      - [58.2.1 Java Persistence API Entities Used in the Main
        Interface](dukes-tutoring002.htm#GKAFJ)
      - [58.2.2 Enterprise Beans Used in the Main
        Interface](dukes-tutoring002.htm#GKAFC)
      - [58.2.3 WebSocket Endpoint Used in the Main
        Interface](dukes-tutoring002.htm#BCGHHCDA)
      - [58.2.4 Facelets Files Used in the Main
        Interface](dukes-tutoring002.htm#GKAET)
      - [58.2.5 Helper Classes Used in the Main
        Interface](dukes-tutoring002.htm#GKADH)
      - [58.2.6 Properties Files](dukes-tutoring002.htm#GKADA)
      - [58.2.7 Deployment Descriptors Used in Duke's
        Tutoring](dukes-tutoring002.htm#GKAEV)
  - [58.3 Administration Interface](dukes-tutoring003.htm#GKAFW)
      - [58.3.1 Enterprise Beans Used in the Administration
        Interface](dukes-tutoring003.htm#GKAEN)
      - [58.3.2 Facelets Files Used in the Administration
        Interface](dukes-tutoring003.htm#GKACB)
      - [58.3.3 CDI Managed Beans Used in the Administration
        Interface](dukes-tutoring003.htm#BCGHIDEG)
      - [58.3.4 Helper Classes Used in the Administration
        Interface](dukes-tutoring003.htm#BCGFFFCA)
  - [58.4 Running the Duke's Tutoring Case Study
    Application](dukes-tutoring004.htm#GKJNN)
      - [58.4.1 Running Duke's Tutoring](dukes-tutoring004.htm#GKJOA)
          - [58.4.1.1 To Build and Deploy Duke's Tutoring Using NetBeans
            IDE](dukes-tutoring004.htm#GKJNR)
          - [58.4.1.2 To Build and Deploy Duke's Tutoring Using
            Maven](dukes-tutoring004.htm#GKJOG)
          - [58.4.1.3 Using Duke's
            Tutoring](dukes-tutoring004.htm#GKJOC)

## [59 Duke's Forest Case Study Example](dukes-forest.htm#GLNPW)

  - [59.1 Overview of the Duke's Forest Case Study
    Example](dukes-forest001.htm#A1256074)
  - [59.2 Design and Architecture of Duke's
    Forest](dukes-forest002.htm#GLNRJ)
      - [59.2.1 The events Project](dukes-forest002.htm#CIHHJEGA)
      - [59.2.2 The entities Project](dukes-forest002.htm#CIHFCIAC)
      - [59.2.3 The dukes-payment
        Project](dukes-forest002.htm#sthref294)
      - [59.2.4 The dukes-resources
        Project](dukes-forest002.htm#sthref295)
      - [59.2.5 The Duke's Store Project](dukes-forest002.htm#sthref296)
          - [59.2.5.1 Enterprise Beans Used in Duke's
            Store](dukes-forest002.htm#sthref297)
          - [59.2.5.2 Facelets Files Used in the Main Interface of
            Duke's Store](dukes-forest002.htm#sthref298)
          - [59.2.5.3 Facelets Files Used in the Administration
            Interface of Duke's Store](dukes-forest002.htm#CIHHDHIH)
          - [59.2.5.4 Managed Beans Used in Duke's
            Store](dukes-forest002.htm#sthref299)
          - [59.2.5.5 Helper Classes Used in Duke's
            Store](dukes-forest002.htm#sthref300)
          - [59.2.5.6 Qualifiers Used in Duke's
            Store](dukes-forest002.htm#CIHEBAFD)
          - [59.2.5.7 Event Handlers Used in Duke's
            Store](dukes-forest002.htm#sthref301)
          - [59.2.5.8 Deployment Descriptors Used in Duke's
            Store](dukes-forest002.htm#sthref302)
      - [59.2.6 The Duke's Shipment
        Project](dukes-forest002.htm#sthref303)
          - [59.2.6.1 Enterprise Beans Used in Duke's
            Shipment](dukes-forest002.htm#sthref304)
          - [59.2.6.2 Facelets Files Used in Duke's
            Shipment](dukes-forest002.htm#sthref305)
          - [59.2.6.3 Managed Beans Used in Duke's
            Shipment](dukes-forest002.htm#sthref306)
          - [59.2.6.4 Helper Class Used in Duke's
            Shipment](dukes-forest002.htm#sthref307)
          - [59.2.6.5 Qualifier Used in Duke's
            Shipment](dukes-forest002.htm#sthref308)
          - [59.2.6.6 Deployment Descriptors Used in Duke's
            Shipment](dukes-forest002.htm#sthref309)
  - [59.3 Building and Deploying the Duke's Forest Case Study
    Application](dukes-forest003.htm#GLNQP)
      - [59.3.1 To Build and Deploy the Duke's Forest Application Using
        NetBeans IDE](dukes-forest003.htm#CHDJDIFH)
      - [59.3.2 To Build and Deploy the Duke's Forest Application Using
        Maven](dukes-forest003.htm#CHDEJHBJ)
  - [59.4 Running the Duke's Forest
    Application](dukes-forest004.htm#GLNSX)
      - [59.4.1 To Register as a Duke's Store
        Customer](dukes-forest004.htm#CHDBDEHH)
      - [59.4.2 To Purchase Products](dukes-forest004.htm#CHDCEJIC)
      - [59.4.3 To Approve Shipment of a
        Product](dukes-forest004.htm#CHDICAIJ)
      - [59.4.4 To Create a New Product](dukes-forest004.htm#CHDIFEGC)

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
<td><a href="title.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

ORACLE CONFIDENTIAL. For authorized use only. Do not distribute to third parties.
