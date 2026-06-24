# 2D Difference Array

## Core Idea

2D Difference Array extends Difference Array to matrices.

Instead of updating every cell inside a rectangle:

```text
(r1,c1) → (r2,c2)
```

we update only the rectangle boundaries.

Then apply 2D Prefix Sum to reconstruct the final matrix.

---

## When to Use

* Multiple rectangle updates.
* Grid range increment.
* Matrix coverage problems.
* Image processing.
* Heatmap generation.
* Large number of rectangle queries.

---

## Trigger Words

* Rectangle update
* Matrix range update
* Grid increment
* Submatrix update
* Multiple updates
* Coverage matrix

---

## General Pattern

```text
Rectangle Update
        ↓
2D Difference Array
        ↓
Mark 4 Corners
        ↓
2D Prefix Sum
        ↓
Final Matrix
```

---

## Rectangle Update Formula

For update:

```text
(r1,c1) → (r2,c2)
+= val
```

Apply:

```java
diff[r1][c1] += val;

diff[r1][c2+1] -= val;

diff[r2+1][c1] -= val;

diff[r2+1][c2+1] += val;
```

---

## Visual Understanding

### Update

```text
+5

┌─────────┐
│         │
│         │
└─────────┘
```

Only 4 corners are modified.

```text
+5      -5


-5      +5
```

---

## General Template

```java
for(int[] q : queries){

    int r1 = q[0];
    int c1 = q[1];
    int r2 = q[2];
    int c2 = q[3];
    int val = q[4];

    diff[r1][c1] += val;

    diff[r1][c2 + 1] -= val;

    diff[r2 + 1][c1] -= val;

    diff[r2 + 1][c2 + 1] += val;
}
```

---

## Building Final Matrix

### Row Prefix

```java
for(int i=0;i<rows;i++){

    for(int j=1;j<cols;j++){

        diff[i][j] += diff[i][j-1];
    }
}
```

---

### Column Prefix

```java
for(int j=0;j<cols;j++){

    for(int i=1;i<rows;i++){

        diff[i][j] += diff[i-1][j];
    }
}
```

---

## Time Complexity

```text
Updates      : O(Q)

Build Matrix : O(R*C)

Total        : O(Q + R*C)
```

## Space Complexity

```text
O(R*C)
```

---

## Important Insights

### Insight 1

1D Difference Array

```text
l      r

+v   -v
```

---

### Insight 2

2D Difference Array

```text
+v      -v

-v      +v
```

---

### Insight 3

After all updates:

```text
Horizontal Prefix
         +
Vertical Prefix
```

reconstructs the final matrix.

---

### Insight 4

Without Difference Array

```text
Q Rectangle Updates

O(Q * R * C)
```

With Difference Array

```text
O(Q + R*C)
```

Huge optimization.

---

## Recognition Pattern

```text
Many Rectangle Updates
          ↓
Updating Each Cell Expensive
          ↓
Mark Corners Only
          ↓
2D Difference Array
```

---

# Problem 1: Range Add Queries (LeetCode 2536)

## Problem Statement

Given n × n matrix.

Each query:

```text
[r1,c1,r2,c2]
```

Increment every cell inside rectangle by 1.

Return final matrix.

---

## Approach

1. Create 2D Difference Array.
2. Mark four corners.
3. Apply 2D Prefix Sum.
4. Return matrix.

---

## Solution

```java
class Solution {

    public int[][] rangeAddQueries(
            int n,
            int[][] queries) {

        int[][] diff =
                new int[n + 1][n + 1];

        for(int[] q : queries){

            int r1 = q[0];
            int c1 = q[1];
            int r2 = q[2];
            int c2 = q[3];

            diff[r1][c1]++;

            diff[r1][c2 + 1]--;

            diff[r2 + 1][c1]--;

            diff[r2 + 1][c2 + 1]++;
        }

        for(int i=0;i<n;i++){

            for(int j=1;j<n;j++){

                diff[i][j] += diff[i][j-1];
            }
        }

        for(int j=0;j<n;j++){

            for(int i=1;i<n;i++){

                diff[i][j] += diff[i-1][j];
            }
        }

        int[][] ans = new int[n][n];

        for(int i=0;i<n;i++){

            for(int j=0;j<n;j++){

                ans[i][j] = diff[i][j];
            }
        }

        return ans;
    }
}
```

### TC

```text
O(Q + N²)
```

### SC

```text
O(N²)
```

---

# Problem 2: Matrix Coverage Problem

## Problem Statement

Given multiple rectangles.

Find how many times each cell is covered.

---

## Approach

Exactly same.

```text
Rectangle Updates
        ↓
2D Difference Array
        ↓
2D Prefix Sum
        ↓
Coverage Count
```

---

## Common Interview Problems

```text
2536 - Increment Submatrices by One

Rectangle Coverage Problems

Heatmap Generation

Image Processing Updates

Grid Simulation Problems
```

---

## 1D vs 2D Difference Array

| Feature        | 1D         | 2D            |
| -------------- | ---------- | ------------- |
| Update Area    | Range      | Rectangle     |
| Marks Needed   | 2          | 4             |
| Reconstruction | Prefix Sum | 2D Prefix Sum |
| Complexity     | O(N+Q)     | O(R*C+Q)      |

---

## Master Formula

```text
Rectangle Update

(r1,c1) → (r2,c2)

diff[r1][c1]       += val

diff[r1][c2+1]     -= val

diff[r2+1][c1]     -= val

diff[r2+1][c2+1]   += val

------------------------

Apply Row Prefix

------------------------

Apply Column Prefix

------------------------

Final Matrix Ready
```
