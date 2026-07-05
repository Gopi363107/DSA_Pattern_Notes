# 08 - Bitmask Dynamic Programming Pattern

> **Core Idea:** Represent a **set of selected elements** using bits and perform Dynamic Programming over those subsets.

---

# What is Bitmask DP?

Bitmask DP is used when:

- The number of elements is **small** (typically `N ≤ 20`).
- We need to consider **all possible subsets**.
- The DP state is a subset of elements.

Instead of storing a boolean array, we compress the state into an integer.

---

# Why Use Bitmask?

Suppose we have

```
4 cities
```

Instead of

```
Visited

[true,false,true,false]
```

store

```
1010
```

as a binary number.

This integer uniquely represents the subset.

---

# Binary Representation

Suppose

```
N = 4
```

Bit positions

```
3 2 1 0
```

Mask

```
1010
```

Means

```
Bit 3 = Selected

Bit 2 = Not Selected

Bit 1 = Selected

Bit 0 = Not Selected
```

---

# Example

People

```
0

1

2

3
```

Mask

```
1101
```

Selected

```
0

2

3
```

---

# Common Bit Operations

## Check Bit

```java
(mask & (1 << i)) != 0
```

Meaning

```
Is i selected?
```

---

## Set Bit

```java
mask | (1 << i)
```

Meaning

```
Select i.
```

---

## Remove Bit

```java
mask & ~(1 << i)
```

Meaning

```
Unselect i.
```

---

## Toggle Bit

```java
mask ^ (1 << i)
```

Meaning

```
Reverse bit.
```

---

## Count Bits

```java
Integer.bitCount(mask)
```

---

# Total Number of States

For

```
N
```

elements

Number of subsets

```
2^N
```

Example

```
N = 4

↓

16 subsets
```

---

# When Should You Think of Bitmask DP?

Whenever the problem contains

- Visit every city
- Visit every node once
- Assignment
- Matching
- Small N
- Choose subset
- TSP
- Hamiltonian
- Traveling
- Permutation with DP

Immediately ask

> Can every subset be represented as a bitmask?

If YES,

think Bitmask DP.

---

# Common State Definitions

---

## State 1

```
dp[mask]
```

Meaning

```
Answer

for subset

mask
```

---

## State 2

```
dp[mask][last]
```

Meaning

```
Answer

for subset

mask

ending at node

last
```

Very common in Traveling Salesman.

---

# Generic Thinking Process

## Step 1

Represent subset using mask.

---

## Step 2

Choose next element.

---

## Step 3

Update new mask.

---

## Step 4

Repeat until

```
All bits set.
```

---

# Generic Transition

```java
for(int next = 0; next < n; next++){

    if((mask & (1 << next)) == 0){

        int newMask = mask | (1 << next);

        // Transition
    }
}
```

---

# Memoization Template

```java
int solve(int mask, int last){

    if(mask == ALL_VISITED)
        return answer;

    if(dp[mask][last] != -1)
        return dp[mask][last];

    int ans = INF;

    for(int next = 0; next < n; next++){

        if((mask & (1 << next)) == 0){

            ans = Math.min(

                ans,

                cost[last][next]

                +

                solve(

                    mask | (1 << next),

                    next
                )
            );
        }
    }

    return dp[mask][last] = ans;
}
```

---

# Tabulation Template

```java
for(int mask = 0;
    mask < (1 << n);
    mask++){

    for(int last = 0;
        last < n;
        last++){

        if((mask & (1 << last)) == 0)
            continue;

        for(int next = 0;
            next < n;
            next++){

            if((mask & (1 << next)) == 0){

                int newMask =
                        mask

                        |

                        (1 << next);

                // Update
            }
        }
    }
}
```

---

# Pattern Recognition

Question contains

```
Subset

Visit All

Assignment

Hamiltonian

Travel

Small N

Permutation
```

↓

Bitmask

↓

DP

↓

Transition

---

# Competitive Programming Insight

Bitmask DP usually appears when

```
N ≤ 20
```

because

```
2^20

≈

1,048,576
```

which is manageable.

For larger

```
N
```

Bitmask DP is usually impossible.

---

# Problem 1

## LeetCode 847 — Shortest Path Visiting All Nodes

Difficulty

Hard

---

## Core Idea

State

```
(mask,

node)
```

Need to visit

```
Every node
```

once.

---

## State

```
dp[mask][node]
```

---

## Transition

Visit every unvisited neighbor.

---

### Time Complexity

```
O(2^N × N)
```

---

# Problem 2

## LeetCode 526 — Beautiful Arrangement

Difficulty

Medium

---

## Core Idea

Use mask to represent

```
Used numbers.
```

Position

↓

Choose unused valid number.

---

## State

```
dp[mask]
```

---

### Time Complexity

```
O(2^N × N)
```

---

# Problem 3

## LeetCode 698 — Partition to K Equal Sum Subsets

Difficulty

Medium

---

## Core Idea

Mask stores

```
Chosen elements.
```

DP tracks

```
Current subset sum.
```

---

## State

```
dp[mask]
```

---

### Time Complexity

```
O(2^N × N)
```

---

# Common Mistakes

❌ Forgetting parentheses in bit operations.

Wrong

```java
mask & 1 << i
```

Correct

```java
(mask & (1 << i))
```

---

❌ Using Bitmask DP for

```
N = 50
```

Impossible.

---

❌ Forgetting to update the new mask.

---

❌ Using recursion without memoization.

---

# Interview Mental Checklist

- Is `N ≤ 20`?
- Can a subset be represented using bits?
- Is my state `dp[mask]` or `dp[mask][last]`?
- What does each bit represent?
- How do I transition to the next subset?

---

# Pattern Summary

| Feature | Description |
|----------|-------------|
| State | `dp[mask]`, `dp[mask][last]` |
| Core Idea | DP over subsets |
| Traversal | All masks |
| Time Complexity | Usually `O(2^N × N)` |
| Space | `O(2^N × N)` |
| Common Topics | TSP, Assignment, Hamiltonian, Visit All |

---

# Mastery Checklist

- [ ] Understand binary masks.
- [ ] Learn bit operations.
- [ ] Write subset transitions.
- [ ] Solve DP with `mask`.
- [ ] Learn Traveling Salesman DP.
- [ ] Solve Visit All Nodes.
- [ ] Recognize subset DP instantly.

---

# Useful Bit Tricks

| Operation | Code |
|-----------|------|
| Check Bit | `(mask & (1<<i)) != 0` |
| Set Bit | `mask \| (1<<i)` |
| Remove Bit | `mask & ~(1<<i)` |
| Toggle Bit | `mask ^ (1<<i)` |
| Count Bits | `Integer.bitCount(mask)` |

---

# Common Applications

```
Traveling Salesman
        ↓
Visit All Nodes
        ↓
Assignment Problem
        ↓
Subset Selection
        ↓
Hamiltonian Path
        ↓
Beautiful Arrangement
        ↓
K Partition
```

---

# Final Goal

After mastering Bitmask DP, you should be able to:

- Represent subsets efficiently using binary masks.
- Design DP states involving subsets and the last visited element.
- Solve Traveling Salesman, Assignment, Hamiltonian, and subset optimization problems.
- Confidently solve Bitmask DP questions asked in Top MNCs, FinTech companies, and competitive programming.

---

> **Golden Rule:** If the problem involves a **small number of elements** and requires exploring **all subsets or visit orders**, think **Bitmask Dynamic Programming**.