# 07 - Tree Dynamic Programming Pattern

> **Core Idea:** Compute answers for every subtree and combine child results to solve the entire tree.

---

# What is Tree DP?

Tree DP is used when:

- The input is a **tree**.
- The answer for a node depends on its children.
- We solve smaller subtrees first, then combine them.

Unlike Array DP:

```
Linear

0 → n
```

Tree DP works on

```
Hierarchy
```

---

# What is a Tree?

A tree is a connected graph with

```
N nodes

N-1 edges
```

Example

```
        1
      / | \
     2  3  4
       / \
      5   6
```

Every node becomes the root of its own subtree.

---

# What is a Subtree?

Subtree rooted at

```
3
```

contains

```
    3
   / \
  5   6
```

Tree DP usually asks

> What is the best answer for this subtree?

---

# Core Idea

Instead of asking

```
What is the answer till index i?
```

Ask

```
What is the answer

for subtree rooted at node?
```

---

# When Should You Think of Tree DP?

Whenever the problem contains

- Binary Tree
- N-ary Tree
- Rooted Tree
- Parent
- Children
- Independent Set
- Maximum Path
- Diameter
- House Robber on Tree
- Ancestors

Immediately ask

> Can the answer for a node be computed using answers from its children?

If YES,

think Tree DP.

---

# Common State Definitions

---

## State 1

One value per node.

```
dp[node]
```

Meaning

```
Best answer

for subtree rooted at node
```

---

## State 2

Two states.

```
dp[node][0]

dp[node][1]
```

Meaning

```
0

Node NOT selected

1

Node selected
```

Very common.

---

## State 3

Multiple states.

```
dp[node][k]
```

Meaning

Depends on problem.

Often

```
Exactly

k

nodes chosen
```

or

```
Distance

Color

Parity
```

---

# Generic Thinking Process

## Step 1

Perform DFS.

---

## Step 2

Solve children first.

(Postorder Traversal)

---

## Step 3

Merge children's answers.

---

## Step 4

Return answer for current node.

---

# Generic DFS Template

```java
void dfs(int node, int parent){

    for(int child : graph[node]){

        if(child == parent)
            continue;

        dfs(child, node);
    }

    // Compute dp[node]
}
```

---

# Why Postorder?

Example

```
      1
     / \
    2   3
```

To compute

```
dp[1]
```

we first need

```
dp[2]

dp[3]
```

Hence

```
Children

↓

Parent
```

---

# Pattern 1

Single State DP

Example

```
Subtree Size

Maximum Sum

Height
```

Transition

```
dp[node]

=

combine(children)
```

---

# Pattern 2

Include / Exclude DP

Most famous Tree DP.

```
dp[node][1]

Choose node
```

```
dp[node][0]

Don't choose node
```

Transition

If choose node

↓

Cannot choose child.

If don't choose node

↓

Child may be chosen or skipped.

---

# Pattern 3

Rerooting DP

Need answer for

```
EVERY

node

as root.
```

Two DFS.

Very common in CP.

---

# Pattern Recognition

Question contains

```
Tree

Binary Tree

Root

Children

Subtree

Path

Independent Set

Diameter
```

↓

DFS

↓

Children

↓

Parent

↓

DP

---

# Competitive Programming Insight

Almost every Tree DP problem starts with

```
DFS
```

The real challenge is

> What should each node return?

---

# Problem 1

## LeetCode 337 — House Robber III

Difficulty

Medium

---

## Core Idea

Either

```
Take node

OR

Skip node
```

---

## State

```
dp[node][0]

Not Rob

dp[node][1]

Rob
```

---

## Transition

If rob current

```
Children

cannot

be robbed.
```

If skip current

```
Children

choose

best option.
```

---

## Java Solution

```java
class Solution {

    public int rob(TreeNode root){

        int[] ans = dfs(root);

        return Math.max(ans[0], ans[1]);
    }

    private int[] dfs(TreeNode node){

        if(node == null)
            return new int[]{0,0};

        int[] left = dfs(node.left);
        int[] right = dfs(node.right);

        int rob =
                node.val

                +

                left[0]

                +

                right[0];

        int skip =
                Math.max(left[0], left[1])

                +

                Math.max(right[0], right[1]);

        return new int[]{skip, rob};
    }
}
```

