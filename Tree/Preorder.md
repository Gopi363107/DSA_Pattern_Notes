# Preorder DFS — Pattern Recognition Notes

---

# Definition

## Traversal Order

```text
Root → Left → Right
```

## Core Idea

> Process the current node BEFORE exploring children.

---

# When Should I Use Preorder DFS?

Use preorder when:

- You need information from the parent before visiting children
- You are building paths
- You are constructing/modifying structures top-down
- You need to carry state from root to child
- You are doing backtracking

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "root to leaf"
- "build"
- "construct"
- "serialize"
- "flatten"
- "path"
- "accumulate"
- "prefix"
- "carry forward"
- "top-down"

→ Think **Preorder DFS**

---

# Mental Model

Ask this question:

> “Do I need the current node value before exploring children?”

If YES → preorder is likely correct.

---

# General Preorder Template

```java
void dfs(TreeNode root) {

    if(root == null) return;

    // process current node

    dfs(root.left);
    dfs(root.right);
}
```

---

# Pattern 1 — Root to Leaf Path Building

---

## Trigger

- Generate paths
- Carry string/list/sum from parent to child
- Need path before going deeper

---

## Problem

LeetCode 257 — Binary Tree Paths

---

## Recognition

We must:

- Start from root
- Add current node to path
- Continue deeper

Current node must be processed first.

So preorder fits naturally.

---

## Solution

```java
class Solution {

    List<String> ans = new ArrayList<>();

    public List<String> binaryTreePaths(TreeNode root) {

        dfs(root, "");

        return ans;
    }

    void dfs(TreeNode root, String path) {

        if(root == null) return;

        path += root.val;

        if(root.left == null && root.right == null) {

            ans.add(path);

            return;
        }

        path += "->";

        dfs(root.left, path);
        dfs(root.right, path);
    }
}
```

---

# Pattern 2 — Carrying Running Information

---

## Trigger

- Running sum
- Prefix sum
- Depth/count tracking
- Parent affects child computation

---

## Problem

LeetCode 112 — Path Sum

---

## Recognition

We subtract current node value BEFORE exploring children.

That means parent information flows downward.

Preorder pattern.

---

## Solution

```java
class Solution {

    public boolean hasPathSum(TreeNode root, int targetSum) {

        if(root == null) return false;

        targetSum -= root.val;

        if(root.left == null && root.right == null) {

            return targetSum == 0;
        }

        return hasPathSum(root.left, targetSum) ||
               hasPathSum(root.right, targetSum);
    }
}
```

---

# Pattern 3 — Tree Modification / Construction

---

## Trigger

- Modify tree while traversing
- Build structure top-down
- Parent rearranges children

---

## Problem

LeetCode 114 — Flatten Binary Tree to Linked List

---

## Recognition

We process current node and rearrange links.

Structure changes from top to bottom.

Preorder thinking is important.

---

## Solution

```java
class Solution {

    TreeNode prev = null;

    public void flatten(TreeNode root) {

        if(root == null) return;

        flatten(root.right);
        flatten(root.left);

        root.right = prev;
        root.left = null;

        prev = root;
    }
}
```

---

# Important Interview Insight

Many tree problems are actually one of these:

| Pattern | Traversal |
|---|---|
| Top-down flow | Preorder |
| Bottom-up calculation | Postorder |

---

# Quick Comparison

| Situation | Use |
|---|---|
| Need parent first | Preorder |
| Need children first | Postorder |
| BST sorted order | Inorder |

---

# Super Important Recognition Shortcut

## Use Preorder When:

```text
Parent → Child information flow
```

---

## Examples

- path sum
- depth tracking
- path generation
- serialization
- top-down DP
- backtracking

---

# One-Line Memory Trick

```text
Preorder = "Do first, then explore"
```

---

# Final Interview Insight

Many hard tree problems are solved by recognizing:

```text
Top-down or Bottom-up
```

- Top-down → Preorder
- Bottom-up → Postorder

This is one of the strongest tree pattern recognitions for interviews at Meta, Google, and Amazon.