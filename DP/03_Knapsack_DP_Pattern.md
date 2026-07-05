# 03 - Knapsack Dynamic Programming Pattern

> **Core Idea:** At every step, decide whether to **take** or **not take** an item while satisfying a capacity or target constraint.

---

# What is Knapsack DP?

Knapsack DP is one of the most important Dynamic Programming patterns.

It is used when:

- We have a collection of items.
- Every item has a value, weight, cost, or contribution.
- We need to maximize, minimize, count, or determine feasibility under some constraint.

The fundamental decision is always:

```
Take the item

OR

Don't take the item
```

---

# Core Idea

Every item gives two choices.

```
Item i

        |
   -------------
   |           |
Take      Not Take
```

The optimal answer comes from combining the best choices.

---

# When Should You Think of Knapsack DP?

Whenever you hear:

- Capacity
- Weight
- Target Sum
- Partition
- Coin
- Subset
- Equal Sum
- Maximum Value
- Minimum Coins
- Ways to Make Target

Immediately ask:

> Can I decide to take or skip each element?

If YES, think Knapsack DP.

---

# Types of Knapsack

## 1. 0/1 Knapsack

Each item can be chosen **once**.

```
Take

OR

Skip
```

Examples

- Partition Equal Subset Sum
- Target Sum
- Ones and Zeroes

---

## 2. Unbounded Knapsack

Each item can be chosen **unlimited times**.

Examples

- Coin Change
- Perfect Squares
- Combination Sum

---

## 3. Bounded Knapsack

Each item has a limited frequency.

Less common in interviews.

---

# State Definition

The most common state is

```
dp[i][j]
```

where

```
i = first i items

j = current capacity / target
```

Meaning

```
Answer using first i items with capacity j
```

---

# Generic Thinking Process

## Step 1

Define the state.

Example

```
dp[i][w]

Maximum value using first i items with capacity w
```

---

## Step 2

Choices

```
Take

Skip
```

---

## Step 3

Transition

Combine the two choices.

---

## Step 4

Base Case

Usually

```
0 items

capacity = 0
```

---

## Step 5

Optimization

Can previous row alone solve it?

If YES

↓

1D DP

---

# Generic 0/1 Knapsack Transition

If

```
weight[i] <= capacity
```

then

```
dp[i][w]

=

max(

take,

not take

)
```

Expanded

```
dp[i][w]

=

max(

value[i] + dp[i-1][w-weight[i]],

dp[i-1][w]

)
```

---

# Generic Unbounded Transition

Difference

Take current item again.

```
dp[i][w]

=

max(

value[i] + dp[i][w-weight[i]],

dp[i-1][w]

)
```

Notice

Take uses

```
dp[i]
```

instead of

```
dp[i-1]
```

---

# Memoization Template

```java
int solve(int index, int capacity){

    if(base case)
        return answer;

    if(dp[index][capacity] != -1)
        return dp[index][capacity];

    int notTake = solve(index - 1, capacity);

    int take = 0;

    if(weight[index] <= capacity){

        take = value[index] +
               solve(index - 1,
                     capacity - weight[index]);

    }

    return dp[index][capacity] =
            Math.max(take, notTake);
}
```

---

# Tabulation Template

```java
for(int i = 1; i <= n; i++){

    for(int w = 0; w <= capacity; w++){

        // transition

    }
}
```

---

# Space Optimization

Since only the previous row is required,

```
O(n × W)
```

↓

```
O(W)
```

For **0/1 Knapsack**, iterate **capacity from right to left**.

```java
for(int item = 0; item < n; item++){

    for(int w = capacity; w >= weight[item]; w--){

        dp[w] = Math.max(
                dp[w],
                value[item] + dp[w-weight[item]]
        );
    }
}
```

---

For **Unbounded Knapsack**, iterate **left to right**.

```java
for(int item = 0; item < n; item++){

    for(int w = weight[item]; w <= capacity; w++){

        dp[w] = Math.max(
                dp[w],
                value[item] + dp[w-weight[item]]
        );
    }
}
```

---

# Pattern Recognition

Question contains

```
Subset

Target

Capacity

Weight

Coin

Partition

Take / Skip

Bag
```

↓

State

```
dp[item][capacity]
```

↓

Take

↓

Skip

↓

Memoization

↓

Tabulation

↓

Space Optimization

---

# Competitive Programming Insight

Almost every Knapsack problem can be transformed into one of these:

- Maximize value
- Minimize cost
- Count ways
- Check possibility

Recognizing which category it belongs to is the hardest part.

---

# Problem 1

