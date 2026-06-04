#  Java Data Structures Complete Operations Cheat Sheet

---

#  1. Array

## Creation

```java
int[] arr = new int[5];

int[] arr2 = {1,2,3,4,5};

String[] names = {"A","B","C"};
```

## Operations

```java
arr.length;

arr[0];

arr[1] = 10;

Arrays.sort(arr);

Arrays.fill(arr, 100);

int idx = Arrays.binarySearch(arr, 10);

int[] copy = Arrays.copyOf(arr, arr.length);

String str = Arrays.toString(arr);
```

---

#  2. ArrayList

## Creation

```java
ArrayList<Integer> list = new ArrayList<>();

List<Integer> list2 = new ArrayList<>();

ArrayList<String> names = new ArrayList<>();
```

## Operations

```java
list.add(10);

list.add(1,20);

list.get(0);

list.set(0,100);

list.remove(0);

list.remove(Integer.valueOf(10));

list.contains(10);

list.indexOf(10);

list.size();

list.isEmpty();

list.clear();

Collections.sort(list);

Collections.reverse(list);

Collections.max(list);

Collections.min(list);
```

---

#  3. String

## Creation

```java
String s = "hello";

String s2 = new String("hello");
```

## Operations

```java
s.length();

s.charAt(0);

s.substring(1);

s.substring(1,4);

s.contains("he");

s.startsWith("h");

s.endsWith("o");

s.indexOf('e');

s.lastIndexOf('l');

s.toUpperCase();

s.toLowerCase();

s.trim();

s.replace("l","x");

s.split(" ");

s.equals(s2);

s.equalsIgnoreCase(s2);

String.join("-", "a","b","c");
```

---

#  4. StringBuilder

## Creation

```java
StringBuilder sb = new StringBuilder();

StringBuilder sb2 = new StringBuilder("hello");
```

## Operations

```java
sb.append("abc");

sb.insert(0,"x");

sb.delete(0,1);

sb.deleteCharAt(0);

sb.reverse();

sb.replace(0,2,"hi");

sb.charAt(0);

sb.setCharAt(0,'A');

sb.length();

sb.toString();
```

---

#  5. HashMap

## Creation

```java
HashMap<Integer,String> map = new HashMap<>();

Map<Integer,String> map2 = new HashMap<>();
```

## Operations

```java
map.put(1,"A");

map.putIfAbsent(2,"B");

map.get(1);

map.getOrDefault(3,"NA");

map.containsKey(1);

map.containsValue("A");

map.remove(1);

map.replace(1,"X");

map.size();

map.isEmpty();

map.clear();

map.keySet();

map.values();

map.entrySet();
```

## Iteration

```java
for(Integer key : map.keySet()){
    System.out.println(key);
}

for(String value : map.values()){
    System.out.println(value);
}

for(Map.Entry<Integer,String> entry : map.entrySet()){
    System.out.println(entry.getKey()+" "+entry.getValue());
}
```

---

#  6. HashSet

## Creation

```java
HashSet<Integer> set = new HashSet<>();

Set<Integer> set2 = new HashSet<>();
```

## Operations

```java
set.add(10);

set.remove(10);

set.contains(10);

set.size();

set.isEmpty();

set.clear();
```

## Iteration

```java
for(int num : set){
    System.out.println(num);
}
```

---

#  7. TreeSet

## Creation

```java
TreeSet<Integer> set = new TreeSet<>();
```

## Operations

```java
set.add(10);

set.remove(10);

set.contains(10);

set.first();

set.last();

set.ceiling(15);

set.floor(15);

set.higher(15);

set.lower(15);

set.pollFirst();

set.pollLast();

set.size();
```

---

#  8. Stack

## Creation

```java
Stack<Integer> stack = new Stack<>();
```

## Operations

```java
stack.push(10);

stack.pop();

stack.peek();

stack.empty();

stack.size();

stack.search(10);
```

---

#  9. Queue

## Creation

```java
Queue<Integer> q = new LinkedList<>();
```

## Operations

```java
q.offer(10);

q.offer(20);

q.poll();

q.peek();

q.size();

q.isEmpty();
```

