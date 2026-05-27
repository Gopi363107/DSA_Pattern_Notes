# Prefix Sum Pattern — 2D Prefix Sum Notes

---

# Definition

The **2D Prefix Sum** pattern preprocesses cumulative sums in a matrix so that:

```text
Any rectangular submatrix sum
can be answered in O(1)
```

Instead of recalculating all cells repeatedly.

---

# Core Intuition

In 1D prefix sum:

```text
We store cumulative row sums
```

In 2D prefix sum:

```text
We store cumulative rectangle sums
```

Each cell stores:

```text
Sum of all elements
from (0,0) → (r,c)
```

---

# MOST IMPORTANT FORMULA

Let:

```text
prefix[r][c]
```

represent:

```text
Sum of rectangle
(0,0) → (r,c)
```

Then:

```text
prefix[r][c]
=
matrix[r][c]
+
top
+
left
-
overlap
```

Formula:

```text
prefix[r][c]
=
matrix[r][c]
+
prefix[r-1][c]
+
prefix[r][c-1]
-
prefix[r-1][c-1]
```

---

# Why Subtract Overlap?

Because:

```text
top + left
```

counts common region TWICE.

So we remove duplicate overlap.

This is the ENTIRE foundation.

---

# Visualization

```text
+---------+
| overlap | left
|---------|
| top     | current
+---------+
```

When adding:

```text
top + left
```

the overlap region gets added twice.

So:

```text
Subtract overlap once
```

---

# When Should I Think About 2D Prefix Sum?

Use this pattern when:

- matrix range sum queries
- rectangle sum
- submatrix calculations
- multiple rectangle queries
- image/grid cumulative operations

---

# Recognition Triggers

If problem contains:

- "submatrix sum"
- "rectangle sum"
- "2D range query"
- "grid sum"
- "many matrix queries"
- "sum region"

→ Think:

```text
2D Prefix Sum
```

---

# Generic Template

## Building 2D Prefix Sum

```java
int rows = matrix.length;
int cols = matrix[0].length;

int[][] prefix =
    new int[rows + 1][cols + 1];

for(int r = 1; r <= rows; r++) {

    for(int c = 1; c <= cols; c++) {

        prefix[r][c] =
            matrix[r - 1][c - 1]
            + prefix[r - 1][c]
            + prefix[r][c - 1]
            - prefix[r - 1][c - 1];
    }
}
```

---

# MOST IMPORTANT QUERY FORMULA

To find rectangle sum:

```text
(r1,c1) → (r2,c2)
```

Formula:

```text
prefix[r2][c2]
-
top
-
left
+
overlap
```

Actual formula:

```text
sum =
prefix[r2+1][c2+1]
-
prefix[r1][c2+1]
-
prefix[r2+1][c1]
+
prefix[r1][c1]
```

---

# MOST IMPORTANT INSIGHT

Exactly like 1D prefix sum:

```text
Current rectangle
-
extra regions
+
overlap correction
```

Same inclusion-exclusion principle.

---

# Pattern 1 — Range Sum Query 2D Immutable

---

## Trigger

- many rectangle queries
- immutable matrix
- repeated submatrix sums

---

## Problem

LeetCode 304 — Range Sum Query 2D Immutable

---

# Key Insight

Precompute all cumulative rectangle sums once.

Then each query becomes:

```text
Constant-time rectangle extraction
```

---

## Solution

```java
class NumMatrix {

    int[][] prefix;

    public NumMatrix(int[][] matrix) {

        int rows = matrix.length;
        int cols = matrix[0].length;

        prefix =
            new int[rows + 1][cols + 1];

        for(int r = 1; r <= rows; r++) {

            for(int c = 1; c <= cols; c++) {

                prefix[r][c] =
                    matrix[r - 1][c - 1]
                    + prefix[r - 1][c]
                    + prefix[r][c - 1]
                    - prefix[r - 1][c - 1];
            }
        }
    }

    public int sumRegion(
        int row1,
        int col1,
        int row2,
        int col2
    ) {

        return
            prefix[row2 + 1][col2 + 1]
            - prefix[row1][col2 + 1]
            - prefix[row2 + 1][col1]
            + prefix[row1][col1];
    }
}
```

---

# Complexity

## Preprocessing

```text
O(rows × cols)
```

## Query Time

```text
O(1)
```

## Space Complexity

```text
O(rows × cols)
```

---

# CP-Level Insight

Without preprocessing:

```text
Each query scans rectangle
```

Worst case:

```text
O(rows × cols)
```

With many queries:

```text
Very slow
```

2D prefix sum converts it into:

```text
Instant rectangle retrieval
```

---

# Dry Run

Matrix:

```text
1 2 3
4 5 6
7 8 9
```

---

# Prefix Matrix

```text
1  3   6
5 12  21
12 27 45
```

Each cell stores:

```text
Total rectangle sum
from origin
```

---

# Query Example

Rectangle:

```text
(1,1) → (2,2)
```

Submatrix:

```text
5 6
8 9
```

Answer:

```text
28
```

Using formula:

```text
45 - 6 - 12 + 1
=
28
```

---

# Pattern 2 — Maximum Sum Submatrix (Optimization Extension)

---

## Trigger

- rectangle optimization
- max rectangle sum
- 2D Kadane relation

---

# Key Insight

Compress rows into:

```text
1D array
```

Then apply:

```text
Kadane’s Algorithm
```

This is advanced CP optimization.

---

# Complexity

Typical optimized complexity:

```text
O(rows² × cols)
```

instead of brute force:

```text
O(n⁴)
```

VERY important interview pattern.

---

# Advanced Competitive Programming Insights

---

# 1. Inclusion-Exclusion Principle

2D prefix sum is entirely based on:

```text
Add needed regions
Subtract duplicate overlap
```

Classic mathematical idea.

---

# 2. Preprocessing vs Query Tradeoff

Spend:

```text
O(n²)
```

once,

to answer future queries in:

```text
O(1)
```

Common CP optimization strategy.

---

# 3. Prefix Sum Generalizes To Dimensions

| Dimension | Pattern |
|---|---|
| 1D | Prefix array |
| 2D | Prefix matrix |
| 3D | Prefix cube |

Same mathematical principle scales.

---

# 4. Rectangle Problems Often Reduce To Prefix Sums

Many grid problems become easy after:

```text
Cumulative preprocessing
```

Very common in competitive programming.

---

# Common Mistake

Students forget:

```text
Subtract overlap
```

This causes:

```text
Double counting
```

Always remember:

```text
+ top
+ left
- overlap
```

---

# One-Line Memory Trick

```text
2D prefix sum =
Rectangle accumulation
with overlap correction.
```

---

# Final Interview Insight

The REAL power of 2D prefix sum is:

```text
Turning expensive rectangle scans
into instant mathematical lookups
```

Instead of recalculating:

```text
Entire submatrices
```

we preprocess reusable cumulative information.

This transforms many:

```text
O(n² × q)
```

solutions into:

```text
O(n² + q)
```