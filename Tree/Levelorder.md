# BFS (Breadth First Search) — Pattern Recognition Notes

---

# Definition

## Traversal Order

```text
Level by Level Traversal
```

BFS explores:

```text
Current Level → Next Level
```

---

# Core Idea

> Process all nearby nodes first before moving deeper.

---

# Data Structure Used

```text
Queue (FIFO)
```

Because:

```text
First In → First Out
```

helps process nodes level-by-level.

---

# When Should I Use BFS?

Use BFS when:

- You need shortest path in an unweighted graph
- You need level-order traversal
- You need minimum steps/moves
- You need nearest/closest node
- You need multi-source expansion
- You need layer-by-layer processing
- You need to simulate spreading
- You need minimum operations

---

# Biggest BFS Intuition

BFS works like:

```text
Wave Expansion
```

Example:

```text
Water spreading
Fire spreading
Virus spreading
Rotting oranges
Distance expansion
```

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "shortest path"
- "minimum steps"
- "minimum moves"
- "minimum operations"
- "nearest"
- "closest"
- "level order"
- "distance"
- "multi-source"
- "spread"
- "time taken"
- "minutes"
- "burn"
- "infect"
- "rotten"
- "all possibilities at current level"
- "fewest transformations"

→ Think **BFS**

---

# Mental Model

Ask this question:

> “Do I need the answer with minimum levels/steps first?”

If YES → BFS is likely correct.

---

# Most Important BFS Property

## BFS Guarantees Shortest Path

ONLY in:

```text
Unweighted Graphs
```

because BFS explores:

```text
distance = 1
distance = 2
distance = 3
```

in order.

---

# General BFS Template (Tree)

```java
Queue<TreeNode> q = new LinkedList<>();

q.offer(root);

while(!q.isEmpty()) {

    TreeNode node = q.poll();

    // process node

    if(node.left != null) {
        q.offer(node.left);
    }

    if(node.right != null) {
        q.offer(node.right);
    }
}
```

---

# Level Order BFS Template

```java
Queue<TreeNode> q = new LinkedList<>();

q.offer(root);

while(!q.isEmpty()) {

    int size = q.size();

    for(int i = 0; i < size; i++) {

        TreeNode node = q.poll();

        // process current level node

        if(node.left != null) {
            q.offer(node.left);
        }

        if(node.right != null) {
            q.offer(node.right);
        }
    }

    // level completed
}
```

---

# Pattern 1 — Level Order Traversal

---

## Trigger

- Level by level traversal
- Zigzag level
- Average of levels
- Right side view
- Nodes at same depth

---

## Problem

LeetCode 102 — Binary Tree Level Order Traversal

---

## Recognition

We must process:

```text
All nodes at same depth together
```

That is classic BFS.

---

## Solution

```java
class Solution {

    public List<List<Integer>> levelOrder(TreeNode root) {

        List<List<Integer>> ans = new ArrayList<>();

        if(root == null) return ans;

        Queue<TreeNode> q = new LinkedList<>();

        q.offer(root);

        while(!q.isEmpty()) {

            int size = q.size();

            List<Integer> level = new ArrayList<>();

            for(int i = 0; i < size; i++) {

                TreeNode node = q.poll();

                level.add(node.val);

                if(node.left != null) {
                    q.offer(node.left);
                }

                if(node.right != null) {
                    q.offer(node.right);
                }
            }

            ans.add(level);
        }

        return ans;
    }
}
```

---

# Pattern 2 — Shortest Path in Unweighted Graph

---

## Trigger

- Minimum steps
- Shortest transformation
- Fewest moves
- Minimum jumps

---

## Problem

LeetCode 127 — Word Ladder

---

## Recognition

Every transformation is:

```text
1 step
```

Need minimum transformations.

Classic shortest path in unweighted graph.

BFS is optimal.

---

## Core Logic

```text
Level = number of transformations
```

First time reaching target:

```text
Guaranteed shortest path
```

---

# Pattern 3 — Multi-Source BFS

---

## Trigger

- Spread simultaneously
- Multiple starting points
- Time-based expansion
- Rotting/burning/infection

---

## Problem

LeetCode 994 — Rotting Oranges

---

## Recognition

All rotten oranges spread simultaneously.

This creates:

```text
Layer-by-layer infection spread
```

Classic multi-source BFS.

---

## Solution

```java
class Solution {

    public int orangesRotting(int[][] grid) {

        Queue<int[]> q = new LinkedList<>();

        int fresh = 0;

        for(int i = 0; i < grid.length; i++) {

            for(int j = 0; j < grid[0].length; j++) {

                if(grid[i][j] == 2) {
                    q.offer(new int[]{i, j});
                }

                if(grid[i][j] == 1) {
                    fresh++;
                }
            }
        }

        int minutes = 0;

        int[][] dir = {
            {1,0},
            {-1,0},
            {0,1},
            {0,-1}
        };

        while(!q.isEmpty() && fresh > 0) {

            int size = q.size();

            for(int i = 0; i < size; i++) {

                int[] cur = q.poll();

                for(int[] d : dir) {

                    int nr = cur[0] + d[0];
                    int nc = cur[1] + d[1];

                    if(nr >= 0 && nc >= 0 &&
                       nr < grid.length &&
                       nc < grid[0].length &&
                       grid[nr][nc] == 1) {

                        grid[nr][nc] = 2;

                        fresh--;

                        q.offer(new int[]{nr, nc});
                    }
                }
            }

            minutes++;
        }

        return fresh == 0 ? minutes : -1;
    }
}
```

---

# Super Important BFS Recognition Patterns

---

# 1. Minimum Steps Problems

If question asks:

```text
minimum operations
minimum moves
minimum jumps
minimum turns
fewest transformations
```

→ BFS is VERY likely.

---

# 2. Layer-by-Layer Problems

If processing happens:

```text
level by level
wave by wave
round by round
minute by minute
```

→ Think BFS.

---

# 3. Simultaneous Expansion Problems

If many sources spread together:

```text
fire
virus
infection
water
distance
signal
```

→ Multi-source BFS.

---

# 4. Nearest Problems

If question asks:

```text
nearest hospital
nearest zero
closest node
minimum distance
```

→ BFS pattern.

---

# 5. State Space Search Problems

If states transform step-by-step:

```text
lock combinations
word transformations
board games
minimum operations
```

→ BFS on states.

---

# Important Interview Insight

DFS is usually:

```text
Deep exploration
```

BFS is usually:

```text
Shortest / minimum / level-based exploration
```

---

# Quick Comparison

| Situation | Use |
|---|---|
| Minimum steps | BFS |
| Level traversal | BFS |
| Deep recursion problems | DFS |
| Top-down flow | Preorder DFS |
| Bottom-up calculation | Postorder DFS |

---

# Common Mistake

Students use DFS for shortest path in unweighted graphs.

But DFS:

```text
Does NOT guarantee shortest path
```

BFS does.

---

# One-Line Memory Trick

```text
BFS = Explore nearest nodes first
```

---

# Final Interview Insight

Many graph and matrix interview problems are secretly asking:

```text
Shortest path or level expansion?
```

If YES:

```text
Think BFS immediately
```

This is one of the highest-frequency interview patterns asked at Meta, Google, Amazon, Uber, and other top product companies.