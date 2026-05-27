# Two Pointers Pattern — Triggered Pointers Notes

---

# Definition

The **Triggered Pointers** pattern uses:

```text
One pointer moving normally
```

while another pointer moves only when:

```text
A specific condition is triggered
```

Unlike normal parallel pointers:

```text
Pointers do NOT always move together
```

Movement depends on events/conditions.

---

# Core Intuition

We process data continuously using:

```text
Main pointer
```

and activate another pointer only when:

```text
Constraint violated
OR
special condition occurs
```

Very common in:

- partition problems
- window adjustments
- duplicate skipping
- rearrangement problems

---

# MOST IMPORTANT IDEA

One pointer acts like:

```text
Explorer
```

Another acts like:

```text
Fixer/Adjuster
```

The second pointer activates only when needed.

---

# When Should I Think About Triggered Pointers?

Use this pattern when:

- Need conditional shrinking
- Need partitioning
- Need duplicate skipping
- Need correction after violation
- Need event-driven pointer movement

---

# Recognition Triggers

If problem contains:

- "when invalid"
- "skip duplicates"
- "partition"
- "move when condition occurs"
- "adjust window"
- "rearrange"
- "Dutch National Flag"
- "remove extra duplicates"

→ Think:

```text
Triggered Pointer Movement
```

---

# Generic Template

```java
int left = 0;

for(int right = 0;
    right < n;
    right++) {

    // process right

    while(condition invalid) {

        // adjust left

        left++;
    }
}
```

OR

```java
while(pointer < n) {

    if(trigger happens) {

        // activate another pointer
    }
}
```

---

# MOST IMPORTANT INSIGHT

Pointers move:

```text
ONLY when necessary
```

This avoids:

```text
Unnecessary operations
```

and gives:

```text
O(n)
```

solutions.

---

# Pattern 1 — Remove Duplicates II

---

## Trigger

- sorted array
- allow duplicates at most twice
- conditional overwrite

---

## Problem

LeetCode 80 — Remove Duplicates from Sorted Array II

---

# Key Insight

Keep element only if:

```text
Current value
!=
value before previous kept element
```

Write pointer moves only when:

```text
Valid element found
```

---

## Solution

```java
class Solution {

    public int removeDuplicates(
        int[] nums
    ) {

        if(nums.length <= 2) {
            return nums.length;
        }

        int slow = 2;

        for(int fast = 2;
            fast < nums.length;
            fast++) {

            if(nums[fast]
               !=
               nums[slow - 2]) {

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

Instead of counting frequencies fully:

```text
Use positional observation
```

Very elegant optimization trick.

---

# Pattern 2 — Sort Colors

---

## Trigger

- partitioning
- rearrangement
- Dutch National Flag

---

## Problem

LeetCode 75 — Sort Colors

---

# Key Insight

Maintain:

```text
0-region
1-region
2-region
```

Pointers move only when:

```text
Specific color encountered
```

Triggered swapping pattern.

---

## Solution

```java
class Solution {

    public void sortColors(int[] nums) {

        int low = 0;
        int mid = 0;
        int high = nums.length - 1;

        while(mid <= high) {

            if(nums[mid] == 0) {

                int temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;

                low++;
                mid++;
            }

            else if(nums[mid] == 1) {

                mid++;
            }

            else {

                int temp = nums[mid];
                nums[mid] = nums[high];
                nums[high] = temp;

                high--;
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

# MOST IMPORTANT CP INSIGHT

Notice:

```text
mid does NOT always move
```

after swapping with `high`.

Why?

Because swapped value still unprocessed.

This is THE KEY observation.

---

# Pattern 3 — 3Sum

---

## Trigger

- sorted array
- skip duplicates
- pair searching

---

## Problem

LeetCode 15 — 3Sum

---

# Key Insight

After finding valid triplet:

```text
Skip duplicate values
```

Pointers move conditionally only when:

```text
Duplicate encountered
```

Triggered duplicate elimination.

---

## Solution

```java
class Solution {

    public List<List<Integer>> threeSum(
        int[] nums
    ) {

        Arrays.sort(nums);

        List<List<Integer>> ans =
            new ArrayList<>();

        for(int i = 0;
            i < nums.length - 2;
            i++) {

            if(i > 0 &&
               nums[i] == nums[i - 1]) {

                continue;
            }

            int left = i + 1;
            int right = nums.length - 1;

            while(left < right) {

                int sum =
                    nums[i]
                    + nums[left]
                    + nums[right];

                if(sum == 0) {

                    ans.add(Arrays.asList(
                        nums[i],
                        nums[left],
                        nums[right]
                    ));

                    while(left < right &&
                          nums[left]
                          == nums[left + 1]) {

                        left++;
                    }

                    while(left < right &&
                          nums[right]
                          == nums[right - 1]) {

                        right--;
                    }

                    left++;
                    right--;
                }

                else if(sum < 0) {

                    left++;
                }

                else {

                    right--;
                }
            }
        }

        return ans;
    }
}
```

---

# Complexity

## Time Complexity

```text
O(n²)
```

## Space Complexity

```text
O(1)
```

Ignoring output list.

---

# Super Important Recognition Patterns

| Situation | Pattern |
|---|---|
| Conditional shrinking | Triggered pointers |
| Skip duplicates | Triggered movement |
| Partitioning | Triggered swaps |
| Event-based pointer updates | Triggered pointers |
| Rearrangement problems | Conditional pointers |

---

# Advanced Competitive Programming Insights

---

# 1. Event-Driven Pointer Movement

Pointers move only after:

```text
Specific events
```

Examples:

- invalid window
- duplicate found
- partition mismatch
- swap needed

---

# 2. Conditional Reprocessing

Sometimes pointer DOES NOT move.

Example:

```text
Sort Colors
```

because swapped value still unknown.

This is very important.

---

# 3. Duplicate Elimination Optimization

Instead of:

```text
HashSet duplicate checking
```

sorted arrays allow:

```text
Pointer skipping
```

More memory efficient.

---

# 4. Partition Boundary Thinking

Many triggered-pointer problems maintain:

```text
Regions/boundaries
```

Example:

```text
[0-region][1-region][unknown][2-region]
```

Very important DSA visualization skill.

---

# Common Mistake

Students often:

```text
Move pointers unconditionally
```

causing:

- skipped elements
- duplicate answers
- incorrect partitions

Instead:

```text
Move pointers ONLY when logic allows
```

---

# One-Line Memory Trick

```text
One pointer explores,
another reacts only when triggered.
```

---

# Final Interview Insight

Triggered pointers are powerful because:

```text
Pointer movement becomes intelligent
```

instead of fixed.

This enables elegant:

- partitioning
- duplicate handling
- conditional shrinking
- event-driven optimization

in:

```text
O(n)
```

or:

```text
O(n²)
```

instead of brute force.