# Big-O Notation — Set 2: Growth, Complexity, and Graphs

> **Questions covered**
>
> 1. Why is Big-O used widely in programming?
> 2. What are time and space complexity?
> 3. How do we draw a graph for one Big-O complexity?
> 4. How do we draw `O(n²)`, `O(n)`, and `O(log n)` on one graph?
> 5. Why does growth matter?
> 6. What is the core meaning of `f(n) = O(g(n))`?

---

# 1. Why Is Big-O Used Widely in Programming?

## 1.1 The Basic Problem

When we write a program, we want to know:

* How much time will it need?
* How much memory will it need?
* What happens when the input becomes larger?
* Which algorithm is better?
* Will the program still work efficiently for millions of inputs?

Consider two algorithms.

### Algorithm A

```text
T₁(n) = 10n
```

### Algorithm B

```text
T₂(n) = n²
```

For a small input:

```text
n = 10
```

we get:

```text
T₁(10) = 100
T₂(10) = 100
```

They look similar.

But consider:

```text
n = 1,000,000
```

Then:

```text
T₁(n) = 10,000,000

T₂(n) = 1,000,000,000,000
```

Now the difference is enormous.

The important information is not just the exact number of operations.

The important question is:

> **How does the amount of work grow when the input grows?**

That is why Big-O is extremely useful.

---

# 1.2 Big-O Gives Us a Common Language

Instead of saying:

```text
"This algorithm performs approximately 10n + 50 operations."
```

we can communicate its asymptotic growth as:

```text
O(n)
```

Another algorithm might be:

```text
O(n²)
```

Another:

```text
O(log n)
```

Now programmers can immediately understand their general scalability.

```text
O(log n)    → very slow growth
O(n)        → linear growth
O(n²)       → quadratic growth
```

Big-O therefore became a standard language for discussing algorithm efficiency.

---

# 1.3 Big-O Makes Algorithms Easier to Compare

Suppose:

```text
Algorithm A → O(n)

Algorithm B → O(n²)
```

For sufficiently large input sizes:

```text
O(n)
```

generally scales much better than:

```text
O(n²)
```

So Big-O gives us a high-level comparison.

We don't need to know:

* which CPU was used
* which programming language was used
* the exact clock speed
* the exact number of machine instructions

to understand the fundamental growth behavior.

---

# 1.4 Big-O Is Not Completely Hardware Independent

This point is important.

Big-O removes many machine-specific details from the **growth classification**, but it does not mean hardware is irrelevant.

For example:

```text
Program A → O(n)
Program B → O(n)
```

Program B could still be much slower because it has a much larger constant factor.

For example:

```text
A = 2n
B = 1,000,000n
```

Both are:

```text
O(n)
```

but their real execution times can be very different.

Therefore:

> **Big-O tells us about asymptotic scalability, not exact real-world performance.**

---

# 1.5 Why Big-O Became So Important in Programming

As software started processing larger and larger amounts of data, scalability became extremely important.

Imagine:

```text
10 inputs
100 inputs
1,000 inputs
1,000,000 inputs
1,000,000,000 inputs
```

An algorithm that looks perfectly fine for:

```text
n = 10
```

may become unusable for:

```text
n = 1,000,000
```

Big-O allows programmers to reason about this growth before running the program on enormous data.

---

# 2. Time Complexity

## 2.1 What Is Time Complexity?

Time complexity describes how the **amount of computational work** performed by an algorithm grows as the input size `n` grows.

We usually represent the amount of work using:

```text
T(n)
```

where:

```text
T = time/work
n = input size
```

Then we describe the growth using Big-O.

For example:

```text
T(n) = O(n)
```

means the algorithm's computational work grows linearly with input size.

---

# 2.2 Time Complexity Does Not Mean Exact Seconds

This is a very important distinction.

Suppose:

```text
T(n) = O(n)
```

It does NOT mean:

```text
"The program takes n seconds."
```

It also does not necessarily mean:

```text
"The program performs exactly n operations."
```

It means that the computational work has an asymptotic upper bound that grows like a constant multiple of `n`.

Formally:

```text
T(n) ≤ Cn
```

for sufficiently large `n`.

---

# 2.3 Example: One Loop

Consider:

```python
for i in range(n):
    print(i)
```

The loop runs:

```text
n
```

times.

So:

```text
T(n) = n
```

Therefore:

```text
T(n) = O(n)
```

We call this **linear time complexity**.

---

# 2.4 Example: Nested Loops

Consider:

```python
for i in range(n):
    for j in range(n):
        work()
```

The outer loop runs:

```text
n
```

times.

For every outer iteration, the inner loop runs:

```text
n
```

times.

Therefore:

```text
n × n = n²
```

So:

```text
T(n) = O(n²)
```

This is called **quadratic time complexity**.

---

# 2.5 Example: Logarithmic Time

Consider an algorithm that repeatedly cuts the problem size in half:

```text
n
n/2
n/4
n/8
n/16
...
```

The question becomes:

> How many times can we divide `n` by 2 before reaching 1?

We get:

```text
n / 2ᵏ = 1
```

Therefore:

```text
n = 2ᵏ
```

Taking logarithm:

```text
k = log₂(n)
```

So the number of steps is:

```text
O(log n)
```

This is called **logarithmic time complexity**.

---

# 3. Space Complexity

## 3.1 What Is Space Complexity?

Space complexity describes how the amount of memory required by an algorithm grows as the input size grows.

We can represent memory usage as:

```text
S(n)
```

Then describe its growth using Big-O.

For example:

```text
S(n) = O(n)
```

means memory usage grows linearly with input size.

---

# 3.2 Example: Constant Space

```python
x = 10
y = 20
z = x + y
```

The number of variables does not depend on `n`.

Therefore:

```text
S(n) = O(1)
```

This is constant space.

---

# 3.3 Example: Linear Space

```python
arr = [0] * n
```

The array contains:

```text
n
```

elements.

Therefore:

```text
S(n) = O(n)
```

---

# 3.4 Example: Quadratic Space

Suppose we create an `n × n` matrix:

```text
matrix[n][n]
```

Number of elements:

```text
n × n = n²
```

Therefore:

```text
S(n) = O(n²)
```

---

# 3.5 Time and Space Together

An algorithm can have different time and space complexities.

For example:

```text
Time  → O(n)
Space → O(1)
```

Another algorithm:

```text
Time  → O(n)
Space → O(n)
```

Another:

```text
Time  → O(n²)
Space → O(n)
```

So when analyzing an algorithm, we should ask two separate questions:

```text
1. How does computational work grow?
       ↓
   Time Complexity

2. How does memory usage grow?
       ↓
   Space Complexity
```

---

# 4. How to Draw a Graph for Big-O

## 4.1 What Are We Trying to Draw?

Suppose we want to visualize:

```text
O(n²)
```

Big-O itself is not a specific curve.

Remember:

```text
O(n²)
```

represents a **class of functions** that are eventually bounded above by a constant multiple of `n²`.

For visualization, we normally choose a representative function:

```text
y = n²
```

and draw that curve.

---

# 4.2 The Two Axes

Every graph has two important axes.

### X-axis

Represents:

```text
Input size n
```

### Y-axis

Represents a representative measure of:

```text
Work / operations / growth
```

Therefore:

```text
              Work
                ↑
                │
                │
                │
                │
                │
                └────────────────→ n
                         Input size
```

---

# 4.3 Example: O(n)

For:

```text
O(n)
```

we use the representative function:

```text
y = n
```

Some values:

```text
n     y=n
1      1
2      2
3      3
4      4
5      5
```

Plotting these points produces a straight line.

Conceptually:

```text
Work
  ↑
  │
  │           *
  │        *
  │      *
  │    *
  │  *
  │*
  └────────────────→ n
```

The important feature is:

> The graph grows at a constant rate.

---

# 4.4 Example: O(n²)

For:

```text
O(n²)
```

we use:

```text
y = n²
```

Values:

```text
n     y=n²
1       1
2       4
3       9
4      16
5      25
6      36
```

The graph curves upward because the growth rate itself keeps increasing.

Conceptually:

```text
Work
  ↑
  │
  │              *
  │           *
  │        *
  │      *
  │    *
  │  *
  │ *
  │*
  └────────────────→ n
```

---

# 5. How to Draw O(n²), O(n), and O(log n) in One Graph

Now we can compare three growth rates.

We use representative functions:

```text
O(n²)   → y = n²

O(n)    → y = n

O(log n) → y = log n
```

All three can be placed on the same coordinate system.

---

## 5.1 The Graph

The important visual relationship is:

```text
Growth
  ↑
  │
  │                         n²
  │                       /
  │                    /
  │                 /
  │              /
  │           /
  │        /       n
  │      /       /
  │    /       /
  │  /       /
  │ /      /   log n
  │/______/________________→ n
```

The exact appearance depends on the graph scale, but the fundamental ordering for sufficiently large `n` is:

```text
O(log n) < O(n) < O(n²)
```

---

# 5.2 What Does the Graph Tell Us?

Suppose:

```text
n = 10
```

Representative values:

```text
log₂(10) ≈ 3.32

n = 10

n² = 100
```

So:

```text
log n     → small
n         → medium
n²        → much larger
```

