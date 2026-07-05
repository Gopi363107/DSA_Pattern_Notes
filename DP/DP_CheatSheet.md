# Dynamic Programming Cheat Sheet

> A one-page revision guide to quickly recognize, design, and solve Dynamic Programming problems during interviews and contests.
---
# DP Problem Solving Flow

```
Recursive Problem?
        │
        ▼
Overlapping Subproblems?
        │
        ▼
Optimal Substructure?
        │
        ▼
Define State
        │
        ▼
Write Recurrence
        │
        ▼
Memoization
        │
        ▼
Tabulation
        │
        ▼
Space Optimization
```
---
# DP Design Template
## Step 1 — Define State
Ask:
> What changes during recursion?
Examples
```
dp[i]

dp[i][j]

dp[index][target]

dp[mask]

dp[node]
```

---

## Step 2 — Transition

Ask

```
Where can I come from?

OR

What choices do I have?
```

---

## Step 3 — Base Case

Usually

```
No elements

Target = 0

Leaf node

Single interval

Destination reached
```

---

## Step 4 — Compute Order

Memoization

↓

Recursive

Tabulation

↓

Bottom-up

---

## Step 5 — Space Optimization

If current state depends only on

```
Previous Row

Previous Column

Previous State
```

↓

Optimize memory.

---

# Pattern Recognition Table

| If Question Contains... | Pattern |
|--------------------------|---------|
| Fibonacci | 1D DP |
| Count Ways | 1D DP |
| Maximum Profit | 1D DP |
| Grid | Grid DP |
| Matrix | Grid DP |
| Obstacles | Grid DP |
| Target Sum | Knapsack DP |
| Subset | Knapsack DP |
| Partition | Knapsack DP |
| LCS | String DP |
| Two Strings | LCS DP |
| Edit Operations | LCS DP |
| Increasing Sequence | LIS DP |
| Envelope | LIS DP |
| Chain | LIS DP |
| Merge | Interval DP |
| Burst | Interval DP |
| Cut | Interval DP |
| Palindrome | Interval DP |
| Tree | Tree DP |
| Subtree | Tree DP |
| Path Sum | Tree DP |
| Visit All | Bitmask DP |
| Assignment | Bitmask DP |
| Small N (≤20) | Bitmask DP |

---

# DP State Cheat Sheet

| Pattern | State |
|----------|-------|
| 1D DP | `dp[i]` |
| Grid DP | `dp[row][col]` |
| Knapsack | `dp[index][target]` |
| LCS | `dp[i][j]` |
| LIS | `dp[i]` |
| Interval DP | `dp[left][right]` |
| Tree DP | `dp[node]` / `dp[node][2]` |
| Bitmask DP | `dp[mask]` / `dp[mask][last]` |

---

# Standard Recurrences

## 1D DP

```text
dp[i]

=

best(

dp[i-1],

dp[i-2]

...)
```

---

## Grid DP

```text
dp[i][j]

=

grid[i][j]

+

best(

Top,

Left
)
```

---

## Knapsack

```text
Take

OR

Not Take
```

```text
dp[i][w]

=

max(

Not Take,

Take
)
```

---

## LCS

```text
If Equal

↓

1 + Diagonal

Else

↓

max(

Top,

Left
)
```

---

## LIS

```text
If

nums[j] < nums[i]

↓

dp[i]

=

max(

dp[i],

dp[j] + 1
)
```

---

## Interval DP

```text
Try every split

k

between

i

and

j
```

---

## Tree DP

```text
Combine

Children

↓

Parent
```

---

## Bitmask DP

```text
Choose

Next Unvisited

↓

Update Mask
```

---

# Time Complexity Cheat Sheet

| Pattern | Time |
|----------|------|
| Fibonacci | O(n) |
| 1D DP | O(n) |
| Grid DP | O(n × m) |
| 0/1 Knapsack | O(n × target) |
| Unbounded Knapsack | O(n × target) |
| LCS | O(n × m) |
| Edit Distance | O(n × m) |
| LIS (DP) | O(n²) |
| LIS (Binary Search) | O(n log n) |
| Interval DP | O(n³) |
| Tree DP | O(n) |
| Bitmask DP | O(2ⁿ × n) |
| TSP | O(2ⁿ × n²) |

---

# Space Complexity Cheat Sheet

| Pattern | Space |
|----------|-------|
| 1D DP | O(n) |
| Space Optimized 1D | O(1) |
| Grid DP | O(n × m) |
| Optimized Grid | O(m) |
| Knapsack | O(target) |
| LCS | O(n × m) |
| Optimized LCS | O(m) |
| Interval DP | O(n²) |
| Tree DP | O(h) recursion |
| Bitmask DP | O(2ⁿ × n) |

