# 06 - Interval Dynamic Programming Pattern

> **Core Idea:** Solve problems by finding the optimal answer for every **subarray** or **substring** (interval) and combining smaller intervals to build larger ones.

---

# What is Interval DP?

Interval DP is used when:

- The problem is about a **continuous interval**.
- We divide an interval into smaller intervals.
- The answer for a larger interval depends on answers from smaller intervals.

Unlike LIS or Knapsack, the state is an **interval**, not a single index.

---

# Core Idea

Suppose we have

```
nums = [3, 1, 5, 8]
```

Instead of asking:

```
What is the answer till index i?
```

we ask:

```
What is the answer for interval

[i...j] ?
```

---

# What is an Interval?

An interval is simply a continuous range.

Example

```
Array

1 2 3 4 5
```

Intervals

```
[1]

[2]

[1,2]

[2,3]

[1,2,3]

[2,3,4]

[1,2,3,4,5]
```

---

# State Definition

Most common

```
dp[i][j]
```

Meaning

```
Answer for interval

[i...j]
```

---

# When Should You Think of Interval DP?

Whenever the problem contains:

- Subarray
- Substring
- Interval
- Range
- Merge
- Burst
- Remove
- Cut
- Parenthesize
- Palindrome

Immediately ask:

> Can I solve a larger interval by splitting it into smaller intervals?

If YES, think Interval DP.

---

# Two Major Interval DP Patterns

---

## Pattern 1 — Split DP

Split the interval at every possible position.

```
[i........j]

      k

[i...k]

[k+1...j]
```

Transition

```
Try every k
```

Take

```
Minimum

Maximum
```

or

```
Best Answer
```

Examples

- Matrix Chain Multiplication
- Minimum Cost to Cut Stick
- Merge Stones

---

## Pattern 2 — Last Operation DP

Instead of choosing the first operation,

choose the **last** operation.

Example

```
Burst Balloons

Remove Boxes

Strange Printer
```

The last operation creates independent subproblems.

---

# Generic Thinking Process

## Step 1

Define

```
dp[i][j]
```

---

## Step 2

Choose

```
Split

OR

Last Operation
```

---

## Step 3

Transition

Combine smaller intervals.

---

## Step 4

Base Case

Usually

```
Single element

or

Empty interval
```

---

## Step 5

Build

Small intervals

↓

Large intervals

---

# Split DP Recurrence

For every split point

```
k
```

between

```
i

and

j
```

```text
dp[i][j]

=

best(

dp[i][k]

+

dp[k+1][j]

+

cost
)
```

---

# Last Operation Recurrence

Choose every possible

```
k
```

as the last operation.

```text
dp[i][j]

=

best(

left interval

+

right interval

+

current contribution

)
```

---

# Memoization Template

```java
int solve(int i, int j){

    if(base case)
        return answer;

    if(dp[i][j] != -1)
        return dp[i][j];

    int ans = INITIAL_VALUE;

    for(int k = i; k < j; k++){

        ans = combine(
                ans,
                solve(i, k),
                solve(k+1, j)
        );
    }

    return dp[i][j] = ans;
}
```

---

# Tabulation Template

Compute intervals by increasing length.

```java
for(int len = 2; len <= n; len++){

    for(int i = 0; i + len - 1 < n; i++){

        int j = i + len - 1;

        // compute dp[i][j]
    }
}
```

---

# Why Iterate by Length?

Example

```
dp[2][5]
```

depends on

```
dp[2][3]

dp[4][5]

dp[2][4]

...
```

Smaller intervals must already be computed.

Therefore

```
Length = 1

↓

Length = 2

↓

Length = 3

↓

...

↓

Length = n
```

---

# Pattern Recognition

Question contains

```
Substring

Subarray

Merge

Burst

Cut

Partition

Palindrome

Range
```

↓

State

```
dp[i][j]
```

↓

Split

↓

Combine

↓

Memoization

↓

Tabulation

---

# Competitive Programming Insight

The hardest part is identifying

```
What is the split?

OR

What should be chosen last?
```

Once identified,

the recurrence becomes much easier.

---

# Problem 1

## LeetCode 312 — Burst Balloons

Difficulty

Hard

---

## Core Idea

Do **NOT** think

```
Which balloon to burst first?
```

Think

```
Which balloon is burst LAST?
```

This makes left and right intervals independent.

---

## State

```
dp[i][j]

Maximum coins

from interval

[i...j]
```

