# Two Sorted Arrays

## Core Idea

Apply Binary Search on one sorted array and derive information from the other sorted array.

Most commonly used for:

```text id="hfwvr5"
Median of Two Sorted Arrays
Kth Element of Two Sorted Arrays
```

---

## When to Use

* Two sorted arrays.
* Need median.
* Need kth smallest element.
* Need partitioning.
* O(log(min(n,m))) expected.

---

## Trigger Words

* Two sorted arrays
* Median
* Kth smallest
* Partition
* Merge not allowed
* Better than O(n+m)

---

## General Pattern

```text id="8v6d8j"
Array 1 Partition
        ↓
Array 2 Partition
        ↓
Left Part Valid ?
        ↓
Move Left / Right
```

---

## Important Insight

Instead of merging arrays:

```text id="2o7vbd"
Binary Search
on Smaller Array
```

---

## Partition Concept

```text id="5jv9n5"
Array1

1 3 | 8 9

Array2

7 11 18 | 19 21

------------------

Left Side

1 3 7 11 18

Right Side

8 9 19 21
```

Valid Partition:

```text id="6glc6y"
max(left) <= min(right)
```

---

## General Template

```java id="czt9js"
while(low <= high) {

    int cut1 = (low + high) / 2;
    int cut2 = requiredLeftSize - cut1;

    if(validPartition)
        return answer;

    else if(left1 > right2)
        high = cut1 - 1;

    else
        low = cut1 + 1;
}
```

---

## Time Complexity

```text id="4c6zhn"
O(log(min(n,m)))
```

## Space Complexity

```text id="o86gw9"
O(1)
```

---

## Recognition Pattern

```text id="w8ax5r"
Two Sorted Arrays
        ↓
Need Median / Kth
        ↓
Cannot Merge
        ↓
Think Partition Binary Search
```

---

# Problem 1: LeetCode 4 - Median of Two Sorted Arrays

## Problem Statement

Find median of two sorted arrays.

Required complexity:

```text id="c4g7gz"
O(log(min(n,m)))
```

---

## Approach

### Step 1

Binary Search on smaller array.

### Step 2

Create partition in both arrays.

### Step 3

Check:

```text id="9h08xq"
left1 <= right2
and
left2 <= right1
```

### Step 4

Compute median.

---

## Solution

```java id="5d5iwq"
class Solution {

    public double findMedianSortedArrays(
            int[] nums1,
            int[] nums2) {

        if (nums1.length > nums2.length)
            return findMedianSortedArrays(
                    nums2, nums1);

        int n1 = nums1.length;
        int n2 = nums2.length;

        int low = 0;
        int high = n1;

        while (low <= high) {

            int cut1 = (low + high) / 2;
            int cut2 = (n1 + n2 + 1) / 2 - cut1;

            int left1 =
                    cut1 == 0
                    ? Integer.MIN_VALUE
                    : nums1[cut1 - 1];

            int left2 =
                    cut2 == 0
                    ? Integer.MIN_VALUE
                    : nums2[cut2 - 1];

            int right1 =
                    cut1 == n1
                    ? Integer.MAX_VALUE
                    : nums1[cut1];

            int right2 =
                    cut2 == n2
                    ? Integer.MAX_VALUE
                    : nums2[cut2];

            if (left1 <= right2 &&
                left2 <= right1) {

                if ((n1 + n2) % 2 == 0) {

                    return (
                        Math.max(left1, left2)
                        +
                        Math.min(right1, right2)
                    ) / 2.0;
                }

                return Math.max(left1, left2);

            } else if (left1 > right2) {

                high = cut1 - 1;

            } else {

                low = cut1 + 1;
            }
        }

        return 0;
    }
}
```

### TC

```text id="ddjewk"
O(log(min(n,m)))
```

### SC

```text id="kqngsl"
O(1)
```

---

# Problem 2: Kth Element of Two Sorted Arrays

## Problem Statement

Find kth smallest element from two sorted arrays.

---

## Approach

### Left Partition Size

```java id="pf4v1r"
k
```

### Partition Rule

```text id="mns1oi"
Elements on Left = k
```

### Valid Partition

```text id="3u9gvk"
left1 <= right2
and
left2 <= right1
```

Answer:

```java id="oqj6an"
max(left1, left2)
```

---

## Solution

```java id="o0v7xh"
public int kthElement(
        int[] arr1,
        int[] arr2,
        int k) {

    if (arr1.length > arr2.length)
        return kthElement(arr2, arr1, k);

    int n1 = arr1.length;
    int n2 = arr2.length;

    int low = Math.max(0, k - n2);
    int high = Math.min(k, n1);

    while (low <= high) {

        int cut1 = (low + high) / 2;
        int cut2 = k - cut1;

        int left1 =
            cut1 == 0
            ? Integer.MIN_VALUE
            : arr1[cut1 - 1];

        int left2 =
            cut2 == 0
            ? Integer.MIN_VALUE
            : arr2[cut2 - 1];

        int right1 =
            cut1 == n1
            ? Integer.MAX_VALUE
            : arr1[cut1];

        int right2 =
            cut2 == n2
            ? Integer.MAX_VALUE
            : arr2[cut2];

        if (left1 <= right2 &&
            left2 <= right1) {

            return Math.max(left1, left2);

        } else if (left1 > right2) {

            high = cut1 - 1;

        } else {

            low = cut1 + 1;
        }
    }

    return -1;
}
```

### TC

```text id="4lf2mz"
O(log(min(n,m)))
```

### SC

```text id="msu0db"
O(1)
```

---

## Key Partition Formula

```text id="m2t4hn"
Median

cut1 + cut2
=
(n1 + n2 + 1) / 2
```

---

```text id="j7o6u4"
Kth Element

cut1 + cut2
=
k
```

---

## Common Problems

```text id="v85ikg"
4    - Median of Two Sorted Arrays
Kth Element of Two Sorted Arrays
```

---

## Master Formula

```text id="ncl2nh"
1. Binary Search Smaller Array

2. Create Partitions

3. Check

   left1 <= right2
   left2 <= right1

4. Valid Partition Found

5. Return Answer
```

---

## Visual Understanding

```text id="y91jtm"
nums1

1 3 | 8 9

nums2

7 11 18 | 19 21

------------------

max(left)
=
18

min(right)
=
19

Median
=
(18 + 19) / 2
```
