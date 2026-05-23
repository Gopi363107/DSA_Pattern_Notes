# BST Insert / Delete Patterns — Recognition Notes

---

# Definition

BST insert/delete problems involve:

```text
Modifying Binary Search Tree structure
```

while maintaining:

```text
BST ordering property
```

BST rule:

```text
Left < Root < Right
```

must remain valid AFTER insertion/deletion.

---

# Core Intuition

BST operations behave like:

```text
Binary Search on a Tree
```

At every node we decide:

```text
Go left
Go right
OR
Modify current node
```

---

# Most Important Observation

BST problems mainly depend on:

```text
Ordering comparisons
```

which allow:

```text
Directional pruning
```

instead of full traversal.

---

# When Should I Think About BST Insert/Delete Pattern?

Use BST modification logic when:

- Need node insertion
- Need node deletion
- Need tree restructuring
- Need BST updates
- Need predecessor/successor replacement
- Need ordered modifications

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "insert into BST"
- "delete node"
- "remove node"
- "BST update"
- "maintain BST"
- "ordered insertion"
- "successor"
- "predecessor"

→ Think **BST Modification Pattern**

---

# Mental Model

Ask this question:

> “Can BST ordering help me decide traversal direction?”

If YES:

```text
Use BST-guided recursion
```

---

# Important BST Delete Cases

Deleting a node has:

```text
3 major cases
```

| Case | Action |
|---|---|
| No child | Remove node |
| One child | Replace with child |
| Two children | Replace using successor/predecessor |

---

# Generic BST Traversal Template

```java
if(val < root.val) {

    root.left = dfs(root.left);
}
else if(val > root.val) {

    root.right = dfs(root.right);
}
else {

    // modify current node
}
```

---

# Pattern 1 — Insert into BST

---

## Trigger

- BST insertion
- ordered insertion
- recursive placement

---

## Problem

LeetCode 701 — Insert into a Binary Search Tree

---

## Recognition

BST property determines:

```text
Correct insertion side
```

Insertion always happens at:

```text
Null position
```

Classic BST traversal pattern.

---

## Solution

```java
class Solution {

    public TreeNode insertIntoBST(
        TreeNode root,
        int val
    ) {

        if(root == null) {

            return new TreeNode(val);
        }

        if(val < root.val) {

            root.left =
                insertIntoBST(root.left, val);
        }
        else {

            root.right =
                insertIntoBST(root.right, val);
        }

        return root;
    }
}
```

---

# Pattern 2 — Delete Node in BST

---

## Trigger

- remove node
- BST deletion
- restructure BST

---

## Problem

LeetCode 450 — Delete Node in a BST

---

## Recognition

Need:

```text
Maintain BST ordering after deletion
```

Three deletion cases:

---

### Case 1 — No Child

```text
Return null
```

---

### Case 2 — One Child

```text
Return existing child
```

---

### Case 3 — Two Children

Replace with:

```text
Inorder successor
```

then delete successor node.

Classic BST restructuring pattern.

---

## Solution

```java
class Solution {

    public TreeNode deleteNode(
        TreeNode root,
        int key
    ) {

        if(root == null) return null;

        if(key < root.val) {

            root.left =
                deleteNode(root.left, key);
        }
        else if(key > root.val) {

            root.right =
                deleteNode(root.right, key);
        }
        else {

            if(root.left == null) {
                return root.right;
            }

            if(root.right == null) {
                return root.left;
            }

            TreeNode successor =
                min(root.right);

            root.val = successor.val;

            root.right =
                deleteNode(
                    root.right,
                    successor.val
                );
        }

        return root;
    }

    TreeNode min(TreeNode root) {

        while(root.left != null) {
            root = root.left;
        }

        return root;
    }
}
```

---

# Pattern 3 — Trim a Binary Search Tree

---

## Trigger

- range filtering
- BST pruning
- remove out-of-range nodes

---

## Problem

LeetCode 669 — Trim a Binary Search Tree

---

## Recognition

Need:

```text
Keep nodes only inside [low, high]
```

BST ordering helps prune entire subtrees.

Example:

```text
root.val < low
```

means:

```text
Entire left subtree is invalid
```

Classic BST pruning optimization.

---

## Solution

```java
class Solution {

    public TreeNode trimBST(
        TreeNode root,
        int low,
        int high
    ) {

        if(root == null) return null;

        if(root.val < low) {

            return trimBST(root.right,
                           low,
                           high);
        }

        if(root.val > high) {

            return trimBST(root.left,
                           low,
                           high);
        }

        root.left =
            trimBST(root.left,
                    low,
                    high);

        root.right =
            trimBST(root.right,
                    low,
                    high);

        return root;
    }
}
```

---

# Super Important Recognition Patterns

---

# 1. Directional Traversal Pattern

BST always asks:

```text
Should I go left or right?
```

This is the MAIN BST mindset.

---

# 2. Null Position Pattern

Insertion always happens at:

```text
First valid null location
```

---

# 3. Successor Replacement Pattern

Deletion with two children usually uses:

```text
Inorder successor
```

because successor preserves BST ordering.

---

# 4. Subtree Pruning Pattern

BST ordering can eliminate:

```text
Entire subtrees
```

without traversal.

Very important optimization.

---

# Important Interview Insight

Many BST modification problems are secretly:

```text
Pointer update problems
```

The challenge is correctly reconnecting:

```text
left/right subtree references
```

after recursion.

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| BST insertion | Directed recursion |
| BST deletion | Restructuring |
| Ordered traversal | Inorder |
| Level expansion | BFS |

---

# Common Mistake

Students often forget:

```text
Delete operation changes subtree roots
```

Always reassign:

```java
root.left = ...
root.right = ...
```

after recursive calls.

---

# One-Line Memory Trick

```text
BST Operations = Binary Search + Pointer Updates
```

---

# Final Interview Insight

Most BST modification problems become easy after recognizing:

```text
BST ordering gives traversal direction
```

That single observation simplifies:

- insertion
- deletion
- trimming
- splitting
- predecessor/successor
- range operations

This is one of the highest-frequency BST interview patterns asked at Meta, Google, Amazon, Uber, and top product companies.