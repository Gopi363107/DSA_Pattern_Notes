# Tree → Graph Conversion Pattern

---

# Definition

This pattern is used when:

```text
A Binary Tree needs
upward movement
(parent traversal)
along with
downward movement
(children traversal)
```

Since a binary tree node does not store:

```text
Parent Pointer
```

we build it manually.

After building parent links:

```text
Tree
→
Undirected Graph
```

Then apply:

```text
BFS
```

or

```text
Graph Traversal
```

---

# Core Intuition

Normal Tree:

```text
Parent
  |
Child
```

Movement:

```text
Downward Only
```

After Parent Mapping:

```text
Parent <--> Child
```

Movement:

```text
Up
Down
```

Tree becomes:

```text
Graph
```

---

# Recognition Triggers

If a Tree Problem contains:

- Distance K
- Infection Spread
- Burn Tree
- Nearest Node
- Start from arbitrary node
- Move upward and downward
- Parent traversal needed

Think:

```text
Parent Map
+
BFS
```

---

# Generic Template

## Step 1

Build Parent Map

```java
Map<TreeNode, TreeNode> parentMap =
    new HashMap<>();

private void buildParent(
    TreeNode node,
    TreeNode parent
){

    if(node == null) return;

    parentMap.put(node, parent);

    buildParent(node.left, node);
    buildParent(node.right, node);
}
```

---

## Step 2

Run BFS from target node

```java
Queue<TreeNode> queue =
    new LinkedList<>();

Set<TreeNode> visited =
    new HashSet<>();

queue.offer(target);
visited.add(target);
```

---

## Step 3

Visit all neighbors

```java
left child
right child
parent
```

```java
if(node.left != null &&
   !visited.contains(node.left)){

    queue.offer(node.left);
    visited.add(node.left);
}

if(node.right != null &&
   !visited.contains(node.right)){

    queue.offer(node.right);
    visited.add(node.right);
}

TreeNode parent =
    parentMap.get(node);

if(parent != null &&
   !visited.contains(parent)){

    queue.offer(parent);
    visited.add(parent);
}
```

---

# Why Visited Set?

After Parent Mapping:

```text
5 <--> 3
```

Without visited:

```text
5 → 3 → 5 → 3
```

Infinite loop.

Therefore:

```java
Set<TreeNode> visited
```

is mandatory.

---

# Pattern 1 — Distance K From Target Node

---

## Problem

LeetCode 863

All Nodes Distance K in Binary Tree

---

## Trigger

Given:

```text
Target Node
+
Distance K
```

Need:

```text
All nodes exactly K edges away
```

---

# Key Insight

Distance means:

```text
Level Traversal
```

Use:

```text
BFS
```

Starting from:

```text
Target Node
```

---

# Example

```text
        3
       / \
      5   1
     / \ / \
    6  2 0  8
      / \
     7   4
```

Target:

```text
5
```

K:

```text
2
```

BFS Levels:

```text
Level 0 → 5

Level 1 → 6,2,3

Level 2 → 7,4,1
```

Answer:

```text
[7,4,1]
```

---

# Algorithm

```text
Build Parent Map

Start BFS from Target

Stop when
distance == K

All nodes currently
inside queue
are the answer
```

---

# Complexity

Time:

```text
O(N)
```

Space:

```text
O(N)
```

---

# Pattern 2 — Binary Tree Infection

---

## Problem

LeetCode 2385

Amount of Time for Binary Tree to Be Infected

---

## Trigger

Given:

```text
Start Node
```

Need:

```text
Minimum time
to infect entire tree
```

---

# Key Insight

Infection spreads:

```text
Parent
Child
```

every minute.

This is exactly:

```text
Multi-Level BFS
```

---

# Example

```text
Minute 0

Target
```

```text
Minute 1

All neighbors
```

```text
Minute 2

Neighbors of neighbors
```

Continue until:

```text
Queue becomes empty
```

---

# Algorithm

```text
Build Parent Map

Find Start Node

Run BFS

Count Levels

Levels
=
Minutes
```

---

# Minute Counting Trick

```java
int minute = -1;

while(!queue.isEmpty()){

    int size = queue.size();

    for(int i = 0;
        i < size;
        i++){

        ...
    }

    minute++;
}
```

---

# Complexity

Time:

```text
O(N)
```

Space:

```text
O(N)
```

---

# Pattern 3 — Burn Binary Tree

---

## Problem

Burning Tree

(Common Interview Question)

---

## Trigger

Given:

```text
Target Node
```

Fire starts from:

```text
Target
```

Need:

```text
Time required
to burn whole tree
```

---

# Observation

Fire spreads exactly like:

```text
Infection
```

to:

```text
Left Child
Right Child
Parent
```

every second.

---

# Key Insight

Burning Tree and Infection Tree are:

```text
Same Problem
```

Only wording changes.

---

# Algorithm

```text
Build Parent Map

Find Target

Run BFS

Count Levels

Answer
=
Total Levels - 1
```

---

# Complexity

Time:

```text
O(N)
```

Space:

```text
O(N)
```

---

# Pattern Recognition Summary

If Tree Problem Contains:

```text
Distance K
```

Think:

```text
Parent Map
+
BFS
```

---

If Tree Problem Contains:

```text
Infection Spread
```

Think:

```text
Parent Map
+
Level BFS
```

---

If Tree Problem Contains:

```text
Burn Tree
```

Think:

```text
Parent Map
+
Level BFS
```

---

# Common Mistakes

## Mistake 1

Forgetting Parent Mapping

Result:

```text
Cannot move upward
```

---

## Mistake 2

Forgetting Visited Set

Result:

```text
Infinite Loop
```

---

## Mistake 3

Wrong Minute Count

Returning:

```text
levels
```

instead of:

```text
levels - 1
```

Use:

```java
int minute = -1;
```

---

# One-Line Memory Trick

```text
Whenever a Tree needs
upward traversal,

convert it into a graph
using Parent Mapping
and solve with BFS.
```

---

# Pattern Family

Tree → Graph Conversion

├── LC 863 Distance K

├── LC 2385 Infection Tree

├── Burn Binary Tree

├── Nearest Node Problems

└── Future Parent Traversal Problems
