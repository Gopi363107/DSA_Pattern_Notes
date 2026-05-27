# Two Pointers Pattern — Converging Pointers Notes

---

# Definition

The **Converging Pointers** pattern uses:

```text
Two pointers moving toward each other
```

Usually:

```text
left → from start
right → from end
```

Used mainly on:

- sorted arrays
- palindrome problems
- pair problems
- optimization problems

---

# Core Intuition

Instead of checking:

```text
All pairs
```

we intelligently eliminate impossible cases.

Main idea:

```text
Use problem properties
(sorted order / symmetry)
```

to reduce search space.

---

# When Should I Think About Converging Pointers?

Use this pattern when:

- Array is sorted
- Need pair/triplet answers
- Need opposite-end processing
- Need palindrome checking
- Need minimizing/maximizing pair values

---

# Recognition Triggers

If problem contains:

- "sorted array"
- "pair sum"
- "two numbers"
- "palindrome"
- "container"
- "closest pair"
- "remove duplicates"
- "two ends"

→ Think:

```text
Converging Two Pointers
```

---

# Generic Template

```java
int left = 0;
int right = n - 1;

while(left < right) {

    if(condition satisfied) {

    }
    else if(need bigger value) {
        left++;
    }
    else {
        right--;
    }
}
```

---

# MOST IMPORTANT INSIGHT

At every step:

```text
One entire set of possibilities
gets eliminated
```

This is WHY complexity becomes:

```text
O(n)
```

instead of:

```text
O(n²)
```

---

# Pattern 1 — Two Sum II

---

## Trigger

- sorted array
- pair sum
- exactly one answer

---

## Problem

LeetCode 167 — Two Sum II

---

# Key Insight

If:

```text
sum too small
```

Need larger value:

```text
left++
```

If:

```text
sum too large
```

Need smaller value:

```text
right--
```

Sorted property enables elimination.

---

## Solution

```java
class Solution {

    public int[] twoSum(
        int[] numbers,
        int target
    ) {

        int left = 0;
        int right = numbers.length - 1;

        while(left < right) {

            int sum =
                numbers[left] + numbers[right];

            if(sum == target) {

                return new int[]{
                    left + 1,
                    right + 1
                };
            }

            if(sum < target) {
                left++;
            }
            else {
                right--;
            }
        }

        return new int[]{};
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

Without sorting insight:

```text
Brute force → O(n²)
```

Converging pointers eliminate one side every move.

---

# Pattern 2 — Valid Palindrome

---

## Trigger

- palindrome
- symmetry
- compare both ends

---

## Problem

LeetCode 125 — Valid Palindrome

---

# Key Insight

Palindrome means:

```text
Characters from both ends
must match
```

Move inward simultaneously.

---

## Solution

```java
class Solution {

    public boolean isPalindrome(String s) {

        int left = 0;
        int right = s.length() - 1;

        while(left < right) {

            while(left < right &&
                  !Character.isLetterOrDigit(
                      s.charAt(left))) {

                left++;
            }

            while(left < right &&
                  !Character.isLetterOrDigit(
                      s.charAt(right))) {

                right--;
            }

            if(Character.toLowerCase(
                    s.charAt(left))
               !=
               Character.toLowerCase(
                    s.charAt(right))) {

                return false;
            }

            left++;
            right--;
        }

        return true;
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

Symmetry problems often reduce to:

```text
Compare mirrored indices
```

Very common interview trick.

---

# Pattern 3 — Container With Most Water

---

## Trigger

- maximize area
- opposite ends
- choose better boundary

---

## Problem

LeetCode 11 — Container With Most Water

---

# Key Insight

Area depends on:

```text
min(height[left], height[right])
```

Smaller height limits area.

So:

```text
Move smaller pointer
```

because bigger one is already optimal.

---

## Solution

```java
class Solution {

    public int maxArea(int[] height) {

        int left = 0;
        int right = height.length - 1;

        int ans = 0;

        while(left < right) {

            int width = right - left;

            int area =
                Math.min(height[left],
                         height[right])
                * width;

            ans = Math.max(ans, area);

            if(height[left] < height[right]) {
                left++;
            }
            else {
                right--;
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
O(n)
```

## Space Complexity

```text
O(1)
```

---

# MOST IMPORTANT CP INSIGHT

Why move smaller pointer?

Because:

```text
Area limited by smaller height
```

Moving taller height cannot improve:

```text
min(height)
```

GENIUS greedy elimination.

---

# Super Important Recognition Patterns

| Situation | Pattern |
|---|---|
| Sorted pair search | Two pointers |
| Palindrome/symmetry | Converging pointers |
| Opposite-end optimization | Two pointers |
| Pair/triplet sums | Two pointers |
| Eliminate impossible ranges | Converging pointers |

---

# Advanced Competitive Programming Insights

---

# 1. Elimination Principle

Every movement removes:

```text
One invalid region
```

This creates:

```text
Linear complexity
```

---

# 2. Sorted Arrays Enable Decisions

Because array sorted:

```text
Pointer movement becomes meaningful
```

Without sorting:

```text
No directional information
```

---

# 3. Greedy + Two Pointers

Many hard problems combine:

```text
Greedy decisions
+
Pointer shrinking
```

Container problem is classic example.

---

# Common Mistake

Students often do:

```text
Nested loops
```

for pair checking.

But sorted structure allows:

```text
Single-pass elimination
```

---

# One-Line Memory Trick

```text
If one pointer movement can eliminate
many possibilities,
think two pointers.
```

---

# Final Interview Insight

The REAL power of converging pointers is:

```text
Search-space elimination
```

Instead of exploring all pairs:

```text
Mathematically discard impossible regions
```

That transforms many:

```text
O(n²)
```

problems into:

```text
O(n)
```