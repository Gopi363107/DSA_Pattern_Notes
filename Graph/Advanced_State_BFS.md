# Advanced State BFS Pattern

## Definition

Normal BFS stores:

```text
(node)
```

Advanced State BFS stores:

```text
(node, state)
```

because reaching the same node with different states can produce different answers.

---

## When To Use

Use when the problem contains:

```text
Position

Keys Collected

Visited Nodes

Inventory

Doors

Masks

Additional Information
```

---

## Trigger Words

```text
Collect All Keys

Visit All Nodes

State Changes

Inventory

Shortest Path + Constraints

Keys and Locks

Bitmask
```

---

# Core Idea

Normal BFS:

```text
(node)
```

Advanced BFS:

```text
(node, state)
```

Example:

```text
Cell (2,3)

Keys = 001
```

and

```text
Cell (2,3)

Keys = 111
```

are completely different states.

---

# Why Normal BFS Fails

Example:

```text
Reach Cell A

without key
```

and later:

```text
Reach Cell A

with key
```

These are not the same.

Therefore visited should be:

```text
(row, col, keys)
```

instead of:

```text
(row, col)
```

---

# State Representation

## Bitmask

Store information using bits.

Example:

```text
a b c
```

Keys:

```text
000

001 -> a

010 -> b

100 -> c

111 -> a,b,c
```

---

## Common Operations

### Add State

```java
mask |= (1 << key);
```

---

### Check State

```java
(mask & (1 << key)) != 0
```

---

### All Collected

```java
mask == targetMask
```

---

# BFS + State Template

```java
Queue<int[]> queue =
        new LinkedList<>();

queue.offer(
    new int[]{
        startNode,
        startMask
    }
);

boolean[][] visited =
        new boolean[n][1 << k];

visited[startNode][startMask]
        = true;

while (!queue.isEmpty()) {

    int[] current =
            queue.poll();

    int node = current[0];
    int mask = current[1];

    for (int neighbor :
            graph[node]) {

        int nextMask = mask;

        if (!visited[
                neighbor
            ][
                nextMask
            ]) {

            visited[
                neighbor
            ][
                nextMask
            ] = true;

            queue.offer(
                new int[]{
                    neighbor,
                    nextMask
                }
            );
        }
    }
}
```

---

# Pattern Recognition

## Step 1

Ask:

```text
Is Position Alone Enough?
```

If NO:

```text
State BFS
```

---

## Step 2

Ask:

```text
Need Keys?
Need Inventory?
Need Collected Items?
```

If YES:

```text
State BFS
```

---

## Step 3

Ask:

```text
Need Visit All Nodes?
```

If YES:

```text
Bitmask BFS
```

---

## Step 4

Ask:

```text
Shortest Path

+

Additional Information?
```

If YES:

```text
State BFS
```

---

# Problem 1

## LC 864 - Shortest Path to Get All Keys

### Recognition

```text
Grid

Keys

Locks

Shortest Path

Collect Everything
```

Pattern:

```text
BFS + Bitmask
```

---

### Core Idea

State:

```text
(row, col, keysMask)
```

Need to know:

```text
Current Position

+

Keys Collected
```

because keys unlock doors.

---

### State Example

```text
Position = (2,3)

Keys = 101
```

means:

```text
a collected

c collected
```

---

### Solution

```java
class Solution {

    public int shortestPathAllKeys(
            String[] grid) {

        int rows = grid.length;
        int cols = grid[0].length();

        Queue<int[]> queue =
                new LinkedList<>();

        boolean[][][] visited =
                new boolean
                [rows]
                [cols]
                [64];

        int allKeys = 0;

        for (int r = 0; r < rows; r++) {

            for (int c = 0; c < cols; c++) {

                char ch =
                        grid[r].charAt(c);

                if (ch == '@') {

                    queue.offer(
                        new int[]{
                            r,c,0
                        }
                    );

                    visited[r][c][0]
                            = true;
                }

                if (ch >= 'a'
                    && ch <= 'f') {

                    allKeys |=
                        (1 <<
                        (ch - 'a'));
                }
            }
        }

        int[][] directions = {

            {-1,0},
            {1,0},
            {0,-1},
            {0,1}
        };

        int steps = 0;

        while (!queue.isEmpty()) {

            int size =
                    queue.size();

            for (int i = 0;
                 i < size;
                 i++) {

                int[] current =
                        queue.poll();

                int row =
                        current[0];

                int col =
                        current[1];

                int mask =
                        current[2];

                if (mask == allKeys) {

                    return steps;
                }

                for (int[] dir :
                        directions) {

                    int nr =
                        row + dir[0];

                    int nc =
                        col + dir[1];

                    int nextMask =
                            mask;

                    if (nr < 0 ||
                        nc < 0 ||
                        nr >= rows ||
                        nc >= cols) {

                        continue;
                    }

                    char ch =
                        grid[nr]
                        .charAt(nc);

                    if (ch == '#') {
                        continue;
                    }

                    if (ch >= 'a'
                        && ch <= 'f') {

                        nextMask |=
                            (1 <<
                            (ch - 'a'));
                    }

                    if (ch >= 'A'
                        && ch <= 'F') {

                        if ((mask &
                            (1 <<
                            (ch - 'A')))
                            == 0) {

                            continue;
                        }
                    }

                    if (!visited
                        [nr]
                        [nc]
                        [nextMask]) {

                        visited
                        [nr]
                        [nc]
                        [nextMask]
                        = true;

                        queue.offer(
                            new int[]{
                                nr,
                                nc,
                                nextMask
                            }
                        );
                    }
                }
            }

            steps++;
        }

        return -1;
    }
}
```

