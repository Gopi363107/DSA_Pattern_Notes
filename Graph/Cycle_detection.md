# Cycle Detection Pattern

---

# Definition

The **Cycle Detection Pattern** is used to determine whether a graph contains a cycle (loop).

A cycle exists when:

```text
Starting from a node

Follow edges

Reach the same node again
```

This pattern is one of the most important graph patterns because many advanced graph problems are built on cycle detection.

---

# Core Idea

The cycle detection logic depends on the graph type.

```text
Undirected Graph
→ Parent Tracking

Directed Graph
→ Recursion Stack / Topological Sort
```

---

# When To Use This Pattern

Use this pattern when the problem asks:

```text
Detect cycle

Detect loop

Circular dependency

Redundant edge

Can all tasks be completed?

Dependency graph

Deadlock detection

Schedule tasks

Course prerequisites

Invalid graph structure
```

---

# Trigger Words

## Undirected Graph

```text
Detect cycle

Extra edge

Redundant connection

Network loop

Tree became graph
```

---

## Directed Graph

```text
Circular dependency

Task scheduling

Course prerequisites

Dependency graph

Can finish all tasks

Build order
```

---

# Types of Cycle Detection

```text
1. Undirected Graph
   DFS + Parent Tracking
   BFS + Parent Tracking

2. Directed Graph
   DFS + Recursion Stack
   Topological Sort
```

---

# Undirected Graph Cycle Detection

---

## Core Idea

Suppose:

```text
0 ----- 1
|       |
|       |
3 ----- 2
```

Cycle exists.

While exploring:

```text
If neighbor is already visited
AND
neighbor != parent

Cycle Found
```

---

## Why Parent Check?

Example:

```text
0 ---- 1
```

When DFS reaches:

```text
0 → 1
```

Node 1 sees:

```text
Neighbor = 0
```

It is already visited.

But that's the parent.

Not a cycle.

---

## DFS Template (Undirected)

```java
boolean dfs(
    int node,
    int parent,
    List<Integer>[] graph,
    boolean[] visited
) {

    visited[node] = true;

    for (int neighbor : graph[node]) {

        if (!visited[neighbor]) {

            if (dfs(
                    neighbor,
                    node,
                    graph,
                    visited
                )) {
                return true;
            }

        } else if (neighbor != parent) {

            return true;

        }
    }

    return false;
}
```

---

## BFS Template (Undirected)

```java
class Pair {

    int node;
    int parent;

    Pair(int node, int parent) {

        this.node = node;
        this.parent = parent;
    }
}

boolean bfs(
    int start,
    List<Integer>[] graph,
    boolean[] visited
) {

    Queue<Pair> queue =
        new LinkedList<>();

    queue.offer(
        new Pair(start, -1)
    );

    visited[start] = true;

    while (!queue.isEmpty()) {

        Pair current =
            queue.poll();

        for (int neighbor :
                graph[current.node]) {

            if (!visited[neighbor]) {

                visited[neighbor] = true;

                queue.offer(
                    new Pair(
                        neighbor,
                        current.node
                    )
                );

            } else if (
                neighbor != current.parent
            ) {

                return true;
            }
        }
    }

    return false;
}
```

---

# Directed Graph Cycle Detection

---

## Core Idea

In directed graphs:

```text
Visited node
≠
Cycle
```

Because revisiting an old node is allowed.

What matters is:

```text
Did we revisit a node
inside the current DFS path?
```

If YES:

```text
Cycle Found
```

---

## Example

```text
0 → 1 → 2
    ↑   ↓
    ←---
```

DFS Path:

```text
0 → 1 → 2
```

Node 2 reaches:

```text
1
```

which is already in current DFS path.

Cycle exists.

---

# Recursion Stack Method

Maintain:

```text
visited[]
pathVisited[]
```

---

## Meaning

```text
visited[node]
→ Ever visited

pathVisited[node]
→ Present in current DFS path
```

---

## DFS Template

