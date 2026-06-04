#  How to Study DSA Problems for Interviews (MNC Level Strategy)

This guide explains how to study every DSA problem in a structured way so that it helps in real interviews (Google, Amazon, Microsoft, etc.).

---

#  1. First Attempt (Struggle Phase)

Before looking at any solution:

- Spend **20–40 minutes** solving it yourself
- Start with brute force approach
- Ask:
  - What is the simplest way to solve this?
  - Can I check all possibilities?

 Even brute force thinking is important in interviews.

---

#  2. Pattern Identification (Most Important Step)

After struggling, identify the pattern:

Ask yourself:

- What is the input type?
  - array / string / tree / graph?
- What is asked?
  - subarray / subsequence / pair / max / min?
- What are constraints?
  - large input → O(n) or O(n log n) required

Then map it to a known pattern:

### Common mappings:
- Subarray + sum → Sliding Window / Prefix Sum
- Next greater/smaller → Monotonic Stack
- Pair in sorted array → Two Pointers
- “At most K” problems → Sliding Window (AtMost K pattern)

👉 This is the core interview skill.

---

#  3. Understand the Optimal Approach

Do NOT just read the solution.

You must understand:

- Why brute force fails?
- What are we optimizing?
- What is removed/reduced?
- Why this data structure works?

### Examples:
- Stack → tracks nearest valid elements
- HashMap → frequency or indexing
- Deque → maintains useful window elements

 If you cannot explain WHY, you don’t understand the solution.

---

#  4. Dry Run (Mandatory Step)

Take a small input and simulate step by step:

- Track pointers / stack / map values
- Write each state change
- Observe how answer evolves

 This builds real understanding.

---

#  5. Re-code Without Help

After understanding:

- Close the solution
- Try coding again from scratch
- If stuck → go back to logic, not code

 Goal: 100% independent implementation

---

#  6. Spaced Revision Rule

Revise the same problem:

- After 1 day
- After 1 week

Check:
- Can I solve it in 10–15 minutes?

If yes → it's learned properly.

---

#  7. Interview Translation Format

For every problem, you should be able to explain:

- Problem type
- Pattern used
- Why that pattern works
- Time & space complexity
- Edge cases

 This is exactly what interviewers evaluate.

---

#  Example Thinking Flow

### Problem: Longest Substring Without Repeating Characters

You should think:

- Pattern: Sliding Window + HashMap
- Why: Need continuous window + uniqueness constraint
- Optimization: store last seen index to avoid rechecking
- Time Complexity: O(n)
- Space Complexity: O(min(n, charset))

---

#  Key Insight (Most Important)

It is NOT about solving 500 problems.

It is about:
- Recognizing patterns quickly
- Explaining clearly
- Adapting to variations of the same problem

---

#  Final Goal

After practice, you should be able to:

- Identify pattern in under 10 seconds
- Explain logic clearly in interview
- Code without hesitation
- Handle variations confidently

---