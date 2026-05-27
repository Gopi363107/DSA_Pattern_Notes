# Kadane’s Algorithm Pattern — Circular Kadane Notes

---

# Definition

Circular Kadane is used for:

```text
Maximum subarray sum
in a circular array
```

Meaning:

```text
Array wraps around
```

Example:

```text
[5, -3, 5]
```

Valid circular subarray:

```text
[5] + [5]
```

because end connects to beginning.

---

# Core Intuition

Normal Kadane handles:

```text
Non-wrapping subarrays
```

Circular arrays introduce:

```text
Wrapping subarrays
```

So answer can come from:

```text
1. Normal subarray
2. Circular subarray
```

---

# MOST IMPORTANT INSIGHT

Circular maximum subarray means:

```text
Take everything
EXCEPT
the minimum subarray
```

GENIUS transformation.

---

# Mathematical Observation

Circular subarray:

```text
(total sum)
-
(minimum subarray)
```

Why?

Because removing the worst middle part leaves:

```text
Best wrapping portion
```

---

# Visual Intuition

Suppose:

```text
[5, -3, 5]
```

Total:

```text
7
```

Minimum subarray:

```text
[-3]
```

Circular answer:

```text
7 - (-3) = 10
```

which represents:

```text
[5] + [5]
```

---

# When Should I Think About Circular Kadane?

Use this pattern when:

- circular array
- cyclic subarray
- wrapping allowed
- ring buffer style problems
- maximum cyclic sum

---

# Recognition Triggers

If problem contains:

- "circular array"
- "wrap around"
- "end connected to start"
- "cyclic subarray"
- "ring structure"

→ Think:

```text
Circular Kadane
```

---

# MOST IMPORTANT FORMULA

```text
Answer
=
max(
    normalMaxSubarray,
    totalSum - minSubarray
)
```

---

# Generic Circular Kadane Template

```java
maxSubarray = KadaneMax(nums)

minSubarray = KadaneMin(nums)

answer =
max(
    maxSubarray,
    totalSum - minSubarray
)
```

---

# IMPORTANT EDGE CASE

If ALL numbers negative:

```text
totalSum - minSubarray = 0
```

which becomes invalid.

Why?

Because it means:

```text
Choosing empty subarray
```

NOT allowed.

So:

```java
if(maxSubarray < 0)
    return maxSubarray;
```

Very important interview edge case.

---

# Pattern 1 — Maximum Sum Circular Subarray

---

## Trigger

- circular array
- maximum cyclic sum
- wrapping allowed

---

## Problem

LeetCode 918 — Maximum Sum Circular Subarray

---

# Key Insight

Two cases:

```text
1. Best subarray completely inside array
2. Best subarray wraps around
```

Wrapping case becomes:

```text
Total - Minimum Subarray
```

---

## Solution

```java
class Solution {

    public int maxSubarraySumCircular(
        int[] nums
    ) {

        int total = 0;

        int curMax = 0;
        int maxSum = nums[0];

        int curMin = 0;
        int minSum = nums[0];

        for(int num : nums) {

            curMax =
                Math.max(
                    num,
                    curMax + num
                );

            maxSum =
                Math.max(
                    maxSum,
                    curMax
                );

            curMin =
                Math.min(
                    num,
                    curMin + num
                );

            minSum =
                Math.min(
                    minSum,
                    curMin
                );

            total += num;
        }

        if(maxSum < 0) {
            return maxSum;
        }

        return Math.max(
            maxSum,
            total - minSum
        );
    }
}
```

---

# Complexity Analysis

---

## Time Complexity

```text
O(n)
```

Single traversal.

---

## Space Complexity

```text
O(1)
```

Only variables used.

---

# MOST IMPORTANT CP INSIGHT

Circular problems often reduce to:

```text
Take everything
except bad middle portion
```

This transformation appears in MANY hard problems.

---

# Deep Mathematical Insight

Normal Kadane finds:

```text
Best kept region
```

Circular Kadane finds:

```text
Worst removed region
```

Both are dual problems.

Very important theoretical understanding.

---

# Why Minimum Subarray?

Suppose circular answer wraps:

```text
[end portion] + [start portion]
```

Then excluded middle section must be:

```text
Minimum possible sum
```

because removing worst part maximizes remaining sum.

This is the ENTIRE proof.

---

# Advanced Competitive Programming Insights

---

# 1. Circular Problems Often Need Complement Thinking

Instead of directly finding:

```text
Wrapping answer
```

find:

```text
What to REMOVE
```

Very important contest trick.

---

# 2. Dual Kadane Technique

Circular Kadane combines:

```text
Maximum Kadane
+
Minimum Kadane
```

Very elegant optimization pattern.

---

# 3. Why Total - Min Works

Because:

```text
Circular chosen part
+
Excluded middle part
=
Entire array
```

So:

```text
Chosen
=
Total - Excluded
```

---

# 4. Empty Subarray Trap

If all numbers negative:

```text
Minimum subarray = entire array
```

Then:

```text
total - min = 0
```

which incorrectly represents:

```text
Taking nothing
```

Huge interview trap.

---

# Common Mistake

Students often forget:

```java
if(maxSum < 0)
```

This causes wrong answers for:

```text
All negative arrays
```

Very common bug.

---

# Super Important Recognition Patterns

| Situation | Pattern |
|---|---|
| Circular maximum sum | Circular Kadane |
| Wrap-around subarray | Total - Minimum |
| Cyclic optimization | Complement thinking |
| Ring array maximum | Dual Kadane |

---

# One-Line Memory Trick

```text
Circular maximum
=
Take everything
except worst middle part
```

---

# Final Interview Insight

Circular Kadane is powerful because it transforms:

```text
Difficult wrapping logic
```

into:

```text
Simple complement math
```

using:

```text
Total Sum
-
Minimum Subarray
```

This is one of the MOST IMPORTANT greedy + Kadane transformations in competitive programming and interviews.