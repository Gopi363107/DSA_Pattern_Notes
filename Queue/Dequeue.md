# Deque (Double Ended Queue)

## Core Idea

Deque stands for:

```text
Double Ended Queue
```

It allows insertion and deletion from:

```text
Front

AND

Back
```

in:

```text
O(1)
```

time.

---

## Definition

Unlike:

```text
Stack
```

which works on:

```text
LIFO
```

and

```text
Queue
```

which works on:

```text
FIFO
```

Deque supports:

```text
Insert Front

Insert Back

Delete Front

Delete Back
```

---

## Visualization

```text
Front                    Back

← 10 20 30 40 50 →
```

Operations can happen at both ends.

---

## When to Use

* Sliding Window Maximum
* Sliding Window Minimum
* Monotonic Queue
* Circular Queue
* LRU Cache
* Palindrome Checking
* 0-1 BFS

---

## Trigger Words

* Double ended
* Front and back
* Sliding window
* Monotonic queue
* Remove from both ends
* Circular structure

---

# Java Implementation

## Declaration

```java
Deque<Integer> dq =
        new ArrayDeque<>();
```

---

# Insertion Operations

## Insert Front

```java
dq.offerFirst(10);
```

---

## Insert Back

```java
dq.offerLast(20);
```

---

## Example

```java
dq.offerFirst(10);
dq.offerLast(20);
dq.offerLast(30);
```

Deque:

```text
10 20 30
```

---

# Deletion Operations

## Delete Front

```java
dq.pollFirst();
```

---

## Delete Back

```java
dq.pollLast();
```

---

## Example

```java
10 20 30

pollFirst()
```

Result:

```text
20 30
```

---

# Peek Operations

## Front Element

```java
dq.peekFirst();
```

---

## Back Element

```java
dq.peekLast();
```

---

# Complete Template

```java
Deque<Integer> dq =
        new ArrayDeque<>();

dq.offerFirst(10);

dq.offerLast(20);

dq.offerLast(30);

System.out.println(
    dq.peekFirst()
);

System.out.println(
    dq.peekLast()
);

dq.pollFirst();

dq.pollLast();
```

---

# Time Complexity

| Operation  | Complexity |
| ---------- | ---------- |
| offerFirst | O(1)       |
| offerLast  | O(1)       |
| pollFirst  | O(1)       |
| pollLast   | O(1)       |
| peekFirst  | O(1)       |
| peekLast   | O(1)       |

---

# Space Complexity

```text
O(N)
```

---

# Important Insights

### Insight 1

Deque can act as:

```text
Stack
```

using:

```java
offerLast()
pollLast()
```

---

### Insight 2

Deque can act as:

```text
Queue
```

using:

```java
offerLast()
pollFirst()
```

---

### Insight 3

Most competitive programmers prefer:

```java
ArrayDeque
```

instead of:

```java
Stack
```

because it is faster.

---

### Insight 4

Monotonic Queue is implemented using:

```java
Deque<Integer>
```

---

# Deque as Stack

## Push

```java
dq.offerLast(x);
```

---

## Pop

```java
dq.pollLast();
```

---

## Top

```java
dq.peekLast();
```

---

# Deque as Queue

## Enqueue

```java
dq.offerLast(x);
```

---

## Dequeue

```java
dq.pollFirst();
```

---

## Front

```java
dq.peekFirst();
```

---

# Problem 1: LeetCode 239 - Sliding Window Maximum

## Problem Statement

Find maximum element in every window.

---

## Approach

Use:

```text
Monotonic Decreasing Deque
```

Front always stores maximum.

---

### TC

```text
O(N)
```

### SC

```text
O(K)
```

---

# Problem 2: LeetCode 862 - Shortest Subarray With Sum At Least K

## Problem Statement

Find shortest subarray having sum ≥ K.

---

## Approach

Use:

```text
Prefix Sum

+

Monotonic Deque
```

---

### TC

```text
O(N)
```

### SC

```text
O(N)
```

---

# Problem 3: LeetCode 1696 - Jump Game VI

## Problem Statement

Find maximum score.

---

## Approach

Maintain:

```text
Maximum DP Value
```

inside a sliding window.

Use:

```text
Monotonic Deque
```

---

### TC

```text
O(N)
```

### SC

```text
O(N)
```

---

# Common Interview Problems

```text
239  - Sliding Window Maximum

862  - Shortest Subarray With Sum At Least K

1696 - Jump Game VI

1425 - Constrained Subsequence Sum

1499 - Max Value Of Equation

1438 - Longest Continuous Subarray
```

---

# Queue vs Deque

| Feature         | Queue | Deque |
| --------------- | ----- | ----- |
| Insert Front    | ❌     | ✅     |
| Insert Back     | ✅     | ✅     |
| Delete Front    | ✅     | ✅     |
| Delete Back     | ❌     | ✅     |
| Sliding Window  | ❌     | ✅     |
| Monotonic Queue | ❌     | ✅     |

---

# Stack vs Queue vs Deque

| DS    | Order |
| ----- | ----- |
| Stack | LIFO  |
| Queue | FIFO  |
| Deque | Both  |

---

# Quick Revision

```text
Need Front Only
        ↓
Queue

----------------

Need Front + Back
        ↓
Deque

----------------

Sliding Window
        ↓
Deque

----------------

Monotonic Queue
        ↓
Deque

----------------

All Operations

O(1)
```

---

# Master Formula

```text
Deque

=

Queue

+

Stack

----------------

Insert Front

Insert Back

Delete Front

Delete Back

----------------

Used In

Sliding Window

Monotonic Queue

0-1 BFS

LRU Cache
```
