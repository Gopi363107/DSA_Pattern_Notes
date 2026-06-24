# Rotated Sorted Array

## Core Idea

A rotated sorted array consists of **two sorted halves**.

Use Binary Search to identify the sorted half and decide where the target can exist.

---

## When to Use

* Rotated sorted array.
* Need to search an element.
* Need minimum element.
* Need rotation count.
* O(log n) expected.

---

## Trigger Words

* Rotated sorted array
* Pivot
* Rotation
* Search target
* Minimum element
* Rotation count

---

## General Pattern

```text
Sorted + Rotated
        ↓
One Half Always Sorted
        ↓
Identify Sorted Half
        ↓
Decide Search Direction
```

---

## General Template (Search Target)

```java
public int search(int[] nums, int target) {

    int low = 0;
    int high = nums.length - 1;

    while (low <= high) {

        int mid = low + (high - low) / 2;

        if (nums[mid] == target)
            return mid;

        if (nums[low] <= nums[mid]) {

            if (nums[low] <= target && target < nums[mid])
                high = mid - 1;
            else
                low = mid + 1;

        } else {

            if (nums[mid] < target && target <= nums[high])
                low = mid + 1;
            else
                high = mid - 1;
        }
    }

    return -1;
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

At least one half is always sorted.

```text
Left Sorted
or
Right Sorted
```

---

### Insight 2

Check if left half is sorted.

```java
nums[low] <= nums[mid]
```

---

### Insight 3

Check if right half is sorted.

```java
nums[mid] <= nums[high]
```

---

### Insight 4

If target lies inside sorted half:

```text
Search Sorted Half
```

Otherwise:

```text
Search Unsorted Half
```

---

## Recognition Pattern

```text
Rotated Sorted Array
         ↓
Need Search / Minimum
         ↓
One Half Sorted
         ↓
Think Rotated Binary Search
```

---

# Problem 1: LeetCode 33 - Search in Rotated Sorted Array

## Problem Statement

Search target in a rotated sorted array.

Return index if found otherwise return -1.

---

## Approach

1. Find sorted half.
2. Check whether target belongs to that half.
3. Move accordingly.
4. Continue Binary Search.

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

            if (nums[low] <= nums[mid]) {

                if (nums[low] <= target && target < nums[mid])
                    high = mid - 1;
                else
                    low = mid + 1;

            } else {

                if (nums[mid] < target && target <= nums[high])
                    low = mid + 1;
                else
                    high = mid - 1;
            }
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

# Problem 2: LeetCode 153 - Find Minimum in Rotated Sorted Array

## Problem Statement

Find the minimum element in a rotated sorted array.

---

## Approach

1. Track minimum answer.
2. Check which half is sorted.
3. Minimum can exist in unsorted half.
4. Eliminate sorted half whenever possible.

---

## Solution

```java
class Solution {

    public int findMin(int[] nums) {

        int low = 0;
        int high = nums.length - 1;
        int ans = Integer.MAX_VALUE;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[low] <= nums[high]) {
                ans = Math.min(ans, nums[low]);
                break;
            }

            if (nums[low] <= nums[mid]) {

                ans = Math.min(ans, nums[low]);
                low = mid + 1;

            } else {

                ans = Math.min(ans, nums[mid]);
                high = mid - 1;
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

# Problem 3: LeetCode 81 - Search in Rotated Sorted Array II

## Problem Statement

Search target in rotated sorted array containing duplicates.

---

## Approach

1. Handle duplicate ambiguity.
2. Shrink both ends.
3. Apply normal rotated binary search.

---

## Solution

```java
class Solution {

    public boolean search(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] == target)
                return true;

            if (nums[low] == nums[mid] &&
                nums[mid] == nums[high]) {

                low++;
                high--;
                continue;
            }

            if (nums[low] <= nums[mid]) {

                if (nums[low] <= target &&
                    target < nums[mid]) {

                    high = mid - 1;
                } else {
                    low = mid + 1;
                }

            } else {

                if (nums[mid] < target &&
                    target <= nums[high]) {

                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }

        return false;
    }
}
```

### TC

```text
O(log n) Average
O(n) Worst Case
```

### SC

```text
O(1)
```

---

## Common LeetCode Problems

```text
33  - Search in Rotated Sorted Array
81  - Search in Rotated Sorted Array II
153 - Find Minimum in Rotated Sorted Array
154 - Find Minimum in Rotated Sorted Array II
```

---

## Master Formula

```text
1. Find Sorted Half
2. Check Target Range
3. Eliminate One Half
4. Continue Binary Search
5. Return Answer
```
