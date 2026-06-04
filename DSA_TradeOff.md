# 🚀 DSA Problem Solving Cheat Sheet
# When to Use Which Data Structure + TC & SC

Always ask:

1. Need fast lookup? → HashMap/HashSet
2. Need min/max repeatedly? → Heap
3. Need ordering? → TreeMap/TreeSet/BST
4. Need shortest path? → BFS/Dijkstra
5. Need range query? → Prefix Sum
6. Need sliding window? → Deque
7. Need parent-child relation? → Tree
8. Need connectivity? → Graph/DSU
9. Need prefix matching? → Trie
10. Need monotonic answer? → Binary Search

---

# 🎯 STEP 1: Identify the Problem Type

Before coding, ask:

1. Do I need fast lookup?
2. Do I need ordering?
3. Do I need min/max frequently?
4. Do I need parent-child structure?
5. Do I need shortest path?
6. Do I need contiguous subarray?
7. Do I need prefix search?
8. Do I need range queries?

The answer usually reveals the data structure.

---

# 📦 ARRAY

## Use When

✅ Index access needed

✅ Fixed sequence

✅ Sliding window

✅ Two pointers

✅ Prefix sum

## Common Patterns

- Two Pointers
- Sliding Window
- Prefix Sum
- Binary Search
- Kadane

## Time Complexity

| Operation | TC |
|------------|----|
| Access | O(1) |
| Search | O(n) |
| Insert End | O(1) |
| Insert Middle | O(n) |
| Delete | O(n) |

## Space Complexity

O(n)

---

# 🔤 STRING

## Use When

✅ Character manipulation

✅ Pattern matching

✅ Palindrome

✅ Substring problems

## Common Patterns

- Two Pointers
- Sliding Window
- Hashing
- KMP
- Trie

## Important Hint

If question contains:

"substring"

"anagram"

"palindrome"

Think String + HashMap/Sliding Window

---

# 🧾 HASHMAP

## Use When

Need:

✅ Frequency counting

✅ Fast lookup

✅ Store value against key

## Keywords

- frequency
- count
- duplicate
- occurrence
- lookup

## Examples

Two Sum

Subarray Sum = K

Majority Element

Anagrams

## Operations

| Operation | TC |
|------------|----|
| Put | O(1) |
| Get | O(1) |
| Remove | O(1) |

Worst Case

O(n)

## Space

O(n)

---

# 🎯 HASHSET

## Use When

Need:

✅ Unique elements

✅ Fast existence check

## Keywords

- distinct
- unique
- duplicate

## Examples

Contains Duplicate

Longest Consecutive Sequence

## Operations

| Operation | TC |
|------------|----|
| Add | O(1) |
| Contains | O(1) |
| Remove | O(1) |

## Space

O(n)

---

# 📚 STACK

## Use When

Need:

✅ Last entered first processed

✅ Undo operation

✅ Backtracking

## Keywords

- nearest greater
- nearest smaller
- balanced bracket
- expression

## Examples

Valid Parentheses

Daily Temperatures

Next Greater Element

Largest Rectangle

## Operations

| Operation | TC |
|------------|----|
| Push | O(1) |
| Pop | O(1) |
| Peek | O(1) |

## Space

O(n)

---

# 🚶 QUEUE

## Use When

Need:

✅ First entered first processed

✅ Level order processing

## Keywords

- level
- shortest steps
- minimum moves

## Examples

Binary Tree Level Order

BFS

Rotting Oranges

## Operations

| Operation | TC |
|------------|----|
| Offer | O(1) |
| Poll | O(1) |
| Peek | O(1) |

## Space

O(n)

---

# 🔥 DEQUE

## Use When

Need:

✅ Add/remove both ends

✅ Sliding window optimization

## Keywords

- window maximum
- window minimum

## Examples

Sliding Window Maximum

Shortest Subarray

## Operations

| Operation | TC |
|------------|----|
| Add First | O(1) |
| Add Last | O(1) |
| Remove First | O(1) |
| Remove Last | O(1) |

## Space

O(n)

---

# ⚡ PRIORITY QUEUE (HEAP)

## Use When

Need:

