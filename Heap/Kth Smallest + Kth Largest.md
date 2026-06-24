# Kth Smallest / Kth Largest

## Core Idea

Kth order problems are about maintaining **only the top K candidates efficiently** instead of sorting the full array.

We use:

```text id="k1"
Heap (Priority Queue)
OR
Quick Select (Partitioning)
```

---

## When to Use

* Kth largest element
* Kth smallest element
* Top K elements
* Stream of numbers
* Dynamic ranking
* Partial sorting

---

## Trigger Words

* Kth largest
* Kth smallest
* Top K
* Smallest/largest element
* Ranking
* Order statistics
* Stream queries

---

## Recognition Pattern

```text id="k2"
Need Kth element
        ↓
Full sorting too slow
        ↓
Maintain only K elements
        ↓
Use Heap or QuickSelect
```

---

# Approach 1: Min Heap (Kth Largest)

## Idea

Keep a Min Heap of size K.

---

## Why Min Heap?

We want:

```text id="k3"
K largest elements
```

So we remove smallest among them.

---

## Steps

```text id="k4"
1. Push elements into heap
2. If size > K → remove smallest
3. Top = Kth largest
```

---

## Code

```java id="k5"
public int findKthLargest(int[] nums, int k){

    PriorityQueue<Integer> pq =
        new PriorityQueue<>();

    for(int num : nums){

        pq.offer(num);

        if(pq.size() > k){
            pq.poll();
        }
    }

    return pq.peek();
}
```

---

## Complexity

```text id="k6"
Time: O(N log K)
Space: O(K)
```

---

# Approach 2: Max Heap (Kth Smallest)

## Idea

Use Max Heap of size K.

---

## Why Max Heap?

We want:

```text id="k7"
K smallest elements
```

So we remove largest among them.

---

## Code

```java id="k8"
public int kthSmallest(int[] nums, int k){

    PriorityQueue<Integer> pq =
        new PriorityQueue<>((a,b) -> b - a);

    for(int num : nums){

        pq.offer(num);

        if(pq.size() > k){
            pq.poll();
        }
    }

    return pq.peek();
}
```

---

## Complexity

```text id="k9"
Time: O(N log K)
Space: O(K)
```

---

# Approach 3: QuickSelect (Optimal Average Case)

## Idea

Use partitioning like QuickSort.

---

## Key Insight

After partition:

```text id="k10"
Left → smaller elements
Right → larger elements
```

---

## Steps

```text id="k11"
1. Pick pivot
2. Partition array
3. Check pivot position
4. Recurse only on one side
```

---

## Code

```java id="k12"
public int findKthLargest(int[] nums, int k){

    int n = nums.length;
    return quickSelect(nums, 0, n - 1, n - k);
}

private int quickSelect(int[] nums, int l, int r, int k){

    int pivot = partition(nums, l, r);

    if(pivot == k){
        return nums[pivot];
    } else if(pivot < k){
        return quickSelect(nums, pivot + 1, r, k);
    } else {
        return quickSelect(nums, l, pivot - 1, k);
    }
}
```

---

## Partition

```java id="k13"
private int partition(int[] nums, int l, int r){

    int pivot = nums[r];
    int i = l;

    for(int j = l; j < r; j++){

        if(nums[j] <= pivot){
            swap(nums, i, j);
            i++;
        }
    }

    swap(nums, i, r);
    return i;
}
```

---

## Complexity

```text id="k14"
Average: O(N)
Worst: O(N²)
Space: O(1)
```

---

# Heap vs QuickSelect

| Method      | Time       | Space | Stability        |
| ----------- | ---------- | ----- | ---------------- |
| Heap        | O(N log K) | O(K)  | Always safe      |
| QuickSelect | O(N) avg   | O(1)  | Risky worst case |

---

# Visual Understanding

## Example

```text id="k15"
nums = [3,2,1,5,6,4]
k = 2
```

---

## Kth Largest

```text id="k16"
Answer = 5
```

---

## Heap Flow

```text id="k17"
Keep only 2 largest:

[3]
[3,2]
remove 1 → keep 3,2
add 5 → remove 2 → [5,3]
add 6 → remove 3 → [6,5]
```

---

# Important Insights

### Insight 1

We never sort fully:

```text id="k18"
Only maintain K elements
```

---

### Insight 2

Heap top always gives:

```text id="k19"
Current Kth element
```

---

### Insight 3

QuickSelect works like:

```text id="k20"
Binary Search on sorted position
```

---

### Insight 4

Best real interview choice:

```text id="k21"
Heap (safe + easy)
```

---

# Common Interview Problems

```text id="k22"
215  - Kth Largest Element in Array

703  - Kth Largest Element in a Stream

347  - Top K Frequent Elements

378  - Kth Smallest in Sorted Matrix

373  - Find K Pairs with Smallest Sums

692  - Top K Frequent Words
```

---

# Pattern Map

| Problem Type  | Technique |
| ------------- | --------- |
| Kth largest   | Min Heap  |
| Kth smallest  | Max Heap  |
| Stream Kth    | Heap      |
| Top K         | Heap      |
| Kth in matrix | Heap      |

---

# Quick Revision

```text id="k23"
Need Kth Element
        ↓
Don’t sort fully
        ↓
Use Heap or QuickSelect

----------------

Kth Largest → Min Heap

Kth Smallest → Max Heap

Best Performance → QuickSelect

----------------

Maintain only K elements
```

---

# Master Formula

```text id="k24"
Kth Element Problems

=

Heap (safe) OR QuickSelect (fast)

-----------------------------

Heap:
Keep size K

QuickSelect:
Partition like binary search

-----------------------------

Answer = Kth position in order
```
