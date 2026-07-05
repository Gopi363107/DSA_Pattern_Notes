# 01 - 1D Dynamic Programming Pattern

> "Current state depends on one or more previous states."

This is the **first DP pattern** every software engineer should master. Around **70% of beginner and intermediate DP problems** belong to this category.

---

# What is 1D DP?

1D DP means:

- We solve problems where **only one variable changes**.
- We store answers in a **single array** (or sometimes just variables).
- Every answer depends on previous answers.

Instead of solving the same subproblem repeatedly, we save it.

---

# Core Idea

Suppose

```
dp[i]
```

means

> Answer for the first i elements
or
Answer till index i.

Then

```
dp[i] = something(dp[i-1], dp[i-2], ...)
```

Every state depends on previously solved states.

---

# When Should You Think of 1D DP?

Whenever you hear:

- Count ways
- Maximum profit
- Minimum cost
- Reach destination
- Jump
- Rob houses
- Climb stairs
- Decode string
- Partition
- Subsequence ending at i

Immediately ask:

> Can I define an answer ending at index i?

If YES,
there is a high chance it is 1D DP.

---

# Triggers

### Trigger 1

Problem asks

> Number of ways

Examples

- Climbing stairs
- Decode ways
- Coin change (ways)

---

### Trigger 2

Problem asks

> Maximum or Minimum

Examples

- House Robber
- Maximum Sum
- Min Cost Climbing Stairs

---

### Trigger 3

Answer depends only on previous indices

Example

```
current = previous + something
```

---

### Trigger 4

Array is processed from left to right

```
0
1
2
3
4
...
n
```

---

# Generic Thinking Process

Whenever you solve DP

Step 1

Find State

```
What does dp[i] represent?
```

Example

```
Maximum money till house i
```

---

Step 2

Transition

```
How can I reach state i?
```

---

Step 3

Base Case

```
dp[0]
dp[1]
```

---

Step 4

Iteration Order

Usually

```
Left → Right
```

---

Step 5

Optimization

Can previous states alone solve it?

If YES

Space Optimization.

---

# General Template

```java
int n = nums.length;

int[] dp = new int[n];

dp[0] = base;

for(int i = 1; i < n; i++){

    dp[i] = transition(dp,...);

}

return dp[n-1];
```

---

# Space Optimized Template

```java
int prev2 = ...;
int prev1 = ...;

for(int i = 2; i < n; i++){

    int curr = transition(prev1, prev2);

    prev2 = prev1;
    prev1 = curr;
}

return prev1;
```

---

# Pattern Recognition

Question asks

```
Maximum

Minimum

Ways

Count

Reach

Jump

Cost

Profit
```

↓

State

```
dp[i]
```

↓

Recurrence

```
dp[i] = function(previous states)
```

↓

Memoization

↓

Tabulation

↓

Space Optimization

---

# Competitive Programming Insight

Always ask

### Can I define

```
dp[i]
```

instead of

```
answer
```

If yes,
the recurrence usually becomes obvious.

---

# Problem 1

## LeetCode 198 - House Robber

Difficulty

Easy

---

## Core Idea

At every house

Two choices

```
Take current house

OR

Skip current house
```

If you take current

```
nums[i] + dp[i-2]
```

If you skip

```
dp[i-1]
```

Take maximum.

---

## State

```
dp[i]

Maximum money till index i
```

---

## Recurrence

```
dp[i] = max(
dp[i-1],
nums[i] + dp[i-2]
)
```

---

## Java Solution

```java
class Solution {

    public int rob(int[] nums) {

        int n = nums.length;

        if(n==1)
            return nums[0];

        int[] dp = new int[n];

        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);

        for(int i=2;i<n;i++){

            dp[i] = Math.max(dp[i-1],
                             nums[i] + dp[i-2]);

        }

        return dp[n-1];
    }
}
```

---

### Time Complexity

```
O(n)
```

### Space Complexity

```
O(n)
```

---

### Space Optimized

```java
class Solution {

    public int rob(int[] nums) {

        int n = nums.length;

        if(n==1)
            return nums[0];

        int prev2 = nums[0];
        int prev1 = Math.max(nums[0], nums[1]);

        for(int i=2;i<n;i++){

            int curr = Math.max(prev1,
                                nums[i] + prev2);

            prev2 = prev1;
            prev1 = curr;
        }

        return prev1;
    }
}
```