---

#  10. Deque

## Creation

```java
Deque<Integer> dq = new ArrayDeque<>();
```

## Operations

```java
dq.offerFirst(10);

dq.offerLast(20);

dq.pollFirst();

dq.pollLast();

dq.peekFirst();

dq.peekLast();

dq.size();

dq.isEmpty();
```

---

#  11. Priority Queue (Heap)

## Min Heap

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
```

## Max Heap

```java
PriorityQueue<Integer> maxHeap =
        new PriorityQueue<>(Collections.reverseOrder());
```

## Operations

```java
pq.offer(10);

pq.offer(5);

pq.offer(20);

pq.poll();

pq.peek();

pq.size();

pq.isEmpty();
```

---

#  12. LinkedList

## Creation

```java
LinkedList<Integer> list = new LinkedList<>();
```

## Operations

```java
list.add(10);

list.addFirst(5);

list.addLast(20);

list.removeFirst();

list.removeLast();

list.getFirst();

list.getLast();

list.size();

list.isEmpty();
```

---

#  13. TreeMap

## Creation

```java
TreeMap<Integer,String> map = new TreeMap<>();
```

## Operations

```java
map.put(1,"A");

map.get(1);

map.remove(1);

map.firstKey();

map.lastKey();

map.ceilingKey(5);

map.floorKey(5);

map.higherKey(5);

map.lowerKey(5);

map.size();
```

---

#  14. Graph (Adjacency List)

## Creation

```java
int n = 5;

List<List<Integer>> graph = new ArrayList<>();

for(int i=0;i<n;i++){
    graph.add(new ArrayList<>());
}
```

## Add Edge

```java
graph.get(0).add(1);

graph.get(1).add(0);
```

## Traversal

```java
for(int neigh : graph.get(node)){
    System.out.println(neigh);
}
```

---

#  15. Binary Tree Node

## Creation

```java
class TreeNode{
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int val){
        this.val = val;
    }
}
```

## Create Tree

```java
TreeNode root = new TreeNode(1);

root.left = new TreeNode(2);

root.right = new TreeNode(3);
```

---

#  16. Trie

## Node

```java
class TrieNode{
    TrieNode[] children = new TrieNode[26];
    boolean isEnd;
}
```

## Root

```java
TrieNode root = new TrieNode();
```

---

#  17. Prefix Sum

## Creation

```java
int[] prefix = new int[n];

prefix[0] = arr[0];

for(int i=1;i<n;i++){
    prefix[i] = prefix[i-1] + arr[i];
}
```

## Range Sum

```java
int sum = prefix[r] -
          (l == 0 ? 0 : prefix[l-1]);
```

---

#  18. Arrays Utility Methods

```java
Arrays.sort(arr);

Arrays.fill(arr,0);

Arrays.binarySearch(arr,5);

Arrays.copyOf(arr,n);

Arrays.equals(arr1,arr2);

Arrays.toString(arr);
```

---

#  19. Collections Utility Methods

```java
Collections.sort(list);

Collections.reverse(list);

Collections.shuffle(list);

Collections.max(list);

Collections.min(list);

Collections.frequency(list,10);

Collections.swap(list,0,1);
```

---

#  Most Important Interview Operations

```java
ArrayList:
add()
get()
set()
remove()
contains()

HashMap:
put()
get()
getOrDefault()
containsKey()

HashSet:
add()
contains()
remove()

Queue:
offer()
poll()
peek()

Stack:
push()
pop()
peek()

Deque:
offerFirst()
offerLast()
pollFirst()
pollLast()

PriorityQueue:
offer()
poll()
peek()

TreeMap:
ceilingKey()
floorKey()

TreeSet:
ceiling()
floor()
higher()
lower()

String:
substring()
charAt()
split()

StringBuilder:
append()
delete()
reverse()
```

---

# 🏆 For DSA Interviews

Master these 10 DS first:

1. Array
2. String
3. HashMap
4. HashSet
5. Stack
6. Queue
7. Deque
8. PriorityQueue
9. Tree
10. Graph

These alone cover roughly 90%+ of coding interview questions.