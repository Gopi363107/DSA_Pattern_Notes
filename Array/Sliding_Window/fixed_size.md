# Fixed Size Sliding Window — Pattern Recognition Notes

---

# Definition

Fixed Size Sliding Window is an optimization technique used when:

```text
A subarray/substring size remains CONSTANT
```

We maintain a window of size `k` and slide it across the array/string efficiently.

Instead of recalculating everything again:

```text
Remove left contribution
Add right contribution
```

This reduces complexity dramatically.

---

# Core Intuition

A fixed-size window means:

```text
Window length NEVER changes
```

At every step:

```text
1. Add new element
2. Remove old element
3. Move window forward
```

This creates:

```text
O(n)
```

solutions instead of:

```text
O(n * k)
```

---

# Most Important Observation

Whenever the problem asks:

```text
"Find something in every subarray of size k"
```

→ Think:

```text
Fixed Size Sliding Window
```

This is the MAIN recognition trigger.

---

# When Should I Think About Fixed Sliding Window?

Use this pattern when:

- Window size is fixed
- Subarray size is exactly `k`
- Need max/min/sum/average of size `k`
- Need all substrings of size `k`
- Need rolling computation
- Need contiguous block processing

---

# Pattern Recognition Triggers

If the problem statement contains words like:

- "subarray of size k"
- "substring of length k"
- "every window of size k"
- "fixed length"
- "contiguous block"
- "maximum sum of size k"
- "average of size k"
- "window length k"
- "exactly k elements"

→ Think **Fixed Sliding Window**

---

# Mental Model

Ask this question:

> “Is the window size ALWAYS constant?”

If YES:

```text
Use Fixed Sliding Window
```

---

# Generic Fixed Sliding Window Template

```java
int left = 0;

for(int right = 0; right < n; right++) {

    // add current element

    if(window size > k) {

        // remove left contribution

        left++;
    }

    if(window size == k) {

        // process answer
    }
}
```

---

# Window Size Formula

```java
window size = right - left + 1
```

---

# Core Sliding Operation

When moving window:

```text
Old Window:
[1 2 3]

New Window:
[2 3 4]
```

Instead of recomputing:

```text
Remove 1
Add 4
```

This is the MAIN optimization insight.

---

# Pattern 1 — Maximum Average Subarray I

---

## Trigger

- maximum average
- subarray size k
- fixed window sum

---

## Problem

LeetCode 643 — Maximum Average Subarray I

---

## Recognition

Need:

```text
Maximum sum among all subarrays of size k
```

Window size never changes.

Classic fixed sliding window.

---

## Brute Force

For every index:

```text
Calculate k-length sum manually
```

---

## Brute Force Complexity

### Time Complexity

```text
O(n * k)
```

because for every position:

```text
We iterate k elements
```

---

### Space Complexity

```text
O(1)
```

---

## Optimized Insight

When sliding:

```text
newSum = oldSum
         - outgoing element
         + incoming element
```

No recomputation needed.

---

## Solution

```java
class Solution {

    public double findMaxAverage(
        int[] nums,
        int k
    ) {

        int sum = 0;

        for(int i = 0; i < k; i++) {

            sum += nums[i];
        }

        int maxSum = sum;

        for(int i = k; i < nums.length; i++) {

            sum += nums[i];

            sum -= nums[i - k];

            maxSum = Math.max(maxSum, sum);
        }

        return (double) maxSum / k;
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

Each element:

- added once
- removed once

No nested traversal.

---

## Space Complexity

```text
O(1)
```

Only variables used.

---

# Pattern 2 — Number of Sub-arrays of Size K and Average ≥ Threshold

---

## Trigger

- fixed length k
- average condition
- count windows

---

## Problem

LeetCode 1343 — Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold

---

## Recognition

Need:

```text
Count valid windows of exact size k
```

Classic fixed-size validation pattern.

---

## Insight

Instead of average:

```text
sum / k >= threshold
```

Convert to:

```text
sum >= threshold * k
```

Avoid floating point operations.

Very important optimization trick.

---

## Solution

```java
class Solution {

    public int numOfSubarrays(
        int[] arr,
        int k,
        int threshold
    ) {

        int target = threshold * k;

        int sum = 0;

        int count = 0;

        for(int i = 0; i < k; i++) {

            sum += arr[i];
        }

        if(sum >= target) {
            count++;
        }

        for(int i = k; i < arr.length; i++) {

            sum += arr[i];

            sum -= arr[i - k];

            if(sum >= target) {
                count++;
            }
        }

        return count;
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

Single traversal after initial window.

---

## Space Complexity

```text
O(1)
```

---

# Pattern 3 — Sliding Window Maximum

---

## Trigger

- maximum in every window
- fixed window maximum
- moving max

---

## Problem

LeetCode 239 — Sliding Window Maximum

---

## Recognition

Need:

```text
Maximum element in every window of size k
```

Naively finding max every time becomes expensive.

Need efficient structure.

Classic deque optimization pattern.

---

# Important Insight

Deque stores:

```text
Useful candidate indices
```

Maintain:

```text
Decreasing order
```

Front always stores:

```text
Maximum element index
```

---

## Solution

```java
class Solution {

    public int[] maxSlidingWindow(
        int[] nums,
        int k
    ) {

        Deque<Integer> dq =
            new LinkedList<>();

        int[] ans =
            new int[nums.length - k + 1];

        int index = 0;

        for(int right = 0;
            right < nums.length;
            right++) {

            while(!dq.isEmpty() &&
                  dq.peekFirst() <= right - k) {

                dq.pollFirst();
            }

            while(!dq.isEmpty() &&
                  nums[dq.peekLast()]
                  < nums[right]) {

                dq.pollLast();
            }

            dq.offerLast(right);

            if(right >= k - 1) {

                ans[index++] =
                    nums[dq.peekFirst()];
            }
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

Why?

Each element:

- inserted once
- removed once

Deque operations are amortized O(1).

---

## Space Complexity

```text
O(k)
```

Deque stores at most `k` indices.

---

# Super Important Recognition Patterns

---

# 1. Exact K Size Pattern

If question says:

```text
exactly k
size k
length k
```

→ Think:

```text
Fixed Sliding Window
```

---

# 2. Rolling Computation Pattern

If consecutive windows overlap:

```text
Reuse previous computation
```

instead of recomputing.

---

# 3. Contiguous Block Pattern

Sliding window ONLY works for:

```text
Contiguous subarrays/substrings
```

Very important.

---

# 4. Running Sum Pattern

Many fixed-window problems reduce to:

```text
Running sum maintenance
```

---

# Important Interview Insight

Most fixed sliding window problems are secretly:

```text
Incremental update problems
```

Instead of recomputing entire windows:

```text
Update only changed elements
```

This is the key optimization mindset.

---

# Quick Comparison

| Situation | Pattern |
|---|---|
| Exact size k | Fixed Window |
| Variable length | Dynamic Window |
| Non-contiguous | Prefix Sum / DP |
| Maximum/minimum window | Deque |

---

# Common Mistake

Students often recompute:

```text
Entire window again
```

which leads to:

```text
O(n * k)
```

instead of:

```text
O(n)
```

Always reuse previous window computation.

---

# One-Line Memory Trick

```text
Fixed Window = Remove left, add right
```

---

# Final Interview Insight

Most fixed-size sliding window problems become easy after recognizing:

```text
The window size NEVER changes
```

That single observation determines:

```text
Two pointers
Rolling computation
O(n) optimization
```

This is one of the highest-frequency array interview patterns asked at Meta, Google, Amazon, Uber, and top product companies.