---

## Recurrence

Choose every balloon

```
k
```

as the last burst.

```
dp[i][j]

=

max(

left

+

right

+

current coins

)
```

---

## Java Solution

```java
class Solution {

    public int maxCoins(int[] nums) {

        int n = nums.length;

        int[] arr = new int[n + 2];

        arr[0] = 1;
        arr[n + 1] = 1;

        for(int i = 0; i < n; i++)
            arr[i + 1] = nums[i];

        int[][] dp = new int[n + 2][n + 2];

        for(int len = 1; len <= n; len++){

            for(int left = 1;
                left <= n - len + 1;
                left++){

                int right = left + len - 1;

                for(int k = left;
                    k <= right;
                    k++){

                    dp[left][right] =
                        Math.max(

                            dp[left][right],

                            dp[left][k-1]

                            +

                            dp[k+1][right]

                            +

                            arr[left-1]

                            *

                            arr[k]

                            *

                            arr[right+1]
                        );
                }
            }
        }

        return dp[1][n];
    }
}
```

---

### Time Complexity

```
O(n³)
```

### Space Complexity

```
O(n²)
```

---

# Problem 2

## LeetCode 1547 — Minimum Cost to Cut a Stick

Difficulty

Hard

---

## Core Idea

Choose

```
Which cut

is performed first
```

inside an interval.

Each cut splits the interval into two smaller intervals.

---

## State

```
dp[i][j]

Minimum cost

to perform cuts

between

i

and

j
```

---

## Recurrence

Try every cut.

Take minimum.

---

### Time Complexity

```
O(n³)
```

### Space Complexity

```
O(n²)
```

---

# Problem 3

## LeetCode 664 — Strange Printer

Difficulty

Hard

---

## Core Idea

The printer can print the same character over existing characters.

Merge equal characters whenever possible.

---

## State

```
dp[i][j]

Minimum turns

to print

substring

[i...j]
```

---

## Recurrence

Start with

```
1 + dp[i+1][j]
```

If matching characters exist later,

merge operations to reduce turns.

---

### Java Solution (Core)

```java
for(int len = 2; len <= n; len++){

    for(int i = 0;
        i + len - 1 < n;
        i++){

        int j = i + len - 1;

        dp[i][j] = 1 + dp[i+1][j];

        for(int k = i + 1;
            k <= j;
            k++){

            if(s.charAt(i) == s.charAt(k)){

                dp[i][j] = Math.min(

                    dp[i][j],

                    dp[i][k-1]

                    +

                    dp[k+1][j]

                );
            }
        }
    }
}
```

---

### Time Complexity

```
O(n³)
```

### Space Complexity

```
O(n²)
```

---

# Common Mistakes

❌ Using prefix DP instead of interval DP.

❌ Wrong interval traversal order.

❌ Forgetting to try every split point.

❌ Incorrect base case for single-element intervals.

❌ Thinking greedily instead of considering all partitions.

---

# Interview Mental Checklist

- Is the answer defined over a subarray or substring?
- Can I define `dp[i][j]`?
- Should I split the interval or choose the last operation?
- Am I iterating by interval length?
- What is the base case?

---

# Pattern Summary

| Feature | Description |
|----------|-------------|
| State | `dp[i][j]` |
| Core Idea | Solve smaller intervals first |
| Transition | Split or Last Operation |
| Traversal | Increasing interval length |
| Time Complexity | Usually `O(n³)` |
| Space | `O(n²)` |
| Common Topics | Burst, Merge, Cut, Palindrome, Parenthesization |

---

# Mastery Checklist

- [ ] Recognize Interval DP problems.
- [ ] Define interval states.
- [ ] Derive split transitions.
- [ ] Understand the "last operation" trick.
- [ ] Write Memoization.
- [ ] Convert to Tabulation.
- [ ] Iterate intervals by increasing length.
- [ ] Solve Burst Balloons, Minimum Cost to Cut a Stick, and Strange Printer.

---

# Split vs Last Operation

| Split DP | Last Operation DP |
|-----------|-------------------|
| Divide interval into two parts | Assume one operation happens last |
| Matrix Chain Multiplication | Burst Balloons |
| Merge Stones | Remove Boxes |
| Cut Stick | Strange Printer |

---

> **Golden Rule:** If the answer is defined for a **continuous interval** and can be built by combining **smaller intervals**, think **Interval Dynamic Programming**.