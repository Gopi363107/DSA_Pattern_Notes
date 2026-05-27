# Prefix Sum Pattern — Difference Array Pattern Notes

---

# Definition

The **Difference Array Pattern** is used for:

```text
Efficient range updates
```

Instead of updating:

```text
Every element in a range
```

we update only:

```text
Boundary points
```

Then reconstruct the final array using:

```text
Prefix Sum
```

---

# Core Intuition

Suppose we want to add:

```text
+5
```

to range:

```text
[L → R]
```

Naively:

```text
Update every element
```

Complexity:

```text
O(n)
```

per query.

Difference array allows:

```text
O(1)
```

range updates.

---

# MOST IMPORTANT IDEA

To apply:

```text
+val
```

on range:

```text
[L → R]
```

Do:

```text
diff[L] += val
```

and:

```text
diff[R + 1] -= val
```

Then later:

```text
Prefix sum reconstructs
the final array
```

GENIUS trick.

---

# Why This Works

Suppose:

```text
diff[L] += 5
```

means:

```text
Start adding +5 from L
```

And:

```text
diff[R+1] -= 5
```

means:

```text
Stop adding +5 after R
```

Prefix sum spreads updates automatically.

---

# Visualization

Initial:

```text
0 0 0 0 0 0
```

Add:

```text
+3 to range [1,4]
```

Difference updates:

```text
0 3 0 0 0 -3
```

Now take prefix sum:

```text
0 3 3 3 3 0
```

Range updated successfully.

---

# When Should I Think About Difference Array?

Use this pattern when:

- many range updates
- interval increment problems
- batch updates
- offline updates
- repeated additions on ranges

---

# Recognition Triggers

If problem contains:

- "add val to range"
- "multiple updates"
- "range increment"
- "batch modifications"
- "interval updates"
- "apply operations"

→ Think:

```text
Difference Array
```

---

# Generic Template

## Applying Updates

```java
int[] diff = new int[n];

for(each update) {

    diff[L] += val;

    if(R + 1 < n) {

        diff[R + 1] -= val;
    }
}
```

---

## Reconstruct Final Array

```java
int[] result = new int[n];

result[0] = diff[0];

for(int i = 1; i < n; i++) {

    result[i] =
        result[i - 1] + diff[i];
}
```

---

# MOST IMPORTANT INSIGHT

Difference array stores:

```text
Where changes START
and STOP
```

Prefix sum later propagates effects.

---

# Pattern 1 — Range Addition

---

## Trigger

- many range increments
- interval updates
- repeated modifications

---

## Problem

LeetCode 370 — Range Addition

---

# Key Insight

Instead of updating every element:

```text
Update only boundaries
```

Then reconstruct final values.

---

## Solution

```java
class Solution {

    public int[] getModifiedArray(
        int length,
        int[][] updates
    ) {

        int[] diff = new int[length];

        for(int[] update : updates) {

            int start = update[0];
            int end = update[1];
            int val = update[2];

            diff[start] += val;

            if(end + 1 < length) {

                diff[end + 1] -= val;
            }
        }

        int[] result =
            new int[length];

        result[0] = diff[0];

        for(int i = 1; i < length; i++) {

            result[i] =
                result[i - 1] + diff[i];
        }

        return result;
    }
}
```

---

# Complexity

## Time Complexity

```text
O(n + q)
```

Where:

```text
q = number of updates
```

---

## Space Complexity

```text
O(n)
```

---

# CP-Level Insight

Without difference array:

```text
Each update → O(n)
```

Total:

```text
O(n × q)
```

Difference array reduces updates to:

```text
O(1)
```

Massive optimization.

---

# Dry Run

Initial:

```text
[0,0,0,0,0]
```

Update:

```text
[1,3,+2]
```

---

# Difference Updates

```text
diff[1] += 2
diff[4] -= 2
```

Difference array:

```text
[0,2,0,0,-2]
```

---

# Prefix Reconstruction

```text
0
2
2
2
0
```

Final array:

```text
[0,2,2,2,0]
```

---

# Pattern 2 — Corporate Flight Bookings

---

## Trigger

- seat bookings
- interval accumulation
- many range additions

---

## Problem

LeetCode 1109 — Corporate Flight Bookings

---

# Key Insight

Each booking affects:

```text
Continuous flight interval
```

Difference array handles interval additions perfectly.

---

## Solution

```java
class Solution {

    public int[] corpFlightBookings(
        int[][] bookings,
        int n
    ) {

        int[] diff = new int[n];

        for(int[] b : bookings) {

            int first = b[0] - 1;
            int last = b[1] - 1;
            int seats = b[2];

            diff[first] += seats;

            if(last + 1 < n) {

                diff[last + 1] -= seats;
            }
        }

        for(int i = 1; i < n; i++) {

            diff[i] += diff[i - 1];
        }

        return diff;
    }
}
```

---

# Complexity

## Time Complexity

```text
O(n + bookings)
```

## Space Complexity

```text
O(n)
```

---

# SUPER IMPORTANT INSIGHT

Difference array is basically:

```text
Inverse operation
of prefix sum
```

Prefix sum:

```text
Builds cumulative values
```

Difference array:

```text
Stores cumulative changes
```

Beautiful duality.

---

# Advanced Competitive Programming Insights

---

# 1. Difference Array = Lazy Range Updates

Instead of immediate updates:

```text
Store update intentions
```

Apply later via prefix sum.

---

# 2. Prefix Sum + Difference Array Are Duals

| Operation | Purpose |
|---|---|
| Prefix Sum | Fast queries |
| Difference Array | Fast updates |

VERY important concept.

---

# 3. Boundary Marking Technique

Difference array marks:

```text
Where effect starts
Where effect ends
```

Extremely powerful CP idea.

---

# 4. Offline Processing Pattern

Difference arrays work beautifully when:

```text
All updates known beforehand
```

Classic offline optimization.

---

# Common Mistake

Students forget boundary check:

```java
if(R + 1 < n)
```

This causes:

```text
Array index out of bounds
```

Very common bug.

---

# One-Line Memory Trick

```text
Difference array marks
where updates begin and end.
```

---

# Final Interview Insight

The REAL power of difference array is:

```text
Turning expensive range updates
into constant-time boundary operations
```

Instead of updating:

```text
Entire ranges repeatedly
```

we only record:

```text
Where changes start and stop
```

Then prefix sum reconstructs everything efficiently.

This transforms many:

```text
O(n × q)
```

solutions into:

```text
O(n + q)
```