# 09 - String Dynamic Programming Problems

> **Goal:** Master every important String DP pattern asked in Top MNCs, FinTech companies, coding interviews, and competitive programming.

---

# Learning Order

Do **NOT** solve these problems randomly.

Follow this progression.

```
One String DP
        ↓
Two String DP
        ↓
LCS Family
        ↓
Transformation DP
        ↓
Counting DP
        ↓
Advanced String DP
```

---

# String DP Family Tree

```
                    String DP
                        │
      ┌─────────────────┼─────────────────┐
      │                 │                 │
 One String DP     Two String DP      Counting DP
      │                 │                 │
 Word Break           LCS        Distinct Subsequences
      │                 │                 │
 Decode Ways      Edit Distance     Interleaving String
                        │
                  Palindrome DP
```

---

# Level 1 — Foundation (Must Solve)

Build the fundamentals of String DP.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 1 | Word Break | LeetCode 139 | Medium | One String DP |
| 2 | Decode Ways | LeetCode 91 | Medium | One String DP |
| 3 | Longest Common Subsequence | LeetCode 1143 | Medium | LCS |
| 4 | Edit Distance | LeetCode 72 | Medium | Transformation DP |

---

# Level 2 — LCS Family

Master two-string comparisons.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 5 | Delete Operation for Two Strings | LeetCode 583 | Medium | LCS Variant |
| 6 | Minimum ASCII Delete Sum for Two Strings | LeetCode 712 | Medium | Weighted LCS |
| 7 | Uncrossed Lines | LeetCode 1035 | Medium | LCS Pattern |

---

# Level 3 — Counting DP

Count the number of valid ways.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 8 | Distinct Subsequences | LeetCode 115 | Hard | Counting DP |
| 9 | Distinct Subsequences II | LeetCode 940 | Hard | Counting DP |
| 10 | Interleaving String | LeetCode 97 | Medium | Two String DP |

---

# Level 4 — Palindrome String DP

Palindrome-based string problems.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 11 | Longest Palindromic Subsequence | LeetCode 516 | Medium | LCS Variant |
| 12 | Minimum Insertion Steps to Make a String Palindrome | LeetCode 1312 | Hard | Palindrome DP |
| 13 | Palindrome Partitioning II | LeetCode 132 | Hard | Interval + String DP |

---

# Level 5 — Matching & Transformation

Advanced transformations.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 14 | Regular Expression Matching | LeetCode 10 | Hard | String Matching DP |
| 15 | Wildcard Matching | LeetCode 44 | Hard | Pattern Matching DP |
| 16 | Shortest Common Supersequence | LeetCode 1092 | Hard | LCS Reconstruction |

---

# Level 6 — Advanced String DP

Frequently asked in top product companies.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 17 | Strange Printer | LeetCode 664 | Hard | Interval + String DP |
| 18 | Count Different Palindromic Subsequences | LeetCode 730 | Hard | Interval Counting |
| 19 | Number of Ways to Form a Target String Given a Dictionary | LeetCode 1639 | Hard | Counting DP |
| 20 | Minimum Window Subsequence | LeetCode 727 | Hard | String DP |

---

# Company Favorites

## Amazon

- 139
- 72
- 115
- 97

---

## Google

- 10
- 44
- 1092
- 1639

---

## Microsoft

- 1143
- 72
- 139

---

## Meta

- 1143
- 97
- 1092

---

## Apple

- 583
- 712
- 516

---

## Uber

- 664
- 730
- 1639

---

## FinTech Companies

Most frequently asked:

- 1143
- 72
- 139
- 115
- 516

---

# Recommended Solving Order (20 Problems)

## Week 1 — Foundations

- [ ] LeetCode 139 Word Break
- [ ] LeetCode 91 Decode Ways
- [ ] LeetCode 1143 Longest Common Subsequence
- [ ] LeetCode 72 Edit Distance

---

## Week 2 — LCS Variations

- [ ] LeetCode 583 Delete Operation for Two Strings
- [ ] LeetCode 712 Minimum ASCII Delete Sum
- [ ] LeetCode 1035 Uncrossed Lines
- [ ] LeetCode 115 Distinct Subsequences

---

## Week 3 — Counting & Palindrome

- [ ] LeetCode 97 Interleaving String
- [ ] LeetCode 516 Longest Palindromic Subsequence
- [ ] LeetCode 1312 Minimum Insertions
- [ ] LeetCode 132 Palindrome Partitioning II
- [ ] LeetCode 940 Distinct Subsequences II

---

## Week 4 — Expert

- [ ] LeetCode 10 Regular Expression Matching
- [ ] LeetCode 44 Wildcard Matching
- [ ] LeetCode 1092 Shortest Common Supersequence
- [ ] LeetCode 664 Strange Printer
- [ ] LeetCode 730 Count Different Palindromic Subsequences
- [ ] LeetCode 1639 Number of Ways to Form Target String

---

# Pattern Recognition Cheat Sheet

| If the question says... | Think... |
|--------------------------|----------|
| One String | `dp[i]` |
| Two Strings | `dp[i][j]` |
| Longest Common | LCS |
| Minimum Operations | Edit Distance |
| Delete / Insert | Transformation DP |
| Count Ways | Counting DP |
| Pattern Matching | Matching DP |
| Word Segmentation | One String DP |
| Palindrome | String + Interval DP |

---

# Standard State Definitions

## One String DP

```
dp[i]
```

Meaning

```
Answer

using first

i

characters
```

---

## Two String DP

```
dp[i][j]
```

Meaning

```
Answer

using first

i

characters of s1

and

first

j

characters of s2
```

---

## Counting DP

```
dp[i][j]
```

Meaning

```
Number of ways

instead of

maximum length
```

---

# Common Transitions

## LCS

```
Match

↓

Diagonal + 1

Else

↓

max(

Top,

Left
)
```

---

## Edit Distance

```
Match

↓

Diagonal

Else

↓

1 +

min(

Insert,

Delete,

Replace
)
```

---

## Word Break

```
Try every

previous split
```

---

## Distinct Subsequences

```
Equal

↓

Take

+

Skip

Not Equal

↓

Skip
```

---

# Time Complexity Guide

| Pattern | Complexity |
|----------|-----------|
| Word Break | `O(n²)` |
| Decode Ways | `O(n)` |
| LCS | `O(nm)` |
| Edit Distance | `O(nm)` |
| Distinct Subsequences | `O(nm)` |
| Wildcard Matching | `O(nm)` |
| Regex Matching | `O(nm)` |
| Strange Printer | `O(n³)` |

---

# Space Optimization

Many String DP problems only depend on the previous row.

Examples

- LCS
- Edit Distance
- Delete Operations
- Minimum ASCII Delete Sum

Space

```
O(nm)

↓

O(m)
```

---

# Interview Tips

Whenever you see strings, ask:

1. One string or multiple strings?
2. Substring or subsequence?
3. What should `dp[i]` or `dp[i][j]` represent?
4. Is this a length, count, or minimum-cost problem?
5. Can I optimize to one row?

---
# Mastery Checklist

## Beginner
- [ ] Solve Word Break.
- [ ] Solve Decode Ways.
- [ ] Solve LCS.
- [ ] Solve Edit Distance.
---
## Intermediate
- [ ] Solve Distinct Subsequences.
- [ ] Solve Longest Palindromic Subsequence.
- [ ] Solve Interleaving String.
---
## Advanced
- [ ] Solve Regular Expression Matching.
- [ ] Solve Wildcard Matching.
- [ ] Solve Shortest Common Supersequence.
- [ ] Recognize String DP immediately.
---