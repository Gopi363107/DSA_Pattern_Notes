# Matrix Binary Search

## Core Idea

Apply Binary Search on a matrix by exploiting its sorted properties.

Two common patterns:

```text
Type 1:
Each Row Sorted
First Element of Row > Last Element of Previous Row
```

```text
Type 2:
Rows Sorted
Columns Sorted
```

---

## When to Use

* Sorted Matrix
* Search Target
* Need O(log n)
* Matrix behaves like sorted array

---

## Trigger Words

* Sorted matrix
* Search target
* Matrix search
* Row sorted
* Column sorted
* O(log(m*n))

---

## Pattern 1: Matrix as Flattened Sorted Array

```text
1  3  5  7
10 11 16 20
23 30 34 60
```

Can be viewed as:

```text
1 3 5 7 10 11 16 20 23 30 34 60
```

Apply normal Binary Search.

---

## General Template (Type 1)

```java
public boolean searchMatrix(int[][] matrix, int target) {

    int m = matrix.length;
    int n = matrix[0].length;

    int low = 0;
    int high = m * n - 1;

    while (low <= high) {

        int mid = low + (high - low) / 2;

        int row = mid / n;
        int col = mid % n;

        if (matrix[row][col] == target)
            return true;

        if (matrix[row][col] < target)
            low = mid + 1;
        else
            high = mid - 1;
    }

    return false;
}
```

---

## Time Complexity

```text
O(log(m*n))
```

## Space Complexity

```text
O(1)
```

---

## Important Insights

### Insight 1

Convert 1D index to 2D index.

```java
row = mid / cols;
col = mid % cols;
```

---

### Insight 2

No need to flatten matrix physically.

Virtual flattening is enough.

---

### Insight 3

Works only when:

```text
Previous Row Last Element
<
Next Row First Element
```

---

## Recognition Pattern

```text
Matrix Fully Sorted
         ↓
Behaves Like Sorted Array
         ↓
Binary Search on Index
```

---

# Problem 1: LeetCode 74 - Search a 2D Matrix

## Problem Statement

Search target in matrix.

Rows are sorted and:

```text
matrix[i][last] < matrix[i+1][0]
```

---

## Approach

1. Treat matrix as sorted array.
2. Binary Search on indices.
3. Convert index to row/column.

---

## Solution

```java
class Solution {

    public boolean searchMatrix(int[][] matrix, int target) {

        int rows = matrix.length;
        int cols = matrix[0].length;

        int low = 0;
        int high = rows * cols - 1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            int row = mid / cols;
            int col = mid % cols;

            if (matrix[row][col] == target)
                return true;

            if (matrix[row][col] < target)
                low = mid + 1;
            else
                high = mid - 1;
        }

        return false;
    }
}
```

### TC

```text
O(log(m*n))
```

### SC

```text
O(1)
```

---

# Pattern 2: Row Wise & Column Wise Sorted Matrix

```text
1   4   7   11
2   5   8   12
3   6   9   16
10 13  14  17
```

Rows sorted.

Columns sorted.

---

## Core Idea

Start from:

```text
Top Right Corner
```

or

```text
Bottom Left Corner
```

---

## Why Top Right?

```text
Current > Target → Move Left
Current < Target → Move Down
```

One row or column gets eliminated every step.

---

## General Template

```java
public boolean searchMatrix(int[][] matrix, int target) {

    int row = 0;
    int col = matrix[0].length - 1;

    while (row < matrix.length && col >= 0) {

        if (matrix[row][col] == target)
            return true;

        if (matrix[row][col] > target)
            col--;
        else
            row++;
    }

    return false;
}
```

---

## Time Complexity

```text
O(m + n)
```

## Space Complexity

```text
O(1)
```

---

# Problem 2: LeetCode 240 - Search a 2D Matrix II

## Problem Statement

Search target in matrix.

Each row sorted.

Each column sorted.

---

## Approach

1. Start at top-right.
2. Compare with target.
3. Move left or down.
4. Eliminate row/column every step.

---

## Solution

```java
class Solution {

    public boolean searchMatrix(int[][] matrix, int target) {

        int row = 0;
        int col = matrix[0].length - 1;

        while (row < matrix.length && col >= 0) {

            if (matrix[row][col] == target)
                return true;

            if (matrix[row][col] > target)
                col--;
            else
                row++;
        }

        return false;
    }
}
```

### TC

```text
O(m+n)
```

### SC

```text
O(1)
```

---

# Problem 3: LeetCode 1901 - Find a Peak Element II

## Problem Statement

Find any peak element in a 2D matrix.

---

## Approach

1. Binary Search on columns.
2. Find maximum element in current column.
3. Compare left and right neighbors.
4. Move toward larger neighbor.

---

## Solution Pattern

```java
Pick Mid Column

Find Max Element Row

Compare:
leftNeighbor
rightNeighbor

Move Toward Larger Side
```

### TC

```text
O(m log n)
```

### SC

```text
O(1)
```

---

## Common LeetCode Problems

```text
74   - Search a 2D Matrix
240  - Search a 2D Matrix II
1901 - Find a Peak Element II
```

---

## Master Formula

```text
Type 1:
Fully Sorted Matrix
        ↓
Flatten Matrix
        ↓
Binary Search

--------------------------------

Type 2:
Rows Sorted
Columns Sorted
        ↓
Start Top Right
        ↓
Move Left / Down
```
