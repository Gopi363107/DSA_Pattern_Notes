# Difference Array + Prefix Sum

## Core Idea

Difference Array handles:

```text
Fast Range Updates
```

Prefix Sum handles:

```text
Fast Reconstruction
```

Together they solve problems involving:

```text
Many Range Updates
            +
Need Final Frequencies
            +
Need Query Aggregation
```

---

## When to Use

* Multiple range updates.
* Coverage counting.
* Frequency accumulation.
* Sweep line problems.
* Event processing.
* Booking systems.

---

## Trigger Words

* Range updates
* Frequency count
* Number of overlaps
* Coverage
* Bookings
* Passengers
* Intervals
* Events

---

## General Pattern

```text
Range Update
      ↓
Difference Array
      ↓
Prefix Sum
      ↓
Frequency / Count Array
      ↓
Answer
```

---

## General Template

```java
int[] diff = new int[n + 1];

for(Query q : queries){

    diff[q.left] += value;

    diff[q.right + 1] -= value;
}

for(int i = 1; i < n; i++){

    diff[i] += diff[i - 1];
}
```

---

## Time Complexity

```text
Updates : O(Q)

Build   : O(N)

Total   : O(N + Q)
```

## Space Complexity

```text
O(N)
```

---

## Important Insights

### Insight 1

Difference Array stores:

```text
Where Effect Starts
Where Effect Ends
```

---

### Insight 2

Prefix Sum converts:

```text
Difference Array
        ↓
Actual Frequencies
```

---

### Insight 3

Most interval problems become:

```text
Mark Start
Mark End
Apply Prefix Sum
```

---

### Insight 4

This is the foundation of:

```text
Sweep Line
Interval Counting
Booking Problems
Traffic Simulation
```

---

## Recognition Pattern

```text
Many Intervals
       ↓
Need Count at Every Point
       ↓
Difference Array
       +
Prefix Sum
```

---

# Problem 1: LeetCode 1094 - Car Pooling

## Problem Statement

Determine whether a vehicle can handle all trips without exceeding capacity.

---

## Approach

Each trip:

```text
[start,end)
```

Passengers enter:

```java
diff[start] += passengers;
```

Passengers leave:

```java
diff[end] -= passengers;
```

Apply Prefix Sum.

Check maximum passengers.

---

## Solution

```java
class Solution {

    public boolean carPooling(
            int[][] trips,
            int capacity) {

        int[] diff = new int[1001];

        for(int[] trip : trips){

            int passengers = trip[0];
            int from = trip[1];
            int to = trip[2];

            diff[from] += passengers;
            diff[to] -= passengers;
        }

        int current = 0;

        for(int x : diff){

            current += x;

            if(current > capacity)
                return false;
        }

        return true;
    }
}
```

### TC

```text
O(N + 1000)
```

### SC

```text
O(1000)
```

---

# Problem 2: LeetCode 1109 - Corporate Flight Bookings

## Problem Statement

Each booking adds seats to a range of flights.

Return seats booked for every flight.

---

## Approach

Booking:

```text
[l,r] += seats
```

Use Difference Array.

Apply Prefix Sum.

---

## Solution

```java
class Solution {

    public int[] corpFlightBookings(
            int[][] bookings,
            int n) {

        int[] diff = new int[n];

        for(int[] booking : bookings){

            int first = booking[0] - 1;
            int last = booking[1] - 1;
            int seats = booking[2];

            diff[first] += seats;

            if(last + 1 < n)
                diff[last + 1] -= seats;
        }

        for(int i = 1; i < n; i++){

            diff[i] += diff[i - 1];
        }

        return diff;
    }
}
```

### TC

```text
O(N + Q)
```

### SC

```text
O(N)
```

---

# Problem 3: LeetCode 1893 - Check if All the Integers in a Range Are Covered

## Problem Statement

Check whether every number in a given range is covered by intervals.

---

## Approach

1. Mark interval coverage.
2. Apply Prefix Sum.
3. Verify every number in range.

---

## Solution

```java
class Solution {

    public boolean isCovered(
            int[][] ranges,
            int left,
            int right) {

        int[] diff = new int[52];

        for(int[] range : ranges){

            diff[range[0]]++;

            diff[range[1] + 1]--;
        }

        int coverage = 0;

        for(int i = 1; i <= 50; i++){

            coverage += diff[i];

            if(i >= left &&
               i <= right &&
               coverage == 0){

                return false;
            }
        }

        return true;
    }
}
```

### TC

```text
O(N + 50)
```

### SC

```text
O(50)
```

---

# Common Interview Problems

```text
1094 - Car Pooling

1109 - Corporate Flight Bookings

1893 - Check if All Integers in Range Are Covered

370  - Range Addition

2381 - Shifting Letters II
```

---

## Difference Array vs Prefix Sum

| Structure           | Purpose                      |
| ------------------- | ---------------------------- |
| Prefix Sum          | Fast Range Query             |
| Difference Array    | Fast Range Update            |
| Difference + Prefix | Fast Update + Reconstruction |

---

## Visual Understanding

```text
Trip 1

[2,5] += 3

Trip 2

[4,7] += 2

--------------------------------

Difference

0 0 3 0 2 0 -3 0 -2

--------------------------------

Prefix Sum

0 0 3 3 5 5 2 2 0

--------------------------------

Passengers At Each Point
```

---

## Master Formula

```text
1. Create Difference Array

2. Mark Start

   diff[l] += val

3. Mark End

   diff[r+1] -= val

4. Apply Prefix Sum

5. Obtain Actual Counts

6. Solve Problem
```
