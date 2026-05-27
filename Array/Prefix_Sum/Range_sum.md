# Prefix Sum Pattern — Range Sum Queries Notes

---

# Definition

The **Prefix Sum** pattern preprocesses cumulative sums so that:

```text
Range queries become O(1)
```

Instead of calculating every subarray repeatedly.

---

# Core Intuition

Store:

```text
Sum from index 0 → i
```

Then any range:

```text
L → R
```

can be computed instantly.

---

# Prefix Sum Formula

If:

```text
prefix[i]
=
sum of elements from 0 → i
```

Then:

```text
RangeSum(L, R)
=
prefix[R] - prefix[L - 1]
```

Special case:

```text
L = 0
```

Then:

```text
answer = prefix[R]
```

---

# Why Prefix Sum Works

Instead of recalculating:

```text
arr[L] + arr[L+1] + ...
```

every time,

we reuse previously computed information.

This converts:

```text
Repeated work
```

into:

```text
One-time preprocessing
```

---

# When Should I Think About Prefix Sum?

Use this pattern when:

- multiple range sum queries
- subarray sums
- cumulative frequencies
- repeated interval calculations
- immutable arrays
- fast query requirements

---

# Recognition Triggers

If problem contains:

- "range sum"
- "sum between L and R"
- "subarray sum"
- "many queries"
- "cumulative"
- "continuous segment"

→ Think:

```text
Prefix Sum
```

---

# Generic Template

## Building Prefix Array

```java
int n = arr.length;

int[] prefix = new int[n];

prefix[0] = arr[0];

for(int i = 1; i < n; i++) {

    prefix[i] =
        prefix[i - 1] + arr[i];
}
```

---

## Range Query

```java
int rangeSum(int L, int R) {

    if(L == 0) {
        return prefix[R];
    }

    return prefix[R] - prefix[L - 1];
}
```

---

# MOST IMPORTANT INSIGHT

Prefix sums convert:

```text
Repeated subarray calculations
```

into:

```text
Constant-time queries
```

Preprocessing cost:

```text
O(n)
```

Query cost:

```text
O(1)
```

---

# Pattern 1 — Range Sum Query Immutable

---

## Trigger

- many sum queries
- immutable array
- repeated ranges

---

## Problem

LeetCode 303 — Range Sum Query Immutable

---

# Key Insight

Precompute cumulative sums once.

Every future query becomes:

```text
Two prefix operations
```

---

## Solution

```java
class NumArray {

    int[] prefix;

    public NumArray(int[] nums) {

        int n = nums.length;

        prefix = new int[n];

        prefix[0] = nums[0];

        for(int i = 1; i < n; i++) {

            prefix[i] =
                prefix[i - 1] + nums[i];
        }
    }

    public int sumRange(int left, int right) {

        if(left == 0) {
            return prefix[right];
        }

        return prefix[right]
             - prefix[left - 1];
    }
}
```

---

# Complexity

## Preprocessing

```text
O(n)
```

## Query Time

```text
O(1)
```

## Space Complexity

```text
O(n)
```

---

# CP-Level Insight

Without prefix sum:

```text
Each query → O(n)
```

For:

```text
q queries
```

Total:

```text
O(n × q)
```

Prefix sum reduces it to:

```text
O(n + q)
```

HUGE optimization.

---

# Pattern 2 — Subarray Sum Equals K

---

## Trigger

- subarray sums
- target sum
- count subarrays

---

## Problem

LeetCode 560 — Subarray Sum Equals K

---

# Key Insight

Suppose current prefix sum is:

```text
currSum
```

Need previous prefix:

```text
previousPrefix = currSum - k
```

If such prefix existed before:

```text
Subarray with sum k exists
```

Use hashmap for frequencies.

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

# MOST IMPORTANT CP INSIGHT

The hashmap stores:

```text
How many times each prefix sum appeared
```

This transforms:

```text
Subarray search
```

into:

```text
Prefix difference matching
```

GENIUS observation.

---

# Pattern 3 — Continuous Subarray Sum

---

## Trigger

- divisible by k
- remainder logic
- subarray divisibility

---

## Problem

LeetCode 523 — Continuous Subarray Sum

---

# Key Insight

If:

```text
prefixSum % k
```

repeats,

then the subarray between them is divisible by:

```text
k
```

Because equal remainders cancel out.

---

## Solution

```java
class Solution {

    public boolean checkSubarraySum(
        int[] nums,
        int k
    ) {

        HashMap<Integer, Integer> map =
            new HashMap<>();

        map.put(0, -1);

        int prefixSum = 0;

        for(int i = 0; i < nums.length; i++) {

            prefixSum += nums[i];

            int rem = prefixSum % k;

            if(map.containsKey(rem)) {

                if(i - map.get(rem) > 1) {
                    return true;
                }
            }
            else {

                map.put(rem, i);
            }
        }

        return false;
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

# SUPER IMPORTANT MODULO INSIGHT

If:

```text
A % k == B % k
```

Then:

```text
(A - B) % k == 0
```

This is the ENTIRE foundation.

---

# Advanced Competitive Programming Insights

---

# 1. Prefix Sum = Preprocessing Pattern

Trade:

```text
Extra memory
```

for:

```text
Fast queries
```

Classic optimization technique.

---

# 2. Prefix Difference Principle

Almost every prefix problem becomes:

```text
Current Prefix - Previous Prefix
```

Recognize this transformation.

---

# 3. HashMap + Prefix Sum

Very powerful combo for:

- subarray counts
- target sums
- divisibility
- frequency tracking

Extremely common in interviews.

---

# 4. Prefix Sum Converts Nested Loops

Brute force:

```text
Check all subarrays
```

Usually:

```text
O(n²)
```

Prefix optimization often gives:

```text
O(n)
```

---

# Common Mistake

Students recompute sums repeatedly:

```text
Inside nested loops
```

This wastes work.

Prefix sum stores reusable information.

---

# One-Line Memory Trick

```text
If repeated range calculations exist,
precompute cumulative information.
```

---

# Final Interview Insight

The REAL power of prefix sums is:

```text
Turning repeated calculations
into reusable information
```

This is one of the MOST IMPORTANT
optimization ideas in DSA.