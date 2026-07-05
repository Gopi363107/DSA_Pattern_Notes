# 05 - Longest Increasing Subsequence (LIS) DP Pattern

> **Core Idea:** Build the best increasing sequence by deciding whether to extend a previous subsequence.

---

# What is LIS DP?

LIS DP is used when:

- We are given an array or sequence.
- We need to find the best increasing (or decreasing) sequence.
- The order of elements must be preserved.
- Elements do **not** have to be contiguous.

This pattern is the foundation for many sequence optimization problems.

---

# What is a Subsequence?

A subsequence keeps the relative order but can skip elements.

Example:

```
nums = [3, 1, 5, 2, 6]
```

Valid subsequences:

```
3 5 6
1 2 6
1 5
```

Invalid:

```
6 5
```

because the order changes.

---

# Example

```
nums =

10 9 2 5 3 7 101 18
```

Longest Increasing Subsequence

```
2 3 7 101
```

Length

```
4
```

---

# Core Idea

For every index

```
i
```

ask

> What is the longest increasing subsequence ending at index i?

Every previous element can potentially extend the current subsequence.

---

# When Should You Think of LIS DP?

Whenever the problem contains:

- Increasing
- Decreasing
- Sequence
- Chain
- Envelope
- Russian Doll
- Maximum chain
- Compatible intervals
- Ordered sequence

Immediately ask:

> Can every previous element extend the current answer?

If YES, think LIS DP.

---

# State Definition

Most common

```
dp[i]
```

Meaning

```
Length of LIS ending at index i
```

---

# Generic Thinking Process

## Step 1

Define

```
dp[i]
```

---

## Step 2

Look at every previous index.

```
0

...

i-1
```

---

## Step 3

Can previous element extend current?

```
nums[j] < nums[i]
```

---

## Step 4

Update

```
dp[i]

=

max(

dp[i],

dp[j] + 1

)
```

---

## Step 5

Answer

Maximum value in

```
dp[]
```

---

# Classic LIS Recurrence

For every

```
j < i
```

If

```
nums[j] < nums[i]
```

Then

```text
dp[i]

=

max(

dp[i],

dp[j] + 1

)
```

---

# O(n²) DP Template

```java
int n = nums.length;

int[] dp = new int[n];

Arrays.fill(dp, 1);

int answer = 1;

for(int i = 0; i < n; i++){

    for(int j = 0; j < i; j++){

        if(nums[j] < nums[i]){

            dp[i] = Math.max(
                    dp[i],
                    dp[j] + 1
            );
        }
    }

    answer = Math.max(answer, dp[i]);
}

return answer;
```

---

# O(n log n) Optimization

Maintain an array

```
tails[]
```

where

```
tails[k]

=

Smallest possible tail

of an increasing subsequence

of length

k+1
```

Use Binary Search.

This gives

```
O(n log n)
```

---

# Binary Search Template

```java
List<Integer> tails = new ArrayList<>();

for(int num : nums){

    int index = Collections.binarySearch(
                    tails,
                    num
                );

    if(index < 0)
        index = -(index + 1);

    if(index == tails.size())
        tails.add(num);
    else
        tails.set(index, num);
}

return tails.size();
```

---

# Pattern Recognition

Question contains

```
Increasing

Decreasing

Chain

Sequence

Envelope

Compatible

Ordering
```

↓

State

```
dp[i]
```

↓

Previous Elements

↓

Transition

↓

Optimization

↓

Binary Search

---

# Competitive Programming Insight

Whenever you see

```
Longest

Increasing

Chain
```

first think

```
LIS
```

Many hard problems reduce to LIS after sorting or transformation.

---

# Problem 1

## LeetCode 300 — Longest Increasing Subsequence

Difficulty

Medium

---

## Core Idea

Find the longest increasing subsequence.

---

## State

```
dp[i]

LIS ending at i
```

---

## Java Solution (O(n²))

```java
class Solution {

    public int lengthOfLIS(int[] nums) {

        int n = nums.length;

        int[] dp = new int[n];

        Arrays.fill(dp, 1);

        int ans = 1;

        for(int i = 0; i < n; i++){

            for(int j = 0; j < i; j++){

                if(nums[j] < nums[i]){

                    dp[i] = Math.max(
                            dp[i],
                            dp[j] + 1
                    );
                }
            }

            ans = Math.max(ans, dp[i]);
        }

        return ans;
    }
}
```

---

### Time Complexity

```
O(n²)
```

### Space Complexity

