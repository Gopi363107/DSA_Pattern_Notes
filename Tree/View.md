# Tree View Patterns — Recognition Notes

---

# Definition

Tree view problems involve:

```text
What nodes are visible from a particular direction
```

such as:

- right side
- left side
- top view
- bottom view
- vertical order
- boundary traversal

These problems focus on:

```text
Position + Level relationships
```

---

# Core Intuition

Most view problems involve:

```text
Level-based traversal
```

which makes:

```text
BFS extremely common
```

because BFS naturally processes:

```text
Level by level
```

---

# Most Important Observation

View problems usually ask:

```text
Which node is FIRST or LAST seen at a level/column?
```

This is the MAIN view pattern.

---

# When Should I Think About View Patterns?

Use view logic when:

- Need visible nodes
- Need left/right side view
- Need vertical traversal
- Need top/bottom nodes
- Need boundary nodes
- Need column grouping
- Need level-based visibility

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "right side"
- "left side"
- "visible"
- "view"
- "top view"
- "bottom view"
- "vertical"
- "boundary"
- "column"
- "horizontal distance"
- "visible nodes"
- "seen from"

→ Think **Tree View Pattern**

---

# Mental Model

Ask this question:

> “Am I selecting specific visible nodes from each level or column?”

If YES:

```text
Think BFS + Position Tracking
```

---

# Important View Categories

| View Type | Main Logic |
|---|---|
| Right View | Last node at each level |
| Left View | First node at each level |
| Top View | First node in each column |
| Bottom View | Last node in each column |
| Vertical Order | Group by column |
| Boundary Traversal | Outer nodes only |

---

# Generic BFS View Template

```java
Queue<TreeNode> q = new LinkedList<>();

q.offer(root);

while(!q.isEmpty()) {

    int size = q.size();

    for(int i = 0; i < size; i++) {

        TreeNode node = q.poll();

        // process view logic

        if(node.left != null) {
            q.offer(node.left);
        }

        if(node.right != null) {
            q.offer(node.right);
        }
    }
}
```

---

# Pattern 1 — Binary Tree Right Side View

---

## Trigger

- right side view
- visible from right
- last node per level

---

## Problem

LeetCode 199 — Binary Tree Right Side View

---

## Recognition

Need:

```text
Last node at every level
```

BFS processes levels naturally.

At each level:

```text
Last processed node = visible node
```

Classic view pattern.

---

## Solution

```java
class Solution {

    public List<Integer> rightSideView(
        TreeNode root
    ) {

        List<Integer> ans =
            new ArrayList<>();

        if(root == null) return ans;

        Queue<TreeNode> q =
            new LinkedList<>();

        q.offer(root);

        while(!q.isEmpty()) {

            int size = q.size();

            for(int i = 0; i < size; i++) {

                TreeNode node = q.poll();

                if(i == size - 1) {
                    ans.add(node.val);
                }

                if(node.left != null) {
                    q.offer(node.left);
                }

                if(node.right != null) {
                    q.offer(node.right);
                }
            }
        }

        return ans;
    }
}
```

---

# Pattern 2 — Binary Tree Zigzag Level Order Traversal

---

## Trigger

- zigzag
- alternating directions
- reverse levels

---

## Problem

LeetCode 103 — Binary Tree Zigzag Level Order Traversal

---

## Recognition

Still:

```text
Level-order traversal
```

But alternate:

```text
Left → Right
Right → Left
```

Classic BFS level manipulation pattern.

---

## Solution

