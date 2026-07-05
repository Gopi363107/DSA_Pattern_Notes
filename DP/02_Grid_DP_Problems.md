# 02 - Grid Dynamic Programming Problems

> **Goal:** Master every important Grid DP pattern asked in Top MNCs, FinTech companies, coding interviews, and competitive programming.

---

# Learning Order

Do **NOT** solve problems randomly.

Follow this progression:

```
Basic Path Counting
        ↓
Path Optimization
        ↓
Obstacles
        ↓
Triangle DP
        ↓
Falling Path DP
        ↓
Multi-Directional DP
        ↓
Multi-Agent DP
        ↓
Advanced Grid DP
```

---

# Level 1 — Foundation (Must Solve)

These problems build the basic Grid DP intuition.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 1 | Unique Paths | 62 | Easy | Path Counting |
| 2 | Unique Paths II | 63 | Medium | Obstacles |
| 3 | Minimum Path Sum | 64 | Medium | Minimum Cost |
| 4 | Pascal's Triangle | 118 | Easy | Grid Construction |
| 5 | Pascal's Triangle II | 119 | Easy | Space Optimized DP |

---

# Level 2 — Triangle DP

Grid shape changes from rectangle to triangle.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 6 | Triangle | 120 | Medium | Bottom-Up DP |
| 7 | Minimum Falling Path Sum | 931 | Medium | Three Directions |
| 8 | Minimum Falling Path Sum II | 1289 | Hard | Optimized Transition |

---

# Level 3 — Maximum / Minimum Path

Optimization problems.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 9 | Cherry Pickup II | 1463 | Hard | Two Robots |
| 10 | Dungeon Game | 174 | Hard | Reverse DP |
| 11 | Maximum Number of Moves in a Grid | 2684 | Medium | Grid Traversal |

---

# Level 4 — Counting Paths

Count all valid paths.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 12 | Out of Boundary Paths | 576 | Medium | Boundary DP |
| 13 | Number of Increasing Paths in a Grid | 2328 | Hard | DFS + Memoization |
| 14 | Count Square Submatrices with All Ones | 1277 | Medium | Grid Counting |

---

# Level 5 — Matrix Optimization

Optimization over every cell.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 15 | Maximal Square | 221 | Medium | Square DP |
| 16 | Largest 1-Bordered Square | 1139 | Medium | Matrix DP |
| 17 | Maximal Rectangle | 85 | Hard | Histogram + DP |

---

# Level 6 — DFS + Memoization

Movement in multiple directions.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 18 | Longest Increasing Path in a Matrix | 329 | Hard | DFS + Memoization |
| 19 | Number of Increasing Paths in a Grid | 2328 | Hard | Memoization |
| 20 | Pacific Atlantic Water Flow* | 417 | Medium | DFS (Related Pattern) |

> **Note:** Pacific Atlantic Water Flow is primarily a graph/DFS problem but helps build intuition for multi-directional grid traversal.

---

# Level 7 — Multi-Agent Grid DP

Two or more players moving simultaneously.

| # | Problem | LeetCode | Difficulty | Pattern |
|---|----------|----------|------------|----------|
| 21 | Cherry Pickup | 741 | Hard | 3D DP |
| 22 | Cherry Pickup II | 1463 | Hard | Dual Robot DP |

---

# Level 8 — Advanced Grid DP

Frequently asked in top companies.

| # | Problem | LeetCode | Difficulty |
|---|----------|----------|------------|
| 23 | Dungeon Game | 174 | Hard |
| 24 | Longest Increasing Path | 329 | Hard |
| 25 | Cherry Pickup | 741 | Hard |
| 26 | Cherry Pickup II | 1463 | Hard |
| 27 | Minimum Falling Path Sum II | 1289 | Hard |
| 28 | Number of Increasing Paths | 2328 | Hard |

---

# Company Favorites

## Amazon

- 62
- 63
- 64
- 120
- 221
- 174

---

## Google

- 329
- 741
- 1463
- 1289
- 2328

