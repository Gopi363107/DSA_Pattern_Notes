# Prefix Sum Pattern — Modulo Pattern Notes

---

# Definition

The **Modulo Prefix Sum Pattern** combines:

```text
Prefix Sum
+
Modulo Arithmetic
+
HashMap
```

to solve problems involving:

- divisibility
- remainder matching
- subarray divisibility
- modular conditions

---

# Core Intuition

Instead of comparing raw sums,

we compare:

```text
Remainders
```

because:

```text
Equal remainders imply divisibility
```

This creates extremely powerful optimizations.

---

# MOST IMPORTANT MODULO PROPERTY

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

# Why This Works

Suppose:

```text
prefixSum1 % k == prefixSum2 % k
```

Then:

```text
(prefixSum2 - prefixSum1)
```

is divisible by:

```text
k
```

Meaning:

```text
Subarray between them
has sum divisible by k
```

GENIUS observation.

---

# When Should I Think About This Pattern?

Use this pattern when:

- divisible by k
- remainder problems
- modulo conditions
- subarray divisibility
- continuous subarray multiple
- modular arithmetic

---

# Recognition Triggers

If problem contains:

- "divisible by k"
- "multiple of k"
- "modulo"
- "remainder"
- "continuous subarray"
- "sum divisible"

→ Think:

```text
Prefix Sum + Modulo
```

---

# Generic Template

```java
HashMap<Integer, Integer> map =
    new HashMap<>();

map.put(0, 1);

int prefixSum = 0;

for(int num : nums) {

    prefixSum += num;

    int rem = prefixSum % k;

    if(rem < 0) {
        rem += k;
    }

    if(map.containsKey(rem)) {

        // valid subarray exists
    }

    map.put(
        rem,
        map.getOrDefault(rem, 0) + 1
    );
}
```

---

# MOST IMPORTANT INSIGHT

We do NOT care about:

```text
Exact prefix sums
```

We care about:

```text
Their remainders
```

because equal remainders create:

```text
Divisible subarrays
```

---

# Pattern 1 — Continuous Subarray Sum

---

## Trigger

- divisible by k
- continuous subarray
- multiple of k

---

## Problem

LeetCode 523 — Continuous Subarray Sum

---

# Key Insight

If same remainder appears again:

```text
Subarray between them
is divisible by k
```

Store first occurrence index.

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

# CP-Level Insight

We are actually checking:

```text
Two prefix sums with same remainder
```

instead of checking all subarrays.

This converts:

```text
O(n²)
```

into:

```text
O(n)
```

---

# Dry Run

```text
nums = [23,2,4,6,7]
k = 6
```

---

## Step 1

```text
prefixSum = 23
23 % 6 = 5
```

Store:

```text
5 → index 0
```

---

## Step 2

```text
prefixSum = 25
25 % 6 = 1
```

Store:

```text
1 → index 1
```

---

## Step 3

```text
prefixSum = 29
29 % 6 = 5
```

Remainder:

```text
5
```

already seen.

Subarray between them:

```text
[2,4]
```

sum divisible by:

```text
6
```

---

# Pattern 2 — Subarray Sums Divisible by K

---

## Trigger

- count divisible subarrays
- modulo frequency
- remainder repetition

---

## Problem

LeetCode 974 — Subarray Sums Divisible by K

---

# Key Insight

If remainder repeats:

```text
Every previous occurrence
forms a valid subarray
```

Store frequencies.

---

## Solution

```java
class Solution {

    public int subarraysDivByK(
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

            int rem = prefixSum % k;

            if(rem < 0) {
                rem += k;
            }

            if(map.containsKey(rem)) {

                count += map.get(rem);
            }

            map.put(
                rem,
                map.getOrDefault(rem, 0) + 1
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
O(k)
```

or

```text
O(n)
```

depending on remainders stored.

---

# SUPER IMPORTANT NEGATIVE MODULO INSIGHT

In Java:

```java
-1 % 5 = -1
```

But mathematically we want:

```text
4
```

So always normalize:

```java
if(rem < 0) {
    rem += k;
}
```

VERY important interview trick.

---

# Advanced Competitive Programming Insights

---

# 1. Modulo Converts Large Numbers Into Patterns

Instead of tracking huge sums:

```text
Track only remainder classes
```

This drastically simplifies problems.

---

# 2. Equal Remainders = Divisible Difference

This identity appears EVERYWHERE in CP.

Master it deeply.

---

# 3. Frequency vs Index Storage

Depending on problem:

| Requirement | Store |
|---|---|
| Count subarrays | Frequency |
| Existence check | First index |
| Longest subarray | Earliest index |

Very common interview variation.

---

# 4. Prefix + Modulo Is a CP Weapon

This combination appears in:

- divisibility
- cyclic behavior
- rolling sums
- periodicity
- hashing concepts

SUPER important.

---

# Common Mistake

Students forget:

```text
Negative modulo normalization
```

This causes hidden test failures.

Always handle:

```java
if(rem < 0) rem += k;
```

---

# One-Line Memory Trick

```text
Equal remainders imply
divisible subarrays.
```

---

# Final Interview Insight

The REAL power of modulo pattern is:

```text
Transforming divisibility problems
into remainder matching
```

Instead of checking:

```text
All subarrays
```

we mathematically detect:

```text
Which previous remainder
creates divisibility
```

This turns many:

```text
O(n²)
```

solutions into:

```text
O(n)
```