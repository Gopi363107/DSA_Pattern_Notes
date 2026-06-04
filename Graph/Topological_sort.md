# Topological Sort Pattern

## Definition

Topological Sort gives a valid ordering of nodes such that:

```text
u → v

u always comes before v
```

Works only for:

```text
DAG
(Directed Acyclic Graph)
```

---

## When To Use

Use when the problem asks:

```text
Dependencies

Prerequisites

Execution Order

Build Order

Task Scheduling

Course Scheduling

Process Order

Alien Dictionary
```

---

## Trigger Words

```text
Complete tasks in order

Prerequisites

Dependencies

Build system

Execution order

Can finish all courses

Schedule courses

Task order
```

---

## Core Idea

A valid ordering exists only if:

```text
Graph is DAG
```

If cycle exists:

```text
No valid ordering possible
```

---

# Approaches

## 1. Kahn's Algorithm (BFS)

Uses:

```text
Queue
Indegree Array
```

### Core Idea

Start with nodes having:

```text
Indegree = 0
```

Process them and remove outgoing edges.

Eventually new nodes become:

```text
Indegree = 0
```

---

## Kahn's Algorithm Template

```java
List<Integer> topoSort(
        int n,
        List<Integer>[] graph) {

    int[] indegree = new int[n];

    for (int node = 0; node < n; node++) {

        for (int neighbor : graph[node]) {

            indegree[neighbor]++;

        }
    }

    Queue<Integer> queue =
            new LinkedList<>();

    for (int i = 0; i < n; i++) {

        if (indegree[i] == 0) {

            queue.offer(i);

        }
    }

    List<Integer> topo =
            new ArrayList<>();

    while (!queue.isEmpty()) {

        int node = queue.poll();

        topo.add(node);

        for (int neighbor : graph[node]) {

            indegree[neighbor]--;

            if (indegree[neighbor] == 0) {

                queue.offer(neighbor);

            }
        }
    }

    return topo;
}
```

---

## 2. DFS Topological Sort

Uses:

```text
Postorder DFS
Reverse Result
```

### Core Idea

Visit all children first.

Then add current node.

Finally reverse the result.

---

## DFS Template

```java
void dfs(int node,
         List<Integer>[] graph,
         boolean[] visited,
         List<Integer> topo) {

    visited[node] = true;

    for (int neighbor : graph[node]) {

        if (!visited[neighbor]) {

            dfs(neighbor,
                graph,
                visited,
                topo);
        }
    }

    topo.add(node);
}
```

### Driver

```java
List<Integer> topoSort(
        int n,
        List<Integer>[] graph) {

    boolean[] visited =
            new boolean[n];

    List<Integer> topo =
            new ArrayList<>();

    for (int i = 0; i < n; i++) {

        if (!visited[i]) {

            dfs(i,
                graph,
                visited,
                topo);
        }
    }

    Collections.reverse(topo);

    return topo;
}
```

---

# Pattern Recognition

## Step 1

Ask:

```text
Need ordering?
```

If yes:

```text
Topological Sort
```

---

## Step 2

Ask:

```text
Dependency graph?
```

If yes:

```text
Topological Sort
```

---

## Step 3

Ask:

```text
Prerequisites?
Build Order?
Task Scheduling?
```

If yes:

```text
Topological Sort
```

---

# Problem 1

## LC 210 - Course Schedule II

### Recognition

```text
Return valid course order

Prerequisites

Dependency Graph
```

Pattern:

```text
Topological Sort
(Kahn's Algorithm)
```

---

### Core Idea

Course:

```text
A → B
```

means:

```text
A before B
```

Generate valid ordering.

If cycle exists:

```text
Return Empty Array
```

---

### Solution

