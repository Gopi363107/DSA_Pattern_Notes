# 09 - String Dynamic Programming Pattern

> **Core Idea:** Solve problems involving one or more strings by defining DP states over character positions and building answers from smaller prefixes or suffixes.

---

# What is String DP?

String DP is used when the input is one or more strings and the answer depends on comparing, matching, transforming, or counting characters.

Unlike Array DP,

```
Index

↓

Value
```

String DP usually works on

```
Character Positions

↓

Prefixes

or

Suffixes
```

---

# When Should You Think of String DP?

Whenever the problem contains

- String
- Subsequence
- Prefix
- Suffix
- Matching
- Transformation
- Edit
- Deletion
- Insertion
- Counting subsequences

Immediately ask

> Can I define the answer using the first i characters (or first i and j characters)?

If YES,

think String DP.

---

# Common String DP Patterns

```
               String DP
                    │
      ┌─────────────┼─────────────┐
      │             │             │
 One String      Two Strings   Three Strings
      │             │
Palindrome      LCS Family
      │             │
Word Break   Edit Distance
```

---

# Common State Definitions

## Pattern 1

One string

```
dp[i]
```

Meaning

```
Answer

using first

i

characters
```

Example

```
Word Break

Decode Ways
```

---

## Pattern 2

Two strings

```
dp[i][j]
```

Meaning

```
Answer

using first

i

characters of s1

and

first

j

characters of s2
```

Example

```
LCS

Edit Distance

Distinct Subsequences
```

---

## Pattern 3

Three strings

```
dp[i][j][k]
```

Rare.

Example

```
LCS of Three Strings
```

---

# Generic Thinking Process

## Step 1

Define

```
dp[i]

or

dp[i][j]
```

---

## Step 2

Compare characters.

```
s1[i]

s2[j]
```

---

## Step 3

Match

OR

Skip

---

## Step 4

Return final state.

---

# Generic Two String Recurrence

If characters match

```
dp[i][j]

=

1

+

dp[i-1][j-1]
```

Else

```
Choose

Best

among possibilities.
```

---

# Generic Memoization Template

```java
int solve(int i, int j){

    if(base case)
        return answer;

    if(dp[i][j] != -1)
        return dp[i][j];

    if(s1.charAt(i) == s2.charAt(j)){

        return dp[i][j] =
                1 +

                solve(i-1, j-1);
    }

    return dp[i][j] =
            Math.max(

                solve(i-1, j),

                solve(i, j-1)

            );
}
```

---

# Generic Tabulation Template

```java
for(int i = 1; i <= n; i++){

    for(int j = 1; j <= m; j++){

        if(s1.charAt(i-1) == s2.charAt(j-1)){

            dp[i][j] =
                    1 +

                    dp[i-1][j-1];
        }
        else{

            dp[i][j] =
                    Math.max(

                        dp[i-1][j],

                        dp[i][j-1]

                    );
        }
    }
}
```

---

# Pattern Recognition

Question contains

```
Two Strings

↓

dp[i][j]
```

Question contains

```
One String

↓

dp[i]
```

Question contains

```
Three Strings

↓

dp[i][j][k]
```

---

# Competitive Programming Insight

Nearly every String DP problem asks one of four questions:

```
Longest

Shortest

Minimum

Count
```

Recognizing which one is required determines the transition.

---

# Problem 1

## LeetCode 139 — Word Break

Difficulty

Medium

---

## Core Idea

At every index,

check whether a valid dictionary word ends there.

---

## State

```
dp[i]

True

if first

i

characters

can be segmented.
```

---

## Transition

Try every possible previous split.

---

### Java Solution

```java
class Solution {

    public boolean wordBreak(String s,
                             List<String> wordDict){

        Set<String> set =
                new HashSet<>(wordDict);

        boolean[] dp =
                new boolean[s.length()+1];

        dp[0] = true;

        for(int i = 1;
            i <= s.length();
            i++){

            for(int j = 0;
                j < i;
                j++){

                if(dp[j] &&
                   set.contains(s.substring(j,i))){

                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[s.length()];
    }
}
```

---

### Time Complexity

```
O(n²)
```

---

# Problem 2

## LeetCode 72 — Edit Distance

Difficulty

Medium

---

## Core Idea

Convert one string into another using

- Insert
- Delete
- Replace

---

## State

```
dp[i][j]

Minimum operations

for prefixes.
```

---

## Transition

Characters equal

↓

Diagonal

Else

↓

Minimum of

Insert

Delete

Replace

---

### Time Complexity

```
O(nm)
```

---

# Problem 3

## LeetCode 115 — Distinct Subsequences

Difficulty

Hard

---

## Core Idea

Count

how many ways

string

t

appears

inside

s.

---

## State

```
dp[i][j]

Ways

to build

first

j

characters

using first

i

characters.
```

---

## Transition

If equal

↓

Take

+

Skip

Else

↓

Skip

---

### Time Complexity

```
O(nm)
```

---

# Common Mistakes

❌ Confusing substring with subsequence.

❌ Wrong indexing (`i` vs `i-1`).

❌ Forgetting base cases for empty strings.

❌ Using recursion without memoization.

❌ Incorrect DP table initialization.

---

# Interview Mental Checklist

- One string or two strings?
- Is this substring or subsequence?
- What should `dp[i]` or `dp[i][j]` represent?
- Match or skip?
- Am I optimizing length, count, or cost?

---

# Pattern Summary

| Feature | Description |
|----------|-------------|
| State | `dp[i]`, `dp[i][j]` |
| Core Idea | Prefix-based DP |
| Time Complexity | Usually `O(n²)` or `O(nm)` |
| Space | `O(n)` or `O(nm)` |
| Common Topics | LCS, Edit Distance, Word Break, Distinct Subsequences |

---

# Mastery Checklist

- [ ] Recognize String DP problems.
- [ ] Distinguish substring vs subsequence.
- [ ] Write one-string DP.
- [ ] Write two-string DP.
- [ ] Understand match/skip transitions.
- [ ] Optimize space where possible.

---

# String DP Variations

| Pattern | Example |
|----------|---------|
| One String | Word Break |
| One String | Decode Ways |
| Two Strings | LCS |
| Two Strings | Edit Distance |
| Two Strings | Distinct Subsequences |
| Interval + String | Palindrome Partitioning |
| Three Strings | LCS of Three Strings |

---

# Space Optimization

Many String DP problems only need

```
Previous Row
```

Therefore

```
O(nm)

↓

O(m)
```

Examples

- LCS
- Edit Distance
- Distinct Subsequences

---

# Final Goal

After mastering String DP, you should be able to:

- Recognize prefix-based DP immediately.
- Design one-string and two-string DP states.
- Solve matching, transformation, counting, and segmentation problems.
- Optimize String DP solutions when only previous states are needed.
- Confidently solve String DP questions asked in Top MNCs, FinTech companies, and competitive programming.

---

> **Golden Rule:** If the answer depends on **characters, prefixes, or matching between strings**, think **String Dynamic Programming**.