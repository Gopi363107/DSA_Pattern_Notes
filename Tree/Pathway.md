# Tree Path-Based Problems — Pattern Recognition Notes

---

# Definition

Path-based problems involve:

```text
Traversing paths between nodes
```

and calculating:

- sums
- maximum values
- sequences
- valid routes
- path existence

A path can be:

- root → leaf
- node → node
- any connected path
- downward path
- zigzag path

---

# Core Intuition

Most path problems involve:

```text
Information flowing through recursion
```

Usually one of:

```text
Top-down flow  → Preorder DFS
Bottom-up flow → Postorder DFS
```

---

# Most Important Observation

Path problems usually ask:

```text
1. Does a path exist?
2. What is the best path?
3. How many valid paths exist?
4. What is the maximum/minimum path?
```

Understanding WHICH type is critical.

---

# When Should I Think About Path Pattern?

Use path logic when:

- Problem mentions root-to-leaf
- Need path sums
- Need maximum path
- Need valid route checking
- Need path counting
- Need path generation
- Need path constraints

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "path"
- "sum"
- "route"
- "root to leaf"
- "maximum path"
- "valid path"
- "target sum"
- "sequence"
- "downward path"
- "count paths"
- "leaf"
- "connected path"

→ Think **Tree Path Pattern**

---

# Mental Model

Ask this question:

> “Am I carrying information THROUGH a traversal path?”

If YES:

```text
Think path-based DFS
```

---

# Important Path Categories

| Path Type | Common Traversal |
|---|---|
| Root → Leaf | Preorder |
| Any Node → Any Node | Postorder |
| Count Valid Paths | Prefix Sum DFS |
| Generate Paths | Backtracking DFS |

---

# Pattern 1 — Root to Leaf Target Sum

---

## Trigger

- root to leaf
- target sum
- path validation

---

## Problem

LeetCode 113 — Path Sum II

---

## Recognition

Need:

```text
Build current path while moving downward
```

Classic:

```text
Preorder + Backtracking
```

because current node must be added BEFORE exploring children.

---

## Solution

```java
class Solution {

    List<List<Integer>> ans = new ArrayList<>();

    public List<List<Integer>> pathSum(
        TreeNode root,
        int targetSum
    ) {

        dfs(root, targetSum,
            new ArrayList<>());

        return ans;
    }

    void dfs(
        TreeNode root,
        int target,
        List<Integer> path
    ) {

        if(root == null) return;

        path.add(root.val);

        target -= root.val;

        if(root.left == null &&
           root.right == null &&
           target == 0) {

            ans.add(new ArrayList<>(path));
        }

        dfs(root.left, target, path);
        dfs(root.right, target, path);

        path.remove(path.size() - 1);
    }
}
```

---

# Pattern 2 — Maximum Path Sum

---

## Trigger

- maximum path
- best path
- any node to any node
- largest sum

---

## Problem

LeetCode 124 — Binary Tree Maximum Path Sum

---

## Recognition

Need:

```text
Best path passing through current node
```

Current node combines:

```text
left contribution + root + right contribution
```

Need child answers first.

Classic:

```text
Postorder DFS
```

---

## Solution

```java
class Solution {

    int maxSum = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {

        dfs(root);

        return maxSum;
    }

    int dfs(TreeNode root) {

        if(root == null) return 0;

        int left =
            Math.max(0, dfs(root.left));

        int right =
            Math.max(0, dfs(root.right));

        maxSum =
            Math.max(maxSum,
                     left + right + root.val);

        return Math.max(left, right)
               + root.val;
    }
}
```

---

# Pattern 3 — Pseudo-Palindromic Paths

---

## Trigger

- path property validation
- digit frequency
- root-to-leaf checking

---

## Problem

LeetCode 1457 — Pseudo-Palindromic Paths in a Binary Tree

---

## Recognition

Need:

```text
Track frequency information along path
```

This is:

```text
Preorder DFS + Backtracking
```

because state flows downward.

---

## Solution

```java
class Solution {

    int ans = 0;

    public int pseudoPalindromicPaths(TreeNode root) {

        dfs(root, new int[10]);

        return ans;
    }

    void dfs(TreeNode root, int[] freq) {

        if(root == null) return;

        freq[root.val]++;

        if(root.left == null &&
           root.right == null) {

            int odd = 0;

            for(int f : freq) {

                if(f % 2 == 1) odd++;
            }

            if(odd <= 1) ans++;
        }

        dfs(root.left, freq);
        dfs(root.right, freq);

        freq[root.val]--;
    }
}
```

---

# Super Important Recognition Patterns

---

# 1. Root-to-Leaf Problems

If question says:

```text
root to leaf
```

→ Usually:

```text
Preorder DFS
```

because path state flows downward.

---

# 2. Any Node to Any Node Problems

If path can start/end anywhere:

```text
node → node
```

→ Usually:

```text
Postorder DFS
```

because parent combines child results.

---

# 3. Path Counting Problems

If question asks:

```text
count valid paths
```

→ Think:

```text
Prefix sum / HashMap DFS
```

---

# 4. Path Generation Problems

If question asks:

```text
return all paths
generate paths
store path sequence
```

→ Think:

```text
Backtracking DFS
```

---

# Important Interview Insight

Many hard tree problems are actually:

```text
Path propagation problems
```

The key question is:

```text
Does information flow:
Top-down?
OR
Bottom-up?
```

That decides traversal.

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Root → leaf path | Preorder |
| Any node path | Postorder |
| Count paths | Prefix Sum DFS |
| Generate all paths | Backtracking |
| Level shortest path | BFS |

---

# Common Mistake

Students confuse:

```text
Root-to-leaf path
```

with:

```text
Any-node path
```

This completely changes the traversal strategy.

---

# One-Line Memory Trick

```text
Root-to-leaf → Top-down
Any-node path → Bottom-up
```

---

# Final Interview Insight

Most difficult tree path problems become easier after identifying:

```text
What type of path is allowed?
```

Because that directly determines:

```text
Traversal direction
State flow
DFS pattern
```

This is one of the highest-frequency tree interview patterns asked at Meta, Google, Amazon, Uber, and top product companies.