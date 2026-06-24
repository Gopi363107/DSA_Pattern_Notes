# Upper Bound

## Core Idea

Find the **first index where value > target**.

---

## When to Use

* Sorted array.
* Need next greater element.
* Need count of elements <= target.
* Need range queries.
* Need insertion position after duplicates.

---

## Trigger Words

* Upper bound
* First greater element
* Strictly greater
* Next larger element
* First position > target

---

## General Template (Java)

```java
public int upperBound(int[] nums, int target) {

    int low = 0;
    int high = nums.length - 1;
    int ans = nums.length;

    while (low <= high) {

        int mid = low + (high - low) / 2;

        if (nums[mid] > target) {
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
nums[mid] > target
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
nums[mid] <= target
```

Cannot be answer.

Move right.

```java
low = mid + 1;
```

---

### Insight 3

Upper Bound returns:

```text
First index having value > target
```

---

### Insight 4

Count of elements less than or equal to target:

```java
upperBound(nums, target)
```

---

# Problem 1: LeetCode 34 - Find First and Last Position of Element in Sorted Array

## Problem Statement

Find the first and last occurrence of a target value.

---

## Approach

1. First Position = Lower Bound(target)
2. Last Position = Upper Bound(target) - 1
3. Verify target exists.

---

## Solution

```java
class Solution {

    public int[] searchRange(int[] nums, int target) {

        int first = lowerBound(nums, target);

        if (first == nums.length || nums[first] != target)
            return new int[]{-1, -1};

        int last = upperBound(nums, target) - 1;

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

    private int upperBound(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;
        int ans = nums.length;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] > target) {
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

# Problem 2: LeetCode 2089 - Find Target Indices After Sorting Array

## Problem Statement

Return all indices where target appears after sorting the array.

---

## Approach

1. Sort the array.
2. First occurrence = Lower Bound(target).
3. Last occurrence = Upper Bound(target) - 1.
4. Add all indices in that range.

---

## Solution

```java
class Solution {

    public List<Integer> targetIndices(int[] nums, int target) {

        Arrays.sort(nums);

        int left = lowerBound(nums, target);
        int right = upperBound(nums, target);

        List<Integer> ans = new ArrayList<>();

        for (int i = left; i < right; i++) {
            ans.add(i);
        }

        return ans;
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

    private int upperBound(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;
        int ans = nums.length;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] > target) {
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
O(n log n)
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
Need First Element > Target
       ↓
Need Next Greater Position
       ↓
Think Upper Bound
```
