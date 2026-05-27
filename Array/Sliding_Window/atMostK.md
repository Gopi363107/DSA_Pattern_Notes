# At Most K Sliding Window Pattern — Recognition Notes

---

# Definition

The **At Most K** pattern is one of the MOST IMPORTANT sliding window techniques.

It is used when the problem asks for:

```text
Subarrays/substrings containing
AT MOST K constraints
```

Examples:

- at most k distinct characters
- at most k odd numbers
- at most k zeros
- at most k replacements
- at most k operations

---

# Core Intuition

We maintain a window such that:

```text
Window always remains VALID
```

where validity means:

```text
Constraint count <= K
```

If window becomes invalid:

```text
Shrink from left
```

until valid again.

---

# Most Important Observation

AtMostK problems are PERFECT for sliding window because:

```text
If a window is valid,
ALL smaller windows inside it are also valid
```

This is the ENTIRE mathematical foundation.

---

# Most Important Formula

```text
Exactly(K)
=
AtMost(K)
-
AtMost(K - 1)
```

This is one of the MOST IMPORTANT competitive programming tricks.

---

# Why This Formula Works

Suppose:

```text
AtMost(2)
=
All windows having:
0,1,2 distinct elements
```

Suppose:

```text
AtMost(1)
=
All windows having:
0,1 distinct elements
```

Subtracting:

```text
AtMost(2) - AtMost(1)
```

leaves only:

```text
Exactly 2 distinct
```

GENIUS observation.

---

# When Should I Think About AtMostK Pattern?

Use this pattern when:

- Need counting of subarrays/substrings
- Constraint says "at most k"
- Need "exactly k"
- Need distinct-element counting
- Need frequency-limited windows
- Need counting-based sliding window

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "at most k"
- "exactly k"
- "k distinct"
- "k odd numbers"
- "k replacements"
- "count subarrays"
- "count substrings"
- "number of valid windows"
- "frequency constraint"

→ Think **AtMostK Sliding Window**

---

# Mental Model

Ask this question:

> “If a window is valid, are all smaller windows also valid?”

If YES:

```text
Use AtMostK Sliding Window
```

---

# Generic AtMostK Template

```java
int left = 0;

for(int right = 0; right < n; right++) {

    // include current element

    while(window invalid) {

        // remove left contribution

        left++;
    }

    ans += right - left + 1;
}
```

---

# MOST IMPORTANT COUNTING INSIGHT

After making window valid:

```text
Number of valid subarrays ending at right
=
window size
=
right - left + 1
```

WHY?

Because ALL subarrays ending at `right` are valid:

```text
[left...right]
[left+1...right]
[left+2...right]
...
[right...right]
```

This is THE MOST IMPORTANT insight in counting problems.

---

# Pattern 1 — Subarrays with K Different Integers

---

## Trigger

- exactly k distinct
- distinct elements
- counting subarrays

---

## Problem

LeetCode 992 — Subarrays with K Different Integers

---

## Recognition

Directly solving:

```text
Exactly K distinct
```

is difficult.

Use powerful trick:

```text
Exactly(K)
=
AtMost(K)
-
AtMost(K-1)
```

Classic advanced sliding window pattern.

---

# Key Insight

Count:

```text
Subarrays with ≤ K distinct
```

Then subtract:

```text
Subarrays with ≤ (K-1) distinct
```

Remaining:

```text
Exactly K distinct
```

---

## Solution

```java
class Solution {

    public int subarraysWithKDistinct(
        int[] nums,
        int k
    ) {

        return atMost(nums, k)
             - atMost(nums, k - 1);
    }

    int atMost(int[] nums, int k) {

        HashMap<Integer, Integer> map =
            new HashMap<>();

        int left = 0;

        int count = 0;

        for(int right = 0;
            right < nums.length;
            right++) {

            map.put(nums[right],
                    map.getOrDefault(
                        nums[right], 0) + 1);

            while(map.size() > k) {

                map.put(nums[left],
                        map.get(nums[left]) - 1);

                if(map.get(nums[left]) == 0) {

                    map.remove(nums[left]);
                }

                left++;
            }

            count += right - left + 1;
        }

        return count;
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

Why?

Each element:

- enters window once
- leaves window once

HashMap operations are average O(1).

---

## Space Complexity

```text
O(k)
```

HashMap stores at most `k` distinct elements.

---

# CP-Level Insight

The REAL trick is NOT sliding window.

The REAL trick is recognizing:

```text
Exactly K
=
AtMost(K)
-
AtMost(K-1)
```

This appears in MANY hard contest problems.

---

# Pattern 2 — Max Consecutive Ones III

---

## Trigger

- at most k replacements
- flip zeros
- longest valid window

---

## Problem

LeetCode 1004 — Max Consecutive Ones III

---

## Recognition

Need longest subarray with:

```text
At most k zeros
```

Window invalid when:

```text
zero count > k
```

Classic AtMostK validity window.

---

## Solution

```java
class Solution {

