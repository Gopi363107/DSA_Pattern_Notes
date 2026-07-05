# 03 - Knapsack Dynamic Programming Problems

> **Goal:** Master every important Knapsack DP pattern asked in Top MNCs, FinTech companies, coding interviews, and competitive programming.

---

# Learning Order

Do **NOT** solve problems randomly.

Follow this progression.

```
0/1 Knapsack
        ↓
Subset Sum
        ↓
Partition DP
        ↓
Target Sum
        ↓
Counting DP
        ↓
Unbounded Knapsack
        ↓
Coin Change
        ↓
Advanced Knapsack
```

---

# Knapsack Family Tree

```
                    Knapsack DP
                         │
         ┌───────────────┴───────────────┐
         │                               │
     0/1 Knapsack                 Unbounded Knapsack
         │                               │
  Subset / Partition               Coin Problems
         │                               │
  Target Sum, Ones & Zeroes      Perfect Squares
```

---

# Level 1 — Foundation (0/1 Knapsack)

Learn the basic **Take / Not Take** pattern.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 1 | 0/1 Knapsack | GFG | Medium | Classic Knapsack |
| 2 | Subset Sum Problem | GFG | Medium | Feasibility |
| 3 | Equal Sum Partition | GFG | Medium | Partition |
| 4 | Partition Equal Subset Sum | LeetCode 416 | Medium | 0/1 Knapsack |
| 5 | Last Stone Weight II | LeetCode 1049 | Medium | Partition |

---

# Level 2 — Target Sum Problems

State is based on **target value**.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 6 | Target Sum | LeetCode 494 | Medium | Subset Transformation |
| 7 | Find Ways to Reach Target | GFG | Medium | Counting |
| 8 | Number of Dice Rolls With Target Sum | LeetCode 1155 | Medium | Counting DP |

---

# Level 3 — Counting Knapsack

Count the number of valid solutions.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 9 | Coin Change II | LeetCode 518 | Medium | Count Ways |
| 10 | Combination Sum IV | LeetCode 377 | Medium | Ordered Counting |
| 11 | Profitable Schemes | LeetCode 879 | Hard | Multi-dimensional DP |

---

# Level 4 — Unbounded Knapsack

Items can be chosen unlimited times.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 12 | Coin Change | LeetCode 322 | Medium | Minimum Coins |
| 13 | Perfect Squares | LeetCode 279 | Medium | Minimum Count |
| 14 | Unbounded Knapsack | GFG | Medium | Classic |
| 15 | Minimum Cost For Tickets | LeetCode 983 | Medium | Cost Optimization |

---

# Level 5 — String / Binary Knapsack

Knapsack on non-numeric states.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 16 | Ones and Zeroes | LeetCode 474 | Medium | 2D Capacity |
| 17 | Form Largest Integer With Digits | LeetCode 1449 | Hard | Knapsack Construction |

---

# Level 6 — Advanced Knapsack

Frequently asked in top product companies.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 18 | Tallest Billboard | LeetCode 956 | Hard | Difference DP |
| 19 | Profitable Schemes | LeetCode 879 | Hard | Multi-State DP |
| 20 | Reduce Dishes | LeetCode 1402 | Hard | Decision DP |
| 21 | Shopping Offers | LeetCode 638 | Medium | State Compression |
| 22 | Minimum Cost to Merge Stones* | LeetCode 1000 | Hard | Interval DP |

> **Note:** Merge Stones belongs to **Interval DP**, but it shares optimization ideas with Knapsack.

---

# Company Favorites

## Amazon

- 416
- 322
- 518
- 983
- 474

---

## Google

- 879
- 956
- 1449
- 494

---

## Microsoft

- 416
- 322
- 279
- 518

---

## Meta

- 494
- 474
- 322
- 416

---

## Apple

- 322
- 416
- 983
- 279

---

## Uber

- 879
- 956
- 518

---

## FinTech Companies

Most frequently asked:

- 416
- 494
- 322
- 518
- 279
- 1049

---

# Recommended Solving Order (22 Problems)

## Week 1 — Basic 0/1 Knapsack

