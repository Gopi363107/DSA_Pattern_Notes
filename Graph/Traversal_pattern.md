# Graph Traversal Pattern (Foundation)

---

# Definition

The **Graph Traversal Pattern** is used to:

```text
Visit every reachable node
Explore connected nodes
Count connected groups
Check reachability
```

The two main traversal techniques are:

```text
DFS (Depth First Search)
BFS (Breadth First Search)
```

---

# Core Idea

A graph can contain:

```text
Nodes (Vertices)
Edges (Connections)
```

Graph Traversal means:

```text
Systematically visiting nodes
without visiting the same node repeatedly.
```

We maintain:

```text
Visited Array / Set
```

to avoid infinite loops.

---

# When To Use This Pattern

Use Graph Traversal when the problem asks:

```text
Visit all nodes

Explore all connected nodes

Count islands

Count groups/components

Can we reach destination?

Traverse graph

Find connected region

Flood fill

Spread through graph

Visit every cell

Find all reachable nodes
```

---

# Trigger Words

## DFS Triggers

```text
Explore deeply

Visit all connected nodes

Backtracking

Tree traversal

Island problems

Connected regions
```

---

## BFS Triggers

```text
Level order traversal

Minimum steps

Shortest path in unweighted graph

Spread process

Nearest node

Multi-source traversal
```

---

## Connected Components Triggers

```text
Count groups

Count islands

Number of provinces

Independent networks

Disconnected graph
```

---

# DFS Traversal

## Core Idea

Go as deep as possible before coming back.

Example:

```text
1
|
2
|
3
|
4
```

Traversal:

```text
1 → 2 → 3 → 4
```

---

## DFS Template (Graph)

```java
void dfs(int node, List<Integer>[] graph, boolean[] visited) {

    visited[node] = true;

    for (int neighbor : graph[node]) {

        if (!visited[neighbor]) {
            dfs(neighbor, graph, visited);
        }

    }
}
```

---

# BFS Traversal

## Core Idea

Visit nodes level by level.

Example:

```text
        1
      /   \
     2     3
    / \   / \
   4  5  6  7
```

Traversal:

```text
1

2 3

4 5 6 7
```

---

## BFS Template (Graph)

```java
void bfs(int start, List<Integer>[] graph) {

    Queue<Integer> queue = new LinkedList<>();
    boolean[] visited = new boolean[graph.length];

    queue.offer(start);
    visited[start] = true;

    while (!queue.isEmpty()) {

        int node = queue.poll();

        for (int neighbor : graph[node]) {

            if (!visited[neighbor]) {

                visited[neighbor] = true;
                queue.offer(neighbor);

            }
        }
    }
}
```

---

# Connected Components

## Core Idea

If graph is disconnected:

```text
Component 1:
1 - 2 - 3

Component 2:
4 - 5

Component 3:
6
```

Answer:

```text
3 Components
```

---

## Template

```java
int countComponents(List<Integer>[] graph) {

    int n = graph.length;

    boolean[] visited = new boolean[n];

    int components = 0;

    for (int i = 0; i < n; i++) {

        if (!visited[i]) {

            dfs(i, graph, visited);
            components++;

        }
    }

    return components;
}
```

---

# Pattern Recognition Flow

## Step 1

Ask:

```text
Do I need to explore connected nodes?
```

If YES:

```text
DFS or BFS
```

---

## Step 2

Ask:

```text
Need shortest path in unweighted graph?
```

If YES:

```text
BFS
```

---

## Step 3

Ask:

```text
Need count of groups/islands/components?
```

If YES:

```text
Connected Components
```

---

# Problem 1

## LC 733 — Flood Fill

### Problem

Given an image grid:

```text
Change all connected cells having
the same color as starting cell.
```

---

### Example

```text
1 1 1
1 1 0
1 0 1
```

Start:

```text
(1,1)
```

New Color:

```text
2
```

Output:

```text
2 2 2
2 2 0
2 0 1
```

---

### Pattern Recognition

Trigger words:

```text
Connected cells

Explore region

Change entire area
```

This is:

```text
DFS Traversal
```

---

### Solution

```java
class Solution {

    int[][] directions = {
        {1,0},
        {-1,0},
        {0,1},
        {0,-1}
    };

    public int[][] floodFill(
        int[][] image,
        int sr,
        int sc,
        int color
    ) {

        int original = image[sr][sc];

        if (original == color)
            return image;

        dfs(image, sr, sc, original, color);

        return image;
    }

    private void dfs(
        int[][] image,
        int row,
        int col,
        int original,
        int color
    ) {

        if (row < 0 || col < 0 ||
            row >= image.length ||
            col >= image[0].length)
            return;

        if (image[row][col] != original)
            return;

        image[row][col] = color;

        for (int[] dir : directions) {

            dfs(
                image,
                row + dir[0],
                col + dir[1],
                original,
                color
            );

        }
    }
}
```

---

### Complexity

```text
Time  : O(m × n)

Space : O(m × n)
```

