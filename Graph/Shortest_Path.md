# Shortest Path Pattern

## Definition

The Shortest Path Pattern is used to find:

```text
Minimum Distance

Minimum Time

Minimum Cost

Fastest Route
```

between nodes in a graph.

---

## When To Use

Use when the problem asks:

```text
Shortest Path

Minimum Distance

Minimum Time

Minimum Cost

Fastest Route

Minimum Effort

Best Path
```

---

## Trigger Words

```text
Minimum distance

Shortest route

Fastest path

Least cost

Minimum effort

Network delay

Travel time
```

---

# Pattern Selection

## Unweighted Graph

Use:

```text
BFS
```

Because every edge has:

```text
Weight = 1
```

---

## Weighted Graph

Use:

```text
Dijkstra
```

Because edges have different weights.

---

## Negative Edge Weights

Use:

```text
Bellman Ford
```

Interview concept is usually enough.

---

# BFS Shortest Path

## Core Idea

In an unweighted graph:

```text
Every edge costs 1
```

The first time we reach a node:

```text
Shortest distance found
```

---

## BFS Template

```java
int[] shortestPath(
        int n,
        List<Integer>[] graph,
        int source) {

    int[] distance =
            new int[n];

    Arrays.fill(distance, -1);

    Queue<Integer> queue =
            new LinkedList<>();

    queue.offer(source);

    distance[source] = 0;

    while (!queue.isEmpty()) {

        int node = queue.poll();

        for (int neighbor : graph[node]) {

            if (distance[neighbor] == -1) {

                distance[neighbor] =
                        distance[node] + 1;

                queue.offer(neighbor);
            }
        }
    }

    return distance;
}
```

### Complexity

```text
Time  : O(V + E)

Space : O(V)
```

---

# Dijkstra Algorithm

## Core Idea

Always process:

```text
Node with minimum distance
```

Use:

```text
Min Heap
(Priority Queue)
```

---

## Dijkstra Template

```java
class Pair {

    int node;
    int distance;

    Pair(int node, int distance) {

        this.node = node;
        this.distance = distance;
    }
}

int[] dijkstra(
        int n,
        List<Pair>[] graph,
        int source) {

    int[] distance =
            new int[n];

    Arrays.fill(
            distance,
            Integer.MAX_VALUE);

    PriorityQueue<Pair> pq =
            new PriorityQueue<>(
                (a, b) ->
                a.distance - b.distance
            );

    distance[source] = 0;

    pq.offer(
        new Pair(source, 0)
    );

    while (!pq.isEmpty()) {

        Pair current =
                pq.poll();

        int node =
                current.node;

        int dist =
                current.distance;

        if (dist >
            distance[node]) {
            continue;
        }

        for (Pair neighbor :
                graph[node]) {

            int next =
                    neighbor.node;

            int weight =
                    neighbor.distance;

            if (distance[node]
                + weight
                < distance[next]) {

                distance[next] =
                        distance[node]
                        + weight;

                pq.offer(
                    new Pair(
                        next,
                        distance[next]
                    )
                );
            }
        }
    }

    return distance;
}
```

### Complexity

```text
Time  : O((V + E) log V)

Space : O(V)
```

---

# Bellman Ford (Concept)

## When To Use

```text
Negative Edge Weights
```

Example:

```text
A -> B = -5
```

Dijkstra fails.

Bellman Ford works.

---

## Core Idea

Relax every edge:

```text
V - 1 times
```

Can also detect:

```text
Negative Cycle
```

---

# Pattern Recognition

## Step 1

Ask:

```text
Minimum distance?
```

If YES:

```text
Shortest Path
```

---

## Step 2

Ask:

```text
Weighted graph?
```

If YES:

```text
Dijkstra
```

Else:

```text
BFS
```

---

## Step 3

Ask:

```text
Negative edges?
```

If YES:

```text
Bellman Ford
```

---

# Problem 1

## LC 743 - Network Delay Time

### Recognition

```text
Signal propagation

Time to reach all nodes

Minimum travel time
```

Pattern:

```text
Dijkstra
```

---

### Core Idea

Find shortest time from:

```text
Source Node K
```

to every node.

Answer:

```text
Maximum shortest distance
```

because the signal must reach everyone.

---

### Solution

