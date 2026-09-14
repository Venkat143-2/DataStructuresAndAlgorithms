# Big-O Notation — Set 4: Purpose, Growth Rates, Code Analysis, and Worked Examples

> **Questions covered**
>
> 1. Why do we use Big-O?
> 2. Big-O is about growth, not only time
> 3. Common growth rates
> 4. How to think about Big-O from code
> 5. Worked examples

---

# 1. Why Do We Use Big-O?

## 1.1 The Problem Big-O Solves

Suppose two programmers create two algorithms for the same problem.

Algorithm A:

```text
T₁(n) = 5n + 20
```

Algorithm B:

```text
T₂(n) = n² + 10
```

If we test both using a small input:

```text
n = 10
```

we get:

```text
T₁(10) = 70
T₂(10) = 110
```

The difference is not very large.

But when:

```text
n = 1,000,000
```

we get approximately:

```text
T₁(n) ≈ 5,000,000

T₂(n) ≈ 1,000,000,000,000
```

Now the difference is enormous.

This leads to the important question:

> **How does an algorithm's resource usage grow when the input becomes larger?**

Big-O gives us a mathematical way to answer this.

---

# 1.2 Big-O Helps Us Study Scalability

**Scalability** means how well an algorithm handles increasing input sizes.

Imagine:

```text
n = 10
n = 100
n = 1,000
n = 10,000
n = 100,000
n = 1,000,000
```

We want to understand what happens to the algorithm as `n` increases.

For example:

```text
O(1)
O(log n)
O(n)
O(n log n)
O(n²)
O(2ⁿ)
O(n!)
```

These have very different growth behaviors.

Big-O lets us classify those behaviors.

---

# 1.3 Big-O Gives Programmers a Common Language

Instead of explaining a complete mathematical function every time, programmers can say:

```text
O(n)
```

and communicate:

> "This algorithm's resource usage grows linearly with the input size."

Or:

```text
O(n²)
```

meaning:

> "This algorithm's resource usage has quadratic growth."

This makes algorithm discussions much easier.

---

# 1.4 Big-O Helps Compare Algorithms

Suppose we have:

```text
Algorithm A → O(log n)

Algorithm B → O(n)

Algorithm C → O(n²)
```

For sufficiently large inputs:

```text
O(log n) < O(n) < O(n²)
```

So we can immediately understand that their scalability is different.

This doesn't automatically mean A is always faster in real life.

Constants, hardware, implementation details, cache behavior, and other factors can matter.

But Big-O tells us about the **asymptotic growth**.

---

# 1.5 Big-O Helps Predict Large-Input Behavior

You may not be able to run an algorithm on:

```text
n = 1,000,000,000
```

just to discover that it is too slow.

Instead, analyze its growth.

For example:

```text
O(n)
```

and:

```text
O(n²)
```

behave very differently as `n` grows.

Therefore:

> **Big-O lets us reason about scalability without having to test every possible input size.**

---

# 1.6 Big-O Reduces Unnecessary Implementation Details

Suppose:

```text
Algorithm A:

T(n) = 3n + 100
```

and:

```text
Algorithm B:

T(n) = 500n + 20
```

Both are:

```text
O(n)
```

The exact constants may matter when optimizing a real program.

But if our question is:

> "What is the asymptotic growth?"

then both are classified as linear.

---

# 1.7 Big-O Is Not Used Only to Say "Fast" or "Slow"

This is a common misunderstanding.

Big-O does not simply mean:

```text
O(n) = fast
O(n²) = slow
```

Instead, Big-O describes:

> **How a function grows as its input becomes large.**

Whether that is acceptable depends on:

* input size
* hardware
* implementation
* constants
* required response time
* memory limits
* application requirements

---

# 2. Big-O Is About Growth, Not Only Time

This distinction is extremely important.

---

# 2.1 Big-O Is Mathematical Notation

Big-O is fundamentally a mathematical notation used to describe asymptotic growth.

