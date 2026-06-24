# Increasing + Decreasing Stack

## Core Idea

A Monotonic Stack maintains elements in a specific order.

Two types:

```text id="a1b2c3"
Monotonic Increasing Stack

Monotonic Decreasing Stack
```

These are the foundation of almost every stack interview problem.

---

## When to Use

* Next Greater Element.
* Next Smaller Element.
* Previous Greater Element.
* Previous Smaller Element.
* Histogram.
* Stock Span.
* Contribution Technique.
* Subarray Minimums.
* Subarray Maximums.

---

## Trigger Words

* Nearest greater
* Nearest smaller
* First greater
* First smaller
* Monotonic
* Span
* Histogram
* Contribution

---

# Monotonic Increasing Stack

## Definition

Elements remain:

```text id="d4e5f6"
Increasing

Bottom → Top
```

Example:

```text id="g7h8i9"
1
3
5
8
```

---

## Pop Condition

```java id="j0k1l2"
while(!st.isEmpty() &&
      st.peek() >= nums[i]){

    st.pop();
}
```

---

## Why?

Remove elements that cannot become:

```text id="m3n4o5"
Next Smaller

Previous Smaller
```

for future elements.

---

## Used For

```text id="p6q7r8"
NSE

PSE

Histogram

Subarray Minimums
```

---

## Generic Template

```java id="s9t0u1"
Stack<Integer> st =
        new Stack<>();

for(int i = 0; i < n; i++){

    while(!st.isEmpty() &&
          st.peek() >= nums[i]){

        st.pop();
    }

    st.push(nums[i]);
}
```

---

# Monotonic Decreasing Stack

## Definition

Elements remain:

```text id="v2w3x4"
Decreasing

Bottom → Top
```

Example:

```text id="y5z6a7"
8
6
4
2
```

---

## Pop Condition

```java id="b8c9d0"
while(!st.isEmpty() &&
      st.peek() <= nums[i]){

    st.pop();
}
```

---

## Why?

Remove elements that cannot become:

```text id="e1f2g3"
Next Greater

Previous Greater
```

for future elements.

---

## Used For

```text id="h4i5j6"
NGE

PGE

Stock Span

Subarray Maximums
```

---

## Generic Template

```java id="k7l8m9"
Stack<Integer> st =
        new Stack<>();

for(int i = 0; i < n; i++){

    while(!st.isEmpty() &&
          st.peek() <= nums[i]){

        st.pop();
    }

    st.push(nums[i]);
}
```

---

# Visual Understanding

## Increasing Stack

### Insert

```text id="n0o1p2"
4 2 5 1
```

---

### Process 4

```text id="q3r4s5"
4
```

---

### Process 2

```text id="t6u7v8"
Pop 4

2
```

---

### Process 5

```text id="w9x0y1"
2
5
```

---

### Process 1

```text id="z2a3b4"
Pop 5

Pop 2

1
```

---

## Final

```text id="c5d6e7"
Increasing Order
```

---

# Stack Selection Rule

## Need Smaller?

Use:

```text id="f8g9h0"
Increasing Stack
```

---

## Need Greater?

Use:

```text id="i1j2k3"
Decreasing Stack
```

---

# Direction Rule

| Problem | Direction    |
| ------- | ------------ |
| NGE     | Right → Left |
| NSE     | Right → Left |
| PGE     | Left → Right |
| PSE     | Left → Right |

---

# Pop Rule Cheat Sheet

| Need    | Pop Condition |
| ------- | ------------- |
| Greater | <=            |
| Smaller | >=            |

---

# Important Insights

### Insight 1

Every element is:

```text id="l4m5n6"
Pushed Once

Popped Once
```

Hence:

```text id="o7p8q9"
O(N)
```

---

### Insight 2

Top of stack always stores:

```text id="r0s1t2"
Nearest Candidate
```

---

### Insight 3

Elements popped once:

```text id="u3v4w5"
Never Return
```

---

### Insight 4

Most monotonic stack problems are:

```text id="x6y7z8"
Nearest Element Problems
```

in disguise.

---

# Problem 1: LeetCode 739 - Daily Temperatures

## Problem Statement

Find number of days until warmer temperature.

---

## Approach

Need:

```text id="a9b0c1"
Next Greater Element
```

Use:

```text id="d2e3f4"
Monotonic Decreasing Stack
```

---

## Solution Pattern

```java id="g5h6i7"
while(!st.isEmpty() &&
      temp[st.peek()] <= temp[i]){

    st.pop();
}
```

---

### TC

```text id="j8k9l0"
O(N)
```

### SC

```text id="m1n2o3"
O(N)
```

---

# Problem 2: LeetCode 907 - Sum of Subarray Minimums

## Problem Statement

Find sum of minimums of all subarrays.

---

## Approach

Need:

```text id="p4q5r6"
Previous Smaller

Next Smaller
```

Use:

```text id="s7t8u9"
Monotonic Increasing Stack
```

---

### TC

```text id="v0w1x2"
O(N)
```

### SC

```text id="y3z4a5"
O(N)
```

---

# Problem 3: LeetCode 901 - Online Stock Span

## Problem Statement

Find stock span.

---

## Approach

Need:

```text id="b6c7d8"
Previous Greater
```

Use:

```text id="e9f0g1"
Monotonic Decreasing Stack
```

---

### TC

```text id="h2i3j4"
O(N)
```

### SC

```text id="k5l6m7"
O(N)
```

---

# Common Interview Problems

```text id="n8o9p0"
496  - Next Greater Element I

503  - Next Greater Element II

739  - Daily Temperatures

901  - Online Stock Span

84   - Largest Rectangle In Histogram

85   - Maximal Rectangle

907  - Sum Of Subarray Minimums

2104 - Sum Of Subarray Ranges
```

---

# Increasing vs Decreasing Stack

| Feature       | Increasing Stack | Decreasing Stack |
| ------------- | ---------------- | ---------------- |
| Order         | Small → Large    | Large → Small    |
| Pop Condition | >=               | <=               |
| Finds         | Smaller          | Greater          |
| Used In       | NSE, PSE         | NGE, PGE         |
| Contribution  | Minimums         | Maximums         |

---

# Quick Revision

```text id="q1r2s3"
Need Smaller?
        ↓
Increasing Stack
        ↓
Pop >=

-------------------

Need Greater?
        ↓
Decreasing Stack
        ↓
Pop <=

-------------------

Push Once

Pop Once

O(N)
```

---

# Master Formula

```text id="t4u5v6"
Smaller Problems

→ Increasing Stack

Pop >=

----------------

Greater Problems

→ Decreasing Stack

Pop <=

----------------

Nearest Element

→ Monotonic Stack

----------------

Push Once

Pop Once

O(N)
```
