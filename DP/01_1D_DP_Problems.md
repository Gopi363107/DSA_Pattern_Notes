# 01 - 1D Dynamic Programming Problems

> Goal: Master every important 1D DP pattern asked in Top MNCs, FinTech companies, and coding interviews.

---

# Learning Order

Do **NOT** solve randomly.

Follow this sequence.

```
Basic Counting DP
        ↓
Basic Optimization DP
        ↓
Linear DP
        ↓
Jump DP
        ↓
Decision DP
        ↓
Partition DP
        ↓
Advanced 1D DP
```

---

# Level 1 — Foundation (Must Solve)

These problems build your DP thinking.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 1 | Fibonacci Number | 509 | Easy | Basic DP |
| 2 | Climbing Stairs | 70 | Easy | Count Ways |
| 3 | Min Cost Climbing Stairs | 746 | Easy | Min Cost |
| 4 | N-th Tribonacci Number | 1137 | Easy | Recurrence |
| 5 | Counting Bits | 338 | Easy | State Transition |

---

# Level 2 — Decision DP

Choose between multiple options.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 6 | House Robber | 198 | Easy | Take / Skip |
| 7 | House Robber II | 213 | Medium | Circular DP |
| 8 | Delete and Earn | 740 | Medium | House Robber Transformation |

---

# Level 3 — Jump DP

Current answer depends on reachable positions.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 9 | Jump Game | 55 | Medium | Reachability |
| 10 | Jump Game II | 45 | Medium | Minimum Jumps |
| 11 | Frog Jump | 403 | Hard | State Expansion |

---

# Level 4 — Count Ways

Count different valid possibilities.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 12 | Decode Ways | 91 | Medium | Count Paths |
| 13 | Decode Ways II | 639 | Hard | Advanced Counting |
| 14 | Combination Sum IV | 377 | Medium | Ordered Ways |
| 15 | Student Attendance Record II | 552 | Hard | Counting DP |

---

# Level 5 — Maximum / Minimum Optimization

Find the best answer.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 16 | Maximum Product Subarray | 152 | Medium | Max / Min DP |
| 17 | Integer Break | 343 | Medium | Max Product |
| 18 | Perfect Squares | 279 | Medium | Minimum Count |
| 19 | Coin Change | 322 | Medium | Minimum Coins |
| 20 | Solving Questions With Brainpower | 2140 | Medium | Skip Decision |

---

# Level 6 — Partition DP

Split array into parts.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 21 | Partition Array for Maximum Sum | 1043 | Medium | Partition DP |
| 22 | Integer Break | 343 | Medium | Partition |
| 23 | Word Break | 139 | Medium | Prefix Partition |

---

# Level 7 — Sequence DP

Work along one sequence.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 24 | Longest Increasing Subsequence | 300 | Medium | Sequence DP |
| 25 | Number of Longest Increasing Subsequence | 673 | Medium | Counting LIS |
| 26 | Wiggle Subsequence | 376 | Medium | State DP |

---

# Level 8 — Prefix DP

State depends on prefix.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 27 | Maximum Subarray | 53 | Easy | Kadane DP |
| 28 | Maximum Absolute Sum | 1749 | Medium | Prefix DP |
| 29 | Best Time to Buy and Sell Stock | 121 | Easy | Profit DP |

---

# Level 9 — String DP (1D)

DP over characters.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 30 | Decode Ways | 91 | Medium | String DP |
| 31 | Word Break | 139 | Medium | Prefix DP |
| 32 | Extra Characters in a String | 2707 | Medium | String Optimization |

---

# Level 10 — Hard Interview Problems

Frequently asked in top product companies.

| # | Problem | LeetCode | Difficulty |
|---|----------|----------|------------|
| 33 | Arithmetic Slices II | 446 | Hard |
| 34 | Student Attendance Record II | 552 | Hard |
| 35 | Decode Ways II | 639 | Hard |
| 36 | Frog Jump | 403 | Hard |
| 37 | Split Array Largest Sum | 410 | Hard (Binary Search + DP) |
| 38 | Burst Balloons* | 312 | Hard (Interval DP, not pure 1D) |

> **Note:** Burst Balloons is included for future reference but belongs to **Interval DP**, not the 1D DP pattern.

---

# Company Favorites

## Amazon

- 70
- 198
- 91
- 322
- 139
- 300

---

## Google

- 300
- 673
- 377
- 1043
- 2140

---

## Microsoft

- 198
- 213
- 91
- 53
- 279

---

## Meta

- 55
- 45
- 139
- 300
- 152

---

## Apple

- 53
- 198
- 322
- 91

---

## Uber

- 2140
- 377
- 1043
- 300

---

## FinTech Companies

Very frequently asked:

- 198
- 213
- 322
- 53
- 55
- 45
- 91
- 139
- 300
- 152

---

# Recommended Solving Order (30-Day Plan)

### Week 1 — Build Fundamentals

- [ ] 509 Fibonacci Number
- [ ] 70 Climbing Stairs
- [ ] 746 Min Cost Climbing Stairs
- [ ] 1137 Tribonacci Number
- [ ] 338 Counting Bits
- [ ] 198 House Robber

---

### Week 2 — Decision & Jump

- [ ] 213 House Robber II
- [ ] 740 Delete and Earn
- [ ] 55 Jump Game
- [ ] 45 Jump Game II
- [ ] 91 Decode Ways
- [ ] 377 Combination Sum IV

---

### Week 3 — Optimization

- [ ] 322 Coin Change
- [ ] 279 Perfect Squares
- [ ] 152 Maximum Product Subarray
- [ ] 2140 Brainpower
- [ ] 1043 Partition Array for Maximum Sum
- [ ] 139 Word Break

---

### Week 4 — Advanced

- [ ] 300 LIS
- [ ] 673 Number of LIS
- [ ] 376 Wiggle Subsequence
- [ ] 2707 Extra Characters
- [ ] 552 Attendance Record II
- [ ] 639 Decode Ways II

---

# Pattern Recognition Cheat Sheet

| If the question says... | Think... |
|--------------------------|----------|
| Count ways | DP Counting |
| Maximum profit | Optimization DP |
| Minimum cost | Min DP |
| Take or Skip | Decision DP |
| Jump | Jump DP |
| Break string | Prefix DP |
| Partition array | Partition DP |
| Increasing sequence | Sequence DP |

---

# Mastery Checklist

## Beginner

- [ ] Can identify a 1D DP problem.
- [ ] Can define `dp[i]`.
- [ ] Can derive the recurrence.
- [ ] Can write memoization.

---

## Intermediate

- [ ] Can convert memoization to tabulation.
- [ ] Can optimize space to `O(1)` where applicable.
- [ ] Can recognize common 1D DP patterns quickly.

---

## Advanced

- [ ] Can solve unseen 1D DP problems within 20–30 minutes.
- [ ] Can derive the recurrence without hints.
- [ ] Can explain the intuition in interviews.
- [ ] Can identify when a problem is **not** 1D DP.

---

# Final Goal

After completing these problems, you should be able to:

- Recognize 1D DP patterns within a few minutes.
- Design the state and recurrence confidently.
- Implement Memoization, Tabulation, and Space Optimization.
- Handle most Easy and Medium 1D DP interview questions and many Hard variants with confidence.