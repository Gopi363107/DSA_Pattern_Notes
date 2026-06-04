# Graph Patterns Roadmap

A structured roadmap to master Graph problems for coding interviews.
---

# Time Complexity Summary

| Pattern | Time Complexity |
|----------|----------------|
| DFS | O(V + E) |
| BFS | O(V + E) |
| Connected Components | O(V + E) |
| Cycle Detection | O(V + E) |
| Topological Sort | O(V + E) |
| Bipartite Graph | O(V + E) |
| Dijkstra | O((V + E) log V) |
| DSU | O(α(n)) |
| Kruskal MST | O(E log E) |
| Prim MST | O(E log V) |
| Grid BFS/DFS | O(R × C) |
| State BFS | O(V × States) |

---

# 1. Graph Traversal Pattern (Foundation)

## Learn

- DFS (Depth First Search)
- BFS (Breadth First Search)
- Connected Components

## Recognition

Use this pattern when the problem says:

- Visit all nodes
- Count groups/components
- Can we reach node X?
- Explore all connected nodes

## Core Concepts

### DFS

- Recursive traversal
- Uses recursion stack
- Good for deep exploration

### BFS

- Level-by-level traversal
- Uses Queue
- Good for shortest path in unweighted graphs

### Connected Components

- Count how many independent groups exist
- Start DFS/BFS from every unvisited node

## Problems

### Easy

- LC 733 - Flood Fill
- LC 841 - Keys and Rooms

### Medium

- LC 200 - Number of Islands
- LC 695 - Max Area of Island

---

# 2. Cycle Detection Pattern

## Learn

### Undirected Graph

- DFS Cycle Detection
- BFS Cycle Detection (Parent Tracking)

### Directed Graph

- DFS + Recursion Stack
- Topological Sort Based Detection

## Recognition

Use when problem says:

- Detect cycle
- Detect loop
- Circular dependency
- Can all tasks be completed?

## Core Concepts

### Undirected Graph

Cycle exists if:

- Visited neighbor is not parent

### Directed Graph

Cycle exists if:

- Node appears again in current DFS path

## Problems

### Medium

- LC 684 - Redundant Connection
- LC 207 - Course Schedule

### Hard

- LC 802 - Find Eventual Safe States

---

# 3. Topological Sort Pattern

## Learn

### Kahn's Algorithm

- BFS
- In-degree array

### DFS Topological Sort

- Postorder DFS
- Reverse result

## Recognition

Use when problem says:

- Dependencies
- Prerequisites
- Execution order
- Build order

## Core Concepts

A valid ordering exists only for DAGs.

DAG = Directed Acyclic Graph

## Problems

### Medium

- LC 210 - Course Schedule II
- LC 1136 - Parallel Courses

### Hard

- LC 1203 - Sort Items by Groups Respecting Dependencies

---

# 4. Bipartite Graph Pattern

## Learn

- Graph Coloring
- BFS Coloring
- DFS Coloring

## Recognition

Use when problem says:

- Divide into two groups
- Team assignment
- No adjacent nodes in same group

## Core Concepts

Assign:

- Color 0
- Color 1

If neighbors receive same color:

Graph is not bipartite.

## Problems

### Medium

- LC 785 - Is Graph Bipartite?
- LC 886 - Possible Bipartition

---

# 5. Shortest Path Pattern

## Learn

### BFS

For unweighted graph

### Dijkstra

For weighted graph

### Bellman-Ford

Concept only

Handles negative edges

## Recognition

Use when problem says:

- Minimum distance
- Minimum time
- Minimum cost
- Fastest route

## Core Concepts

### BFS

Shortest path in unweighted graph

TC = O(V + E)

SC = O(V)

### Dijkstra

Shortest path in weighted graph

TC = O((V + E) log V)

SC = O(V)

## Problems

### Medium

- LC 743 - Network Delay Time
- LC 1514 - Path With Maximum Probability

### Hard

- LC 1631 - Path With Minimum Effort

---

# 6. Union Find (DSU) Pattern

## Learn

- Find
- Union
- Path Compression
- Union by Rank

## Recognition

Use when problem says:

- Connectivity
- Merge groups
- Dynamic components
- Cycle detection

## Core Concepts

Efficiently maintain connected components.

## Complexity

Find:

O(α(n))

Union:

O(α(n))

Space:

O(n)

## Problems

### Medium

- LC 547 - Number of Provinces
- LC 684 - Redundant Connection
- LC 1319 - Number of Operations to Make Network Connected

---

# 7. Minimum Spanning Tree Pattern

## Learn

### Kruskal

- Sort edges
- DSU

### Prim

- Priority Queue

## Recognition

Use when problem says:

- Connect all nodes
- Minimum total cost
- Minimum wiring cost
- Minimum network cost

## Core Concepts

MST connects all nodes using:

- N - 1 edges
- Minimum possible cost

## Complexity

### Kruskal

TC = O(E log E)

SC = O(V)

### Prim

TC = O(E log V)

SC = O(V)

## Problems

### Medium

- LC 1584 - Min Cost to Connect All Points
- LC 1135 - Connecting Cities With Minimum Cost

---

# 8. Grid Graph Pattern

## Learn

- DFS
- BFS
- Multi-Source BFS
- Flood Fill

## Recognition

Use when problem contains:

- Matrix
- Grid
- Islands
- Up/Down/Left/Right movement

## Core Concepts

Treat every cell as a graph node.

## Problems

### Medium

- LC 994 - Rotting Oranges
- LC 542 - 01 Matrix

### Hard

- LC 286 - Walls and Gates

---

# 9. Backtracking on Graph Pattern

## Learn

- DFS Path Exploration
- Backtracking

## Recognition

Use when problem says:

- Find all paths
- Explore every possibility
- Enumerate routes

## Core Concepts

Choose

Explore

Backtrack

## Problems

### Medium

- LC 797 - All Paths From Source to Target

### Hard

- LC 980 - Unique Paths III

---

# 10. Advanced State BFS Pattern

## Learn

- BFS + State
- BFS + Bitmask

## Recognition

Use when state contains:

- Position
- Keys collected
- Visited nodes
- Additional information

## Core Concepts

Store:

(position, state)

instead of:

(position)

## Problems

### Hard

- LC 864 - Shortest Path to Get All Keys
- LC 847 - Shortest Path Visiting All Nodes

---

# Interview Priority Order

## Tier 1 (Must Know)

1. DFS
2. BFS
3. Connected Components
4. Cycle Detection
5. Topological Sort

## Tier 2 (Very Important)

6. Bipartite Graph
7. Shortest Path (BFS + Dijkstra)
8. Union Find (DSU)
9. Grid BFS / DFS

## Tier 3 (Advanced)

10. Minimum Spanning Tree
11. Backtracking on Graph
12. State BFS
13. BFS + Bitmask

---

# Recommended Learning Sequence

Week 1

- DFS
- BFS
- Connected Components

Week 2

- Cycle Detection
- Topological Sort

Week 3

- Bipartite Graph
- Union Find

Week 4

- Shortest Path
- Grid Problems

Week 5

- Minimum Spanning Tree

Week 6

- Backtracking on Graph
- State BFS

---

# Placement Preparation Focus

For top MNC and fintech interviews, prioritize:

1. DFS
2. BFS
3. Cycle Detection
4. Topological Sort
5. Union Find
6. Dijkstra
7. Grid BFS/DFS
8. Bipartite Graph
9. Minimum Spanning Tree
10. State BFS

Mastering the first 8 topics covers the majority of graph questions asked in coding interviews.