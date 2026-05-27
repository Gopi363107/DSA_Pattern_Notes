# Kadane’s Algorithm Pattern — Maximum Product Subarray Notes

---

# Definition

The **Maximum Product Subarray** problem asks for:

```text
Largest product of
a contiguous subarray
```

Unlike normal Kadane:

```text
Products behave differently
because of negatives
```

---

# Core Intuition

For sums:

```text
Negative values are bad
```

But for products:

```text
Negative × Negative
=
Positive
```

So:

```text
Minimum product can suddenly
become maximum product
```

This changes EVERYTHING.

---

# MOST IMPORTANT INSIGHT

At every index:

We must track BOTH:

```text
1. Maximum product ending here
2. Minimum product ending here
```

because either one may become answer later.

---

# Why Minimum Product Matters

Suppose:

```text
Current number = negative
```

Then:

```text
(minimum negative)
×
(negative number)
=
large positive
```

Example:

```text
[-2, 3, -4]
```

At `-4`:

```text
(-6) × (-4) = 24
```

Huge positive answer.

---

# When Should I Think About This Pattern?

Use this pattern when:

- maximum product
- contiguous multiplication
- sign flipping
- positive/negative switching
- multiplicative DP

---

# Recognition Triggers

If problem contains:

- "maximum product"
- "contiguous product"
- "subarray product"
- "negative flipping"
- "largest multiplication"

→ Think:

```text
Dual Kadane
(max + min tracking)
```

---

# MOST IMPORTANT MENTAL MODEL

At every index:

```text
Current element can:

1. Start new subarray
2. Extend previous maximum
3. Extend previous minimum
```

ONLY these possibilities exist.

---

# Generic Template

```java
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
```

---

# Pattern 1 — Maximum Product Subarray

---

## Trigger

- contiguous product
- negative sign changes
- maximum multiplication

---

## Problem

LeetCode 152 — Maximum Product Subarray

---

# Key Insight

Because negatives can flip signs:

```text
Track both extremes
```

This is the ENTIRE trick.

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
                Math.max(
                    nums[i],
                    Math.max(
                        maxProd * nums[i],
                        minProd * nums[i]
                    )
                );

            minProd =
                Math.min(
                    nums[i],
                    Math.min(
                        temp * nums[i],
                        minProd * nums[i]
                    )
                );

            ans =
                Math.max(ans,
                         maxProd);
        }

        return ans;
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

Normal Kadane tracks:

```text
Only maximum contribution
```

Product Kadane tracks:

```text
Both extremes
```

because:

```text
Negative values reverse behavior
```

This is the key theoretical difference.

---

# Deep Mathematical Insight

For sums:

```text
Order relation preserved
```

Example:

```text
larger + x
stays larger
```

But for multiplication:

```text
Order can flip
```

because:

```text
negative × negative
=
positive
```

So greedy removal alone fails.

---

# Visual Example

Suppose:

```text
[-2, 3, -4]
```

Step-by-step:

---

## At -2

```text
max = -2
min = -2
```

---

## At 3

```text
max = 3
min = -6
```

---

## At -4

```text
max =
(-6) × (-4)
=
24
```

Huge jump caused by:

```text
minimum negative product
```

This is THE CORE insight.

---

# Advanced Competitive Programming Insights

---

# 1. Sign Flipping Problems Need Dual Tracking

Whenever:

```text
Negative values can invert behavior
```

track:

```text
maximum
+
minimum
```

Very important DP trick.

---

# 2. Multiplication Breaks Greedy Logic

In normal Kadane:

```text
Negative prefixes discarded
```

Not true here.

Bad-looking negative product may later become best answer.

---

# 3. State Compression DP

We only need:

```text
Previous max
Previous min
```

So DP compresses to:

```text
O(1) space
```

Very important optimization insight.

---

# 4. Local Extremes Build Global Answer

At each index:

```text
Best/worst product ending HERE
```

Eventually forms:

```text
Global maximum
```

Classic DP transition idea.

---

# Common Mistake

Students often track only:

```text
Maximum product
```

Fails because:

```text
Minimum negative product
may become future maximum
```

This is THE MOST COMMON mistake.

---

# Super Important Recognition Patterns

| Situation | Pattern |
|---|---|
| Maximum contiguous product | Dual Kadane |
| Sign-flipping contribution | Max + Min tracking |
| Negative inversion problems | Extreme tracking |
| Multiplicative DP | Product Kadane |

---

# One-Line Memory Trick

```text
For products,
minimum can become maximum.
```

---

# Final Interview Insight

Maximum Product Subarray is powerful because it teaches:

```text
Negative values can reverse optimization behavior
```

So instead of tracking only:

```text
Best state
```

we track:

```text
Both extremes
```

This is one of the MOST IMPORTANT DP/Kadane variations asked in interviews and competitive programming.