# Tree Transformation Patterns — Recognition Notes

---

# Definition

Tree transformation problems involve:

```text
Modifying the structure or values of a tree
```

Examples:

- flattening
- inverting
- rearranging
- converting
- serializing
- deleting
- rebuilding links

The tree changes during traversal.

---

# Core Intuition

Transformation problems usually involve:

```text
Updating current node connections
```

while traversing the tree.

Most commonly:

```text
Preorder DFS
```

because parent modifications happen BEFORE children.

Sometimes:

```text
Postorder DFS
```

is used when child transformations must finish first.

---

# Most Important Observation

Transformation problems usually ask:

```text
How should the current node change?
```

based on:

- child structure
- traversal order
- parent relationship

---

# When Should I Think About Tree Transformation?

Use transformation logic when:

- Tree structure changes
- Need pointer rewiring
- Need flattening/conversion
- Need mirror/invert operations
- Need serialization/deserialization
- Need node deletion/replacement
- Need tree reshaping

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "flatten"
- "invert"
- "convert"
- "transform"
- "serialize"
- "deserialize"
- "delete nodes"
- "rearrange"
- "modify tree"
- "change structure"
- "replace values"
- "mirror"

→ Think **Tree Transformation Pattern**

---

# Mental Model

Ask this question:

> “Am I modifying node links or values during traversal?”

If YES:

```text
Think Tree Transformation
```

---

# Important Transformation Categories

| Transformation Type | Common Traversal |
|---|---|
| Top-down rewiring | Preorder |
| Child-first restructuring | Postorder |
| Level transformations | BFS |
| Serialization | DFS/BFS |

---

# Pattern 1 — Invert Binary Tree

---

## Trigger

- mirror tree
- swap children
- invert structure

---

## Problem

LeetCode 226 — Invert Binary Tree

---

## Recognition

Need:

```text
Swap left and right children
```

at every node.

Transformation happens directly at current node.

Classic transformation pattern.

---

## Solution

```java
class Solution {

    public TreeNode invertTree(TreeNode root) {

        if(root == null) return null;

        TreeNode temp = root.left;

        root.left = root.right;

        root.right = temp;

        invertTree(root.left);
        invertTree(root.right);

        return root;
    }
}
```

---

# Pattern 2 — Add One Row to Tree

---

## Trigger

- insert nodes
- restructure levels
- modify child links

---

## Problem

LeetCode 623 — Add One Row to Tree

---

## Recognition

Need:

```text
Insert new nodes at a specific depth
```

and reconnect existing children.

Classic pointer rewiring problem.

---

## Solution

```java
class Solution {

    public TreeNode addOneRow(
        TreeNode root,
        int val,
        int depth
    ) {

        if(depth == 1) {

            TreeNode node =
                new TreeNode(val);

            node.left = root;

            return node;
        }

        dfs(root, val, 1, depth);

        return root;
    }

    void dfs(
        TreeNode root,
        int val,
        int level,
        int depth
    ) {

        if(root == null) return;

        if(level == depth - 1) {

            TreeNode left =
                new TreeNode(val);

            TreeNode right =
                new TreeNode(val);

            left.left = root.left;

            right.right = root.right;

            root.left = left;

            root.right = right;

            return;
        }

        dfs(root.left, val,
            level + 1, depth);

        dfs(root.right, val,
            level + 1, depth);
    }
}
```

---

# Pattern 3 — Delete Leaves With a Given Value

---

## Trigger

- delete nodes
- remove subtree
- child cleanup
- recursive deletion

---

## Problem

LeetCode 1325 — Delete Leaves With a Given Value

---

## Recognition

Need:

```text
Delete child nodes first
```

because current node may become a leaf AFTER deletion.

Classic:

```text
Postorder Transformation
```

---

## Solution

```java
class Solution {

    public TreeNode removeLeafNodes(
        TreeNode root,
        int target
    ) {

        if(root == null) return null;

        root.left =
            removeLeafNodes(
                root.left,
                target
            );

        root.right =
            removeLeafNodes(
                root.right,
                target
            );

        if(root.left == null &&
           root.right == null &&
           root.val == target) {

            return null;
        }

        return root;
    }
}
```

---

# Super Important Recognition Patterns

---

# 1. Pointer Rewiring Pattern

If problem modifies:

```text
left/right child links
```

→ Think:

```text
Transformation problem
```

---

# 2. Current Node Modification Pattern

If current node changes:

```text
before children
```

→ Usually:

```text
Preorder DFS
```

---

# 3. Child Cleanup Pattern

If current node depends on:

```text
already transformed children
```

→ Usually:

```text
Postorder DFS
```

---

# 4. Tree Reshaping Pattern

If problem involves:

```text
flatten
mirror
convert
rearrange
```

→ Think:

```text
Recursive structure transformation
```

---

# Important Interview Insight

Many transformation problems are secretly:

```text
Pointer manipulation problems
```

The real challenge is correctly updating:

```text
left/right references
```

during recursion.

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Parent modifies first | Preorder |
| Child cleanup first | Postorder |
| Level-wise modification | BFS |
| Tree reconstruction | Construction Pattern |

---

# Common Mistake

Students often forget:

```text
Recursive calls can change child references
```

Always reassign:

```java
root.left = dfs(root.left);
root.right = dfs(root.right);
```

when subtree structure may change.

---

# One-Line Memory Trick

```text
Transformation Problems = Modify tree during traversal
```

---

# Final Interview Insight

Most difficult transformation problems become easier after identifying:

```text
Should modification happen:
Before recursion?
OR
After recursion?
```

That single decision determines:

```text
Traversal order
Pointer handling
Recursion flow
```

This is one of the most important recursive tree patterns asked at Meta, Google, Amazon, Uber, and top product companies.