```
O(n)
```

---

### Optimization

Binary Search

```
O(n log n)
```

---

# Problem 2

## LeetCode 673 — Number of Longest Increasing Subsequence

Difficulty

Medium

---

## Core Idea

Maintain

```
length[]

count[]
```

instead of only

```
dp[]
```

---

## State

```
length[i]

LIS length

ending at i
```

```
count[i]

Number of LIS

ending at i
```

---

## Transition

Update

```
length

and

count
```

carefully.

---

## Java Solution

```java
class Solution {

    public int findNumberOfLIS(int[] nums) {

        int n = nums.length;

        int[] len = new int[n];
        int[] count = new int[n];

        Arrays.fill(len, 1);
        Arrays.fill(count, 1);

        int maxLen = 1;

        for(int i = 0; i < n; i++){

            for(int j = 0; j < i; j++){

                if(nums[j] < nums[i]){

                    if(len[j] + 1 > len[i]){

                        len[i] = len[j] + 1;
                        count[i] = count[j];

                    }else if(len[j] + 1 == len[i]){

                        count[i] += count[j];
                    }
                }
            }

            maxLen = Math.max(maxLen, len[i]);
        }

        int ans = 0;

        for(int i = 0; i < n; i++){

            if(len[i] == maxLen)
                ans += count[i];
        }

        return ans;
    }
}
```

---

### Time Complexity

```
O(n²)
```

### Space Complexity

```
O(n)
```

---

# Problem 3

## LeetCode 354 — Russian Doll Envelopes

Difficulty

Hard

---

## Core Idea

Sort envelopes by:

- Width ascending
- Height descending (if widths are equal)

Then perform LIS on heights.

---

## State

```
LIS

on

height
```

---

## Java Solution

```java
class Solution {

    public int maxEnvelopes(int[][] envelopes) {

        Arrays.sort(envelopes, (a, b) -> {

            if(a[0] == b[0])
                return b[1] - a[1];

            return a[0] - b[0];
        });

        List<Integer> tails = new ArrayList<>();

        for(int[] e : envelopes){

            int h = e[1];

            int idx = Collections.binarySearch(
                    tails,
                    h
            );

            if(idx < 0)
                idx = -(idx + 1);

            if(idx == tails.size())
                tails.add(h);
            else
                tails.set(idx, h);
        }

        return tails.size();
    }
}
```

---

### Time Complexity

```
O(n log n)
```

### Space Complexity

```
O(n)
```

---

# Common Mistakes

❌ Confusing subsequence with subarray.

❌ Forgetting that order must be preserved.

❌ Using `<=` instead of `<` for strictly increasing problems.

❌ Forgetting to initialize every `dp[i]` with `1`.

❌ Assuming Binary Search reconstructs the actual LIS.

---

# Interview Mental Checklist

- Is this asking for an increasing sequence?
- Does every previous element affect the current one?
- Can I define `dp[i]`?
- Is `O(n²)` acceptable?
- Can Binary Search optimize it to `O(n log n)`?

---

# Pattern Summary

| Feature | Description |
|----------|-------------|
| State | `dp[i]` |
| Core Decision | Extend Previous Sequence |
| Dimension | 1D |
| Time Complexity | `O(n²)` or `O(n log n)` |
| Space | `O(n)` |
| Common Topics | LIS, Chains, Envelopes, Bridges, Subsequences |

---

# Mastery Checklist

- [ ] Understand subsequence vs subarray.
- [ ] Solve LIS using `O(n²)` DP.
- [ ] Learn Binary Search optimization.
- [ ] Solve counting variants.
- [ ] Solve chain-based problems.
- [ ] Know when sorting converts a problem into LIS.

---

# O(n²) vs O(n log n)

| Feature | O(n²) DP | O(n log n) Binary Search |
|----------|----------|--------------------------|
| Finds Length | ✅ | ✅ |
| Reconstruct LIS Easily | ✅ | ❌ (requires additional arrays) |
| Simpler | ✅ | ❌ |
| Interview Friendly | ✅ | ✅ |
| Competitive Programming | Sometimes | Preferred |

---

# Related Transformations

Many problems become LIS after preprocessing:

- Sort envelopes → LIS
- Sort bridges → LIS
- Pair sorting → LIS
- Box stacking → LIS
- Maximum chain of pairs → LIS

---

> **Golden Rule:** If a problem asks for the **longest increasing (or decreasing) ordered sequence**, first think **LIS Dynamic Programming**.