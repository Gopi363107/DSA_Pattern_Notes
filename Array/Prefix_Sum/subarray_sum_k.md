# Prefix Sum Pattern — Subarray Sum Equals K Notes

---

# Definition

The **Subarray Sum Equals K** pattern uses:

```text
Prefix Sum
+
HashMap
```

to count subarrays efficiently.

Instead of checking:

```text
All possible subarrays
```

we use mathematical relationships between prefix sums.

---

# Core Intuition

Suppose:

```text
Current Prefix Sum = currSum
```

We need:

```text
Subarray Sum = k
```

That means:

```text
currSum - previousPrefix = k
```

Rearranging:

```text
previousPrefix = currSum - k
```

So if:

```text
currSum - k
```

already appeared before,

then a valid subarray exists.

---

# MOST IMPORTANT FORMULA

If:

```text
prefix[j] - prefix[i] = k
```

Then:

```text
Subarray(i+1 → j) has sum k
```

This is the ENTIRE foundation.

---

# Why HashMap?

We need fast lookup for:

```text
currSum - k
```

HashMap gives:

```text
O(1)
```

average lookup time.

---

# When Should I Think About This Pattern?

Use this pattern when:

- subarray sum problems
- target sum problems
- count subarrays
- negative numbers exist
- continuous segment problems

---

# Recognition Triggers

If problem contains:

- "subarray sum"
- "equals k"
- "count subarrays"
- "continuous subarray"
- "sum target"
- negative numbers

→ Think:

```text
Prefix Sum + HashMap
```

---

# Why Sliding Window Fails Here

Sliding window works only when:

```text
All numbers positive
```

Because window movement becomes predictable.

But with:

```text
Negative numbers
```

sum can increase/decrease unpredictably.

So we use:

```text
Prefix Sum
```

instead.

---

# Generic Template

```java
HashMap<Integer, Integer> map =
    new HashMap<>();

map.put(0, 1);

int prefixSum = 0;

for(int num : nums) {

    prefixSum += num;

    if(map.containsKey(
            prefixSum - k)) {

        // valid subarray found
    }

    map.put(
        prefixSum,
        map.getOrDefault(
            prefixSum,
            0
        ) + 1
    );
}
```

---

# MOST IMPORTANT INSIGHT

At every index:

```text
We ask:
"Have I seen a prefix sum
that can form k?"
```

This converts:

```text
Subarray search
```

into:

```text
Prefix matching
```

GENIUS optimization.

---

# Pattern 1 — Count Subarrays Equal to K

---

## Trigger

- count subarrays
- target sum
- negative numbers present

---

## Problem

LeetCode 560 — Subarray Sum Equals K

---

# Key Insight

If:

```text
currSum - k
```

exists earlier,

then the subarray between them sums to:

```text
k
```

Store frequencies in hashmap.

---

## Solution

```java
class Solution {

    public int subarraySum(
        int[] nums,
        int k
    ) {

        HashMap<Integer, Integer> map =
            new HashMap<>();

        map.put(0, 1);

        int prefixSum = 0;
        int count = 0;

        for(int num : nums) {

            prefixSum += num;

            if(map.containsKey(
                    prefixSum - k)) {

                count +=
                    map.get(prefixSum - k);
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

# CP-Level Insight

Brute force checks:

```text
All subarrays
```

Complexity:

```text
O(n²)
```

Prefix + hashmap transforms it into:

```text
Single-pass lookup
```

Amazing optimization.

---

# Dry Run

```text
nums = [1, 2, 3]
k = 3
```

---

## Step 1

```text
prefixSum = 1
Need:
1 - 3 = -2
```

Not found.

Store:

```text
1
```

---

## Step 2

```text
prefixSum = 3
Need:
3 - 3 = 0
```

Found.

Count becomes:

```text
1
```

Subarray:

```text
[1,2]
```

---

## Step 3

```text
prefixSum = 6
Need:
6 - 3 = 3
```

Found.

Count becomes:

```text
2
```

Subarray:

```text
[3]
```

---

# Final Answer

```text
2
```

---

# Pattern 2 — Maximum Size Subarray Sum Equals K

---

## Trigger

- longest subarray
- target sum
- maximize length

---

## Problem

LeetCode 325 — Maximum Size Subarray Sum Equals k

---

# Key Insight

If:

```text
currSum - k
```

exists earlier,

then:

```text
Current index - earlier index
```

gives valid subarray length.

Store FIRST occurrence only.

---

## Solution

```java
class Solution {

    public int maxSubArrayLen(
        int[] nums,
        int k
    ) {

        HashMap<Integer, Integer> map =
            new HashMap<>();

        int prefixSum = 0;
        int maxLen = 0;

        for(int i = 0; i < nums.length; i++) {

            prefixSum += nums[i];

            if(prefixSum == k) {

                maxLen = i + 1;
            }

            if(map.containsKey(
                    prefixSum - k)) {

                maxLen = Math.max(
                    maxLen,
                    i - map.get(
                        prefixSum - k
                    )
                );
            }

            map.putIfAbsent(
                prefixSum,
                i
            );
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

# SUPER IMPORTANT INSIGHT

For:

```text
Longest length
```

Store:

```text
FIRST occurrence
```

Because earlier index gives:

```text
Larger subarray
```

---

# Advanced Competitive Programming Insights

---

# 1. Prefix Difference Thinking

Almost ALL subarray problems become:

```text
Current Prefix - Old Prefix
```

Train your brain to see this transformation.

---

# 2. HashMap Stores History

The hashmap represents:

```text
All previous prefix sums
```

We continuously ask:

```text
Can previous history help now?
```

---

# 3. Frequency vs Index Storage

Depending on problem:

| Requirement | Store |
|---|---|
| Count subarrays | Frequency |
| Longest subarray | First index |
| Shortest subarray | Latest index |

VERY important interview insight.

---

# 4. Negative Numbers Destroy Sliding Window

If negatives exist:

```text
Window size logic breaks
```

Prefix sum becomes the preferred tool.

---

# Common Mistake

Students forget:

```text
map.put(0, 1)
```

Why needed?

Because subarrays starting from:

```text
index 0
```

must also count.

---

# One-Line Memory Trick

```text
If subarray sum needed,
think:
Current Prefix - Old Prefix
```

---

# Final Interview Insight

The REAL power of this pattern is:

```text
Transforming subarray problems
into prefix relationships
```

Instead of exploring:

```text
All subarrays
```

we mathematically identify:

```text
Exactly which previous prefix
is needed
```

This converts many:

```text
O(n²)
```

solutions into:

```text
O(n)
```