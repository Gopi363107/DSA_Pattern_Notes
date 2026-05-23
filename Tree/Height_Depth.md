# Tree Height / Depth Pattern — Recognition Notes

---

# Definition

Tree height/depth problems focus on:

```text
Distance between nodes in a tree
```

Usually measured using:

- number of nodes
- number of edges
- subtree levels

---

# Core Intuition

Most height/depth problems follow:

```text
Child → Parent information flow
```

That means:

```text
Postorder DFS is commonly used
```

because parent calculations depend on child answers.

---

# Important Terminology

---

# Height of a Node

```text
Maximum distance from current node to leaf
```

Example:

```text
Leaf node height = 0
```

---

# Depth of a Node

```text
Distance from root to current node
```

Example:

```text
Root depth = 0
```

---

# Height vs Depth

| Concept | Direction |
|---|---|
| Depth | Root → Node |
| Height | Node → Leaf |

---

# When Should I Think About Height/Depth Pattern?

Use this pattern when:

- Problem involves subtree heights
- Parent depends on child depth
- Longest/maximum path exists
- Need node levels
- Need vertical distance calculations
- Need ancestor distance
- Need deepest node/subtree

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "deepest"
- "height"
- "depth"
- "distance"
- "maximum path"
- "levels"
- "subtree height"
- "farthest"
- "ancestor"
- "longest"
- "diameter"
- "deepest leaf"
- "lowest level"

→ Think **Height/Depth Pattern**

---

# Mental Model

Ask this question:

> “Does the parent need child height/depth information first?”

If YES:

```text
Postorder DFS is likely correct
```

---

# Generic Height Template

```java
int dfs(TreeNode root) {

    if(root == null) return 0;

    int left = dfs(root.left);
    int right = dfs(root.right);

    return Math.max(left, right) + 1;
}
```

---

# Pattern 1 — Deepest Leaves Sum

---

## Trigger

- deepest nodes
- bottom-most level
- level tracking

---

## Problem

LeetCode 1302 — Deepest Leaves Sum

---

## Recognition

Need:

```text
Sum of nodes at maximum depth
```

We track:

- current level
- deepest level found

Classic depth tracking pattern.

---

## Solution

```java
class Solution {

    int maxDepth = -1;
    int sum = 0;

    public int deepestLeavesSum(TreeNode root) {

        dfs(root, 0);

        return sum;
    }

    void dfs(TreeNode root, int depth) {

        if(root == null) return;

        if(depth > maxDepth) {

            maxDepth = depth;

            sum = root.val;
        }
        else if(depth == maxDepth) {

            sum += root.val;
        }

        dfs(root.left, depth + 1);
        dfs(root.right, depth + 1);
    }
}
```

---

# Pattern 2 — Lowest Common Ancestor of Deepest Leaves

---

## Trigger

- deepest subtree
- compare subtree heights
- ancestor from depths

---

## Problem

LeetCode 1123 — Lowest Common Ancestor of Deepest Leaves

---

## Recognition

Need:

```text
Compare left subtree depth vs right subtree depth
```

If:

- left deeper → answer in left
- right deeper → answer in right
- equal → current node is answer

Classic height comparison pattern.

---

## Solution

```java
class Solution {

    public TreeNode lcaDeepestLeaves(TreeNode root) {

        return dfs(root).node;
    }

    class Pair {

        TreeNode node;
        int depth;

        Pair(TreeNode n, int d) {
            node = n;
            depth = d;
        }
    }

    Pair dfs(TreeNode root) {

        if(root == null) {
            return new Pair(null, 0);
        }

        Pair left = dfs(root.left);
        Pair right = dfs(root.right);

        if(left.depth > right.depth) {
            return new Pair(left.node, left.depth + 1);
        }

        if(right.depth > left.depth) {
            return new Pair(right.node, right.depth + 1);
        }

        return new Pair(root, left.depth + 1);
    }
}
```

---

# Pattern 3 — Find Bottom Left Tree Value

---

## Trigger

- last level
- leftmost deepest node
- level traversal

---

## Problem

LeetCode 513 — Find Bottom Left Tree Value

---

## Recognition

Need:

```text
Leftmost node at deepest level
```

Depth tracking problem.

Can solve using:

- DFS depth tracking
- BFS level traversal

---

## Solution (DFS)

```java
class Solution {

    int maxDepth = -1;
    int ans = 0;

    public int findBottomLeftValue(TreeNode root) {

        dfs(root, 0);

        return ans;
    }

    void dfs(TreeNode root, int depth) {

        if(root == null) return;

        if(depth > maxDepth) {

            maxDepth = depth;

            ans = root.val;
        }

        dfs(root.left, depth + 1);
        dfs(root.right, depth + 1);
    }
}
```

---

# Super Important Recognition Patterns

---

# 1. Compare Left vs Right Heights

If question requires:

```text
left subtree vs right subtree
```

→ Think:

```text
Postorder height calculation
```

---

# 2. Deepest Node Problems

If question asks:

```text
deepest
bottom-most
last level
maximum depth
```

→ Think:

```text
Depth tracking
```

---

# 3. Longest Path Problems

If question asks:

```text
diameter
maximum path
farthest node
longest route
```

→ Height pattern is likely involved.

---

# 4. Ancestor + Depth Problems

If question mixes:

```text
ancestor + deepest
```

→ Usually compare subtree heights.

---

# Important Interview Insight

Most tree DP problems are actually:

```text
Height propagation problems
```

Understanding height flow makes hard trees much easier.

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Parent depends on child heights | Postorder |
| Track current level | Depth DFS |
| Level-by-level traversal | BFS |
| Deepest node problems | Height/Depth |

---

# Common Mistake

Students confuse:

```text
Depth and Height
```

Remember:

```text
Depth = Root → Node
Height = Node → Leaf
```

---

# One-Line Memory Trick

```text
Height = Bottom-up
Depth = Top-down
```

---

# Final Interview Insight

Many difficult tree problems become easier after identifying:

```text
Am I tracking depth?
OR
Am I calculating height?
```

That single recognition often decides the entire solution approach in interviews at Meta, Google, Amazon, and top product companies.