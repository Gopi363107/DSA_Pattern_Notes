# Grid Graph Pattern

## Definition

In Grid Graph problems:

```text
Every Cell
=
Graph Node
```

Neighbors are usually:

```text
Up

Down

Left

Right
```

Sometimes:

```text
8 Directions
(Diagonals Included)
```

---

## When To Use

Use when the problem contains:

```text
Matrix

Grid

2D Array

Islands

Rotting

Rooms

Land/Water

Shortest Path in Grid
```

---

## Trigger Words

```text
Grid

Matrix

Island

Flood Fill

Rotting Oranges

Walls and Gates

Nearest Cell

Distance to Land

Up/Down/Left/Right
```

---

# Core Idea

Treat each cell as a graph node.

Example:

```text
1 1 0

1 0 1

0 1 1
```

becomes:

```text
Graph of Connected Cells
```

Use:

```text
DFS
→ Explore Region

BFS
→ Shortest Distance

Multi-Source BFS
→ Multiple Starting Points
```

---

# Direction Array

Used in almost every grid problem.

```java
int[][] directions = {

    {-1, 0}, // Up
    { 1, 0}, // Down
    { 0,-1}, // Left
    { 0, 1}  // Right
};
```

---

# DFS Template

```java
void dfs(int row,
         int col,
         int[][] grid) {

    int m = grid.length;
    int n = grid[0].length;

    if (row < 0 ||
        col < 0 ||
        row >= m ||
        col >= n ||
        grid[row][col] == 0) {

        return;
    }

    grid[row][col] = 0;

    for (int[] dir : directions) {

        dfs(
            row + dir[0],
            col + dir[1],
            grid
        );
    }
}
```

---

# BFS Template

```java
Queue<int[]> queue =
        new LinkedList<>();

queue.offer(
    new int[]{row, col}
);

while (!queue.isEmpty()) {

    int[] current =
            queue.poll();

    int r = current[0];
    int c = current[1];

    for (int[] dir : directions) {

        int nr = r + dir[0];
        int nc = c + dir[1];

        if (valid cell) {

            queue.offer(
                new int[]{nr, nc}
            );
        }
    }
}
```

---

# Multi-Source BFS

## Core Idea

Instead of:

```text
One Source
```

Start BFS from:

```text
Multiple Sources
```

simultaneously.

Common in:

```text
Rotting Oranges

Walls and Gates

01 Matrix
```

---

## Template

```java
Queue<int[]> queue =
        new LinkedList<>();

for (all source cells) {

    queue.offer(
        new int[]{r, c}
    );
}

while (!queue.isEmpty()) {

    int[] current =
            queue.poll();

    for (int[] dir : directions) {

        int nr = current[0] + dir[0];
        int nc = current[1] + dir[1];

        if (valid cell) {

            queue.offer(
                new int[]{nr, nc}
            );
        }
    }
}
```

---

# Flood Fill Pattern

## Core Idea

Starting from one cell:

```text
Visit Entire Connected Region
```

Usually solved using:

```text
DFS

or

BFS
```

---

# Pattern Recognition

## Step 1

Ask:

```text
Matrix/Grid?
```

If YES:

```text
Grid Graph
```

---

## Step 2

Ask:

```text
Need Region Traversal?
```

If YES:

```text
DFS
```

---

## Step 3

Ask:

```text
Need Minimum Distance?
```

If YES:

```text
BFS
```

---

## Step 4

Ask:

```text
Multiple Starting Cells?
```

If YES:

```text
Multi-Source BFS
```

---

# Problem 1

## LC 994 - Rotting Oranges

### Recognition

```text
Grid

Spread Process

Multiple Rotten Oranges

Minimum Time
```

Pattern:

```text
Multi-Source BFS
```

---

### Core Idea

Initially push:

```text
All Rotten Oranges
```

into queue.

Each BFS level:

```text
1 Minute
```

Rot spreads to fresh oranges.

---

### Solution