As `n` becomes larger, the difference becomes increasingly dramatic.

---

# 5.3 Why Does O(n²) Eventually Separate So Much?

Compare:

```text
n
```

and:

```text
n²
```

At:

```text
n = 10
```

we have:

```text
n  = 10
n² = 100
```

At:

```text
n = 100
```

we have:

```text
n  = 100
n² = 10,000
```

At:

```text
n = 1,000
```

we have:

```text
n  = 1,000
n² = 1,000,000
```

The quadratic function grows much faster.

---

# 6. Why Does Growth Matter?

This is one of the most important ideas in algorithm analysis.

## 6.1 Small Input Can Hide a Bad Algorithm

Imagine two algorithms:

```text
A → O(n)

B → O(n²)
```

For:

```text
n = 5
```

the difference may be small:

```text
A → 5
B → 25
```

But for:

```text
n = 1,000,000
```

we get:

```text
A → 1,000,000

B → 1,000,000,000,000
```

Now the difference is enormous.

Therefore:

> **An algorithm's growth rate becomes increasingly important as the input size increases.**

---

# 6.2 Growth Is More Important Than One Exact Measurement

Suppose you test two algorithms using:

```text
n = 10
```

and find:

```text
Algorithm A → 1 ms
Algorithm B → 2 ms
```

You might conclude:

```text
A is better.
```

But that does not tell the complete story.

Suppose:

```text
A → O(n²)

B → O(n)
```

For a much larger input, B may eventually become dramatically better.

This is why algorithm analysis studies **growth**, rather than relying only on one benchmark.

---

# 6.3 Growth Determines Scalability

Scalability asks:

> "What happens when the problem becomes much larger?"

Consider:

```text
O(log n)
O(n)
O(n²)
O(2ⁿ)
O(n!)
```

Their growth rates are very different.

A rough ordering for sufficiently large `n` is:

```text
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

The higher-growth algorithms become increasingly expensive as input grows.

---

# 6.4 The Real Question Behind Big-O

When analyzing an algorithm, don't only ask:

> "How fast is it for this input?"

Ask:

> **"How does its resource requirement grow when the input size grows?"**

That is the deeper reason asymptotic analysis matters.

---

# 7. The Core Meaning of `f(n) = O(g(n))`

This is the most important mathematical definition to understand.

We write:

```text
f(n) = O(g(n))
```

when there exist constants:

```text
C > 0
```

and:

```text
n₀ > 0
```

such that:

```text
f(n) ≤ Cg(n)
```

for every:

```text
n ≥ n₀
```

---

# 7.1 Translate It Into English

The mathematical statement:

```text
f(n) = O(g(n))
```

means:

> **There exists a fixed constant C and a threshold n₀ such that, from n₀ onward, f(n) never grows beyond C times g(n).**

This is the mental model you should remember.

---

# 7.2 Visual Meaning

Imagine:

```text
f(n)
```

and:

```text
Cg(n)
```

on a graph.

Big-O says that eventually:

```text
f(n)
```

stays at or below:

```text
Cg(n)
```

Conceptually:

```text
Growth
  ↑
  │
  │                    Cg(n)
  │                  /
  │                /
  │              /
  │      f(n)   /
  │       _____/
  │     /
  │   /
  │__/
  └────────────────────→ n
             ↑
            n₀
```

The important point is:

```text
For n ≥ n₀:

f(n) ≤ Cg(n)
```

---

# 7.3 What Does C Mean?

`C` is a fixed positive constant.

For example:

```text
C = 5
```

Then:

```text
f(n) ≤ 5g(n)
```

eventually.

It does not mean:

```text
C = 5n
```

because then C would grow with n.

The constant must remain constant.

---

# 7.4 What Does n₀ Mean?

`n₀` is the point from which the bound must hold.

For example:

```text
f(n) ≤ 5g(n)
```

may not be true for:

```text
n = 1
n = 2
n = 3
```

but if it becomes true from:

```text
n = 10
```

and stays true afterward, we can choose:

```text
n₀ = 10
```

So:

```text
n₀
```

is simply the threshold for "sufficiently large input."

---

# 7.5 Example

Suppose:

```text
f(n) = 3n + 10
```

We want to show:

```text
f(n) = O(n)
```

We need:

```text
3n + 10 ≤ Cn
```

Choose:

```text
C = 4
```

Then:

```text
3n + 10 ≤ 4n
```

which simplifies to:

```text
10 ≤ n
```

Therefore this is true for:

```text
n ≥ 10
```

So:

```text
C = 4
n₀ = 10
```

and therefore:

```text
3n + 10 = O(n)
```

---

# 7.6 What Big-O Does NOT Mean

If:

```text
f(n) = O(n)
```

it does NOT mean:

```text
f(n) = n
```

It does NOT mean:

```text
f(n) ≤ n
```

It does NOT mean:

```text
f(n) takes exactly n seconds
```

It does NOT mean:

```text
f(n) performs exactly n operations
```

It means:

```text
There exists C > 0 and n₀ > 0

