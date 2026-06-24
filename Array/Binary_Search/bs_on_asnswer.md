# Binary Search on Answers

## Core Idea

Instead of searching in an array, search on the **answer space**.

Binary Search is used when:

```text
Answer is numeric
        +
Brute Force checks every answer
        +
A Valid / Invalid pattern exists
```

---

## When to Use

* Need minimum possible answer.
* Need maximum possible answer.
* Need optimal value.
* Large search space.
* Monotonic True/False pattern exists.

---

## Trigger Words

* Minimum possible
* Maximum possible
* Minimize
* Maximize
* Capacity
* Speed
* K days
* K workers
* K operations
* Smallest value satisfying condition
* Largest value satisfying condition

---

## General Pattern

```text
Answer Space
     ↓
Check Mid Answer
     ↓
Valid ?
     ↓
Search Left or Right
```

---

## General Template (Java)

```java
public int solve(int[] nums) {

    int low = minimumPossibleAnswer;
    int high = maximumPossibleAnswer;
    int ans = -1;

    while (low <= high) {

        int mid = low + (high - low) / 2;

        if (isPossible(nums, mid)) {
            ans = mid;
            high = mid - 1; // minimize
        } else {
            low = mid + 1;
        }
    }

    return ans;
}
```

---

## Time Complexity

```text
O(log(Search Space) * Check Function)
```

## Space Complexity

```text
O(1)
```

---

## Important Insights

### Insight 1

Binary Search is not limited to arrays.

It can be applied on:

```text
Speed
Capacity
Distance
Time
Pages
Bananas
Days
```

---

### Insight 2

Need a monotonic pattern.

Example:

```text
Answer = 4 → Invalid
Answer = 5 → Invalid
Answer = 6 → Valid
Answer = 7 → Valid
Answer = 8 → Valid
```

Binary Search becomes possible.

---

### Insight 3

For Minimum Answer Problems

```java
if(valid)
    high = mid - 1;
```

Move left to find smaller answer.

---

### Insight 4

For Maximum Answer Problems

```java
if(valid)
    low = mid + 1;
```

Move right to find larger answer.

---

## Recognition Pattern

```text
Brute Force Over Answers
           ↓
Can Check Answer Efficiently
           ↓
True / False Pattern Exists
           ↓
Think Binary Search on Answers
```

---

# Problem 1: LeetCode 875 - Koko Eating Bananas

## Problem Statement

Find the minimum eating speed so Koko can finish all bananas within h hours.

---

## Approach

### Answer Space

```text
Minimum Speed = 1
Maximum Speed = max(piles)
```

### Check Function

For a speed k:

```text
Calculate total hours required.
```

If:

```text
hours <= h
```

Then speed is valid.

---

## Solution

```java
class Solution {

    public int minEatingSpeed(int[] piles, int h) {

        int low = 1;
        int high = 0;

        for (int pile : piles)
            high = Math.max(high, pile);

        int ans = high;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (canFinish(piles, h, mid)) {
                ans = mid;
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return ans;
    }

    private boolean canFinish(int[] piles, int h, int speed) {

        long hours = 0;

        for (int pile : piles) {
            hours += (pile + speed - 1) / speed;
        }

        return hours <= h;
    }
}
```

### TC

```text
O(n log(maxPile))
```

### SC

```text
O(1)
```

---

# Problem 2: LeetCode 1011 - Capacity To Ship Packages Within D Days

## Problem Statement

Find minimum ship capacity required to deliver packages within given days.

---

## Approach

### Answer Space

```text
Minimum Capacity = max(weights)
Maximum Capacity = sum(weights)
```

### Check Function

Simulate shipping.

If packages can be delivered within:

```text
days <= givenDays
```

Capacity is valid.

---

## Solution

```java
class Solution {

    public int shipWithinDays(int[] weights, int days) {

        int low = 0;
        int high = 0;

        for (int w : weights) {
            low = Math.max(low, w);
            high += w;
        }

        int ans = high;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (canShip(weights, days, mid)) {
                ans = mid;
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return ans;
    }

    private boolean canShip(int[] weights, int days, int capacity) {

        int requiredDays = 1;
        int load = 0;

        for (int weight : weights) {

            if (load + weight > capacity) {
                requiredDays++;
                load = weight;
            } else {
                load += weight;
            }
        }

        return requiredDays <= days;
    }
}
```

### TC

```text
O(n log(sum(weights)))
```

### SC

```text
O(1)
```

---

## Master Formula

```text
1. Find Answer Range
2. Create Check Function
3. Check Mid Answer
4. If Valid → Store Answer + Move Left
5. Else → Move Right
6. Return Best Answer
```

---

## Common LeetCode Problems

```text
875  - Koko Eating Bananas
1011 - Capacity To Ship Packages Within D Days
1283 - Find Smallest Divisor Given Threshold
1482 - Minimum Number of Days to Make m Bouquets
1552 - Magnetic Force Between Two Balls
1760 - Minimum Limit of Balls in a Bag
2187 - Minimum Time to Complete Trips
```