```java
boolean dfs(
    int node,
    List<Integer>[] graph,
    boolean[] visited,
    boolean[] pathVisited
) {

    visited[node] = true;
    pathVisited[node] = true;

    for (int neighbor : graph[node]) {

        if (!visited[neighbor]) {

            if (dfs(
                    neighbor,
                    graph,
                    visited,
                    pathVisited
                )) {

                return true;
            }

        } else if (
            pathVisited[neighbor]
        ) {

            return true;

        }
    }

    pathVisited[node] = false;

    return false;
}
```

---

# Topological Sort Based Detection

---

## Core Idea

A DAG (Directed Acyclic Graph)

must have:

```text
Valid Topological Order
```

If cycle exists:

```text
Topological Sort
cannot process all nodes
```

---

## Detection Rule

After Kahn's Algorithm:

```text
processedNodes == totalNodes
```

No cycle.

Otherwise:

```text
Cycle exists.
```

---

## Template

```java
boolean hasCycle(
    int n,
    List<Integer>[] graph
) {

    int[] indegree =
        new int[n];

    for (int node = 0;
         node < n;
         node++) {

        for (int neighbor :
                graph[node]) {

            indegree[neighbor]++;

        }
    }

    Queue<Integer> queue =
        new LinkedList<>();

    for (int i = 0;
         i < n;
         i++) {

        if (indegree[i] == 0) {

            queue.offer(i);

        }
    }

    int count = 0;

    while (!queue.isEmpty()) {

        int node =
            queue.poll();

        count++;

        for (int neighbor :
                graph[node]) {

            indegree[neighbor]--;

            if (
                indegree[neighbor]
                == 0
            ) {

                queue.offer(
                    neighbor
                );

            }
        }
    }

    return count != n;
}
```

---

# Pattern Recognition Flow

## Step 1

Ask:

```text
Graph Directed?
```

If NO:

```text
Undirected Cycle Detection
```

---

## Step 2

Ask:

```text
Need cycle detection?
```

Use:

```text
DFS + Parent

or

BFS + Parent
```

---

## Step 3

If Directed:

```text
Dependency graph?

Course graph?

Task graph?
```

Use:

```text
DFS Recursion Stack

or

Topological Sort
```

---

# Problem 1

## LC 684 — Redundant Connection

---

### Problem

A graph started as a tree.

One extra edge was added.

Return:

```text
The edge causing cycle
```

---

### Example

```text
1 - 2

|   |

3 --
```

Extra edge:

```text
2 - 3
```

creates cycle.

Return:

```text
[2,3]
```

---

### Pattern Recognition

Trigger words:

```text
Extra edge

Redundant edge

Tree becomes graph

Cycle detection
```

Undirected Graph.

---

### Core Idea

For every edge:

```text
Try connecting it

If endpoints already connected

Cycle Found
```

Use Union Find.

---

### Solution

```java
class Solution {

    int[] parent;

    public int[] findRedundantConnection(
        int[][] edges
    ) {

        int n = edges.length;

        parent =
            new int[n + 1];

        for (int i = 0;
             i <= n;
             i++) {

            parent[i] = i;

        }

        for (int[] edge : edges) {

            int u = edge[0];
            int v = edge[1];

            int pu = find(u);
            int pv = find(v);

            if (pu == pv) {

                return edge;

            }

            parent[pu] = pv;
        }

        return new int[0];
    }

    private int find(int node) {

        if (parent[node] == node)
            return node;

        return parent[node] =
            find(parent[node]);
    }
}
```

---

### Complexity

```text
Time  : O(N α(N))

Space : O(N)
```

---

# Problem 2

## LC 207 — Course Schedule

---

### Problem

Given:

```text
numCourses

prerequisites
```

Determine:

```text
Can all courses be completed?
```

---

### Pattern Recognition

Trigger words:

```text
Course schedule

Prerequisite

Dependency graph

Can finish all tasks
```

Directed Graph Cycle Detection.

---

### Core Idea

If cycle exists:

```text
Course A needs B

Course B needs A
```

Impossible.

---

### Solution (DFS)

