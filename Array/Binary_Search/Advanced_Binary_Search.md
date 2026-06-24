# Advanced Binary Search

## Core Idea

Advanced Binary Search is about finding an optimal answer using a monotonic property.

```text
Answer Space
      ↓
Valid / Invalid
      ↓
Monotonic Pattern
      ↓
Binary Search
```

---

## MNC Interview Patterns

### Pattern 1

Minimize Maximum

```text
Split Array Largest Sum
Allocate Books
Painter's Partition
Ship Packages
```

---

### Pattern 2

Maximize Minimum

```text
Aggressive Cows
Magnetic Force Between Balls
Maximum Minimum Distance
```

---

### Pattern 3

Minimum Feasible Answer

```text
Koko Eating Bananas
Minimum Divisor
Minimum Days
Minimum Time
```

---

### Pattern 4

Partition Binary Search

```text
Median of Two Sorted Arrays
Kth Element of Two Sorted Arrays
```

---

### Pattern 5

Mathematical Binary Search

```text
Square Root
Nth Root
Perfect Square
```

---

## Golden Recognition Pattern

```text
Can Brute Force All Answers
            ↓
Need Better Complexity
            ↓
Can Check One Answer Efficiently
            ↓
True/False Pattern Exists
            ↓
Binary Search on Answers
```

---

## Generic Template (Minimum Answer)

```java
int low = minAnswer;
int high = maxAnswer;
int ans = high;

while(low <= high){

    int mid = low + (high - low) / 2;

    if(isPossible(mid)){
        ans = mid;
        high = mid - 1;
    }else{
        low = mid + 1;
    }
}

return ans;
```

---

## Generic Template (Maximum Answer)

```java
int low = minAnswer;
int high = maxAnswer;
int ans = low;

while(low <= high){

    int mid = low + (high - low) / 2;

    if(isPossible(mid)){
        ans = mid;
        low = mid + 1;
    }else{
        high = mid - 1;
    }
}

return ans;
```

---

## Important Insights

### Insight 1

Always find Answer Space.

```text
low  = minimum possible answer
high = maximum possible answer
```

---

### Insight 2

Write Check Function First.

```java
boolean isPossible(mid)
```

Most interview mistakes happen here.

---

### Insight 3

Monotonic Property Must Exist.

Example:

```text
1 → False
2 → False
3 → False
4 → True
5 → True
6 → True
```

Binary Search works.

---

### Insight 4

For Minimize Problems

```java
if(valid)
    high = mid - 1;
```

---

### Insight 5

For Maximize Problems

```java
if(valid)
    low = mid + 1;
```

---

# Problem 1: LeetCode 410 - Split Array Largest Sum

## Problem Statement

Split array into k subarrays.

Minimize largest subarray sum.

---

## Answer Space

```text
low  = max(nums)
high = sum(nums)
```

---

## Approach

Check whether array can be divided into at most k parts using maxSum = mid.

---

## Solution

```java
class Solution {

    public int splitArray(int[] nums, int k) {

        int low = 0;
        int high = 0;

        for(int num : nums){
            low = Math.max(low, num);
            high += num;
        }

        int ans = high;

        while(low <= high){

            int mid = low + (high - low) / 2;

            if(canSplit(nums, k, mid)){
                ans = mid;
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }

        return ans;
    }

    private boolean canSplit(int[] nums,
                             int k,
                             int maxSum){

        int parts = 1;
        int sum = 0;

        for(int num : nums){

            if(sum + num > maxSum){
                parts++;
                sum = num;
            }else{
                sum += num;
            }
        }

        return parts <= k;
    }
}
```

### TC

```text
O(n log(sum(nums)))
```

### SC

```text
O(1)
```

---

# Problem 2: LeetCode 1552 - Magnetic Force Between Two Balls

## Problem Statement

Place m balls.

Maximize minimum distance.

---

## Answer Space

```text
low  = 1

high =
max(position)
-
min(position)
```

---

## Approach

Greedily place balls.

Check if at least m balls can be placed with distance = mid.

---

## Solution

```java
class Solution {

    public int maxDistance(int[] position,
                           int m) {

        Arrays.sort(position);

        int low = 1;

        int high =
            position[position.length - 1]
            - position[0];

        int ans = 1;

        while(low <= high){

            int mid = low + (high - low) / 2;

            if(canPlace(position,m,mid)){
                ans = mid;
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }

        return ans;
    }

    private boolean canPlace(int[] pos,
                             int m,
                             int dist){

        int count = 1;
        int last = pos[0];

        for(int i=1;i<pos.length;i++){

            if(pos[i] - last >= dist){
                count++;
                last = pos[i];
            }
        }

        return count >= m;
    }
}
```

### TC

```text
O(n log(maxDistance))
```

### SC

```text
O(1)
```

---

# Top MNC Binary Search Problems

## Must Solve

```text
69    - Sqrt(x)
367   - Valid Perfect Square
875   - Koko Eating Bananas
1011  - Capacity To Ship Packages Within D Days
1283  - Find Smallest Divisor Given Threshold
1482  - Minimum Number of Days to Make m Bouquets
1552  - Magnetic Force Between Two Balls
1760  - Minimum Limit of Balls in a Bag
2187  - Minimum Time to Complete Trips
410   - Split Array Largest Sum
```

---

## Hard Level

```text
4     - Median of Two Sorted Arrays
483   - Smallest Good Base
644   - Maximum Average Subarray II
719   - Find K-th Smallest Pair Distance
786   - K-th Smallest Prime Fraction
```

---

## Binary Search Interview Checklist

```text
✓ Classic Binary Search

✓ Lower Bound

✓ Upper Bound

✓ Search Insert Position

✓ First / Last Occurrence

✓ Rotated Sorted Array

✓ Peak Element

✓ Binary Search on Answers

✓ Matrix Binary Search

✓ Infinite Array

✓ Median of Two Sorted Arrays

✓ Split Array Largest Sum

✓ Aggressive Cows Pattern

✓ Kth Element Problems
```

---

## Master Formula

```text
1. Identify Search Space

2. Identify Monotonic Property

3. Build Check Function

4. Apply Binary Search

5. Minimize
   -> high = mid - 1

6. Maximize
   -> low = mid + 1

7. Return Best Answer
```
