# Merge K Sorted Lists / Arrays

## Core Idea

We are given **K sorted lists/arrays** and need to merge them into one sorted output.

Instead of merging one by one:

```text id="m1"
K-way merge using Heap (Priority Queue)
```

gives optimal performance.

---

## When to Use

* K sorted arrays
* K sorted linked lists
* External sorting
* Merge intervals of sorted streams
* Streaming sorted data
* Top merging problems

---

## Trigger Words

* Merge K sorted
* Multiple sorted lists
* Combine sorted streams
* Sorted input chunks
* External sorting
* Priority merge

---

## Recognition Pattern

```text id="m2"
Multiple Sorted Inputs
          ↓
Need Final Sorted Output
          ↓
Pairwise merge is slow
          ↓
Use Min Heap (K-way merge)
```

---

# Core Idea

At any moment:

```text id="m3"
We only care about the SMALLEST current element among all lists
```

Heap helps track that efficiently.

---

# Approach 1: Min Heap (Optimal)

## Idea

Push first element of each list into heap.

---

## Step Flow

```text id="m4"
1. Insert first element of all K lists
2. Extract minimum
3. Add next element from same list
4. Repeat
```

---

## Why It Works

Heap always contains:

```text id="m5"
Current smallest unprocessed elements from each list
```

---

# Java Code (K Sorted Arrays)

```java id="m6"
class Node {
    int val;
    int row;
    int col;

    Node(int v, int r, int c){
        val = v;
        row = r;
        col = c;
    }
}
```

---

```java id="m7"
public List<Integer> mergeKSorted(int[][] arr){

    PriorityQueue<Node> pq =
        new PriorityQueue<>((a,b) -> a.val - b.val);

    int k = arr.length;

    for(int i = 0; i < k; i++){
        pq.offer(new Node(arr[i][0], i, 0));
    }

    List<Integer> result =
        new ArrayList<>();

    while(!pq.isEmpty()){

        Node cur = pq.poll();

        result.add(cur.val);

        int r = cur.row;
        int c = cur.col + 1;

        if(c < arr[r].length){
            pq.offer(new Node(arr[r][c], r, c));
        }
    }

    return result;
}
```

---

## Time Complexity

```text id="m8"
O(N log K)
```

Where:

```text id="m9"
N = total elements
K = number of lists
```

---

## Space Complexity

```text id="m10"
O(K)
```

---

# Approach 2: Divide and Conquer

## Idea

Merge lists like merge sort.

---

## Steps

```text id="m11"
Split K lists into halves
Merge recursively
```

---

## Code

```java id="m12"
public ListNode mergeKLists(ListNode[] lists){

    if(lists.length == 0) return null;

    return merge(lists, 0, lists.length - 1);
}

private ListNode merge(ListNode[] lists, int l, int r){

    if(l == r) return lists[l];

    int mid = l + (r - l) / 2;

    ListNode left = merge(lists, l, mid);
    ListNode right = merge(lists, mid + 1, r);

    return mergeTwo(left, right);
}
```

---

## Merge Two Lists

```java id="m13"
private ListNode mergeTwo(ListNode a, ListNode b){

    ListNode dummy = new ListNode(-1);
    ListNode temp = dummy;

    while(a != null && b != null){

        if(a.val < b.val){
            temp.next = a;
            a = a.next;
        } else {
            temp.next = b;
            b = b.next;
        }

        temp = temp.next;
    }

    if(a != null) temp.next = a;
    if(b != null) temp.next = b;

    return dummy.next;
}
```

---

## Complexity

```text id="m14"
Time: O(N log K)
Space: O(log K)
```

---

# Approach 3: Brute Force (Not Recommended)

## Idea

Collect all elements and sort.

---

## Code

```text id="m15"
Flatten → Sort → Return
```

---

## Complexity

```text id="m16"
Time: O(N log N)
Space: O(N)
```

---

# Linked List Version (Important)

## Same Idea

Instead of arrays:

```text id="m17"
Use ListNode in Heap
```

---

## Heap Node

```java id="m18"
class Node {
    ListNode node;

    Node(ListNode n){
        node = n;
    }
}
```

---

## Key Trick

```text id="m19"
Push head of each list
Extract min
Push next node
```

---

# Visual Understanding

## Example

```text id="m20"
List 1: 1 → 4 → 7
List 2: 2 → 5 → 8
List 3: 3 → 6 → 9
```

---

## Heap Flow

```text id="m21"
1,2,3 → extract 1
4,2,3 → extract 2
4,5,3 → extract 3
...
```

---

# Important Insights

### Insight 1

Heap always stores:

```text id="m22"
K candidates (one per list)
```

---

### Insight 2

We never scan full lists again.

```text id="m23"
Only next element is pushed
```

---

### Insight 3

Each element:

```text id="m24"
Inserted once

Removed once
```

---

### Insight 4

Optimal for streaming merge.

---

# Common Interview Problems

```text id="m25"
23   - Merge K Sorted Lists

373  - Find K Pairs with Smallest Sums

378  - Kth Smallest in Sorted Matrix

347  - Top K Frequent Elements

632  - Smallest Range Covering Elements

786  - Kth Smallest Prime Fraction
```

---

# Pattern Map

| Problem Type    | Technique |
| --------------- | --------- |
| K sorted merge  | Min Heap  |
| K lists merge   | Heap      |
| Sorted matrix   | Heap      |
| Pair sums       | Heap      |
| Streaming merge | Heap      |

---

# Quick Revision

```text id="m26"
K Sorted Inputs
        ↓
Need Sorted Output
        ↓
Use Min Heap
        ↓
Push first elements
        ↓
Extract min + push next
```

---

# Master Formula

```text id="m27"
K-Way Merge

=

Min Heap over all lists

-----------------------

Always keep smallest available elements

-----------------------

Process one element at a time

-----------------------

O(N log K)
```