It is not itself a unit of time.

For example:

```text
O(n)
```

doesn't mean:

```text
n seconds
```

It means that the relevant function grows no faster than a constant multiple of `n`, eventually.

---

# 2.2 Big-O Can Describe Time

Suppose an algorithm performs:

```text
n
```

units of computational work.

We can write:

```text
T(n) = O(n)
```

where:

```text
T(n)
```

represents computational time/work as a function of input size.

This is called:

> **Time complexity**

---

# 2.3 Big-O Can Describe Space

Suppose an algorithm creates an array containing `n` elements:

```python
arr = [0] * n
```

The memory requirement grows with `n`.

Therefore:

```text
S(n) = O(n)
```

where:

```text
S(n)
```

represents space/memory usage.

This is called:

> **Space complexity**

---

# 2.4 The Same Big-O Can Describe Different Resources

Consider:

```text
T(n) = O(n)
```

This tells us about time if `T(n)` represents time.

But:

```text
S(n) = O(n)
```

tells us about space if `S(n)` represents memory.

So:

```text
             Big-O
                │
       ┌────────┴────────┐
       ↓                 ↓
     Time              Space
     T(n)              S(n)
       │                 │
       ↓                 ↓
   O(g(n))            O(g(n))
```

Big-O is the mathematical notation.

Time and space are the resources being analyzed.

---

# 2.5 Big-O Can Describe Other Things Too

The same mathematical idea can be applied to other quantities.

For example:

```text
Memory usage
Number of operations
Communication cost
Disk operations
Database operations
```

The key requirement is that we have a function whose growth we want to analyze.

Therefore:

> **Big-O is about the growth of a function, not inherently about time.**

---

# 3. Common Growth Rates

Let's build a hierarchy of commonly encountered growth rates.

For sufficiently large `n`, a typical ordering is:

```text
O(1)
   ↓
O(log n)
   ↓
O(n)
   ↓
O(n log n)
   ↓
O(n²)
   ↓
O(n³)
   ↓
O(2ⁿ)
   ↓
O(n!)
```

The lower levels generally grow faster than the levels above them.

---

# 3.1 O(1) — Constant

Representative function:

```text
f(n) = 1
```

The amount of work does not depend on `n`.

Example:

```python
x = arr[0]
```

Assuming array indexing is constant-time:

```text
Time → O(1)
```

Whether the array contains:

```text
10 elements
```

or:

```text
10,000,000 elements
```

the operation is still one array access.

---

# 3.2 O(log n) — Logarithmic

Representative function:

```text
f(n) = log n
```

This commonly appears when the problem size repeatedly shrinks by a constant factor.

Example:

```text
n
n/2
n/4
n/8
n/16
...
```

Binary search is the classic example.

Conceptually:

```text
1000
 ↓ /2
500
 ↓ /2
250
 ↓ /2
125
 ↓ /2
...
```

The number of steps grows logarithmically.

---

# 3.3 O(n) — Linear

Representative function:

```text
f(n) = n
```

The work grows proportionally with the input size.

Example:

```python
for x in arr:
    print(x)
```

If:

```text
len(arr) = n
```

then the loop runs approximately:

```text
n
```

times.

Therefore:

```text
O(n)
```

---

# 3.4 O(n log n) — Linearithmic

Representative function:

```text
f(n) = n log n
```

This commonly appears in efficient comparison-based sorting algorithms.

Examples include:

```text
Merge Sort → O(n log n)
Heap Sort  → O(n log n)
```

It grows faster than:

```text
O(n)
```

but slower than:

```text
O(n²)
```

for sufficiently large `n`.

---

# 3.5 O(n²) — Quadratic

Representative function:

```text
f(n) = n²
```

A common source is nested loops.

Example:

```python
for i in range(n):
    for j in range(n):
        work()
```

The total number of executions is:

```text
n × n = n²
```

Therefore:

```text
O(n²)
```

---

# 3.6 O(n³) — Cubic

