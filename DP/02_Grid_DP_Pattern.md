# 02 - Grid Dynamic Programming Pattern

> **Core Idea:** Solve problems where the state is represented by a **cell in a 2D grid**, and each cell's answer depends on previously computed neighboring cells.

---

# What is Grid DP?

Grid DP is used when:

- The input is a **2D matrix/grid**.
- You move from one cell to another following certain rules.
- The answer for a cell depends on answers from adjacent cells.

Typical state:

```
dp[i][j]
```

where

```
i = row
j = column
```

---

# Core Idea

Suppose

```
dp[i][j]
```

means

- Minimum cost to reach `(i, j)`
- Number of ways to reach `(i, j)`
- Maximum score till `(i, j)`
- Maximum path sum ending at `(i, j)`

Each state is computed from previously solved neighboring cells.

---

# When Should You Think of Grid DP?

Whenever the problem contains:

- Matrix
- Grid
- Board
- Dungeon
- Triangle
- Chessboard
- Robot movement
- Path counting
- Path optimization

Immediately ask:

> Can I define the answer for each cell independently?

If YES, Grid DP is likely the correct approach.

---

# Common Movement Directions

### Right and Down

```
↓

→
```

Example:

- Unique Paths
- Minimum Path Sum

---

### Right, Down, Diagonal

```
↘
→
↓

```

Example:

- Some image processing problems

---

### Down-Left, Down, Down-Right

```
↙
↓
↘
```

Example:

- Minimum Falling Path Sum

---

### Four Directions

```
↑
↓

← →

```

Usually requires:

- DFS + Memoization
- Graph + DP

Example:

- Longest Increasing Path in Matrix

---

# State Definition

Always define

```
dp[i][j]
```

Example

```
Minimum cost to reach cell (i,j)
```

or

```
Maximum chocolates collected till (i,j)
```

---

# Generic Thinking Process

## Step 1

Define State

```
dp[i][j]
```

---

## Step 2

Find Transition

Where can we come from?

Example

```
Top

Left
```

---

## Step 3

Base Case

Usually

```
dp[0][0]
```

or

```
first row

first column
```

---

## Step 4

Iteration Order

Must compute parents before children.

Usually

```
Top → Bottom

Left → Right
```

---

## Step 5

Optimization

If only previous row is required

↓

Space Optimization

---

# Generic Template

```java
int[][] dp = new int[m][n];

dp[0][0] = base;

for(int i = 0; i < m; i++){

    for(int j = 0; j < n; j++){

        // transition

    }
}

return dp[m-1][n-1];
```

---

# Memoization Template

```java
int solve(int i, int j){

    if(base case)
        return value;

    if(dp[i][j] != -1)
        return dp[i][j];

    return dp[i][j] = transition;
}
```

---

# Space Optimization Template

If only previous row is needed:

```java
int[] prev = new int[n];

for(int i = 0; i < m; i++){

    int[] curr = new int[n];

    // fill curr

    prev = curr;
}
```

Space

```
O(n)
```

instead of

```
O(m*n)
```

---

# Pattern Recognition

Question contains

```
Grid

Matrix

Board

Robot

Triangle

Dungeon
```

↓

State

```
dp[i][j]
```

↓

Movement

↓

Transition

↓

Memoization

↓

Tabulation

↓

Space Optimization

---

# Competitive Programming Insight

Grid DP is often just **1D DP extended to two dimensions**.

Instead of

```
dp[i]
```

we now have

```
dp[i][j]
```

---

# Problem 1

## LeetCode 62 — Unique Paths

Difficulty

Easy

---

## Core Idea

Robot moves only

- Right
- Down

Count total paths.

---

## State

```
dp[i][j]

Number of ways to reach (i,j)
```

---

## Recurrence

```
dp[i][j]
=
dp[i-1][j]
+
dp[i][j-1]
```

---

## Java Solution

```java
class Solution {

    public int uniquePaths(int m, int n) {

        int[][] dp = new int[m][n];

        for(int i = 0; i < m; i++)
            dp[i][0] = 1;

        for(int j = 0; j < n; j++)
            dp[0][j] = 1;

        for(int i = 1; i < m; i++){

            for(int j = 1; j < n; j++){

                dp[i][j] = dp[i-1][j] + dp[i][j-1];

            }
        }

        return dp[m-1][n-1];
    }
}
```

