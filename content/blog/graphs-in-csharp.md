---
title: "Graphs in Csharp"
date: 2023-04-27T12:05:02+03:00
draft: false
tags : ["C#", "Graphs", "Data Structures"]
---

In data structures and algorithms, a graph is a data structure that consists of a set of nodes (also called vertices) and a set of edges connecting the nodes. Each edge has a direction and a weight, and may represent a relationship or a flow of information between the nodes it connects.

Networks, like social networks, transportation networks, and communication networks, are often shown as graphs. They can be used to model many different kinds of problems, such as finding the shortest path between two nodes or determining whether a graph is connected.

Here is an example of a graph class implemented in C#:

```csharp	
// Graph class
public class Graph
{
    // Dictionary to store the edges in the graph
    Dictionary<int, List<Tuple<int, int>>> edges = new Dictionary<int, List<Tuple<int, int>>>();

    // Method to add an edge to the graph
    public void AddEdge(int u, int v, int w)
    {
        if (!edges.ContainsKey(u))
            edges.Add(u, new List<Tuple<int, int>>());

        edges[u].Add(new Tuple<int, int>(v, w));
    }

    // Method to get the neighbors of a node
    public List<Tuple<int, int>> GetNeighbors(int u)
    {
        return edges[u];
    }
}
```
This ```Graph``` class uses a dictionary to store the edges in the graph, with the keys representing the starting node of the edge and the values representing the ending nodes of the edge. Each edge is represented as a tuple containing the ending node and the weight of the edge. The ```AddEdge``` method adds an edge to the graph, and the ```GetNeighbors``` method returns the list of neighbors for a given node`

[GitHub Source Code link](https://github.com/nirzaf/GraphDataStructure)
