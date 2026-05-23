# BST Validation Patterns — Recognition Notes

---

# Definition

BST validation problems involve checking whether a tree satisfies:

```text
Binary Search Tree properties
```

A valid BST follows:

```text
Left Subtree  < Root < Right Subtree
```

for EVERY node.

---

# Core Intuition

Most BST validation problems depend on:

```text
Ordering relationships
```

between nodes.

The MOST important property is:

```text
Inorder traversal of BST is strictly increasing
```

This is the MAIN BST validation pattern.

---

# Most Important Observation

BST validation is NOT just:

```text
left child < parent < right child
```

It is:

```text
ALL nodes in left subtree < current node
ALL nodes in right subtree > current node
```

This is the BIGGEST interview mistake.

---

# When Should I Think About BST Validation?

Use BST validation logic when:

- Need to verify BST property
- Need ordered traversal checking
- Need subtree range checking
- Need increasing sequence validation
- Need BST correction/recovery
- Need BST constraint propagation

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "validate BST"
- "binary search tree"
- "increasing order"
- "sorted traversal"
- "BST property"
- "recover BST"
- "invalid node"
- "ordered tree"
- "strictly increasing"

→ Think **BST Validation Pattern**

---

# Mental Model

Ask this question:

> “Does every node need to satisfy ordering constraints?”

If YES:

```text
Think BST validation
```

---

# Two Major BST Validation Approaches

| Approach | Core Idea |
|---|---|
| Inorder Traversal | Sequence must be increasing |
| Min/Max Range | Node must stay within valid range |

---

# Pattern 1 — Inorder Validation

---

## Trigger

- increasing order
- sorted traversal
- inorder checking

---

## Problem

LeetCode 98 — Validate Binary Search Tree

---

## Recognition

Inorder traversal of BST gives:

```text
strictly increasing sequence
```

If current node becomes:

```text
<= previous node
```

BST becomes invalid.

Classic inorder validation pattern.

---

## Solution

```java
class Solution {

    TreeNode prev = null;

    public boolean isValidBST(TreeNode root) {

        if(root == null) return true;

        if(!isValidBST(root.left)) {
            return false;
        }

        if(prev != null &&
           root.val <= prev.val) {

            return false;
        }

        prev = root;

        return isValidBST(root.right);
    }
}
```

---

# Pattern 2 — Min/Max Range Validation

---

## Trigger

- subtree constraints
- recursive ranges
- BST bounds checking

---

## Problem

LeetCode 98 — Validate Binary Search Tree

---

## Recognition

Every node must stay inside:

```text
(min, max)
```

ranges inherited from ancestors.

Example:

```text
Left subtree → smaller than ancestor
Right subtree → larger than ancestor
```

Classic constraint propagation pattern.

---

## Solution

```java
class Solution {

    public boolean isValidBST(TreeNode root) {

        return dfs(root, Long.MIN_VALUE,
                         Long.MAX_VALUE);
    }

    boolean dfs(
        TreeNode root,
        long min,
        long max
    ) {

        if(root == null) return true;

        if(root.val <= min ||
           root.val >= max) {

            return false;
        }

        return dfs(root.left,
                   min,
                   root.val)

            && dfs(root.right,
                   root.val,
                   max);
    }
}
```

---

# Pattern 3 — Recover Binary Search Tree

---

## Trigger

- swapped nodes
- corrupted BST
- recover ordering

---

## Problem

LeetCode 99 — Recover Binary Search Tree

---

## Recognition

Inorder traversal should be:

```text
sorted
```

Swapped nodes create:

```text
ordering violations
```

Need to detect:

```text
prev.val > current.val
```

Classic inorder anomaly detection.

---

## Solution

```java
class Solution {

    TreeNode first = null;
    TreeNode second = null;
    TreeNode prev = null;

    public void recoverTree(TreeNode root) {

        dfs(root);

        int temp = first.val;

        first.val = second.val;

        second.val = temp;
    }

    void dfs(TreeNode root) {

        if(root == null) return;

        dfs(root.left);

        if(prev != null &&
           prev.val > root.val) {

            if(first == null) {
                first = prev;
            }

            second = root;
        }

        prev = root;

        dfs(root.right);
    }
}
```

---

# Super Important Recognition Patterns

---

# 1. Sorted Inorder Pattern

If question involves:

```text
sorted
increasing
ordered
BST traversal
```

→ Think:

```text
Inorder traversal
```

---

# 2. Constraint Propagation Pattern

If node validity depends on:

```text
ancestor ranges
```

→ Think:

```text
Min/Max recursion
```

---

# 3. Ordering Violation Pattern

If question involves:

```text
invalid BST
swapped nodes
corruption
```

→ Think:

```text
Inorder ordering break
```

---

# 4. BST Property Pattern

Remember:

```text
BST property applies to ENTIRE subtree
```

NOT just immediate children.

---

# Important Interview Insight

Many BST problems are secretly:

```text
Ordered sequence problems
```

because BST inorder traversal behaves like:

```text
Sorted Array
```

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Need sorted traversal | Inorder |
| Need subtree ranges | Min/Max DFS |
| Need subtree aggregation | Postorder |
| Need shortest path | BFS |

---

# Common Mistake

WRONG validation:

```text
left child < root < right child
```

Correct validation:

```text
ALL left subtree nodes < root
ALL right subtree nodes > root
```

This mistake causes many interview failures.

---

# One-Line Memory Trick

```text
Valid BST = Strictly increasing inorder traversal
```

---

# Final Interview Insight

Most BST validation problems become easier after recognizing:

```text
BST behaves like a sorted structure
```

That single observation helps solve:

- validation
- recovery
- kth smallest
- BST iterators
- predecessor/successor
- closest value

This is one of the highest-frequency tree interview patterns asked at Meta, Google, Amazon, Uber, and top product companies.