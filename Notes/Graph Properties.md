---
tags: 
- graph
---

## Property Graph

### Nodes, Labels and Properties

Recall that nodes are the graph elements that represent the _things_ in our data. We can use two additional elements to provide some extra context to the data.

Let’s take a look at how we can use these additional elements to improve our social graph.

#### Labels

![[728b73ccc523daff813ca2edfea2f74a_MD5.jpg]]

By adding a label to a node, we are signifying that the node belongs to a subset of nodes within the graph. Labels are important in Neo4j because they provide a starting point for a Cypher statement.

Let’s take **Michael** and **Sarah** - in this context both of these nodes are **persons**.

We can embellish the graph by adding more labels to these nodes; Michael identifies as **male** and Sarah is **female**. In this context, Michael is an **employee** of a company, but we don’t have any information about Sarah’s employment status.

Michael works for a **company** called Graph Inc, so we can add that label to the node that represents a company.

In Neo4j, a node can have zero, one, or many labels.

#### Node properties

So far we’re assuming that the nodes represent Michael, Sarah, and Graph Inc. We can make this concrete by adding properties to the node.

Properties are key, value pairs and can be added or removed from a node as necessary. Property values can be a single value or list of values [that conform to the Cypher type system](https://neo4j.com/docs/cypher-manual/current/values-and-types/property-structural-constructed/).

![[45fdbe8894b32dfbf3659e68f8dfeeaf_MD5.jpg]]

By adding _firstName_ and _lastName_ properties, we can see that the Michael node refers to **Michael Faraday**, known for Faraday’s law of induction, the Faraday cage and lesser known as the inventor of the Party Balloon. Michael was _born_ on 22 September 1791.

Sarah’s full name is **Sarah Faraday**, and her _maidenName_ is **Barnard**.

By looking at the _name_ property on the Graph Inc node, we can see that it refers to the company **Graph Inc**, with a _city_ of **London**, has 56 employees (_numEmployees_), and does business as Graph Incorporated and GI (_dba_).

Properties do not need to exist for each node with a particular label. If a property does not exist for a node, it is treated as a `null` value.

### Relationships

A relationship in Neo4j is a connection between two nodes.

#### Relationship direction

![[8be8f50cfc7cd626cd9f4e96aa9a2f98_MD5.jpg]]

In Neo4j, each relationship **must** have a direction in the graph. Although this direction is required, the relationship can be queried in either direction, or ignored completely at query time.

A relationship is created between a **source node** and a **destination node**, so these nodes must exist before you create the relationship.

If we consider the concept of directed & undirected graphs that we discussed in the previous module, the direction of the _MARRIED_TO_ relationship must exist and may provide some additional context but can be ignored for the purpose of the query. In Neo4j, the _MARRIED_TO_ relationship must have a direction.

The direction of a relationship can be important when it comes to hierarchy, although whether the relationships point up or down towards the tree is an arbitrary decision.

#### Relationship type

![[b951739a4b45f1e8804e2b5b39147c2f_MD5.jpg]]

Each relationship in a neo4j graph **must** have a type. This allows us to choose at query time which part of the graph we will traverse.

For example, we can traverse through _every_ relationship from Michael, or we can specify the _MARRIED_TO_ relationship to end up only at Sarah’s node.

Here are sample Cypher statement statements to support this:

```cypher
// traverse the Michael node to return the Sarah node
MATCH (p:Person {firstName: 'Michael'})-[:MARRIED_TO]-(n) RETURN n;

// traverse the Michael node to return the Graph Inc node
MATCH (p:Person {firstName: 'Michael'})-[:WORKS_AT]-(n) RETURN n;

// traverse all relationships from the Michael node
// to return the Sarah node and the Graph Inc node
MATCH (p:Person {firstName: 'Michael'})--(n) RETURN n
```

#### Relationship properties

As with nodes, relationships can also have properties. These can refer to a cost or distance in a weighted graph or just provide additional context to a relationship.

![[3840869c6471acee49a704e0d2ebcabb_MD5.jpg]]

In our graph, we can place a property on the _MARRIED_TO_ relationship to hold the date in which Michael and Sarah were married. This _WORKS_AT_ relationship has a _roles_ property to signify any roles that the employee has filled at the company. If Michael also worked at another company, his _WORKS_AT_ relationship to the other company would have a different value for the _roles_ property.

[Watch](https://graphacademy.neo4j.com/courses/neo4j-fundamentals/2-property-graphs/1-property-graph/#video)[Read](https://graphacademy.neo4j.com/courses/neo4j-fundamentals/2-property-graphs/1-property-graph/#transcript)

 [[Vector Databases]]  [[Graph Structure]]  [[Graph Elements]]