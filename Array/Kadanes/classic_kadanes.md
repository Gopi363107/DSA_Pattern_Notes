# Kadane’s Algorithm Pattern — Classic + Variations Notes

---

# Definition

Kadane’s Algorithm is used for:

```text
Maximum/Minimum subarray problems
```

It optimizes:

```text
O(n²)
→
O(n)
```

using:

```text
Running contribution logic
```

---

# Core Intuition

At every index:

Ask:

```text
Should I extend previous subarray
OR
start fresh from current element?
```

Core recurrence:

```text
currentSum =
max(nums[i],
    currentSum + nums[i])
```

---

# MOST IMPORTANT INSIGHT

Negative contribution hurts future answers.

So:

```text
Discard bad prefix
```

This is the ENTIRE foundation.

---

# When Should I Think About Kadane’s?

Use Kadane when problem asks:

- maximum subarray
- minimum subarray
- largest contiguous sum
- best continuous segment
- maximum profit style
- circular subarray
- sign contribution optimization

---

# Recognition Triggers

If problem contains:

- "maximum subarray"
- "contiguous"
- "continuous segment"
- "largest sum"
- "maximum range"
- "best interval"
- "minimum subarray"
- "maximum product"

→ Think:

```text
Kadane’s Algorithm
```

---

# Generic Kadane Template

```java
int current = nums[0];
int best = nums[0];

for(int i = 1;
    i < nums.length;
    i++) {

    current =
        Math.max(nums[i],
                 current + nums[i]);

    best =
        Math.max(best, current);
}
```

---

# MOST IMPORTANT MENTAL MODEL

At every index:

```text
Either:
1. continue old subarray
2. start new subarray
```

Only these TWO possibilities exist.

---

# Pattern 1 — Maximum Subarray

---

## Trigger

- largest contiguous sum
- maximum subarray

---

## Problem

LeetCode 53 — Maximum Subarray

---

# Key Insight

If previous sum becomes negative:

```text
It only reduces future sums
```

So restart from current element.

---

## Solution

```java
class Solution {

    public int maxSubArray(int[] nums) {

        int current = nums[0];
        int best = nums[0];

        for(int i = 1;
            i < nums.length;
            i++) {

            current =
                Math.max(nums[i],
                         current + nums[i]);

            best =
                Math.max(best, current);
        }

        return best;
    }
}
```

---

# Complexity

## Time Complexity

```text
O(n)
```

## Space Complexity

```text
O(1)
```

---

# CP-Level Insight

Kadane works because:

```text
Negative prefixes are useless
```

Very important greedy observation.

---

# Pattern 2 — Maximum Circular Subarray

---

## Trigger

- circular array
- wrap-around subarray
- maximum cyclic sum

---

## Problem

LeetCode 918 — Maximum Sum Circular Subarray

---

# Key Insight

Two possibilities:

```text
1. Normal maximum subarray
2. Circular subarray
```

Circular subarray means:

```text
Total Sum
-
Minimum Subarray
```

GENIUS transformation.

---

## Solution

```java
class Solution {

    public int maxSubarraySumCircular(
        int[] nums
    ) {

        int total = 0;

        int maxSum = nums[0];
        int curMax = 0;

        int minSum = nums[0];
        int curMin = 0;

        for(int num : nums) {

            curMax =
                Math.max(curMax + num,
                         num);

            maxSum =
                Math.max(maxSum,
                         curMax);

            curMin =
                Math.min(curMin + num,
                         num);

            minSum =
                Math.min(minSum,
                         curMin);

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

# Complexity

## Time Complexity

```text
O(n)
```

## Space Complexity

```text
O(1)
```

---

# MOST IMPORTANT CP INSIGHT

Circular problems often become:

```text
Total
-
Unwanted middle portion
```

Very high-level observation.

---

# Pattern 3 — Maximum Product Subarray

---

## Trigger

- maximum product
- negative flipping
- sign changes

---

## Problem

LeetCode 152 — Maximum Product Subarray

---

# Key Insight

Negative × Negative:

```text
Can become maximum positive
```

So track BOTH:

```text
max product
min product
```

Very important variation.

---

## Solution

```java
class Solution {

    public int maxProduct(int[] nums) {

        int maxProd = nums[0];
        int minProd = nums[0];

        int ans = nums[0];

        for(int i = 1;
            i < nums.length;
            i++) {

            int temp = maxProd;

            maxProd =
                Math.max(nums[i],
                    Math.max(
                        maxProd * nums[i],
                        minProd * nums[i]
                    ));

            minProd =
                Math.min(nums[i],
                    Math.min(
                        temp * nums[i],
                        minProd * nums[i]
                    ));

            ans =
                Math.max(ans,
                         maxProd);
        }

        return ans;
    }
}
```

---

# Complexity

## Time Complexity

```text
O(n)
```

## Space Complexity

```text
O(1)
```

---

# MOST IMPORTANT INSIGHT

Unlike sums:

```text
Negative values can become useful later
```

So we cannot discard blindly.

This changes entire logic.

---

# Super Important Recognition Patterns

| Situation | Pattern |
|---|---|
| Maximum contiguous sum | Classic Kadane |
| Minimum contiguous sum | Reverse Kadane |
| Circular maximum sum | Kadane + total sum |
| Maximum product | Dual Kadane |
| Sign-flipping contribution | Kadane variations |

---

# Advanced Competitive Programming Insights

---

# 1. Greedy Contribution Principle

Kadane is fundamentally:

```text
Greedy contribution removal
```

Bad prefixes removed immediately.

---

# 2. Local Optimal → Global Optimal

At each index:

```text
Best subarray ending HERE
```

eventually builds:

```text
Global best
```

Classic DP optimization insight.

---

# 3. Prefix Interpretation

Kadane can also be viewed as:

```text
Current Prefix Sum
-
Minimum Prefix Seen
```

Very important advanced viewpoint.

---

# 4. Product Problems Need Dual Tracking

For multiplication:

```text
Minimum can become maximum
```

because of sign flipping.

Huge interview insight.

---

# Common Mistake

Students often:

```text
Reset sum to 0 blindly
```

Fails for:

```text
All negative arrays
```

Always initialize from:

```text
nums[0]
```

---

# One-Line Memory Trick

```text
If previous contribution hurts future answer,
discard it.
```

---

# Final Interview Insight

Kadane’s REAL power is:

```text
Contribution analysis
```

Instead of checking all subarrays:

```text
Instantly remove useless prefixes
```

This transforms:

```text
O(n²)
```

into:

```text
O(n)
```

using elegant greedy + DP thinking.