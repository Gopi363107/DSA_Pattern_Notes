# Lower Bound

## Core Idea

Find the **first index where value >= target**.

---

## When to Use

* Sorted array.
* Need first occurrence.
* Need insertion position.
* Need count/range based problems.

---

## Trigger Words

* First occurrence
* First position
* Lower bound
* Insert position
* Smallest index satisfying condition
* First element >= target

---

## General Template (Java)

```java
public int lowerBound(int[] nums, int target) {

    int low = 0;
    int high = nums.length - 1;
    int ans = nums.length;

    while (low <= high) {

        int mid = low + (high - low) / 2;

        if (nums[mid] >= target) {
            ans = mid;
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }

    return ans;
}
```

---

## Time Complexity

```text
O(log n)
```

## Space Complexity

```text
O(1)
```

---

## Important Insights

### Insight 1

```java
nums[mid] >= target
```

Current index can be an answer.

Store it and continue searching left.

```java
ans = mid;
high = mid - 1;
```

---

### Insight 2

```java
nums[mid] < target
```

Cannot be answer.

Move right.

```java
low = mid + 1;
```

---

### Insight 3

Lower Bound returns:

```text
First index having value >= target
```

---

### Insight 4

If no valid answer exists:

```java
return nums.length;
```

---

# Problem 1: LeetCode 35 - Search Insert Position

## Problem Statement

Given a sorted array and a target value, return its index if found.

If not found, return the index where it should be inserted.

---

## Approach

1. Find first index where value >= target.
2. That position is the insertion position.
3. Return the answer.

---

## Solution

```java
class Solution {

    public int searchInsert(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;
        int ans = nums.length;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] >= target) {
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

# Problem 2: LeetCode 34 - Find First and Last Position of Element in Sorted Array

## Problem Statement

Find the first and last occurrence of a target value.

---

## Approach

1. First Position = Lower Bound(target)
2. Verify target exists.
3. Last Position = Lower Bound(target + 1) - 1

---

## Solution

```java
class Solution {

    public int[] searchRange(int[] nums, int target) {

        int first = lowerBound(nums, target);

        if (first == nums.length || nums[first] != target)
            return new int[]{-1, -1};

        int last = lowerBound(nums, target + 1) - 1;

        return new int[]{first, last};
    }

    private int lowerBound(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;
        int ans = nums.length;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] >= target) {
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

## Recognition Pattern

```text
Sorted Array
       ↓
Need First Position
       ↓
Need First Element >= Target
       ↓
Think Lower Bound
```
