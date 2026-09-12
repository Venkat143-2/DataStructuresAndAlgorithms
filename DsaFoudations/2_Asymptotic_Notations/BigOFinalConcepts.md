# Big-O Notation — Remaining Concepts

This document completes the remaining concepts needed to understand and apply **Big-O notation properly in DSA and programming**.

> **Important:** This document focuses only on Big-O. Other asymptotic notations such as Ω, Θ, little-o, and little-omega are intentionally not discussed here.

---

# Table of Contents

1. [Input Size — What Does n Actually Represent?](#1-input-size--what-does-n-actually-represent)
2. [Multiple Input Variables — n, m, V, E](#2-multiple-input-variables--n-m-v-e)
3. [Logarithms and Why Log Base Is Ignored](#3-logarithms-and-why-log-base-is-ignored)
4. [Best, Average, and Worst Case](#4-best-average-and-worst-case)
5. [Time Complexity vs Operation Counting](#5-time-complexity-vs-operation-counting)
6. [Auxiliary Space vs Total Space](#6-auxiliary-space-vs-total-space)
7. [Amortized Analysis](#7-amortized-analysis)
8. [Sequential and Nested Complexity](#8-sequential-and-nested-complexity)
9. [Dependent Loops](#9-dependent-loops)
10. [Branch-Dependent Complexity](#10-branch-dependent-complexity)
11. [Recursion and Recurrence Basics](#11-recursion-and-recurrence-basics)
12. [Tricky Loop Patterns](#12-tricky-loop-patterns)
13. [Mathematical Summations Useful for Big-O](#13-mathematical-summations-useful-for-big-o)
14. [Common Big-O Analysis Mistakes](#14-common-big-o-analysis-mistakes)
15. [How to Derive Complexity Instead of Memorizing Patterns](#15-how-to-derive-complexity-instead-of-memorizing-patterns)
16. [Final Big-O Checklist](#16-final-big-o-checklist)
17. [Final Mental Model](#17-final-mental-model)

---

# 1. Input Size — What Does n Actually Represent?

One of the most important ideas in Big-O is understanding what the variable `n` actually represents.

Beginners often learn:

> `n` = number of elements.

That is useful for arrays, but it is **not universally true**.

`n` represents the **size of the input relevant to the problem**.

The meaning of input size depends on the problem.

---

## 1.1 Array

Suppose:

```python
arr = [10, 20, 30, 40, 50]
```

There are 5 elements.

So:

```text
n = number of elements
```

If an algorithm scans the entire array:

```text
n elements
↓
n operations
↓
O(n)
```

---

## 1.2 String

For a string:

```text
"hello"
```

the input size is normally its length.

```text
n = length of string
```

For:

```python
for ch in s:
    ...
```

the loop executes approximately `n` times.

Therefore:

```text
O(n)
```

---

## 1.3 Matrix

For a matrix:

```text
n × m
```

there are:

```text
n × m
```

elements.

So if we visit every element:

```text
O(nm)
```

If it is specifically a square matrix:

```text
n × n
```

then:

```text
O(n²)
```

The important point is that `n²` is appropriate because the two dimensions are both represented by `n`.

---

## 1.4 Graph

Graph problems commonly use:

```text
V = number of vertices
E = number of edges
```

For example:

```text
O(V + E)
```

This is more meaningful than simply writing:

```text
O(n)
```

because a graph has two important dimensions.

---

## 1.5 Linked List

For a linked list:

```text
n = number of nodes
```

Traversing all nodes:

```text
O(n)
```

---

## 1.6 Number Problems

This becomes more interesting.

Suppose the input is:

```text
N = 1,000,000
```

Sometimes the relevant input size is not `N` itself.

For algorithms involving the binary representation of a number, the input size can be:

```text
number of bits
```

The number of bits required to represent `N` is approximately:

```text
log₂ N
```

So an algorithm performing one operation per bit may have complexity:

```text
O(log N)
```

This is why you should always ask:

> **What actually grows when the input gets larger?**

---

## 1.7 Input Size Is a Modeling Decision

The most important rule:

> **Before calculating Big-O, define what your input-size variable represents.**

For example:

```text
Array       → n = number of elements
String      → n = string length
Matrix      → n × m dimensions
Graph       → V vertices, E edges
Number      → N may be value; bit-length may be log N
```

Do not blindly write `n`.

---

# 2. Multiple Input Variables — n, m, V, E

Not every problem has one input-size variable.

Sometimes there are several independent quantities.

---

## 2.1 n and m

Consider:

```python
for i in range(n):
    for j in range(m):
        work()
```

The outer loop executes:

```text
n times
```

The inner loop executes:

```text
m times
```

Total:

```text
n × m
```

Therefore:

```text
O(nm)
```

---

## 2.2 Why Not O(n²)?

Because we do not know that:

```text
n = m
```

They may be completely different.

For example:

```text
n = 1,000,000
m = 10
```

Then:

```text
nm = 10,000,000
```

while:

```text
n² = 1,000,000,000,000
```

Those are very different.

So preserve separate variables when the inputs are independent.

---

## 2.3 Graphs: V and E

For graphs:

```text
V = vertices
E = edges
```

A traversal such as BFS or DFS is commonly analyzed as:

```text
O(V + E)
```

because the algorithm may process:

```text
vertices → V
edges    → E
```

The two quantities represent different parts of the input.

---

## 2.4 Different Input Sizes

Consider:

```python
for i in range(n):
    work()

for j in range(m):
    work()
```

Total:

```text
n + m
```

Therefore:

```text
O(n + m)
```

Do not automatically convert this to:

```text
O(n)
```

unless there is a justified relationship between n and m.

---

## 2.5 Rule

When variables represent independent input dimensions:

```text
Keep them separate.
```

Examples:

```text
O(n + m)
O(nm)
O(V + E)
O(VE)
```

Only simplify them when you have a valid relationship between the variables.

---

# 3. Logarithms and Why Log Base Is Ignored

Logarithms appear frequently in algorithm analysis.

The most important thing is understanding **why**.

---

## 3.1 What Is a Logarithm?

Consider:

```text
log₂ 8 = 3
```

because:

```text
2³ = 8
```

Similarly:

```text
log₂ 16 = 4
```

because:

```text
2⁴ = 16
```

A logarithm answers:

> **How many times do we need to multiply the base by itself to reach the number?**

---

## 3.2 Why Does log Appear in Algorithms?

A logarithm commonly appears when the problem size is repeatedly reduced by a constant factor.

For example:

```text
n
n/2
n/4
n/8
n/16
...
1
```

How many divisions by 2 are required?

We need `k` such that:

```text
n / 2ᵏ = 1
```

Therefore:

```text
n = 2ᵏ
```

Taking log₂:

```text
k = log₂ n
```

Therefore:

```text
O(log n)
```

---

## 3.3 Binary Search

Binary search repeatedly cuts the search space approximately in half:

```text
n
↓
n/2
↓
n/4
↓
n/8
↓
...
↓
1
```

Therefore:

```text
O(log n)
```

The important observation is:

> **The input is shrinking multiplicatively, not decreasing by one.**

---

## 3.4 Why Does the Log Base Not Matter in Big-O?

Consider:

```text
log₂ n
log₁₀ n
ln n
```

Using the change-of-base formula:

```text
logₐ n = log_b n / log_b a
```

Therefore:

```text
log₂ n = log₁₀ n / log₁₀ 2
```

`1 / log₁₀ 2` is a fixed constant.

So:

```text
log₂ n
```

and:

```text
log₁₀ n
```

differ only by a constant multiplier.

Therefore their asymptotic growth is classified the same way:

```text
O(log₂ n) = O(log₁₀ n) = O(ln n)
```

Usually we simply write:

```text
O(log n)
```

---

## 3.5 Important Distinction

The base does matter for the **actual numerical value**.

But when classifying asymptotic growth, the base contributes only a constant factor.

So:

```text
Exact calculation → base matters
Big-O classification → base does not matter
```

---

# 4. Best, Average, and Worst Case

Big-O can be used to describe the growth of different cases.

The case and the notation are separate ideas.

The three common cases are:

```text
Best Case
Average Case
Worst Case
```

---

## 4.1 Example — Linear Search

Suppose:

```python
for i in range(n):
    if arr[i] == target:
        return i
```

Consider different inputs.

### Best case

The target is the first element.

```text
1 comparison
```

So:

```text
O(1)
```

---

### Worst case

The target is at the end, or does not exist.

We may inspect all `n` elements.

```text
n comparisons
```

So:

```text
O(n)
```

---

### Average case

If the target is equally likely to occur at any position, the average number of checks is roughly proportional to n.

So:

```text
O(n)
```

---

## 4.2 Why Study Different Cases?

Because the same algorithm can behave very differently depending on the input.

When analyzing an algorithm, always ask:

```text
What happens in the best case?
What happens in the average case?
What happens in the worst case?
```

Then specify which one you are reporting.

---

## 4.3 Important

Do not say:

> "Big-O means worst case."

Instead:

> **Big-O is the notation used to express an asymptotic upper bound. Best, average, and worst case describe which input behavior we are analyzing.**

---

# 5. Time Complexity vs Operation Counting

Before obtaining Big-O, we often need to estimate how much work an algorithm performs.

This is where **operation counting** comes in.

---

## 5.1 What Is an Operation?

Examples:

```text
Assignment
Comparison
Addition
Subtraction
Array access
Function call
```

Suppose:

```python
x = a + b
```

We might approximately count:

```text
1 addition
1 assignment
```

The exact counting model can vary.

---

## 5.2 Why Don't We Count Every CPU Instruction?

Because the goal of algorithm analysis is usually not to predict exact machine execution.

Instead, we want to understand how the work grows.

Suppose:

```text
T(n) = 5n + 20
```

We can classify it as:

```text
O(n)
```

We don't need to know whether the computer performs exactly 5 or 7 low-level instructions for every iteration.

---

## 5.3 Operation Counting as a Bridge

Think:

```text
CODE
 ↓
Count approximate operations
 ↓
Build T(n)
 ↓
Simplify growth
 ↓
Big-O
```

For example:

```python
for i in range(n):
    x += 1
```

Approximately:

```text
n iterations
```

So:

```text
T(n) ≈ n
```

Therefore:

```text
O(n)
```

---

## 5.4 Exact Work vs Asymptotic Classification

These are different goals.

### Exact/approximate operation count

```text
T(n) = 3n + 2
```

### Asymptotic classification

```text
O(n)
```

The first contains more detail.

The second focuses on growth.

---

# 6. Auxiliary Space vs Total Space

Space complexity can also be misunderstood.

There are two useful ideas:

```text
Total space
Auxiliary space
```

---

## 6.1 Total Space

Total space can include:

```text
Input data
+
Extra memory used by algorithm
```

Suppose:

```python
arr = [1, 2, 3, ..., n]
```

The input itself requires:

```text
O(n)
```

memory.

If the algorithm also creates another array of size n:

```text
O(n)
```

extra memory.

Total memory is still:

```text
O(n)
```

because:

```text
n + n = 2n
```

and the growth is linear.

---

## 6.2 Auxiliary Space

Auxiliary space means the **extra memory used by the algorithm apart from the input itself**.

Example:

```python
def sum_array(arr):
    total = 0

    for x in arr:
        total += x

    return total
```

The input array contains n elements:

```text
Input space → O(n)
```

But the algorithm only creates:

```text
total
x
```

a fixed number of variables.

Therefore:

```text
Auxiliary space → O(1)
```

---

## 6.3 Why This Distinction Matters

Suppose someone says:

> "The sum algorithm uses O(n) space."

That could mean they are counting the input.

But usually, when discussing algorithm efficiency, we care about:

```text
Extra/Auxiliary space
```

which is:

```text
O(1)
```

So always clarify whether you mean:

```text
Total space
```

or:

```text
Auxiliary space
```

---

## 6.4 Recursive Algorithms

Recursion adds another source of space:

```text
Call stack
```

For example:

```python
def f(n):
    if n == 0:
        return

    f(n - 1)
```

There are approximately n active calls.

Therefore the recursion stack requires:

```text
O(n)
```

auxiliary space.

---

# 7. Amortized Analysis

Amortized analysis is an important concept for understanding operations whose cost changes over time.

The key idea:

> **An occasional expensive operation can be spread across many cheap operations.**

---

## 7.1 Dynamic Array Example

Consider a dynamic array.

Normally:

```text
append()
```

may be cheap.

But eventually the array becomes full.

The implementation may need to:

```text
1. Allocate a larger array
2. Copy existing elements
3. Insert the new element
```

If there are n existing elements, that particular operation may cost:

```text
O(n)
```

---

## 7.2 Does That Mean Every Append Is O(n)?

No.

Most appends are cheap.

For example:

```text
append → cheap
append → cheap
append → cheap
append → resize → expensive
append → cheap
append → cheap
...
```

The expensive resize happens only occasionally.

Across a long sequence of operations, the total cost can be spread across many operations.

This gives an **amortized O(1)** cost per append for a standard dynamically growing array.

---

## 7.3 Important Mental Model

Do not analyze only one operation when amortized analysis is relevant.

Instead ask:

> **What is the total cost of many operations, and how much does that cost average out to per operation?**

For example:

```text
One expensive operation
        ↓
spread across
        ↓
many cheap operations
        ↓
average cost per operation
        ↓
amortized complexity
```

---

## 7.4 Amortized vs Average Case

These are not the same idea.

### Average-case analysis

Usually asks:

> What is the expected cost over different possible inputs, according to a probability model?

### Amortized analysis

Asks:

> What is the average cost per operation over a sequence of operations, even when some individual operations are expensive?

This distinction becomes important when studying data structures.

---

# 8. Sequential and Nested Complexity

This is one of the most important practical Big-O skills.

---

## 8.1 Sequential Work → Add

Consider:

```python
for i in range(n):
    work()

for j in range(n):
    work()
```

First loop:

```text
O(n)
```

Second loop:

```text
O(n)
```

Together:

```text
O(n) + O(n)
```

```text
= O(2n)
```

```text
= O(n)
```

So:

> **Sequential sections are added.**

---

## 8.2 Different Sizes

```python
for i in range(n):
    work()

for j in range(m):
    work()
```

Complexity:

```text
O(n + m)
```

---

## 8.3 Nested Work → Multiply

Consider:

```python
for i in range(n):
    for j in range(n):
        work()
```

Outer:

```text
n
```

Inner:

```text
n
```

Total:

```text
n × n
```

Therefore:

```text
O(n²)
```

---

## 8.4 Nested With Different Sizes

```python
for i in range(n):
    for j in range(m):
        work()
```

Total:

```text
n × m
```

Therefore:

```text
O(nm)
```

---

## 8.5 Important Rule

Remember:

```text
Sequential → ADD
Nested → MULTIPLY
```

But do not blindly apply this rule.

Always ask:

> **How many times does the inner operation actually execute?**

This becomes especially important with dependent loops.

---

# 9. Dependent Loops

Dependent loops are loops where the number of iterations of one loop depends on another variable.

These are a common source of mistakes.

---

## 9.1 Example

```python
for i in range(n):
    for j in range(i):
        work()
```

The inner loop does not always execute n times.

Let's calculate.

When:

```text
i = 0 → 0 iterations
i = 1 → 1 iteration
i = 2 → 2 iterations
i = 3 → 3 iterations
...
i = n-1 → n-1 iterations
```

Total work:

```text
0 + 1 + 2 + 3 + ... + (n-1)
```

Using the summation formula:

```text
n(n-1)/2
```

Therefore:

```text
O(n²)
```

---

## 9.2 Why Isn't It O(n × n)?

Interestingly, the final answer is O(n²), but the reasoning matters.

We did not simply assume:

```text
n × n
```

We calculated:

```text
0 + 1 + 2 + ... + (n-1)
```

and discovered:

```text
n(n-1)/2
```

which grows quadratically.

This distinction becomes important for more complicated loops.

---

## 9.3 Another Example

```python
for i in range(n):
    for j in range(i, n):
        work()
```

Number of inner iterations:

```text
n + (n-1) + (n-2) + ... + 1
```

Total:

```text
n(n+1)/2
```

Therefore:

```text
O(n²)
```

---

## 9.4 Key Skill

When a loop depends on another variable:

> **Do not immediately multiply the loop bounds. Count the actual number of iterations.**

---

# 10. Branch-Dependent Complexity

Algorithms often contain conditions.

For example:

```python
if condition:
    do_work_n_times()
else:
    do_work_n_squared_times()
```

The branches can have different complexities.

---

## 10.1 Best Case

Suppose:

```text
if condition:
    O(n)
else:
    O(n²)
```

If the first branch executes:

```text
O(n)
```

That can represent the best-case behavior.

---

## 10.2 Worst Case

If the second branch executes:

```text
O(n²)
```

then the worst-case behavior is:

```text
O(n²)
```

---

## 10.3 General Rule

For branches:

```text
if branch A → O(f(n))
else branch B → O(g(n))
```

the case you are analyzing determines which branch behavior matters.

For worst-case analysis, consider the branch with the greatest growth among possible branches.

---

## 10.4 Branches Are Different From Sequential Code

Consider:

```python
if condition:
    O(n)
else:
    O(n²)
```

Only one branch executes.

We do not normally calculate:

```text
O(n + n²)
```

because both branches are not executed.

Instead, identify the behavior of each possible path and analyze the case of interest.

---

# 11. Recursion and Recurrence Basics

Recursion is one of the most important places where Big-O becomes more mathematical.

Instead of counting loops directly, we often describe recursive work using a **recurrence relation**.

---

## 11.1 What Is a Recurrence?

A recurrence describes the running time of a recursive function in terms of smaller inputs.

For example:

```python
def f(n):
    if n <= 1:
        return

    f(n // 2)
```

The function performs:

```text
one recursive call with n/2
```

plus a constant amount of additional work.

We can express this as:

```text
T(n) = T(n/2) + O(1)
```

---

## 11.2 Understanding T(n)

Think of:

```text
T(n)
```

as:

> The total work required for an input of size n.

Then:

```text
T(n/2)
```

means:

> The work required for the smaller problem of size n/2.

---

## 11.3 Example: Halving Recursion

```text
T(n) = T(n/2) + O(1)
```

The input sizes become:

```text
n
n/2
n/4
n/8
...
1
```

Number of levels:

```text
log₂ n
```

Each level performs constant additional work.

Therefore:

```text
O(log n)
```

---

## 11.4 Example: Linear Recursion

Consider:

```python
def f(n):
    if n <= 1:
        return

    f(n - 1)
```

Recurrence:

```text
T(n) = T(n-1) + O(1)
```

The sequence is:

```text
n
n-1
n-2
n-3
...
1
```

Approximately n levels.

Therefore:

```text
O(n)
```

---

## 11.5 Example: Two Recursive Calls

Consider:

```text
T(n) = 2T(n/2) + O(1)
```

There are:

```text
2 calls at level 1
4 calls at level 2
8 calls at level 3
...
```

The recursion tree has approximately n total leaves.

Therefore:

```text
O(n)
```

---

## 11.6 Why Recurrences Matter

Later, algorithms such as:

```text
Merge Sort
Quick Sort
Binary Search
Divide and Conquer algorithms
Tree algorithms
```

will require this way of thinking.

So the important skill is:

> **Turn recursive code into a recurrence before trying to determine its Big-O.**

---

# 12. Tricky Loop Patterns

Some loops cannot be analyzed correctly by simply looking at their syntax.

You need to understand how the loop variable changes.

---

## 12.1 Increasing by 1

```python
for i in range(n):
    work()
```

Values:

```text
0, 1, 2, 3, ..., n-1
```

Number of iterations:

```text
n
```

Complexity:

```text
O(n)
```

---

## 12.2 Increasing by a Constant

```python
for i in range(0, n, 5):
    work()
```

Approximately:

```text
n/5
```

iterations.

Therefore:

```text
O(n)
```

The constant 5 does not change the growth class.

---

## 12.3 Doubling

```python
i = 1

while i < n:
    work()
    i *= 2
```

Values:

```text
1
2
4
8
16
32
...
```

After k iterations:

```text
i = 2ᵏ
```

We need:

```text
2ᵏ ≥ n
```

Therefore:

```text
k ≥ log₂ n
```

Complexity:

```text
O(log n)
```

---

## 12.4 Halving

```python
while n > 1:
    n //= 2
```

Values:

```text
n
n/2
n/4
n/8
...
```

Therefore:

```text
O(log n)
```

---

## 12.5 Multiplication by a Constant

```python
i = 1

while i < n:
    work()
    i *= 3
```

Values:

```text
1
3
9
27
81
...
```

The number of iterations is:

```text
log₃ n
```

Therefore:

```text
O(log n)
```

The base does not affect the asymptotic classification.

---

## 12.6 Square Growth

Consider:

```python
i = 2

while i < n:
    work()
    i *= i
```

Values:

```text
2
4
16
256
65536
...
```

This grows much faster than ordinary doubling.

Let's express it:

```text
i₀ = 2
i₁ = 2²
i₂ = 2⁴
i₃ = 2⁸
i₄ = 2¹⁶
```

After k iterations:

```text
i = 2^(2^k)
```

We need:

```text
2^(2^k) ≥ n
```

Taking logarithms:

```text
2^k ≥ log₂ n
```

Taking logarithms again:

```text
k ≥ log₂(log₂ n)
```

Therefore:

```text
O(log log n)
```

This is an important example because it demonstrates why you should analyze the **actual change of the variable**, rather than memorize loop shapes.

---

## 12.7 Decreasing by 1

```python
i = n

while i > 0:
    work()
    i -= 1
```

Values:

```text
n
n-1
n-2
...
1
```

Therefore:

```text
O(n)
```

---

## 12.8 Two Independent Loops

```python
for i in range(n):
    work()

i = 1
while i < n:
    work()
    i *= 2
```

Complexities:

```text
O(n)
+
O(log n)
```

Total:

```text
O(n + log n)
```

Since n grows faster than log n:

```text
O(n)
```

---

# 13. Mathematical Summations Useful for Big-O

You do not need advanced mathematics to analyze most beginner DSA problems.

But a few formulas are extremely useful.

---

## 13.1 Sum of First n Integers

```text
1 + 2 + 3 + ... + n
```

Formula:

```text
n(n + 1) / 2
```

Growth:

```text
O(n²)
```

---

## 13.2 Why?

Expand:

```text
n(n+1)/2
```

```text
= (n²+n)/2
```

```text
= n²/2 + n/2
```

The dominant growth is:

```text
n²
```

Therefore:

```text
O(n²)
```

---

## 13.3 Sum of Squares

```text
1² + 2² + 3² + ... + n²
```

Formula:

```text
n(n+1)(2n+1)/6
```

Highest power:

```text
n³
```

Therefore:

```text
O(n³)
```

---

## 13.4 Sum of Cubes

```text
1³ + 2³ + ... + n³
```

Formula:

```text
[n(n+1)/2]²
```

Highest power:

```text
n⁴
```

Therefore:

```text
O(n⁴)
```

---

## 13.5 Geometric Series

Consider:

```text
1 + 2 + 4 + 8 + ... + n
```

The sum is proportional to n:

```text
O(n)
```

The final largest term dominates the geometric progression.

---

## 13.6 Harmonic Series

Consider:

```text
1 + 1/2 + 1/3 + ... + 1/n
```

This grows approximately like:

```text
log n
```

Therefore:

```text
O(log n)
```

This appears in some advanced loop analyses.

---

## 13.7 Useful Pattern Table

| Mathematical Pattern      |   Growth |
| ------------------------- | -------: |
| `1 + 1 + ... + 1` n times |     O(n) |
| `1 + 2 + ... + n`         |    O(n²) |
| `1² + 2² + ... + n²`      |    O(n³) |
| `1³ + 2³ + ... + n³`      |    O(n⁴) |
| `1 + 2 + 4 + ... + n`     |     O(n) |
| `1 + 1/2 + ... + 1/n`     | O(log n) |

These formulas become useful when loops generate varying numbers of iterations.

---

# 14. Common Big-O Analysis Mistakes

Even after learning the concepts, several mistakes appear repeatedly.

---

## Mistake 1: Automatically Calling Every Loop O(n)

Not every loop executes n times.

Example:

```python
i = 1
while i < n:
    i *= 2
```

This is:

```text
O(log n)
```

not O(n).

---

## Mistake 2: Automatically Calling Every Nested Loop O(n²)

Consider:

```python
for i in range(n):
    for j in range(i):
        work()
```

The answer happens to be:

```text
O(n²)
```

but you should derive it.

Other nested loops can produce:

```text
O(n log n)
O(nm)
O(n)
O(log n)
```

depending on how the variables change.

---

## Mistake 3: Adding Nested Complexities

Wrong thinking:

```text
O(n) + O(n)
```

for nested loops.

Nested loops represent repeated work:

```text
n × n
```

So:

```text
O(n²)
```

---

## Mistake 4: Multiplying Sequential Complexities

Wrong:

```text
O(n) × O(n)
```

for two independent sequential loops.

Correct:

```text
O(n) + O(n)
= O(n)
```

---

## Mistake 5: Ignoring Different Input Variables

Wrong:

```text
O(n²)
```

for:

```python
for i in range(n):
    for j in range(m):
        work()
```

Correct:

```text
O(nm)
```

when n and m are independent.

---

## Mistake 6: Forgetting the Cost Inside the Loop

Suppose:

```python
for i in range(n):
    binary_search(...)
```

The outer loop is n iterations.

But each binary search costs:

```text
O(log n)
```

So total:

```text
O(n log n)
```

You must analyze the complete body of the loop.

---

## Mistake 7: Ignoring Function Calls

Consider:

```python
for i in range(n):
    expensive_function()
```

You cannot determine the total complexity until you know the complexity of:

```text
expensive_function()
```

If:

```text
expensive_function() → O(n)
```

then:

```text
n calls × O(n)
```

can produce:

```text
O(n²)
```

---

## Mistake 8: Counting Input Space as Extra Space

If an algorithm only uses a few variables while processing an existing array:

```text
Auxiliary space → O(1)
```

even though:

```text
Input itself → O(n)
```

---

## Mistake 9: Thinking Constants Never Matter

For asymptotic classification:

```text
100n → O(n)
```

But in real software:

```text
100n
```

may be significantly slower than:

```text
n
```

Big-O classification and real-world performance are related but not identical.

---

## Mistake 10: Thinking Big-O Gives Exact Runtime

```text
O(n)
```

does not tell you:

```text
10 ms
100 ms
1 second
```

It describes growth.

---

## Mistake 11: Forgetting Early Returns

Consider:

```python
for i in range(n):
    if arr[i] == target:
        return i
```

The algorithm can finish early.

So different cases can have different complexities.

---

## Mistake 12: Blindly Memorizing Patterns

This is perhaps the most dangerous mistake.

Do not memorize:

```text
one loop → O(n)
two loops → O(n²)
```

as universal rules.

Instead ask:

```text
How many times does the actual work execute?
```

---

# 15. How to Derive Complexity Instead of Memorizing Patterns

This is the most important section for becoming good at DSA.

Your goal should not be:

> "I memorized 20 Big-O patterns."

Your goal should be:

> **"Give me unfamiliar code and I can derive its complexity."**

---

## Step 1 — Identify the Input

Ask:

```text
What is the input?
What does n represent?
Are there multiple input sizes?
```

Example:

```text
Array → n
Matrix → n × m
Graph → V, E
```

---

## Step 2 — Find the Basic Work

Ask:

> What operation am I actually trying to count?

For example:

```text
comparison
array access
addition
function call
```

---

## Step 3 — Determine How Many Times It Executes

This is the heart of Big-O analysis.

For:

```python
for i in range(n):
    work()
```

the answer is:

```text
n
```

For:

```python
i = 1
while i < n:
    work()
    i *= 2
```

the answer is:

```text
log n
```

For:

```python
for i in range(n):
    for j in range(i):
        work()
```

the answer requires a summation.

---

## Step 4 — Look at How the Input Changes

Ask:

```text
Does the variable:
    increase by 1?
    increase by a constant?
    double?
    triple?
    halve?
    square itself?
    decrease by 1?
```

This often immediately reveals the growth pattern.

---

## Step 5 — Analyze Sequential Sections

If code does:

```text
A
then
B
then
C
```

calculate:

```text
T(n) = T_A(n) + T_B(n) + T_C(n)
```

Then simplify.

---

## Step 6 — Analyze Nested Sections

If one piece of work occurs inside another:

```text
outer repetitions
×
inner repetitions
```

But only if the repetitions are genuinely independent.

If the inner loop depends on the outer loop, derive the actual count.

---

## Step 7 — Analyze Conditions

For branches:

```text
if A
else B
```

analyze each possible path.

Then decide whether you need:

```text
Best case
Average case
Worst case
```

---

## Step 8 — Analyze Function Calls

Whenever you see:

```python
some_function()
```

ask:

> What is the complexity of this function?

Then include that cost.

---

## Step 9 — For Recursion, Build a Recurrence

Example:

```text
T(n) = T(n/2) + O(1)
```

Then analyze how the problem size changes:

```text
n → n/2 → n/4 → ... → 1
```

---

## Step 10 — Build the Mathematical Expression

You might obtain:

```text
T(n) = 3n² + 10n + 50
```

or:

```text
T(n) = n log n + n
```

or:

```text
T(n) = n + m
```

---

## Step 11 — Simplify for Asymptotic Growth

Remove fixed multiplicative constants:

```text
5n → n
```

Remove slower-growing terms:

```text
n² + n → n²
```

Therefore:

```text
O(n²)
```

---

# A Powerful Example

Consider:

```python
for i in range(n):
    j = 1

    while j < n:
        work()
        j *= 2
```

Do not simply look at the syntax.

Think:

### Outer loop

```text
n iterations
```

### Inner loop

```text
1, 2, 4, 8, ...
```

Therefore:

```text
log n iterations
```

### Combined

For every outer iteration, the inner loop performs log n work.

Therefore:

```text
n × log n
```

Final:

```text
O(n log n)
```

This is the kind of reasoning you should develop.

---

# Another Example — Dependent Loop

```python
for i in range(n):
    for j in range(i):
        work()
```

Don't say:

```text
outer = n
inner = n
therefore n²
```

Instead:

```text
i = 0 → 0
i = 1 → 1
i = 2 → 2
...
i = n-1 → n-1
```

Total:

```text
0 + 1 + 2 + ... + (n-1)
```

```text
= n(n-1)/2
```

Therefore:

```text
O(n²)
```

The final answer is the same, but the reasoning is much stronger.

---

# 16. Final Big-O Checklist

Whenever you analyze an algorithm, run through this checklist.

## Input

```text
□ What is the input?
□ What does n represent?
□ Are there multiple variables?
□ Are the variables independent?
```

---

## Time

```text
□ What basic operation am I counting?
□ How many times does it execute?
□ Are loops sequential?
□ Are loops nested?
□ Are loop bounds dependent?
□ Does the input shrink?
□ Does a variable double/halve?
□ Are there function calls?
□ Is there recursion?
□ Are there branches?
□ Which case am I analyzing?
```

---

## Mathematical Analysis

```text
□ Can I write T(n)?
□ Do I need a summation?
□ Do I need a recurrence?
□ What is the dominant growth?
□ Are there constants?
□ Are there lower-order terms?
```

---

## Space

```text
□ What memory does the input already occupy?
□ What extra memory does the algorithm create?
□ Is there a data structure growing with n?
□ Is recursion using stack space?
□ Am I reporting auxiliary or total space?
```

---

## Final Classification

```text
□ Simplify the mathematical expression
□ State the Big-O
□ Make sure the variables are correct
□ Verify the reasoning
```

---

# 17. Final Mental Model

You should now think about Big-O as a **process**, not a collection of formulas.

```text
                    CODE
                      │
                      ▼
             Identify the input
                      │
                      ▼
             Define input size
                      │
                      ▼
          Find the basic operation
                      │
                      ▼
        Count how often it executes
                      │
            ┌─────────┴─────────┐
            ▼                   ▼
        Sequential            Nested
            │                   │
            ▼                   ▼
           ADD              MULTIPLY
            │                   │
            └─────────┬─────────┘
                      ▼
              Check dependencies
                      │
                      ▼
             Check input changes
                      │
             ┌────────┴────────┐
             ▼                 ▼
         Shrinks?            Recursion?
             │                 │
             ▼                 ▼
          log n             Recurrence
             │                 │
             └────────┬────────┘
                      ▼
               Build T(n)/S(n)
                      │
                      ▼
             Study growth as n ↑
                      │
                      ▼
          Remove fixed constants
                      │
                      ▼
          Remove lower-order terms
                      │
                      ▼
                    BIG-O
```

---

# The Core Questions Your Brain Should Ask

When you see an unfamiliar piece of code, don't immediately ask:

> "Which Big-O pattern is this?"

Instead ask:

### Question 1

> **What is my input size?**

### Question 2

> **What work am I counting?**

### Question 3

> **How many times does that work happen?**

### Question 4

> **Does the number of repetitions depend on another variable?**

### Question 5

> **Does the input decrease or increase multiplicatively?**

### Question 6

> **Are operations sequential or nested?**

### Question 7

> **Are there different branches or recursive calls?**

### Question 8

> **Can I express the total work mathematically?**

### Question 9

> **How does that mathematical function grow as n becomes large?**

### Question 10

> **What Big-O describes that growth?**

That is the real skill.

---

# Big-O From First Principles

The complete chain is:

```text
Problem
   ↓
Algorithm
   ↓
Input size
   ↓
Operations
   ↓
Number of operations
   ↓
Mathematical function
   ↓
Growth as input becomes large
   ↓
Ignore fixed multiplicative constants
   ↓
Ignore slower-growing terms
   ↓
Big-O
```

For example:

```text
Code
 ↓
n outer iterations
 ↓
log n inner iterations
 ↓
n × log n work
 ↓
T(n) = n log n
 ↓
O(n log n)
```

---

# The Most Important Big-O Skills

If you want to become strong at DSA, prioritize these skills:

```text
1. Identify input size
2. Count iterations
3. Understand loop-variable growth
4. Handle nested loops
5. Handle dependent loops
6. Handle multiple input variables
7. Analyze function calls
8. Understand recursion
9. Build summations
10. Build recurrences
11. Analyze space
12. Distinguish different cases
13. Derive instead of memorize
```

---

# Final Big-O Mental Model

> **Big-O is a mathematical way of describing how the resource usage of an algorithm grows as its input size becomes large.**

The process is:

```text
Code
 ↓
What is the input?
 ↓
What does n represent?
 ↓
What work happens?
 ↓
How many times?
 ↓
How does the input change?
 ↓
Sequential / nested / dependent / recursive?
 ↓
Build mathematical expression
 ↓
Study its growth
 ↓
Ignore fixed multiplicative constants
 ↓
Ignore slower-growing terms
 ↓
Big-O
```

And when you get stuck on a DSA problem, remember:

> **Don't guess the Big-O from the shape of the code. Count the actual work.**

That single habit will take you much further than memorizing complexity patterns.

---

# One-Page Big-O Revision

```text
INPUT
────────────────────────────────────
Array       → n elements
String      → n characters
Matrix      → n × m
Graph       → V vertices, E edges
Number      → may depend on value or bit-length


COMMON GROWTH
────────────────────────────────────
O(1)        → constant
O(log n)    → repeated multiplication/division
O(n)        → linear
O(n log n)  → n work across log n levels
O(n²)       → quadratic
O(n³)       → cubic
O(2ⁿ)       → exponential
O(n!)       → factorial


LOOP THINKING
────────────────────────────────────
+1          → usually O(n)
+constant   → usually O(n)
×constant   → O(log n)
÷constant   → O(log n)
dependent   → derive using summation
nested      → determine actual repeated work


COMBINATION
────────────────────────────────────
Sequential → ADD
Nested      → MULTIPLY
Branches    → analyze each path
Recursion   → recurrence


MATHEMATICS
────────────────────────────────────
1 + 2 + ... + n
→ O(n²)

1² + 2² + ... + n²
→ O(n³)

1 + 2 + 4 + ... + n
→ O(n)

1 + 1/2 + ... + 1/n
→ O(log n)


SPACE
────────────────────────────────────
Input space
+
Auxiliary space
=
Total space

Existing input ≠ automatically extra space


ANALYSIS
────────────────────────────────────
Code
 ↓
Input
 ↓
Basic operation
 ↓
Number of executions
 ↓
Mathematical expression
 ↓
Growth
 ↓
Big-O
```

---

# Final Rule

If you remember only one thing:

> **Big-O analysis is not about recognizing a loop pattern. It is about deriving how many times the important work happens and then studying how that quantity grows as the input becomes large.**
