# 05 - Longest Increasing Subsequence (LIS) DP Problems

> **Goal:** Master every important LIS-based Dynamic Programming pattern asked in Top MNCs, FinTech companies, coding interviews, and competitive programming.

---

# Learning Order

Do **NOT** solve these problems randomly.

Follow this progression.

```
Classic LIS
      ↓
LIS Variations
      ↓
Chain Problems
      ↓
Sorting + LIS
      ↓
Advanced Sequence DP
      ↓
Hard LIS Transformations
```

---

# LIS Family Tree

```
                    LIS DP
                      │
      ┌───────────────┼────────────────┐
      │               │                │
 Increasing      Chain Problems   Sequence DP
      │               │                │
Russian Doll   Pair Chain      Bitonic Sequence
      │               │                │
Bridges      Box Stacking    Advanced LIS
```

---

# Level 1 — Foundation (Must Solve)

These problems build the core LIS intuition.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 1 | Longest Increasing Subsequence | LeetCode 300 | Medium | Classic LIS |
| 2 | Number of Longest Increasing Subsequence | LeetCode 673 | Medium | Counting LIS |
| 3 | Longest Continuous Increasing Subsequence | LeetCode 674 | Easy | Adjacent LIS |
| 4 | Maximum Length of Pair Chain | LeetCode 646 | Medium | Chain DP |

---

# Level 2 — Chain Problems

Convert objects into LIS.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 5 | Russian Doll Envelopes | LeetCode 354 | Hard | Sorting + LIS |
| 6 | Best Team With No Conflicts | LeetCode 1626 | Medium | Sorting + LIS |
| 7 | Longest String Chain | LeetCode 1048 | Medium | Chain DP |

---

# Level 3 — Increasing / Decreasing Variants

Build sequences in different directions.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 8 | Longest Bitonic Subsequence | GFG | Medium | LIS + LDS |
| 9 | Minimum Removals to Make Mountain Array | LeetCode 1671 | Hard | LIS + LDS |
| 10 | Wiggle Subsequence | LeetCode 376 | Medium | State DP |

---

# Level 4 — Sequence Optimization

Optimization over increasing sequences.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 11 | Maximum Sum Increasing Subsequence | GFG | Medium | Weighted LIS |
| 12 | Largest Divisible Subset | LeetCode 368 | Medium | LIS Variant |
| 13 | Arithmetic Slices II | LeetCode 446 | Hard | Difference DP |

---

# Level 5 — Advanced Sorting + LIS

Frequently asked in product companies.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 14 | Building Bridges | GFG | Medium | Sorting + LIS |
| 15 | Box Stacking | GFG | Hard | 3D LIS |
| 16 | Circus Tower | CTCI | Medium | Multi-dimensional LIS |

---

# Level 6 — Advanced Sequence DP

Hard interview problems.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 17 | Longest Arithmetic Subsequence | LeetCode 1027 | Medium | Difference DP |
| 18 | Longest Fibonacci Subsequence | LeetCode 873 | Medium | Pair DP |
| 19 | Make Array Strictly Increasing | LeetCode 1187 | Hard | DP + Binary Search |
| 20 | Maximum Balanced Subsequence Sum | LeetCode 2926 | Hard | Fenwick Tree + LIS Idea |

---

# Company Favorites

## Amazon

- 300
- 673
- 354
- 376
- 368

---

## Google

- 354
- 1626
- 1187
- 873
- 1027

---

## Microsoft

- 300
- 673
- 646
- 376

---

## Meta

- 300
- 354
- 368
- 1048

---

## Apple

- 300
- 376
- 1626
- 646

---

## Uber

- 354
- 1027
- 1187

---

## FinTech Companies

Most frequently asked:

- 300
- 673
- 646
- 354
- 368
- 376

---

# Recommended Solving Order (20 Problems)

## Week 1 — Classic LIS

- [ ] LeetCode 300 Longest Increasing Subsequence
- [ ] LeetCode 673 Number of LIS
- [ ] LeetCode 674 Longest Continuous Increasing Subsequence
- [ ] LeetCode 646 Maximum Length of Pair Chain

---

## Week 2 — LIS Transformations

- [ ] LeetCode 354 Russian Doll Envelopes
- [ ] LeetCode 1626 Best Team With No Conflicts
- [ ] LeetCode 1048 Longest String Chain
- [ ] GFG Maximum Sum Increasing Subsequence
- [ ] LeetCode 368 Largest Divisible Subset