✅ Largest element repeatedly

✅ Smallest element repeatedly

✅ Top K

## Keywords

- kth
- top k
- minimum
- maximum

## Examples

Kth Largest

Merge K Sorted Lists

Task Scheduler

## Operations

| Operation | TC |
|------------|----|
| Insert | O(log n) |
| Delete | O(log n) |
| Peek | O(1) |

## Space

O(n)

---

# 🌳 TREE

## Use When

Need:

✅ Hierarchical structure

✅ Recursive traversal

## Common Traversals

DFS

BFS

Inorder

Preorder

Postorder

## Examples

Diameter

LCA

Path Sum

Max Depth

## Typical Complexity

Traversal

TC = O(n)

SC = O(h)

h = tree height

---

# 🔍 BST

## Use When

Need:

✅ Ordered data

✅ Search efficiently

## Operations

| Operation | Average |
|------------|----------|
| Search | O(log n) |
| Insert | O(log n) |
| Delete | O(log n) |

Worst

O(n)

---

# 🌐 GRAPH

## Use When

Need:

✅ Relationship modeling

✅ Connectivity

✅ Shortest path

## Keywords

- route
- path
- connection
- network

## Common Algorithms

BFS

DFS

Dijkstra

Topological Sort

Union Find

## Traversal

TC = O(V + E)

SC = O(V)

---

# ⚡ TRIE

## Use When

Need:

✅ Prefix searching

✅ Dictionary search

## Keywords

- prefix
- autocomplete
- dictionary

## Examples

Word Search

Implement Trie

Autocomplete

## Operations

| Operation | TC |
|------------|----|
| Insert | O(L) |
| Search | O(L) |
| StartsWith | O(L) |

L = word length

---

# 🔗 LINKED LIST

## Use When

Need:

✅ Frequent insertion/deletion

## Keywords

- reverse list
- cycle
- merge list

## Examples

Reverse Linked List

Cycle Detection

Merge Two Lists

## Operations

| Operation | TC |
|------------|----|
| Insert Head | O(1) |
| Delete Head | O(1) |
| Search | O(n) |

---

# 📊 PREFIX SUM

## Use When

Need:

✅ Multiple range sum queries

## Keywords

- range sum
- subarray sum

## Example

Subarray Sum

Range Sum Query

## Complexity

Build

TC = O(n)

Query

TC = O(1)

Space

O(n)

---

# ⚡ BINARY SEARCH

## Use When

Array is:

✅ Sorted

OR

Answer space is monotonic

## Keywords

- sorted
- minimum possible
- maximum possible
- kth

## Complexity

TC = O(log n)

SC = O(1)

---

# 🔥 UNION FIND (DSU)

## Use When

Need:

✅ Connectivity

✅ Cycle detection

## Keywords

- connected components
- cycle in graph

## Complexity

Almost O(1)

O(α(n))

Space

O(n)

---

# 🎯 QUICK INTERVIEW DECISION TABLE

| If You See | Use |
|------------|------|
| Frequency Count | HashMap |
| Unique Elements | HashSet |
| Nearest Greater/Smaller | Stack |
| Level Order | Queue |
| Sliding Window Maximum | Deque |
| Top K | Heap |
| Sorted Search | Binary Search |
| Prefix Search | Trie |
| Parent Child | Tree |
| Network Connections | Graph |
| Connectivity | DSU |
| Range Sum Query | Prefix Sum |
| Fast Insert/Delete | Linked List |
| Ordered Keys | TreeMap |
| Ordered Unique Values | TreeSet |

---

# 🏆 Golden Rule

Always ask:

1. Need fast lookup? → HashMap/HashSet
2. Need min/max repeatedly? → Heap
3. Need ordering? → TreeMap/TreeSet/BST
4. Need shortest path? → BFS/Dijkstra
5. Need range query? → Prefix Sum
6. Need sliding window? → Deque
7. Need parent-child relation? → Tree
8. Need connectivity? → Graph/DSU
9. Need prefix matching? → Trie
10. Need monotonic answer? → Binary Search

If you can answer these 10 questions while reading a problem, you'll identify the correct data structure much faster in interviews.