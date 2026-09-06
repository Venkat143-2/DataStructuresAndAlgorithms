# Asymptotic Notations — Foundation

## 1. Who introduced asymptotic notation?

There is **not one single person who introduced all asymptotic notations**.

The historical development happened gradually:

- **Paul Bachmann** — strongly associated with the introduction of **Big-O notation** in number theory in 1894.
- **Edmund Landau** — developed and popularized important asymptotic notation, especially **little-o**, and helped systematize asymptotic analysis.
- **Donald Knuth** — strongly established and popularized **Big-Theta (Θ)** and the modern use of asymptotic notation in computer science and algorithm analysis.

So, for learning purposes:

| Notation | Historical association |
|---|---|
| Big-O, O | Paul Bachmann |
| Little-o, o | Edmund Landau |
| Big-Omega, Ω | Edmund Landau / later development |
| Little-omega, ω | Edmund Landau / later development |
| Big-Theta, Θ | Donald Knuth popularized it in computer science |

> Important: These attributions are historical associations, not the claim that one person independently invented the entire asymptotic family.

---

## 2. What problem led to asymptotic notation?

Asymptotic notation was originally developed for **mathematics and number theory**, not specifically for computer algorithms.

Mathematicians often needed to describe how a function behaves when its input becomes **very large**.

For example:

```text
f(n) = n² + 3n + 10
```

The exact value depends on `n`, but when `n` becomes extremely large, the `n²` term becomes much more important than `3n` and `10`.

Instead of repeatedly writing the complete function, asymptotic notation gives us a compact way to describe its **long-term growth**.

The central question became:

> "As n becomes very large, how does this function grow compared with another function?"

---

## 3. "Why do we need growth? It is just a function. Can't we solve the answer and compare?"

Yes — for a particular value of `n`, we can calculate the exact answer and compare it.

For example, let:

```text
f(n) = n² + 3n + 10
g(n) = 3n + 10
```

At `n = 10`:

```text
f(10) = 140
g(10) = 40
```

So `f(10)` is larger.

But asymptotic analysis asks a different question:

> "What happens as n keeps increasing toward infinity?"

For example:

```text
n = 10
n = 100
n = 1,000
n = 1,000,000
...
```

The important thing is not one particular answer. We want to understand the **relationship between the functions as the input becomes extremely large**.

For these two functions:

```text
n² + 3n + 10
3n + 10
```

the first function eventually grows much faster.

We can see this using a ratio:

```text
(n² + 3n + 10) / (3n + 10)
```

As `n → ∞`, this ratio tends to infinity.

That tells us something stronger than simply saying:

> "`n² + 3n + 10` is larger."

It tells us:

> "`n² + 3n + 10` grows strictly faster than `3n + 10`."

This idea of comparing **long-term growth** is the foundation of asymptotic analysis.

---

## 4. What does "growth" mean?

Growth simply means:

> **How quickly the value of a function increases as its input increases.**

Consider:

```text
f(n) = n
g(n) = n²
h(n) = 2ⁿ
```

As `n` becomes larger:

```text
n       → grows linearly
n²      → grows quadratically
2ⁿ      → grows exponentially
```

For example:

| n | n | n² | 2ⁿ |
|---:|---:|---:|---:|
| 2 | 2 | 4 | 4 |
| 4 | 4 | 16 | 16 |
| 8 | 8 | 64 | 256 |
| 16 | 16 | 256 | 65,536 |

The values themselves are not the main idea.

The important question is:

> **How does each function behave when `n` becomes very large?**

---

## 5. Why don't we just compare exact values?

Because exact values depend on the particular input.

Suppose two algorithms take:

```text
A(n) = 100n
B(n) = n²
```

For small `n`, `100n` can be larger.

But eventually `n²` becomes much larger.

For example:

```text
n = 10

A = 1,000
B = 100
```

Here `A` is larger.

But:

```text
n = 1,000

A = 100,000
B = 1,000,000
```

Now `B` is much larger.

So one finite comparison does not tell us the long-term behavior.

Asymptotic notation lets us describe the behavior as:

```text
n → ∞
```

---

## 6. What are asymptotic notations?

The five standard asymptotic notations used in algorithm analysis are:

| Name | Symbol |
|---|---|
| Big-O | `O` |
| Little-o | `o` |
| Big-Omega | `Ω` |
| Little-omega | `ω` |
| Big-Theta | `Θ` |

We will study each notation separately.

---

## 7. Why are asymptotic notations used for time and space complexity?

Algorithms do not have a fixed running time or memory usage.

Their resource usage depends on the **input size `n`**.

For example, an algorithm might perform:

```text
T(n) = 3n² + 5n + 20
```

operations.

We usually do not care about the exact constants `3`, `5`, and `20`.

We want to understand how the required resources grow when the input becomes large.

The dominant term is:

```text
n²
```

So we describe the growth as:

```text
T(n) = O(n²)
```

Similarly, if an algorithm uses:

```text
S(n) = 4n + 100
```

units of memory, its asymptotic growth is:

```text
S(n) = O(n)
```

Therefore, asymptotic notation gives us a machine-independent way to compare algorithms based mainly on their **growth rate**.

---

## 8. Why do we ignore constants and lower-order terms?

Suppose:

```text
T(n) = 5n² + 100n + 500
```

When `n` becomes extremely large:

```text
n²
```

grows much faster than:

```text
n
```

and the constant:

```text
500
```

does not grow at all.

Therefore, the `n²` term dominates the long-term behavior.

So:

```text
5n² + 100n + 500
```

belongs to the same asymptotic growth class as:

```text
n²
```

and we write:

```text
T(n) = Θ(n²)
```

This does **not** mean the two functions have exactly the same values.

It means they have the same asymptotic order of growth.

---

## 9. What is a bound?

A **bound** gives us a limit on how a function behaves.

There are two basic directions:

### Upper bound

An upper bound says:

> "The function does not grow beyond this rate, up to a constant factor, after some point."

Think:

```text
CEILING
──────────────
       f(n)
```

This is the idea behind **Big-O**.

---

### Lower bound

A lower bound says:

> "The function grows at least this fast, up to a constant factor, after some point."

Think:

```text
       f(n)
──────────────
FLOOR
```

This is the idea behind **Big-Omega**.

---

### Both upper and lower bounds

If a function has both:

```text
upper bound
    ↓
   f(n)
    ↑
lower bound
```

and both bounds have the same growth rate, we have a **tight bound**.

This is the idea behind **Big-Theta**.

---

## 10. What does "asymptotic" mean?

"Asymptotic" means we are interested in behavior as the input becomes **arbitrarily large**.

Mathematically:

```text
n → ∞
```

We are not primarily interested in:

```text
n = 5
n = 10
n = 100
```

individually.

We are interested in the long-term pattern.

That is why asymptotic analysis is useful for algorithms: input sizes can become very large, and we want to know how an algorithm scales.

---

## 11. Does Big-O mean "worst case"?

**No.**

This is an important distinction.

There are two different ideas:

### Case analysis

- Best case
- Average case
- Worst case

### Asymptotic notation

- `O`
- `o`
- `Ω`
- `ω`
- `Θ`

They describe different things.

For example, we might analyze the **worst-case running time** and find:

```text
T(n) = O(n²)
```

But Big-O itself does not mean "worst case."

It means **asymptotic upper bound**.

---

## 12. Does Big-O mean exact equality?

No.

If:

```text
f(n) = O(n²)
```

it does **not** mean:

```text
f(n) = n²
```

It means that eventually `f(n)` can be bounded above by a constant multiple of `n²`.

For example:

```text
f(n) = 5n + 10
```

is:

```text
O(n)
```

because eventually it fits below some constant multiple of `n`.

It is also:

```text
O(n²)
O(n³)
O(2ⁿ)
```

because those are all valid upper bounds.

This shows why Big-O can be a **loose bound**.

---

## 13. Why do we have five different notations?

Because "compare two functions" can mean different things.

We may want to ask:

### 1. Is `f` at most as fast as `g`?

→ **Big-O**

```text
f = O(g)
```

### 2. Is `f` strictly smaller in growth than `g`?

→ **Little-o**

```text
f = o(g)
```

### 3. Is `f` at least as fast as `g`?

→ **Big-Omega**

```text
f = Ω(g)
```

### 4. Is `f` strictly faster than `g`?

→ **Little-omega**

