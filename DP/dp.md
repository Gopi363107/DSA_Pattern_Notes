# Dynamic Programming (DP) - Complete Guide

> **Goal:** Understand Dynamic Programming from first principles rather than memorizing solutions.

---

# What is Dynamic Programming?

Dynamic Programming (DP) is an optimization technique used to solve problems that can be broken down into **smaller overlapping subproblems**.

Instead of solving the same subproblem multiple times, DP solves it **once**, stores the answer, and reuses it whenever needed.

This avoids unnecessary computation and significantly improves performance.

---

# Why Do We Need Dynamic Programming?

Consider calculating the Fibonacci number.

```
fib(5)
├── fib(4)
│   ├── fib(3)
│   │   ├── fib(2)
│   │   └── fib(1)
│   └── fib(2)
└── fib(3)
    ├── fib(2)
    └── fib(1)
```

Notice that:

* `fib(3)` is computed multiple times.
* `fib(2)` is computed even more times.

This repeated work causes exponential time complexity.

Dynamic Programming stores the answer after computing it once.

```
fib(3)

Computed once
↓

Store result

↓

Reuse whenever needed
```

This reduces the complexity dramatically.

---

# When Should You Think About DP?

Ask yourself these questions:

### 1. Can the problem be divided into smaller versions of itself?

Example:

```
Minimum cost to reach stair 10

↓

Depends on

Minimum cost to reach stair 9

Minimum cost to reach stair 8
```

---

### 2. Are the same subproblems solved repeatedly?

If yes, DP is a strong candidate.

---

### 3. Does the answer depend on previous answers?

Examples:

* Fibonacci
* Climbing Stairs
* House Robber
* Longest Common Subsequence
* Knapsack

---

# Two Important Properties of DP

## 1. Overlapping Subproblems

The same subproblem appears many times.

Example:

```
fib(5)

↓

fib(3)

↓

Needed again later
```

Instead of recomputing, store the answer.

---

## 2. Optimal Substructure

The optimal solution can be built from optimal solutions of smaller subproblems.

Example:

```
Shortest Path

A → B → C

Best(A → C)

=

Best(A → B)

+

Best(B → C)
```

---

# The DP Thought Process

Every DP problem follows the same journey.

```
Problem

↓

Identify the state

↓

Find the recurrence

↓

Recursive solution

↓

Memoization

↓

Tabulation

↓

Space Optimization
```

Never jump directly to tabulation.

Always understand the recurrence first.

---

# Step 1 — Understand the Problem

Ask:

* What do I need to compute?
* What decisions can I make?
* What smaller problem helps solve the current problem?

Example:

```
Climbing Stairs

Need ways to reach stair n

↓

To reach n

You come from

n-1

or

n-2
```

---

# Step 2 — Define the State

The **state** represents the information needed to solve a subproblem.

Examples:

```
dp[i]

Meaning:

Answer for index i
```

```
dp[i][j]

Meaning:

Answer using i items and capacity j
```

```
dp[row][col]

Meaning:

Answer for that cell
```

A good state captures everything needed to compute the answer.

---

# Step 3 — Find the Recurrence Relation

The recurrence explains how the current answer depends on previous answers.

General form:

```
Current Answer

=

Function(previous answers)
```

Example:

Fibonacci

```
F(n)

=

F(n-1)

+

F(n-2)
```

Climbing Stairs

```
Ways(n)

=

Ways(n-1)

+

Ways(n-2)
```

House Robber

```
dp[i]

=

max(

Take current house,

Skip current house

)
```

The recurrence is the heart of every DP problem.

---

# Step 4 — Write the Recursive Solution

Start with recursion because it mirrors the recurrence directly.

General structure:

```
Solve(state)

↓

If base case

Return answer

↓

Compute using recurrence

↓

Return answer
```

Example:

```
Solve(n)

=

Solve(n-1)

+

Solve(n-2)
```

