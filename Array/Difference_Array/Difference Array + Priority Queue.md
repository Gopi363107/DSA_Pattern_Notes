# Difference Array + Priority Queue.md

## Core Idea

Difference Array tracks:

```text id="a1b2c3"
Range Effects
```

Priority Queue manages:

```text id="d4e5f6"
Best Candidate
Current Maximum
Current Minimum
Earliest Ending
```

Together they solve problems involving:

```text id="g7h8i9"
Intervals
     +
Active Ranges
     +
Optimal Selection
```

---

## When to Use

* Active interval tracking.
* Resource allocation.
* Meeting scheduling.
* Maximum overlap.
* Event processing.
* Interval optimization.

---

## Trigger Words

* Active intervals
* Ongoing ranges
* Earliest ending
* Minimum resources
* Meeting rooms
* Servers
* Platforms
* Capacity allocation

---

## General Pattern

```text id="j0k1l2"
Process Timeline
        ↓
Add New Interval
        ↓
Remove Expired Interval
        ↓
Priority Queue
        ↓
Maintain Active State
```

---

## Recognition Pattern

```text id="m3n4o5"
Intervals
     ↓
Need Active Intervals
     ↓
Need Fast Removal
     ↓
Priority Queue
     +
Difference Array
```

---

## Why Combine Them?

Difference Array gives:

```text id="p6q7r8"
How Many Events Exist
```

Priority Queue gives:

```text id="s9t0u1"
Which Event Ends First
```

Together:

```text id="v2w3x4"
Efficient Interval Processing
```

---

## Important Insights

### Insight 1

Difference Array

```text id="y5z6a7"
Tracks Count
```

---

### Insight 2

Priority Queue

```text id="b8c9d0"
Tracks Order
```

---

### Insight 3

Most interval scheduling problems become:

```text id="e1f2g3"
Sort
 ↓
Sweep
 ↓
Priority Queue
```

---

### Insight 4

When active intervals matter:

```text id="h4i5j6"
Use Min Heap
```

to remove expired intervals efficiently.

---

## Time Complexity

```text id="k7l8m9"
Sorting     : O(N log N)

Heap Ops    : O(N log N)

Total       : O(N log N)
```

---

## Space Complexity

```text id="n0o1p2"
O(N)
```

---

# Problem 1: LeetCode 253 - Meeting Rooms II

## Problem Statement

Find minimum meeting rooms required.

---

## Approach

Sort meetings by start time.

Use Min Heap:

```text id="q3r4s5"
Store End Times
```

Remove completed meetings.

Heap size gives active rooms.

---

## Solution

```java id="t6u7v8"
class Solution {

    public int minMeetingRooms(
            int[][] intervals) {

        Arrays.sort(
            intervals,
            (a,b) -> a[0] - b[0]
        );

        PriorityQueue<Integer> pq =
                new PriorityQueue<>();

        int answer = 0;

        for(int[] meeting : intervals){

            while(!pq.isEmpty() &&
                  pq.peek() <= meeting[0]){

                pq.poll();
            }

            pq.offer(meeting[1]);

            answer =
                Math.max(answer,
                         pq.size());
        }

        return answer;
    }
}
```

### TC

```text id="w9x0y1"
O(N log N)
```

### SC

```text id="z2a3b4"
O(N)
```

---

# Problem 2: LeetCode 2406 - Divide Intervals Into Minimum Number of Groups

## Problem Statement

Find minimum groups required such that intervals inside a group do not overlap.

---

## Approach

Exactly same as Meeting Rooms II.

Active intervals are stored inside Min Heap.

Maximum active intervals = answer.

---

## Solution

```java id="c5d6e7"
class Solution {

    public int minGroups(
            int[][] intervals) {

        Arrays.sort(
            intervals,
            (a,b) -> a[0] - b[0]
        );

        PriorityQueue<Integer> pq =
                new PriorityQueue<>();

        int answer = 0;

        for(int[] interval : intervals){

            while(!pq.isEmpty() &&
                  pq.peek() < interval[0]){

                pq.poll();
            }

            pq.offer(interval[1]);

            answer =
                Math.max(answer,
                         pq.size());
        }

        return answer;
    }
}
```