---

# Memoization vs Tabulation

| Memoization | Tabulation |
|--------------|------------|
| Top-down | Bottom-up |
| Recursive | Iterative |
| Easy to write | Faster execution |
| Uses recursion stack | No recursion stack |
| Solves only needed states | Computes all states |

---

# Space Optimization Checklist

Can I remove a dimension?

Depends only on

```
Previous Row
```

↓

Use rolling array.

Depends only on

```
Previous State
```

↓

Use variables.

---

# Binary Search Optimization

Applicable in

✅ LIS

✅ Russian Doll Envelopes

Not applicable in

❌ LCS

❌ Knapsack

❌ Interval DP

❌ Tree DP

---

# DP Pattern Decision Tree

```
Start
 │
 ├── One Array?
 │      │
 │      ▼
 │    1D DP
 │
 ├── Grid?
 │      │
 │      ▼
 │    Grid DP
 │
 ├── Target / Capacity?
 │      │
 │      ▼
 │   Knapsack DP
 │
 ├── Two Strings?
 │      │
 │      ▼
 │    LCS DP
 │
 ├── Increasing Sequence?
 │      │
 │      ▼
 │     LIS DP
 │
 ├── Interval / Substring?
 │      │
 │      ▼
 │   Interval DP
 │
 ├── Tree?
 │      │
 │      ▼
 │    Tree DP
 │
 └── Small N + Subsets?
        │
        ▼
    Bitmask DP
```

---

# Interview Checklist

Before coding, ask yourself:

- [ ] What is my DP state?
- [ ] What are the choices?
- [ ] What is the recurrence?
- [ ] What is the base case?
- [ ] Memoization or Tabulation?
- [ ] Can I optimize space?
- [ ] Time complexity?
- [ ] Space complexity?

---

# Common Mistakes

❌ Wrong DP state.

❌ Incorrect base case.

❌ Forgetting memoization.

❌ Wrong traversal order.

❌ Array index out of bounds.

❌ Integer overflow.

❌ Using recursion without caching.

❌ Missing space optimization opportunities.

---

# Top Interview DP Problems

### 1D DP

- Fibonacci
- Climbing Stairs
- House Robber
- Coin Change

### Grid DP

- Unique Paths
- Minimum Path Sum
- Cherry Pickup II

### Knapsack DP

- 0/1 Knapsack
- Partition Equal Subset Sum
- Target Sum

### LCS DP

- Longest Common Subsequence
- Edit Distance
- Distinct Subsequences

### LIS DP

- Longest Increasing Subsequence
- Russian Doll Envelopes
- Number of LIS

### Interval DP

- Burst Balloons
- Minimum Cost to Cut a Stick
- Strange Printer

### Tree DP

- House Robber III
- Diameter of Binary Tree
- Binary Tree Maximum Path Sum

### Bitmask DP

- Beautiful Arrangement
- Shortest Path Visiting All Nodes
- Smallest Sufficient Team

---

# Ultimate DP Learning Order

```
Introduction to DP
        ↓
1D DP
        ↓
Grid DP
        ↓
Knapsack DP
        ↓
LCS / String DP
        ↓
LIS DP
        ↓
Interval DP
        ↓
Tree DP
        ↓
Bitmask DP
        ↓
Digit DP
        ↓
Probability DP
        ↓
Game DP
        ↓
DP Optimization
```

---

# Golden Rules

1. **State first, code later.**
2. **Every DP starts as recursion.**
3. **Memoization before Tabulation.**
4. **Optimize space only after the correct solution works.**
5. **Recognize the pattern before thinking about implementation.**
6. **Understand the recurrence instead of memorizing code.**
7. **Practice problems in increasing difficulty, not randomly.**

---

# DP Master Formula

```
Identify Pattern
        ↓
Define State
        ↓
Write Recurrence
        ↓
Handle Base Cases
        ↓
Memoization
        ↓
Tabulation
        ↓
Space Optimization
        ↓
Analyze TC & SC
        ↓
Practice Similar Problems
```

---

# Final Goal

After mastering these patterns, you should be able to:

- Instantly identify the correct DP pattern.
- Derive states and recurrences without memorization.
- Convert recursion to memoization and tabulation.
- Optimize both time and space where applicable.
- Solve Dynamic Programming problems confidently in coding interviews, competitive programming, and Top MNC/FinTech assessments.