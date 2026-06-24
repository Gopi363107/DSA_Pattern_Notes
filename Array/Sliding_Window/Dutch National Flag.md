# Dutch National Flag

## Core Idea

Partition an array into three regions using three pointers.

```text
0s | 1s | Unknown | 2s
```

Process the unknown region and place elements in their correct section.

---

## When to Use

* Array contains 3 categories.
* Sort 0s, 1s, 2s.
* Three-way partitioning.
* Partition around pivot.
* In-place sorting required.

---

## Trigger Words

* Sort Colors
* 0,1,2 array
* Three-way partition
* Three categories
* Pivot partitioning
* In-place sorting

---

## General Pattern

```text
0 Region | 1 Region | Unknown | 2 Region

low          mid               high
```

---

## Three Pointers

```java
int low = 0;
int mid = 0;
int high = nums.length - 1;
```

---

## Rules

### Case 1

```java
nums[mid] == 0
```

Swap:

```java
swap(low, mid);
```

Move:

```java
low++;
mid++;
```

---

### Case 2

```java
nums[mid] == 1
```

Already in correct region.

```java
mid++;
```

---

### Case 3

```java
nums[mid] == 2
```

Swap:

```java
swap(mid, high);
```

Move:

```java
high--;
```

Do NOT move mid.

---

## General Template (Java)

```java
public void sortColors(int[] nums) {

    int low = 0;
    int mid = 0;
    int high = nums.length - 1;

    while(mid <= high){

        if(nums[mid] == 0){

            swap(nums, low, mid);

            low++;
            mid++;

        }
        else if(nums[mid] == 1){

            mid++;

        }
        else{

            swap(nums, mid, high);

            high--;
        }
    }
}

private void swap(
        int[] nums,
        int i,
        int j){

    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```

---

## Time Complexity

```text
O(N)
```

## Space Complexity

```text
O(1)
```

---

## Important Insights

### Insight 1

Array is divided into four parts.

```text
0 ... low-1       -> 0s

low ... mid-1     -> 1s

mid ... high      -> Unknown

high+1 ... n-1    -> 2s
```

---

### Insight 2

When:

```java
nums[mid] == 2
```

Do not increment mid.

Reason:

```text
New element comes from right side.

Needs processing.
```

---

### Insight 3

Single pass sorting.

```text
No Counting

No Extra Array

No Sorting Algorithm
```

---

## Visual Understanding

### Initial

```text
2 0 2 1 1 0

L
M
          H
```

---

### After Processing

```text
0 0 1 1 2 2
```

---

## Recognition Pattern

```text
Three Distinct Categories
            ↓
Need In-Place Sorting
            ↓
Single Pass Preferred
            ↓
Dutch National Flag
```

---

# Problem 1: LeetCode 75 - Sort Colors

## Problem Statement

Sort an array containing:

```text
0 1 2
```

without using built-in sort.

---

## Approach

Use:

```text
low
mid
high
```

Maintain three regions.

---

## Solution

```java
class Solution {

    public void sortColors(int[] nums) {

        int low = 0;
        int mid = 0;
        int high = nums.length - 1;

        while(mid <= high){

            if(nums[mid] == 0){

                swap(nums, low, mid);

                low++;
                mid++;
            }
            else if(nums[mid] == 1){

                mid++;
            }
            else{

                swap(nums, mid, high);

                high--;
            }
        }
    }

    private void swap(
            int[] nums,
            int i,
            int j){

        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

### TC

```text
O(N)
```

### SC

```text
O(1)
```

---

# Problem 2: Three-Way Partition Around Pivot

## Problem Statement

Partition array into:

```text
< pivot

= pivot

> pivot
```

---

## Approach

Use Dutch National Flag logic.

Replace:

```text
0 -> < pivot

1 -> = pivot

2 -> > pivot
```

---

## Solution

```java
public void partition(
        int[] nums,
        int pivot){

    int low = 0;
    int mid = 0;
    int high = nums.length - 1;

    while(mid <= high){

        if(nums[mid] < pivot){

            swap(nums, low, mid);

            low++;
            mid++;
        }
        else if(nums[mid] == pivot){

            mid++;
        }
        else{

            swap(nums, mid, high);

            high--;
        }
    }
}
```

### TC

```text
O(N)
```

### SC

```text
O(1)
```

---

## Common Interview Problems

```text
75   - Sort Colors

2161 - Partition Array According to Given Pivot

Three Way Partition

QuickSort Partition Variant
```

---

## Dutch National Flag vs Counting Sort

| Technique           | TC   | SC   |
| ------------------- | ---- | ---- |
| Counting Sort       | O(N) | O(1) |
| Dutch National Flag | O(N) | O(1) |

---

## Master Formula

```text
low = start

mid = start

high = end

------------------

0

swap(low, mid)

low++
mid++

------------------

1

mid++

------------------

2

swap(mid, high)

high--

------------------

while(mid <= high)
```