### TC

```text id="f8g9h0"
O(N log N)
```

### SC

```text id="i1j2k3"
O(N)
```

---

# Problem 3: LeetCode 1094 - Car Pooling

## Problem Statement

Determine whether all trips fit inside vehicle capacity.

---

## Approach 1

Difference Array

```text id="l4m5n6"
Range Updates
```

---

## Approach 2

Priority Queue

```text id="o7p8q9"
Track Active Trips
```

Store:

```text id="r0s1t2"
Ending Locations
Passengers
```

Remove completed trips.

Maintain current passengers.

---

## Solution

```java id="u3v4w5"
class Solution {

    public boolean carPooling(
            int[][] trips,
            int capacity) {

        Arrays.sort(
            trips,
            (a,b) -> a[1] - b[1]
        );

        PriorityQueue<int[]> pq =
            new PriorityQueue<>(
                (a,b) -> a[0] - b[0]
            );

        int passengers = 0;

        for(int[] trip : trips){

            while(!pq.isEmpty() &&
                  pq.peek()[0] <= trip[1]){

                passengers -= pq.poll()[1];
            }

            passengers += trip[0];

            if(passengers > capacity)
                return false;

            pq.offer(
                new int[]{
                    trip[2],
                    trip[0]
                }
            );
        }

        return true;
    }
}
```

### TC

```text id="x6y7z8"
O(N log N)
```

### SC

```text id="a9b0c1"
O(N)
```

---

# Problem 4: LeetCode 1851 - Minimum Interval to Include Each Query

## Problem Statement

For every query find smallest interval containing it.

---

## Approach

Sort intervals.

Sort queries.

Priority Queue stores:

```text id="d2e3f4"
Interval Length
Interval End
```

Remove invalid intervals.

Top of heap gives answer.

---

## Key Insight

Priority Queue always keeps:

```text id="g5h6i7"
Best Active Interval
```

for current query.

---

### TC

```text id="j8k9l0"
O((N+Q) log N)
```

### SC

```text id="m1n2o3"
O(N)
```

---

## Common Interview Problems

```text id="p4q5r6"
253  - Meeting Rooms II

2406 - Divide Intervals Into Minimum Number Of Groups

1094 - Car Pooling

1851 - Minimum Interval To Include Each Query

759  - Employee Free Time

632  - Smallest Range Covering K Lists
```

---

## Difference Array vs Priority Queue

| Technique        | Purpose                      |
| ---------------- | ---------------------------- |
| Difference Array | Count Active Events          |
| Sweep Line       | Process Timeline             |
| Priority Queue   | Track Best Active Interval   |
| Difference + PQ  | Active Interval Optimization |

---

## Visual Understanding

```text id="s7t8u9"
Intervals

[1,5]
[2,6]
[4,8]

----------------

Start 1

Heap

5

----------------

Start 2

Heap

5 6

----------------

Start 4

Heap

5 6 8

----------------

Active Intervals = 3
```

---

## Master Formula

```text id="v0w1x2"
1. Sort Intervals

2. Process Left To Right

3. Remove Expired Intervals

4. Add Current Interval

5. Heap Stores Active State

6. Use Heap Top

7. Update Answer
```

---

## Difference Array Roadmap

```text id="y3z4a5"
Basic Difference Array
        ↓
Difference Array + Prefix Sum
        ↓
2D Difference Array
        ↓
Difference Array + Sweep Line
        ↓
Difference Array + Greedy
        ↓
Circular Difference Array
        ↓
Difference Array + Binary Search
        ↓
Difference Array + Priority Queue
        ↓
Coordinate Compression + Difference Array
        ↓
Advanced Interval Problems
```
