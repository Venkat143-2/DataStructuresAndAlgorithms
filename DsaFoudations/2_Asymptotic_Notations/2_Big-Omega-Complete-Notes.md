# Big-Ω (Big Omega) — Complete Notes

> **Goal:** Understand Big-Ω from first principles, prove Ω formally, connect it to code, and avoid common mistakes.

---

## 1. What is Big-Ω?

Big-Ω is an **asymptotic lower-bound notation**.

It describes a function that grows **at least as fast as** another function, up to a positive constant factor, for sufficiently large input sizes.

We write:

$$
f(n) \in \Omega(g(n))
$$

Read it as:

> **f(n) is Big-Ω of g(n).**

Informally:

> After some point, `f(n)` does not grow slower than a constant multiple of `g(n)`.

---

# 2. Why Do We Need Big-Ω?

Suppose two algorithms have running times:

$$
T_1(n)=5n+20
$$

and

$$
T_2(n)=n^2+3n+10
$$

Exact operation counts can depend on:

- programming language
- compiler
- hardware
- implementation details
- constant operations

Asymptotic notation lets us focus on how the running time behaves as `n` becomes large.

Big-Ω is useful when we want to describe a **lower bound**.

---

# 3. Formal Definition

We say:

$$
f(n) \in \Omega(g(n))
$$

if there exist constants:

$$
c>0
$$

and

$$
n_0>0
$$

such that:

$$
f(n) \geq c\,g(n)
$$

for every:

$$
n\geq n_0
$$

The complete definition is:

$$
\boxed{
\exists c>0,\exists n_0>0
\text{ such that }
f(n)\geq c\,g(n)
\text{ for all }n\geq n_0
}
$$

---

# 4. Understand Every Part of the Definition

Suppose:

$$
f(n)\in\Omega(g(n))
$$

### `f(n)`

The function we are analyzing.

For algorithms, this is usually the running-time or operation-count function.

### `g(n)`

The function used as the lower bound.

### `c`

A positive constant.

$$
c>0
$$

We only need **one valid positive value** of `c`.

We do not need the largest possible value.

### `n₀`

The point from which the inequality must remain true.

$$
n\geq n_0
$$

The inequality does **not** need to work for every small value of `n`.

### `f(n) ≥ c·g(n)`

This is the most important part.

For sufficiently large `n`, `f(n)` must stay above a positive constant multiple of `g(n)`.

---

# 5. Intuition

Think of:

$$
f(n)\geq c\,g(n)
$$

as:

```text
f(n)
 ↑
 │                 f(n)
 │              /
 │           /
 │        /
 │     /     c·g(n)
 │   /     /
 │ /     /
 └────────────────────→ n
       n₀
```

After `n₀`, `f(n)` must not fall below `c·g(n)`.

The exact behavior before `n₀` does not matter.

---

# 6. Simple Example

Consider:

$$
f(n)=3n+5
$$

We want to prove:

$$
f(n)\in\Omega(n)
$$

We need:

$$
3n+5\geq c n
$$

Choose:

$$
c=1
$$

Then:

$$
3n+5\geq n
$$

which is true for every:

$$
n\geq1
$$

Therefore:

$$
\boxed{3n+5\in\Omega(n)}
$$

One valid choice is:

$$
c=1,\qquad n_0=1
$$

---

# 7. The Standard Proof Pattern

Whenever you need to prove:

$$
f(n)\in\Omega(g(n))
$$

use this structure:

### Step 1 — Identify `f(n)`

Write the function being analyzed.

### Step 2 — Identify `g(n)`

Write the proposed lower bound.

### Step 3 — Choose `c`

Choose any convenient:

$$
c>0
$$

### Step 4 — Find `n₀`

Determine when:

$$
f(n)\geq c\,g(n)
$$

becomes true.

### Step 5 — Prove the inequality

Show:

$$
f(n)\geq c\,g(n)
$$

for every:

$$
n\geq n_0
$$

### Step 6 — Conclude

$$
\boxed{f(n)\in\Omega(g(n))}
$$

---

# 8. Polynomial Functions

For a polynomial:

$$
f(n)=a_kn^k+a_{k-1}n^{k-1}+\cdots+a_1n+a_0
$$

the highest-degree term determines the tight asymptotic growth when its leading coefficient is positive.

For example:

$$
f(n)=5n^3+7n^2+2n+10
$$

The dominant term is:

$$
5n^3
$$

Therefore:

$$
f(n)\in\Theta(n^3)
$$

and consequently:

$$
f(n)\in\Omega(n^3)
$$

---

# 9. Positive Lower-Order Terms

Consider:

$$
f(n)=n^2+4n+7
$$

Since all additional terms are non-negative:

$$
n^2+4n+7\geq n^2
$$

Therefore:

$$
f(n)\in\Omega(n^2)
$$

A valid choice is:

$$
c=1,\qquad n_0=1
$$

---

# 10. Negative Lower-Order Terms

Negative terms require more care.

Consider:

$$
f(n)=n^2-4n
$$

We want:

$$
f(n)\in\Omega(n^2)
$$

Start by factoring:

$$
n^2-4n=n^2\left(1-\frac{4}{n}\right)
$$

We want:

$$
1-\frac{4}{n}\geq\frac12
$$

Therefore:

$$
\frac{4}{n}\leq\frac12
$$

which gives:

$$
n\geq8
$$

Thus, for:

$$
n\geq8
$$

we have:

$$
n^2-4n\geq\frac12n^2
$$

Therefore:

$$
\boxed{n^2-4n\in\Omega(n^2)}
$$

with:

$$
c=\frac12,\qquad n_0=8
$$

---

# 11. Several Negative Terms

Consider:

$$
f(n)=n^3-5n^2-10n
$$

Factor out the dominant term:

$$
f(n)=n^3
\left(
1-\frac5n-\frac{10}{n^2}
\right)
$$

For sufficiently large `n`, the expression inside the parentheses approaches `1`.

Therefore we can choose a positive constant such as:

$$
c=\frac12
$$

once `n` is sufficiently large.

Then:

$$
f(n)\geq\frac12n^3
$$

for all sufficiently large `n`.

Hence:

$$
f(n)\in\Omega(n^3)
$$

The important idea is:

> Negative lower-order terms do not destroy the dominant asymptotic order, but the formal proof must still establish a valid lower bound.

---

# 12. Big-Ω and Logarithmic Functions

Growth comparison:

$$
\log n \ll n
$$

Therefore:

$$
n\in\Omega(\log n)
$$

One way to see this is the ratio:

$$
\frac{n}{\log n}
$$

As `n` approaches infinity:

$$
\frac{n}{\log n}\rightarrow\infty
$$

Therefore:

$$
n\in\Omega(\log n)
$$

Similarly:

$$
n^2\in\Omega(\log n)
$$

and:

$$
n\log n\in\Omega(n)
$$

---

# 13. Big-Ω and Exponential Functions

Exponential functions eventually grow faster than polynomial functions.

For example:

$$
2^n\in\Omega(n^3)
$$

and:

$$
2^n\in\Omega(n\log n)
$$

and:

$$
2^n\in\Omega(\log n)
$$

A useful growth hierarchy is:

$$
\boxed{
\log n
\ll
\sqrt n
\ll
n
\ll
n\log n
\ll
n^2
\ll
n^3
\ll
2^n
\ll
n!
}
$$

This is a useful mental model, not a replacement for proof.

---

# 14. Ratio Method

A useful way to compare two functions is:

$$
\frac{f(n)}{g(n)}
$$

### If:

$$
\lim_{n\to\infty}\frac{f(n)}{g(n)}=\infty
$$

then:

$$
f(n)\in\Omega(g(n))
$$

### If:

$$
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
$$

then:

$$
f(n)\notin\Omega(g(n))
$$

### If:

$$
0<
\lim_{n\to\infty}\frac{f(n)}{g(n)}
<\infty
$$

then:

$$
f(n)\in\Theta(g(n))
$$

---

# 15. Code → Mathematical Function → Big-Ω

The correct workflow is:

```text
CODE
  ↓
COUNT OPERATIONS
  ↓
T(n)
  ↓
Choose g(n)
  ↓
Prove T(n) ≥ c·g(n)
  ↓
T(n) ∈ Ω(g(n))
```

Do not jump directly from code to an Ω answer without understanding the operation count.

---

# 16. Single Loop

```python
for i in range(n):
    print(i)
```

The loop executes `n` times.

Therefore:

$$
T(n)=n
$$

So:

$$
T(n)\in\Omega(n)
$$

In fact:

$$
T(n)\in\Theta(n)
$$

---

# 17. Sequential Loops

```python
for i in range(n):
    print(i)

for j in range(n):
    print(j)
```

First loop:

$$
n
$$

