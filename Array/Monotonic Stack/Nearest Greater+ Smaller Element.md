# Nearest Greater/Smaller Element

## Core Idea

Find the nearest element that is:

```text
Greater
OR
Smaller
```

on either:

```text
Left Side
OR
Right Side
```

using a Monotonic Stack.

---

## Types

```text
NGE → Next Greater Element

NSE → Next Smaller Element

PGE → Previous Greater Element

PSE → Previous Smaller Element
```

---

## When to Use

* Nearest greater element.
* Nearest smaller element.
* Stock span.
* Histogram problems.
* Subarray minimum.
* Subarray maximum.
* Monotonic stack problems.

---

## Trigger Words

* Nearest greater
* Nearest smaller
* First greater
* First smaller
* Next greater
* Previous greater
* Next smaller
* Previous smaller

---

## General Pattern

```text
Current Element
        ↓
Remove Useless Elements
        ↓
Top Of Stack
        ↓
Nearest Answer
        ↓
Push Current Element
```

---

## Recognition Pattern

```text
Need Nearest Element
           ↓
Greater / Smaller
           ↓
Left / Right
           ↓
Monotonic Stack
```

---

# Monotonic Stack Types

## Monotonic Increasing Stack

```text
Bottom → Top

1
2
4
8
```

Used For:

```text
Smaller Element Problems
```

---

## Monotonic Decreasing Stack

```text
Bottom → Top

8
5
3
1
```

Used For:

```text
Greater Element Problems
```

---

# Direction Rule

| Problem          | Direction    |
| ---------------- | ------------ |
| Next Greater     | Right → Left |
| Next Smaller     | Right → Left |
| Previous Greater | Left → Right |
| Previous Smaller | Left → Right |

---

# Pop Rule

| Problem | Pop Condition |
| ------- | ------------- |
| Greater | <=            |
| Smaller | >=            |

---

# Generic Template

## Next Greater Element

```java
for(int i=n-1;i>=0;i--){

    while(!st.isEmpty() &&
          st.peek() <= nums[i]){

        st.pop();
    }

    ans[i] =
        st.isEmpty()
        ? -1
        : st.peek();

    st.push(nums[i]);
}
```

---

## Next Smaller Element

```java
for(int i=n-1;i>=0;i--){

    while(!st.isEmpty() &&
          st.peek() >= nums[i]){

        st.pop();
    }

    ans[i] =
        st.isEmpty()
        ? -1
        : st.peek();

    st.push(nums[i]);
}
```

---

## Previous Greater Element

```java
for(int i=0;i<n;i++){

    while(!st.isEmpty() &&
          st.peek() <= nums[i]){

        st.pop();
    }

    ans[i] =
        st.isEmpty()
        ? -1
        : st.peek();

    st.push(nums[i]);
}
```

---

## Previous Smaller Element

```java
for(int i=0;i<n;i++){

    while(!st.isEmpty() &&
          st.peek() >= nums[i]){

        st.pop();
    }

    ans[i] =
        st.isEmpty()
        ? -1
        : st.peek();

    st.push(nums[i]);
}
```

---

# Index Version

Most interview problems need:

```text
Indices

NOT Values
```

Store:

```java
Stack<Integer> st;
```

containing indices.

---

## Index Template

```java
while(!st.isEmpty() &&
      nums[st.peek()] <= nums[i]){

    st.pop();
}
```

---

# Important Insights

### Insight 1

Every element is:

```text
Pushed Once

Popped Once
```

Therefore:

```text
O(N)
```

---

### Insight 2

Stack Top Always Represents:

```text
Nearest Valid Candidate
```

---

### Insight 3

When an element becomes useless:

```text
Remove It Forever
```

using pop.

---

### Insight 4

Most Monotonic Stack Problems are:

```text
Nearest Element Problems
```

in disguise.

---

# Visual Understanding

## NGE Example

```text
Array

2 1 4 3
```

---

### Process 3

```text
Stack

3

NGE = -1
```

---

### Process 4

```text
Pop 3

Stack Empty

NGE = -1
```

---

### Process 1

```text
Stack

4

NGE = 4
```

---

### Process 2

```text
Stack

4

NGE = 4
```

---

### Answer

```text
4 4 -1 -1
```

---

# Time Complexity

```text
O(N)
```

---

# Space Complexity

```text
O(N)
```

---

# Problem 1: LeetCode 496 - Next Greater Element I

## Problem Statement

Find next greater element for each number.

---

## Approach

Use:

```text
Monotonic Decreasing Stack
```

to compute NGE.

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

# Problem 2: LeetCode 739 - Daily Temperatures

## Problem Statement

Find days until a warmer temperature.

---

## Approach

Find:

```text
Next Greater Element
```

using indices.

---

## Solution Pattern

```java
while(!st.isEmpty() &&
      temp[st.peek()] <= temp[i]){

    st.pop();
}
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

# Problem 3: LeetCode 901 - Online Stock Span

## Problem Statement

Find span of stock prices.

---

## Approach

Find:

```text
Previous Greater Element
```

using a monotonic stack.

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

# Master Formula

```text
Need Greater?
    ↓
Monotonic Decreasing Stack

Need Smaller?
    ↓
Monotonic Increasing Stack

Need Next?
    ↓
Right → Left

Need Previous?
    ↓
Left → Right

Push Once
Pop Once

O(N)
```

---

# Quick Revision Table

| Problem | Stack Type | Direction    |
| ------- | ---------- | ------------ |
| NGE     | Decreasing | Right → Left |
| NSE     | Increasing | Right → Left |
| PGE     | Decreasing | Left → Right |
| PSE     | Increasing | Left → Right |

```
Pop <= → Greater Problems

Pop >= → Smaller Problems
```
