# Two Pointers Pattern — Parallel Pointers Notes

---

# Definition

The **Parallel Pointers** pattern uses:

```text
Two pointers moving
in the SAME direction
```

Usually:

```text
slow → processes valid portion
fast → explores array/string
```

or:

```text
pointer1
pointer2
```

moving together.

---

# Core Intuition

Instead of restarting loops:

```text
Reuse previous work
```

Both pointers move forward:

```text
Never backward
```

This creates:

```text
Linear complexity
```

---

# When Should I Think About Parallel Pointers?

Use this pattern when:

- Need in-place modification
- Need duplicate removal
- Need merging
- Need partitioning
- Need comparing sequences
- Need fast/slow processing

---

# Recognition Triggers

If problem contains:

- "remove duplicates"
- "in-place"
- "sorted array"
- "move zeros"
- "merge arrays"
- "compress"
- "partition"
- "stable rearrangement"

→ Think:

```text
Parallel Two Pointers
```

---

# Generic Template

```java
int slow = 0;

for(int fast = 0;
    fast < n;
    fast++) {

    if(valid condition) {

        // place/update

        slow++;
    }
}
```

---

# MOST IMPORTANT INSIGHT

Usually:

```text
fast → reads data
slow → writes answer
```

This avoids:

```text
Extra arrays
```

Very important optimization.

---

# Pattern 1 — Remove Duplicates from Sorted Array

---

## Trigger

- sorted array
- remove duplicates
- in-place

---

## Problem

LeetCode 26 — Remove Duplicates from Sorted Array

---

# Key Insight

Since array sorted:

```text
Duplicates stay together
```

Keep only:

```text
First occurrence
```

---

## Solution

```java
class Solution {

    public int removeDuplicates(
        int[] nums
    ) {

        int slow = 1;

        for(int fast = 1;
            fast < nums.length;
            fast++) {

            if(nums[fast]
               !=
               nums[fast - 1]) {

                nums[slow] =
                    nums[fast];

                slow++;
            }
        }

        return slow;
    }
}
```

---

# Complexity

## Time Complexity

```text
O(n)
```

## Space Complexity

```text
O(1)
```

---

# CP-Level Insight

Important observation:

```text
Sorted property groups duplicates
```

Without sorting:

```text
Problem becomes harder
```

---

# Pattern 2 — Move Zeroes

---

## Trigger

- move elements
- stable order
- in-place shifting

---

## Problem

LeetCode 283 — Move Zeroes

---

# Key Insight

Keep:

```text
All non-zero values
```

at front.

`slow` tracks:

```text
Next insertion position
```

---

## Solution

```java
class Solution {

    public void moveZeroes(int[] nums) {

        int slow = 0;

        for(int fast = 0;
            fast < nums.length;
            fast++) {

            if(nums[fast] != 0) {

                int temp = nums[slow];
                nums[slow] = nums[fast];
                nums[fast] = temp;

                slow++;
            }
        }
    }
}
```

---

# Complexity

## Time Complexity

```text
O(n)
```

## Space Complexity

```text
O(1)
```

---

# CP-Level Insight

This is actually:

```text
Stable partitioning
```

Very common hidden pattern.

---

# Pattern 3 — Merge Sorted Array

---

## Trigger

- merge arrays
- sorted inputs
- compare sequences

---

## Problem

LeetCode 88 — Merge Sorted Array

---

# Key Insight

Compare:

```text
Largest remaining values
```

and place from back.

Avoids overwriting values.

---

## Solution

```java
class Solution {

    public void merge(
        int[] nums1,
        int m,
        int[] nums2,
        int n
    ) {

        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;

        while(i >= 0 && j >= 0) {

            if(nums1[i] > nums2[j]) {

                nums1[k] = nums1[i];
                i--;
            }
            else {

                nums1[k] = nums2[j];
                j--;
            }

            k--;
        }

        while(j >= 0) {

            nums1[k] = nums2[j];

            j--;
            k--;
        }
    }
}
```

---

# Complexity

## Time Complexity

```text
O(m + n)
```

## Space Complexity

```text
O(1)
```

---

# MOST IMPORTANT CP INSIGHT

Filling from back prevents:

```text
Overwriting useful values
```

Very important interview observation.

---

# Super Important Recognition Patterns

| Situation | Pattern |
|---|---|
| In-place modification | Parallel pointers |
| Stable rearrangement | Slow/Fast pointers |
| Duplicate removal | Parallel pointers |
| Array compression | Slow/Fast |
| Merge sorted sequences | Parallel pointers |

---

# Advanced Competitive Programming Insights

---

# 1. Read Pointer vs Write Pointer

Most parallel-pointer problems use:

```text
Fast pointer → reads
Slow pointer → writes
```

This is the MOST IMPORTANT mental model.

---

# 2. Stable Processing

Relative order remains same.

Example:

```text
Move Zeroes
```

preserves non-zero order.

Very important hidden property.

---

# 3. In-Place Optimization

Instead of:

```text
Using extra arrays
```

reuse original array carefully.

Space reduces:

```text
O(n) → O(1)
```

---

# 4. Monotonic Pointer Movement

Pointers only move:

```text
Forward
```

So total operations remain:

```text
O(n)
```

Amortized analysis insight.

---

# Common Mistake

Students often:

```text
Shift elements repeatedly
```

causing:

```text
O(n²)
```

Instead:

```text
Write directly using slow pointer
```

---

# One-Line Memory Trick

```text
One pointer explores,
another pointer builds answer.
```

---

# Final Interview Insight

The REAL power of parallel pointers is:

```text
Efficient in-place processing
```

without:

```text
Extra memory
```

This pattern appears constantly in:

- arrays
- strings
- linked lists
- sorting
- partitioning
- compression problems