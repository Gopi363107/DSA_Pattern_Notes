# Minimum Spanning Tree (MST) Pattern

## Definition

A Minimum Spanning Tree (MST) connects all nodes using:

```text
N - 1 Edges

Minimum Total Cost
```

without forming cycles.

---

## When To Use

Use when the problem asks:

```text
Connect All Nodes

Minimum Cost

Minimum Wiring Cost

Minimum Network Cost

Minimum Road Cost

Minimum Cable Cost

Connect Cities
```

---

## Trigger Words

```text
Connect all nodes

Minimum total cost

Minimum network

Minimum spanning tree

Connect cities

Connect points

Cheapest connection
```

---

# Core Idea

Given:

```text
N Nodes
```

MST must:

```text
Connect Every Node

Use Exactly N - 1 Edges

Have No Cycle

Have Minimum Cost
```

---

## Example

```text
A ---5--- B

|         |

2         3

|         |

C ---4--- D
```

Choose:

```text
A-C = 2

B-D = 3

C-D = 4
```

Total:

```text
9
```

Minimum possible.

---

# Approaches

## 1. Kruskal Algorithm

Uses:

```text
Sort Edges

DSU
```

---

## Core Idea

Process edges from:

```text
Smallest Cost
→ Largest Cost
```

Take an edge only if:

```text
It does not create a cycle
```

---

## Kruskal Template

```java
class Edge {

    int u;
    int v;
    int weight;

    Edge(int u,
         int v,
         int weight) {

        this.u = u;
        this.v = v;
        this.weight = weight;
    }
}

int kruskal(
        int n,
        List<Edge> edges) {

    Collections.sort(
        edges,
        (a, b) ->
        a.weight - b.weight
    );

    DSU dsu = new DSU(n);

    int cost = 0;

    for (Edge edge : edges) {

        if (dsu.find(edge.u)
            != dsu.find(edge.v)) {

            dsu.union(
                edge.u,
                edge.v
            );

            cost += edge.weight;
        }
    }

    return cost;
}
```

### Complexity

```text
Time  : O(E log E)

Space : O(V)
```

---

# 2. Prim Algorithm

Uses:

```text
Priority Queue

Greedy Expansion
```

---

## Core Idea

Start from any node.

Always pick:

```text
Minimum Cost Edge
```

that expands the tree.

---

## Prim Template

```java
int prim(
        int n,
        List<int[]>[] graph) {

    boolean[] visited =
            new boolean[n];

    PriorityQueue<int[]> pq =
            new PriorityQueue<>(
                (a,b) ->
                a[1] - b[1]
            );

    pq.offer(
        new int[]{0, 0}
    );

    int mstCost = 0;

    while (!pq.isEmpty()) {

        int[] current =
                pq.poll();

        int node = current[0];
        int cost = current[1];

        if (visited[node]) {
            continue;
        }

        visited[node] = true;

        mstCost += cost;

        for (int[] neighbor :
                graph[node]) {

            if (!visited[
                neighbor[0]
            ]) {

                pq.offer(
                    new int[]{
                        neighbor[0],
                        neighbor[1]
                    }
                );
            }
        }
    }

    return mstCost;
}
```

### Complexity

```text
Time  : O(E log V)

Space : O(V)
```

---

# Kruskal vs Prim

| Kruskal | Prim |
|----------|----------|
| Sort Edges | Priority Queue |
| Uses DSU | Uses Visited Array |
| Edge Based | Node Based |
| Good for Sparse Graph | Good for Dense Graph |
| O(E log E) | O(E log V) |

---

# Pattern Recognition

## Step 1

Ask:

```text
Need to connect all nodes?
```

If YES:

```text
MST
```

---

## Step 2

Ask:

```text
Need minimum total cost?
```

If YES:

```text
MST
```

---

## Step 3

Ask:

```text
Need cheapest network?
```

If YES:

```text
Kruskal / Prim
```

---

# Problem 1

## LC 1584 - Min Cost to Connect All Points

### Recognition

```text
Connect All Points

Minimum Cost
```

Pattern:

```text
MST
```

---

### Core Idea

Each point:

```text
Node
```

Distance:

```text
|x1-x2| + |y1-y2|
```

is edge weight.

Build MST using:

```text
Prim
```

---

### Solution (Prim)

```java
class Solution {

    public int minCostConnectPoints(
            int[][] points) {

        int n = points.length;

        boolean[] visited =
                new boolean[n];

        PriorityQueue<int[]> pq =
                new PriorityQueue<>(
                    (a,b) ->
                    a[1] - b[1]
                );

        pq.offer(
            new int[]{0, 0}
        );

        int cost = 0;
        int edges = 0;

        while (!pq.isEmpty()
                && edges < n) {

            int[] current =
                    pq.poll();

            int node = current[0];
            int weight = current[1];

            if (visited[node]) {
                continue;
            }

            visited[node] = true;

            cost += weight;

            edges++;

            for (int next = 0;
                 next < n;
                 next++) {

                if (!visited[next]) {

                    int dist =
                        Math.abs(
                            points[node][0]
                            - points[next][0]
                        )
                        +
                        Math.abs(
                            points[node][1]
                            - points[next][1]
                        );

                    pq.offer(
                        new int[]{
                            next,
                            dist
                        }
                    );
                }
            }
        }

        return cost;
    }
}
```

### Complexity

```text
Time  : O(N² log N)

Space : O(N)
```

---

# Problem 2

## LC 1135 - Connecting Cities With Minimum Cost

### Recognition

```text
Connect Cities

Minimum Cost

Network Cost
```

Pattern:

```text
MST
```

---

### Core Idea

Sort roads by cost.

Keep adding smallest road.

Skip road if:

```text
Cycle Forms
```

Use:

```text
Kruskal + DSU
```

---

### Solution

```java
class Solution {

    public int minimumCost(
            int n,
            int[][] connections) {

        Arrays.sort(
            connections,
            (a,b) ->
            a[2] - b[2]
        );

        DSU dsu =
                new DSU(n + 1);

        int cost = 0;
        int edges = 0;

        for (int[] edge :
                connections) {

            int u = edge[0];
            int v = edge[1];
            int w = edge[2];

            if (dsu.find(u)
                != dsu.find(v)) {

                dsu.union(u, v);

                cost += w;

                edges++;
            }
        }

        return edges == n - 1
                ? cost
                : -1;
    }
}
```

### Complexity

```text
Time  : O(E log E)

Space : O(V)
```

---

# Complexity Summary

| Algorithm | Time | Space |
|------------|--------|--------|
| Kruskal | O(E log E) | O(V) |
| Prim | O(E log V) | O(V) |

---

# Interview Cheat Sheet

| Question Says | Pattern |
|--------------|----------|
| Connect All Nodes | MST |
| Minimum Total Cost | MST |
| Minimum Network Cost | MST |
| Minimum Wiring Cost | MST |
| Connect Cities | MST |
| Connect Points | MST |
| Cheapest Network | MST |
| Spanning Tree | MST |

---

# Memory Trick

```text
MST

=
Connect All Nodes

+
Minimum Cost

+
N - 1 Edges
```

```text
Kruskal

=
Sort Edges
+
DSU
```

```text
Prim

=
Priority Queue
+
Greedy Expansion
```

---

# Key Takeaway

```text
Need to Connect All Nodes?
→ MST

Need Minimum Total Cost?
→ MST

Need Cheapest Network?
→ MST

Kruskal
→ Sort Edges + DSU

Prim
→ Priority Queue
```