This version is usually simple but inefficient due to repeated work.

---

# Step 5 — Memoization (Top-Down DP)

Memoization stores computed answers so each state is solved only once.

Workflow:

```
Solve(state)

↓

Already computed?

↓

Yes

Return stored answer

↓

No

Compute

↓

Store

↓

Return
```

Advantages:

* Easy to convert from recursion.
* Only computes states that are actually needed.

Complexity:

```
Time

≈ Number of states

×

Transition cost
```

---

# Step 6 — Tabulation (Bottom-Up DP)

Instead of recursion, compute answers from the smallest state upward.

Workflow:

```
Base Case

↓

Small Problems

↓

Medium Problems

↓

Original Problem
```

Example:

```
dp[0]

↓

dp[1]

↓

dp[2]

↓

...

↓

dp[n]
```

Advantages:

* No recursion overhead.
* No stack overflow.
* Usually preferred in interviews.

---

# Step 7 — Space Optimization

Many DP problems only require a few previous states.

Instead of storing the entire DP table:

```
dp[0]

dp[1]

dp[2]

...

dp[n]
```

Store only the values that are still needed.

Example:

Fibonacci

Instead of:

```
0 1 1 2 3 5 8
```

Store:

```
prev2

prev1

current
```

Memory reduces from:

```
O(n)

↓

O(1)
```

Only optimize space after the tabulation solution is correct.

---

# The Complete DP Workflow

```
Problem

↓

State

↓

Recurrence

↓

Recursive Solution

↓

Memoization

↓

Tabulation

↓

Space Optimization
```

This is the recommended order for learning and solving DP problems.

---

# General DP Template

## Step 1

Understand the problem.

---

## Step 2

Define the state.

```
What does dp[...] represent?
```

---

## Step 3

Write the recurrence.

```
Current answer

=

Function(previous answers)
```

---

## Step 4

Identify the base cases.

---

## Step 5

Implement recursion.

---

## Step 6

Add memoization.

---

## Step 7

Convert to tabulation.

---

## Step 8

Optimize space if possible.

---

# Time Complexity Rule

A useful mental model:

```
Time Complexity

=

(Number of States)

×

(Work per State)
```

Examples:

| States | Work per State | Complexity |
| ------ | -------------- | ---------- |
| n      | O(1)           | O(n)       |
| n²     | O(1)           | O(n²)      |
| n²     | O(n)           | O(n³)      |

---

# Common DP Patterns

## 1. Linear / 1D DP

Examples:

* Fibonacci
* Climbing Stairs
* House Robber
* Min Cost Climbing Stairs
* Decode Ways

---

## 2. Grid DP

Examples:

* Unique Paths
* Minimum Path Sum
* Triangle

---

## 3. Knapsack DP

Examples:

* 0/1 Knapsack
* Partition Equal Subset Sum
* Target Sum

---

## 4. String DP

Examples:

* Longest Common Subsequence
* Edit Distance
* Distinct Subsequences

---

## 5. Interval DP

Examples:

* Burst Balloons
* Matrix Chain Multiplication

---

## 6. Tree DP

Examples:

* House Robber III
* Diameter-based DP problems

---

## 7. Bitmask DP

Examples:

* Traveling Salesman
* Assignment Problems

---

# Common Mistakes

* Jumping directly to DP without understanding the recurrence.
* Choosing an incorrect state definition.
* Forgetting base cases.
* Filling the DP table in the wrong order.
* Performing space optimization before verifying tabulation.
* Memorizing solutions instead of understanding the transition.

---

# DP Problem-Solving Checklist

Before coding, answer these questions:

* What is the state?
* What decision is made at each step?
* What is the recurrence?
* What are the base cases?
* What is the recursive solution?
* Can I add memoization?
* Can I convert it to tabulation?
* Can I optimize space?

If you can answer these questions confidently, you can solve most Dynamic Programming problems systematically instead of relying on memorization.
