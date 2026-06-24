# Difference Array + Greedy

## Core Idea

Difference Array efficiently tracks the effect of range operations.

Greedy decides:

```text id="a1g2h3"
When to Apply
How Much to Apply
```

Together they solve problems where:

```text id="b2h3i4"
Range Updates
       +
Local Optimal Decisions
```

are required.

---

## When to Use

* Range operations.
* Window updates.
* Minimize operations.
* Transform array.
* Greedy interval decisions.
* Large constraints.

---

## Trigger Words

* Minimum operations
* Range increment
* Range decrement
* Window size k
* Make array equal
* Convert array
* Greedy updates

---

## General Pattern

```text id="c3i4j5"
Process Left To Right
         ↓
Greedy Decision
         ↓
Apply Range Effect
         ↓
Difference Array
         ↓
Continue
```

---

## Why Difference Array?

Without Difference Array:

```text id="d4j5k6"
Apply Operation

O(k)
```

for every step.

---

With Difference Array:

```text id="e5k6l7"
Apply Operation

O(1)
```

---

## Generic Template

```java id="f6l7m8"
int currentEffect = 0;

for(int i = 0; i < n; i++){

    currentEffect += diff[i];

    int currentValue =
        nums[i] + currentEffect;

    if(currentValue < target){

        int need =
            target - currentValue;

        operations += need;

        currentEffect += need;

        diff[i + k] -= need;
    }
}
```

---

## Time Complexity

```text id="g7m8n9"
O(N)
```

## Space Complexity

```text id="h8n9o0"
O(N)
```

---

## Important Insights

### Insight 1

Greedy decides at the earliest position.

```text id="i9o0p1"
Fix Current Index
Before Moving Forward
```

---

### Insight 2

Difference Array delays removal of effect.

```java id="j0p1q2"
diff[i + k] -= effect;
```

---

### Insight 3

Running value:

```java id="k1q2r3"
currentEffect += diff[i];
```

represents all active operations.

---

### Insight 4

Most problems become:

```text id="l2r3s4"
Left To Right Scan
         +
Range Effect Tracking
```

---

## Recognition Pattern

```text id="m3s4t5"
Need Minimum Operations
           ↓
Range Update Involved
           ↓
Process Left To Right
           ↓
Difference Array + Greedy
```

---

# Problem 1: LeetCode 995 - Minimum Number of K Consecutive Bit Flips

## Problem Statement

Given binary array.

Flip any subarray of size k.

Find minimum flips to make all elements 1.

---

## Approach

Process from left to right.

If current bit becomes:

```text id="n4t5u6"
0
```

must flip here greedily.

Use Difference Array to track active flips.

---

## Solution

```java id="o5u6v7"
class Solution {

    public int minKBitFlips(
            int[] nums,
            int k) {

        int n = nums.length;

        int[] diff = new int[n + 1];

        int flips = 0;
        int active = 0;

        for(int i = 0; i < n; i++){

            active += diff[i];

            int bit =
                (nums[i] + active) % 2;

            if(bit == 0){

                if(i + k > n)
                    return -1;

                flips++;

                active++;

                diff[i + k]--;
            }
        }

        return flips;
    }
}
```

### TC

```text id="p6v7w8"
O(N)
```

### SC

```text id="q7w8x9"
O(N)
```

---

# Problem 2: LeetCode 2772 - Apply Operations to Make All Array Elements Equal to Zero

## Problem Statement

Each operation subtracts 1 from a subarray of size k.

Determine if entire array can become zero.

---

## Approach

At index i:

```text id="r8x9y0"
Need nums[i]
operations
```

Greedily apply them.

Difference Array tracks active decrements.

---

## Solution

```java id="s9y0z1"
class Solution {

    public boolean checkArray(
            int[] nums,
            int k) {

        int n = nums.length;

        int[] diff = new int[n + 1];

        int active = 0;

        for(int i = 0; i < n; i++){

            active += diff[i];

            nums[i] += active;

            if(nums[i] < 0)
                return false;

            if(nums[i] > 0){

                if(i + k > n)
                    return false;

                int need = nums[i];

                active -= need;

                diff[i + k] += need;
            }
        }

        return true;
    }
}
```

### TC

```text id="t0z1a2"
O(N)
```

### SC

```text id="u1a2b3"
O(N)
```

---

# Problem 3: Range Increment Transformation

## Problem Statement

Convert an array into target array using minimum range increments.

---

## Approach

Greedy:

```text id="v2b3c4"
Fix Leftmost Incorrect Position
```

Apply update.

Track effect using Difference Array.

---

## Solution Pattern

```java id="w3c4d5"
current += diff[i];

actual =
nums[i] + current;

if(actual < target[i]){

    need =
    target[i] - actual;

    current += need;

    diff[i + k] -= need;
}
```

---

## Common Interview Problems

```text id="x4d5e6"
995  - Minimum Number of K Consecutive Bit Flips

2772 - Apply Operations to Make All Array Elements Equal to Zero

Range Increment Transformation Problems

Window Operation Problems
```

---

## Difference Array vs Difference Array + Greedy

| Technique               | Purpose            |
| ----------------------- | ------------------ |
| Difference Array        | Fast Range Update  |
| Difference + Prefix     | Reconstruction     |
| Difference + Sweep Line | Interval Events    |
| Difference + Greedy     | Minimum Operations |

---

## Visual Understanding

```text id="y5e6f7"
Array

0 0 0 1 1

k = 3

Index 0

Need Flip

Apply

[0,2]

----------------

Difference Array

Track Flip Effect

----------------

Move Forward

Greedily Fix First Bad Position
```

---

## Master Formula

```text id="z6f7g8"
1. Scan Left To Right

2. Maintain Active Effect

3. Fix Current Position Greedily

4. Apply Range Update

5. Store Removal Using Difference Array

6. Continue

7. Answer Obtained
```
