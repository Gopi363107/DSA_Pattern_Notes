# Circular Difference Array

## Core Idea

Circular Difference Array is used when range updates happen on a circular array.

Normal Difference Array handles:

```text
[l, r]
where l <= r
```

Circular Difference Array handles:

```text
[l, r]
where l > r
```

which means the range wraps around the end of the array.

---

## When to Use

* Circular arrays.
* Ring buffers.
* Cyclic updates.
* Rotation problems.
* Wrap-around intervals.
* Circular scheduling.

---

## Trigger Words

* Circular array
* Wrap around
* Rotation
* Ring
* Clockwise
* Cyclic
* Modular indexing

---

## General Pattern

```text
Circular Range
      ↓
Does Range Wrap?
      ↓
YES
      ↓
Split Into Two Ranges
      ↓
Apply Difference Array
      ↓
Prefix Sum
```

---

## Important Insight

### Case 1

Normal Range

```text
l <= r
```

Example:

```text
[2,5]
```

Apply normal Difference Array.

```java
diff[l] += val;

diff[r + 1] -= val;
```

---

### Case 2

Circular Range

```text
l > r
```

Example:

```text
[6,2]
```

Affected Elements:

```text
6 7 0 1 2
```

Split Into:

```text
[6,7]

[0,2]
```

Apply Difference Array on both ranges.

---

## Visual Understanding

```text
Index

0 1 2 3 4 5 6 7

Update

[6,2]

Affected

6 7 0 1 2
```

Split:

```text
[6,7]

[0,2]
```

---

## General Template (Java)

```java
public void update(
        int[] diff,
        int n,
        int l,
        int r,
        int val){

    if(l <= r){

        diff[l] += val;

        if(r + 1 < n)
            diff[r + 1] -= val;
    }
    else{

        // Range [l,n-1]

        diff[l] += val;

        // Range [0,r]

        diff[0] += val;

        if(r + 1 < n)
            diff[r + 1] -= val;
    }
}
```

---

## Building Final Array

```java
for(int i = 1; i < n; i++){

    diff[i] += diff[i - 1];
}
```

---

## Time Complexity

```text
Single Update : O(1)

Q Updates      : O(Q)

Build Array    : O(N)

Total          : O(N + Q)
```

---

## Space Complexity

```text
O(N)
```

---

## Recognition Pattern

```text
Circular Array
      ↓
Range Update
      ↓
Range Wraps Around
      ↓
Split Into Two Ranges
      ↓
Difference Array
```

---

# Problem 1: LeetCode 798 - Smallest Rotation with Highest Score

## Problem Statement

Find rotation having maximum score.

---

## Core Observation

Each element contributes positively over a circular range of rotations.

Instead of checking every rotation:

```text
O(N²)
```

Use Circular Difference Array.

---

## Approach

For every element:

1. Find valid rotation interval.
2. Add contribution using Circular Difference Array.
3. Compute prefix sum.
4. Find maximum score.

---

## Solution

```java
class Solution {

    public int bestRotation(int[] nums) {

        int n = nums.length;

        int[] diff = new int[n + 1];

        for(int i = 0; i < n; i++){

            int start = (i + 1) % n;

            int end =
                (i - nums[i] + n + 1) % n;

            diff[start]++;

            diff[end]--;

            if(start >= end)
                diff[0]++;
        }

        int score = 0;

        int maxScore = -1;

        int answer = 0;

        for(int k = 0; k < n; k++){

            score += diff[k];

            if(score > maxScore){

                maxScore = score;

                answer = k;
            }
        }

        return answer;
    }
}
```

### TC

```text
O(N)
```

### SC

```text
O(N)
```

---

# Problem 2: Circular Range Increment Queries

## Problem Statement

Perform multiple updates:

```text
[l,r] += val
```

where:

```text
l > r
```

means wrap-around.

---

## Approach

### Normal Range

```text
l <= r
```

Apply standard Difference Array.

---

### Circular Range

```text
l > r
```

Split into:

```text
[l,n-1]

[0,r]
```

Apply updates separately.

---

## Solution

```java
public int[] circularRangeUpdate(
        int n,
        int[][] queries){

    int[] diff = new int[n];

    for(int[] q : queries){

        int l = q[0];
        int r = q[1];
        int val = q[2];

        if(l <= r){

            diff[l] += val;

            if(r + 1 < n)
                diff[r + 1] -= val;
        }
        else{

            diff[l] += val;

            diff[0] += val;

            if(r + 1 < n)
                diff[r + 1] -= val;
        }
    }

    for(int i = 1; i < n; i++){

        diff[i] += diff[i - 1];
    }

    return diff;
}
```

### TC

```text
O(N + Q)
```

### SC

```text
O(N)
```

---

## Common Interview Problems

```text
798 - Smallest Rotation with Highest Score

Circular Range Updates

Ring Buffer Problems

Clock Rotation Problems

Circular Scheduling Problems
```

---

## Normal vs Circular Difference Array

| Feature     | Normal  | Circular     |
| ----------- | ------- | ------------ |
| Range       | Linear  | Cyclic       |
| Wrap Around | No      | Yes          |
| Updates     | 2 Marks | 2 or 4 Marks |
| Logic       | Simple  | Split Range  |

---

## Master Formula

```text
If l <= r

    Normal Difference Array

Else

    Split Into

    [l,n-1]

    [0,r]

Apply Updates

Build Prefix Sum

Return Answer
```

---

## Difference Array Roadmap

```text
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
Coordinate Compression + Difference Array
        ↓
Advanced Interval Problems
```
