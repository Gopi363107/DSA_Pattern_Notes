# Monotonic Queue

## Core Idea

A Monotonic Queue maintains elements in:

```text
Increasing Order

OR

Decreasing Order
```

while supporting:

```text
Insert

Delete

Get Min/Max
```

in:

```text
O(1)
```

amortized time.

---

## Why Not Stack?

Stack solves:

```text
Nearest Element Problems
```

Queue solves:

```text
Sliding Window Problems
```

---

## When to Use

* Sliding Window Maximum.
* Sliding Window Minimum.
* Fixed size window.
* Dynamic window.
* Stream processing.
* Window optimization.

---

## Trigger Words

* Sliding window
* Window size k
* Maximum in window
* Minimum in window
* Moving window
* Continuous subarray
* Stream data

---

## Recognition Pattern

```text
Array
  ↓
Window Size K
  ↓
Need Max / Min
For Every Window
  ↓
Monotonic Queue
```

---

# Monotonic Decreasing Queue

## Purpose

Find:

```text
Maximum
```

inside every window.

---

## Structure

```text
Front → Largest

Back → Smallest
```

Example:

```text
9 7 5 2
```

---

## Insert Rule

```java
while(!dq.isEmpty() &&
      nums[dq.peekLast()] <= nums[i]){

    dq.pollLast();
}
```

Then:

```java
dq.offerLast(i);
```

---

## Why?

Smaller elements can never become maximum.

Remove them.

---

# Monotonic Increasing Queue

## Purpose

Find:

```text
Minimum
```

inside every window.

---

## Structure

```text
Front → Smallest

Back → Largest
```

Example:

```text
1 3 5 8
```

---

## Insert Rule

```java
while(!dq.isEmpty() &&
      nums[dq.peekLast()] >= nums[i]){

    dq.pollLast();
}
```

Then:

```java
dq.offerLast(i);
```

---

## Why?

Larger elements can never become minimum.

Remove them.

---

# Window Expiration Rule

Before processing:

```java
if(dq.peekFirst() <= i - k){

    dq.pollFirst();
}
```

---

## Meaning

Remove indices that moved outside the window.

---

# General Template (Maximum)

```java
Deque<Integer> dq =
        new ArrayDeque<>();

for(int i = 0; i < n; i++){

    while(!dq.isEmpty() &&
          dq.peekFirst() <= i - k){

        dq.pollFirst();
    }

    while(!dq.isEmpty() &&
          nums[dq.peekLast()] <= nums[i]){

        dq.pollLast();
    }

    dq.offerLast(i);

    if(i >= k - 1){

        answer.add(
            nums[dq.peekFirst()]
        );
    }
}
```

---

## Time Complexity

```text
O(N)
```

---

## Space Complexity

```text
O(K)
```

---

# Important Insights

### Insight 1

Store:

```text
Indices

NOT Values
```

---

### Insight 2

Front always contains:

```text
Current Maximum

OR

Current Minimum
```

---

### Insight 3

Every element is:

```text
Inserted Once

Removed Once
```

Hence:

```text
O(N)
```

---

### Insight 4

Queue always contains:

```text
Useful Candidates
```

Only.

---

# Visual Understanding

## Example

```text
nums = [1,3,-1,-3,5,3,6,7]

k = 3
```

---

### Window

```text
1 3 -1

Max = 3
```

---

### Window

```text
3 -1 -3

Max = 3
```

---

### Window

```text
-1 -3 5

Max = 5
```

---

# Problem 1: LeetCode 239 - Sliding Window Maximum

## Problem Statement

Find maximum value in every window of size k.

---

## Approach

Use:

```text
Monotonic Decreasing Queue
```

Front always stores maximum.

---

## Solution

```java
class Solution {

    public int[] maxSlidingWindow(
            int[] nums,
            int k) {

        int n = nums.length;

        int[] ans =
            new int[n - k + 1];

        Deque<Integer> dq =
            new ArrayDeque<>();

        int idx = 0;

        for(int i = 0; i < n; i++){

            while(!dq.isEmpty() &&
                  dq.peekFirst() <= i - k){

                dq.pollFirst();
            }

            while(!dq.isEmpty() &&
                  nums[dq.peekLast()] <= nums[i]){

                dq.pollLast();
            }

            dq.offerLast(i);

            if(i >= k - 1){

                ans[idx++] =
                    nums[dq.peekFirst()];
            }
        }

        return ans;
    }
}
```

### TC

```text
O(N)
```

### SC

```text
O(K)
```

---

# Problem 2: LeetCode 862 - Shortest Subarray with Sum at Least K

## Problem Statement

Find shortest subarray having sum ≥ K.

---

## Approach

Use:

```text
Prefix Sum
      +
Monotonic Increasing Queue
```

Maintain increasing prefix sums.

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

# Problem 3: LeetCode 1438 - Longest Continuous Subarray With Absolute Diff ≤ Limit

## Problem Statement

Find longest valid subarray.

---

## Approach

Maintain:

```text
Maximum Queue

+

Minimum Queue
```

Window valid if:

```text
max - min <= limit
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

1438 - Longest Continuous Subarray

1696 - Jump Game VI

1425 - Constrained Subsequence Sum

1499 - Max Value Of Equation
```

---

# Monotonic Stack vs Monotonic Queue

| Feature         | Stack           | Queue          |
| --------------- | --------------- | -------------- |
| Purpose         | Nearest Element | Sliding Window |
| Structure       | LIFO            | FIFO           |
| NGE/NSE         | Yes             | No             |
| Window Problems | No              | Yes            |
| Max/Min Window  | No              | Yes            |
| Complexity      | O(N)            | O(N)           |

---

# Quick Revision

```text
Need Nearest Greater?
        ↓
Monotonic Stack

------------------

Need Window Maximum?
        ↓
Monotonic Queue

------------------

Maximum Window
        ↓
Decreasing Queue

------------------

Minimum Window
        ↓
Increasing Queue

------------------

Each Element

Enter Once

Leave Once

O(N)
```

---

# Master Formula

```text
Sliding Window
        ↓
Need Maximum
        ↓
Decreasing Queue

------------------

Sliding Window
        ↓
Need Minimum
        ↓
Increasing Queue

------------------
Front
=
Answer
------------------
O(N)
```
