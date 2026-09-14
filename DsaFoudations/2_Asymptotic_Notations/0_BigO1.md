# Big-O Notation — Set 1: Foundation

> **Goal:** Understand where asymptotic notation came from, why Big-O was created, what Big-O actually means, and what guarantee `O(n)`, `O(n²)`, `O(log n)`, etc. provide.

---

# 1. How Did Asymptotic Notations Come Into Mathematics, and How Did They Come Into Time and Space Complexity?

## 1.1 First: What Problem Were Mathematicians Trying to Solve?

Before computer science, mathematicians already studied **functions**.

For example:

```text
f(n) = n
f(n) = n²
f(n) = 2ⁿ
f(n) = log n
```

They wanted to understand questions like:

> "What happens to a function when `n` becomes extremely large?"

For example:

```text
n       n²
10      100
100     10,000
1,000   1,000,000
```

The exact values are not always the most important thing.

The important question is:

> **How fast does the function grow?**

This led mathematics toward the study of **asymptotic behavior**.

---

## 1.2 What Does "Asymptotic" Mean?

Asymptotic analysis is concerned with the behavior of a function as its input becomes very large.

In simple words:

```text
Asymptotic analysis
        ↓
What happens when n → ∞?
        ↓
How does the function grow?
```

For example:

```text
f(n) = n² + 10n + 100
```

When `n` becomes very large:

```text
n²
```

grows much faster than:

```text
10n
```

and:

```text
100
```

Therefore, the `n²` term determines the dominant growth.

So we can describe:

```text
f(n) = O(n²)
```

---

## 1.3 Where Did Big-O Come From?

Big-O notation was originally a **mathematical notation**, not a programming notation.

A major historical milestone was **Paul Bachmann**, who used O-notation in **1894** in mathematical number theory.

The `O` is associated with the German word:

> **Ordnung**

which means approximately:

> **order**

Later mathematicians, especially **Edmund Landau**, helped develop and popularize systematic asymptotic notation.

So:

```text
Mathematics
    ↓
Study of function growth
    ↓
Asymptotic behavior
    ↓
Asymptotic notation
    ↓
Big-O, little-o, Ω, Θ, etc.
```

### Important

Big-O was **not invented specifically for computer algorithms**.

It existed in mathematics before computer science used it.

---

# 1.4 How Did Mathematics Connect to Algorithms?

Now let's move from mathematics to computer science.

Suppose we have this algorithm:

```python
for i in range(n):
    print(i)
```

How much work does it perform?

Approximately:

```text
n iterations
```

So we can describe its work using a mathematical function:

```text
T(n) = n
```

Here:

```text
T(n)
```

means:

> The amount of computational work required for an input of size `n`.

Now mathematics already had tools for studying how functions grow.

Therefore:

```text
Algorithm
    ↓
Count computational work
    ↓
Create a mathematical function T(n)
    ↓
Study how T(n) grows
    ↓
Use asymptotic notation
    ↓
T(n) = O(n)
```

That is the fundamental connection.

---

# 1.5 How Did Time Complexity Come From This?

Consider:

```python
for i in range(n):
    work()
```

The operation:

```text
work()
```

runs approximately `n` times.

Therefore:

```text
T(n) = n
```

We describe its growth as:

```text
T(n) = O(n)
```

This is called its **time complexity**.

But remember:

> `O(n)` does NOT necessarily mean the program takes exactly `n` seconds.

It describes how the amount of computational work grows with input size.

---

# 1.6 How Did Space Complexity Come From This?

The same mathematical idea can be applied to memory.

Suppose:

```python
arr = [0] * n
```

The program creates `n` elements.

Therefore memory usage grows approximately as:

```text
S(n) = n
```

So:

```text
S(n) = O(n)
```

This is its **space complexity**.

Therefore:

```text
Time:
T(n) = O(g(n))

Space:
S(n) = O(g(n))
```

Both use the same mathematical concept.

---

# 1.7 The Complete Evolution

The easiest way to remember the history is:

```text
Mathematics
    │
    │ studied functions
    ↓
Function Growth
    │
    │ "How does f(n) behave as n becomes large?"
    ↓
Asymptotic Analysis
    │
    ↓
Asymptotic Notation
    │
    ├── Big-O
    ├── little-o
    ├── Big-Ω
    ├── little-ω
    └── Big-Θ
         │
         │ adopted by computer science
         ↓
Algorithm Analysis
         │
         ├── Time Complexity
         │
         └── Space Complexity
```

