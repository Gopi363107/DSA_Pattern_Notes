# Monotonic Stack + Contribution Technique

## Core Idea

Instead of finding answers for every subarray:

```text
O(N²)
```

Find:

```text
How Much Each Element Contributes
```

to the final answer.

Use:

```text
Monotonic Stack
       +
Contribution Counting
```

to achieve:

```text
O(N)
```

---

## When to Use

* Sum of subarray minimums.
* Sum of subarray maximums.
* Sum of subarray ranges.
* Histogram problems.
* Contribution counting.
* Nearest greater/smaller problems.

---

## Trigger Words

* Sum of minimums
* Sum of maximums
* Contribution
* Every subarray
* Count subarrays
* Total contribution
* Range contribution

---

## Recognition Pattern

```text
Need Answer For
All Subarrays
        ↓
Brute Force O(N²)
Too Large
        ↓
Find Contribution
Of Each Element
        ↓
Monotonic Stack
```

---

# Contribution Formula

Suppose:

```text
nums[i]
```

is the minimum.

Find:

```text
Previous Smaller Element
(PSE)

Next Smaller Element
(NSE)
```

---

## Left Choices

```text
left = i - PSE
```

---

## Right Choices

```text
right = NSE - i
```

---

## Total Subarrays

where nums[i] is minimum:

```text
left × right
```

---

## Contribution

```text
nums[i] × left × right
```

---

# For Minimum Contribution

Need:

```text
Previous Smaller

Next Smaller
```

---

## Formula

```text
Contribution

=

nums[i]

×

(i - PSE)

×

(NSE - i)
```

---

# For Maximum Contribution

Need:

```text
Previous Greater

Next Greater
```

---

## Formula

```text
Contribution

=

nums[i]

×

(i - PGE)

×

(NGE - i)
```

---

# Why It Works

For every element:

```text
Choose Left Boundary

×

Choose Right Boundary
```

Every combination creates one valid subarray.

---

# Visual Understanding

## Example

```text
1 3 2
```

For:

```text
3
```

---

### Previous Greater

```text
none

PGE = -1
```

---

### Next Greater

```text
none

NGE = n
```

---

### Left Choices

```text
1 - (-1)

= 2
```

---

### Right Choices

```text
3 - 1

= 2
```

---

### Contribution

```text
3 × 2 × 2

= 12
```

---

# Generic Minimum Template

## PSE

```java
for(int i = 0; i < n; i++){

    while(!st.isEmpty() &&
          nums[st.peek()] > nums[i]){

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

## NSE

```java
for(int i = n - 1; i >= 0; i--){

    while(!st.isEmpty() &&
          nums[st.peek()] >= nums[i]){

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

# Contribution Calculation

```java
long answer = 0;

for(int i = 0; i < n; i++){

    long left =
        i - pse[i];

    long right =
        nse[i] - i;

    answer +=
        (long)nums[i]
        * left
        * right;
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

# Problem 1: LeetCode 907 - Sum of Subarray Minimums

## Problem Statement

Find:

```text
Sum Of Minimum
Of Every Subarray
```

---

## Approach

For each element:

```text
Find Number Of
Subarrays Where
It Is Minimum
```

using:

```text
PSE + NSE
```

---

## Solution

```java
class Solution {

    public int sumSubarrayMins(
            int[] arr) {

        int n = arr.length;

        int[] pse = new int[n];
        int[] nse = new int[n];

        Stack<Integer> st =
                new Stack<>();

        for(int i = 0; i < n; i++){

            while(!st.isEmpty() &&
                  arr[st.peek()] > arr[i]){

                st.pop();
            }

            pse[i] =
                st.isEmpty()
                ? -1
                : st.peek();

            st.push(i);
        }

        st.clear();

        for(int i = n - 1; i >= 0; i--){

            while(!st.isEmpty() &&
                  arr[st.peek()] >= arr[i]){

                st.pop();
            }

            nse[i] =
                st.isEmpty()
                ? n
                : st.peek();

            st.push(i);
        }

        long ans = 0;
        long mod = 1000000007;

        for(int i = 0; i < n; i++){

            long left =
                i - pse[i];

            long right =
                nse[i] - i;

            ans +=
                (long)arr[i]
                * left
                * right;

            ans %= mod;
        }

        return (int)ans;
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

# Problem 2: LeetCode 2104 - Sum of Subarray Ranges

## Problem Statement

Find:

```text
(Maximum - Minimum)

for every subarray
```

---

## Approach

```text
Answer

=

Total Maximum Contribution

-

Total Minimum Contribution
```

---

## Formula

```text
Sum(Max Contribution)

-

Sum(Min Contribution)
```

---

## Required

For Maximum:

```text
PGE + NGE
```

For Minimum:

```text
PSE + NSE
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

# Problem 3: LeetCode 84 - Largest Rectangle in Histogram

## Core Observation

Each bar contributes as:

```text
Height
×
Width
```

---

## Width

Computed using:

```text
Previous Smaller

Next Smaller
```

---

## Area

```text
height

×

(nse - pse - 1)
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
907  - Sum Of Subarray Minimums

2104 - Sum Of Subarray Ranges

84   - Largest Rectangle In Histogram

85   - Maximal Rectangle

2281 - Sum Of Total Strength Of Wizards

1856 - Maximum Subarray Min Product
```

---

# Quick Revision Table

| Problem          | Required  |
| ---------------- | --------- |
| Subarray Minimum | PSE + NSE |
| Subarray Maximum | PGE + NGE |
| Subarray Range   | Max - Min |
| Histogram        | PSE + NSE |

---

# Master Formula

```text
For Every Element

Find Left Boundary

Find Right Boundary

Count Subarrays

left × right

Contribution

=

value × left × right

Add Contributions

Answer Ready
```