```java
class Solution {

    public int orangesRotting(
            int[][] grid) {

        int rows = grid.length;
        int cols = grid[0].length;

        Queue<int[]> queue =
                new LinkedList<>();

        int fresh = 0;

        for (int r = 0;
             r < rows;
             r++) {

            for (int c = 0;
                 c < cols;
                 c++) {

                if (grid[r][c] == 2) {

                    queue.offer(
                        new int[]{r,c}
                    );

                } else if (
                    grid[r][c] == 1
                ) {

                    fresh++;
                }
            }
        }

        int minutes = 0;

        int[][] directions = {

            {-1,0},
            {1,0},
            {0,-1},
            {0,1}
        };

        while (!queue.isEmpty()
                && fresh > 0) {

            int size =
                    queue.size();

            minutes++;

            for (int i = 0;
                 i < size;
                 i++) {

                int[] current =
                        queue.poll();

                for (int[] dir :
                        directions) {

                    int nr =
                        current[0]
                        + dir[0];

                    int nc =
                        current[1]
                        + dir[1];

                    if (nr >= 0 &&
                        nc >= 0 &&
                        nr < rows &&
                        nc < cols &&
                        grid[nr][nc] == 1) {

                        grid[nr][nc] = 2;

                        fresh--;

                        queue.offer(
                            new int[]{
                                nr,nc
                            }
                        );
                    }
                }
            }
        }

        return fresh == 0
                ? minutes
                : -1;
    }
}
```

### Complexity

```text
Time  : O(M × N)

Space : O(M × N)
```

---

# Problem 2

## LC 542 - 01 Matrix

### Recognition

```text
Nearest Zero

Minimum Distance

Grid
```

Pattern:

```text
Multi-Source BFS
```

---

### Core Idea

Push:

```text
All Zero Cells
```

into queue.

Expand outward.

First time reaching a cell:

```text
Shortest Distance Found
```

---

### Solution

```java
class Solution {

    public int[][] updateMatrix(
            int[][] mat) {

        int rows = mat.length;
        int cols = mat[0].length;

        Queue<int[]> queue =
                new LinkedList<>();

        int[][] distance =
                new int[rows][cols];

        for (int r = 0;
             r < rows;
             r++) {

            for (int c = 0;
                 c < cols;
                 c++) {

                if (mat[r][c] == 0) {

                    queue.offer(
                        new int[]{r,c}
                    );

                } else {

                    distance[r][c] = -1;
                }
            }
        }

        int[][] directions = {

            {-1,0},
            {1,0},
            {0,-1},
            {0,1}
        };

        while (!queue.isEmpty()) {

            int[] current =
                    queue.poll();

            for (int[] dir :
                    directions) {

                int nr =
                    current[0]
                    + dir[0];

                int nc =
                    current[1]
                    + dir[1];

                if (nr >= 0 &&
                    nc >= 0 &&
                    nr < rows &&
                    nc < cols &&
                    distance[nr][nc] == -1) {

                    distance[nr][nc] =
                        distance[
                            current[0]
                        ][
                            current[1]
                        ] + 1;

                    queue.offer(
                        new int[]{
                            nr,nc
                        }
                    );
                }
            }
        }

        return distance;
    }
}
```

### Complexity

```text
Time  : O(M × N)

Space : O(M × N)
```

---

# Problem 3

## LC 286 - Walls and Gates

### Recognition

```text
Grid

Nearest Gate

Minimum Distance
```

Pattern:

```text
Multi-Source BFS
```

---

### Core Idea

Push:

```text
All Gates
```

into queue.

Expand simultaneously.

First time reaching a room:

```text
Shortest Distance
```

---

### Interview Insight

These three problems are almost identical:

```text
994 Rotting Oranges

542 01 Matrix

286 Walls and Gates
```

Recognition:

```text
Multiple Sources

Minimum Distance

Grid

→ Multi-Source BFS
```

---

# Complexity Summary

| Algorithm | Time | Space |
|------------|--------|--------|
| DFS Grid Traversal | O(M×N) | O(M×N) |
| BFS Grid Traversal | O(M×N) | O(M×N) |
| Multi-Source BFS | O(M×N) | O(M×N) |
| Flood Fill | O(M×N) | O(M×N) |

---

# Interview Cheat Sheet

| Question Says | Pattern |
|--------------|----------|
| Matrix/Grid | Grid Graph |
| Islands | DFS/BFS |
| Flood Fill | DFS/BFS |
| Nearest Cell | BFS |
| Minimum Distance | BFS |
| Rotting Oranges | Multi-Source BFS |
| Walls and Gates | Multi-Source BFS |
| 01 Matrix | Multi-Source BFS |
| Land/Water Regions | DFS |

---

# Memory Trick

```text
Grid
=
Graph
```

```text
Region Count
=
DFS
```

```text
Shortest Distance
=
BFS
```

```text
Multiple Sources
=
Multi-Source BFS
```

```text
Connected Region
=
Flood Fill
```

---

# Key Takeaway

```text
Matrix Problem?
→ Think Graph

Count Regions?
→ DFS

Minimum Distance?
→ BFS

Multiple Starting Points?
→ Multi-Source BFS

Connected Area Traversal?
→ Flood Fill
```