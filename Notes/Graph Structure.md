---
tags:
- graph
---

## **Graph Structure

## Graph characteristics and traversal

There are a few types of graph characteristics to consider. In addition, there are many ways that a graph may be traversed to answer a question.

### Directed vs. undirected graphs

![[7379ffbe747416a74f5d4bdeed8f04fc_MD5.jpg]]

In an undirected graph, relationships are considered to be bi-directional or symmetric.

An example of an undirected graph would include the concept of marriage. If _Michael_ is married to _Sarah_, then it stands to reason that _Sarah_ is also married to _Michael_.

A directed graph adds an additional dimension of information to the graph. Relationships with the same type but in opposing directions carry a different semantic meaning.

![[Directed Graph.jpg]]

For example, if marriage is a symmetrical relationship, then the concept of love is asymmetrical. Although two people may like or love each other, the amount that they do so may vary drastically. Directional relationships can often be qualified with some sort of weighting. Here we see that the strength of the LOVES relationship describes how much one person loves another.

At a larger scale, a large network of social connections may also be used to understand network effects and predict the transfer of information or disease. Given the strength of connections between people, we can predict how information would spread through a network.

### Weighted vs. unweighted graphs

The concept of love is also an example of a weighted graph.

In a weighted graph, the relationships between nodes carry a value that represents a variety of measures, for example cost, time, distance or priority.

A basic shortest path algorithm would calculate the shortest distance between two nodes in the graph. This could be useful for finding the fastest walking route to the local store or working out the most efficient route to travel from city to city.

![[eeb1299c10032e42bcd128d02ccaaefb_MD5.jpg]]

In this example, the question that we might have for this graph is: What is the shortest drive from Springfield to Centerville? Using the _HAS_ROAD_ relationships and the distance for these relationships, we can see that the shortest drive will be to start in Springfield, then go to Cliffside, then to Newtown, and finally arrive in Centerville.

More complex shortest path algorithms (for example, Dijkstra’s algorithm or A* search algorithm) take a weighting property on the relationship into account when calculating the shortest path. Say we have to send a package using an international courier, we may prefer to send the package by air so it arrives quickly, in which case the weighting we would take into account is the time it takes to get from one point to the next.

Inversely, if cost is an issue we may prefer to send the package by sea and therefore use a property that represents cost to send the package.

### Graph traversal

How one answers questions about the data in a graph is typically implemented by traversing the graph. To find the shortest path between Springfield to Centerville, the application would need to traverse all paths between the two cities to find the shortest one.

- Springfield-Newtown-Centerville = 26
- Springfield-Cliffside-Newtown-Centerville = 23
- Springfield-Cliffside-Melrose-Certerville = 49

Traversal implies that the relationships are followed in the graph. There are different types of traversals in graph theory that can impact application performance. For example, can a relationship be traversed multiple times or can a node be visited multiple times?

Neo4j’s Cypher statement language is optimized for node traversal so that relationships are not traversed multiple times, which is a huge performance win for an application.

[Watch](https://graphacademy.neo4j.com/courses/neo4j-fundamentals/1-graph-thinking/3-graph-structure/#video)[Read](https://graphacademy.neo4j.com/courses/neo4j-fundamentals/1-graph-thinking/3-graph-structure/#transcript)

[[Graphs]]     [[Vector Databases]]