## Classic 0/1 Knapsack

Difficulty

Medium

---

## Core Idea

Choose each item at most once.

---

## State

```
dp[i][w]

Maximum value
```

---

## Recurrence

```
Take

value[i] +
dp[i-1][w-weight[i]]

Not Take

dp[i-1][w]
```

Take maximum.

---

## Java Solution

```java
class Solution {

    public int knapsack(int[] weight,
                        int[] value,
                        int capacity){

        int n = weight.length;

        int[][] dp = new int[n+1][capacity+1];

        for(int i=1;i<=n;i++){

            for(int w=0;w<=capacity;w++){

                dp[i][w] = dp[i-1][w];

                if(weight[i-1] <= w){

                    dp[i][w] = Math.max(
                        dp[i][w],
                        value[i-1] +
                        dp[i-1][w-weight[i-1]]
                    );
                }
            }
        }

        return dp[n][capacity];
    }
}
```

---

### Time Complexity

```
O(n × W)
```

### Space Complexity

```
O(n × W)
```

---

### Optimization

```
O(W)
```

---

# Problem 2

## LeetCode 416 — Partition Equal Subset Sum

Difficulty

Medium

---

## Core Idea

Can we choose a subset whose sum equals

```
totalSum / 2
```

This is a feasibility version of 0/1 Knapsack.

---

## State

```
dp[i][sum]

Can we form sum using first i numbers?
```

---

## Recurrence

```
Take

OR

Skip
```

using logical OR.

---

## Java Solution

```java
class Solution {

    public boolean canPartition(int[] nums) {

        int sum = 0;

        for(int x : nums)
            sum += x;

        if(sum % 2 != 0)
            return false;

        int target = sum / 2;

        boolean[] dp = new boolean[target + 1];

        dp[0] = true;

        for(int num : nums){

            for(int s = target; s >= num; s--){

                dp[s] = dp[s] || dp[s-num];

            }
        }

        return dp[target];
    }
}
```

---

### Time Complexity

```
O(n × target)
```

### Space Complexity

```
O(target)
```

---

# Problem 3

## LeetCode 322 — Coin Change

Difficulty

Medium

---

## Core Idea

Each coin can be used unlimited times.

Find the minimum number of coins needed to form the amount.

This is an **Unbounded Knapsack** problem.

---

## State

```
dp[x]

Minimum coins needed for amount x
```

---

## Recurrence

```
dp[x]

=

min(

dp[x],

1 + dp[x-coin]

)
```

---

## Java Solution

```java
class Solution {

    public int coinChange(int[] coins, int amount) {

        int[] dp = new int[amount + 1];

        Arrays.fill(dp, amount + 1);

        dp[0] = 0;

        for(int coin : coins){

            for(int x = coin; x <= amount; x++){

                dp[x] = Math.min(
                        dp[x],
                        dp[x-coin] + 1
                );
            }
        }

        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```

---

### Time Complexity

```
O(n × amount)
```

### Space Complexity

```
O(amount)
```

---

# Common Mistakes

❌ Forgetting whether an item can be reused.

❌ Using the wrong iteration direction in 1D DP.

❌ Incorrect base case.

❌ Confusing counting, optimization, and feasibility variants.

❌ Forgetting to check capacity before taking an item.

---

# Interview Mental Checklist

- Is every item used once or multiple times?
- Is this maximizing, minimizing, counting, or feasibility?
- What does `dp[i][j]` represent?
- What are the take and skip transitions?
- Can I optimize from `O(n × W)` to `O(W)`?

---

# Pattern Summary

| Feature | Description |
|----------|-------------|
| State | `dp[item][capacity]` |
| Core Decision | Take / Not Take |
| Variants | 0/1, Unbounded, Bounded |
| Transition | Depends on reuse rule |
| Time Complexity | Usually `O(n × W)` |
| Space | `O(n × W)` → `O(W)` |
| Common Topics | Subset, Partition, Coin Change, Target Sum |

---

# Mastery Checklist

- [ ] Recognize Knapsack problems quickly.
- [ ] Distinguish between 0/1 and Unbounded Knapsack.
- [ ] Define the DP state correctly.
- [ ] Derive the take/not-take recurrence.
- [ ] Write Memoization.
- [ ] Convert to Tabulation.
- [ ] Optimize to 1D DP.
- [ ] Remember iteration direction:
  - Right → Left for **0/1 Knapsack**
  - Left → Right for **Unbounded Knapsack**

---

> **Golden Rule:** If every element presents a **take-or-skip** decision under a capacity or target constraint, think **Knapsack Dynamic Programming** first.