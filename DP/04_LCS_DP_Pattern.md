# 04 - Longest Common Subsequence (LCS) DP Pattern

> **Core Idea:** Compare two sequences and find the optimal answer by matching or skipping characters/elements.

---

# What is LCS DP?

LCS DP is used when:

- There are **two strings** or **two sequences**.
- We need to compare them.
- We need to find:
  - Longest Common Subsequence
  - Shortest Common Supersequence
  - Edit Distance
  - Matching Characters
  - Minimum Operations
  - Sequence Alignment

The entire pattern is built around:

```
Match

OR

Skip
```

---

# What is a Subsequence?

A subsequence preserves order but may skip elements.

Example:

```
String = "abcdef"
```

Valid subsequences:

```
abc
ace
bdf
af
```

Invalid:

```
cba
fed
```

because order changes.

---

# Example of LCS

```
text1 = "abcde"

text2 = "ace"
```

Common subsequences:

```
a
c
e
ac
ae
ce
ace
```

Longest:

```
ace
```

Length =

```
3
```

---

# Core Idea

At every position:

```
i in string1

j in string2
```

We compare:

```
s1[i]

s2[j]
```

Two possibilities:

### Case 1

Characters match

```
s1[i] == s2[j]
```

Take both.

```
1 + answer of remaining strings
```

---

### Case 2

Characters don't match

Skip one character.

```
Skip from string1

OR

Skip from string2
```

Take the best answer.

---

# When Should You Think of LCS DP?

Whenever the question contains:

- Two strings
- Two arrays
- Matching sequences
- Common subsequence
- Minimum insertions
- Minimum deletions
- Edit operations
- Palindrome transformation

Immediately ask:

> Can I compare two sequences character by character?

If YES, think LCS DP.

---

# State Definition

Most common:

```
dp[i][j]
```

Meaning:

```
Answer using

s1[0...i-1]

and

s2[0...j-1]
```

---

# Generic Thinking Process

## Step 1

Define

```
dp[i][j]
```

---

## Step 2

Compare characters

```
s1[i-1]

s2[j-1]
```

---

## Step 3

Match

```
1 + dp[i-1][j-1]
```

---

## Step 4

No Match

```
max(
dp[i-1][j],
dp[i][j-1]
)
```

---

## Step 5

Build table

Top → Bottom

Left → Right

---

# LCS Recurrence

If

```
s1[i-1] == s2[j-1]
```

then

```text
dp[i][j]
=
1 + dp[i-1][j-1]
```

Otherwise

```text
dp[i][j]
=
max(
dp[i-1][j],
dp[i][j-1]
)
```

---

# Memoization Template

```java
int solve(int i, int j){

    if(i == 0 || j == 0)
        return 0;

    if(dp[i][j] != -1)
        return dp[i][j];

    if(s1.charAt(i-1) == s2.charAt(j-1)){

        return dp[i][j] =
                1 + solve(i-1, j-1);
    }

    return dp[i][j] =
            Math.max(
                solve(i-1, j),
                solve(i, j-1)
            );
}
```

---

# Tabulation Template

```java
for(int i=1;i<=n;i++){

    for(int j=1;j<=m;j++){

        if(match){

            dp[i][j] =
                1 + dp[i-1][j-1];

        }else{

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

# Space Optimization

Only previous row is needed.

```java
int[] prev = new int[m+1];

for(int i=1;i<=n;i++){

    int[] curr = new int[m+1];

    for(int j=1;j<=m;j++){

        // transition

    }

    prev = curr;
}
```

Space:

```
O(m)
```

instead of

```
O(n*m)
```

---

# Pattern Recognition

Question contains:

```
Two Strings

Two Arrays

Common

Subsequence

Deletion

Insertion

Palindrome

Edit
```

↓

State

```
dp[i][j]
```

↓

Match / Not Match

↓

LCS Recurrence

↓

Memoization

↓

Tabulation

↓

Space Optimization

---

# Competitive Programming Insight

Nearly every string DP problem is derived from:

```
LCS
```

or

```
Edit Distance
```

Mastering LCS unlocks most string DP problems.

---

# Problem 1

## LeetCode 1143 — Longest Common Subsequence

Difficulty

Medium

---

## Core Idea

Find the longest subsequence common to both strings.

---

## State

```
dp[i][j]

LCS length
```

---

## Java Solution

```java
class Solution {

