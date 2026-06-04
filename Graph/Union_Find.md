# Union Find (DSU) Pattern

## Definition

Union Find (Disjoint Set Union - DSU) is used to efficiently:

```text
Maintain Connected Components

Merge Groups

Check Connectivity

Detect Cycles
```

---

## When To Use

Use when the problem asks:

```text
Connectivity

Connected Components

Merge Groups

Network Connections

Dynamic Components

Cycle Detection

Friend Circles

Number of Provinces
```

---

## Trigger Words

```text
Connected?

Same Group?

Merge Components

Union Sets

Network Connection

Redundant Connection

Dynamic Graph
```

---

# Core Idea

Each node initially belongs to its own group.

```text
1   2   3   4
```

After:

```text
Union(1,2)

Union(2,3)
```

Groups become:

```text
1 - 2 - 3

4
```

Now:

```text
Find(1) == Find(3)
```

means:

```text
Same Component
```

---

# Operations

## Find

Returns:

```text
Ultimate Parent
```

Example:

```text
1 → 2 → 3

Find(1) = 3
Find(2) = 3
Find(3) = 3
```

---

## Union

Merges two components.

```java
union(u, v)
```

---

# Path Compression

## Idea

Without compression:

```text
1 → 2 → 3 → 4 → 5
```

Find becomes expensive.

After Path Compression:

```text
      5
    / | \
   1  2  3  4
```

Future Find operations become:

```text
Almost O(1)
```

---

# Union by Rank

## Idea

Always attach:

```text
Smaller Tree

to

Larger Tree
```

This prevents deep chains.

---

# DSU Template

```java
class DSU {

    int[] parent;
    int[] rank;

    DSU(int n) {

        parent = new int[n];
        rank = new int[n];

        for (int i = 0; i < n; i++) {

            parent[i] = i;
        }
    }

    int find(int node) {

        if (parent[node] == node) {

            return node;
        }

        return parent[node] =
                find(parent[node]);
    }

    void union(int u, int v) {

        int parentU = find(u);
        int parentV = find(v);

        if (parentU == parentV) {

            return;
        }

        if (rank[parentU] <
            rank[parentV]) {

            parent[parentU] =
                    parentV;

        } else if (
            rank[parentV] <
            rank[parentU]
        ) {

            parent[parentV] =
                    parentU;

        } else {

            parent[parentV] =
                    parentU;

            rank[parentU]++;
        }
    }
}
```

---

# Pattern Recognition

## Step 1

Ask:

```text
Need Connectivity Check?
```

If YES:

```text
DSU
```

---

## Step 2

Ask:

```text
Need Dynamic Merging?
```

If YES:

```text
DSU
```

---

## Step 3

Ask:

```text
Need Connected Components?
```

If YES:

```text
DSU
```

---

## Step 4

Ask:

```text
Cycle Detection in
Undirected Graph?
```

If YES:

```text
DSU
```

---

# Problem 1

## LC 547 - Number of Provinces

### Recognition

```text
Connected Cities

Number of Groups

Connected Components
```

Pattern:

```text
DSU
```

---

### Core Idea

Initially:

```text
Every City

=
Own Province
```

Whenever:

```text
isConnected[i][j] == 1
```

Union them.

Count unique parents.

---

### Solution

```java
class Solution {

    public int findCircleNum(
            int[][] isConnected) {

        int n = isConnected.length;

        DSU dsu = new DSU(n);

        for (int i = 0; i < n; i++) {

            for (int j = i + 1;
                 j < n;
                 j++) {

                if (isConnected[i][j] == 1) {

                    dsu.union(i, j);
                }
            }
        }

        int provinces = 0;

        for (int i = 0; i < n; i++) {

            if (dsu.find(i) == i) {

                provinces++;
            }
        }

        return provinces;
    }
}
```

### Complexity

```text
Time  : O(n²)

Space : O(n)
```

---

# Problem 2

## LC 684 - Redundant Connection

### Recognition

```text
Extra Edge

Cycle Detection

Undirected Graph
```

Pattern:

```text
DSU
```

---

### Core Idea

Before union:

```text
Check Parent
```

If:

```text
find(u) == find(v)
```

Then:

```text
Cycle Found
```

Return current edge.

---

### Solution

```java
class Solution {

    public int[] findRedundantConnection(
            int[][] edges) {

        int n = edges.length;

        DSU dsu =
                new DSU(n + 1);

        for (int[] edge : edges) {

            int u = edge[0];
            int v = edge[1];

            if (dsu.find(u)
                == dsu.find(v)) {

                return edge;
            }

            dsu.union(u, v);
        }

        return new int[0];
    }
}
```

### Complexity

```text
Time  : O(N α(N))

Space : O(N)
```

---

# Problem 3

## LC 1319 - Number of Operations to Make Network Connected

### Recognition

```text
Connect Network

Minimum Operations

Merge Components
```

Pattern:

```text
DSU
```

---

### Core Idea

Need:

```text
components - 1
```

extra cables.

First check:

```text
connections.length

>=

n - 1
```

Otherwise impossible.

---

### Solution

```java
class Solution {

    public int makeConnected(
            int n,
            int[][] connections) {

        if (connections.length
            < n - 1) {

            return -1;
        }

        DSU dsu =
                new DSU(n);

        for (int[] edge :
                connections) {

            dsu.union(
                edge[0],
                edge[1]
            );
        }

        int components = 0;

        for (int i = 0; i < n; i++) {

            if (dsu.find(i) == i) {

                components++;
            }
        }

        return components - 1;
    }
}
```

### Complexity

```text
Time  : O(N α(N))

Space : O(N)
```

---

# Complexity Summary

| Operation | Complexity |
|------------|------------|
| Find | O(α(n)) |
| Union | O(α(n)) |
| DSU Space | O(n) |

---

# Interview Cheat Sheet

| Question Says | Pattern |
|--------------|----------|
| Connected Components | DSU |
| Number of Provinces | DSU |
| Same Group | DSU |
| Merge Groups | DSU |
| Dynamic Connectivity | DSU |
| Redundant Edge | DSU |
| Cycle Detection | DSU |
| Network Connection | DSU |

---

# Memory Trick

```text
Find
=
Ultimate Parent
```

```text
Union
=
Merge Components
```

```text
Path Compression
=
Flatten Tree
```

```text
Union By Rank
=
Attach Smaller Tree
```

```text
Same Parent
=
Same Component
```

---

# Key Takeaway

```text
Need Connectivity?
→ DSU

Need Dynamic Merging?
→ DSU

Need Component Counting?
→ DSU

Need Fast Cycle Detection?
→ DSU

Core Operations:

Find
Union
Path Compression
Union By Rank
```