```java
class Solution {

    public List<List<Integer>> zigzagLevelOrder(
        TreeNode root
    ) {

        List<List<Integer>> ans =
            new ArrayList<>();

        if(root == null) return ans;

        Queue<TreeNode> q =
            new LinkedList<>();

        q.offer(root);

        boolean reverse = false;

        while(!q.isEmpty()) {

            int size = q.size();

            LinkedList<Integer> level =
                new LinkedList<>();

            for(int i = 0; i < size; i++) {

                TreeNode node = q.poll();

                if(reverse) {
                    level.addFirst(node.val);
                }
                else {
                    level.addLast(node.val);
                }

                if(node.left != null) {
                    q.offer(node.left);
                }

                if(node.right != null) {
                    q.offer(node.right);
                }
            }

            reverse = !reverse;

            ans.add(level);
        }

        return ans;
    }
}
```

---

# Pattern 3 — Vertical Order Traversal

---

## Trigger

- vertical order
- column traversal
- horizontal distance

---

## Problem

LeetCode 987 — Vertical Order Traversal of a Binary Tree

---

## Recognition

Need:

```text
Group nodes by column index
```

Rules:

```text
left child  -> column - 1
right child -> column + 1
```

Requires:

- BFS/DFS
- Column tracking
- Sorting/grouping

Classic coordinate-based tree pattern.

---

## Solution

```java
class Solution {

    public List<List<Integer>> verticalTraversal(
        TreeNode root
    ) {

        TreeMap<Integer,
            List<int[]>> map =
                new TreeMap<>();

        Queue<Object[]> q =
            new LinkedList<>();

        q.offer(new Object[]{root, 0, 0});

        while(!q.isEmpty()) {

            Object[] arr = q.poll();

            TreeNode node =
                (TreeNode) arr[0];

            int row = (int) arr[1];
            int col = (int) arr[2];

            map.putIfAbsent(
                col,
                new ArrayList<>());

            map.get(col)
               .add(new int[]{
                   row,
                   node.val
               });

            if(node.left != null) {

                q.offer(new Object[]{
                    node.left,
                    row + 1,
                    col - 1
                });
            }

            if(node.right != null) {

                q.offer(new Object[]{
                    node.right,
                    row + 1,
                    col + 1
                });
            }
        }

        List<List<Integer>> ans =
            new ArrayList<>();

        for(List<int[]> list : map.values()) {

            Collections.sort(list,
                (a, b) -> {

                if(a[0] == b[0]) {
                    return a[1] - b[1];
                }

                return a[0] - b[0];
            });

            List<Integer> cur =
                new ArrayList<>();

            for(int[] x : list) {
                cur.add(x[1]);
            }

            ans.add(cur);
        }

        return ans;
    }
}
```

---

# Super Important Recognition Patterns

---

# 1. Level Visibility Pattern

If question asks:

```text
visible nodes at each level
```

→ Usually:

```text
BFS level traversal
```

---

# 2. First/Last Node Pattern

If question asks:

```text
first node
last node
visible side node
```

→ Think:

```text
Level boundary nodes
```

---

# 3. Column-Based Pattern

If problem mentions:

```text
vertical
column
horizontal distance
```

→ Think:

```text
Column indexing
```

---

# 4. Boundary Traversal Pattern

If question asks:

```text
outer nodes
edge traversal
boundary
```

→ Think:

```text
Left boundary + Leaves + Right boundary
```

---

# Important Interview Insight

Most view problems are actually:

```text
Coordinate tracking problems
```

where nodes are organized by:

- level
- column
- visibility order

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Level visibility | BFS |
| Column grouping | Vertical Traversal |
| Deep recursive calculation | DFS |
| Subtree aggregation | Postorder |

---

# Common Mistake

Students sometimes use DFS directly for view problems.

But BFS naturally guarantees:

```text
Correct level ordering
```

which simplifies visibility logic.

---

# One-Line Memory Trick

```text
View Problems = Level/Column Visibility
```

---

# Final Interview Insight

Most difficult tree view problems become easier after identifying:

```text
Am I grouping nodes by:
Level?
Column?
Visibility order?
```

That single recognition usually determines:

```text
Traversal type
Extra data structures
Coordinate tracking
```

This is one of the highest-frequency BFS-based tree patterns asked at Meta, Google, Amazon, Uber, and top product companies.