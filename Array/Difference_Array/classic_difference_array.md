# Basic Difference Array

## Core Idea

Difference Array is used to perform multiple range updates efficiently.

Instead of updating every element in a range:

```text
[l, r] += val
```

Update only boundaries.

```text
diff[l]     += val
diff[r + 1] -= val
```

Then reconstruct the final array using Prefix Sum.

---

## When to Use

* Multiple range updates.
* Large number of queries.
* Offline updates.
* Need O(1) range update.

---

## Trigger Words

* Range increment
* Range update
* Add value to subarray
* Multiple updates
* Batch updates
* Difference array

---

## General Pattern

```text
Range Update
      ↓
Mark Boundaries
      ↓
Difference Array
      ↓
Prefix Sum
      ↓
Final Array
```

---

## Basic Example

### Initial Array

```text
0 0 0 0 0
```

Query:

```text
[1,3] += 5
```

Difference Array:

```text
0 5 0 0 -5
```

Prefix Sum:

```text
0 5 5 5 0
```

Final Array Obtained.

---

## General Template (Java)

```java
public int[] rangeUpdate(int n,
                         int[][] queries) {

    int[] diff = new int[n];

    for(int[] q : queries){

        int left = q[0];
        int right = q[1];
        int val = q[2];

        diff[left] += val;

        if(right + 1 < n)
            diff[right + 1] -= val;
    }

    for(int i = 1; i < n; i++){
        diff[i] += diff[i - 1];
    }

    return diff;
}
```

---

## Time Complexity

```text
Range Update : O(1)

Q Queries    : O(Q)

Build Array  : O(N)

Total        : O(N + Q)
```

## Space Complexity

```text
O(N)
```

---

## Important Insights

### Insight 1

Normal Update

```text
Update [l,r]

O(r-l+1)
```

Difference Array

```text
O(1)
```

---

### Insight 2

Start of range:

```java
diff[l] += val;
```

---

### Insight 3

End of range:

```java
diff[r+1] -= val;
```

Stops propagation after r.

---

### Insight 4

Final array is obtained using:

```java
Prefix Sum
```

---

## Recognition Pattern

```text
Many Range Updates
          ↓
Direct Update Too Slow
          ↓
Need O(1) Update
          ↓
Think Difference Array
```

---

# Problem 1: LeetCode 370 - Range Addition

## Problem Statement

Perform multiple range increment operations.

Return final array.

---

## Approach

1. Create Difference Array.
2. Mark update boundaries.
3. Apply Prefix Sum.
4. Return final array.

---

## Solution

```java
class Solution {

    public int[] getModifiedArray(
            int length,
            int[][] updates) {

        int[] diff = new int[length];

        for(int[] update : updates){

            int start = update[0];
            int end = update[1];
            int inc = update[2];

            diff[start] += inc;

            if(end + 1 < length)
                diff[end + 1] -= inc;
        }

        for(int i = 1; i < length; i++){
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

# Problem 2: LeetCode 2381 - Shifting Letters II

## Problem Statement

Apply multiple range shifts on characters.

---

## Approach

1. Difference Array for shifts.
2. Prefix Sum to compute net shift.
3. Apply shifts to characters.

---

## Solution

```java
class Solution {

    public String shiftingLetters(
            String s,
            int[][] shifts) {

        int n = s.length();

        int[] diff = new int[n + 1];

        for(int[] shift : shifts){

            int l = shift[0];
            int r = shift[1];

            int val =
                shift[2] == 1 ? 1 : -1;

            diff[l] += val;
            diff[r + 1] -= val;
        }

        StringBuilder ans =
                new StringBuilder();

        int currentShift = 0;

        for(int i = 0; i < n; i++){

            currentShift += diff[i];

            int ch =
                s.charAt(i) - 'a';

            ch =
                ((ch + currentShift)
                % 26 + 26) % 26;

            ans.append((char)(ch + 'a'));
        }

        return ans.toString();
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

# Common Difference Array Problems

```text
370   - Range Addition
1094  - Car Pooling
1109  - Corporate Flight Bookings
2381  - Shifting Letters II
2772  - Apply Operations to Make Array Equal to Zero
```

---

## Difference Array vs Prefix Sum

| Technique        | Use Case          |
| ---------------- | ----------------- |
| Prefix Sum       | Fast Range Query  |
| Difference Array | Fast Range Update |

---

## Master Formula

```text
Range Update [l,r] += val

diff[l] += val

diff[r+1] -= val

------------------

After All Queries

Apply Prefix Sum

------------------

Result = Final Array
```

---

## Visual Understanding

```text
Array

0 0 0 0 0 0

Update

[1,4] += 3

Difference Array

0 3 0 0 0 -3

Prefix Sum

0 3 3 3 3 0

Final Array
```
