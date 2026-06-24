# NGE + NSE + PGE + PSE

## Core Idea

Monotonic Stack helps find:

```text
Nearest Greater Element

Nearest Smaller Element
```

in:

```text
O(N)
```

instead of:

```text
O(N²)
```

---

## Full Forms

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
* Histogram.
* Subarray minimum.
* Subarray maximum.
* Monotonic stack problems.

---

## Trigger Words

* Next greater
* Previous greater
* Next smaller
* Previous smaller
* Nearest greater
* Nearest smaller
* First greater
* First smaller

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

# NGE (Next Greater Element)

## Definition

Find first greater element on the right.

---

## Example

```text
Array

2 1 4 3

NGE

4 4 -1 -1
```

---

## Template

```java
public int[] nextGreaterElement(
        int[] nums){

    int n = nums.length;

    int[] nge = new int[n];

    Stack<Integer> st =
            new Stack<>();

    for(int i = n - 1; i >= 0; i--){

        while(!st.isEmpty() &&
              st.peek() <= nums[i]){

            st.pop();
        }

        nge[i] =
            st.isEmpty()
            ? -1
            : st.peek();

        st.push(nums[i]);
    }

    return nge;
}
```

### Stack Type

```text
Monotonic Decreasing Stack
```

---

# NSE (Next Smaller Element)

## Definition

Find first smaller element on the right.

---

## Example

```text
Array

4 2 5 1

NSE

2 1 1 -1
```

---

## Template

```java
public int[] nextSmallerElement(
        int[] nums){

    int n = nums.length;

    int[] nse = new int[n];

    Stack<Integer> st =
            new Stack<>();

    for(int i = n - 1; i >= 0; i--){

        while(!st.isEmpty() &&
              st.peek() >= nums[i]){

            st.pop();
        }

        nse[i] =
            st.isEmpty()
            ? -1
            : st.peek();

        st.push(nums[i]);
    }

    return nse;
}
```

### Stack Type

```text
Monotonic Increasing Stack
```

---

# PGE (Previous Greater Element)

## Definition

Find first greater element on the left.

---

## Example

```text
Array

2 1 4 3

PGE

-1 2 -1 4
```

---

## Template

```java
public int[] previousGreaterElement(
        int[] nums){

    int n = nums.length;

    int[] pge = new int[n];

    Stack<Integer> st =
            new Stack<>();

    for(int i = 0; i < n; i++){

        while(!st.isEmpty() &&
              st.peek() <= nums[i]){

            st.pop();
        }

        pge[i] =
            st.isEmpty()
            ? -1
            : st.peek();

        st.push(nums[i]);
    }

    return pge;
}
```

### Stack Type

```text
Monotonic Decreasing Stack
```

---

# PSE (Previous Smaller Element)

## Definition

Find first smaller element on the left.

---

## Example

```text
Array

4 2 5 1

PSE

-1 -1 2 -1
```

---

## Template

```java
public int[] previousSmallerElement(
        int[] nums){

    int n = nums.length;

    int[] pse = new int[n];

    Stack<Integer> st =
            new Stack<>();

    for(int i = 0; i < n; i++){

        while(!st.isEmpty() &&
              st.peek() >= nums[i]){

            st.pop();
        }

        pse[i] =
            st.isEmpty()
            ? -1
            : st.peek();

        st.push(nums[i]);
    }

    return pse;
}
```

### Stack Type

```text
Monotonic Increasing Stack
```

---

# Direction Trick

| Pattern | Direction    |
| ------- | ------------ |
| NGE     | Right → Left |
| NSE     | Right → Left |
| PGE     | Left → Right |
| PSE     | Left → Right |

---

# Stack Trick

| Pattern | Pop Condition |
| ------- | ------------- |
| NGE     | <=            |
| NSE     | >=            |
| PGE     | <=            |
| PSE     | >=            |

---

# Index Version

Most interview problems require:

```text
Index

NOT Value
```

Store:

```java
Stack<Integer> st;
```

containing indices.

---

## NGE Index Template

```java
for(int i=n-1;i>=0;i--){

    while(!st.isEmpty() &&
          nums[st.peek()] <= nums[i]){

        st.pop();
    }

    nge[i] =
        st.isEmpty()
        ? -1
        : st.peek();

    st.push(i);
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
O(N)
```

---

# Problem 1: LeetCode 496 - Next Greater Element I

## Problem Statement

For each element find next greater element.

---

## Approach

Use NGE.

Store answers using stack.

---

## TC

```text
O(N)
```

### SC

```text
O(N)
```

---

# Problem 2: LeetCode 503 - Next Greater Element II

## Problem Statement

Find NGE in circular array.

---

## Approach

Traverse:

```text
2 * N
```

elements.

Use modulo.

```java
i % n
```

---

## TC

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
Need Nearest Greater?

→ Monotonic Decreasing Stack

---------------------

Need Nearest Smaller?

→ Monotonic Increasing Stack

---------------------

Need Right Side?

→ Traverse Right To Left

---------------------

Need Left Side?

→ Traverse Left To Right

---------------------

Each Element

Push Once
Pop Once

O(N)
```