### Time Complexity

```
O(m*n)
```

### Space Complexity

```
O(m*n)
```

---

### Space Optimization

```
O(n)
```

using one array.

---

# Problem 2

## LeetCode 64 — Minimum Path Sum

Difficulty

Medium

---

## Core Idea

Choose the minimum cost path.

---

## State

```
dp[i][j]

Minimum cost to reach (i,j)
```

---

## Recurrence

```
dp[i][j]
=
grid[i][j]
+
min(
dp[i-1][j],
dp[i][j-1]
)
```

---

## Java Solution

```java
class Solution {

    public int minPathSum(int[][] grid) {

        int m = grid.length;
        int n = grid[0].length;

        int[][] dp = new int[m][n];

        dp[0][0] = grid[0][0];

        for(int i = 1; i < m; i++)
            dp[i][0] = dp[i-1][0] + grid[i][0];

        for(int j = 1; j < n; j++)
            dp[0][j] = dp[0][j-1] + grid[0][j];

        for(int i = 1; i < m; i++){

            for(int j = 1; j < n; j++){

                dp[i][j] = grid[i][j] +
                        Math.min(dp[i-1][j], dp[i][j-1]);

            }
        }

        return dp[m-1][n-1];
    }
}
```

---

### Time Complexity

```
O(m*n)
```

### Space Complexity

```
O(m*n)
```

---

# Problem 3

## LeetCode 931 — Minimum Falling Path Sum

Difficulty

Medium

---

## Core Idea

From each cell, move to:

- Down
- Down-Left
- Down-Right

Find the minimum path sum.

---

## State

```
dp[i][j]

Minimum path sum ending at (i,j)
```

---

## Recurrence

```
dp[i][j]
=
matrix[i][j]
+
min(
up,
up-left,
up-right
)
```

---

## Java Solution

```java
class Solution {

    public int minFallingPathSum(int[][] matrix) {

        int n = matrix.length;

        int[][] dp = new int[n][n];

        for(int j = 0; j < n; j++)
            dp[0][j] = matrix[0][j];

        for(int i = 1; i < n; i++){

            for(int j = 0; j < n; j++){

                int up = dp[i-1][j];

                int left = j > 0 ? dp[i-1][j-1] : Integer.MAX_VALUE;

                int right = j < n-1 ? dp[i-1][j+1] : Integer.MAX_VALUE;

                dp[i][j] = matrix[i][j] +
                        Math.min(up, Math.min(left, right));

            }
        }

        int ans = Integer.MAX_VALUE;

        for(int j = 0; j < n; j++)
            ans = Math.min(ans, dp[n-1][j]);

        return ans;
    }
}
```

---

### Time Complexity

```
O(n²)
```

### Space Complexity

```
O(n²)
```

---

### Optimization

Store only the previous row.

Space

```
O(n)
```

---

# Common Mistakes

❌ Wrong iteration order

❌ Ignoring boundary cells

❌ Incorrect initialization of first row/column

❌ Forgetting blocked cells (obstacles)

❌ Accessing invalid indices

---

# Mental Checklist During Interviews

- What does `dp[i][j]` represent?
- From which neighboring cells can I reach `(i, j)`?
- What are the base cases?
- What is the correct traversal order?
- Can I optimize from `O(m*n)` space to `O(n)`?

---

# Pattern Summary

| Feature | Description |
|----------|-------------|
| State | `dp[i][j]` |
| Dimension | 2D |
| Direction | Depends on movement rules |
| Transition | Neighboring cells |
| Time Complexity | Usually `O(m*n)` |
| Space | `O(m*n)` → often `O(n)` |
| Common Topics | Paths, Cost, Obstacles, Triangle, Matrix |

---

# Mastery Checklist

- [ ] Recognize Grid DP problems.
- [ ] Define `dp[i][j]`.
- [ ] Derive transitions from neighboring cells.
- [ ] Write Memoization.
- [ ] Convert to Tabulation.
- [ ] Optimize to one-row DP when possible.
- [ ] Solve Unique Paths, Minimum Path Sum, and Minimum Falling Path Sum without notes.

---

> **Golden Rule:** If each cell's answer depends on previously visited neighboring cells, think **Grid Dynamic Programming**.