### Complexity

```text
Time  : O(M × N × 2^K)

Space : O(M × N × 2^K)
```

---

# Problem 2

## LC 847 - Shortest Path Visiting All Nodes

### Recognition

```text
Visit Every Node

Shortest Path

Graph

Bitmask
```

Pattern:

```text
Multi-Source BFS + Bitmask
```

---

### Core Idea

State:

```text
(node, visitedMask)
```

Example:

```text
Node = 3

Visited = 10111
```

Need:

```text
Current Node

+

Visited Nodes
```

---

### Solution

```java
class Solution {

    public int shortestPathLength(
            int[][] graph) {

        int n = graph.length;

        int targetMask =
                (1 << n) - 1;

        Queue<int[]> queue =
                new LinkedList<>();

        boolean[][] visited =
                new boolean
                [n]
                [1 << n];

        for (int i = 0;
             i < n;
             i++) {

            int mask =
                    (1 << i);

            queue.offer(
                new int[]{
                    i,
                    mask
                }
            );

            visited[i][mask]
                    = true;
        }

        int steps = 0;

        while (!queue.isEmpty()) {

            int size =
                    queue.size();

            for (int i = 0;
                 i < size;
                 i++) {

                int[] current =
                        queue.poll();

                int node =
                        current[0];

                int mask =
                        current[1];

                if (mask
                    == targetMask) {

                    return steps;
                }

                for (int neighbor :
                        graph[node]) {

                    int nextMask =
                        mask |
                        (1 << neighbor);

                    if (!visited
                        [neighbor]
                        [nextMask]) {

                        visited
                        [neighbor]
                        [nextMask]
                            = true;

                        queue.offer(
                            new int[]{
                                neighbor,
                                nextMask
                            }
                        );
                    }
                }
            }

            steps++;
        }

        return -1;
    }
}
```

### Complexity

```text
Time  : O(N × 2^N)

Space : O(N × 2^N)
```

---

# State BFS vs Normal BFS

| Normal BFS | State BFS |
|------------|------------|
| (node) | (node, state) |
| Single Visited | Multi-State Visited |
| Position Only | Position + Extra Info |
| Simpler | More Powerful |

---

# Complexity Summary

| Algorithm | Time | Space |
|------------|--------|--------|
| BFS + State | Depends on State Space | State Space |
| BFS + Bitmask | O(N × 2^N) | O(N × 2^N) |
| Shortest Path All Keys | O(M×N×2^K) | O(M×N×2^K) |
| Visit All Nodes | O(N×2^N) | O(N×2^N) |

---

# Interview Cheat Sheet

| Question Says | Pattern |
|--------------|----------|
| Collect All Keys | BFS + Bitmask |
| Visit All Nodes | BFS + Bitmask |
| Position + Inventory | State BFS |
| Keys and Locks | State BFS |
| Shortest Path + State | State BFS |
| Additional Information | State BFS |
| Graph TSP Variant | BFS + Bitmask |

---

# Memory Trick

```text
Normal BFS

=
(node)
```

```text
State BFS

=
(node, state)
```

```text
Keys

=
Bitmask
```

```text
Visited Nodes

=
Bitmask
```

```text
Shortest Path
+
Extra Information

=
State BFS
```

---

# Key Takeaway

```text
Position Alone Not Enough?
→ State BFS

Need Keys?
→ Bitmask

Need Visit All Nodes?
→ Bitmask BFS

Need Shortest Path
with Extra Information?
→ Advanced State BFS
```