# Assignment 1 — Graph Algorithms on a Randomly Generated City Network

This project models a network of cities connected by roads as an undirected, weighted graph, and explores fundamental graph theory concepts on it: random graph construction, connectivity, and shortest paths.

## Overview

The graph represents `N = 500` cities as nodes, with roads as weighted, undirected edges. Each city is randomly connected to a handful of others, and the resulting network is analyzed for its structure and connectivity.

## Concepts Explored

### 1. Random Graph Construction
A graph is built on 500 nodes where:
- Each node is given a random degree between 2 and 7, controlling how many roads connect it to other cities.
- Edges carry random weights between 5 and 50, representing road distance or cost.
- Duplicate edges and self-loops are explicitly avoided, keeping the graph simple.

This produces a sparse, randomly connected network — a common way to simulate real-world infrastructure graphs (road networks, utility grids, communication networks) where nodes rarely connect to every other node.

### 2. Connected Components
Using depth-first search (DFS), the graph is decomposed into its connected components — groups of cities that can all reach one another through some sequence of roads.

- The largest component identifies the biggest cluster of mutually reachable cities.
- Looking at all components (their count, sizes, largest, and smallest) reveals whether the network is fully connected (a single component spanning all 500 cities) or fragmented into isolated clusters — an important property when reasoning about network resilience and reachability.

### 3. Single-Source Shortest Paths (Dijkstra's Algorithm)
From a fixed source city, Dijkstra's algorithm computes the shortest weighted distance to every other reachable city using a min-priority queue, greedily expanding the closest unvisited node at each step.

- Cities unreachable from the source are explicitly identified.
- The city with the maximum shortest-path distance from the source is reported — effectively the "farthest" or most peripheral city in the network, useful for identifying bottlenecks or worst-case travel scenarios.

## Algorithmic Complexity

| Task | Algorithm | Complexity |
|---|---|---|
| Graph construction | Randomized adjacency list build | O(N · deg) |
| Connected components | Depth-First Search | O(V + E) |
| Shortest paths | Dijkstra's Algorithm (binary heap) | O((V + E) log V) |

## Sample Output

```
Total Cities = 500
Total Roads = 1486

Largest Component Size = 500

Total Components = 1
Largest Cluster = 500
Smallest Cluster = 500

City 0 : 0
City 1 : 42
...
Maximum Distance City = 315
Distance = 135
```

(Exact numbers vary between runs since the graph is randomly generated.)

## Key Takeaways

- A sparse random graph with degree 2–7 per node is often, but not guaranteed to be, fully connected — component analysis is essential to verify this rather than assume it.
- DFS-based component discovery and Dijkstra's shortest-path algorithm are complementary tools: one answers "can I get there at all?" and the other answers "what's the cheapest way to get there?"
- The farthest-city analysis highlights how shortest-path algorithms can be used beyond simple point-to-point queries — e.g., identifying network eccentricity, a step toward concepts like graph diameter and radius.