    public int longestOnes(
        int[] nums,
        int k
    ) {

        int left = 0;

        int zeros = 0;

        int ans = 0;

        for(int right = 0;
            right < nums.length;
            right++) {

            if(nums[right] == 0) {
                zeros++;
            }

            while(zeros > k) {

                if(nums[left] == 0) {
                    zeros--;
                }

                left++;
            }

            ans =
                Math.max(ans,
                         right - left + 1);
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

Two pointers move forward only.

---

## Space Complexity

```text
O(1)
```

Only counters used.

---

# CP-Level Insight

Many:

```text
At most K modifications
```

problems reduce to:

```text
Maintain invalid count
```

instead of tracking the actual modifications.

Very important simplification trick.

---

# Pattern 3 — Fruit Into Baskets

---

## Trigger

- at most 2 distinct
- longest subarray
- type constraints

---

## Problem

LeetCode 904 — Fruit Into Baskets

---

## Recognition

Need longest subarray with:

```text
At most 2 distinct elements
```

Classic hashmap sliding window.

---

## Solution

```java
class Solution {

    public int totalFruit(int[] fruits) {

        HashMap<Integer, Integer> map =
            new HashMap<>();

        int left = 0;

        int ans = 0;

        for(int right = 0;
            right < fruits.length;
            right++) {

            map.put(
                fruits[right],
                map.getOrDefault(
                    fruits[right], 0
                ) + 1
            );

            while(map.size() > 2) {

                map.put(
                    fruits[left],
                    map.get(fruits[left]) - 1
                );

                if(map.get(fruits[left]) == 0) {

                    map.remove(fruits[left]);
                }

                left++;
            }

            ans =
                Math.max(ans,
                         right - left + 1);
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

Every element processed at most twice.

---

## Space Complexity

```text
O(k)
```

Map stores at most 2 distinct elements.

---

# Super Important Recognition Patterns

---

# 1. Counting Window Pattern

If problem asks:

```text
Count subarrays/substrings
```

→ Usually:

```text
count += window size
```

Very important.

---

# 2. Exactly K Trick

If problem asks:

```text
Exactly K
```

→ Usually think:

```text
AtMost(K)
-
AtMost(K-1)
```

HIGH-FREQUENCY interview trick.

---

# 3. Distinct Element Pattern

If validity depends on:

```text
Unique/distinct counts
```

→ Use:

```text
HashMap frequencies
```

---

# 4. Modification Budget Pattern

If problem allows:

```text
At most K changes/flips/replacements
```

→ Track invalid elements count.

---

# Advanced Competitive Programming Insights

---

# 1. Why `count += window size` Works

Suppose valid window:

```text
[left .... right]
```

Then ALL smaller suffix windows ending at `right` are valid.

Count added:

```text
right - left + 1
```

This is the CORE math insight.

---

# 2. Monotonic Validity

Sliding window works because:

```text
If current window invalid,
larger windows also invalid
```

This creates monotonic behavior.

Very important theoretical insight.

---

# 3. HashMap Frequency Optimization

Instead of storing full windows:

```text
Store frequencies only
```

This reduces:

```text
Validation to O(1)
```

---

# 4. Two-Pointer Amortized Complexity

Even though nested loops exist:

```text
Total operations ≤ 2n
```

because pointers never move backward.

CRITICAL CP insight.

---

# Important Interview Insight

Most hard sliding window counting problems become easy after identifying:

```text
Can valid windows be counted incrementally?
```

If YES:

```text
Sliding window becomes possible
```

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Exact size k | Fixed Window |
| Longest valid window | Variable Window |
| Exactly k constraints | AtMost(K)-AtMost(K-1) |
| Counting valid windows | AtMostK |

---

# Common Mistake

Students often try:

```text
Generate all subarrays
```

which leads to:

```text
O(n²)
```

Instead:

```text
Count windows mathematically
```

using sliding window.

---

# One-Line Memory Trick

```text
Exactly(K)
=
AtMost(K)
-
AtMost(K-1)
```

---

# Final Interview Insight

Most advanced sliding window problems become easy after recognizing:

```text
Valid windows form continuous ranges
```

That single observation enables:

```text
Two pointers
Incremental counting
O(n) optimization
```

This is one of the MOST IMPORTANT competitive programming and interview patterns asked at Meta, Google, Amazon, Uber, ICPC, and Codeforces.