    public int longestCommonSubsequence(
            String text1,
            String text2) {

        int n = text1.length();
        int m = text2.length();

        int[][] dp =
                new int[n+1][m+1];

        for(int i=1;i<=n;i++){

            for(int j=1;j<=m;j++){

                if(text1.charAt(i-1)
                    == text2.charAt(j-1)){

                    dp[i][j] =
                        1 + dp[i-1][j-1];

                }else{

                    dp[i][j] =
                        Math.max(
                            dp[i-1][j],
                            dp[i][j-1]
                        );
                }
            }
        }

        return dp[n][m];
    }
}
```

---

### Time Complexity

```
O(n*m)
```

### Space Complexity

```
O(n*m)
```

---

### Optimization

```
O(m)
```

---

# Problem 2

## LeetCode 583 — Delete Operation for Two Strings

Difficulty

Medium

---

## Core Idea

Convert both strings into their LCS.

Characters outside the LCS must be deleted.

---

## Formula

```text
Answer

=

(n - LCS)

+

(m - LCS)
```

---

## State

Same as LCS.

---

## Java Solution

```java
class Solution {

    public int minDistance(
            String word1,
            String word2) {

        int lcs = getLCS(word1, word2);

        return
            word1.length() - lcs +
            word2.length() - lcs;
    }

    private int getLCS(
            String a,
            String b){

        int n = a.length();
        int m = b.length();

        int[][] dp =
                new int[n+1][m+1];

        for(int i=1;i<=n;i++){

            for(int j=1;j<=m;j++){

                if(a.charAt(i-1)
                        == b.charAt(j-1)){

                    dp[i][j] =
                        1 + dp[i-1][j-1];

                }else{

                    dp[i][j] =
                        Math.max(
                            dp[i-1][j],
                            dp[i][j-1]
                        );
                }
            }
        }

        return dp[n][m];
    }
}
```

---

### Time Complexity

```
O(n*m)
```

### Space Complexity

```
O(n*m)
```

---

# Problem 3

## LeetCode 1312 — Minimum Insertion Steps to Make a String Palindrome

Difficulty

Hard

---

## Core Idea

Find:

```text
Longest Palindromic Subsequence
```

LPS is simply:

```text
LCS(
string,
reverse(string)
)
```

---

## Formula

```text
Minimum Insertions

=

n - LPS
```

---

## State

Standard LCS DP.

---

## Java Solution

```java
class Solution {

    public int minInsertions(String s) {

        String rev =
                new StringBuilder(s)
                        .reverse()
                        .toString();

        int lps = lcs(s, rev);

        return s.length() - lps;
    }

    private int lcs(
            String a,
            String b){

        int n = a.length();
        int m = b.length();

        int[][] dp =
                new int[n+1][m+1];

        for(int i=1;i<=n;i++){

            for(int j=1;j<=m;j++){

                if(a.charAt(i-1)
                        == b.charAt(j-1)){

                    dp[i][j] =
                        1 + dp[i-1][j-1];

                }else{

                    dp[i][j] =
                        Math.max(
                            dp[i-1][j],
                            dp[i][j-1]
                        );
                }
            }
        }

        return dp[n][m];
    }
}
```

---

### Time Complexity

```
O(n²)
```

### Space Complexity

```
O(n²)
```

---

# Common Mistakes

❌ Confusing substring with subsequence.

❌ Using contiguous matching logic.

❌ Wrong indexing (`i-1`, `j-1`).

❌ Forgetting base row and column.

❌ Using greedy matching.

---

# Interview Mental Checklist

- Are there two sequences?
- Is this a match/skip problem?
- Can I define `dp[i][j]`?
- Does matching give `1 + dp[i-1][j-1]`?
- Can I reduce space to `O(m)`?

---

# Pattern Summary

| Feature | Description |
|----------|-------------|
| State | `dp[i][j]` |
| Core Decision | Match / Skip |
| Dimension | 2D |
| Time Complexity | Usually `O(n*m)` |
| Space | `O(n*m)` → `O(m)` |
| Common Topics | LCS, Insertions, Deletions, Palindrome, Edit Operations |

---

# Mastery Checklist

- [ ] Understand subsequence vs substring.
- [ ] Solve Longest Common Subsequence.
- [ ] Derive the recurrence naturally.
- [ ] Convert Memoization → Tabulation.
- [ ] Optimize space.
- [ ] Understand LCS transformations.
- [ ] Solve insertion/deletion/palindrome problems.

---

# LCS Transformation Formulas

## Minimum Deletions

```text
n - LCS
```

---

## Minimum Insertions

```text
n - LPS
```

---

## Longest Palindromic Subsequence

```text
LCS(
string,
reverse(string)
)
```

---

## Delete Operation for Two Strings

```text
(n - LCS)
+
(m - LCS)
```

---

> **Golden Rule:** If a problem compares **two sequences** and asks for matching, transformation, insertion, deletion, or alignment, think **LCS Dynamic Programming** first.