Second loop:

$$
n
$$

Total:

$$
T(n)=n+n=2n
$$

Therefore:

$$
T(n)\in\Theta(n)
$$

and:

$$
T(n)\in\Omega(n)
$$

It is **not** `Ω(n²)`.

---

# 18. Nested Loops

```python
for i in range(n):
    for j in range(n):
        print(i, j)
```

The outer loop executes `n` times.

The inner loop executes `n` times for each outer iteration.

Therefore:

$$
T(n)=n\cdot n=n^2
$$

Hence:

$$
T(n)\in\Theta(n^2)
$$

and:

$$
T(n)\in\Omega(n^2)
$$

---

# 19. Triangular Nested Loop

```python
for i in range(n):
    for j in range(i):
        print(i, j)
```

The inner loop executes:

$$
0+1+2+\cdots+(n-1)
$$

times.

Using:

$$
1+2+\cdots+(n-1)
=
\frac{n(n-1)}2
$$

we get:

$$
T(n)=\frac{n(n-1)}2
$$

Expand:

$$
T(n)=\frac{n^2-n}{2}
$$

Therefore:

$$
T(n)\in\Theta(n^2)
$$

and:

$$
T(n)\in\Omega(n^2)
$$

---

# 20. Doubling Loop

```python
i = 1

while i < n:
    i = i * 2
```

Values of `i`:

```text
1
2
4
8
16
32
...
```

After `k` iterations:

$$
i=2^k
$$

The loop stops when:

$$
2^k\geq n
$$

Taking logarithms:

$$
k\geq\log_2 n
$$

Therefore:

$$
T(n)\in\Theta(\log n)
$$

and:

$$
T(n)\in\Omega(\log n)
$$

---

# 21. Best, Average, and Worst Case

These are different from O, Ω, and Θ.

### Best case

The input requiring the least work.

### Average case

The expected work over a specified input distribution.

### Worst case

The input requiring the most work.

---

## Important misconception

Do **not** memorize:

```text
Big-O   = Worst case
Big-Ω   = Best case
```

That is an oversimplification.

Instead:

```text
Best / Average / Worst
        ↓
Which running-time function?
        ↓
O / Ω / Θ
        ↓
What kind of asymptotic bound?
```

For example:

$$
T_{worst}(n)\in\Omega(n)
$$

is a Big-Ω lower bound on the **worst-case function**.

---

# 22. Linear Search Example

Suppose we search for an element in an array.

### Best case

The target is the first element.

$$
T_{best}(n)=1
$$

Therefore:

$$
T_{best}(n)\in\Theta(1)
$$

### Worst case

The target is the last element or absent.

$$
T_{worst}(n)=n
$$

Therefore:

$$
T_{worst}(n)\in\Theta(n)
$$

### Average case

Under a specified uniform model where the target is equally likely to be in any position:

$$
T_{avg}(n)
=
\frac{1+2+\cdots+n}{n}
$$

$$
=
\frac{n+1}{2}
$$

Therefore:

$$
T_{avg}(n)\in\Theta(n)
$$

---

# 23. Big-O vs Big-Ω vs Big-Θ

## Big-O

Upper bound:

$$
f(n)\leq c\,g(n)
$$

Meaning:

> `f(n)` grows no faster than `g(n)`, up to a constant factor.

---

## Big-Ω

Lower bound:

$$
f(n)\geq c\,g(n)
$$

Meaning:

> `f(n)` grows at least as fast as `g(n)`, up to a constant factor.

---

## Big-Θ

Tight bound:

$$
c_1g(n)\leq f(n)\leq c_2g(n)
$$

Meaning:

> `f(n)` and `g(n)` have the same asymptotic growth rate.

---

# 24. Relationship Between O, Ω, and Θ

If:

$$
f(n)\in\Theta(g(n))
$$

then:

$$
f(n)\in O(g(n))
$$

and:

$$
f(n)\in\Omega(g(n))
$$

So:

```text
              Θ(g(n))
              /     \
             ↓       ↓
          O(g(n))  Ω(g(n))
```

---

# 25. One Function Can Have Many Ω Bounds

Suppose:

$$
f(n)=n^3
$$

Then all of these are true:

$$
f(n)\in\Omega(1)
$$

$$
f(n)\in\Omega(n)
$$

$$
f(n)\in\Omega(n^2)
$$

$$
f(n)\in\Omega(n^3)
$$

But:

$$
f(n)\notin\Omega(n^4)
$$

The tight bound is:

$$
\boxed{f(n)\in\Theta(n^3)}
$$

---

# 26. Common Big-Ω Mistakes

## Mistake 1 — Ω means best case

❌ Wrong.

Ω is a lower-bound notation.

Best/average/worst describes the input case.

---

## Mistake 2 — Ω means exact growth

❌ Wrong.

If:

$$
f(n)\in\Omega(n)
$$

that does not mean:

$$
f(n)=n
$$

Ω only gives a lower bound.

---

## Mistake 3 — Choosing `c = 0`

❌ Invalid.

The definition requires:

$$
c>0
$$

---

## Mistake 4 — Choosing negative `c`

❌ Invalid.

Again:

$$
c>0
$$

---

## Mistake 5 — Forgetting `n₀`

A valid proof must work for every:

$$
n\geq n_0
$$

---

## Mistake 6 — Checking only one value of `n`

Checking `n = 10` does not prove the statement.

You need a general inequality that works for **all** sufficiently large `n`.

---

## Mistake 7 — Using the wrong inequality

Big-Ω requires:

$$
f(n)\geq c\,g(n)
$$

Not:

$$
f(n)\leq c\,g(n)
$$

---

## Mistake 8 — Dropping negative terms blindly

For:

$$
n^2-100n
$$

you cannot immediately claim:

$$
n^2-100n\geq n^2
$$

That inequality is false.

You need a proper lower-bound proof.

---

## Mistake 9 — Thinking nested loops always mean `n²`

Nested loops can have different iteration patterns.

For example:

```python
for i in range(n):
    for j in range(i):
        ...
```

has:

$$
T(n)=\frac{n(n-1)}2
$$

which is still:

$$
\Theta(n^2)
$$

but must be derived correctly.

---

## Mistake 10 — Thinking sequential loops multiply

```python
for i in range(n):
    ...

for j in range(n):
    ...
```

gives:

$$
n+n=2n
$$

not:

$$
n^2
$$

---

# 27. Big-Ω Proof Checklist

Whenever you need to prove:

$$
f(n)\in\Omega(g(n))
$$

use this checklist:

- [ ] Identify `f(n)`
- [ ] Identify `g(n)`
- [ ] Choose `c > 0`
- [ ] Find `n₀ > 0`
- [ ] Prove `f(n) ≥ c·g(n)`
- [ ] Make sure it works for every `n ≥ n₀`
- [ ] State the conclusion

Final form:

$$
\boxed{f(n)\in\Omega(g(n))}
$$

---

# 28. Complete Asymptotic Map

```text
                         ALGORITHM
                             |
                             v
                          T(n)
                             |
              +--------------+--------------+
              |              |              |
              v              v              v
            BEST          AVERAGE         WORST
              |              |              |
              +--------------+--------------+
                             |
                             v
                    ASYMPTOTIC BOUND
                             |
              +--------------+--------------+
              |              |              |
              v              v              v
             O              Ω              Θ
           Upper           Lower           Tight
```

Remember:

> **Best / Average / Worst tells you WHICH running-time function you are analyzing.**

> **O / Ω / Θ tells you HOW you are describing that function asymptotically.**

---

# 29. Quick Memory Table

| Concept | Meaning | Mathematical condition |
|---|---|---|
| Big-O | Upper bound | `f(n) ≤ c·g(n)` |
| Big-Ω | Lower bound | `f(n) ≥ c·g(n)` |
| Big-Θ | Tight bound | `c₁g(n) ≤ f(n) ≤ c₂g(n)` |
| Best case | Minimum work for a given input size | `T_best(n)` |
| Average case | Expected work under a specified distribution | `T_avg(n)` |
| Worst case | Maximum work for a given input size | `T_worst(n)` |

---

# 30. Practice Problems

## Level 1 — True or False

### Q1

$$
n^2+5n+10\in\Omega(n^2)
$$

### Q2

$$
3n+7\in\Omega(n^2)
$$

### Q3

$$
n^3+10n^2\in\Omega(n)
$$

### Q4

$$
\log n\in\Omega(n)
$$

### Q5

$$
2^n\in\Omega(n^5)
$$

---

## Level 2 — Find `c` and `n₀`

### Q6

Prove:

$$
3n+5\in\Omega(n)
$$

Find:

$$
c=?,\qquad n_0=?
$$

### Q7

Prove:

$$
n^2-4n\in\Omega(n^2)
$$