```java
class Solution {

    class Pair {

        int node;
        int time;

        Pair(int node, int time) {

            this.node = node;
            this.time = time;
        }
    }

    public int networkDelayTime(
            int[][] times,
            int n,
            int k) {

        List<Pair>[] graph =
                new ArrayList[n + 1];

        for (int i = 1; i <= n; i++) {

            graph[i] =
                    new ArrayList<>();
        }

        for (int[] edge : times) {

            graph[edge[0]].add(
                new Pair(
                    edge[1],
                    edge[2]
                )
            );
        }

        int[] dist =
                new int[n + 1];

        Arrays.fill(
                dist,
                Integer.MAX_VALUE);

        PriorityQueue<Pair> pq =
                new PriorityQueue<>(
                    (a, b) ->
                    a.time - b.time
                );

        dist[k] = 0;

        pq.offer(
            new Pair(k, 0)
        );

        while (!pq.isEmpty()) {

            Pair current =
                    pq.poll();

            if (current.time >
                dist[current.node]) {
                continue;
            }

            for (Pair next :
                    graph[current.node]) {

                if (dist[current.node]
                    + next.time
                    < dist[next.node]) {

                    dist[next.node] =
                        dist[current.node]
                        + next.time;

                    pq.offer(
                        new Pair(
                            next.node,
                            dist[next.node]
                        )
                    );
                }
            }
        }

        int answer = 0;

        for (int i = 1; i <= n; i++) {

            if (dist[i]
                == Integer.MAX_VALUE) {

                return -1;
            }

            answer =
                Math.max(
                    answer,
                    dist[i]
                );
        }

        return answer;
    }
}
```

### Complexity

```text
Time  : O((V+E)logV)

Space : O(V+E)
```

---

# Problem 2

## LC 1514 - Path With Maximum Probability

### Recognition

```text
Maximum Probability

Best Path

Weighted Graph
```

Pattern:

```text
Modified Dijkstra
```

---

### Core Idea

Normal Dijkstra:

```text
Minimum Distance
```

Here:

```text
Maximum Probability
```

Use:

```text
Max Heap
```

instead of Min Heap.

---

### Solution

```java
class Solution {

    class Pair {

        int node;
        double probability;

        Pair(int node,
             double probability) {

            this.node = node;
            this.probability =
                    probability;
        }
    }

    public double maxProbability(
            int n,
            int[][] edges,
            double[] succProb,
            int start,
            int end) {

        List<Pair>[] graph =
                new ArrayList[n];

        for (int i = 0; i < n; i++) {

            graph[i] =
                    new ArrayList<>();
        }

        for (int i = 0;
             i < edges.length;
             i++) {

            int u = edges[i][0];
            int v = edges[i][1];

            graph[u].add(
                new Pair(
                    v,
                    succProb[i]
                )
            );

            graph[v].add(
                new Pair(
                    u,
                    succProb[i]
                )
            );
        }

        double[] best =
                new double[n];

        best[start] = 1.0;

        PriorityQueue<Pair> pq =
                new PriorityQueue<>(
                    (a,b) ->
                    Double.compare(
                        b.probability,
                        a.probability
                    )
                );

        pq.offer(
            new Pair(start,1.0)
        );

        while (!pq.isEmpty()) {

            Pair current =
                    pq.poll();

            if (current.node == end) {

                return current.probability;
            }

            for (Pair next :
                    graph[current.node]) {

                double newProb =
                        current.probability
                        * next.probability;

                if (newProb >
                    best[next.node]) {

                    best[next.node] =
                            newProb;

                    pq.offer(
                        new Pair(
                            next.node,
                            newProb
                        )
                    );
                }
            }
        }

        return 0.0;
    }
}
```

### Complexity

```text
Time  : O((V+E)logV)

Space : O(V)
```

---

# Problem 3

## LC 1631 - Path With Minimum Effort

### Recognition

```text
Grid

Minimum Effort

Best Path
```

Pattern:

```text
Dijkstra on Grid
```

---

### Core Idea

Path Cost:

```text
Maximum absolute difference
between adjacent cells
```

Minimize:

```text
Maximum Edge Weight
```

Use Dijkstra.

---

### Interview Insight

This problem teaches:

```text
Dijkstra is not only for sums.

It can optimize:

Minimum Maximum

Maximum Probability

Minimum Effort

Minimum Cost
```

---

# Complexity Summary

| Algorithm | Time | Space |
|------------|--------|--------|
| BFS | O(V+E) | O(V) |
| Dijkstra | O((V+E)logV) | O(V) |
| Bellman Ford | O(V×E) | O(V) |

---

# Interview Cheat Sheet

| Question Says | Pattern |
|--------------|----------|
| Minimum Distance | BFS / Dijkstra |
| Shortest Route | BFS / Dijkstra |
| Fastest Route | Dijkstra |
| Minimum Time | Dijkstra |
| Minimum Cost | Dijkstra |
| Maximum Probability | Modified Dijkstra |
| Minimum Effort | Dijkstra |
| Negative Edge | Bellman Ford |

---

# Memory Trick

```text
Unweighted Graph
=
BFS
```

```text
Weighted Graph
=
Dijkstra
```

```text
Negative Edge
=
Bellman Ford
```

```text
Shortest Path
=
Priority Queue
(Often Dijkstra)
```

---

# Key Takeaway

```text
Need Minimum Distance?
→ Shortest Path

Unweighted Graph?
→ BFS

Weighted Graph?
→ Dijkstra

Negative Weights?
→ Bellman Ford

Grid + Minimum Cost?
→ Usually Dijkstra
```