# 04 - Longest Common Subsequence (LCS) DP Problems

> **Goal:** Master every important LCS-based Dynamic Programming pattern asked in Top MNCs, FinTech companies, coding interviews, and competitive programming.

---

# Learning Order

Do **NOT** solve these problems randomly.

Follow this progression.

```
Basic LCS
      ↓
LCS Transformations
      ↓
Palindrome DP
      ↓
Edit Operations
      ↓
Sequence Matching
      ↓
Advanced String DP
```

---

# LCS Family Tree

```
                   LCS DP
                      │
        ┌─────────────┼─────────────┐
        │             │             │
   String Matching  Palindrome   Edit Operations
        │             │             │
   Deletion       Insertions     Edit Distance
        │             │             │
   SCS           LPS          Sequence Alignment
```

---

# Level 1 — Foundation (Must Solve)

These problems build the core LCS intuition.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 1 | Longest Common Subsequence | LeetCode 1143 | Medium | Classic LCS |
| 2 | Print Longest Common Subsequence | GFG | Medium | LCS Reconstruction |
| 3 | Longest Common Substring | LeetCode 718* / GFG | Medium | Similar but Different |
| 4 | Uncrossed Lines | LeetCode 1035 | Medium | LCS on Arrays |

> **Note:** LeetCode 718 is technically *Maximum Length of Repeated Subarray*, which uses the same DP idea as **Longest Common Substring**, but substring and subsequence are different patterns.

---

# Level 2 — LCS Transformations

Use LCS to solve transformation problems.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 5 | Delete Operation for Two Strings | LeetCode 583 | Medium | LCS Formula |
| 6 | Shortest Common Supersequence | LeetCode 1092 | Hard | LCS Reconstruction |
| 7 | Minimum ASCII Delete Sum | LeetCode 712 | Medium | Weighted LCS |

---

# Level 3 — Palindrome DP

Convert palindrome problems into LCS.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 8 | Longest Palindromic Subsequence | LeetCode 516 | Medium | LCS with Reverse |
| 9 | Minimum Insertions to Make a String Palindrome | LeetCode 1312 | Hard | LPS |
| 10 | Minimum Deletions to Make String Balanced* | LeetCode 1653 | Medium | DP Variant |

> **Note:** LeetCode 1653 is not a direct LCS problem, but the optimization mindset is closely related.

---

# Level 4 — Edit Operations

Transform one string into another.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 11 | Edit Distance | LeetCode 72 | Hard | Edit DP |
| 12 | One Edit Distance | LeetCode 161 | Medium | String Comparison |
| 13 | Delete Columns to Make Sorted III | LeetCode 960 | Hard | LCS Variant |

---

# Level 5 — Advanced Sequence Matching

Compare complex sequences.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 14 | Distinct Subsequences | LeetCode 115 | Hard | Counting DP |
| 15 | Is Subsequence | LeetCode 392 | Easy | Simplified LCS |
| 16 | Number of Matching Subsequences | LeetCode 792 | Medium | Multiple Subsequences |

---

# Level 6 — Advanced String DP

Frequently asked in top product companies.

| # | Problem | Platform | Difficulty | Pattern |
|---|---------|----------|------------|----------|
| 17 | Interleaving String | LeetCode 97 | Medium | 2D DP |
| 18 | Regular Expression Matching | LeetCode 10 | Hard | Pattern Matching |
| 19 | Wildcard Matching | LeetCode 44 | Hard | Pattern Matching |
| 20 | Strange Printer | LeetCode 664 | Hard | Interval DP |

> **Note:** Strange Printer belongs to **Interval DP**, but it builds upon the same string DP foundation.

---

# Company Favorites

## Amazon

- 1143
- 72
- 583
- 516
- 115

---

## Google

- 1092
- 712
- 44
- 10
- 97

---

## Microsoft

- 72
- 1143
- 583
- 392

---

## Meta

- 1143
- 72
- 115
- 516

---

## Apple

- 1143
- 72
- 1092
- 516

---

## Uber

- 97
- 712
- 115
- 44

---

## FinTech Companies

Most frequently asked:

- 1143
- 72
- 583
- 516
- 392
- 115

---

# Recommended Solving Order (20 Problems)

## Week 1 — LCS Fundamentals

- [ ] LeetCode 1143 Longest Common Subsequence
- [ ] GFG Print LCS
- [ ] GFG Longest Common Substring
- [ ] LeetCode 1035 Uncrossed Lines