Representative function:

```text
f(n) = n³
```

Three nested loops can produce this.

Example:

```python
for i in range(n):
    for j in range(n):
        for k in range(n):
            work()
```

Number of executions:

```text
n × n × n = n³
```

Therefore:

```text
O(n³)
```

---

# 3.7 O(2ⁿ) — Exponential

Representative function:

```text
f(n) = 2ⁿ
```

This appears in many brute-force algorithms involving subsets or combinations.

For example, the number of subsets of a set containing `n` elements is:

```text
2ⁿ
```

The growth is extremely fast.

Values:

```text
n       2ⁿ
1        2
2        4
3        8
4       16
10    1024
20    1,048,576
30    1,073,741,824
```

---

# 3.8 O(n!) — Factorial

Representative function:

```text
f(n) = n!
```

Factorial growth is extremely fast.

For example:

```text
5!  = 120
10! = 3,628,800
20! = 2,432,902,008,176,640,000
```

Factorial complexity commonly appears in brute-force permutation problems.

---

# 4. How to Think About Big-O From Code

This is one of the most important DSA skills.

Don't memorize:

```text
for loop → O(n)
nested loop → O(n²)
```

only.

Instead learn to ask:

> **How many times does the fundamental work happen as a function of n?**

---

# 4.1 Step 1 — Identify the Input Size

First determine what `n` represents.

Example:

```python
for i in range(n):
    print(i)
```

Here:

```text
n = number of iterations possible
```

But sometimes:

```text
n = length of an array
```

or:

```text
n = number of nodes
```

or:

```text
n = number of characters
```

You must identify what grows.

---

# 4.2 Step 2 — Find the Repeated Work

Look for operations that repeat.

Example:

```python
for i in range(n):
    work()
```

The operation:

```text
work()
```

repeats:

```text
n
```

times.

Therefore:

```text
O(n)
```

---

# 4.3 Step 3 — Count Nested Repetition

Consider:

```python
for i in range(n):
    for j in range(n):
        work()
```

First loop:

```text
n
```

Second loop:

```text
n
```

Together:

```text
n × n = n²
```

Therefore:

```text
O(n²)
```

---

# 4.4 Step 4 — Sequential Blocks Are Added

Consider:

```python
for i in range(n):
    work()

for j in range(n):
    work()
```

First loop:

```text
n
```

Second loop:

```text
n
```

Total:

```text
n + n = 2n
```

Therefore:

```text
O(2n)
```

which simplifies to:

```text
O(n)
```

So:

> **Sequential blocks are added.**

---

# 4.5 Step 5 — Nested Blocks Are Multiplied

Consider:

```python
for i in range(n):
    for j in range(n):
        work()
```

The loops are nested.

Therefore:

```text
n × n = n²
```

So:

```text
O(n²)
```

Remember:

```text
Sequential → Add

Nested → Multiply
```

---

# 4.6 Step 6 — Fixed Loops Are Constants

Consider:

```python
for i in range(n):
    for j in range(100):
        work()
```

The outer loop:

```text
n
```

The inner loop:

```text
100
```

Total:

```text
100n
```

Therefore:

```text
O(100n)
```

which becomes:

```text
O(n)
```

because `100` is a constant.

---

# 4.7 Step 7 — Look for Problem-Size Reduction

Consider:

```text
n
n/2
n/4
n/8
n/16
...
```

The problem size is repeatedly divided.

This suggests:

```text
O(log n)
```

The key observation is:

> **If the input size is repeatedly divided by a constant factor, think logarithm.**

---

# 5. Worked Examples

Now let's apply the thinking process.

---

## Example 1 — One Loop

```python
def example(arr):
    for x in arr:
        print(x)
```

Assume:

```text
n = len(arr)
```

The loop executes:

```text
n
```

times.

Therefore:

```text
Time = O(n)
```

If no additional memory proportional to `n` is created:

```text
Space = O(1)
```

---

