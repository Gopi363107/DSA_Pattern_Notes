# Top K Elements

## Core Idea

Top K problems are about finding the **K most frequent / largest / best elements** without sorting the entire dataset.

We use:

```text id="tk1"
Heap (Priority Queue)
+ Frequency Map (sometimes)
```

---

## When to Use

* Top K frequent elements
* Top K largest/smallest values
* Most frequent words
* K best candidates
* Streaming data ranking
* Partial ordering problems

---

## Trigger Words

* Top K
* Most frequent
* Highest frequency
* K largest/smallest
* Best K results
* Ranking
* Leaderboard

---

## Recognition Pattern

```text id="tk2"
Need Top K results
         ↓
Full sort too expensive
         ↓
Keep only K best candidates
         ↓
Use Heap
```

---

# Core Idea

We only care about:

```text id="tk3"
K most relevant elements
```

So we discard everything else early.

---

# Approach 1: Min Heap (Most Important)

## Idea

Keep a **Min Heap of size K**.

---

## Why Min Heap?

We want:

```text id="tk4"
Top K largest / frequent elements
```

So we remove the smallest among current candidates.

---

## Steps

```text id="tk5"
1. Count frequency (if needed)
2. Push into heap
3. If size > K → remove smallest
4. Heap contains Top K
```

---

## Code: Top K Frequent Elements

```java id="tk6"
public int[] topKFrequent(int[] nums, int k){

    Map<Integer, Integer> map =
        new HashMap<>();

    for(int num : nums){
        map.put(num, map.getOrDefault(num, 0) + 1);
    }

    PriorityQueue<Integer> pq =
        new PriorityQueue<>(
            (a,b) -> map.get(a) - map.get(b)
        );

    for(int key : map.keySet()){

        pq.offer(key);

        if(pq.size() > k){
            pq.poll();
        }
    }

    int[] result = new int[k];

    for(int i = k - 1; i >= 0; i--){
        result[i] = pq.poll();
    }

    return result;
}
```

---

## Complexity

```text id="tk7"
Time: O(N log K)
Space: O(N)
```

---

# Approach 2: Max Heap (Alternative)

## Idea

Use Max Heap and extract K times.

---

## Code

```java id="tk8"
PriorityQueue<int[]> pq =
    new PriorityQueue<>((a,b) -> b[1] - a[1]);

for(Map.Entry<Integer,Integer> e : map.entrySet()){
    pq.offer(new int[]{e.getKey(), e.getValue()});
}

List<Integer> result = new ArrayList<>();

for(int i = 0; i < k; i++){
    result.add(pq.poll()[0]);
}
```

---

## Complexity

```text id="tk9"
Time: O(N log N)
Space: O(N)
```

---

# Approach 3: Bucket Sort (Advanced Optimization)

## Idea

Group elements by frequency.

---

## Steps

```text id="tk10"
1. Build frequency map
2. Create buckets of size N
3. Place elements in bucket[freq]
4. Traverse from high frequency to low
```

---

## Code

```java id="tk11"
public int[] topKFrequent(int[] nums, int k){

    Map<Integer,Integer> map =
        new HashMap<>();

    for(int num : nums){
        map.put(num, map.getOrDefault(num,0)+1);
    }

    List<Integer>[] bucket =
        new List[nums.length + 1];

    for(int key : map.keySet()){

        int freq = map.get(key);

        if(bucket[freq] == null){
            bucket[freq] = new ArrayList<>();
        }

        bucket[freq].add(key);
    }

    List<Integer> result =
        new ArrayList<>();

    for(int i = bucket.length - 1; i >= 0 && result.size() < k; i--){

        if(bucket[i] != null){
            result.addAll(bucket[i]);
        }
    }

    return result.stream().mapToInt(i -> i).toArray();
}
```

---

## Complexity

```text id="tk12"
Time: O(N)
Space: O(N)
```

---

# Approach 4: QuickSelect (Advanced)

## Idea

Partition to find Top K boundary.

---

## Use Case

```text id="tk13"
When exact ordering is not needed
```

---

# Visual Understanding

## Example

```text id="tk14"
nums = [1,1,1,2,2,3]
k = 2
```

---

## Frequency Map

```text id="tk15"
1 → 3
2 → 2
3 → 1
```

---

## Heap Flow (K=2)

```text id="tk16"
Add 1 → [1]
Add 2 → [2,1]
Add 3 → remove 1 → [3,2]
```

---

# Important Insights

### Insight 1

We never sort full data:

```text id="tk17"
Only maintain K best candidates
```

---

### Insight 2

Heap size is always:

```text id="tk18"
<= K
```

---

### Insight 3

Frequency map is often required:

```text id="tk19"
For ranking based problems
```

---

### Insight 4

Bucket sort is fastest when:

```text id="tk20"
Range is bounded (frequency-based)
```

---

# Common Interview Problems

```text id="tk21"
347  - Top K Frequent Elements

692  - Top K Frequent Words

215  - Kth Largest Element

373  - K Pairs with Smallest Sum

451  - Sort Characters by Frequency

973  - K Closest Points to Origin
```

---

# Pattern Map

| Problem Type      | Technique      |
| ----------------- | -------------- |
| Top K frequent    | Min Heap + Map |
| Top K largest     | Min Heap       |
| Top K smallest    | Max Heap       |
| Frequency ranking | Bucket Sort    |
| Pair ranking      | Heap           |

---

# Quick Revision

```text id="tk22"
Need Top K Results
        ↓
Count frequency (if needed)
        ↓
Use Min Heap of size K
        ↓
Or Bucket Sort for O(N)
```

---

# Master Formula

```text id="tk23"
Top K Problems

=

Heap (most used)
OR
Bucket Sort (optimized)
OR
QuickSelect (advanced)

-------------------------

Always maintain only K best elements

-------------------------

Answer = Top ranked subset
```