such that

f(n) ≤ Cn

for every n ≥ n₀.
```

---

# 7.7 Why Is Big-O an Upper Bound?

The symbol:

```text
O
```

is used to express an asymptotic upper bound.

For example:

```text
f(n) = O(n²)
```

means that eventually `f(n)` is no larger than some constant multiple of:

```text
n²
```

It does NOT necessarily mean that `n²` is the tightest possible description.

For example:

```text
n = O(n²)
```

is mathematically true.

But the tighter description is:

```text
n = Θ(n)
```

Therefore:

> **Big-O gives an upper bound, but the bound can be loose.**

---

# 8. Big-O and Time/Space Together

We can now connect everything.

## Time

Start with an algorithm.

```text
Algorithm
    ↓
Count computational work
    ↓
Create T(n)
    ↓
Analyze growth
    ↓
T(n) = O(g(n))
```

## Space

Start with an algorithm.

```text
Algorithm
    ↓
Count memory usage
    ↓
Create S(n)
    ↓
Analyze growth
    ↓
S(n) = O(g(n))
```

So Big-O itself is not "time complexity."

Instead:

```text
Big-O
  ↓
Mathematical notation
  ↓
Describes asymptotic growth
```

It can then be applied to:

```text
Time complexity
Space complexity
```

and other resource-growth problems.

---

# 9. The Complete Mental Model

Think of the entire topic as one chain:

```text
Input size
    ↓
Algorithm
    ↓
Resource usage
    ↓
Mathematical function
    ↓
Growth as n becomes large
    ↓
Asymptotic analysis
    ↓
Big-O notation
```

For example:

```text
Input size = n

Algorithm:
    for i in range(n):
        work()

        ↓

Work:
    T(n) = n

        ↓

Growth:
    linear

        ↓

Big-O:
    T(n) = O(n)
```

Another:

```text
Input size = n

Nested loops:

    n × n

        ↓

T(n) = n²

        ↓

Quadratic growth

        ↓

T(n) = O(n²)
```

---

# 10. Quick Revision

## Why is Big-O widely used?

Because it gives programmers a common mathematical language for describing and comparing how algorithms scale as input size grows.

---

## What is time complexity?

The asymptotic growth of an algorithm's computational work as input size increases.

```text
T(n) = O(g(n))
```

---

## What is space complexity?

The asymptotic growth of an algorithm's memory usage as input size increases.

```text
S(n) = O(g(n))
```

---

## How do we graph one complexity?

Choose a representative function.

For:

```text
O(n)
```

use:

```text
y = n
```

For:

```text
O(n²)
```

use:

```text
y = n²
```

Then:

```text
X-axis → input size n

Y-axis → representative work/growth
```

---

## How do we compare three complexities?

Use representative functions:

```text
O(log n) → y = log n

O(n) → y = n

O(n²) → y = n²
```

For sufficiently large `n`:

```text
log n < n < n²
```

---

## Why does growth matter?

Because small input sizes can hide the difference between algorithms.

As input becomes larger, different growth rates can produce enormous differences in required time or memory.

---

## What is the core meaning of `f(n) = O(g(n))`?

```text
f(n) = O(g(n))
```

means:

```text
There exist C > 0 and n₀ > 0

such that

f(n) ≤ Cg(n)

for every n ≥ n₀.
```

### Memorize this sentence:

> **Big-O means that eventually, the function `f(n)` stays at or below some constant multiple of `g(n)`.**

---

# Final Mental Picture

```text
                     BIG-O
                       │
                       ↓
              Asymptotic upper bound
                       │
                       ↓
                 f(n) = O(g(n))
                       │
             ┌─────────┴─────────┐
             ↓                   ↓
       "eventually"        "constant multiple"
             │                   │
            n₀                   C
             │                   │
             └─────────┬─────────┘
                       ↓
                 f(n) ≤ Cg(n)
```

And in DSA:

```text
                    Algorithm
                        │
             ┌──────────┴──────────┐
             ↓                     ↓
           Time                  Space
          T(n)                   S(n)
             │                     │
             └──────────┬──────────┘
                        ↓
                 Asymptotic growth
                        ↓
                     Big-O
```

> **The deepest idea is not memorizing `O(n)`, `O(n²)`, or `O(log n)`. The real skill is learning to look at an algorithm and understand how its resource usage grows as `n` becomes larger.**
