# Backtracking on Graph Pattern

## Definition

Backtracking on Graphs is used when we need to:

```text
Find All Paths

Explore Every Possibility

Enumerate Routes

Generate Valid Paths
```

Instead of finding one answer, we explore:

```text
All Possible Answers
```

---

## When To Use

Use when the problem asks:

```text
Find all paths

Generate all routes

Explore every possibility

Enumerate paths

Visit every valid route

Count all possible paths
```

---

## Trigger Words

```text
All Paths

Every Path

All Routes

Unique Paths

Generate Paths

Explore All Possibilities

Visit Every Cell
```

---

# Core Idea

Backtracking follows:

```text
Choose

Explore

Backtrack
```

---

## Generic Flow

```text
Choose Next Node

↓

Explore Further

↓

Undo Choice

↓

Try Another Path
```

---

## Visualization

```text
0
|
1
| \
2  3
 \/
  4
```

Possible Paths:

```text
0 → 1 → 2 → 4

0 → 1 → 3 → 4
```

Backtracking explores both.

---

# Generic Backtracking Template

```java
void dfs(int node,
         List<Integer>[] graph,
         List<Integer> path) {

    path.add(node);

    if (isGoal(node)) {

        saveAnswer(path);

    } else {

        for (int neighbor :
                graph[node]) {

            dfs(
                neighbor,
                graph,
                path
            );
        }
    }

    path.remove(
        path.size() - 1
    );
}
```

---

# Visited Backtracking Template

Used when revisiting is not allowed.

```java
void dfs(int node) {

    visited[node] = true;

    for (int neighbor :
            graph[node]) {

        if (!visited[neighbor]) {

            dfs(neighbor);
        }
    }

    visited[node] = false;
}
```

---

# Pattern Recognition

## Step 1

Ask:

```text
Need all paths?
```

If YES:

```text
Backtracking
```

---

## Step 2

Ask:

```text
Need every route?
```

If YES:

```text
Backtracking
```

---

## Step 3

Ask:

```text
Need all valid possibilities?
```

If YES:

```text
Backtracking
```

---

## Step 4

Ask:

```text
Need path generation?
```

If YES:

```text
Backtracking
```

---

# Problem 1

## LC 797 - All Paths From Source to Target

### Recognition

```text
All Paths

Source

Target
```

Pattern:

```text
DFS + Backtracking
```

---

### Core Idea

Start from:

```text
Node 0
```

Explore every possible path.

When reaching:

```text
Node n - 1
```

store current path.

---

### Solution

```java
class Solution {

    List<List<Integer>> answer =
            new ArrayList<>();

    public List<List<Integer>>
    allPathsSourceTarget(
            int[][] graph) {

        List<Integer> path =
                new ArrayList<>();

        dfs(
            0,
            graph,
            path
        );

        return answer;
    }

    private void dfs(
            int node,
            int[][] graph,
            List<Integer> path) {

        path.add(node);

        if (node
            == graph.length - 1) {

            answer.add(
                new ArrayList<>(path)
            );

        } else {

            for (int neighbor :
                    graph[node]) {

                dfs(
                    neighbor,
                    graph,
                    path
                );
            }
        }

        path.remove(
            path.size() - 1
        );
    }
}
```

### Complexity

```text
Time  : O(All Paths)

Space : O(Path Length)
```

---

# Problem 2

## LC 980 - Unique Paths III

### Recognition

```text
Visit Every Cell

Unique Path

Grid

Backtracking
```

Pattern:

```text
DFS + Backtracking
```

---

### Core Idea

Need to:

```text
Start at Source

Visit Every Empty Cell

Exactly Once

Reach Destination
```

Backtrack after every move.

---

### Solution

```java
class Solution {

    int paths = 0;
    int emptyCells = 0;

    int[][] directions = {

        {-1,0},
        {1,0},
        {0,-1},
        {0,1}
    };

    public int uniquePathsIII(
            int[][] grid) {

        int startRow = 0;
        int startCol = 0;

        for (int r = 0;
             r < grid.length;
             r++) {

            for (int c = 0;
                 c < grid[0].length;
                 c++) {

                if (grid[r][c] == 0) {

                    emptyCells++;
                }

                if (grid[r][c] == 1) {

                    startRow = r;
                    startCol = c;
                }
            }
        }

        dfs(
            startRow,
            startCol,
            grid,
            -1
        );

        return paths;
    }

    private void dfs(
            int row,
            int col,
            int[][] grid,
            int count) {

        if (row < 0 ||
            col < 0 ||
            row >= grid.length ||
            col >= grid[0].length ||
            grid[row][col] == -1) {

            return;
        }

        if (grid[row][col] == 2) {

            if (count
                == emptyCells) {

                paths++;
            }

            return;
        }

        int temp =
                grid[row][col];

        grid[row][col] = -1;

        for (int[] dir :
                directions) {

            dfs(
                row + dir[0],
                col + dir[1],
                grid,
                count + 1
            );
        }

        grid[row][col] = temp;
    }
}
```

### Complexity

```text
Time  : O(4^(M×N))

Space : O(M×N)
```

---

# Common Backtracking Pattern

```java
path.add(choice);

dfs(...);

path.remove(
    path.size() - 1
);
```

---

# Complexity Summary

| Algorithm | Time | Space |
|------------|--------|--------|
| DFS Path Exploration | Exponential | O(Path Length) |
| All Paths Source Target | O(All Paths) | O(Path Length) |
| Unique Paths III | O(4^(M×N)) | O(M×N) |

---

# Interview Cheat Sheet

| Question Says | Pattern |
|--------------|----------|
| All Paths | Backtracking |
| Every Route | Backtracking |
| Enumerate Paths | Backtracking |
| Unique Paths | Backtracking |
| Explore Possibilities | Backtracking |
| Visit Every Cell | Backtracking |
| Generate Paths | Backtracking |

---

# Memory Trick

```text
Choose

↓

Explore

↓

Backtrack
```

```text
path.add()

↓

dfs()

↓

path.remove()
```

```text
Need All Answers
=
Backtracking
```

---

# Key Takeaway

```text
Need All Paths?
→ Backtracking

Need Every Possibility?
→ Backtracking

Need Route Generation?
→ Backtracking

Core Formula:

Choose
→ Explore
→ Undo Choice
```