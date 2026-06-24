# Heap + Graph

## Core Idea

Heap + Graph problems appear when:

```text id="c1"
Graph has weights + we need BEST / SHORTEST / MIN COST path dynamically
```

We combine:

```text id="c2"
Graph Traversal (BFS/DFS)
+
Heap (Priority Queue)
```

to always pick the “best next node”.

---

## When to Use

* Shortest path in weighted graph
* Minimum cost to reach destination
* K shortest / best values
* MST-like problems
* Network delay / propagation
* Dynamic path optimization

---

## Trigger Words

* Minimum cost
* Shortest path
* Cheapest route
* Kth smallest path
* Connect nodes with minimum cost
* Time to reach all nodes
* Weighted edges

---

## Recognition Pattern

```text id="c3"
Graph + Weights
        ↓
Need Minimum / Maximum Optimal Choice
        ↓
BFS/DFS not enough
        ↓
Use Heap (Priority Queue)
```

---

# Core Technique

## Why Heap?

Normal BFS:

```text id="c4"
Unweighted shortest path only
```

Heap BFS (Dijkstra idea):

```text id="c5"
Always expand smallest cost node first
```

---

# Heap + Graph Template (Dijkstra Style)

## Basic Structure

```java id="c6"
class Node {
    int v;
    int cost;

    Node(int v, int cost){
        this.v = v;
        this.cost = cost;
    }
}
```

---

## Dijkstra Template

```java id="c7"
public int dijkstra(List<List<int[]>> graph, int n, int src){

    int[] dist = new int[n];
    Arrays.fill(dist, Integer.MAX_VALUE);

    PriorityQueue<int[]> pq =
        new PriorityQueue<>((a,b) -> a[1] - b[1]);

    pq.offer(new int[]{src, 0});
    dist[src] = 0;

    while(!pq.isEmpty()){

        int[] cur = pq.poll();
        int node = cur[0];
        int cost = cur[1];

        if(cost > dist[node]) continue;

        for(int[] edge : graph.get(node)){

            int nei = edge[0];
            int wt = edge[1];

            if(cost + wt < dist[nei]){

                dist[nei] = cost + wt;
                pq.offer(new int[]{nei, dist[nei]});
            }
        }
    }

    return dist[n-1];
}
```

---

## Time Complexity

```text id="c8"
O((V + E) log V)
```

---

## Space Complexity

```text id="c9"
O(V + E)
```

---

# Type 1: Shortest Path Problems

## Idea

Always pick node with minimum distance so far.

---

## Pattern

```text id="c10"
Use Min Heap
Relax edges
Update distance array
```

---

## Example Problems

```text id="c11"
Dijkstra shortest path
Network Delay Time
Path with minimum effort
Cheapest flights within K stops
```

---

# Type 2: Kth / Top K in Graph

## Idea

Maintain heap of best K values.

---

## Pattern

```text id="c12"
Max Heap / Min Heap
Keep only K best paths
```

---

## Example

```text id="c13"
Kth shortest path
K closest nodes
K highest probability path
```

---

# Type 3: MST + Heap (Prim’s Algorithm)

## Idea

Pick minimum weight edge connecting new node.

---

## Pattern

```text id="c14"
Start node
Push all edges to heap
Pick smallest edge
Expand tree
```

---

## Prim’s Template

```java id="c15"
public int prim(int n, List<List<int[]>> graph){

    boolean[] visited = new boolean[n];

    PriorityQueue<int[]> pq =
        new PriorityQueue<>((a,b) -> a[1] - b[1]);

    pq.offer(new int[]{0, 0});

    int cost = 0;

    while(!pq.isEmpty()){

        int[] cur = pq.poll();
        int node = cur[0];
        int wt = cur[1];

        if(visited[node]) continue;

        visited[node] = true;
        cost += wt;

        for(int[] edge : graph.get(node)){

            if(!visited[edge[0]]){
                pq.offer(new int[]{edge[0], edge[1]});
            }
        }
    }

    return cost;
}
```

---

## Complexity

```text id="c16"
O(E log V)
```

---

# Type 4: Multi-Source Heap BFS

## Idea

Start from multiple nodes at once.

---

## Pattern

```text id="c17"
Push all sources into heap
Run Dijkstra-like expansion
```

---

## Example

```text id="c18"
Rotting Oranges (variant)
Multi-source shortest path
Spread problems
```

---

# Type 5: Grid + Heap

## Idea

Grid becomes graph.

Each cell = node.

---

## Pattern

```text id="c19"
Move 4 directions
Use heap for best cost path
```

---

## Example

```text id="c20"
Path with minimum effort
Dungeon game
Swim in rising water
```

---

# Important Insights

### Insight 1

Heap ensures:

```text id="c21"
Always process BEST candidate first
```

---

### Insight 2

Graph + weights → BFS is not enough

```text id="c22"
Need Dijkstra / Heap BFS
```

---

### Insight 3

Visited check avoids:

```text id="c23"
Re-processing worse paths
```

---

### Insight 4

Distance array is crucial:

```text id="c24"
Tracks best known cost
```

---

# Common Interview Problems

```text id="c25"
743  - Network Delay Time

1631 - Path With Minimum Effort

778  - Swim In Rising Water

1514 - Path With Maximum Probability

787  - Cheapest Flights Within K Stops

1631 - MST Grid Variant
```

---

# Pattern Map

| Type                | Technique           |
| ------------------- | ------------------- |
| Shortest Path       | Dijkstra (Min Heap) |
| MST                 | Prim (Min Heap)     |
| K Best Paths        | Heap                |
| Grid Optimization   | Heap BFS            |
| Multi-source spread | Heap BFS            |

---

# Quick Revision

```text id="c26"
Graph + Weights
        ↓
Need Optimal Path
        ↓
Use Heap

----------------

Shortest Path → Dijkstra

MST → Prim

K Best → Heap Tracking

Grid → Heap BFS

----------------

Always Pick Best Node First
```

---

# Master Formula

```text id="c27"
Graph Problems

+

Weights

=

Heap Based Search

-------------------

BFS → Unweighted

Heap → Weighted

-------------------

Answer = Best Path / Minimum Cost
```
