# K Closest / Nearest Node Patterns — Recognition Notes

---

# Definition

K closest problems involve finding:

```text
Nearest / closest / minimum difference elements
```

relative to:

- a target value
- a target node
- a position
- a distance

These problems commonly appear in:

- BSTs
- graphs
- arrays
- matrices
- trees

---

# Core Intuition

Most k-closest problems depend on:

```text
Distance comparison
```

The MAIN question is usually:

```text
How do we efficiently track nearest elements?
```

---

# Most Important Observation

K-closest problems usually involve one of:

| Pattern | Main Technique |
|---|---|
| Closest value in BST | BST traversal |
| K closest values | Heap / Inorder |
| Distance K from node | BFS |
| Nearest points | Heap |
| Kth nearest | Priority Queue |

---

# When Should I Think About K Closest Pattern?

Use this pattern when:

- Need nearest nodes
- Need minimum difference
- Need k closest values
- Need nodes at distance k
- Need closest target search
- Need top-k candidates

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "closest"
- "nearest"
- "minimum difference"
- "distance k"
- "top k"
- "k nearest"
- "closest value"
- "minimum distance"
- "near target"
- "within distance"

→ Think **K Closest Pattern**

---

# Mental Model

Ask this question:

> “Am I trying to minimize distance from a target?”

If YES:

```text
Think K Closest / Distance Pattern
```

---

# Important K-Closest Categories

| Problem Type | Main Pattern |
|---|---|
| Closest BST value | BST traversal |
| K closest values | Heap / Sliding window |
| Distance K nodes | BFS from target |
| Closest leaf | Graph BFS |
| Minimum difference | Inorder traversal |

---

# Pattern 1 — Closest Binary Search Tree Value

---

## Trigger

- closest value
- nearest node
- BST search optimization

---

## Problem

LeetCode 270 — Closest Binary Search Tree Value

---

## Recognition

BST property helps decide:

```text
Move left or right
```

while tracking:

```text
Minimum difference
```

Classic BST-guided search.

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

# Pattern 2 — All Nodes Distance K in Binary Tree

---

## Trigger

- distance k
- nodes k away
- graph-style traversal

---

## Problem

LeetCode 863 — All Nodes Distance K in Binary Tree

---

## Recognition

Tree must behave like:

```text
Undirected graph
```

because movement happens:

- left
- right
- parent

Need:

```text
BFS starting from target node
```

Classic graph conversion pattern.

---

## Solution

```java
class Solution {

    HashMap<TreeNode, TreeNode> parent =
        new HashMap<>();

    public List<Integer> distanceK(
        TreeNode root,
        TreeNode target,
        int k
    ) {

        build(root, null);

        Queue<TreeNode> q =
            new LinkedList<>();

        HashSet<TreeNode> vis =
            new HashSet<>();

        q.offer(target);

        vis.add(target);

        int dist = 0;

        while(!q.isEmpty()) {

            int size = q.size();

            if(dist == k) {

                List<Integer> ans =
                    new ArrayList<>();

                for(TreeNode node : q) {
                    ans.add(node.val);
                }

                return ans;
            }

            for(int i = 0; i < size; i++) {

                TreeNode node = q.poll();

                if(node.left != null &&
                   !vis.contains(node.left)) {

                    vis.add(node.left);

                    q.offer(node.left);
                }

                if(node.right != null &&
                   !vis.contains(node.right)) {

                    vis.add(node.right);

                    q.offer(node.right);
                }

                TreeNode par = parent.get(node);

                if(par != null &&
                   !vis.contains(par)) {

                    vis.add(par);

                    q.offer(par);
                }
            }

            dist++;
        }

        return new ArrayList<>();
    }

    void build(
        TreeNode root,
        TreeNode par
    ) {

        if(root == null) return;

        parent.put(root, par);

        build(root.left, root);

        build(root.right, root);
    }
}
```

---

# Pattern 3 — Minimum Absolute Difference in BST

---

## Trigger

- minimum difference
- closest pair
- ordered comparison

---

## Problem

LeetCode 530 — Minimum Absolute Difference in BST

---

## Recognition

BST inorder traversal gives:

```text
sorted order
```

Closest values in sorted order are always:

```text
adjacent elements
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

# Super Important Recognition Patterns

---

# 1. Closest in BST Pattern

If problem asks:

```text
closest value
minimum difference
nearest BST node
```

→ Think:

```text
BST traversal + difference tracking
```

---

# 2. Distance K Pattern

If movement occurs:

```text
up + down
```

→ Convert tree into:

```text
Undirected graph
```

then apply BFS.

---

# 3. Sorted Neighbor Pattern

If closest values are needed in BST:

```text
Closest values appear adjacent in inorder traversal
```

This is VERY important.

---

# 4. Top-K Candidate Pattern

If question asks:

```text
k closest
top k nearest
```

→ Usually think:

```text
Heap / Priority Queue
```

---

# Important Interview Insight

Many nearest-node problems secretly become:

```text
Distance minimization problems
```

The key is identifying:

```text
What defines "distance"?
```

Examples:

- numeric difference
- edge distance
- level distance
- coordinate distance

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Closest BST value | BST traversal |
| Nodes distance k | BFS |
| Minimum BST difference | Inorder |
| K nearest candidates | Heap |
| Shortest expansion | BFS |

---

# Common Mistake

Students often use:

```text
Full traversal
```

even when BST ordering can prune search efficiently.

Always use BST property whenever possible.

---

# One-Line Memory Trick

```text
Closest Problems = Minimize distance efficiently
```

---

# Final Interview Insight

Most k-closest interview problems become easier after identifying:

```text
What kind of distance is being measured?
```

That determines:

```text
DFS
BFS
Heap
BST traversal
Sliding window
```

This is one of the highest-frequency interview patterns asked at Meta, Google, Amazon, Uber, and top product companies.