---

### Time Complexity

```
O(N)
```

### Space Complexity

```
O(H)
```

---

# Problem 2

## LeetCode 124 — Binary Tree Maximum Path Sum

Difficulty

Hard

---

## Core Idea

Every node can be

```
Highest point

of

maximum path.
```

Need

Global Answer.

---

## State

DFS returns

```
Maximum gain

from node
```

Global variable stores

```
Maximum path.
```

---

## Java Solution

```java
class Solution {

    int answer = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root){

        dfs(root);

        return answer;
    }

    private int dfs(TreeNode node){

        if(node == null)
            return 0;

        int left =
                Math.max(0,
                dfs(node.left));

        int right =
                Math.max(0,
                dfs(node.right));

        answer = Math.max(

                answer,

                node.val

                +

                left

                +

                right
        );

        return node.val

                +

                Math.max(left, right);
    }
}
```

---

### Time Complexity

```
O(N)
```

### Space Complexity

```
O(H)
```

---

# Problem 3

## LeetCode 543 — Diameter of Binary Tree

Difficulty

Easy

---

## Core Idea

Diameter

=

Longest path passing through a node.

---

## State

DFS returns

```
Height
```

Global variable stores

```
Diameter
```

---

## Java Solution

```java
class Solution {

    int diameter = 0;

    public int diameterOfBinaryTree(TreeNode root){

        dfs(root);

        return diameter;
    }

    private int dfs(TreeNode node){

        if(node == null)
            return 0;

        int left = dfs(node.left);

        int right = dfs(node.right);

        diameter = Math.max(
                diameter,
                left + right
        );

        return 1 + Math.max(left, right);
    }
}
```

---

### Time Complexity

```
O(N)
```

### Space Complexity

```
O(H)
```

---

# Common Mistakes

❌ Using preorder instead of postorder.

❌ Forgetting parent check in undirected trees.

❌ Recomputing child answers.

❌ Confusing subtree answer with global answer.

❌ Ignoring recursion stack space.

---

# Interview Mental Checklist

- Is the input a tree?
- Can every node compute its answer using children?
- What should DFS return?
- Do I need one state or two states?
- Is a global answer required?

---

# Pattern Summary

| Feature | Description |
|----------|-------------|
| State | `dp[node]`, `dp[node][2]` |
| Traversal | DFS (Postorder) |
| Core Idea | Combine child results |
| Time Complexity | Usually `O(N)` |
| Space | `O(H)` recursion |
| Common Topics | House Robber, Diameter, Maximum Path, Independent Set |

---

# Mastery Checklist

- [ ] Recognize Tree DP problems.
- [ ] Write DFS confidently.
- [ ] Understand postorder traversal.
- [ ] Learn Include/Exclude DP.
- [ ] Understand subtree DP.
- [ ] Learn rerooting basics.
- [ ] Solve House Robber III, Diameter, and Maximum Path Sum.

---

# Tree DP Variations

| Pattern | Example |
|----------|---------|
| Single State | Subtree Sum |
| Include / Exclude | House Robber III |
| Height DP | Diameter |
| Path DP | Maximum Path Sum |
| Rerooting DP | Tree Distances |
| DP on Rooted Tree | Independent Set |

---

# DFS Flow

```
DFS(node)

↓

Solve Left

↓

Solve Right

↓

Merge Answers

↓

Return DP Value
```

---

# Final Goal

After mastering Tree DP, you should be able to:

- Recognize subtree-based DP immediately.
- Design the correct DP state for each node.
- Use DFS to compute answers efficiently.
- Solve binary tree and general tree DP problems in **O(N)**.
- Confidently tackle Tree DP questions asked in Top MNCs, FinTech companies, and competitive programming.

---

> **Golden Rule:** If the answer for a node depends on the answers of its **children**, think **Tree Dynamic Programming**.