# Example 2 — Two Sequential Loops

```python
def example(arr):
    for x in arr:
        print(x)

    for x in arr:
        print(x)
```

First loop:

```text
n
```

Second loop:

```text
n
```

Total:

```text
n + n = 2n
```

Drop the constant:

```text
O(2n) = O(n)
```

Therefore:

```text
Time = O(n)
```

---

# Example 3 — Nested Loops

```python
def example(n):
    for i in range(n):
        for j in range(n):
            print(i, j)
```

Outer loop:

```text
n
```

Inner loop for each outer iteration:

```text
n
```

Total:

```text
n × n = n²
```

Therefore:

```text
Time = O(n²)
```

---

# Example 4 — Nested Loop With Different Sizes

Suppose:

```python
for i in range(n):
    for j in range(m):
        work()
```

The outer loop runs:

```text
n
```

times.

The inner loop runs:

```text
m
```

times for each outer iteration.

Therefore:

```text
T(n,m) = nm
```

So:

```text
Time = O(nm)
```

Do NOT automatically write:

```text
O(n²)
```

unless:

```text
m = n
```

This is an important habit.

---

# Example 5 — Constant Inner Loop

```python
for i in range(n):
    for j in range(10):
        work()
```

Total:

```text
n × 10
```

Therefore:

```text
T(n) = 10n
```

Ignoring the constant:

```text
O(n)
```

---

# Example 6 — Quadratic Plus Linear

```python
for i in range(n):
    for j in range(n):
        work()

for k in range(n):
    work()
```

First part:

```text
n²
```

Second part:

```text
n
```

Total:

```text
n² + n
```

The dominant term is:

```text
n²
```

Therefore:

```text
O(n²)
```

More tightly:

```text
Θ(n²)
```

---

# Example 7 — Three Nested Loops

```python
for i in range(n):
    for j in range(n):
        for k in range(n):
            work()
```

Total:

```text
n × n × n
```

Therefore:

```text
n³
```

So:

```text
Time = O(n³)
```

---

# Example 8 — Logarithmic Loop

Consider:

```python
i = n

while i > 1:
    i = i // 2
```

Values of `i` look like:

```text
n
n/2
n/4
n/8
n/16
...
1
```

The number of iterations is approximately:

```text
log₂(n)
```

Therefore:

```text
Time = O(log n)
```

---

# Example 9 — Linear Inside Logarithmic

Consider:

```python
i = n

while i > 1:
    for j in range(n):
        work()

    i = i // 2
```

The `while` loop runs:

```text
O(log n)
```

times.

Inside each iteration, the `for` loop runs:

```text
O(n)
```

times.

Therefore:

```text
O(n) × O(log n)
```

which gives:

```text
O(n log n)
```

---

# Example 10 — Constant Work

```python
def example(arr):
    x = arr[0]
    y = arr[1]
    z = x + y
    return z
```

There are a fixed number of operations.

The number of operations does not grow with `n`.

Therefore:

```text
Time = O(1)
```

---

# Example 11 — Space Complexity

```python
def example(n):
    arr = [0] * n
    return arr
```

The array stores:

```text
n
```

elements.

Therefore:

```text
Space = O(n)
```

The time needed to create/fill it is also typically:

```text
Time = O(n)
```

So:

```text
Time  → O(n)
Space → O(n)
```

---

# Example 12 — Constant Extra Space

```python
def example(arr):
    total = 0

    for x in arr:
        total += x

    return total
```

The loop processes:

```text
n
```

elements.

Therefore:

```text
Time = O(n)
```

But the algorithm only uses a fixed number of extra variables:

```text
total
x
```

Therefore:

```text
Extra Space = O(1)
```

So:

```text
Time  → O(n)
Space → O(1)
```

---

# 6. A Practical Big-O Analysis Checklist

When you see code, follow this process:

```text
1. What is the input size?
        ↓
2. What operation repeats?
        ↓
3. How many times does it repeat?
        ↓
4. Are repetitions sequential or nested?
        ↓
5. Is the problem size shrinking?
        ↓
6. Write the mathematical function
        ↓
7. Remove constants
        ↓
8. Remove lower-order terms
        ↓
9. State the final Big-O
```

---

# 7. The Most Important Patterns

## Pattern 1 — One loop

```python
for i in range(n):
    work()
```

Result:

```text
O(n)
```

---

## Pattern 2 — Nested loops

```python
for i in range(n):
    for j in range(n):
        work()
```

Result:

```text
O(n²)
```

---

## Pattern 3 — Sequential loops

```python
for i in range(n):
    work()

for j in range(n):
    work()
```

Result:

```text
O(n + n)
= O(2n)
= O(n)
```

---

## Pattern 4 — Halving

```text
n → n/2 → n/4 → n/8 → ...
```

Result:

```text
O(log n)
```

---

## Pattern 5 — Fixed inner loop

```python
for i in range(n):
    for j in range(100):
        work()
```

Result:

```text
O(100n)
= O(n)
```

---

## Pattern 6 — Different input sizes

```python
for i in range(n):
    for j in range(m):
        work()
```

Result:

```text
O(nm)
```

Not automatically:

```text
O(n²)
```

---

# 8. Common Mistakes

## Mistake 1

Thinking:

```text
O(n)
```

means:

> "Exactly n operations."

Wrong.

It means the function is eventually bounded above by a constant multiple of `n`.

---

## Mistake 2

Thinking:

```text
O(n)
```

means:

> "The program takes n seconds."

Wrong.

Big-O describes growth, not a fixed time measurement.

---

## Mistake 3

Thinking Big-O is only for time.

Wrong.

It can describe:

```text
Time → T(n)
Space → S(n)
```

and other resource functions.

---

## Mistake 4

Adding nested loops.

For nested loops, repetitions are usually multiplied.

```text
n × n = n²
```

---

## Mistake 5

Multiplying sequential loops.

Sequential loops are added.

```text
n + n = 2n = O(n)
```

---

## Mistake 6

Ignoring different input variables.

If:

```text
n = array size
m = another input size
```

then:

```text
O(nm)
```

should not automatically become:

```text
O(n²)
```

---

# 9. Final Mental Model

Big-O should not be memorized as a collection of rules.

Instead, develop this thought process:

```text
                CODE
                  ↓
          Identify input size
                  ↓
          Find repeated work
                  ↓
       Count how often it happens
                  ↓
          Build T(n) or S(n)
                  ↓
        Study its growth as n ↑
                  ↓
        Ignore irrelevant constants
        and lower-order terms
                  ↓
             BIG-O
```

For example:

```text
Nested loop
     ↓
n × n
     ↓
n²
     ↓
quadratic growth
     ↓
O(n²)
```

Another:

```text
Halving
     ↓
n → n/2 → n/4 → ...
     ↓
log₂(n) steps
     ↓
O(log n)
```

---

# 10. Final Summary

### Why do we use Big-O?

To describe and compare how an algorithm's resource usage grows as the input size becomes large.

### Is Big-O only about time?

No.

Big-O is mathematical notation for asymptotic growth. It can describe time, space, and other resource functions.

### Common growth rates

```text
O(1)
O(log n)
O(n)
O(n log n)
O(n²)
O(n³)
O(2ⁿ)
O(n!)
```

### How should you analyze code?

Ask:

```text
What grows?
     ↓
How many times does the work repeat?
     ↓
Sequential or nested?
     ↓
Does the input shrink?
     ↓
What function T(n) or S(n) describes it?
     ↓
What is the dominant growth?
     ↓
Big-O
```

---

# Final One-Sentence Mental Model

> **Big-O is a mathematical language for describing how a function's resource usage grows as input size becomes large; in DSA, we use it to analyze time, space, and other resources by turning code into a function such as `T(n)` or `S(n)` and then studying its dominant asymptotic growth.**