```java
class Solution {

    public boolean canFinish(
        int numCourses,
        int[][] prerequisites
    ) {

        List<Integer>[] graph =
            new ArrayList[numCourses];

        for (int i = 0;
             i < numCourses;
             i++) {

            graph[i] =
                new ArrayList<>();

        }

        for (int[] edge :
                prerequisites) {

            graph[edge[1]]
                .add(edge[0]);
        }

        boolean[] visited =
            new boolean[numCourses];

        boolean[] pathVisited =
            new boolean[numCourses];

        for (int i = 0;
             i < numCourses;
             i++) {

            if (!visited[i]) {

                if (dfs(
                        i,
                        graph,
                        visited,
                        pathVisited
                    )) {

                    return false;
                }
            }
        }

        return true;
    }

    private boolean dfs(
        int node,
        List<Integer>[] graph,
        boolean[] visited,
        boolean[] pathVisited
    ) {

        visited[node] = true;
        pathVisited[node] = true;

        for (int neighbor :
                graph[node]) {

            if (!visited[neighbor]) {

                if (dfs(
                        neighbor,
                        graph,
                        visited,
                        pathVisited
                    )) {

                    return true;
                }

            } else if (
                pathVisited[neighbor]
            ) {

                return true;
            }
        }

        pathVisited[node] = false;

        return false;
    }
}
```

---

### Complexity

```text
Time  : O(V + E)

Space : O(V)
```

---

# Problem 3

## LC 802 — Find Eventual Safe States

---

### Problem

Return all nodes that are:

```text
Never part of a cycle

Cannot reach a cycle
```

---

### Pattern Recognition

Trigger words:

```text
Safe states

Cycle states

Nodes leading to cycle

Directed graph
```

---

### Core Idea

Node can be:

```text
Safe

Unsafe (cycle)

Leads to cycle
```

Use DFS cycle detection.

---

### State Meaning

```text
0 = Unvisited

1 = Visiting

2 = Safe
```

---

### Solution

```java
class Solution {

    public List<Integer>
    eventualSafeNodes(
        int[][] graph
    ) {

        int n = graph.length;

        int[] state =
            new int[n];

        List<Integer> answer =
            new ArrayList<>();

        for (int i = 0;
             i < n;
             i++) {

            if (dfs(
                    i,
                    graph,
                    state
                )) {

                answer.add(i);
            }
        }

        return answer;
    }

    private boolean dfs(
        int node,
        int[][] graph,
        int[] state
    ) {

        if (state[node] != 0) {

            return state[node] == 2;
        }

        state[node] = 1;

        for (int neighbor :
                graph[node]) {

            if (!dfs(
                    neighbor,
                    graph,
                    state
                )) {

                return false;
            }
        }

        state[node] = 2;

        return true;
    }
}
```

---

### Complexity

```text
Time  : O(V + E)

Space : O(V)
```

---

# Interview Cheat Sheet

| If Question Says | Pattern |
|------------------|----------|
| Detect cycle | Cycle Detection |
| Detect loop | Cycle Detection |
| Redundant edge | Undirected Cycle |
| Tree becomes graph | Undirected Cycle |
| Circular dependency | Directed Cycle |
| Course schedule | Directed Cycle |
| Task dependency | Directed Cycle |
| Build order | Topological Sort |
| Safe states | Directed Cycle |
| Can finish all tasks | Directed Cycle |

---

# Key Takeaway

```text
Undirected Graph

Cycle exists when:
Visited Neighbor != Parent

------------------------------------------------

Directed Graph

Cycle exists when:
Node appears again in current DFS path

------------------------------------------------

Topological Sort

Processed Nodes < Total Nodes

Cycle Exists
```

---

# Quick Memory Formula

```text
Undirected
=
Visited + Parent Check

Directed
=
Visited + PathVisited

Topological Sort
=
Count Processed Nodes
```

Next Patterns:

```text
3. Topological Sort Pattern
4. Shortest Path Pattern
5. Union Find Pattern
6. Multi Source BFS Pattern
7. Graph Coloring Pattern
8. Strongly Connected Components
```