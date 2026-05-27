# Variable Size Sliding Window — Pattern Recognition Notes

---

# Definition

Variable Size Sliding Window is used when:

```text
Window size changes dynamically
```

based on a condition.

Unlike fixed-size windows:

```text
Expand window when valid
Shrink window when invalid
```

This is one of the MOST important patterns in:

- Interviews
- Competitive Programming
- Online Assessments

---

# Core Intuition

We maintain a window:

```text
[left ... right]
```

and dynamically adjust it.

At every step:

```text
1. Expand right pointer
2. Maintain condition
3. Shrink left if needed
4. Update answer
```

---

# Most Important Observation

Variable sliding window problems ALWAYS involve:

```text
A condition becoming valid/invalid
```

Examples:

- sum > k
- unique characters
- at most k distinct
- frequency constraints
- product < k
- replacement limit

This is the MAIN recognition trigger.

---

# When Should I Think About Variable Sliding Window?

Use this pattern when:

- Window size is NOT fixed
- Need longest/shortest valid subarray
- Need at most/exactly constraints
- Need frequency maintenance
- Need distinct element control
- Need continuous optimization

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "longest"
- "smallest"
- "minimum length"
- "maximum length"
- "at most"
- "at least"
- "without repeating"
- "distinct characters"
- "continuous subarray"
- "valid window"
- "maintain condition"

→ Think **Variable Sliding Window**

---

# Mental Model

Ask this question:

> “Does the window size change based on a condition?”

If YES:

```text
Use Variable Sliding Window
```

---

# Most Important Insight

Variable window problems usually follow:

```text
Expand → Violate → Shrink → Become Valid
```

This is the ENTIRE pattern.

---

# Generic Variable Sliding Window Template

```java
int left = 0;

for(int right = 0; right < n; right++) {

    // include nums[right]

    while(window becomes invalid) {

        // remove nums[left]

        left++;
    }

    // update answer
}
```

---

# Core Competitive Programming Insight

Most CP sliding window problems are actually:

```text
Constraint maintenance problems
```

You are NOT solving subarrays directly.

You are maintaining:

```text
A VALID STATE
```

This mindset is extremely important.

---

# Fixed vs Variable Window

| Feature | Fixed Window | Variable Window |
|---|---|
| Window size | Constant | Dynamic |
| Main operation | Slide | Expand/Shrink |
| Recognition | Exact k | Constraint-based |
| Typical question | Every window of size k | Longest/shortest valid window |

---

# Pattern 1 — Longest Substring Without Repeating Characters

---

## Trigger

- unique characters
- without repeating
- longest substring

---

## Problem

LeetCode 3 — Longest Substring Without Repeating Characters

---

## Recognition

Need:

```text
Longest valid window
```

where:

```text
All characters are unique
```

Window becomes invalid when duplicate appears.

Classic variable sliding window.

---

# Brute Force

Generate all substrings.

Check uniqueness manually.

---

# Brute Force Complexity

## Time Complexity

```text
O(n^3)
```

Why?

- O(n²) substrings
- O(n) uniqueness check

---

## Space Complexity

```text
O(n)
```

---

# Optimized Insight

When duplicate appears:

```text
Shrink window until valid again
```

No need to restart.

This is the BIGGEST sliding window optimization.

---

## Solution

```java
class Solution {

    public int lengthOfLongestSubstring(
        String s
    ) {

        HashSet<Character> set =
            new HashSet<>();

        int left = 0;

        int maxLen = 0;

        for(int right = 0;
            right < s.length();
            right++) {

            while(set.contains(
                    s.charAt(right))) {

                set.remove(s.charAt(left));

                left++;
            }

            set.add(s.charAt(right));

            maxLen =
                Math.max(maxLen,
                         right - left + 1);
        }

        return maxLen;
    }
}
```

---

# Complexity Analysis

---

## Time Complexity

```text
O(n)
```

Why?

Each character:

- enters window once
- leaves window once

Two-pointer amortized analysis.

---

## Space Complexity

```text
O(k)
```

where:

```text
k = unique characters
```

---

# CP-Level Insight

The key realization:

```text
Left pointer NEVER moves backward
```

This guarantees:

```text
Total operations ≤ 2n
```

Very important competitive programming insight.

---

# Pattern 2 — Minimum Size Subarray Sum

---

## Trigger

- smallest subarray
- minimum length
- sum ≥ target

---

## Problem

LeetCode 209 — Minimum Size Subarray Sum

---

## Recognition

Need:

```text
Smallest valid window
```

Window becomes valid when:

```text
sum >= target
```

Then shrink aggressively.

Classic shrinking-window optimization.

---

## Solution

