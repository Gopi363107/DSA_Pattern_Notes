# Peak / Mountain / Bitonic Array

## Core Idea

Use Binary Search on the **slope direction**.

```text
Increasing
    ↑
  Peak
    ↓
Decreasing
```

Peak element is always located where:

```java
nums[mid] > nums[mid + 1]
```

or

```java
nums[mid] > nums[mid - 1]
```

---

## When to Use

* Peak Element.
* Mountain Array.
* Bitonic Array.
* Maximum Element.
* Search in Mountain Array.

---

## Trigger Words

* Peak element
* Mountain array
* Bitonic array
* Local maximum
* Maximum element
* Increasing then decreasing

---

## General Pattern

```text
Increasing Slope
        ↓
     Peak
        ↓
Decreasing Slope
```

---

## General Template (Find Peak)

```java
public int findPeak(int[] nums) {

    int low = 0;
    int high = nums.length - 1;

    while (low < high) {

        int mid = low + (high - low) / 2;

        if (nums[mid] > nums[mid + 1])
            high = mid;
        else
            low = mid + 1;
    }

    return low;
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
nums[mid] > nums[mid + 1]
```

You are on the decreasing slope.

Peak lies:

```text
Left Side (including mid)
```

```java
high = mid;
```

---

### Insight 2

```java
nums[mid] < nums[mid + 1]
```

You are on the increasing slope.

Peak lies:

```text
Right Side
```

```java
low = mid + 1;
```

---

### Insight 3

Use

```java
while(low < high)
```

instead of

```java
while(low <= high)
```

to avoid out-of-bound access for:

```java
nums[mid + 1]
```

---

### Insight 4

At termination:

```java
low == high
```

This index is the peak.

---

## Recognition Pattern

```text
Increasing Then Decreasing
           ↓
Need Peak / Maximum
           ↓
Slope Comparison
           ↓
Think Peak Binary Search
```

---

# Problem 1: LeetCode 162 - Find Peak Element

## Problem Statement

Find any peak element.

A peak element is greater than its neighbors.

---

## Approach

1. Compare mid and mid+1.
2. Decide slope direction.
3. Move toward peak.
4. Return final index.

---

## Solution

```java
class Solution {

    public int findPeakElement(int[] nums) {

        int low = 0;
        int high = nums.length - 1;

        while (low < high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] > nums[mid + 1])
                high = mid;
            else
                low = mid + 1;
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

# Problem 2: LeetCode 852 - Peak Index in a Mountain Array

## Problem Statement

Return the peak index of a mountain array.

---

## Approach

Exactly same as Peak Element.

Mountain array guarantees:

```text
Increasing → Peak → Decreasing
```

---

## Solution

```java
class Solution {

    public int peakIndexInMountainArray(int[] arr) {

        int low = 0;
        int high = arr.length - 1;

        while (low < high) {

            int mid = low + (high - low) / 2;

            if (arr[mid] > arr[mid + 1])
                high = mid;
            else
                low = mid + 1;
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

# Problem 3: LeetCode 1095 - Find in Mountain Array

## Problem Statement

Search target in a mountain array.

---

## Approach

### Step 1

Find Peak.

### Step 2

Binary Search on increasing half.

### Step 3

Binary Search on decreasing half.

---

## Solution Pattern

```java
peak = findPeak()

search left ascending part

if found return index

search right descending part
```

---

### TC

```text
O(log n)
```

### SC

```text
O(1)
```

---

## Bitonic Array Search Template

```java
int peak = findPeak(arr);

int left = binarySearchAscending(arr, 0, peak, target);

if(left != -1)
    return left;

return binarySearchDescending(
    arr,
    peak + 1,
    arr.length - 1,
    target
);
```

---

## Common LeetCode Problems

```text
162  - Find Peak Element
852  - Peak Index in Mountain Array
1095 - Find in Mountain Array
```

---

## Master Formula

```text
1. Compare nums[mid] and nums[mid+1]
2. Determine Slope
3. Move Toward Peak
4. Find Peak Index
5. (Optional) Apply Binary Search on Both Sides
```

---

## Visual Understanding

```text
1  3  7  12  15  11  6  2
            ↑
          Peak

Left Side  -> Increasing
Right Side -> Decreasing
```