```text
f = ω(g)
```

### 5. Do `f` and `g` grow at the same asymptotic rate?

→ **Big-Theta**

```text
f = Θ(g)
```

We will understand the exact meaning of each one separately.

---

## 14. A very important mental model

Think of asymptotic notation as a language for comparing growth.

Suppose:

```text
f(n) = n² + 3n + 10
g(n) = n
```

Instead of repeatedly saying:

> "`f` becomes larger than `g`, and eventually grows much faster..."

we can use asymptotic notation to describe the relationship precisely.

The five notations give us different ways to express that relationship:

```text
O   → upper bound
o   → strict upper bound
Ω   → lower bound
ω   → strict lower bound
Θ   → tight bound
```

The word **strict** is important for `o` and `ω`.

---

## 15. Big-O's basic mental model

For now, remember Big-O as:

> **A constant-scaled ceiling that eventually contains the function.**

If:

```text
f(n) = O(g(n))
```

we are saying:

```text
f(n) ≤ c · g(n)
```

for sufficiently large `n`, where `c` is some positive constant.

Formally:

```text
There exist constants c > 0 and n₀ > 0
such that

0 ≤ f(n) ≤ c·g(n)

for every n ≥ n₀.
```

The two important pieces are:

- `c` → allows a constant scaling of the comparison function.
- `n₀` → tells us where the asymptotic comparison starts to matter.

---

## 16. Why is there an n₀?

Because asymptotic analysis cares about **eventual behavior**, not what happens for a few small inputs.

A function may behave differently for small `n`, but eventually follow a particular growth relationship.

For example:

```text
5n + 10
```

We can show:

```text
5n + 10 ≤ 6n
```

when:

```text
n ≥ 10
```

Therefore:

```text
5n + 10 = O(n)
```

We do not need the inequality to hold for every tiny value of `n`.

We only need it to hold from some point onward.

---

## 17. Why Big-Theta is different from Big-O

Big-O asks:

> "Can I find an upper ceiling?"

Big-Theta asks:

> "Can I find both a ceiling and a floor with the same growth rate?"

For example:

```text
f(n) = 5n + 10
```

We know:

```text
f(n) = O(n)
```

and also:

```text
f(n) = Ω(n)
```

Therefore:

```text
f(n) = Θ(n)
```

So:

```text
Θ = O + Ω
```

conceptually.

---

## 18. Is there a standard "little-Theta"?

In the standard asymptotic notation family used in algorithm analysis, the usual five are:

```text
O, o, Ω, ω, Θ
```

There is **no universally standard sixth notation called little-Theta** that plays the same role as `o` and `ω`.

The reason is important.

`O` gives a one-sided upper bound:

```text
f ≤ constant × g
```

so it makes sense to strengthen it into a strict upper relationship:

```text
f/g → 0
```

which is little-o.

Similarly, `Ω` gives a one-sided lower bound, and it has strict little-omega.

But `Θ` already gives a **two-sided tight growth relationship**.

So the standard asymptotic family does not need a "little-Theta" counterpart.

A stronger relationship often used in mathematics is:

```text
f(n) ~ g(n)
```

which means:

```text
f(n) / g(n) → 1
```

This is called **asymptotic equivalence**.

---

## 19. Important relationships between the five notations

The basic hierarchy is:

```text
o(g) ⊂ O(g)

ω(g) ⊂ Ω(g)
```

And:

```text
Θ(g) = O(g) ∩ Ω(g)
```

Meaning:

```text
f = Θ(g)

iff

f = O(g)
and
f = Ω(g)
```

So the five notations are not five unrelated concepts.

They are different ways of describing the **relative growth of functions**.

---

## 20. The main idea to remember before studying each notation

Do not start by memorizing formulas.

Start with this question:

> **"When n becomes very large, how does f(n) grow compared with g(n)?"**

Then the notation tells us what kind of relationship exists.

```text
              Compare growth
                    │
        ┌───────────┴───────────┐
        │                       │
     One-sided               Two-sided
        │                       │
   ┌────┴────┐                  Θ
   │         │
 Upper     Lower
   │         │
   O         Ω
   │         │
 strict    strict
   │         │
   o         ω
```

This is the foundation.

Next, study the five notations **one at a time**, starting with Big-O.
