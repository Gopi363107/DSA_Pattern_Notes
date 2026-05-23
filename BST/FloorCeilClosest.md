# BST Floor / Ceil / Closest Value Pattern — Recognition Notes

---

# Definition

Floor/Ceil problems involve finding values relative to a target.

---

# Important Definitions

| Concept | Meaning |
|---|---|
| Floor | Greatest value ≤ target |
| Ceil | Smallest value ≥ target |
| Closest Value | Minimum absolute difference from target |

These problems are extremely common in:

- BSTs
- Binary Search
- Ordered Sets/Maps
- Range Queries

---

# Core Intuition

BST ordering gives:

```text
Left < Root < Right
```

This allows us to:

```text
Move intelligently toward target
```

instead of traversing the full tree.

---

# Most Important Observation

While traversing BST:

```text
Current node may become:
- floor candidate
- ceil candidate
- closest candidate
```

We continuously update the best answer.

---

# When Should I Think About Floor/Ceil Pattern?

Use this pattern when:

- Need nearest smaller value
- Need nearest larger value
- Need closest target value
- Need predecessor/successor
- Need ordered nearest search
- Need range boundaries

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "closest"
- "nearest"
- "floor"
- "ceil"
- "lower bound"
- "upper bound"
- "minimum difference"
- "nearest smaller"
- "nearest larger"
- "closest value"

→ Think **Floor/Ceil Pattern**

---

# Mental Model

Ask this question:

> “Can BST ordering help eliminate half the search space?”

If YES:

```text
Use BST-guided traversal
```

---

# Important Traversal Logic

---

# Floor Logic

Need:

```text
Largest value <= target
```

---

## Cases

### If root.val == target

```text
Answer found directly
```

---

### If root.val < target

```text
Current node is a possible floor
Move RIGHT for larger valid candidate
```

---

### If root.val > target

```text
Move LEFT
```

because current node is too large.

---

# Ceil Logic

Need:

```text
Smallest value >= target
```

---

## Cases

### If root.val == target

```text
Answer found directly
```

---

### If root.val > target

```text
Current node is possible ceil
Move LEFT for smaller valid candidate
```

---

### If root.val < target

```text
Move RIGHT
```

because current node is too small.

---

# Generic Floor Template

```java
int floor = -1;

while(root != null) {

    if(root.val == target) {

        floor = root.val;
        break;
    }

    if(root.val < target) {

        floor = root.val;

        root = root.right;
    }
    else {

        root = root.left;
    }
}
```

---

# Generic Ceil Template

```java
int ceil = -1;

while(root != null) {

    if(root.val == target) {

        ceil = root.val;
        break;
    }

    if(root.val > target) {

        ceil = root.val;

        root = root.left;
    }
    else {

        root = root.right;
    }
}
```

---

# Pattern 1 — Closest Value in BST

---

## Trigger

- closest value
- nearest target
- minimum difference

---

## Problem

LeetCode 270 — Closest Binary Search Tree Value

---

## Recognition

Need:

```text
Minimum absolute difference
```

Update closest candidate while traversing toward target.

Classic BST nearest-search pattern.

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

# Pattern 2 — Minimum Absolute Difference in BST

---

## Trigger

- minimum difference
- closest pair
- nearest adjacent values

---

## Problem

LeetCode 530 — Minimum Absolute Difference in BST

---

## Recognition

BST inorder traversal gives:

```text
Sorted order
```

Closest values in sorted order are always:

```text
Adjacent values
```

Classic inorder ordering pattern.

---

## Solution

```java
class Solution {

    Integer prev = null;

    int minDiff = Integer.MAX_VALUE;

    public int getMinimumDifference(
        TreeNode root
    ) {

        dfs(root);

        return minDiff;
    }

    void dfs(TreeNode root) {

        if(root == null) return;

        dfs(root.left);

        if(prev != null) {

            minDiff =
                Math.min(
                    minDiff,
                    root.val - prev
                );
        }

        prev = root.val;

        dfs(root.right);
    }
}
```

---

# Pattern 3 — Inorder Successor in BST

---

## Trigger

- next greater node
- ceil-like search
- successor

---

## Problem

LeetCode 285 — Inorder Successor in BST

---

## Recognition

Need:

```text
Smallest node greater than target
```

This is basically:

```text
BST ceil logic
```

---

## Solution

```java
class Solution {

    public TreeNode inorderSuccessor(
        TreeNode root,
        TreeNode p
    ) {

        TreeNode ans = null;

        while(root != null) {

            if(root.val > p.val) {

                ans = root;

                root = root.left;
            }
            else {

                root = root.right;
            }
        }

        return ans;
    }
}
```

---

# Super Important Recognition Patterns

---

# 1. Candidate Update Pattern

During traversal:

```text
Current node may become best answer
```

Always update candidate BEFORE moving.

---

# 2. Directional Pruning Pattern

BST ordering eliminates:

```text
Half of search space
```

at every step.

This is the MAIN BST optimization.

---

# 3. Adjacent Sorted Pattern

In BST inorder traversal:

```text
Closest values appear adjacent
```

Very important observation.

---

# 4. Successor / Predecessor Pattern

| Concept | Meaning |
|---|---|
| Successor | Next greater value |
| Predecessor | Next smaller value |

These are basically:

```text
Ceil / Floor problems
```

---

# Important Interview Insight

Many BST nearest-value problems are secretly:

```text
Binary Search problems on trees
```

The tree structure behaves like:

```text
Sorted Array Navigation
```

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Closest value | BST traversal |
| Minimum difference | Inorder |
| Successor | Ceil logic |
| Predecessor | Floor logic |
| Distance K | BFS |

---

# Common Mistake

Students often perform:

```text
Full DFS traversal
```

even though BST ordering allows:

```text
O(height)
```

optimized solutions.

Always use BST property.

---

# One-Line Memory Trick

```text
Floor → nearest smaller
Ceil → nearest larger
Closest → minimum difference
```

---

# Final Interview Insight

Most floor/ceil interview problems become easy after recognizing:

```text
BST allows directional pruning
```

That single observation simplifies:

- predecessor/successor
- closest value
- range queries
- nearest search
- lower/upper bounds

This is one of the highest-frequency BST interview patterns asked at Meta, Google, Amazon, Uber, and top product companies.