---

# Problem 2

## LC 841 — Keys and Rooms

### Problem

Each room contains keys to other rooms.

Determine:

```text
Can we visit every room?
```

---

### Pattern Recognition

Trigger words:

```text
Reachability

Visit all nodes

Can reach every room
```

Graph traversal.

Use:

```text
DFS
```

---

### Solution

```java
class Solution {

    public boolean canVisitAllRooms(List<List<Integer>> rooms) {

        boolean[] visited =
                new boolean[rooms.size()];

        dfs(0, rooms, visited);

        for (boolean room : visited) {

            if (!room)
                return false;

        }

        return true;
    }

    private void dfs(
        int room,
        List<List<Integer>> rooms,
        boolean[] visited
    ) {

        visited[room] = true;

        for (int next : rooms.get(room)) {

            if (!visited[next]) {

                dfs(next, rooms, visited);

            }
        }
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

## LC 200 — Number of Islands

### Problem

Count the number of islands.

Island means:

```text
Connected group of '1'
```

---

### Example

```text
1 1 0 0

1 1 0 0

0 0 1 0

0 0 0 1
```

Answer:

```text
3
```

---

### Pattern Recognition

Trigger words:

```text
Count islands

Count connected groups

Count regions
```

This is:

```text
Connected Components
```

---

### Core Idea

Whenever we find:

```text
Unvisited land
```

Start DFS.

Entire island becomes visited.

Increase count.

---

### Solution

```java
class Solution {

    int[][] directions = {
        {1,0},
        {-1,0},
        {0,1},
        {0,-1}
    };

    public int numIslands(char[][] grid) {

        int islands = 0;

        for (int row = 0;
             row < grid.length;
             row++) {

            for (int col = 0;
                 col < grid[0].length;
                 col++) {

                if (grid[row][col] == '1') {

                    dfs(grid, row, col);
                    islands++;

                }
            }
        }

        return islands;
    }

    private void dfs(
        char[][] grid,
        int row,
        int col
    ) {

        if (row < 0 || col < 0 ||
            row >= grid.length ||
            col >= grid[0].length ||
            grid[row][col] == '0')
            return;

        grid[row][col] = '0';

        for (int[] dir : directions) {

            dfs(
                grid,
                row + dir[0],
                col + dir[1]
            );

        }
    }
}
```

---

### Complexity

```text
Time  : O(m × n)

Space : O(m × n)
```

---

# Problem 4

## LC 695 — Max Area of Island

### Problem

Find:

```text
Largest island size
```

---

### Example

```text
1 1 0

1 1 0

0 0 1
```

Areas:

```text
4

1
```

Answer:

```text
4
```

---

### Pattern Recognition

Trigger words:

```text
Connected region

Explore island

Maximum area
```

Graph Traversal + DFS.

---

### Core Idea

DFS returns:

```text
Current island size
```

Keep maximum.

---

### Solution

```java
class Solution {

    int[][] directions = {
        {1,0},
        {-1,0},
        {0,1},
        {0,-1}
    };

    public int maxAreaOfIsland(int[][] grid) {

        int maxArea = 0;

        for (int row = 0;
             row < grid.length;
             row++) {

            for (int col = 0;
                 col < grid[0].length;
                 col++) {

                if (grid[row][col] == 1) {

                    maxArea = Math.max(
                        maxArea,
                        dfs(grid, row, col)
                    );

                }
            }
        }

        return maxArea;
    }

    private int dfs(
        int[][] grid,
        int row,
        int col
    ) {

        if (row < 0 || col < 0 ||
            row >= grid.length ||
            col >= grid[0].length ||
            grid[row][col] == 0)
            return 0;

        grid[row][col] = 0;

        int area = 1;

        for (int[] dir : directions) {

            area += dfs(
                grid,
                row + dir[0],
                col + dir[1]
            );

        }

        return area;
    }
}
```

---

### Complexity

```text
Time  : O(m × n)

Space : O(m × n)
```

---

# Interview Cheat Sheet

| If Question Says | Pattern |
|------------------|----------|
| Visit all nodes | DFS / BFS |
| Reach node X | DFS / BFS |
| Can visit every node | DFS / BFS |
| Count islands | Connected Components |
| Count groups | Connected Components |
| Count provinces | Connected Components |
| Flood fill | DFS |
| Explore region | DFS |
| Shortest path (unweighted) | BFS |
| Level order traversal | BFS |
| Spread process | BFS |
| Maximum island area | DFS |

---

# Key Takeaway

```text
DFS
→ Deep exploration

BFS
→ Level-by-level exploration

Connected Components
→ Count disconnected groups

Graph Traversal Pattern
→ Foundation of all graph problems
```

Next Patterns:

```text
1. Cycle Detection Pattern
2. Topological Sort Pattern
3. Shortest Path Pattern
4. Union Find Pattern
5. Multi Source BFS Pattern
6. Grid Traversal Pattern
7. Backtracking on Graph Pattern
```