---

## Week 3 — Advanced Sequences

- [ ] GFG Longest Bitonic Subsequence
- [ ] LeetCode 1671 Minimum Mountain Removals
- [ ] LeetCode 376 Wiggle Subsequence
- [ ] LeetCode 1027 Longest Arithmetic Subsequence
- [ ] LeetCode 873 Longest Fibonacci Subsequence

---

## Week 4 — Expert

- [ ] GFG Building Bridges
- [ ] GFG Box Stacking
- [ ] LeetCode 1187 Make Array Strictly Increasing
- [ ] LeetCode 2926 Maximum Balanced Subsequence Sum

---

# Pattern Recognition Cheat Sheet

| If the question says... | Think... |
|--------------------------|----------|
| Increasing sequence | LIS |
| Longest chain | LIS |
| Compatible pairs | Sorting + LIS |
| Envelope nesting | Sorting + LIS |
| Bridges | Sorting + LIS |
| Mountain array | LIS + LDS |
| Divisible subset | LIS Variant |
| Maximum increasing sum | Weighted LIS |
| Arithmetic sequence | Difference DP |

---

# Standard State Definitions

## Classic LIS

```
dp[i]
```

Meaning:

```
Length of LIS ending at index i
```

---

## Counting LIS

```
length[i]

count[i]
```

Meaning:

```
Longest length

and

number of LIS

ending at i
```

---

## Weighted LIS

```
dp[i]
```

Meaning:

```
Maximum sum ending at index i
```

---

## Bitonic

```
lis[i]

lds[i]
```

Meaning:

```
Longest Increasing ending at i

+

Longest Decreasing starting at i
```

---

# Common Transitions

## Classic LIS

```
if(nums[j] < nums[i])

dp[i] = max(
dp[i],
dp[j] + 1
)
```

---

## Counting LIS

Update

```
length

and

count
```

simultaneously.

---

## Maximum Sum Increasing Subsequence

```
dp[i]

=

max(

dp[i],

dp[j] + nums[i]

)
```

---

## Bitonic

```
Answer

=

LIS

+

LDS

-

1
```

---

# Time Complexity Guide

| Problem Type | Complexity |
|--------------|-----------|
| Classic DP | `O(n²)` |
| Binary Search LIS | `O(n log n)` |
| Counting LIS | `O(n²)` |
| Russian Doll | `O(n log n)` |
| Bitonic | `O(n²)` |
| Longest Arithmetic Subsequence | `O(n²)` |

---

# Binary Search Optimization

Binary Search can optimize only problems where we need:

- Length of LIS
- Longest increasing chain after sorting

It **cannot** directly solve:

- Counting LIS
- Maximum Sum LIS
- Bitonic Sequence
- Divisible Subset

---

# Interview Tips

Whenever you encounter a sequence problem, ask:

1. Is order important?
2. Do elements need to be contiguous?
3. Can each previous element extend the current answer?
4. Can sorting transform the problem into LIS?
5. Is Binary Search optimization applicable?

---

# Mastery Checklist

## Beginner

- [ ] Solve Classic LIS.
- [ ] Understand subsequence vs subarray.
- [ ] Implement the `O(n²)` solution.

---

## Intermediate

- [ ] Learn the `O(n log n)` Binary Search solution.
- [ ] Solve Counting LIS.
- [ ] Solve Weighted LIS.
- [ ] Solve Russian Doll Envelopes.

---

## Advanced

- [ ] Solve Bitonic Sequence.
- [ ] Solve Longest Arithmetic Subsequence.
- [ ] Solve Box Stacking.
- [ ] Recognize hidden LIS transformations.

---

# Common Transformations

Many difficult problems become LIS after preprocessing.

Examples:

```
Sort Envelopes
        ↓
LIS

Sort Bridges
        ↓
LIS

Sort Pairs
        ↓
LIS

Sort Boxes
        ↓
LIS

Sort Players
        ↓
LIS
```

---

# Final Goal

After completing this roadmap, you should be able to:

- Instantly recognize LIS-based problems.
- Decide whether `O(n²)` DP or `O(n log n)` Binary Search is appropriate.
- Transform chain and sorting problems into LIS.
- Solve weighted, counting, and bitonic sequence variants.
- Confidently solve LIS questions commonly asked in Top MNCs, FinTech companies, and coding interviews.