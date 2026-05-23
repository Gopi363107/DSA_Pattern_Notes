# Inorder DFS — Pattern Recognition Notes

---

# Definition

## Traversal Order

```text
Left → Root → Right
```

## Core Idea

> Process the current node BETWEEN exploring left and right children.

---

# When Should I Use Inorder DFS?

Use inorder when:

- You need nodes in sorted order
- You are working with BST properties
- You need kth smallest/largest element
- You need ordered traversal
- You must process left side before current node

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "sorted"
- "BST"
- "kth smallest"
- "increasing order"
- "ascending"
- "validate BST"
- "minimum difference"
- "ordered traversal"

→ Think **Inorder DFS**

---

# Mental Model

Ask this question:

> “Do I need the left subtree processed BEFORE the current node?”

If YES → inorder is likely correct.

---

# Most Important Property

## Inorder Traversal of BST Gives Sorted Order

Example:

```text
        4
       / \
      2   6
     / \ / \
    1  3 5  7
```

Inorder:

```text
1 2 3 4 5 6 7
```

This is the BIGGEST inorder pattern.

---

# General Inorder Template

```java
void dfs(TreeNode root) {

    if(root == null) return;

    dfs(root.left);

    // process current node

    dfs(root.right);
}
```

---

# Pattern 1 — BST Sorted Traversal

---

## Trigger

- Sorted output
- Increasing order
- BST traversal
- Ordered processing

---

## Problem

LeetCode 94 — Binary Tree Inorder Traversal

---

## Recognition

In BST:

```text
Left < Root < Right
```

So visiting:

```text
Left → Root → Right
```

naturally gives sorted order.

---

## Solution

```java
class Solution {

    List<Integer> ans = new ArrayList<>();

    public List<Integer> inorderTraversal(TreeNode root) {

        dfs(root);

        return ans;
    }

    void dfs(TreeNode root) {

        if(root == null) return;

        dfs(root.left);

        ans.add(root.val);

        dfs(root.right);
    }
}
```

---

# Pattern 2 — Validate BST

---

## Trigger

- BST validation
- Increasing sequence checking
- Previous node comparison

---

## Problem

LeetCode 98 — Validate Binary Search Tree

---

## Recognition

Valid BST inorder traversal must be:

```text
strictly increasing
```

If current value becomes smaller than previous value:

→ BST is invalid.

---

## Solution

```java
class Solution {

    TreeNode prev = null;

    public boolean isValidBST(TreeNode root) {

        if(root == null) return true;

        if(!isValidBST(root.left)) return false;

        if(prev != null && root.val <= prev.val) {
            return false;
        }

        prev = root;

        return isValidBST(root.right);
    }
}
```

---

# Pattern 3 — Kth Smallest Element in BST

---

## Trigger

- kth smallest
- kth largest
- ordered counting
- sorted traversal

---

## Problem

LeetCode 230 — Kth Smallest Element in a BST

---

## Recognition

Inorder traversal gives sorted order.

So:

- 1st visited node = smallest
- 2nd visited node = second smallest
- kth visited node = kth smallest

---

## Solution

```java
class Solution {

    int count = 0;
    int ans = 0;

    public int kthSmallest(TreeNode root, int k) {

        dfs(root, k);

        return ans;
    }

    void dfs(TreeNode root, int k) {

        if(root == null) return;

        dfs(root.left, k);

        count++;

        if(count == k) {
            ans = root.val;
            return;
        }

        dfs(root.right, k);
    }
}
```

---

# Important Interview Insight

Most inorder problems are connected to:

```text
BST + Sorted Order
```

This is the MAIN inorder pattern.

---

# Quick Comparison

| Situation | Use |
|---|---|
| Need sorted order | Inorder |
| Need parent first | Preorder |
| Need children first | Postorder |

---

# Super Important Recognition Shortcut

## Use Inorder When:

```text
Left side must finish BEFORE current node
```

---

## Examples

- BST validation
- kth smallest
- sorted traversal
- minimum difference in BST
- recovering BST
- inorder iterator

---

# Common Mistake

Students often use preorder/postorder for BST problems.

But if the problem says:

```text
sorted / kth / increasing / BST
```

→ Inorder is usually the correct first thought.

---

# One-Line Memory Trick

```text
Inorder = "Sorted order in BST"
```

---

# Final Interview Insight

Many BST interview problems are solved by recognizing:

```text
BST → Inorder → Sorted Sequence
```

This is one of the highest-frequency tree patterns asked in interviews at Meta, Google, Amazon, and top product companies.