- [ ] GFG 0/1 Knapsack
- [ ] GFG Subset Sum
- [ ] GFG Equal Sum Partition
- [ ] LeetCode 416 Partition Equal Subset Sum
- [ ] LeetCode 1049 Last Stone Weight II

---

## Week 2 — Target & Counting

- [ ] LeetCode 494 Target Sum
- [ ] GFG Find Ways to Reach Target
- [ ] LeetCode 1155 Dice Rolls With Target Sum
- [ ] LeetCode 518 Coin Change II
- [ ] LeetCode 377 Combination Sum IV

---

## Week 3 — Unbounded Knapsack

- [ ] LeetCode 322 Coin Change
- [ ] LeetCode 279 Perfect Squares
- [ ] GFG Unbounded Knapsack
- [ ] LeetCode 983 Minimum Cost For Tickets
- [ ] LeetCode 474 Ones and Zeroes

---

## Week 4 — Advanced

- [ ] LeetCode 879 Profitable Schemes
- [ ] LeetCode 956 Tallest Billboard
- [ ] LeetCode 638 Shopping Offers
- [ ] LeetCode 1449 Form Largest Integer With Digits

---

# Pattern Recognition Cheat Sheet

| If the question says... | Think... |
|--------------------------|----------|
| Capacity | Knapsack |
| Weight | 0/1 Knapsack |
| Target Sum | Subset DP |
| Equal Partition | Partition DP |
| Coin | Unbounded Knapsack |
| Unlimited reuse | Unbounded DP |
| Take or Skip | 0/1 Knapsack |
| Number of ways | Counting DP |
| Minimum coins | Optimization DP |

---

# State Definitions

## 0/1 Knapsack

```
dp[i][w]
```

Meaning:

```
Maximum value using first i items with capacity w
```

---

## Subset Sum

```
dp[i][sum]
```

Meaning:

```
Can first i items make sum?
```

---

## Coin Change

```
dp[amount]
```

Meaning:

```
Minimum coins needed to make amount
```

---

## Coin Change II

```
dp[amount]
```

Meaning:

```
Number of ways to make amount
```

---

# Common Transitions

## 0/1 Knapsack

```
Take

OR

Skip
```

```
dp[i][w] =
max(
take,
skip
)
```

---

## Feasibility

```
dp[i][sum] =
take
OR
skip
```

---

## Counting

```
dp[target] += dp[target-item]
```

---

## Minimum

```
dp[target] =
min(
current,
1 + previous
)
```

---

# Space Optimization Rules

## 0/1 Knapsack

Traverse capacity:

```
Right → Left
```

```java
for (int w = capacity; w >= weight; w--)
```

Reason:

- Prevents using the same item more than once.

---

## Unbounded Knapsack

Traverse capacity:

```
Left → Right
```

```java
for (int w = weight; w <= capacity; w++)
```

Reason:

- Allows reusing the current item multiple times.

---

# Interview Tips

Whenever you encounter a problem involving subsets or targets, ask:

1. Is each item used once or multiple times?
2. Is this a maximize, minimize, count, or feasibility problem?
3. What does my DP state represent?
4. What are the take and skip transitions?
5. Can I reduce the DP table to one dimension?

---

# Mastery Checklist

## Beginner

- [ ] Solve Classic 0/1 Knapsack.
- [ ] Solve Subset Sum.
- [ ] Solve Partition Equal Subset Sum.

---

## Intermediate

- [ ] Solve Target Sum.
- [ ] Solve Coin Change.
- [ ] Solve Coin Change II.
- [ ] Optimize all solutions to 1D DP.

---

## Advanced

- [ ] Recognize 0/1 vs Unbounded immediately.
- [ ] Solve multi-dimensional Knapsack.
- [ ] Handle counting, optimization, and feasibility variants.
- [ ] Solve hard Knapsack problems within interview time.

---

# Final Goal

After completing this roadmap, you should be able to:

- Instantly recognize Knapsack-based problems.
- Correctly classify them as **0/1**, **Unbounded**, **Counting**, or **Partition**.
- Derive the DP state and transition naturally.
- Apply proper space optimization techniques.
- Confidently solve most Knapsack questions asked in Top MNCs, FinTech companies, and coding interviews.