Find:

$$
c=?,\qquad n_0=?
$$

### Q8

Prove:

$$
5n^2-10n+20\in\Omega(n^2)
$$

Find:

$$
c=?,\qquad n_0=?
$$

---

## Level 3 — Code → T(n) → Ω

### Q9

```python
for i in range(n):
    print(i)
```

Find:

1. `T(n)`
2. `g(n)`
3. `c`
4. `n₀`
5. Proof
6. Final Ω result

### Q10

```python
for i in range(n):
    for j in range(n):
        print(i, j)
```

Find:

1. `T(n)`
2. `g(n)`
3. `c`
4. `n₀`
5. Final Ω result

---

## Level 4 — Sequential vs Nested

### Q11

```python
for i in range(n):
    print(i)

for j in range(n):
    print(j)
```

Find:

$$
T(n)=?
$$

Then:

$$
\Theta(?)
$$

and:

$$
\Omega(?)
$$

### Q12

```python
for i in range(n):
    for j in range(i):
        print(i, j)
```

Find:

$$
T(n)=?
$$

Then:

$$
\Theta(?)
$$

and:

$$
\Omega(?)
$$

---

## Level 5 — Logarithmic / Exponential

### Q13

Prove:

$$
n\log n\in\Omega(n)
$$

Use:

$$
\frac{n\log n}{n}
$$

### Q14

Determine whether:

$$
n\in\Omega(n^2)
$$

is true or false.

Use:

$$
\frac{n}{n^2}
$$

### Q15

Determine whether:

$$
2^n\in\Omega(n^3)
$$

is true or false.

Explain the growth relationship.

---

## Level 6 — O / Ω / Θ

### Q16

$$
f(n)=7n^2+3n+100
$$

Find:

$$
O(?),\quad\Omega(?),\quad\Theta(?)
$$

### Q17

$$
f(n)=n^3+n^2+n
$$

Find the tight bound.

### Q18

$$
f(n)=10n+\log n+50
$$

Find:

$$
\Theta(?)
$$

### Q19

$$
f(n)=n^2-100n
$$

Find:

$$
\Theta(?)
$$

Be careful with the negative term.

---

## Level 7 — Tricky

### Q20

Is this true?

$$
n^2\in\Omega(n^3)
$$

Give a mathematical reason.

### Q21

Is this true?

$$
n^3\in\Omega(n^2)
$$

If yes, give a valid `c` and `n₀`.

### Q22

Is this true?

$$
n^2+n\in\Omega(n^2+n^3)
$$

Analyze it carefully.

### Q23

```python
i = 1

while i < n:
    i = i * 2
```

Find:

$$
T(n)=?
$$

Then:

$$
\Theta(?)
$$

and:

$$
\Omega(?)
$$

---

# 31. Final Challenge

Consider:

```python
for i in range(n):
    for j in range(i):
        print(i, j)

for k in range(n):
    print(k)
```

Find:

1. First loop's work
2. Second loop's work
3. Total `T(n)`
4. Simplified `T(n)`
5. Tight bound `Θ(?)`
6. Big-Ω bound
7. Valid `c`
8. Valid `n₀`
9. Complete proof

---

# 32. Final Big-Ω Mental Model

Remember this:

```text
              BIG-Ω
                |
                v
           Lower Bound
                |
                v
       f(n) ≥ c·g(n)
                |
        +-------+-------+
        |               |
      c > 0           n ≥ n₀
        |               |
        +-------+-------+
                |
                v
        Prove for ALL
        sufficiently
        large n
```

### The one sentence to remember

> **`f(n) ∈ Ω(g(n))` means that there exist positive constants `c` and `n₀` such that `f(n) ≥ c·g(n)` for every `n ≥ n₀`.**

---

# Big-Ω Mastery Checklist

- [x] What Big-Ω means
- [x] Why Big-Ω is used
- [x] Formal definition
- [x] `f(n)`, `g(n)`, `c`, `n₀`
- [x] Meaning of sufficiently large `n`
- [x] Direct comparison proofs
- [x] Polynomial functions
- [x] Negative lower-order terms
- [x] Logarithmic functions
- [x] Exponential functions
- [x] Ratio method
- [x] Code → mathematical function → Ω
- [x] Best / average / worst case
- [x] Common mistakes
- [x] Big-O vs Big-Ω vs Big-Θ
- [ ] Complete practice set
- [ ] Final Big-Ω mastery test
