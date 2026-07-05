# 08 - Bitmask Dynamic Programming Problems

> **Goal:** Master every important Bitmask DP pattern asked in Top MNCs, FinTech companies, coding interviews, and competitive programming.

---

# Learning Order

Do **NOT** solve these problems randomly.

Follow this progression.

```
Basic Bitmask
       ↓
Subset DP
       ↓
Assignment DP
       ↓
Traveling Salesman DP
       ↓
Advanced State Compression
       ↓
Hard Bitmask DP
```

---

# Bitmask DP Family Tree

```
                  Bitmask DP
                       │
      ┌────────────────┼────────────────┐
      │                │                │
   Subset DP      Assignment DP      TSP DP
      │                │                │
 Partition      Job Assignment     Visit All Nodes
      │                │                │
State Compression   Matching     Hamiltonian Path
```

---

# Level 1 — Foundation (Must Solve)

Learn subset representation and simple transitions.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 1 | Beautiful Arrangement | LeetCode 526 | Medium | Basic Bitmask DP |
| 2 | Can I Win | LeetCode 464 | Medium | Bitmask + Minimax |
| 3 | Partition to K Equal Sum Subsets | LeetCode 698 | Medium | Subset DP |
| 4 | Matchsticks to Square | LeetCode 473 | Medium | Subset DP |

---

# Level 2 — Assignment DP

Assign one object to another.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 5 | Campus Bikes II | LeetCode 1066 | Medium | Assignment DP |
| 6 | Maximum Compatibility Score Sum | LeetCode 1947 | Medium | Assignment DP |
| 7 | Assign Cookies to Children* | Custom / CP | Medium | Assignment DP |

> **Note:** Classical Assignment Problem is commonly found on CSES, AtCoder, and Codeforces.

---

# Level 3 — Traveling Salesman (TSP)

Visit every node exactly once.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 8 | Shortest Path Visiting All Nodes | LeetCode 847 | Hard | State Compression |
| 9 | Traveling Salesman Problem | CSES / GFG | Hard | TSP DP |
| 10 | Hamiltonian Flights | CSES | Hard | Hamiltonian DP |

---

# Level 4 — Subset Optimization

Optimize over subsets.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 11 | Parallel Courses II | LeetCode 1494 | Hard | Subset Transition |
| 12 | Stickers to Spell Word | LeetCode 691 | Hard | State Compression |
| 13 | Minimum Number of Work Sessions | LeetCode 1986 | Medium | Bitmask + DP |

---

# Level 5 — Advanced State Compression

Compress large state spaces.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 14 | Smallest Sufficient Team | LeetCode 1125 | Hard | Skill Mask |
| 15 | Number of Squareful Arrays | LeetCode 996 | Hard | Permutation DP |
| 16 | Maximum Students Taking Exam | LeetCode 1349 | Hard | Row Bitmask DP |

---

# Level 6 — Expert Bitmask DP

Frequently asked in top product companies.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 17 | Number of Ways to Wear Different Hats | LeetCode 1434 | Hard | DP on Masks |
| 18 | Shortest Superstring | LeetCode 943 | Hard | TSP Variant |
| 19 | Minimum XOR Sum of Two Arrays | LeetCode 1879 | Hard | Assignment DP |
| 20 | Count Special Integers | LeetCode 2376 | Hard | Digit DP + Bitmask |

---

# Company Favorites

## Amazon

- 698
- 847
- 526
- 1986

---

## Google

- 943
- 1125
- 1879
- 1494

---

## Microsoft

- 847
- 698
- 1066

---

## Meta

- 1125
- 691
- 847

---

## Apple

- 1947
- 1986
- 526

---

## Uber

- 943
- 1494
- 1879

---

## FinTech Companies

Most frequently asked:

- 698
- 526
- 847
- 1066
- 1986

---

# Recommended Solving Order (20 Problems)

## Week 1 — Fundamentals

- [ ] LeetCode 526 Beautiful Arrangement
- [ ] LeetCode 464 Can I Win
- [ ] LeetCode 698 Partition to K Equal Sum Subsets
- [ ] LeetCode 473 Matchsticks to Square

---

## Week 2 — Assignment DP

- [ ] LeetCode 1066 Campus Bikes II
- [ ] LeetCode 1947 Maximum Compatibility Score Sum
- [ ] Classical Assignment Problem (CSES / GFG)
- [ ] LeetCode 1986 Minimum Work Sessions

---

## Week 3 — Traveling Salesman

- [ ] LeetCode 847 Shortest Path Visiting All Nodes
- [ ] Traveling Salesman Problem
- [ ] CSES Hamiltonian Flights
- [ ] LeetCode 691 Stickers to Spell Word

