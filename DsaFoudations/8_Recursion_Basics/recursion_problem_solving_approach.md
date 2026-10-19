# Recursion Problem-Solving Guide for Competitive Programming

A practical guide to recognizing recursive structure, deriving a recursive solution, and deciding when recursion needs backtracking, memoization, or a different algorithm.

## Table of Contents

1. [The Most Important Question](#1-the-most-important-question)
2. [How to Recognize Recursive Structure](#2-how-to-recognize-recursive-structure)
3. [The Six-Question Method](#3-the-six-question-method)
4. [Five Common Recursion Patterns](#4-five-common-recursion-patterns)
5. [Derive a Solution from Scratch](#5-derive-a-solution-from-scratch)
6. [Approaching Hard CP Problems](#6-approaching-hard-cp-problems)
7. [Constraints and Complexity](#7-constraints-and-complexity)
8. [Common Mistakes](#8-common-mistakes)
9. [Practice Checklist](#9-practice-checklist)
10. [Quick Reference](#10-quick-reference)

---

## 1. The Most Important Question

Instead of asking:

> “Is this a recursion problem?”

Ask:

> **“Can I solve this problem by solving smaller versions of the same problem?”**

Recursion is a way to express a solution, not a category that every problem belongs to. Many problems can be expressed recursively, but recursion may not be the most efficient or safest implementation.

A correct recursive solution needs a clear definition of the function, a way to reach a base case, and a rule for using smaller states to solve the current state.

---

## 2. How to Recognize Recursive Structure

Look for these five signals. They are clues, not proof that recursion is required.

### Signal 1: A smaller version of the same problem

Can the problem for size `n` be solved using the answer for size `n - 1`?

Examples:
- Processing a sequence one element at a time.
- Computing a value from a smaller input.
- Removing one item and solving the remaining problem.

Ask: **Can I reduce the input while keeping the same problem structure?**

### Signal 2: Multiple choices

Does each step offer choices, such as:
- Include or exclude an element.
- Choose one of several next moves.
- Place one item in one of several positions.

Ask: **Can I make a choice, solve the remaining problem, and then try another choice?**

This often suggests backtracking or search.

### Signal 3: Recursive input structure

Does the input contain smaller structures of the same kind?

Examples:
- Trees and subtrees.
- Nested lists or expressions.
- Divide-and-conquer ranges.

Ask: **Can I solve the smaller parts and then combine their answers?**

### Signal 4: Divide and combine

Can the problem be divided into smaller subproblems, with their results combined into the final answer?

Example: merge sort divides an array into two halves, sorts each half, and merges them.

Ask: **Can I divide the problem, solve each part, and combine the results?**

### Signal 5: Enumerating possibilities

Must you generate all:
- Subsets?
- Permutations?
- Valid strings?
- Paths or arrangements?

Ask: **Can I represent the possibilities as a decision tree and explore its branches?**

### Important caution

A loop, explicit stack, queue, dynamic programming, greedy algorithm, graph algorithm, or mathematical observation may be better. Do not force recursion just because it is possible.

---

## 3. The Six-Question Method

Use these questions before writing code.

### 1. What exactly am I solving?

Define the function in one sentence.

Examples:
- `sum_n(n)` returns the sum from `1` through `n`.
- `solve(i)` processes the sequence starting at index `i`.
- `dfs(node)` explores a graph from `node`.
- `solve(i, target)` determines whether a target can be formed using elements from index `i` onward.

The meaning of the function is its **state definition**.

### 2. What smaller problem can I solve?

Find a smaller input or a next state that moves you toward a simpler problem.

Examples:
- `n` becomes `n - 1`.
- Index `i` becomes `i + 1`.
- An array range becomes two smaller ranges.
- A tree node leads to its children.

### 3. What is the base case?

Identify the smallest state whose answer is known immediately.

Check:
- Is the base case correct?
- Can every valid recursive path reach a base case?
- Are empty, invalid, or impossible states handled where necessary?

### 4. How do I combine the smaller answers?

Depending on the task, you might:
- Add a value.
- Take the minimum or maximum.
- Combine two results.
- Check whether any choice succeeds.
- Count successful choices.
- Collect valid solutions.

### 5. What is the complexity?

Estimate:
- How many states or calls are explored?
- How much work happens per call?
- Are the same states recomputed?
- How deep can the calls become?

A correct solution may still be too slow.

### 6. Which technique fits?

- **Plain recursion:** a straightforward chain of smaller calls.
- **Backtracking:** explore choices and undo state changes to try alternatives.
- **Memoization / DP:** cache answers when the same state appears repeatedly.
- **Divide and conquer:** solve smaller parts and combine their answers.
- **Iteration / explicit stack:** useful when recursion depth or overhead is a concern.

### The workflow to remember

```text
DEFINE
  |
  v
REDUCE
  |
  v
BASE CASE
  |
  v
COMBINE
  |
  v
ANALYZE
  |
  v
OPTIMIZE
```

---

## 4. Five Common Recursion Patterns

These are reusable structures, not complete solutions to every problem.

### Pattern A: Reduce the input

Use when the problem can be reduced to a smaller input of the same kind.

```python
def solve(n):
    if n == 0:
        return

    solve(n - 1)
```

Ask: **Can I solve a smaller input and use its result for the current input?**

### Pattern B: Make multiple choices

Use when each step offers alternatives, such as include/exclude.

```python
def solve(i):
    if i == n:
        return

    # Choice 1: exclude the current element
    solve(i + 1)

    # Choice 2: include the current element
    solve(i + 1)
```

This shows the branching structure only. A complete solution must record the choices and produce the required answer.

Ask: **What decisions are possible at this step?**

### Pattern C: Divide and conquer

Use when a problem can be split into smaller parts and their results combined.

```text
solve(problem)
    |
    +--> solve(left part)
    |
    +--> solve(right part)
    |
    +--> combine both results
```

Example: merge sort.

Ask: **Can I split the problem into smaller parts and combine their answers?**

### Pattern D: Repeated states

Use memoization when the same state is reached repeatedly and its answer can be reused.

```python
def solve(state):
    if state in memo:
        return memo[state]

    # Compute the answer from smaller states.
    # memo[state] = answer
    # return answer
```

Example: Fibonacci with memoization or a dynamic programming problem with overlapping states.

Ask: **Am I solving the same state more than once?**

### Pattern E: Choose, explore, undo

Use backtracking when choices change the current path or shared state.

```text
for each allowed choice:
    make the choice
    explore recursively
    undo the choice
```

Examples: permutations, constrained arrangements, and some path-search problems.

Ask: **After exploring one choice, must I restore the state before trying the next?**

Patterns can overlap. Backtracking can use recursion trees, and a search may need memoization if it reaches the same state repeatedly.

---

## 5. Derive a Solution from Scratch

### Example: Sum of the first `n` positive integers

Problem: For `n = 4`, calculate `1 + 2 + 3 + 4 = 10`.

### Step 1: Define the function

Let `sum_n(n)` mean:

> The sum of all integers from `1` through `n`.

### Step 2: Find the smaller problem

Separate the last number:

\[
1 + 2 + \cdots + n
=
(1 + 2 + \cdots + (n-1)) + n
\]

Therefore:

\[
\operatorname{sum\_n}(n)
=
\operatorname{sum\_n}(n-1) + n
\]

### Step 3: Find the base case

The sum of zero positive integers is zero:

\[
\operatorname{sum\_n}(0)=0
\]

### Step 4: Write the code

```python
def sum_n(n):
    if n == 0:
        return 0

    return sum_n(n - 1) + n

print(sum_n(4))  # 10
```

### Step 5: Trace the calls and returns

```text
sum_n(4) = sum_n(3) + 4
sum_n(3) = sum_n(2) + 3
sum_n(2) = sum_n(1) + 2
sum_n(1) = sum_n(0) + 1
sum_n(0) = 0  <- base case
```

Returning:

```text
sum_n(0) = 0
sum_n(1) = 0 + 1  = 1
sum_n(2) = 1 + 2  = 3
sum_n(3) = 3 + 3  = 6
sum_n(4) = 6 + 4  = 10
```

### What to learn from this example

We derived the solution from:
1. The meaning of the function.
2. A relationship to a smaller problem.
3. A base case whose answer is already known.

**Define what the function means before deciding what its code should be.**

---

## 6. Approaching Hard CP Problems

The hardest part is often finding the right state and making the solution efficient.

### A. Understand the requirements

- Restate the problem in your own words.
- Identify input, output, constraints, and validity rules.
- Work through small examples by hand.
- Look for edge cases.

### B. Define the state

Ask what information uniquely describes the remaining problem.

Possible state components:
- An index.
- A left/right range.
- A remaining target or budget.
- A current graph node.
- A subset of visited nodes.
- A combination of several variables.

Avoid adding parameters without a reason. Every parameter should represent information needed to define the subproblem.

### C. List the transitions

Ask: **From this state, which next states are allowed?**

Examples:
- A sequence may move to the next index.
- A graph traversal may visit an unvisited neighbor.
- A subset generator may include or exclude the current element.
- A divide-and-conquer algorithm may split a range.

### D. Establish correctness

Explain:
- Why every valid possibility is considered.
- Why invalid results are rejected.
- Why each recursive path progresses or terminates.
- Why combining the subproblem results produces the required answer.

### E. Analyze efficiency

A branching search with two choices at each of `n` positions can generate roughly `2^n` leaves. That may be manageable for small `n` but impossible for large `n`.

If the solution is too slow, investigate:
- Pruning branches that cannot lead to a valid answer.
- Memoizing repeated states.
- Dynamic programming.
- Greedy or mathematical properties.
- More efficient data structures or algorithms.

---

## 7. Constraints and Complexity

These are rough clues, not fixed rules. The right algorithm depends on the exact constraints and structure.

| Problem characteristic | What to investigate |
|---|---|
| Small `n`, all possibilities required | Recursion / backtracking |
| Repeated states | Memoization / dynamic programming |
| Independent smaller ranges | Divide and conquer |
| Tree input | DFS or recursive tree processing |
| Graph traversal | DFS recursion or an explicit stack |
| Very deep input | Iteration or an explicit stack |
| Tight time limits | Complexity analysis and stronger algorithms |

### Complexity questions

For every recursive solution, ask:

1. How many calls or distinct states can occur?
2. How many recursive calls can one state make?
3. What work is performed in each call?
4. What is the maximum recursion depth?
5. Can states repeat, and can their answers be cached?

Do not assume that every recursive solution is exponential. Complexity depends on the number of states, branching, repeated work, and work per call.

---

## 8. Common Mistakes

### Mistake 1: Writing code before defining the function

If you cannot explain what `solve(i, target)` means, pause and define its return value or purpose first.

### Mistake 2: Guessing the base case

Derive it from the smallest valid state. Consider empty inputs and impossible states when relevant.

### Mistake 3: Forgetting what a recursive call returns

A call may return a number, Boolean, collection, or no value. Know what the caller needs from it.

### Mistake 4: Confusing the recursion tree and call stack

- **Recursion tree:** the overall branching structure of calls.
- **Call stack:** the active calls along the current execution path.

### Mistake 5: Ignoring complexity

A logically correct solution may be too slow if it explores too many possibilities or recomputes the same states.

### Mistake 6: Forcing recursion

A loop, queue, explicit stack, DP table, greedy algorithm, graph algorithm, or mathematical observation may be more suitable.

---

## 9. Practice Checklist

Use this checklist every time you solve a new problem. Try to answer each item on paper before coding.

- [ ] I understand the problem and have tried a small example.
- [ ] I can describe what my recursive function means in one sentence.
- [ ] I know what each parameter represents.
- [ ] I found a smaller state or listed the possible choices.
- [ ] I identified the base case and why it is correct.
- [ ] I derived the transition or combination rule.
- [ ] I traced calls and returns on a small example.
- [ ] I checked edge cases.
- [ ] I estimated time complexity and maximum recursion depth.
- [ ] I decided whether plain recursion, backtracking, memoization, DP, or another algorithm fits.

### A useful practice routine

1. Spend 10–15 minutes trying to discover the recursive structure.
2. Write the function meaning in plain English.
3. Derive the base case and transitions on paper.
4. Trace a small example.
5. Write the code and analyze its complexity.
6. If stuck, identify which step is blocking you instead of immediately reading the full solution.

Measure progress by how often you can derive the state, base case, and transition without looking at a solution—not simply by how many problems you finish.

---

## 10. Quick Reference

Before coding, write these three lines:

```text
State: What does solve(...) mean?

Base case: When is the answer immediately known?

Transition: How can smaller states solve this state?
```

Then add:

```text
Choices: What next states are allowed?

Complexity: How many states/calls and how much work?

Optimization: Are there repeated states or unnecessary branches?
```

### Three levels of recursion skill

- **Recognize recursion:** spot a smaller subproblem, recursive structure, or decision tree.
- **Derive recursion:** define the state, base case, and transition.
- **Master recursion for CP:** derive a correct solution while controlling time, memory, and complexity.

The central habit is simple:

> **Define → Reduce → Stop → Combine → Analyze → Optimize.**

Build this reasoning habit with small problems first. Then apply it to increasingly difficult competitive-programming problems.
