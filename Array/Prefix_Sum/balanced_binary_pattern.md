# Prefix Sum Pattern — Balanced Binary Pattern Notes

---

# Definition

The **Balanced Binary Pattern** transforms binary arrays into:

```text
Prefix Sum problems
```

by converting values mathematically.

Usually:

```text
0 → -1
1 → +1
```

Then balanced subarrays become:

```text
Subarray sum = 0
```

---

# Core Intuition

A binary subarray is balanced when:

```text
Number of 0s == Number of 1s
```

After transformation:

```text
0 → -1
1 → +1
```

equal counts cancel out.

So:

```text
Balanced subarray
⇔
Subarray sum = 0
```

GENIUS transformation.

---

# MOST IMPORTANT TRANSFORMATION

Convert:

```text
0 → -1
1 → +1
```

Why?

Because:

```text
Equal number of +1 and -1
gives sum 0
```

This converts:

```text
Counting problem
```

into:

```text
Prefix Sum problem
```

---

# Why This Works

Suppose subarray contains:

```text
3 ones
3 zeros
```

After conversion:

```text
(+1 +1 +1)
+
(-1 -1 -1)
=
0
```

So balanced condition becomes:

```text
Subarray sum = 0
```

---

# When Should I Think About This Pattern?

Use this pattern when:

- equal 0s and 1s
- balanced binary array
- equal frequency
- same count problems
- binary subarray balancing

---

# Recognition Triggers

If problem contains:

- "equal number of 0 and 1"
- "balanced binary"
- "same frequency"
- "equal count"
- binary arrays

→ Think:

```text
0 → -1 transformation
+
Prefix Sum
```

---

# Generic Template

```java
HashMap<Integer, Integer> map =
    new HashMap<>();

map.put(0, -1);

int prefixSum = 0;

for(int i = 0; i < nums.length; i++) {

    if(nums[i] == 0) {
        prefixSum += -1;
    }
    else {
        prefixSum += 1;
    }

    if(map.containsKey(prefixSum)) {

        // balanced subarray found
    }
    else {

        map.put(prefixSum, i);
    }
}
```

---

# MOST IMPORTANT INSIGHT

We are NOT solving:

```text
Binary counting directly
```

Instead we convert it into:

```text
Zero-sum subarray problem
```

This is a VERY famous CP trick.

---

# Pattern 1 — Contiguous Array

---

## Trigger

- equal 0s and 1s
- longest balanced subarray
- binary array

---

## Problem

LeetCode 525 — Contiguous Array

---

# Key Insight

If same prefix sum appears again:

```text
Subarray between them
has sum 0
```

Meaning:

```text
Equal number of 0s and 1s
```

Store FIRST occurrence.

---

## Solution

```java
class Solution {

    public int findMaxLength(
        int[] nums
    ) {

        HashMap<Integer, Integer> map =
            new HashMap<>();

        map.put(0, -1);

        int prefixSum = 0;
        int maxLen = 0;

        for(int i = 0; i < nums.length; i++) {

            if(nums[i] == 0) {
                prefixSum += -1;
            }
            else {
                prefixSum += 1;
            }

            if(map.containsKey(prefixSum)) {

                maxLen = Math.max(
                    maxLen,
                    i - map.get(prefixSum)
                );
            }
            else {

                map.put(prefixSum, i);
            }
        }

        return maxLen;
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
O(n)
```

---

# CP-Level Insight

Without transformation:

```text
Equal frequency tracking
looks difficult
```

Transformation simplifies it into:

```text
Zero-sum detection
```

Beautiful reduction trick.

---

# Dry Run

```text
nums = [0,1,0]
```

After transformation:

```text
[-1,+1,-1]
```

---

## Step 1

```text
prefixSum = -1
```

Store:

```text
-1 → index 0
```

---

## Step 2

```text
prefixSum = 0
```

Already exists at:

```text
index -1
```

Length:

```text
2
```

Subarray:

```text
[0,1]
```

Balanced.

---

## Step 3

```text
prefixSum = -1
```

Seen before at:

```text
index 0
```

Length:

```text
2
```

Subarray:

```text
[1,0]
```

Balanced.

---

# Final Answer

```text
2
```

---

# Pattern 2 — Equal Number of 0s and 1s Count

---

## Trigger

- count balanced subarrays
- equal frequency
- binary counting

---

# Key Insight

If same prefix sum appears multiple times:

```text
Every previous occurrence
forms a balanced subarray
```

Store frequencies.

---

## Solution

```java
class Solution {

    public int countBalanced(
        int[] nums
    ) {

        HashMap<Integer, Integer> map =
            new HashMap<>();

        map.put(0, 1);

        int prefixSum = 0;
        int count = 0;

        for(int num : nums) {

            if(num == 0) {
                prefixSum += -1;
            }
            else {
                prefixSum += 1;
            }

            if(map.containsKey(prefixSum)) {

                count += map.get(prefixSum);
            }

            map.put(
                prefixSum,
                map.getOrDefault(
                    prefixSum,
                    0
                ) + 1
            );
        }

        return count;
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
O(n)
```

---

# SUPER IMPORTANT INSIGHT

Repeated prefix sums mean:

```text
Difference between them = 0
```

Zero difference means:

```text
Balanced binary subarray
```

---

# Advanced Competitive Programming Insights

---

# 1. Transformation Is The REAL Trick

Hard problems often become easy after:

```text
Value transformation
```

This is one of the MOST IMPORTANT CP skills.

---

# 2. Equal Frequency Problems

Many equal-frequency problems reduce to:

```text
Zero-sum subarrays
```

after appropriate conversion.

---

# 3. Prefix Sum Detects Balance

If prefix sum repeats:

```text
Net contribution between them = 0
```

This automatically detects balance.

---

# 4. Earliest Index Gives Maximum Length

For longest subarray:

```text
Store FIRST occurrence
```

because earliest index maximizes distance.

VERY important interview insight.

---

# Common Mistake

Students forget:

```text
map.put(0, -1)
```

Why needed?

Because balanced subarrays starting from:

```text
index 0
```

must also count.

---

# One-Line Memory Trick

```text
Convert balance problems
into zero-sum problems.
```

---

# Final Interview Insight

The REAL power of balanced binary pattern is:

```text
Mathematical transformation
```

Instead of directly handling:

```text
Equal counts
```

we cleverly convert the problem into:

```text
Repeated prefix sums
```

This transforms many:

```text
O(n²)
```

solutions into:

```text
O(n)
```