---

## Week 4 — Advanced

- [ ] LeetCode 1125 Smallest Sufficient Team
- [ ] LeetCode 996 Number of Squareful Arrays
- [ ] LeetCode 1349 Maximum Students Taking Exam
- [ ] LeetCode 1434 Number of Ways to Wear Different Hats
- [ ] LeetCode 943 Shortest Superstring
- [ ] LeetCode 1879 Minimum XOR Sum

---

# Pattern Recognition Cheat Sheet

| If the question says... | Think... |
|--------------------------|----------|
| Small `N` (≤20) | Bitmask DP |
| Visit all cities | TSP |
| Visit every node once | State Compression |
| Assignment | Assignment DP |
| Choose subset | Subset DP |
| Skills | Bitmask |
| Matching | Assignment DP |
| Hamiltonian | Bitmask DP |
| Permutation DP | `dp[mask][last]` |

---

# Standard State Definitions

## Subset DP

```
dp[mask]
```

Meaning

```
Best answer

for subset

mask
```

---

## Traveling Salesman

```
dp[mask][last]
```

Meaning

```
Minimum cost

after visiting

mask

ending at

last
```

---

## Assignment DP

```
dp[mask]
```

Meaning

```
Best assignment

for selected jobs
```

---

# Common Transitions

## Add New Element

```java
newMask = mask | (1 << next);
```

---

## Check Availability

```java
(mask & (1 << next)) == 0
```

---

## Iterate All Masks

```java
for(mask = 0; mask < (1 << n); mask++)
```

---

## Iterate Set Bits

```java
for(int bit = mask;
    bit > 0;
    bit &= (bit - 1))
```

---

# Time Complexity Guide

| Pattern | Complexity |
|----------|-----------|
| Subset DP | `O(2^N × N)` |
| TSP DP | `O(2^N × N²)` |
| Assignment DP | `O(2^N × N)` |
| State Compression | `O(2^N × N)` |
| Row Bitmask DP | Depends on rows × masks |

---

# Bit Tricks to Remember

| Operation | Code |
|-----------|------|
| Check | `(mask & (1<<i)) != 0` |
| Set | `mask \| (1<<i)` |
| Remove | `mask & ~(1<<i)` |
| Toggle | `mask ^ (1<<i)` |
| Count Bits | `Integer.bitCount(mask)` |
| Lowest Set Bit | `mask & -mask` |

---

# Interview Tips

Whenever you encounter a problem, ask:

1. Is `N ≤ 20`?
2. Can every subset be represented as a bitmask?
3. Is my DP state `dp[mask]` or `dp[mask][last]`?
4. Am I exploring subsets or permutations?
5. Can I compress the state to reduce complexity?

---

# Mastery Checklist

## Beginner

- [ ] Learn binary representation.
- [ ] Master bit operations.
- [ ] Solve Beautiful Arrangement.
- [ ] Solve Partition to K Equal Sum Subsets.

---

## Intermediate

- [ ] Solve Assignment DP.
- [ ] Solve Campus Bikes II.
- [ ] Solve Traveling Salesman.

---

## Advanced

- [ ] Solve Shortest Superstring.
- [ ] Solve Smallest Sufficient Team.
- [ ] Solve Maximum Students Taking Exam.
- [ ] Recognize Bitmask DP immediately.

---

# Common Transformations

Many hard problems become Bitmask DP after compressing the state.

```
Assignment
      ↓
Bitmask DP

Traveling Salesman
      ↓
dp[mask][last]

Visit Every Node
      ↓
State Compression

Skill Matching
      ↓
Skill Mask

Subset Selection
      ↓
dp[mask]

Permutation
      ↓
dp[mask][last]
```

---

# Final Goal

After completing this roadmap, you should be able to:

- Instantly recognize Bitmask DP problems.
- Represent subsets efficiently using bitmasks.
- Design subset and state-compressed DP solutions.
- Solve Traveling Salesman, Assignment, Hamiltonian, and subset optimization problems.
- Confidently solve Bitmask DP questions asked in Top MNCs, FinTech companies, and competitive programming.

---

# Ultimate Bitmask DP Roadmap

```
526  → Beautiful Arrangement
          ↓
698  → Partition to K Equal Sum Subsets
          ↓
1066 → Campus Bikes II
          ↓
847  → Shortest Path Visiting All Nodes
          ↓
1494 → Parallel Courses II
          ↓
1125 → Smallest Sufficient Team
          ↓
943  → Shortest Superstring
          ↓
1879 → Minimum XOR Sum
```

> **Golden Rule:** If the problem has a **small number of elements** and asks you to optimize over **subsets, assignments, or visit orders**, think **Bitmask Dynamic Programming**.