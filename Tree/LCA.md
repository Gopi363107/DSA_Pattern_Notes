# Lowest Common Ancestor (LCA) — Pattern Recognition Notes

---

# Definition

## Lowest Common Ancestor (LCA)

The LCA of two nodes `p` and `q` is:

```text
The lowest node in the tree that has both p and q as descendants
```

A node can also be a descendant of itself.

---

# Example

```text
        3
       / \
      5   1
     / \ / \
    6  2 0  8
      / \
     7   4
```

### LCA of 5 and 1

```text
3
```

### LCA of 7 and 4

```text
2
```

---

# Core Intuition

LCA problems are mainly about:

```text
Searching both subtrees
```

and determining:

```text
Where two paths meet
```

---

# Most Important Observation

If:

- one node is found in left subtree
- another node is found in right subtree

Then:

```text
Current node = LCA
```

This is the MAIN LCA pattern.

---

# When Should I Think About LCA?

Use LCA logic when:

- Need common parent/ancestor
- Need meeting point of two nodes
- Need path intersection
- Need subtree containing both nodes
- Need nearest shared ancestor

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "lowest common ancestor"
- "common parent"
- "common node"
- "ancestor"
- "both nodes"
- "meeting point"
- "shared path"
- "nearest common"
- "path intersection"
- "smallest subtree"

→ Think **LCA Pattern**

---

# Mental Model

Ask this question:

> “Am I searching for the node where two search paths combine?”

If YES:

```text
Think LCA immediately
```

---

# Core LCA Flow

```text
Left subtree contains one node
Right subtree contains one node
```

↓

```text
Current node becomes LCA
```

---

# Generic LCA Template

```java
TreeNode dfs(TreeNode root, TreeNode p, TreeNode q) {

    if(root == null) return null;

    if(root == p || root == q) {
        return root;
    }

    TreeNode left = dfs(root.left, p, q);
    TreeNode right = dfs(root.right, p, q);

    if(left != null && right != null) {
        return root;
    }

    return left != null ? left : right;
}
```

---

# Pattern 1 — Basic Binary Tree LCA

---

## Trigger

- common ancestor
- shared parent
- nearest common node

---

## Problem

LeetCode 236 — Lowest Common Ancestor of a Binary Tree

---

## Recognition

Three possibilities:

```text
1. Both nodes in left subtree
2. Both nodes in right subtree
3. One in left, one in right
```

Case 3:

```text
Current node = answer
```

Classic LCA pattern.

---

## Solution

```java
class Solution {

    public TreeNode lowestCommonAncestor(
        TreeNode root,
        TreeNode p,
        TreeNode q
    ) {

        if(root == null) return null;

        if(root == p || root == q) {
            return root;
        }

        TreeNode left =
            lowestCommonAncestor(root.left, p, q);

        TreeNode right =
            lowestCommonAncestor(root.right, p, q);

        if(left != null && right != null) {
            return root;
        }

        return left != null ? left : right;
    }
}
```

---

# Pattern 2 — LCA in BST

---

## Trigger

- BST ancestor
- ordered ancestor search
- BST property usage

---

## Problem

LeetCode 235 — Lowest Common Ancestor of a Binary Search Tree

---

## Recognition

BST gives:

```text
Left < Root < Right
```

So:

- both smaller → go left
- both larger → go right
- split happens → current node is LCA

---

## Solution

```java
class Solution {

    public TreeNode lowestCommonAncestor(
        TreeNode root,
        TreeNode p,
        TreeNode q
    ) {

        while(root != null) {

            if(p.val < root.val &&
               q.val < root.val) {

                root = root.left;
            }
            else if(p.val > root.val &&
                    q.val > root.val) {

                root = root.right;
            }
            else {
                return root;
            }
        }

        return null;
    }
}
```

---

# Pattern 3 — Smallest Subtree With All Deepest Nodes

---

## Trigger

- deepest nodes
- common subtree
- ancestor of deepest nodes

---

## Problem

LeetCode 865 — Smallest Subtree with all the Deepest Nodes

---

## Recognition

Need:

```text
LCA of deepest nodes
```

This combines:

- height calculation
- LCA logic

Classic advanced tree pattern.

---

## Solution

```java
class Solution {

    public TreeNode subtreeWithAllDeepest(TreeNode root) {

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

# Super Important Recognition Patterns

---

# 1. Split Point Pattern

If:

```text
One node found left
One node found right
```

→ Current node becomes LCA.

This is the MOST important pattern.

---

# 2. Path Intersection Problems

If question asks:

```text
Where do two paths meet?
```

→ Think LCA.

---

# 3. Common Ancestor Problems

If question involves:

```text
shared parent
nearest ancestor
common node
```

→ LCA pattern.

---

# 4. Deepest Node Ancestor Problems

If question mixes:

```text
deepest + ancestor
```

→ Usually:

```text
Height + LCA combined
```

---

# Important Interview Insight

Many hard tree problems secretly reduce to:

```text
Find the merge point of two recursive searches
```

That is exactly:

```text
LCA logic
```

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Parent depends on children | Postorder |
| Need common ancestor | LCA |
| BST sorted traversal | Inorder |
| Level traversal | BFS |

---

# Common Mistake

Students try storing full paths separately.

But recursive LCA naturally finds:

```text
The merge point directly
```

without extra space.

---

# One-Line Memory Trick

```text
LCA = Where two recursive paths meet
```

---

# Final Interview Insight

Most LCA problems are solved by recognizing:

```text
Where do the two searches split or merge?
```

That single observation solves many medium and hard tree interview questions asked at Meta, Google, Amazon, Uber, and top product companies.