# Scheduling / Meeting Rooms

## Core Idea

Scheduling problems are based on:

```text id="a1b2c3"
Intervals (start, end)
```

Goal is to:

```text id="d4e5f6"
Select, Arrange, or Minimize Overlaps
```

using Greedy + Sorting + Heap/Queue.

---

## When to Use

* Meeting scheduling
* Room allocation
* CPU / task scheduling
* Interval overlap problems
* Resource optimization
* Minimum number of groups

---

## Trigger Words

* Meetings
* Intervals
* Overlap
* Minimum rooms
* Schedule tasks
* Can attend all
* Resource allocation

---

## Recognition Pattern

```text id="g7h8i9"
Intervals Given
       ↓
Need Optimal Arrangement
       ↓
Sort By Time
       ↓
Greedy / Heap / Sweep Line
```

---

# Types of Scheduling Problems

## Type 1: Can Attend All Meetings

### Idea

Check if any overlap exists.

---

## Approach

Sort by start time:

```text id="j0k1l2"
If current.start < previous.end → conflict
```

---

## Code

```java id="m3n4o5"
Arrays.sort(intervals, (a,b) -> a[0] - b[0]);

for(int i = 1; i < intervals.length; i++){

    if(intervals[i][0] < intervals[i-1][1]){
        return false;
    }
}

return true;
```

---

## Complexity

```text id="p6q7r8"
Time: O(N log N)
Space: O(1)
```

---

# Type 2: Minimum Meeting Rooms

## Idea

Find maximum number of overlapping intervals.

---

## Approach (Heap)

Use Min Heap for end times.

---

## Code

```java id="s9t0u1"
Arrays.sort(intervals, (a,b) -> a[0] - b[0]);

PriorityQueue<Integer> pq =
        new PriorityQueue<>();

int maxRooms = 0;

for(int[] meeting : intervals){

    while(!pq.isEmpty() &&
          pq.peek() <= meeting[0]){

        pq.poll();
    }

    pq.offer(meeting[1]);

    maxRooms =
        Math.max(maxRooms, pq.size());
}
```

---

## Complexity

```text id="v2w3x4"
Time: O(N log N)
Space: O(N)
```

---

# Type 3: Minimum Number of Groups

## Idea

Same as meeting rooms but groups = parallel intervals.

---

## Approach

Heap tracks active intervals.

---

## Code

```java id="y5z6a7"
Arrays.sort(intervals, (a,b) -> a[0] - b[0]);

PriorityQueue<Integer> pq =
        new PriorityQueue<>();

int groups = 0;

for(int[] interval : intervals){

    while(!pq.isEmpty() &&
          pq.peek() < interval[0]){

        pq.poll();
    }

    pq.offer(interval[1]);

    groups =
        Math.max(groups, pq.size());
}
```

---

# Type 4: Merge Intervals

## Idea

Combine overlapping intervals.

---

## Approach

Sort + merge.

---

## Code

```java id="b8c9d0"
Arrays.sort(intervals, (a,b) -> a[0] - b[0]);

List<int[]> result = new ArrayList<>();

int[] current = intervals[0];

for(int i = 1; i < intervals.length; i++){

    if(intervals[i][0] <= current[1]){

        current[1] =
            Math.max(current[1], intervals[i][1]);

    } else {

        result.add(current);
        current = intervals[i];
    }
}

result.add(current);
```

---

## Complexity

```text id="e1f2g3"
Time: O(N log N)
Space: O(N)
```

---

# Type 5: Minimum Resource Scheduling

## Idea

Assign resources efficiently.

---

## Approach

Use Min Heap:

```text id="h4i5j6"
Track earliest finishing resource
```

---

# Type 6: Weighted Scheduling (Advanced)

## Idea

Choose intervals with maximum profit.

---

## Approach

DP + Binary Search

```text id="k7l8m9"
Sort + DP + Upper Bound
```

---

# Core Techniques

## 1. Sorting

```text id="n0o1p2"
Sort by start time OR end time
```

---

## 2. Greedy

```text id="q3r4s5"
Pick earliest finishing interval
```

---

## 3. Heap

```text id="t6u7v8"
Track active intervals
```

---

## 4. Sweep Line

```text id="w9x0y1"
Process events chronologically
```

---

# Visual Understanding

## Example

```text id="z2a3b4"
(1,4)
(2,5)
(7,9)
```

---

## Step

```text id="c5d6e7"
1,4 → active

2,5 → overlap

7,9 → new room
```

---

# Important Insights

### Insight 1

All scheduling problems reduce to:

```text id="f8g9h0"
Sorting + Greedy Decision
```

---

### Insight 2

Heap is used when:

```text id="i1j2k3"
We need dynamic tracking of active intervals
```

---

### Insight 3

Overlap count is key:

```text id="l4m5n6"
Max overlap = min rooms required
```

---

### Insight 4

End time sorting is powerful:

```text id="o7p8q9"
Greedy works best with earliest finish
```

---

# Common Interview Problems

```text id="r0s1t2"
56   - Merge Intervals

57   - Insert Interval

252  - Meeting Rooms

253  - Meeting Rooms II

2406 - Minimum Groups

435  - Non-overlapping Intervals

452  - Minimum Arrows to Burst Balloons
```

---

# Pattern Map

| Problem Type         | Technique    |
| -------------------- | ------------ |
| Check overlap        | Sorting      |
| Min rooms            | Heap         |
| Merge intervals      | Greedy       |
| Scheduling max tasks | DP + Sorting |
| Resource allocation  | Heap + Sweep |

---

# Quick Revision

```text id="u3v4w5"
Intervals Given
        ↓
Sort By Start/End
        ↓
Check Overlap
        ↓
Use Greedy OR Heap
        ↓
Get Optimal Scheduling
```

---

# Master Formula

```text id="x6y7z8"
Scheduling Problems

=

Intervals + Sorting

+

Greedy OR Heap

-------------------

Overlap → Heap

Optimization → Greedy

Merging → Sorting

-------------------

Answer = Best Arrangement
```
