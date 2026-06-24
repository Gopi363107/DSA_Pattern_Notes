# Two Heaps (Median Pattern)

## Core Idea

Two Heaps pattern is used to maintain the **median dynamically** in a stream of numbers.

We split numbers into:

```text id="t1"
Left side → Max Heap (smaller half)
Right side → Min Heap (larger half)
```

So we can always get median in:

```text id="t2"
O(1)
```

---

## When to Use

* Running median in stream
* Sliding window median
* Online data analysis
* Real-time ranking systems
* Balancing two halves of data

---

## Trigger Words

* Median of data stream
* Continuously adding numbers
* Balance left and right halves
* Middle element
* Streaming input
* Dynamic dataset

---

## Recognition Pattern

```text id="t3"
Stream of numbers
        ↓
Need median at any time
        ↓
Need fast insert + median query
        ↓
Use Two Heaps
```

---

# Core Structure

## Left Heap (Max Heap)

Stores:

```text id="t4"
Smaller half of numbers
```

Top gives:

```text id="t5"
Maximum of left side
```

---

## Right Heap (Min Heap)

Stores:

```text id="t6"
Larger half of numbers
```

Top gives:

```text id="t7"
Minimum of right side
```

---

# Invariant Rules

## Rule 1: Size Balance

```text id="t8"
|left| == |right|
OR
|left| == |right| + 1
```

Left heap can have at most 1 extra element.

---

## Rule 2: Ordering

```text id="t9"
Max(left) ≤ Min(right)
```

---

# How Median is Found

## Case 1: Odd number of elements

```text id="t10"
Median = top of left heap
```

---

## Case 2: Even number of elements

```text id="t11"
Median = (top of left + top of right) / 2
```

---

# Insert Algorithm

## Step 1: Insert into correct heap

```java id="t12"
if(left.isEmpty() || num <= left.peek()){
    left.offer(num);
} else {
    right.offer(num);
}
```

---

## Step 2: Balance heaps

```java id="t13"
if(left.size() > right.size() + 1){
    right.offer(left.poll());
}

if(right.size() > left.size()){
    left.offer(right.poll());
}
```

---

# Java Implementation

```java id="t14"
class MedianFinder {

    PriorityQueue<Integer> left =
        new PriorityQueue<>(Collections.reverseOrder());

    PriorityQueue<Integer> right =
        new PriorityQueue<>();

    public void addNum(int num){

        if(left.isEmpty() || num <= left.peek()){
            left.offer(num);
        } else {
            right.offer(num);
        }

        if(left.size() > right.size() + 1){
            right.offer(left.poll());
        }

        if(right.size() > left.size()){
            left.offer(right.poll());
        }
    }

    public double findMedian(){

        if(left.size() == right.size()){
            return (left.peek() + right.peek()) / 2.0;
        }

        return left.peek();
    }
}
```

---

## Time Complexity

```text id="t15"
Insert: O(log N)
Median Query: O(1)
```

---

## Space Complexity

```text id="t16"
O(N)
```

---

# Visual Understanding

## Example Stream

```text id="t17"
5, 15, 1, 3
```

---

### Step 1: 5

```text id="t18"
left = [5]
right = []
median = 5
```

---

### Step 2: 15

```text id="t19"
left = [5]
right = [15]
median = (5 + 15)/2 = 10
```

---

### Step 3: 1

```text id="t20"
left = [5,1]
right = [15]
median = 5
```

---

### Step 4: 3

```text id="t21"
left = [3,1]
right = [5,15]
median = (3 + 5)/2 = 4
```

---

# Why It Works

We always maintain:

```text id="t22"
Left = smaller half

Right = larger half
```

So median is always near the boundary.

---

# Important Insights

### Insight 1

We never sort full stream:

```text id="t23"
Only maintain partial order using heaps
```

---

### Insight 2

Balancing is critical:

```text id="t24"
Without balance → wrong median
```

---

### Insight 3

Max heap helps get:

```text id="t25"
Middle-left value instantly
```

---

### Insight 4

This pattern is:

```text id="t26"
Dynamic version of sorted array median
```

---

# Common Interview Problems

```text id="t27"
295  - Find Median from Data Stream

480  - Sliding Window Median

703  - Kth Largest Element in a Stream

502  - IPO (Max Heap variant)

1578 - Minimum Time to Make Rope Colorful (greedy + heap mix)
```

---

# Pattern Map

| Problem Type          | Technique                |
| --------------------- | ------------------------ |
| Median in stream      | Two Heaps                |
| Sliding window median | Two Heaps + Lazy removal |
| Kth largest stream    | Min Heap                 |
| Dynamic ranking       | Heaps                    |

---

# Quick Revision

```text id="t28"
Need Median in Stream
        ↓
Split into two halves
        ↓
Left = Max Heap
Right = Min Heap
        ↓
Balance sizes
        ↓
Median = Top(s)
```

---

# Master Formula

```text id="t29"
Two Heaps Pattern

=

Left Max Heap (smaller half)
+
Right Min Heap (larger half)

-------------------------

Balance sizes

Maintain order

Get median instantly

-------------------------

Median = Boundary of two heaps
```
