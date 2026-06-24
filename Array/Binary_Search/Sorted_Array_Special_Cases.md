# Sorted Array Special Cases

## Core Idea

Some Binary Search problems on sorted arrays don't directly ask to find a target.

Instead, they ask for:

```text id="l4k7v0"
Floor
Ceil
Closest Element
Frequency
First Occurrence
Last Occurrence
Count of Occurrences
```

These are special applications of Binary Search.

---

## When to Use

* Sorted array.
* Need nearest value.
* Need frequency.
* Need occurrence count.
* Need predecessor/successor.

---

## Trigger Words

* Floor
* Ceil
* Closest element
* Count occurrences
* Frequency
* First occurrence
* Last occurrence
* Nearest value

---

## Pattern Overview

```text id="zwxhhw"
Sorted Array
      ↓
Target Related Query
      ↓
Lower Bound / Upper Bound
      ↓
Derive Answer
```

---

# Floor in Sorted Array

## Core Idea

Find the largest element:

```text id="r0ekjy"
<= target
```

---

## Template

```java id="5e7txz"
public int floor(int[] nums, int target) {

    int low = 0;
    int high = nums.length - 1;

    int ans = -1;

    while (low <= high) {

        int mid = low + (high - low) / 2;

        if (nums[mid] <= target) {

            ans = nums[mid];
            low = mid + 1;

        } else {

            high = mid - 1;
        }
    }

    return ans;
}
```

---

## Important Insight

```java id="rjopag"
nums[mid] <= target
```

Can be answer.

Try finding a larger valid value.

---

# Ceil in Sorted Array

## Core Idea

Find the smallest element:

```text id="1uq43y"
>= target
```

---

## Template

```java id="1qqm2u"
public int ceil(int[] nums, int target) {

    int low = 0;
    int high = nums.length - 1;

    int ans = -1;

    while (low <= high) {

        int mid = low + (high - low) / 2;

        if (nums[mid] >= target) {

            ans = nums[mid];
            high = mid - 1;

        } else {

            low = mid + 1;
        }
    }

    return ans;
}
```

---

## Important Insight

```java id="pqzyzi"
nums[mid] >= target
```

Can be answer.

Try finding smaller valid value.

---

# First Occurrence

## Core Idea

Find leftmost occurrence.

---

## Template

```java id="rj20n0"
if(nums[mid] == target) {
    ans = mid;
    high = mid - 1;
}
```

---

# Last Occurrence

## Core Idea

Find rightmost occurrence.

---

## Template

```java id="mxb1wb"
if(nums[mid] == target) {
    ans = mid;
    low = mid + 1;
}
```

---

# Count Occurrences

## Formula

```java id="0e4gbj"
count =
lastOccurrence -
firstOccurrence + 1;
```

---

## Recognition Pattern

```text id="3lf53d"
Need Frequency
      ↓
Find First Occurrence
      ↓
Find Last Occurrence
      ↓
Compute Count
```

---

# Problem 1: LeetCode 34 - Find First and Last Position of Element in Sorted Array

## Problem Statement

Find starting and ending position of target.

---

## Approach

1. Find First Occurrence.
2. Find Last Occurrence.
3. Return both indices.

---

## Solution

```java id="ztfjlwm"
class Solution {

    public int[] searchRange(int[] nums, int target) {

        int first = firstOccurrence(nums, target);
        int last = lastOccurrence(nums, target);

        return new int[]{first, last};
    }

    private int firstOccurrence(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;
        int ans = -1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {

                ans = mid;
                high = mid - 1;

            } else if (nums[mid] < target) {

                low = mid + 1;

            } else {

                high = mid - 1;
            }
        }

        return ans;
    }

    private int lastOccurrence(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;
        int ans = -1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {

                ans = mid;
                low = mid + 1;

            } else if (nums[mid] < target) {

                low = mid + 1;

            } else {

                high = mid - 1;
            }
        }

        return ans;
    }
}
```

### TC

```text id="h7qpmh"
O(log n)
```

### SC

```text id="tb68bk"
O(1)
```

---

# Problem 2: LeetCode 35 - Search Insert Position

## Problem Statement

Return insertion position of target.

---

## Approach

Use Lower Bound.

---

## Solution

```java id="87dhfd"
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

```text id="2d6khu"
O(log n)
```

### SC

```text id="9iww0v"
O(1)
```

---

# Problem 3: LeetCode 744 - Find Smallest Letter Greater Than Target

## Problem Statement

Find the smallest character strictly greater than target.

---

## Approach

Use Upper Bound.

Find:

```text id="v8gyd2"
First Character > Target
```

---

## Solution

```java id="4jy6hl"
class Solution {

    public char nextGreatestLetter(char[] letters,
                                   char target) {

        int low = 0;
        int high = letters.length - 1;

        char ans = letters[0];

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (letters[mid] > target) {

                ans = letters[mid];
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

```text id="8nflpx"
O(log n)
```

### SC

```text id="wz0n9y"
O(1)
```

---

## Common Special Cases

```text id="0m1b1k"
Floor in Sorted Array
Ceil in Sorted Array
First Occurrence
Last Occurrence
Count Occurrences
Search Insert Position
Next Greater Element
Next Smaller Element
Closest Element
```

---

## Master Formula

```text id="cl9odt"
Need First Valid Answer
         ↓
Use Lower Bound

-------------------

Need Next Greater
         ↓
Use Upper Bound

-------------------

Need Frequency
         ↓
First Occurrence +
Last Occurrence

-------------------

Need Floor / Ceil
         ↓
Track Best Candidate
```