---

## Week 2 — LCS Applications

- [ ] LeetCode 583 Delete Operation for Two Strings
- [ ] LeetCode 1092 Shortest Common Supersequence
- [ ] LeetCode 712 Minimum ASCII Delete Sum
- [ ] LeetCode 516 Longest Palindromic Subsequence
- [ ] LeetCode 1312 Minimum Insertions

---

## Week 3 — Edit Operations

- [ ] LeetCode 72 Edit Distance
- [ ] LeetCode 161 One Edit Distance
- [ ] LeetCode 392 Is Subsequence
- [ ] LeetCode 115 Distinct Subsequences
- [ ] LeetCode 792 Number of Matching Subsequences

---

## Week 4 — Advanced

- [ ] LeetCode 97 Interleaving String
- [ ] LeetCode 44 Wildcard Matching
- [ ] LeetCode 10 Regular Expression Matching
- [ ] LeetCode 960 Delete Columns to Make Sorted III

---

# Pattern Recognition Cheat Sheet

| If the question says... | Think... |
|--------------------------|----------|
| Two strings | LCS |
| Two arrays | LCS |
| Common subsequence | LCS |
| Common substring | Longest Common Substring |
| Minimum insertions | LPS |
| Minimum deletions | LCS Formula |
| Palindrome | LPS = LCS(s, reverse(s)) |
| Edit operations | Edit Distance |
| Pattern matching | String DP |

---

# Standard State Definitions

## Longest Common Subsequence

```
dp[i][j]
```

Meaning:

```
LCS length of

s1[0...i-1]

and

s2[0...j-1]
```

---

## Edit Distance

```
dp[i][j]
```

Meaning:

```
Minimum operations to convert

s1[0...i-1]

into

s2[0...j-1]
```

---

## Distinct Subsequences

```
dp[i][j]
```

Meaning:

```
Number of ways

s1[0...i-1]

can form

s2[0...j-1]
```

---

# Common Transitions

## LCS

If characters match:

```
1 + dp[i-1][j-1]
```

Else:

```
max(
dp[i-1][j],
dp[i][j-1]
)
```

---

## Longest Common Substring

If characters match:

```
1 + dp[i-1][j-1]
```

Else:

```
0
```

---

## Edit Distance

```
Insert

Delete

Replace
```

Take the minimum.

---

## Distinct Subsequences

Match:

```
take + skip
```

No Match:

```
skip
```

---

# Space Optimization

Many LCS-based problems allow:

```
O(n × m)
```

↓

```
O(m)
```

using only the previous row.

Exceptions:

- Printing the actual LCS
- Shortest Common Supersequence reconstruction

These require the complete DP table.

---

# Important Formulas

## Longest Palindromic Subsequence

```
LPS

=

LCS(
s,
reverse(s)
)
```

---

## Minimum Insertions

```
n - LPS
```

---

## Minimum Deletions

```
n - LPS
```

(for making a string a palindrome)

---

## Delete Operation for Two Strings

```
(n - LCS)
+
(m - LCS)
```

---

## Shortest Common Supersequence Length

```
n + m - LCS
```

---

# Interview Tips

Whenever you see two strings, ask:

1. Is this asking for a subsequence or a substring?
2. Can I define `dp[i][j]`?
3. Is the decision based on **match vs skip**?
4. Is this an LCS transformation problem?
5. Can the solution be optimized to `O(m)` space?

---

# Mastery Checklist

## Beginner

- [ ] Solve Longest Common Subsequence.
- [ ] Understand subsequence vs substring.
- [ ] Write Memoization and Tabulation.

---

## Intermediate

- [ ] Solve palindrome transformation problems.
- [ ] Solve deletion and insertion problems.
- [ ] Optimize LCS to `O(m)` space.

---

## Advanced

- [ ] Solve Edit Distance confidently.
- [ ] Solve Distinct Subsequences.
- [ ] Print the actual LCS.
- [ ] Recognize LCS-based transformations immediately.

---

# Final Goal

After completing this roadmap, you should be able to:

- Instantly recognize LCS-based problems.
- Differentiate between subsequence and substring DP.
- Derive the correct DP state and recurrence.
- Apply LCS transformations to solve insertion, deletion, palindrome, and supersequence problems.
- Confidently solve string DP questions commonly asked in Top MNCs, FinTech companies, and coding interviews.