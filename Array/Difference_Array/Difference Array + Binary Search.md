# Difference Array + Binary Search.md

## Core Idea

Difference Array is used to efficiently apply range updates.

Binary Search is used to find:

```text id="a1b2c3"
Minimum Answer

OR

Maximum Answer
```

Together they solve problems where:

```text id="d4e5f6"
Range Updates
        +
Feasibility Check
        +
Optimal Answer
```

are required.

---

## When to Use

* Multiple range updates.
* Binary search on answer.
* Feasibility checking.
* Coverage problems.
* Capacity problems.
* Resource allocation.

---

## Trigger Words

* Minimum operations
* Maximum possible value
* Earliest query
* Smallest answer
* Largest answer
* Feasible or not
* Range updates

---

## General Pattern

```text id="g7h8i9"
Binary Search Answer
         ↓
Apply Updates
         ↓
Difference Array
         ↓
Check Feasibility
         ↓
Move Left / Right
```

---

## Recognition Pattern

```text id="j0k1l2"
Need Optimal Answer
          ↓
Can Validate One Answer
          ↓
Range Updates Involved
          ↓
Difference Array
          +
Binary Search
```

---

## Generic Template

```java id="m3n4o5"
int low = minAnswer;
int high = maxAnswer;
int ans = high;

while(low <= high){

    int mid = low + (high - low) / 2;

    if(isPossible(mid)){

        ans = mid;
        high = mid - 1;

    }else{

        low = mid + 1;
    }
}

return ans;
```

---

## Important Insight

### Difference Array

Provides:

```text id="p6q7r8"
Fast Range Update

O(1)
```

---

### Binary Search

Provides:

```text id="s9t0u1"
Optimal Answer

O(log AnswerSpace)
```

---

### Combined Complexity

```text id="v2w3x4"
O(N log AnswerSpace)
```

instead of

```text id="y5z6a7"
O(N × AnswerSpace)
```

---

## Time Complexity

```text id="b8c9d0"
O(Check × log AnswerSpace)
```

---

## Space Complexity

```text id="e1f2g3"
Usually O(N)
```

---

# Problem 1: LeetCode 3356 - Zero Array Transformation II

## Problem Statement

Given range decrement operations.

Find minimum queries required to make all elements zero.

---

## Core Observation

If first:

```text id="h4i5j6"
k queries
```

can make array zero,

then:

```text id="k7l8m9"
k+1
k+2
k+3
```

can also make it zero.

Monotonic property exists.

Apply Binary Search.

---

## Approach

Binary Search:

```text id="n0o1p2"
How Many Queries?
```

Check:

```text id="q3r4s5"
Can First Mid Queries
Make Array Zero?
```

Use Difference Array to apply all queries efficiently.

---

## Solution

```java id="t6u7v8"
class Solution {

    public int minZeroArray(
            int[] nums,
            int[][] queries) {

        int low = 0;
        int high = queries.length;
        int ans = -1;

        while(low <= high){

            int mid =
                low + (high - low) / 2;

            if(canMake(nums, queries, mid)){

                ans = mid;
                high = mid - 1;

            }else{

                low = mid + 1;
            }
        }

        return ans;
    }

    private boolean canMake(
            int[] nums,
            int[][] queries,
            int k){

        int n = nums.length;

        int[] diff =
            new int[n + 1];

        for(int i = 0; i < k; i++){

            int l = queries[i][0];
            int r = queries[i][1];
            int val = queries[i][2];

            diff[l] += val;

            diff[r + 1] -= val;
        }

        int available = 0;

        for(int i = 0; i < n; i++){

            available += diff[i];

            if(available < nums[i])
                return false;
        }

        return true;
    }
}
```

### TC

```text id="w9x0y1"
O(N log Q)
```

### SC

```text id="z2a3b4"
O(N)
```

---

# Problem 2: Maximum Beauty of an Array After Applying Operation

## Problem Statement

Each element can affect a range.

Find maximum achievable frequency.

---

## Approach

Convert influence ranges into intervals.

Use:

```text id="c5d6e7"
Difference Array
```

to count coverage.

Binary Search possible frequency.

---

## Core Idea

```text id="f8g9h0"
Value Coverage
      ↓
Difference Array
      ↓
Check Feasibility
      ↓
Binary Search Answer
```

---

## Solution Pattern

```java id="i1j2k3"
isPossible(mid){

    Apply Ranges

    Build Prefix

    Check Coverage

}
```

---

### TC

```text id="l4m5n6"
O(N log N)
```

---

### SC

```text id="o7p8q9"
O(N)
```

---

# Problem 3: Range Coverage Feasibility

## Problem Statement

Find minimum updates needed to cover all positions.

---

## Approach

Binary Search:

```text id="r0s1t2"
Number Of Updates
```

Difference Array:

```text id="u3v4w5"
Apply First Mid Updates
```

Check:

```text id="x6y7z8"
All Positions Covered?
```

---

## Solution Pattern

```java id="a9b0c1"
boolean isPossible(int mid){

    apply first mid updates

    build prefix sum

    verify coverage

}
```

---

## Common Interview Problems

```text id="d2e3f4"
3356 - Zero Array Transformation II

Range Coverage Problems

Minimum Queries Problems

Maximum Frequency Problems

Resource Allocation Problems
```

---

## Difference Array vs Difference Array + Binary Search

| Technique                  | Purpose            |
| -------------------------- | ------------------ |
| Difference Array           | Fast Range Update  |
| Difference + Prefix        | Reconstruction     |
| Difference + Sweep Line    | Interval Events    |
| Difference + Greedy        | Minimum Operations |
| Difference + Binary Search | Optimal Answer     |

---

## Visual Understanding

```text id="g5h6i7"
Binary Search

1 2 3 4 5 6 7

        mid
         ↓

Apply First Mid Queries
         ↓

Difference Array
         ↓

Build Prefix
         ↓

Feasible ?
         ↓

Move Left / Right
```

---

## Master Formula

```text id="j8k9l0"
1. Identify Answer Space

2. Binary Search Mid

3. Apply Updates Using
   Difference Array

4. Build Prefix Sum

5. Check Feasibility

6. If Valid

      high = mid - 1

7. Else

      low = mid + 1

8. Return Answer
```

---

## Difference Array Roadmap

```text id="m1n2o3"
Basic Difference Array
        ↓
Difference Array + Prefix Sum
        ↓
2D Difference Array
        ↓
Difference Array + Sweep Line
        ↓
Difference Array + Greedy
        ↓
Circular Difference Array
        ↓
Difference Array + Binary Search
        ↓
Coordinate Compression + Difference Array
        ↓
Advanced Interval Problems
```
