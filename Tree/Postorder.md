# Postorder DFS — Pattern Recognition Notes

---

# Definition

## Traversal Order

```text
Left → Right → Root
```

## Core Idea

> Process the current node AFTER exploring both children.

---

# When Should I Use Postorder DFS?

Use postorder when:

- You need information from children before processing parent
- You are solving bottom-up problems
- You need subtree calculations
- You are deleting/freeing trees
- Parent answer depends on child answers
- You are doing tree DP

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "height"
- "diameter"
- "subtree"
- "maximum path"
- "balanced"
- "depth"
- "calculate from children"
- "bottom-up"
- "merge results"
- "aggregate"

→ Think **Postorder DFS**

---

# Mental Model

Ask this question:

> “Do I need answers from children BEFORE processing the current node?”

If YES → postorder is likely correct.

---

# Core Intuition

Postorder is mainly used for:

```text
Child → Parent information flow
```

Children compute first.

Parent uses those results later.

---

# General Postorder Template

```java
int dfs(TreeNode root) {

    if(root == null) return 0;

    int left = dfs(root.left);
    int right = dfs(root.right);

    // process current node using child results

    return someValue;
}
```

---

# Pattern 1 — Height / Depth Calculation

---

## Trigger

- height
- depth
- longest path
- subtree height

---

## Problem

LeetCode 104 — Maximum Depth of Binary Tree

---

## Recognition

To calculate current node height:

```text
current = max(leftHeight, rightHeight) + 1
```

We need child heights first.

So postorder fits naturally.

---

## Solution

```java
class Solution {

    public int maxDepth(TreeNode root) {

        if(root == null) return 0;

        int left = maxDepth(root.left);
        int right = maxDepth(root.right);

        return Math.max(left, right) + 1;
    }
}
```

---

# Pattern 2 — Balanced Binary Tree

---

## Trigger

- balance checking
- subtree validation
- compare left/right subtree

---

## Problem

LeetCode 110 — Balanced Binary Tree

---

## Recognition

To check balance at current node:

```text
abs(leftHeight - rightHeight) <= 1
```

Need child subtree heights first.

Bottom-up flow.

Postorder pattern.

---

## Solution

```java
class Solution {

    public boolean isBalanced(TreeNode root) {

        return dfs(root) != -1;
    }

    int dfs(TreeNode root) {

        if(root == null) return 0;

        int left = dfs(root.left);

        if(left == -1) return -1;

        int right = dfs(root.right);

        if(right == -1) return -1;

        if(Math.abs(left - right) > 1) {
            return -1;
        }

        return Math.max(left, right) + 1;
    }
}
```

---

# Pattern 3 — Diameter of Binary Tree

---

## Trigger

- longest path
- subtree contribution
- path through current node

---

## Problem

LeetCode 543 — Diameter of Binary Tree

---

## Recognition

Diameter at current node:

```text
leftHeight + rightHeight
```

Need child heights first.

Classic postorder problem.

---

## Solution

```java
class Solution {

    int diameter = 0;

    public int diameterOfBinaryTree(TreeNode root) {

        dfs(root);

        return diameter;
    }

    int dfs(TreeNode root) {

        if(root == null) return 0;

        int left = dfs(root.left);
        int right = dfs(root.right);

        diameter = Math.max(diameter, left + right);

        return Math.max(left, right) + 1;
    }
}
```

---

# Important Interview Insight

Most hard tree problems are:

```text
Bottom-up calculations
```

This is where postorder dominates.

---

# Quick Comparison

| Situation | Use |
|---|---|
| Need children first | Postorder |
| Need parent first | Preorder |
| Need BST sorted order | Inorder |

---

# Super Important Recognition Shortcut

## Use Postorder When:

```text
Children → Parent information flow
```

---

## Examples

- height calculation
- diameter
- balanced tree
- maximum path sum
- subtree DP
- tree deletion
- lowest common ancestor variations

---

# Common Mistake

Students often try preorder for subtree calculations.

But if parent depends on child answers:

```text
ALWAYS think Postorder first
```

---

# One-Line Memory Trick

```text
Postorder = "Solve children first, then parent"
```

---

# Final Interview Insight

Many difficult tree problems become easy after recognizing:

```text
Bottom-up computation
```

That usually means:

```text
Postorder DFS
```

This is one of the strongest advanced tree patterns asked in interviews at Meta, Google, Amazon, and top product-based companies.