Time

```
O(n)
```

Space

```
O(1)
```

---

# Problem 2

## LeetCode 740 - Delete and Earn

Difficulty

Medium

---

## Core Idea

After grouping equal values, taking value `x` means you cannot take `x-1` or `x+1`.

This transforms directly into the House Robber pattern.

---

## State

```
dp[i]

Maximum points considering values from 0 to i
```

---

## Recurrence

```
dp[i] = max(
dp[i-1],
points[i] + dp[i-2]
)
```

where `points[i]` is the total score earned by taking all occurrences of value `i`.

---

## Java Solution

```java
class Solution {

    public int deleteAndEarn(int[] nums) {

        int max = 0;

        for(int num : nums)
            max = Math.max(max, num);

        int[] points = new int[max + 1];

        for(int num : nums)
            points[num] += num;

        if(max == 0)
            return points[0];

        int[] dp = new int[max + 1];

        dp[0] = points[0];
        dp[1] = Math.max(points[0], points[1]);

        for(int i = 2; i <= max; i++){

            dp[i] = Math.max(dp[i - 1], points[i] + dp[i - 2]);

        }

        return dp[max];
    }
}
```

---

### Time Complexity

```
O(n + maxValue)
```

### Space Complexity

```
O(maxValue)
```

---

### Optimization

Space can be reduced to **O(1)** using two variables (`prev1`, `prev2`), exactly like House Robber.

---

# Problem 3

## LeetCode 91 - Decode Ways

Difficulty

Medium

---

## Core Idea

At every position

```
Take one digit

OR

Take two digits
```

if valid.

---

## State

```
dp[i]

Number of ways to decode first i characters
```

---

## Recurrence

```
If one digit valid
dp[i] += dp[i-1]

If two digits valid
dp[i] += dp[i-2]
```

---

## Java Solution

```java
class Solution {

    public int numDecodings(String s) {

        int n = s.length();

        int[] dp = new int[n + 1];

        dp[0] = 1;

        dp[1] = s.charAt(0) == '0' ? 0 : 1;

        for(int i = 2; i <= n; i++){

            int one = Integer.parseInt(s.substring(i - 1, i));

            if(one >= 1 && one <= 9)
                dp[i] += dp[i - 1];

            int two = Integer.parseInt(s.substring(i - 2, i));

            if(two >= 10 && two <= 26)
                dp[i] += dp[i - 2];
        }

        return dp[n];
    }
}
```

---

### Time Complexity

```
O(n)
```

### Space Complexity

```
O(n)
```

---

### Optimization

Only the previous two states are required, so the solution can be optimized to **O(1)** space.

---

# Common Mistakes

❌ Wrong definition of state

❌ Missing base cases

❌ Incorrect iteration order

❌ Forgetting edge cases (`n = 1`, empty input)

❌ Using recursion without memoization (causes TLE)

---

# Mental Checklist During Interviews

- What does `dp[i]` represent?
- What are my choices at index `i`?
- Which previous states are needed?
- What are the base cases?
- Can I convert recursion to tabulation?
- Can I reduce space from `O(n)` to `O(1)`?

---

# Pattern Summary

| Feature | Description |
|----------|-------------|
| State | `dp[i]` |
| Dimension | One variable changes |
| Direction | Left → Right |
| Transition | From previous states |
| Complexity | Usually `O(n)` |
| Space | `O(n)` → often `O(1)` |
| Common Topics | Ways, Cost, Profit, Jump, Robbery, Decoding |

---

# Mastery Checklist

- [ ] Identify when a problem fits the 1D DP pattern.
- [ ] Define an appropriate `dp[i]` state.
- [ ] Derive the recurrence relation.
- [ ] Write the memoized solution.
- [ ] Convert it to tabulation.
- [ ] Optimize space when only previous states are required.
- [ ] Solve representative problems like **House Robber**, **Delete and Earn**, and **Decode Ways** without looking at notes.

---

> **Golden Rule:** If the answer at index `i` depends only on a few previous indices (`i-1`, `i-2`, ...), think **1D Dynamic Programming** first.