# Lowest Common Ancestor in BST — Pattern Recognition Notes

---

# Definition

LCA in BST problems involve finding:

```text
The lowest node where two target nodes split
```

inside a:

```text
Binary Search Tree
```

Unlike normal binary tree LCA:

```text
BST ordering property helps optimize search
```

---

# Core Intuition

BST property:

```text
Left < Root < Right
```

This allows us to decide:

```text
Go left
Go right
OR
Current node is answer
```

without exploring both subtrees.

---

# Most Important Observation

The FIRST node where:

```text
p and q go in different directions
```

becomes:

```text
LCA
```

This is the MAIN BST-LCA pattern.

---

# Example

```text
          6
        /   \
       2     8
      / \   / \
     0   4 7   9
        / \
       3   5
```

### LCA of 2 and 8

```text
6
```

because:

```text
2 is left
8 is right
```

Split happens at 6.

---

# When Should I Think About BST LCA?

Use BST LCA logic when:

- Tree is BST
- Need common ancestor
- Need split point
- Need optimized ancestor search
- Need nearest common parent

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "lowest common ancestor"
- "BST"
- "split point"
- "common parent"
- "nearest common ancestor"
- "ancestor search"
- "binary search tree"

→ Think **BST LCA Pattern**

---

# Mental Model

Ask this question:

> “Are both nodes on the same side of the current BST node?”

If YES:

```text
Continue search in that side
```

If NO:

```text
Current node becomes LCA
```

---

# Key BST-LCA Cases

| Situation | Action |
|---|---|
| Both smaller than root | Go left |
| Both greater than root | Go right |
| Split occurs | Current node = LCA |

---

# Generic BST LCA Template

```java
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
```

---

# Pattern 1 — Basic BST LCA

---

## Trigger

- BST ancestor
- split node
- nearest common node

---

## Problem

LeetCode 235 — Lowest Common Ancestor of a Binary Search Tree

---

## Recognition

BST ordering avoids:

```text
Searching both subtrees
```

because BST tells exactly:

```text
Which direction to move
```

Classic BST-guided traversal.

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

# Pattern 2 — Closest Value in BST

---

## Trigger

- closest node
- nearest value
- BST navigation

---

## Problem

LeetCode 270 — Closest Binary Search Tree Value

---

## Recognition

Same BST navigation idea:

```text
Move only toward useful side
```

instead of full traversal.

This is another BST-direction optimization pattern.

---

## Solution

```java
class Solution {

    public int closestValue(
        TreeNode root,
        double target
    ) {

        int closest = root.val;

        while(root != null) {

            if(Math.abs(root.val - target)
               < Math.abs(closest - target)) {

                closest = root.val;
            }

            if(target < root.val) {
                root = root.left;
            }
            else {
                root = root.right;
            }
        }

        return closest;
    }
}
```

---

# Pattern 3 — Split BST

---

## Trigger

- divide BST
- partition tree
- split by value

---

## Problem

LeetCode 776 — Split BST

---

## Recognition

Need:

```text
Separate nodes:
<= target
> target
```

BST ordering helps recursively split.

Classic BST partitioning pattern.

---

## Solution

```java
class Solution {

    public TreeNode[] splitBST(
        TreeNode root,
        int target
    ) {

        if(root == null) {

            return new TreeNode[]{
                null,
                null
            };
        }

        if(root.val <= target) {

            TreeNode[] arr =
                splitBST(root.right, target);

            root.right = arr[0];

            return new TreeNode[]{
                root,
                arr[1]
            };
        }
        else {

            TreeNode[] arr =
                splitBST(root.left, target);

            root.left = arr[1];

            return new TreeNode[]{
                arr[0],
                root
            };
        }
    }
}
```

---

# Super Important Recognition Patterns

---

# 1. Split Point Pattern

If:

```text
One node goes left
One node goes right
```

→ Current node becomes:

```text
LCA
```

This is the MOST important BST-LCA observation.

---

# 2. Same Side Pattern

If both nodes are:

```text
smaller
OR
greater
```

→ Continue only in one subtree.

---

# 3. BST Navigation Pattern

BST problems often avoid:

```text
Full DFS traversal
```

because ordering gives:

```text
Directional pruning
```

---

# 4. Binary Search on Tree Pattern

BST traversal behaves like:

```text
Binary Search
```

This is why many BST problems become:

```text
O(height)
```

instead of:

```text
O(n)
```

---

# Important Interview Insight

Many BST problems are secretly:

```text
Directional decision problems
```

You repeatedly ask:

```text
Should I go left?
Should I go right?
Or stop here?
```

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Normal tree LCA | Postorder DFS |
| BST LCA | BST traversal |
| Sorted order traversal | Inorder |
| Level expansion | BFS |

---

# Common Mistake

Students sometimes solve BST-LCA using:

```text
Normal binary tree LCA
```

which becomes:

```text
O(n)
```

But BST property gives:

```text
O(height)
```

optimized solution.

---

# One-Line Memory Trick

```text
BST LCA = First split point
```

---

# Final Interview Insight

Most BST ancestor problems become easy after recognizing:

```text
BST gives directional pruning
```

That single observation simplifies:

- LCA
- closest value
- insert/delete
- predecessor/successor
- range search
- split operations

This is one of the highest-frequency BST interview patterns asked at Meta, Google, Amazon, Uber, and top product companies.