---

## Microsoft

- 62
- 64
- 931
- 221

---

## Meta

- 62
- 63
- 64
- 329
- 120

---

## Apple

- 64
- 120
- 221
- 931

---

## Uber

- 329
- 174
- 741
- 1463

---

## FinTech Companies

Most frequently asked:

- 62
- 63
- 64
- 120
- 931
- 221

---

# Recommended Solving Order (25 Problems)

## Week 1 — Fundamentals

- [ ] 62 Unique Paths
- [ ] 63 Unique Paths II
- [ ] 64 Minimum Path Sum
- [ ] 118 Pascal's Triangle
- [ ] 119 Pascal's Triangle II

---

## Week 2 — Intermediate

- [ ] 120 Triangle
- [ ] 931 Minimum Falling Path Sum
- [ ] 1277 Count Square Submatrices
- [ ] 221 Maximal Square
- [ ] 2684 Maximum Number of Moves

---

## Week 3 — Advanced

- [ ] 576 Out of Boundary Paths
- [ ] 329 Longest Increasing Path
- [ ] 174 Dungeon Game
- [ ] 1289 Minimum Falling Path Sum II
- [ ] 1463 Cherry Pickup II

---

## Week 4 — Expert

- [ ] 741 Cherry Pickup
- [ ] 2328 Number of Increasing Paths
- [ ] 1139 Largest 1-Bordered Square
- [ ] 85 Maximal Rectangle

---

# Pattern Recognition Cheat Sheet

| If the question says... | Think... |
|--------------------------|----------|
| Grid | Grid DP |
| Matrix | 2D DP |
| Robot movement | Path DP |
| Minimum cost | Optimization DP |
| Count paths | Counting DP |
| Triangle | Triangle DP |
| Falling | Three-direction DP |
| Obstacles | Boundary DP |
| Two robots | Multi-Agent DP |
| Move in four directions | DFS + Memoization |

---

# Standard Grid DP State

```
dp[i][j]
```

Common meanings:

- Minimum cost to reach `(i, j)`
- Maximum score till `(i, j)`
- Number of ways to reach `(i, j)`
- Longest path ending at `(i, j)`

---

# Common Transitions

### Right & Down

```
dp[i][j] =
f(dp[i-1][j], dp[i][j-1])
```

---

### Down, Down-Left, Down-Right

```
dp[i][j] =
f(
dp[i-1][j],
dp[i-1][j-1],
dp[i-1][j+1]
)
```

---

### DFS + Memoization

```
dp[i][j] =
1 + max(all valid neighbours)
```

---

# Space Optimization Opportunities

Usually possible for:

- Unique Paths
- Minimum Path Sum
- Triangle
- Falling Path Sum

Reduce:

```
O(m × n)
```

↓

```
O(n)
```

using one previous row.

---

# Interview Tips

Whenever you see a matrix, ask yourself:

1. What does `dp[i][j]` represent?
2. From where can I reach this cell?
3. What are the base cells?
4. What traversal order ensures dependencies are already computed?
5. Can I optimize the memory to one row?

---

# Mastery Checklist

## Beginner

- [ ] Recognize Grid DP problems.
- [ ] Define `dp[i][j]`.
- [ ] Handle first row and first column correctly.

---

## Intermediate

- [ ] Write Memoization.
- [ ] Convert to Tabulation.
- [ ] Optimize space to `O(n)` when applicable.

---

## Advanced

- [ ] Solve Triangle DP confidently.
- [ ] Solve DFS + Memoization Grid DP.
- [ ] Handle multi-agent Grid DP.
- [ ] Recognize when Grid DP is the right approach over BFS/DFS.

---

# Final Goal

After completing this roadmap, you should be able to:

- Instantly identify Grid DP problems.
- Design the correct state and transition.
- Solve classic path-counting and path-optimization questions.
- Handle advanced matrix DP problems involving multiple directions or multiple agents.
- Confidently solve most Grid DP interview questions from top product companies and FinTech firms.