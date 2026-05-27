# Prefix XOR Pattern — XOR Prefix Notes

---

# Definition

The **Prefix XOR Pattern** preprocesses cumulative XOR values so that:

```text
Subarray XOR queries
become efficient
```

Just like prefix sum,

but using:

```text
XOR operation
```

instead of addition.

---

# Core Intuition

Store:

```text
XOR from index 0 → i
```

Then any subarray XOR can be computed using:

```text
Prefix XOR relationships
```

---

# MOST IMPORTANT XOR PROPERTY

XOR has a magical cancellation property:

```text
A ^ A = 0
```

and:

```text
A ^ 0 = A
```

This is the ENTIRE foundation.

---

# Prefix XOR Formula

If:

```text
prefixXor[i]
=
XOR from 0 → i
```

Then:

```text
XOR(L → R)
=
prefixXor[R]
^
prefixXor[L - 1]
```

Why?

Because common prefixes cancel out.

---

# Why This Works

Suppose:

```text
prefixXor[R]
=
a ^ b ^ c ^ d
```

and:

```text
prefixXor[L-1]
=
a ^ b
```

Then:

```text
(a ^ b ^ c ^ d)
^
(a ^ b)
```

Since:

```text
a ^ a = 0
b ^ b = 0
```

Remaining:

```text
c ^ d
```

GENIUS cancellation trick.

---

# When Should I Think About Prefix XOR?

Use this pattern when:

- subarray XOR
- XOR equals k
- cumulative XOR
- bit manipulation + subarrays
- XOR range queries

---

# Recognition Triggers

If problem contains:

- "XOR subarray"
- "range XOR"
- "cumulative XOR"
- "XOR equals k"
- "binary xor"
- bitwise subarray problems

→ Think:

```text
Prefix XOR
```

---

# Generic Template

## Building Prefix XOR

```java
int[] prefixXor =
    new int[n];

prefixXor[0] = arr[0];

for(int i = 1; i < n; i++) {

    prefixXor[i] =
        prefixXor[i - 1] ^ arr[i];
}
```

---

## Range XOR Query

```java
int rangeXor(int L, int R) {

    if(L == 0) {
        return prefixXor[R];
    }

    return prefixXor[R]
           ^ prefixXor[L - 1];
}
```

---

# MOST IMPORTANT INSIGHT

XOR behaves similarly to:

```text
Addition + subtraction
```

because XOR cancels duplicates automatically.

This enables:

```text
Fast subarray computations
```

---

# Pattern 1 — XOR Queries of a Subarray

---

## Trigger

- multiple XOR queries
- subarray XOR
- immutable array

---

## Problem

LeetCode 1310 — XOR Queries of a Subarray

---

# Key Insight

Subarray XOR becomes:

```text
Prefix XOR cancellation
```

Exactly like prefix sum subtraction.

---

## Solution

```java
class Solution {

    public int[] xorQueries(
        int[] arr,
        int[][] queries
    ) {

        int n = arr.length;

        int[] prefix =
            new int[n];

        prefix[0] = arr[0];

        for(int i = 1; i < n; i++) {

            prefix[i] =
                prefix[i - 1] ^ arr[i];
        }

        int[] ans =
            new int[queries.length];

        for(int i = 0; i < queries.length; i++) {

            int L = queries[i][0];
            int R = queries[i][1];

            if(L == 0) {

                ans[i] = prefix[R];
            }
            else {

                ans[i] =
                    prefix[R]
                    ^ prefix[L - 1];
            }
        }

        return ans;
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

Without prefix XOR:

```text
Each query scans subarray
```

Complexity:

```text
O(n × q)
```

Prefix XOR reduces queries to:

```text
O(1)
```

---

# Pattern 2 — Count Subarrays With XOR Equal to K

---

## Trigger

- subarray XOR equals k
- count subarrays
- XOR target

---

## Problem

Classic XOR Prefix Problem

---

# Key Insight

Suppose current XOR is:

```text
currXor
```

Need:

```text
Subarray XOR = k
```

Then:

```text
previousXor
=
currXor ^ k
```

because:

```text
A ^ B = C
⇒
A = B ^ C
```

VERY important XOR identity.

---

## Solution

```java
class Solution {

    public int countSubarrays(
        int[] nums,
        int k
    ) {

        HashMap<Integer, Integer> map =
            new HashMap<>();

        map.put(0, 1);

        int xor = 0;
        int count = 0;

        for(int num : nums) {

            xor ^= num;

            if(map.containsKey(xor ^ k)) {

                count +=
                    map.get(xor ^ k);
            }

            map.put(
                xor,
                map.getOrDefault(
                    xor,
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

# Dry Run

```text
nums = [4,2,2,6,4]
k = 6
```

---

## Step 1

```text
xor = 4
Need:
4 ^ 6 = 2
```

Not found.

Store:

```text
4
```

---

## Step 2

```text
xor = 6
Need:
6 ^ 6 = 0
```

Found.

Count becomes:

```text
1
```

Subarray:

```text
[4,2]
```

---

## Step 3

Continue similarly.

---

# SUPER IMPORTANT XOR INSIGHT

For XOR problems:

```text
Need previousXor
=
currXor ^ target
```

This is analogous to:

```text
currSum - k
```

in prefix sums.

---

# Advanced Competitive Programming Insights

---

# 1. XOR Is Reversible

Unlike addition:

```text
XOR automatically cancels duplicates
```

This makes it PERFECT for prefix patterns.

---

# 2. Prefix XOR Mirrors Prefix Sum

| Prefix Sum | Prefix XOR |
|---|---|
| subtraction | xor cancellation |
| currSum - k | currXor ^ k |

Very important analogy.

---

# 3. Bit Manipulation + Prefix Pattern

Prefix XOR combines:

```text
Bit manipulation
+
HashMap optimization
```

Very common in CP.

---

# 4. XOR Problems Often Hide Prefix Logic

Many difficult XOR problems secretly reduce to:

```text
Repeated prefix XOR relationships
```

Recognizing this is a huge skill.

---

# Common Mistake

Students forget:

```text
XOR is NOT addition
```

You cannot use:

```text
currXor - k
```

Instead use:

```text
currXor ^ k
```

VERY important.

---

# One-Line Memory Trick

```text
Prefix XOR works because
equal XOR parts cancel out.
```

---

# Final Interview Insight

The REAL power of prefix XOR is:

```text
Using XOR cancellation
to isolate subarray values
```

Instead of recalculating:

```text
Entire subarrays
```

we mathematically eliminate:

```text
Common prefixes
```

This transforms many:

```text
O(n²)
```

solutions into:

```text
O(n)
```