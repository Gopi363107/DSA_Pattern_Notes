# Monotonic Stack + Histogram Pattern

## Core Idea

For every bar:

```text
Height = Current Bar

Width = Maximum Expansion
        To Left And Right
```

Use Monotonic Stack to find:

```text
Previous Smaller Element (PSE)

Next Smaller Element (NSE)
```

which determine the width.

---

## When to Use

* Largest rectangle problems.
* Histogram problems.
* Maximum area.
* Rectangle expansion.
* Binary matrix rectangle problems.
* Width based optimization.

---

## Trigger Words

* Largest rectangle
* Histogram
* Maximum area
* Rectangle area
* Expand left and right
* Width calculation
* Previous smaller
* Next smaller

---

## Recognition Pattern

```text
Need Maximum Area
         ↓
Area = Height × Width
         ↓
Need Maximum Width
         ↓
Find First Smaller
On Left And Right
         ↓
Monotonic Stack
```

---

# Core Formula

For every index:

```text
Height = nums[i]
```

---

## Left Boundary

```text
PSE
```

Previous Smaller Element

---

## Right Boundary

```text
NSE
```

Next Smaller Element

---

## Width

```text
NSE - PSE - 1
```

---

## Area

```text
Height × Width
```

---

## Final Formula

```text
Area

=

nums[i]

×

(NSE - PSE - 1)
```

---

# Visual Understanding

## Histogram

```text
Index

0 1 2 3 4 5

Height

2 1 5 6 2 3
```

---

For:

```text
Height = 5
```

---

## Previous Smaller

```text
Index = 1

Height = 1
```

---

## Next Smaller

```text
Index = 4

Height = 2
```

---

## Width

```text
4 - 1 - 1

= 2
```

---

## Area

```text
5 × 2

= 10
```

---

# PSE Template

```java
int[] pse = new int[n];

Stack<Integer> st =
        new Stack<>();

for(int i = 0; i < n; i++){

    while(!st.isEmpty() &&
          heights[st.peek()] >= heights[i]){

        st.pop();
    }

    pse[i] =
        st.isEmpty()
        ? -1
        : st.peek();

    st.push(i);
}
```

---

# NSE Template

```java
int[] nse = new int[n];

Stack<Integer> st =
        new Stack<>();

for(int i = n - 1; i >= 0; i--){

    while(!st.isEmpty() &&
          heights[st.peek()] >= heights[i]){

        st.pop();
    }

    nse[i] =
        st.isEmpty()
        ? n
        : st.peek();

    st.push(i);
}
```

---

# Area Calculation

```java
long maxArea = 0;

for(int i = 0; i < n; i++){

    long width =
        nse[i] - pse[i] - 1;

    long area =
        (long)heights[i] * width;

    maxArea =
        Math.max(maxArea, area);
}
```

---

# Optimized One Pass Template

No need to explicitly compute:

```text
PSE

NSE
```

Compute area while popping.

---

## One Pass Code

```java
public int largestRectangleArea(
        int[] heights){

    int n = heights.length;

    Stack<Integer> st =
            new Stack<>();

    int maxArea = 0;

    for(int i = 0; i <= n; i++){

        while(!st.isEmpty() &&
             (i == n ||
              heights[st.peek()] >= heights[i])){

            int height =
                heights[st.pop()];

            int nse = i;

            int pse =
                st.isEmpty()
                ? -1
                : st.peek();

            int width =
                nse - pse - 1;

            maxArea =
                Math.max(
                    maxArea,
                    height * width
                );
        }

        st.push(i);
    }

    return maxArea;
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

# Important Insights

### Insight 1

When a bar gets popped:

```text
Current Index
=
Next Smaller
```

---

### Insight 2

After pop:

```text
Stack Top
=
Previous Smaller
```

---

### Insight 3

Every bar is:

```text
Pushed Once

Popped Once
```

Hence:

```text
O(N)
```

---

### Insight 4

Histogram Pattern is basically:

```text
Nearest Smaller Left

+

Nearest Smaller Right

+

Area Formula
```

---

# Problem 1: LeetCode 84 - Largest Rectangle in Histogram

## Problem Statement

Find largest rectangle area.

---

## Approach

For every bar:

```text
Find Maximum Width
```

using:

```text
PSE + NSE
```

---

## Solution

```java
class Solution {

    public int largestRectangleArea(
            int[] heights){

        int n = heights.length;

        Stack<Integer> st =
                new Stack<>();

        int maxArea = 0;

        for(int i = 0; i <= n; i++){

            while(!st.isEmpty() &&
                 (i == n ||
                  heights[st.peek()] >= heights[i])){

                int height =
                    heights[st.pop()];

                int nse = i;

                int pse =
                    st.isEmpty()
                    ? -1
                    : st.peek();

                int width =
                    nse - pse - 1;

                maxArea =
                    Math.max(
                        maxArea,
                        height * width
                    );
            }

            st.push(i);
        }

        return maxArea;
    }
}
```

### TC

```text
O(N)
```

### SC

```text
O(N)
```

---

# Problem 2: LeetCode 85 - Maximal Rectangle

## Problem Statement

Find largest rectangle of:

```text
1's
```

inside a binary matrix.

---

## Core Observation

Convert every row into a histogram.

Example:

```text
1 0 1 0 0

↓

1 0 1 0 0

↓

2 0 2 1 1

↓

3 1 3 2 2
```

---

## Approach

For each row:

```text
Build Histogram
       ↓
Largest Rectangle Histogram
       ↓
Update Answer
```

---

### TC

```text
O(R × C)
```

### SC

```text
O(C)
```

---

# Problem 3: LeetCode 1793 - Maximum Score of a Good Subarray

## Core Observation

Need largest width around a pivot.

Use Histogram-style expansion.

Find nearest smaller elements.

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
84   - Largest Rectangle In Histogram

85   - Maximal Rectangle

1793 - Maximum Score Of A Good Subarray

1727 - Largest Submatrix With Rearrangements

221  - Maximal Square (Related)
```

---

# Histogram Pattern vs Contribution Pattern

| Pattern      | Formula              |
| ------------ | -------------------- |
| Contribution | value × left × right |
| Histogram    | height × width       |

---

## Quick Revision

```text
Need Maximum Area
        ↓
Area = Height × Width
        ↓
Need Width
        ↓
Find PSE
Find NSE
        ↓
Width = NSE - PSE - 1
        ↓
Area = Height × Width
        ↓
Maximum Answer
```

---

# Master Formula

```text
For Every Bar

Find Previous Smaller

Find Next Smaller

Width

=

NSE - PSE - 1

Area

=

Height × Width

Take Maximum
```
