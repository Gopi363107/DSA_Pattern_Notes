# Tree Construction — Pattern Recognition Notes

---

# Definition

Tree construction problems involve:

```text
Building/Reconstructing a tree
```

using:

- traversal arrays
- parent-child relations
- preorder/inorder/postorder
- BST properties
- recursion boundaries

---

# Core Intuition

Most tree construction problems follow:

```text
Create current node first
```

then recursively build:

```text
Left subtree
Right subtree
```

This is mainly a:

```text
Preorder DFS Pattern
```

because we process parent nodes before children.

---

# When Should I Think About Tree Construction?

Use tree construction logic when:

- Need to rebuild tree
- Given traversal arrays
- Need recursive partitioning
- Need subtree boundaries
- Need to create nodes recursively
- Need top-down tree building

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "construct tree"
- "build tree"
- "reconstruct"
- "deserialize"
- "recover tree"
- "create BST"
- "given preorder"
- "given inorder"
- "given postorder"
- "convert array to BST"

→ Think **Tree Construction Pattern**

---

# Mental Model

Ask this question:

> “Am I creating the current node before recursively building children?”

If YES:

```text
Preorder-style construction is likely involved
```

---

# Most Important Construction Observation

Traversal arrays determine:

```text
1. Current root
2. Left subtree range
3. Right subtree range
```

That is the MAIN construction pattern.

---

# Generic Construction Template

```java
TreeNode build(...) {

    if(base condition) return null;

    TreeNode root = new TreeNode(...);

    root.left = build(...);

    root.right = build(...);

    return root;
}
```

---

# Pattern 1 — Build Tree from Preorder + Inorder

---

## Trigger

- preorder + inorder
- reconstruct binary tree
- traversal rebuilding

---

## Problem

LeetCode 105 — Construct Binary Tree from Preorder and Inorder Traversal

---

## Recognition

### Key Observations

Preorder gives:

```text
Root first
```

Inorder gives:

```text
Left | Root | Right
```

Steps:

1. Take root from preorder
2. Find root position in inorder
3. Left side = left subtree
4. Right side = right subtree

Classic recursive partitioning pattern.

---

## Solution

```java
class Solution {

    int preIndex = 0;

    HashMap<Integer, Integer> map = new HashMap<>();

    public TreeNode buildTree(
        int[] preorder,
        int[] inorder
    ) {

        for(int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }

        return dfs(preorder, 0, inorder.length - 1);
    }

    TreeNode dfs(
        int[] preorder,
        int left,
        int right
    ) {

        if(left > right) return null;

        int rootVal = preorder[preIndex++];

        TreeNode root = new TreeNode(rootVal);

        int mid = map.get(rootVal);

        root.left =
            dfs(preorder, left, mid - 1);

        root.right =
            dfs(preorder, mid + 1, right);

        return root;
    }
}
```

---

# Pattern 2 — Build Tree from Inorder + Postorder

---

## Trigger

- inorder + postorder
- reconstruct using postorder

---

## Problem

LeetCode 106 — Construct Binary Tree from Inorder and Postorder Traversal

---

## Recognition

Postorder gives:

```text
Root at the END
```

So:

1. Take root from postorder backward
2. Partition inorder
3. Build RIGHT subtree first
4. Then LEFT subtree

Right-first is important.

---

## Solution

```java
class Solution {

    int postIndex;

    HashMap<Integer, Integer> map =
        new HashMap<>();

    public TreeNode buildTree(
        int[] inorder,
        int[] postorder
    ) {

        postIndex = postorder.length - 1;

        for(int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }

        return dfs(postorder, 0, inorder.length - 1);
    }

    TreeNode dfs(
        int[] postorder,
        int left,
        int right
    ) {

        if(left > right) return null;

        int rootVal = postorder[postIndex--];

        TreeNode root = new TreeNode(rootVal);

        int mid = map.get(rootVal);

        root.right =
            dfs(postorder, mid + 1, right);

        root.left =
            dfs(postorder, left, mid - 1);

        return root;
    }
}
```

---

# Pattern 3 — Convert Sorted Array to BST

---

## Trigger

- sorted array
- balanced BST
- binary search construction

---

## Problem

LeetCode 108 — Convert Sorted Array to Binary Search Tree

---

## Recognition

Sorted array means:

```text
Middle element becomes root
```

because BST requires:

```text
Left < Root < Right
```

This becomes:

```text
Binary Search + Recursion
```

---

## Solution

```java
class Solution {

    public TreeNode sortedArrayToBST(int[] nums) {

        return dfs(nums, 0, nums.length - 1);
    }

    TreeNode dfs(int[] nums, int left, int right) {

        if(left > right) return null;

        int mid = left + (right - left) / 2;

        TreeNode root = new TreeNode(nums[mid]);

        root.left = dfs(nums, left, mid - 1);

        root.right = dfs(nums, mid + 1, right);

        return root;
    }
}
```

---

# Super Important Recognition Patterns

---

# 1. Traversal Partition Pattern

If question gives:

```text
preorder + inorder
postorder + inorder
```

→ Think:

```text
Partition inorder into left/right subtrees
```

---

# 2. Root Identification Pattern

Remember:

| Traversal | Root Position |
|---|---|
| Preorder | Beginning |
| Postorder | End |

This decides construction direction.

---

# 3. Recursive Range Pattern

Construction problems usually use:

```text
left boundary
right boundary
```

to define subtree ranges.

---

# 4. Balanced BST Pattern

If input is:

```text
sorted
```

→ Middle element usually becomes root.

---

# Important Interview Insight

Most construction problems are actually:

```text
Recursive partitioning problems
```

You repeatedly divide:

```text
Left subtree
Right subtree
```

using traversal information.

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Parent created first | Preorder |
| Build from traversal arrays | Construction |
| Child answers first | Postorder |
| Sorted BST traversal | Inorder |

---

# Common Mistake

Students forget:

```text
Postorder construction builds RIGHT subtree first
```

because root is processed backward.

This is one of the most common interview mistakes.

---

# One-Line Memory Trick

```text
Construction = Find root, split subtree, recurse
```

---

# Final Interview Insight

Most tree construction interview questions become easy after recognizing:

```text
Where is the root located?
```

Once root position is identified:

```text
Remaining elements naturally split into:
Left subtree + Right subtree
```

This is one of the most important recursive tree patterns asked at Meta, Google, Amazon, Uber, and top product companies.