### The key idea

Computer science did not invent the underlying idea of asymptotic growth.

It **applied mathematical asymptotic analysis to functions that describe algorithmic resources**.

---

# 2. Who Invented Big-O?

## Short Answer

**Paul Bachmann** is generally credited with introducing Big-O notation in **1894**.

It appeared in his work on number theory.

The notation was later developed and popularized through the work of mathematicians such as **Edmund Landau**.

---

## 2.1 Was Big-O Invented by Computer Scientists?

No.

Big-O was a mathematical idea before modern computer science existed.

The historical sequence is approximately:

```text
Paul Bachmann
     ↓
O-notation
     ↓
Edmund Landau and later mathematicians
     ↓
Asymptotic notation becomes widely used
     ↓
Computer science adopts it
     ↓
Algorithm analysis
```

---

## 2.2 Why Is Landau Also Frequently Mentioned?

You may see websites saying:

> "Landau invented Big-O."

This can be misleading.

A better historical understanding is:

* **Paul Bachmann** introduced O-notation in 1894.
* **Edmund Landau** later adopted and systematized asymptotic notation.
* Landau is particularly associated with **little-o notation** and the development of asymptotic analysis.

Therefore:

> **Bachmann is credited with introducing Big-O; Landau played an important role in developing and popularizing asymptotic notation.**

---

# 3. What Was the Reason for Inventing Big-O in Functions?

This is one of the most important questions.

The purpose was not:

> "Let's make a complicated notation."

The purpose was to make it easier to describe **growth behavior**.

---

# 3.1 The Problem With Exact Functions

Suppose:

```text
f(n) = 5n² + 20n + 100
```

and another function is:

```text
g(n) = 1000n² + 3n + 50
```

If we only look at the exact formulas, they look very different.

But when `n` becomes extremely large, both are fundamentally dominated by:

```text
n²
```

So we want a way to communicate:

> "These functions have the same fundamental growth order."

Asymptotic notation gives us that language.

Both functions are:

```text
O(n²)
```

and more precisely:

```text
Θ(n²)
```

---

# 3.2 Why Ignore Constants?

Consider:

```text
f(n) = n
g(n) = 1,000,000n
```

The second function is obviously much larger for the same `n`.

But both grow **linearly**.

Graphically:

```text
n
│
│       /
│      /
│     /
│    /
│   /
└──────────── n
```

and:

```text
1,000,000n
│
│        /
│       /
│      /
│     /
│    /
└──────────── n
```

The slopes are different.

But the fundamental growth pattern is the same:

```text
linear growth
```

Therefore:

```text
n = O(n)

1,000,000n = O(n)
```

The constant changes the scale, but not the growth category.

---

# 3.3 Why Ignore Lower-Order Terms?

Consider:

```text
f(n) = n² + 100n + 500
```

For large `n`:

```text
n²
```

eventually dominates:

```text
100n
```

which dominates:

```text
500
```

So:

```text
n² + 100n + 500
```

has quadratic growth.

Therefore:

```text
f(n) = O(n²)
```

and, more tightly:

```text
f(n) = Θ(n²)
```

---

# 3.4 What Big-O Gives Mathematicians

Big-O gives a compact way to say:

> "This function does not grow faster than a particular asymptotic rate, up to a constant factor."

Instead of writing a complicated inequality every time, we can write:

```text
f(n) = O(g(n))
```

That is much easier to communicate.

---

# 3.5 Why Was This Useful for Computer Science?

Now imagine comparing algorithms.

Algorithm A:

```text
T₁(n) = 10n + 100
```

Algorithm B:

```text
T₂(n) = n² + 5n
```

For small inputs, B might sometimes be acceptable.

But as `n` becomes large:

```text
10n
```

grows much more slowly than:

```text
n²
```

So:

```text
Algorithm A → O(n)

Algorithm B → O(n²)
```

This immediately tells us something important about scalability.

That is why asymptotic notation became extremely useful in algorithm analysis.

---

# 4. What Is Big-O?

## 4.1 Simple Definition

> **Big-O notation describes an asymptotic upper bound on the growth of a function.**

In DSA, we commonly use it to describe how an algorithm's:

* time
* memory
* or other resources

grow as input size `n` increases.

---

# 4.2 Formal Definition

We write:

```text
f(n) = O(g(n))
```

if there exist constants:

```text
C > 0
```

and:

```text
n₀ > 0
```

such that:

```text
0 ≤ f(n) ≤ Cg(n)
```

for every:

```text
n ≥ n₀
```

---

# 4.3 The Most Important Mental Translation

Whenever you see:

```text
f(n) = O(g(n))
```

translate it mentally into:

> **"Eventually, f(n) stays at or below some constant multiple of g(n)."**

The word **eventually** is extremely important.

---

# 4.4 Example

Suppose:

```text
f(n) = 3n + 10
```

We want to prove:

```text
f(n) = O(n)
```

We need to find a constant `C` such that:

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

This becomes:

```text
10 ≤ n
```

Therefore it is true whenever:

```text
n ≥ 10
```

So we can choose:

```text
C = 4
n₀ = 10
```

Therefore:

```text
3n + 10 = O(n)
```

---

# 4.5 What Does C Mean?

`C` is a **fixed positive constant**.

It does not grow with `n`.

For example:

```text
C = 4
```

means:

```text
f(n) ≤ 4g(n)
```

eventually.

It does NOT mean that `C` changes for every `n`.

---

# 4.6 What Does n₀ Mean?

`n₀` is the point from which the Big-O bound must hold.

For:

```text
3n + 10 = O(n)
```

we found:

```text
C = 4
n₀ = 10
```

Meaning:

```text
For every n ≥ 10:

3n + 10 ≤ 4n
```

We don't care whether the inequality works for every small value of `n`.

We only need it to work from some point onward.

---

# 4.7 Why Do We Say "Eventually"?

Asymptotic analysis focuses on large inputs.

Suppose:

```text
f(n) = n² + 100n
```

For small values, the `100n` term can be significant.

But as `n` becomes huge:

```text
n²
```

dominates.

So asymptotic analysis asks:

> "What happens when the input becomes sufficiently large?"

This is the meaning of **eventually**.

---

# 4.8 Big-O Is Not Exact Equality

This is a very common misunderstanding.

If:

```text
f(n) = O(n)
```

it does NOT mean:

```text
f(n) = n
```

For example:

```text
f(n) = 100n + 500
```

is:

```text
O(n)
```

even though:

```text
100n + 500 ≠ n
```

Big-O describes a **growth relationship**, not exact equality.

---

# 5. Is Big-O Guaranteed for Time and Space Not to Grow Beyond O(n), O(n²), O(log n), etc.?

## Short Answer

**Yes, but there is an important detail.**

If:

```text
T(n) = O(n)
```

then there exists some constant:

```text
C > 0
```

and some threshold:

```text
n₀ > 0
```

such that:

```text
T(n) ≤ Cn
```

for every:

```text
n ≥ n₀
```

---

# 5.1 This Is the Actual Guarantee

If:

```text
T(n) = O(n)
```

you can say:

```text
T(n) ≤ Cn
```

eventually.

You should **NOT** say:

```text
T(n) ≤ n
```

That is too strong.

You should also **NOT** say:

```text
T(n) ≤ C × O(n)
```

because `O(n)` is not a numerical value.

The correct mathematical statement is:

```text
T(n) ≤ Cn
```

for sufficiently large `n`.

---

# 5.2 Example

Suppose an algorithm performs:

```text
T(n) = 100n + 50
```

Is it:

```text
O(n)?
```

Yes.

Although:

```text
100n + 50
```

is much larger than:

```text
n
```

for many values of `n`, we can choose a constant multiplier.

For example, choose:

```text
C = 101
```

For sufficiently large `n`:

```text
100n + 50 ≤ 101n
```

This requires:

```text
50 ≤ n
```

Therefore:

```text
n ≥ 50
```

So:

```text
T(n) = O(n)
```

---

# 5.3 What About O(n²)?

Suppose:

```text
T(n) = 3n² + 10n + 20
```

We can say:

```text
T(n) = O(n²)
```

because eventually:

```text
T(n) ≤ Cn²
```

for some constant `C`.

The algorithm's actual work can be:

```text
3n² + 10n + 20
```

It does not need to be exactly:

```text
n²
```

---

# 5.4 What About O(log n)?

Suppose:

```text
T(n) = 5log₂(n) + 10
```

Then:

```text
T(n) = O(log n)
```

because there exists some constant `C` such that eventually:

```text
T(n) ≤ C log n
```

Again, it does not mean:

```text
T(n) ≤ log n
```

It means:

```text
T(n) ≤ C log n
```

eventually.

---

# 5.5 The Same Idea Applies to Space

Suppose:

```text
S(n) = 4n + 100
```

Then:

```text
S(n) = O(n)
```

This means:

```text
S(n) ≤ Cn
```

for sufficiently large `n`.

So Big-O can describe both:

```text
Time:
T(n) = O(g(n))

Space:
S(n) = O(g(n))
```

---

# 5.6 But There Is One Important Warning

Do not misunderstand:

```text
O(n)
```

as:

> "The program will never use more than some exact amount of memory/time."

Big-O is an **asymptotic mathematical bound**.

For example:

```text
T(n) = 1,000,000n
```

is still:

```text
O(n)
```

Even though it could be much slower than:

```text
T(n) = n
```

in practice.

So:

```text
Big-O
    ↓
describes growth
    ↓
not exact runtime
    ↓
not exact memory usage
```

---

# 5.7 Another Important Warning: Big-O Can Be Loose

Consider:

```text
f(n) = n
```

It is true that:

```text
f(n) = O(n)
```

But it is also true that:

```text
f(n) = O(n²)
```

because eventually:

```text
n ≤ n²
```

for `n ≥ 1`.

Therefore:

```text
O(n²)
```

is a valid upper bound for a linear function.

But it is not the most informative one.

The tighter description is:

```text
Θ(n)
```

So:

> **Big-O gives an upper bound, but it does not necessarily give the tightest bound.**

---

# 5.8 The Most Important Distinction

When you see:

```text
T(n) = O(n)
```

DO NOT think:

```text
❌ T(n) = n

❌ T(n) ≤ n

❌ Exactly n operations

❌ Exactly n seconds

❌ Big-O always means worst case
```

Think:

```text
✅ There exists C > 0

✅ There exists n₀ > 0

✅ For every n ≥ n₀:

      T(n) ≤ Cn
```

---

# 5.9 Your Mental Model

Remember this:

```text
             Big-O
               │
               ↓
       Asymptotic upper bound
               │
               ↓
       f(n) = O(g(n))
               │
               ↓
     Eventually f(n) ≤ Cg(n)
               │
        ┌──────┴──────┐
        ↓             ↓
       C             n₀
        │             │
   fixed constant   threshold
```

The entire concept can be compressed into one sentence:

> **`f(n) = O(g(n))` means that after some sufficiently large input size `n₀`, the function `f(n)` will never exceed a constant multiple `C` of `g(n)`.**

---

# Quick Revision

## Q1. How did asymptotic notation come into mathematics?

It came from the mathematical study of how functions behave and grow as their inputs become very large.

---

## Q2. How did it enter computer science?

Algorithms produce resource-usage functions such as:

```text
T(n) = time/work
S(n) = memory
```

Mathematical asymptotic notation was then applied to these functions.

---

## Q3. Who invented Big-O?

**Paul Bachmann** introduced O-notation in 1894. Edmund Landau later played an important role in developing and popularizing asymptotic notation.

---

## Q4. Why was Big-O invented?

To describe the **asymptotic growth** of functions compactly without being distracted by exact constants and lower-order details.

---

## Q5. What is Big-O?

> Big-O is an asymptotic upper bound.

Formally:

```text
f(n) = O(g(n))
```

means:

```text
∃ C > 0, ∃ n₀ > 0
such that

f(n) ≤ Cg(n)

for every n ≥ n₀.
```

---

# Final Mental Model

Whenever you see:

```text
O(n)
O(n²)
O(log n)
O(n log n)
```

think:

```text
"What is the growth rate?"
```

not:

```text
"How many exact operations?"
```

And whenever you see:

```text
f(n) = O(g(n))
```

think:

```text
        f(n)
          │
          │ eventually
          ↓
       ≤ Cg(n)
```

That is the heart of Big-O.

---

# One-Line Definition

> **Big-O notation is a mathematical way to express an asymptotic upper bound on how a function grows as its input becomes large. In DSA, it is used to describe how an algorithm's time or space requirements scale with input size.**
