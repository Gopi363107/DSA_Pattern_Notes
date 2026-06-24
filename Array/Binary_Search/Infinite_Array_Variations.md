# Infinite Array Variations

## Core Idea

Array size is unknown (or treated as infinite).

First find a search range containing the target, then apply Binary Search.

---

## When to Use

* Infinite sorted array.
* Unknown array size.
* Stream of sorted data.
* Need first occurrence in infinite array.

---

## Trigger Words

* Infinite array
* Unknown size
* Sorted stream
* Search target
* First positive
* First occurrence

---

## General Pattern

```text
Start Small Range
       ↓
Expand Exponentially
       ↓
Target Falls Inside Range
       ↓
Apply Binary Search
```

---

## General Template

```java
public int search(int[] arr, int target) {

    int low = 0;
    int high = 1;

    while (arr[high] < target) {

        low = high + 1;
        high = high * 2;
    }

    return binarySearch(arr, low, high, target);
}
```

---

## Time Complexity

```text
Range Expansion : O(log position)
Binary Search   : O(log position)

Total           : O(log position)
```

## Space Complexity

```text
O(1)
```

---

## Important Insights

### Insight 1

Cannot directly apply Binary Search.

Need valid search boundaries first.

---

### Insight 2

Expand exponentially.

```java
high = high * 2;
```

Search space grows very fast.

---

### Insight 3

After expansion:

```text
Target ∈ [low, high]
```

Normal Binary Search becomes possible.

---

### Insight 4

Expansion takes:

```text
O(log position)
```

because range doubles every step.

---

## Recognition Pattern

```text
Sorted Array
      +
Unknown Size
      ↓
Expand Window
      ↓
Binary Search
```

---

# Problem 1: Search in Infinite Sorted Array

## Problem Statement

Find target in a sorted array whose size is unknown.

---

## Approach

### Step 1

Expand range until:

```java
arr[high] >= target
```

### Step 2

Apply Binary Search.

---

## Solution

```java
class Solution {

    public int search(int[] arr, int target) {

        int low = 0;
        int high = 1;

        while (arr[high] < target) {

            low = high + 1;
            high = high * 2;
        }

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (arr[mid] == target)
                return mid;

            if (arr[mid] < target)
                low = mid + 1;
            else
                high = mid - 1;
        }

        return -1;
    }
}
```

### TC

```text
O(log position)
```

### SC

```text
O(1)
```

---

# Problem 2: First Occurrence of 1 in Infinite Binary Array

## Problem Statement

Infinite sorted binary array:

```text
0 0 0 0 0 1 1 1 1 1 ...
```

Find first occurrence of 1.

---

## Approach

### Step 1

Expand range until:

```java
arr[high] == 1
```

### Step 2

Apply Lower Bound for 1.

---

## Solution

```java
class Solution {

    public int firstOne(int[] arr) {

        int low = 0;
        int high = 1;

        while (arr[high] == 0) {

            low = high + 1;
            high = high * 2;
        }

        int ans = -1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (arr[mid] == 1) {

                ans = mid;
                high = mid - 1;

            } else {

                low = mid + 1;
            }
        }

        return ans;
    }
}
```

### TC

```text
O(log firstOnePosition)
```

### SC

```text
O(1)
```

---

# Problem 3: LeetCode 278 - First Bad Version

## Problem Statement

Find first bad version.

All versions after a bad version are also bad.

---

## Approach

Monotonic Pattern:

```text
Good Good Good Good
 ↓
Bad Bad Bad Bad
```

Find first bad version using Lower Bound.

---

## Solution

```java
public class Solution extends VersionControl {

    public int firstBadVersion(int n) {

        int low = 1;
        int high = n;
        int ans = n;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (isBadVersion(mid)) {

                ans = mid;
                high = mid - 1;

            } else {

                low = mid + 1;
            }
        }

        return ans;
    }
}
```

### TC

```text
O(log n)
```

### SC

```text
O(1)
```

---

# Problem 4: LeetCode 374 - Guess Number Higher or Lower

## Problem Statement

Guess a hidden number.

API returns:

```text
-1 → Too High
 1 → Too Low
 0 → Correct
```

---

## Approach

Classic Binary Search on answer.

---

## Solution

```java
public class Solution extends GuessGame {

    public int guessNumber(int n) {

        int low = 1;
        int high = n;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            int res = guess(mid);

            if (res == 0)
                return mid;

            if (res == 1)
                low = mid + 1;
            else
                high = mid - 1;
        }

        return -1;
    }
}
```

### TC

```text
O(log n)
```

### SC

```text
O(1)
```

---

## Common Infinite Array Problems

```text
Search in Infinite Sorted Array
First Occurrence of 1 in Infinite Binary Array
278 - First Bad Version
374 - Guess Number Higher or Lower
```

---

## Master Formula

```text
1. Start with Small Window

   low = 0
   high = 1

2. Expand Window

   high *= 2

3. Stop When Target Is Inside Range

4. Apply Binary Search

5. Return Answer
```

---

## Visual Understanding

```text
Target = 80

[1, 2]
     ↓

[1, 4]
     ↓

[1, 8]
     ↓

[1, 16]
     ↓

[1, 32]
     ↓

[1, 64]
     ↓

[1, 128]

Target Found In Range
       ↓
Binary Search
```