```java
class Solution {

    public int minSubArrayLen(
        int target,
        int[] nums
    ) {

        int left = 0;

        int sum = 0;

        int minLen = Integer.MAX_VALUE;

        for(int right = 0;
            right < nums.length;
            right++) {

            sum += nums[right];

            while(sum >= target) {

                minLen =
                    Math.min(minLen,
                             right - left + 1);

                sum -= nums[left];

                left++;
            }
        }

        return minLen == Integer.MAX_VALUE
               ? 0
               : minLen;
    }
}
```

---

# Complexity Analysis

---

## Time Complexity

```text
O(n)
```

Each element:

- added once
- removed once

---

## Space Complexity

```text
O(1)
```

---

# CP-Level Insight

For:

```text
minimum window problems
```

the strategy is usually:

```text
Expand until valid
Shrink while valid
```

This is a HIGH-FREQUENCY contest pattern.

---

# Pattern 3 — Longest Repeating Character Replacement

---

## Trigger

- replace characters
- at most k changes
- longest valid substring

---

## Problem

LeetCode 424 — Longest Repeating Character Replacement

---

## Recognition

Need longest window where:

```text
window size - max frequency <= k
```

This is one of the MOST important sliding window formulas.

---

# Key Insight

Minimum replacements needed:

```text
window length
-
most frequent character count
```

because:

```text
Convert all others into majority character
```

GENIUS interview insight.

---

## Solution

```java
class Solution {

    public int characterReplacement(
        String s,
        int k
    ) {

        int[] freq = new int[26];

        int left = 0;

        int maxFreq = 0;

        int ans = 0;

        for(int right = 0;
            right < s.length();
            right++) {

            freq[s.charAt(right) - 'A']++;

            maxFreq =
                Math.max(
                    maxFreq,
                    freq[s.charAt(right) - 'A']
                );

            while((right - left + 1)
                    - maxFreq > k) {

                freq[s.charAt(left) - 'A']--;

                left++;
            }

            ans =
                Math.max(ans,
                         right - left + 1);
        }

        return ans;
    }
}
```

---

# Complexity Analysis

---

## Time Complexity

```text
O(n)
```

Even though while-loop exists:

```text
Each pointer moves at most n times
```

---

## Space Complexity

```text
O(1)
```

Fixed alphabet size.

---

# CP-Level Insight

VERY IMPORTANT:

We do NOT recompute maxFreq when shrinking.

Why?

Because slightly stale maxFreq still preserves correctness.

This is an ADVANCED sliding window optimization used heavily in CP.

---

# Super Important Recognition Patterns

---

# 1. Longest Valid Window Pattern

If question asks:

```text
longest valid substring/subarray
```

→ Usually:

```text
Expand while valid
Shrink when invalid
```

---

# 2. Smallest Valid Window Pattern

If question asks:

```text
minimum length
smallest window
```

→ Usually:

```text
Expand until valid
Shrink aggressively
```

---

# 3. At Most K Pattern

If question says:

```text
at most k distinct
at most k replacements
at most k operations
```

→ Think:

```text
Frequency map + shrinking window
```

---

# 4. Frequency Constraint Pattern

If validity depends on:

```text
counts/frequencies
```

→ Use:

```text
HashMap / Frequency Array
```

---

# Advanced Competitive Programming Insights

---

# 1. Amortized Analysis

Even with nested while-loop:

```text
O(n)
```

because:

```text
Each pointer moves only forward
```

This is CRITICAL.

---

# 2. Window Validity Framework

Most CP sliding window problems reduce to:

```text
Maintain a valid window state
```

NOT:

```text
Enumerate subarrays
```

This mindset changes everything.

---

# 3. Monotonic Window Property

Sliding window works BEST when:

```text
Validity changes monotonically
```

Example:

```text
If window invalid,
larger window also invalid
```

This allows shrinking logic.

---

# 4. Exactly K Trick

Very advanced CP trick:

```text
Exactly K
=
At Most K
-
At Most (K - 1)
```

Used in MANY hard problems.

Extremely important.

---

# Important Interview Insight

Most sliding window hard problems are actually:

```text
Constraint-maintenance problems
```

The challenge is identifying:

```text
What makes the window valid?
```

Once identified:

```text
Expand/Shrink becomes natural
```

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Exact size k | Fixed Window |
| Dynamic validity | Variable Window |
| Prefix accumulation | Prefix Sum |
| Ordered nearest search | Binary Search |

---

# Common Mistake

Students often restart the window completely after invalidation.

Wrong approach.

Correct idea:

```text
Shrink minimally until valid again
```

This preserves:

```text
O(n)
```

complexity.

---

# One-Line Memory Trick

```text
Expand → Violate → Shrink → Valid
```

---

# Final Interview Insight

Most variable sliding window problems become easy after identifying:

```text
What condition defines a VALID window?
```

That single observation determines:

```text
Data structure
Shrinking logic
Optimization strategy
```

This is one of the MOST IMPORTANT interview and competitive programming patterns asked at Meta, Google, Amazon, Uber, Codeforces, ICPC, and top product companies.