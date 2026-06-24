# Classic Binary Search

## Core Idea

Search in a **sorted array** by repeatedly eliminating half of the search space.

---

## When to Use

* Array is sorted.
* Need to find existence of an element.
* Need exact position/index of an element.

---

## Trigger Words

* Sorted array
* Search target
* Find index
* Element exists or not
* O(log n) expected

---

## General Template (Java)

```java
public int binarySearch(int[] nums, int target) {
    int low = 0;
    int high = nums.length - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (nums[mid] == target)
            return mid;
        else if (nums[mid] < target)
            low = mid + 1;
        else
            high = mid - 1;
    }

    return -1;
}
```

---

## Time Complexity

```text
Best    : O(1)
Average : O(log n)
Worst   : O(log n)
```

## Space Complexity

```text
O(1)
```

---

## Important Insights

### Insight 1

Always calculate mid as:

```java
int mid = low + (high - low) / 2;
```

Avoid:

```java
int mid = (low + high) / 2;
```

to prevent integer overflow.

### Insight 2

```java
while(low <= high)
```

Use `<=` because the search space contains a single element at the end.

### Insight 3

```java
nums[mid] < target
```

Target can only exist on the right side.

```java
low = mid + 1;
```

### Insight 4

```java
nums[mid] > target
```

Target can only exist on the left side.

```java
high = mid - 1;
```

---

# Problem 1: LeetCode 704 - Binary Search

## Problem Statement

Given a sorted array of integers `nums` and an integer `target`, return the index of target if it exists. Otherwise return `-1`.

---

## Approach

1. Maintain search space `[low, high]`.
2. Compute middle element.
3. Compare with target.
4. Eliminate one half.
5. Continue until found or search space becomes empty.

---

## Solution

```java
class Solution {
    public int search(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] == target)
                return mid;

            if (nums[mid] < target)
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

# Problem 2: LeetCode 35 - Search Insert Position

## Problem Statement

Given a sorted array and a target value, return its index if found.

If not found, return the index where it should be inserted.

---

## Approach

1. Apply normal binary search.
2. If target found, return index.
3. If target not found:

   * `low` will point to the correct insertion position.
4. Return `low`.

---

## Solution

```java
class Solution {
    public int searchInsert(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] == target)
                return mid;

            if (nums[mid] < target)
                low = mid + 1;
            else
                high = mid - 1;
        }

        return low;
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

## Recognition Pattern

```text
Sorted Array
       ↓
Find/Search Target
       ↓
Need Better Than O(n)
       ↓
Think Binary Search
```
