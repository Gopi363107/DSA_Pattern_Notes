# Heap + Greedy

## Core Idea

Heap + Greedy is used when:

```text id="g1"
We must always pick the BEST available option
BUT choices keep changing dynamically
```

So we combine:

```text id="g2"
Greedy Decision Making
+
Heap (to track best option efficiently)
```

---

## When to Use

* Scheduling with deadlines
* Maximum profit problems
* K selection problems
* Interval optimization
* Task selection under constraints
* Resource allocation problems

---

## Trigger Words

* Maximum profit
* Minimum cost
* Schedule tasks
* Pick best K
* Deadline
* Interval optimization
* Greedy selection

---

## Recognition Pattern

```text id="g3"
Need BEST choice repeatedly
            ↓
But choices change over time
            ↓
Greedy alone is not enough
            ↓
Use Heap to track best candidate
```

---

# Why Heap + Greedy Works

Greedy alone:

```text id="g4"
Fix decision → may fail later
```

Heap helps:

```text id="g5"
Always know current best valid option
```

---

# Type 1: Scheduling with Deadlines

## Idea

Pick tasks with maximum profit before deadline.

---

## Approach

Sort by deadline + use Min Heap for profit.

---

## Pattern

```text id="g6"
Sort tasks by deadline
Use heap for selected tasks
Replace smaller profit if needed
```

---

## Code

```java id="g7"
class Task {
    int profit;
    int deadline;

    Task(int p, int d){
        profit = p;
        deadline = d;
    }
}
```

---

```java id="g8"
public int jobScheduling(Task[] tasks){

    Arrays.sort(tasks, (a,b) -> a.deadline - b.deadline);

    PriorityQueue<Integer> pq =
        new PriorityQueue<>();

    for(Task t : tasks){

        pq.offer(t.profit);

        if(pq.size() > t.deadline){
            pq.poll();
        }
    }

    int total = 0;

    for(int p : pq){
        total += p;
    }

    return total;
}
```

---

## Complexity

```text id="g9"
Time: O(N log N)
Space: O(N)
```

---

# Type 2: K Largest / Smallest Problems

## Idea

Maintain heap of size K.

---

## Pattern

```text id="g10"
Iterate elements
Push into heap
If size > K → remove worst
```

---

## Example

```text id="g11"
Kth largest element
Top K frequent elements
K closest points
```

---

## Code

```java id="g12"
PriorityQueue<Integer> pq =
    new PriorityQueue<>();

for(int x : nums){

    pq.offer(x);

    if(pq.size() > k){
        pq.poll();
    }
}

return pq.peek();
```

---

## Complexity

```text id="g13"
Time: O(N log K)
Space: O(K)
```

---

# Type 3: Interval Greedy Optimization

## Idea

Choose intervals that maximize usage.

---

## Pattern

```text id="g14"
Sort intervals
Use heap to track active intervals
Greedily assign resources
```

---

## Example

```text id="g15"
Minimum meeting rooms
Maximum events attendable
Non-overlapping intervals
```

---

# Type 4: Connect / Merge Cost Problems

## Idea

Always merge smallest cost first.

---

## Pattern

```text id="g16"
Use Min Heap
Repeatedly combine smallest elements
Accumulate cost
```

---

## Example

```text id="g17"
Connect ropes with minimum cost
Optimal merge pattern
Huffman coding idea
```

---

## Code

```java id="g18"
PriorityQueue<Integer> pq =
    new PriorityQueue<>();

for(int x : arr){
    pq.offer(x);
}

int cost = 0;

while(pq.size() > 1){

    int a = pq.poll();
    int b = pq.poll();

    int sum = a + b;

    cost += sum;

    pq.offer(sum);
}

return cost;
```

---

## Complexity

```text id="g19"
O(N log N)
```

---

# Type 5: Greedy Selection with Constraints

## Idea

Select best valid option under constraints.

---

## Pattern

```text id="g20"
Push all options into heap
Pick best valid option
Remove invalid choices dynamically
```

---

## Example

```text id="g21"
Task scheduler
Rearrange strings
CPU scheduling problems
```

---

# Important Insights

### Insight 1

Greedy decides:

```text id="g22"
WHAT to pick
```

Heap decides:

```text id="g23"
WHAT is best available now
```

---

### Insight 2

Heap ensures:

```text id="g24"
Fast retrieval of best candidate
```

---

### Insight 3

Sorting alone is not enough when:

```text id="g25"
Choices depend on dynamic constraints
```

---

### Insight 4

Heap maintains:

```text id="g26"
Live optimal set
```

---

# Common Interview Problems

```text id="g27"
23   - Merge k Sorted Lists

502  - IPO (Maximize Capital)

621  - Task Scheduler

253  - Meeting Rooms II

1353 - Maximum Number of Events

857  - Minimum Cost to Hire K Workers

1834 - Single-Threaded CPU

1167 - Minimum Cost to Connect Sticks
```

---

# Pattern Map

| Type                | Technique     |
| ------------------- | ------------- |
| Top K               | Min Heap      |
| Max Profit          | Max Heap      |
| Scheduling          | Greedy + Heap |
| Merge Cost          | Min Heap      |
| Resource Allocation | Heap          |

---

# Quick Revision

```text id="g28"
Need Best Choice Repeatedly
            ↓
Use Heap

----------------

Need Fixed Order Only
            ↓
Use Sorting

----------------

Dynamic Best Choice
            ↓
Greedy + Heap

----------------

Top K Problems
            ↓
Heap Size K
```

---

# Master Formula

```text id="g29"
Greedy + Heap

=

Make best decision

BUT track candidates dynamically

----------------

Heap = Live best options

Greedy = Selection logic

----------------

Answer = Optimal sequence of choices
```
