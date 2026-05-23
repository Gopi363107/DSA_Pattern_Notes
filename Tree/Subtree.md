# Tree Subtree Pattern — Recognition Notes

---

# Definition

Subtree problems involve:

```text
Solving problems inside smaller trees
```

where every node itself becomes:

```text
Root of another subtree
```

A subtree contains:

- current node
- left subtree
- right subtree

---

# Core Intuition

Most subtree problems follow:

```text
Compute child subtree answers first
```

then use them to calculate:

```text
Current subtree answer
```

This is mainly:

```text
Postorder DFS
```

because information flows:

```text
Child → Parent
```

---

# Most Important Observation

Every tree node can be treated as:

```text
A subtree root
```

This is the MAIN subtree mindset.

---

# When Should I Think About Subtree Pattern?

Use subtree logic when:

- Need subtree sums
- Need subtree heights
- Need subtree validation
- Need subtree comparison
- Need subtree aggregation
- Need subtree counting
- Need local tree answers

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "subtree"
- "sum of subtree"
- "largest subtree"
- "smallest subtree"
- "same tree"
- "balanced subtree"
- "subtree size"
- "subtree average"
- "all descendants"
- "complete subtree"
- "subtree rooted at"

→ Think **Subtree Pattern**

---

# Mental Model

Ask this question:

> “Does each node need information from its left and right subtree first?”

If YES:

```text
Think Postorder DFS
```

---

# Generic Subtree Template

```java
int dfs(TreeNode root) {

    if(root == null) return 0;

    int left = dfs(root.left);
    int right = dfs(root.right);

    // compute subtree answer

    return someSubtreeValue;
}
```

---

# Pattern 1 — Subtree of Another Tree

---

## Trigger

- same subtree
- subtree matching
- tree comparison

---

## Problem

LeetCode 572 — Subtree of Another Tree

---

## Recognition

Need:

```text
Check whether a subtree exactly matches another tree
```

At every node:

```text
Try matching entire subtree
```

Classic subtree comparison pattern.

---

## Solution

```java
class Solution {

    public boolean isSubtree(
        TreeNode root,
        TreeNode subRoot
    ) {

        if(root == null) return false;

        if(isSame(root, subRoot)) {
            return true;
        }

        return isSubtree(root.left, subRoot)
            || isSubtree(root.right, subRoot);
    }

    boolean isSame(TreeNode a, TreeNode b) {

        if(a == null && b == null) {
            return true;
        }

        if(a == null || b == null) {
            return false;
        }

        if(a.val != b.val) {
            return false;
        }

        return isSame(a.left, b.left)
            && isSame(a.right, b.right);
    }
}
```

---

# Pattern 2 — Most Frequent Subtree Sum

---

## Trigger

- subtree sum
- subtree aggregation
- frequency counting

---

## Problem

LeetCode 508 — Most Frequent Subtree Sum

---

## Recognition

Need:

```text
Sum of every subtree
```

Current subtree sum:

```text
leftSum + rightSum + root.val
```

Classic postorder aggregation.

---

## Solution

```java
class Solution {

    HashMap<Integer, Integer> map =
        new HashMap<>();

    int maxFreq = 0;

    public int[] findFrequentTreeSum(
        TreeNode root
    ) {

        dfs(root);

        List<Integer> list =
            new ArrayList<>();

        for(int key : map.keySet()) {

            if(map.get(key) == maxFreq) {
                list.add(key);
            }
        }

        int[] ans = new int[list.size()];

        for(int i = 0; i < list.size(); i++) {
            ans[i] = list.get(i);
        }

        return ans;
    }

    int dfs(TreeNode root) {

        if(root == null) return 0;

        int left = dfs(root.left);
        int right = dfs(root.right);

        int sum = left + right + root.val;

        map.put(sum,
            map.getOrDefault(sum, 0) + 1);

        maxFreq =
            Math.max(maxFreq, map.get(sum));

        return sum;
    }
}
```

---

# Pattern 3 — Count Complete Tree Nodes

---

## Trigger

- subtree size
- node counting
- complete subtree optimization

---

## Problem

LeetCode 222 — Count Complete Tree Nodes

---

## Recognition

Need:

```text
Count nodes efficiently
```

Observation:

If:

```text
left height == right height
```

then subtree is:

```text
Perfect Binary Tree
```

Node count becomes:

```text
2^height - 1
```

Subtree structure recognition pattern.

---

## Solution

```java
class Solution {

    public int countNodes(TreeNode root) {

        if(root == null) return 0;

        int leftHeight = left(root);
        int rightHeight = right(root);

        if(leftHeight == rightHeight) {

            return (1 << leftHeight) - 1;
        }

        return 1
            + countNodes(root.left)
            + countNodes(root.right);
    }

    int left(TreeNode root) {

        int h = 0;

        while(root != null) {

            h++;

            root = root.left;
        }

        return h;
    }

    int right(TreeNode root) {

        int h = 0;

        while(root != null) {

            h++;

            root = root.right;
        }

        return h;
    }
}
```

---

# Super Important Recognition Patterns

---

# 1. Every Node as Root Pattern

Subtree problems usually ask:

```text
What answer exists for subtree rooted at current node?
```

This is the BIGGEST subtree mindset.

---

# 2. Aggregate Child Results Pattern

If current node combines:

```text
left subtree answer
right subtree answer
```

→ Think:

```text
Postorder DFS
```

---

# 3. Tree Comparison Pattern

If problem asks:

```text
same tree
identical subtree
matching structure
```

→ Think:

```text
Recursive subtree comparison
```

---

# 4. Subtree Property Validation

If checking:

```text
balanced subtree
BST subtree
largest subtree
```

→ Usually:

```text
Return subtree information upward
```

---

# Important Interview Insight

Many advanced tree problems are secretly:

```text
Subtree DP problems
```

Each node computes:

```text
Answer for its own subtree
```

and returns it upward.

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Parent depends on child subtree | Postorder |
| Root-to-leaf flow | Preorder |
| Subtree aggregation | Subtree Pattern |
| Level expansion | BFS |

---

# Common Mistake

Students sometimes think subtree problems require:

```text
Global traversal only
```

But the real pattern is:

```text
Solve smaller subtrees recursively
```

---

# One-Line Memory Trick

```text
Subtree Problems = Every node becomes a mini-problem
```

---

# Final Interview Insight

Most difficult subtree problems become easier after recognizing:

```text
What information should each subtree return upward?
```

That single question usually determines:

```text
DFS structure
Return type
Traversal order
```

This is one of the strongest recursive tree patterns asked at Meta, Google, Amazon, Uber, and top product companies.