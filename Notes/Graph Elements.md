---
tags:
- graph
---

## Graph Elements

Let’s take a closer look at the two elements that make up a graph:

- Nodes (also known as vertices)
- Relationships (also known as edges)

![[5046d4945ee8896b8949397cb7fb4ec2_MD5.jpg]]

### Nodes

![[Graph Nodes.jpg]]

**Nodes** (or vertices) are the circles in a graph. Nodes commonly represent _objects_, _entities_, or merely _things_.

In the [Seven Bridges of Königsberg](https://graphacademy.neo4j.com/courses/neo4j-fundamentals/1-graph-thinking/1-seven-bridges/) example in the previous lesson, nodes were used to represent the land masses.

Another example that everyone can relate to is the concept of a social graph. People interact with each other and form relationships of varying strengths.

The diagram to the right has two nodes which represent two people, **Michael** and **Sarah**. On their own, these elements are uninspiring. But when we start to connect these circles together, things start to get interesting.

#### Nodes typically represent things

Examples of entities that could typically be represented as a node are: person, product, event, book or subway station.

### Relationships

![[Graph Relationships.jpg]]

**Relationships** (or _edges_) are used to connect nodes. We can use relationships to describe how nodes are connected to each other. For example **Michael** has the **WORKS_AT** relationship to **Graph Inc** because he works there. **Michael** has the **MARRIED_TO** relationship to **Sarah** because he is married to her.

All of a sudden, we know that we are looking at the beginnings of some sort of _social graph_.

Now, let’s introduce a third person, **Hans**, to our Graph.

![[Relationships - Edges.jpg]]

**Hans** also _works for_ **Graph Inc** along with Michael. Depending on the size of the company and the properties of the relationship, we may be able to infer that Michael and Hans know each other.

If that is the case, how likely is it that Sarah and Hans know each other?

These are all questions that can be answered using a graph.

#### Relationships are typically verbs.

We could use a relationship to represent a personal or professional connection (_Person **knows** Person, Person **married to** Person_), to state a fact (_Person **lives in** Location_, _Person **owns** Car_, _Person **rated** Movie_), or even to represent a hierarchy (_Parent **parent of** Child, Software **depends on** Library_).

[Watch](https://graphacademy.neo4j.com/courses/neo4j-fundamentals/1-graph-thinking/2-graph-elements/#video)[Read](https://graphacademy.neo4j.com/courses/neo4j-fundamentals/1-graph-thinking/2-graph-elements/#transcript)

[[Graph Structure]]     [[Vector Databases]]  [[Graph Theory]]

[[Graph Properties]]