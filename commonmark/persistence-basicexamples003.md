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
<td><a href="persistence-basicexamples002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-basicexamples004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span></a></td>
<td> </td>
</tr>
</tbody>
</table>

Beta Draft: 2017-06-12

# 38.3 The roster Application

The `roster` application maintains the team rosters for players in
recreational sports leagues. The application has four components: Java
Persistence API entities (`Player`, `Team`, and `League`), a stateful
session bean (`RequestBean`), an application client (`RosterClient`),
and three helper classes (`PlayerDetails`, `TeamDetails`, and
`LeagueDetails`).

Functionally, `roster` is similar to the `order` application, with three
new features that `order` does not have: many-to-many relationships,
entity inheritance, and automatic table creation at deployment time.

The database schema in the Java DB database for the `roster` application
is shown in [Figure 38-2](#CHDCHJHG).

Figure 38-2 Database Schema for the roster Application

![Description of Figure 38-2 follows](img/jeett_dt_025.png)  
[Description of "Figure 38-2 Database Schema for the roster
Application"](img_text/jeett_dt_025.htm)  
  

  

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Note:</p>
In this diagram, for simplicity, the <code dir="ltr">PERSISTENCE_ROSTER_</code> prefix is omitted from the table names.</td>
</tr>
</tbody>
</table>

  

## 38.3.1 Relationships in the roster Application

A recreational sports system has the following relationships.

  - A player can be on many teams.

  - A team can have many players.

  - A team is in exactly one league.

  - A league has many teams.

In `roster` this system is reflected by the following relationships
between the `Player`, `Team`, and `League` entities.

  - There is a many-to-many relationship between `Player` and `Team`.

  - There is a many-to-one relationship between `Team` and `League`.

### 38.3.1.1 The Many-To-Many Relationship in roster

The many-to-many relationship between `Player` and `Team` is specified
by using the `@ManyToMany` annotation. In `Team.java`, the `@ManyToMany`
annotation decorates the `getPlayers` method:

``` oac_no_warn
@ManyToMany
@JoinTable(
    name="PERSISTENCE_ROSTER_TEAM_PLAYER",
    joinColumns=
        @JoinColumn(name="TEAM_ID", referencedColumnName="ID"),
    inverseJoinColumns=
        @JoinColumn(name="PLAYER_ID", referencedColumnName="ID")
)
public Collection<Player> getPlayers() {
    return players;
}
```

The `@JoinTable` annotation is used to specify a database table that
will associate player IDs with team IDs. The entity that specifies the
`@JoinTable` is the owner of the relationship, so the `Team` entity is
the owner of the relationship with the `Player` entity. Because `roster`
uses automatic table creation at deployment time, the container will
create a join table named `PERSISTENCE_ROSTER_TEAM_PLAYER`.

`Player` is the inverse, or nonowning, side of the relationship with
`Team`. As one-to-one and many-to-one relationships, the nonowning side
is marked by the `mappedBy` element in the relationship annotation.
Because the relationship between `Player` and `Team` is bidirectional,
the choice of which entity is the owner of the relationship is
arbitrary.

In `Player.java`, the `@ManyToMany` annotation decorates the `getTeams`
method:

``` oac_no_warn
@ManyToMany(mappedBy="players")
public Collection<Team> getTeams() {
    return teams;
}
```

## 38.3.2 Entity Inheritance in the roster Application

The `roster` application shows how to use entity inheritance, as
described in [Entity Inheritance](persistence-intro003.htm#BNBQN).

The `League` entity in `roster` is an abstract entity with two concrete
subclasses: `SummerLeague` and `WinterLeague`. Because `League` is an
abstract class, it cannot be instantiated:

``` oac_no_warn
@Entity
@Table(name = "PERSISTENCE_ROSTER_LEAGUE")
public abstract class League implements Serializable { ... }
```

Instead, when creating a league, clients use `SummerLeague` or
`WinterLeague`. `SummerLeague` and `WinterLeague` inherit the persistent
properties defined in `League` and add only a constructor that verifies
that the sport parameter matches the type of sport allowed in that
seasonal league. For example, here is the `SummerLeague` entity:

``` oac_no_warn
...
@Entity
public class SummerLeague extends League implements Serializable {

    /** Creates a new instance of SummerLeague */
    public SummerLeague() {
    }

    public SummerLeague(String id, String name, String sport) 
            throws IncorrectSportException {
        this.id = id;
        this.name = name;
        if (sport.equalsIgnoreCase("swimming") ||
                sport.equalsIgnoreCase("soccer") ||
                sport.equalsIgnoreCase("basketball") ||
                sport.equalsIgnoreCase("baseball")) {
            this.sport = sport;
        } else {
            throw new IncorrectSportException("Sport is not a summer sport.");
        }
    }
}
```

The `roster` application uses the default mapping strategy of
`InheritanceType.SINGLE_TABLE`, so the `@Inheritance` annotation is not
required. If you want to use a different mapping strategy, decorate
`League` with `@Inheritance` and specify the mapping strategy in the
`strategy` element:

``` oac_no_warn
@Entity
@Inheritance(strategy=JOINED)
@Table(name="PERSISTENCE_ROSTER_LEAGUE")
public abstract class League implements Serializable { ... }
```

The `roster` application uses the default discriminator column name, so
the `@DiscriminatorColumn` annotation is not required. Because you are
using automatic table generation in `roster`, the Persistence provider
will create a discriminator column called `DTYPE` in the
`PERSISTENCE_ROSTER_LEAGUE` table, which will store the name of the
inherited entity used to create the league. If you want to use a
different name for the discriminator column, decorate `League` with
`@DiscriminatorColumn` and set the `name` element:

``` oac_no_warn
@Entity
@DiscriminatorColumn(name="DISCRIMINATOR")
@Table(name="PERSISTENCE_ROSTER_LEAGUE")
public abstract class League implements Serializable { ... }
```

## 38.3.3 Criteria Queries in the roster Application

The `roster` application uses Criteria API queries, as opposed to the
JPQL queries used in `order`. Criteria queries are Java programming
language, typesafe queries defined in the business tier of `roster`, in
the `RequestBean` stateful session bean.

The following topics are addressed here:

  - [Section 38.3.3.1, "Metamodel Classes in the roster
    Application"](#GJJEX)

  - [Section 38.3.3.2, "Obtaining a CriteriaBuilder Instance in
    RequestBean"](#GJJFN)

  - [Section 38.3.3.3, "Creating Criteria Queries in RequestBean's
    Business Methods"](#GJJFF)

### 38.3.3.1 Metamodel Classes in the roster Application

Metamodel classes model an entity's attributes and are used by Criteria
queries to navigate to an entity's attributes. Each entity class in
`roster` has a corresponding metamodel class, generated at compile time,
with the same package name as the entity and appended with an underscore
character (\_). For example, the `roster.entity.Player` entity has a
corresponding metamodel class, `roster.entity.Player_`.

Each persistent field or property in the entity class has a
corresponding attribute in the entity's metamodel class. For the
`Player` entity, the corresponding metamodel class is as follows:

``` oac_no_warn
@StaticMetamodel(Player.class)
public class Player_ {
    public static volatile SingularAttribute<Player, String> id;
    public static volatile SingularAttribute<Player, String> name;
    public static volatile SingularAttribute<Player, String> position;
    public static volatile SingularAttribute<Player, Double> salary;
    public static volatile CollectionAttribute<Player, Team> teams;
}
```

### 38.3.3.2 Obtaining a CriteriaBuilder Instance in RequestBean

The `CriteriaBuilder` interface defines methods to create criteria query
objects and create expressions for modifying those query objects.
`RequestBean` creates an instance of `CriteriaBuilder` by using a
`@PostConstruct` method, `init`:

``` oac_no_warn
@PersistenceContext
private EntityManager em;
private CriteriaBuilder cb;

@PostConstruct
private void init() {
    cb = em.getCriteriaBuilder();
}
```

The `EntityManager` instance is injected at runtime, and then that
`EntityManager` object is used to create the `CriteriaBuilder` instance
by calling `getCriteriaBuilder`. The `CriteriaBuilder` instance is
created in a `@PostConstruct` method to ensure that the `EntityManager`
instance has been injected by the enterprise bean container.

### 38.3.3.3 Creating Criteria Queries in RequestBean's Business Methods

Many of the business methods in `RequestBean` define Criteria queries.
One business method, `getPlayersByPosition`, returns a list of players
who play a particular position on a team:

``` oac_no_warn
public List<PlayerDetails> getPlayersByPosition(String position) {
    logger.info("getPlayersByPosition");
    List<Player> players = null;
    
    try {
        CriteriaQuery<Player> cq = cb.createQuery(Player.class);
        if (cq != null) {
            Root<Player> player = cq.from(Player.class);

            // set the where clause
            cq.where(cb.equal(player.get(Player_.position), position));
            cq.select(player);
            TypedQuery<Player> q = em.createQuery(cq);
            players = q.getResultList();
        }
        return copyPlayersToDetails(players);
    } catch (Exception ex) {
        throw new EJBException(ex);
    }
}
```

A query object is created by calling the `CriteriaBuilder` object's
`createQuery` method, with the type set to `Player` because the query
will return a list of players.

The query root, the base entity from which the query will navigate to
find the entity's attributes and related entities, is created by calling
the `from` method of the query object. This sets the `FROM` clause of
the query.

The `WHERE` clause, set by calling the `where` method on the query
object, restricts the results of the query according to the conditions
of an expression. The `CriteriaBuilder.equal` method compares the two
expressions. In `getPlayersByPosition`, the `position` attribute of the
`Player_` metamodel class, accessed by calling the `get` method of the
query root, is compared to the `position` parameter passed to
`getPlayersByPosition`.

The `SELECT` clause of the query is set by calling the `select` method
of the query object. The query will return `Player` entities, so the
query root object is passed as a parameter to `select`.

The query object is prepared for execution by calling
`EntityManager.createQuery`, which returns a `TypedQuery<T>` object with
the type of the query, in this case `Player`. This typed query object is
used to execute the query, which occurs when the `getResultList` method
is called, and a `List<Player>` collection is returned.

## 38.3.4 Automatic Table Generation in the roster Application

At deployment time, GlassFish Server will automatically drop and create
the database tables used by `roster`. This is done by setting the
`javax.persistence.schema-generation.database.action` property to
`drop-and-create` in `persistence.xml`:

``` oac_no_warn
<?xml version="1.0" encoding="UTF-8"?>
<persistence version="2.1" 
    xmlns="http://xmlns.jcp.org/xml/ns/persistence"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence
        http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1.xsd">
  <persistence-unit name="em" transaction-type="JTA">
    <jta-data-source>java:comp/DefaultDataSource</jta-data-source>
    <properties>
      <property name="javax.persistence.schema-generation.database.action" 
                value="drop-and-create"/>
    </properties>
  </persistence-unit>
</persistence>
```

## 38.3.5 Running the roster Example

You can use either NetBeans IDE or Maven to build, package, deploy, and
run the `roster` application.

The following topics are addressed here:

  - [Section 38.3.5.1, "To Run the roster Example Using NetBeans
    IDE"](#GIQUG)

  - [Section 38.3.5.2, "To Run the roster Example Using Maven"](#GIQSJ)

### 38.3.5.1 To Run the roster Example Using NetBeans IDE

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  If the database server is not already running, start it by following
    the instructions in [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK).

3.  From the File menu, choose Open Project.

4.  In the Open Project dialog box, navigate to:
    
    ``` oac_no_warn
    tut-install/examples/persistence
    ```

5.  Select the `roster` folder.

6.  Select the Open Required Projects check box.

7.  Click Open Project.

8.  In the Projects tab, right-click the `roster` project and select
    Build.
    
    This will compile, package, and deploy the EAR to GlassFish Server.
    
    You will see the following partial output from the application
    client in the Output tab:
    
    ``` oac_no_warn
    List all players in team T2:
    P6 Ian Carlyle goalkeeper 555.0
    P7 Rebecca Struthers midfielder 777.0
    P8 Anne Anderson forward 65.0
    P9 Jan Wesley defender 100.0
    P10 Terry Smithson midfielder 100.0
    
    List all teams in league L1:
    T1 Honey Bees Visalia
    T2 Gophers Manteca
    T5 Crows Orland
    
    List all defenders:
    P2 Alice Smith defender 505.0
    P5 Barney Bold defender 100.0
    P9 Jan Wesley defender 100.0
    P22 Janice Walker defender 857.0
    P25 Frank Fletcher defender 399.0
    ```

### 38.3.5.2 To Run the roster Example Using Maven

1.  Make sure that GlassFish Server has been started (see [Starting and
    Stopping GlassFish Server](usingexamples002.htm#BNADI)).

2.  If the database server is not already running, start it by following
    the instructions in [Starting and Stopping the Java DB
    Server](usingexamples004.htm#BNADK).

3.  In a terminal window, go to:
    
    ``` oac_no_warn
    tut-install/examples/persistence/roster/roster-ear/
    ```

4.  Enter the following command:
    
    ``` oac_no_warn
    mvn install
    ```
    
    This compiles the source files and packages the application into an
    EAR file located at
    tut-install`/examples/persistence/roster/target/roster.ear`. The EAR
    file is then deployed to GlassFish Server. GlassFish Server will
    then drop and create the database tables during deployment, as
    specified in `persistence.xml`.
    
    After successfully deploying the EAR, the client stubs are retrieved
    and the application client is run using the appclient application
    included with GlassFish Server.
    
    You will see the output, which begins as follows:
    
    ``` oac_no_warn
    [echo] running application client container.
    [exec] List all players in team T2:
    [exec] P6 Ian Carlyle goalkeeper 555.0
    [exec] P7 Rebecca Struthers midfielder 777.0
    [exec] P8 Anne Anderson forward 65.0
    [exec] P9 Jan Wesley defender 100.0
    [exec] P10 Terry Smithson midfielder 100.0
    
    [exec] List all teams in league L1:
    [exec] T1 Honey Bees Visalia
    [exec] T2 Gophers Manteca
    [exec] T5 Crows Orland
    
    [exec] List all defenders:
    [exec] P2 Alice Smith defender 505.0
    [exec] P5 Barney Bold defender 100.0
    [exec] P9 Jan Wesley defender 100.0
    [exec] P22 Janice Walker defender 857.0
    [exec] P25 Frank Fletcher defender 399.0
    ```

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
<td><a href="persistence-basicexamples002.htm"><img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span></a> </td>
<td><a href="persistence-basicexamples004.htm"><img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
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
