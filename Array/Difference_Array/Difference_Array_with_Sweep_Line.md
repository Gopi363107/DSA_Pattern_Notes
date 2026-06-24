# Difference Array with Sweep Line

## Core Idea

Sweep Line is essentially a Difference Array applied on events.

Instead of processing every point individually:

```text
Start Event  -> +value
End Event    -> -value
```

Store changes only at event positions.

Then sweep from left to right accumulating values.

---

## When to Use

* Interval overlaps.
* Meeting rooms.
* Maximum concurrent users.
* Booking systems.
* Population changes.
* Event timelines.
* Coverage counting.

---

## Trigger Words

* Overlapping intervals
* Concurrent events
* Active intervals
* Maximum overlap
* Meeting rooms
* Passengers
* Bookings
* Population
* Timeline

---

## General Pattern

```text
Intervals
    ↓
Create Events
    ↓
Start = +1
End   = -1
    ↓
Sort Events
    ↓
Sweep Line
    ↓
Answer
```

---

## Difference Array Interpretation

Interval:

```text
[2,5]
```

Store:

```java
map.put(2, +1);
map.put(6, -1);
```

During sweep:

```text
Position  ActiveCount

2         1
3         1
4         1
5         1
6         0
```

---

## General Template

```java
TreeMap<Integer,Integer> events =
        new TreeMap<>();

for(int[] interval : intervals){

    int start = interval[0];
    int end = interval[1];

    events.put(start,
        events.getOrDefault(start,0)+1);

    events.put(end + 1,
        events.getOrDefault(end+1,0)-1);
}

int active = 0;

for(int delta : events.values()){

    active += delta;
}
```

---

## Time Complexity

```text
Event Creation : O(N)

Sorting Events : O(N log N)

Sweep          : O(N)

Total          : O(N log N)
```

## Space Complexity

```text
O(N)
```

---

## Important Insights

### Insight 1

Difference Array

```text
Index Based
```

Works when coordinates are small.

---

### Insight 2

Sweep Line

```text
Event Based
```

Works when coordinates are huge.

Example:

```text
10^9
```

No large array needed.

---

### Insight 3

Sweep Line is a Sparse Difference Array.

Instead of:

```text
0 0 0 0 0 ...
```

Store only changes.

---

### Insight 4

Most interval problems become:

```text
Start -> +1

End   -> -1
```

Then accumulate.

---

## Recognition Pattern

```text
Intervals
     ↓
Need Active Count
     ↓
Need Maximum Overlap
     ↓
Difference Array
     +
Sweep Line
```

---

# Problem 1: LeetCode 253 - Meeting Rooms II

## Problem Statement

Find minimum meeting rooms required.

---

## Approach

Meeting Start:

```java
+1
```

Meeting End:

```java
-1
```

Sweep through timeline.

Maximum active meetings = answer.

---

## Solution

```java
class Solution {

    public int minMeetingRooms(int[][] intervals) {

        TreeMap<Integer,Integer> events =
                new TreeMap<>();

        for(int[] meeting : intervals){

            events.put(
                meeting[0],
                events.getOrDefault(
                    meeting[0],0)+1
            );

            events.put(
                meeting[1],
                events.getOrDefault(
                    meeting[1],0)-1
            );
        }

        int active = 0;
        int answer = 0;

        for(int delta : events.values()){

            active += delta;

            answer =
                Math.max(answer,active);
        }

        return answer;
    }
}
```

### TC

```text
O(N log N)
```

### SC

```text
O(N)
```

---

# Problem 2: LeetCode 1094 - Car Pooling

## Problem Statement

Check whether all trips fit inside vehicle capacity.

---

## Approach

Passenger enters:

```java
+passengers
```

Passenger leaves:

```java
-passengers
```

Sweep through locations.

---

## Solution Pattern

```java
start += passengers;

end   -= passengers;
```

Track active passengers.

If:

```text
active > capacity
```

Return false.

---

### TC

```text
O(N log N)
```

### SC

```text
O(N)
```

---

# Problem 3: LeetCode 1854 - Maximum Population Year

## Problem Statement

Find year with maximum population.

---

## Approach

Birth:

```java
+1
```

Death:

```java
-1
```

Sweep years.

Maximum active population gives answer.

---

## Solution

```java
class Solution {

    public int maximumPopulation(
            int[][] logs) {

        int[] diff = new int[101];

        for(int[] log : logs){

            diff[log[0] - 1950]++;

            diff[log[1] - 1950]--;
        }

        int population = 0;
        int maxPopulation = 0;
        int answer = 1950;

        for(int i=0;i<101;i++){

            population += diff[i];

            if(population > maxPopulation){

                maxPopulation = population;
                answer = 1950 + i;
            }
        }

        return answer;
    }
}
```

### TC

```text
O(N)
```

### SC

```text
O(1)
```

---

# Problem 4: LeetCode 732 - My Calendar III

## Problem Statement

After every booking, return maximum overlap.

---

## Approach

Sweep Line + TreeMap.

Store:

```java
start -> +1

end   -> -1
```

After each booking:

Sweep events.

Maximum active intervals = answer.

---

### TC

```text
O(N²)
```

---

## Common Interview Problems

```text
253  - Meeting Rooms II

1094 - Car Pooling

1854 - Maximum Population Year

729  - My Calendar I

731  - My Calendar II

732  - My Calendar III
```

---

## Difference Array vs Sweep Line

| Technique            | Best For          |
| -------------------- | ----------------- |
| Difference Array     | Small Coordinates |
| Sweep Line           | Large Coordinates |
| Difference + Prefix  | Dense Updates     |
| Sweep Line + TreeMap | Sparse Updates    |

---

## Visual Understanding

```text
Intervals

[1,5]
[2,6]
[4,8]

Events

1 -> +1
2 -> +1
4 -> +1
6 -> -1
7 -> -1
9 -> -1

----------------

Sweep

1 : 1

2 : 2

4 : 3

6 : 2

7 : 1

9 : 0

Maximum Overlap = 3
```

---

## Master Formula

```text
Interval Start
       ↓
Add Event (+)

Interval End
       ↓
Add Event (-)

Sort Events
       ↓
Sweep Left To Right
       ↓
Maintain Active Count
       ↓
Answer
```