```java
class Solution {

    public int[] findOrder(
            int numCourses,
            int[][] prerequisites) {

        List<Integer>[] graph =
                new ArrayList[numCourses];

        for (int i = 0; i < numCourses; i++) {

            graph[i] = new ArrayList<>();
        }

        int[] indegree =
                new int[numCourses];

        for (int[] edge : prerequisites) {

            graph[edge[1]].add(edge[0]);

            indegree[edge[0]]++;
        }

        Queue<Integer> queue =
                new LinkedList<>();

        for (int i = 0; i < numCourses; i++) {

            if (indegree[i] == 0) {

                queue.offer(i);
            }
        }

        int[] answer =
                new int[numCourses];

        int index = 0;

        while (!queue.isEmpty()) {

            int node = queue.poll();

            answer[index++] = node;

            for (int neighbor : graph[node]) {

                indegree[neighbor]--;

                if (indegree[neighbor] == 0) {

                    queue.offer(neighbor);
                }
            }
        }

        if (index != numCourses) {

            return new int[0];
        }

        return answer;
    }
}
```

### Complexity

```text
Time  : O(V + E)

Space : O(V + E)
```

---

# Problem 2

## LC 1136 - Parallel Courses

### Recognition

```text
Semesters

Course Dependencies

Minimum Levels
```

Pattern:

```text
Topological Sort + BFS Levels
```

---

### Core Idea

One BFS Level:

```text
One Semester
```

Process all indegree 0 courses together.

---

### Solution

```java
class Solution {

    public int minimumSemesters(
            int n,
            int[][] relations) {

        List<Integer>[] graph =
                new ArrayList[n + 1];

        for (int i = 1; i <= n; i++) {

            graph[i] = new ArrayList<>();
        }

        int[] indegree =
                new int[n + 1];

        for (int[] edge : relations) {

            graph[edge[0]].add(edge[1]);

            indegree[edge[1]]++;
        }

        Queue<Integer> queue =
                new LinkedList<>();

        for (int i = 1; i <= n; i++) {

            if (indegree[i] == 0) {

                queue.offer(i);
            }
        }

        int semesters = 0;
        int completed = 0;

        while (!queue.isEmpty()) {

            int size = queue.size();

            semesters++;

            for (int i = 0; i < size; i++) {

                int node = queue.poll();

                completed++;

                for (int neighbor : graph[node]) {

                    indegree[neighbor]--;

                    if (indegree[neighbor] == 0) {

                        queue.offer(neighbor);
                    }
                }
            }
        }

        return completed == n
                ? semesters
                : -1;
    }
}
```

### Complexity

```text
Time  : O(V + E)

Space : O(V + E)
```

---

# Problem 3

## LC 1203 - Sort Items by Groups Respecting Dependencies

### Recognition

```text
Group Dependencies

Item Dependencies

Ordering Problem
```

Pattern:

```text
Double Topological Sort
```

---

### Core Idea

Need ordering on:

```text
Groups

AND

Items
```

Perform:

```text
Topological Sort on Groups

Topological Sort on Items
```

Then combine.

---

### Interview Insight

This problem teaches:

```text
Topological Sort can be applied
on multiple graphs simultaneously.
```

Most interviews focus on recognizing:

```text
Dependency Graph

=> Topological Sort
```

rather than memorizing the full implementation.

---

# Complexity Summary

| Algorithm | Time | Space |
|------------|--------|--------|
| Kahn BFS | O(V+E) | O(V+E) |
| DFS Topological Sort | O(V+E) | O(V) |
| Course Schedule II | O(V+E) | O(V+E) |
| Parallel Courses | O(V+E) | O(V+E) |

---

# Interview Cheat Sheet

| Question Says | Pattern |
|--------------|----------|
| Prerequisites | Topological Sort |
| Dependencies | Topological Sort |
| Build Order | Topological Sort |
| Execution Order | Topological Sort |
| Course Schedule | Topological Sort |
| Task Scheduling | Topological Sort |
| Parallel Courses | Topological Sort + Levels |
| Dependency Graph | Topological Sort |

---

# Memory Trick

```text
Topological Sort

= Ordering Problem

Dependency Graph

= DAG

Kahn BFS

= Indegree + Queue

DFS Version

= Postorder DFS
  + Reverse Result
```

---

# Key Takeaway

```text
Need Valid Order?
→ Topological Sort

Need Dependency Resolution?
→ Topological Sort

Need Prerequisite Processing?
→ Topological Sort

Need Semester/Level Processing?
→ Kahn BFS
```