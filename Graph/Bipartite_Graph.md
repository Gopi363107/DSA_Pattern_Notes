# Bipartite Graph Pattern

## Definition

A graph is Bipartite if we can divide all nodes into:

```text
Group A
Group B
```

such that:

```text
No two adjacent nodes
belong to the same group
```

---

## When To Use

Use when the problem asks:

```text
Divide into two groups

Team assignment

Possible bipartition

Enemy relationships

No adjacent nodes in same group

Two-color graph
```

---

## Trigger Words

```text
Two groups

Two teams

Red / Blue coloring

Possible bipartition

Dislike relationships

No adjacent nodes together
```

---

## Core Idea

Assign each node:

```text
Color 0

Color 1
```

For every edge:

```text
u ---- v
```

Colors must be:

```text
0 - 1

or

1 - 0
```

If we ever get:

```text
0 - 0

or

1 - 1
```

Graph is NOT Bipartite.

---

## Visualization

Valid Bipartite:

```text
0 --- 1
|     |
1 --- 0
```

Not Bipartite:

```text
0
| \
|  \
1---?
```

Third node needs both colors.

Impossible.

---

## Key Observation

```text
Even Cycle
→ Bipartite

Odd Cycle
→ Not Bipartite
```

Example:

```text
0 - 1 - 2 - 3 - 0
```

Even Cycle

```text
Bipartite
```

---

Example:

```text
0 - 1
 \ /
  2
```

Odd Cycle

```text
Not Bipartite
```

---

# BFS Coloring

## Template

```java
boolean bfs(int start,
            int[][] graph,
            int[] color) {

    Queue<Integer> queue =
            new LinkedList<>();

    queue.offer(start);

    color[start] = 0;

    while (!queue.isEmpty()) {

        int node = queue.poll();

        for (int neighbor : graph[node]) {

            if (color[neighbor] == -1) {

                color[neighbor] =
                        1 - color[node];

                queue.offer(neighbor);

            } else if (
                color[neighbor]
                == color[node]
            ) {

                return false;
            }
        }
    }

    return true;
}
```

---

# DFS Coloring

## Template

```java
boolean dfs(int node,
            int currentColor,
            int[][] graph,
            int[] color) {

    color[node] = currentColor;

    for (int neighbor : graph[node]) {

        if (color[neighbor] == -1) {

            if (!dfs(
                    neighbor,
                    1 - currentColor,
                    graph,
                    color
                )) {

                return false;
            }

        } else if (
            color[neighbor]
            == currentColor
        ) {

            return false;
        }
    }

    return true;
}
```

---

# Complete Driver Template

```java
boolean isBipartite(int[][] graph) {

    int n = graph.length;

    int[] color = new int[n];

    Arrays.fill(color, -1);

    for (int i = 0; i < n; i++) {

        if (color[i] == -1) {

            if (!dfs(
                    i,
                    0,
                    graph,
                    color
                )) {

                return false;
            }
        }
    }

    return true;
}
```

---

# Pattern Recognition

## Step 1

Ask:

```text
Need two groups?
```

If YES:

```text
Bipartite Graph
```

---

## Step 2

Ask:

```text
No adjacent nodes
in same team?
```

If YES:

```text
Graph Coloring
```

---

## Step 3

Ask:

```text
Enemy relationship?

Dislike relationship?

Possible partition?
```

If YES:

```text
Bipartite Graph
```

---

# Problem 1

## LC 785 - Is Graph Bipartite?

### Recognition

```text
Check whether graph
can be divided into
two groups
```

Pattern:

```text
Graph Coloring
```

---

### Core Idea

Assign:

```text
0

1
```

to neighboring nodes.

If neighbors receive same color:

```text
Not Bipartite
```

---

### Solution (DFS)

```java
class Solution {

    public boolean isBipartite(
            int[][] graph) {

        int n = graph.length;

        int[] color =
                new int[n];

        Arrays.fill(color, -1);

        for (int i = 0; i < n; i++) {

            if (color[i] == -1) {

                if (!dfs(
                        i,
                        0,
                        graph,
                        color
                    )) {

                    return false;
                }
            }
        }

        return true;
    }

    private boolean dfs(
            int node,
            int currentColor,
            int[][] graph,
            int[] color) {

        color[node] =
                currentColor;

        for (int neighbor :
                graph[node]) {

            if (color[neighbor] == -1) {

                if (!dfs(
                        neighbor,
                        1 - currentColor,
                        graph,
                        color
                    )) {

                    return false;
                }

            } else if (
                color[neighbor]
                == currentColor
            ) {

                return false;
            }
        }

        return true;
    }
}
```

### Complexity

```text
Time  : O(V + E)

Space : O(V)
```

---

# Problem 2

## LC 886 - Possible Bipartition

### Recognition

```text
People

Dislikes

Split into two groups
```

Pattern:

```text
Bipartite Graph
```

---

### Core Idea

Create graph:

```text
u dislikes v
```

means:

```text
u and v
must be in different groups
```

Then perform graph coloring.

---

### Solution

```java
class Solution {

    public boolean possibleBipartition(
            int n,
            int[][] dislikes) {

        List<Integer>[] graph =
                new ArrayList[n + 1];

        for (int i = 1; i <= n; i++) {

            graph[i] =
                    new ArrayList<>();
        }

        for (int[] edge : dislikes) {

            int u = edge[0];
            int v = edge[1];

            graph[u].add(v);
            graph[v].add(u);
        }

        int[] color =
                new int[n + 1];

        Arrays.fill(color, -1);

        for (int i = 1; i <= n; i++) {

            if (color[i] == -1) {

                if (!dfs(
                        i,
                        0,
                        graph,
                        color
                    )) {

                    return false;
                }
            }
        }

        return true;
    }

    private boolean dfs(
            int node,
            int currentColor,
            List<Integer>[] graph,
            int[] color) {

        color[node] =
                currentColor;

        for (int neighbor :
                graph[node]) {

            if (color[neighbor] == -1) {

                if (!dfs(
                        neighbor,
                        1 - currentColor,
                        graph,
                        color
                    )) {

                    return false;
                }

            } else if (
                color[neighbor]
                == currentColor
            ) {

                return false;
            }
        }

        return true;
    }
}
```

### Complexity

```text
Time  : O(V + E)

Space : O(V)
```

---

# Complexity Summary

| Algorithm | Time | Space |
|------------|--------|--------|
| BFS Coloring | O(V+E) | O(V) |
| DFS Coloring | O(V+E) | O(V) |
| Is Bipartite | O(V+E) | O(V) |
| Possible Bipartition | O(V+E) | O(V) |

---

# Interview Cheat Sheet

| Question Says | Pattern |
|--------------|----------|
| Two Groups | Bipartite |
| Two Teams | Bipartite |
| Enemy Graph | Bipartite |
| Dislike Relationship | Bipartite |
| No Adjacent Same Group | Bipartite |
| Graph Coloring | Bipartite |
| Possible Bipartition | Bipartite |

---

# Memory Trick

```text
Color 0

Color 1

Neighbor
=
Opposite Color
```

```text
Same Color Neighbor
=
Not Bipartite
```

```text
Odd Cycle
=
Not Bipartite
```

```text
Even Cycle
=
Bipartite
```

---

# Key Takeaway

```text
Need Two Groups?
→ Bipartite

Need Team Assignment?
→ Bipartite

Need Enemy Separation?
→ Bipartite

Solution:
Graph Coloring
(BFS or DFS)
```