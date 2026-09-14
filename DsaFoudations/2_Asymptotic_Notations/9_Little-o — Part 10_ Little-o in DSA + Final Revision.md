# Little-o Notation — Part 10: Little-o in DSA + Final Revision

> **Goal:** Connect Little-o notation with DSA and algorithm analysis, understand what it actually tells us about algorithms, and finish with a complete revision of everything learned in Parts 1–10.

---

# 1. From Mathematics to DSA

Little-o notation originally comes from mathematical analysis, where functions are compared according to their growth.

In computer science, we apply the same idea to:

- Time complexity
- Space complexity
- Number of operations
- Input growth
- Algorithm comparison
- Scalability

Suppose two algorithms have running times:

\[
T_1(n)=n\log n
\]

and:

\[
T_2(n)=n^2
\]

We can compare them using:

\[
\frac{T_1(n)}{T_2(n)}
\]

\[
=
\frac{n\log n}{n^2}
\]

\[
=
\frac{\log n}{n}
\]

and:

\[
\frac{\log n}{n}\to0
\]

Therefore:

\[
\boxed{
T_1(n)=o(T_2(n))
}
\]

This means Algorithm 1 grows strictly slower than Algorithm 2.

---

# 2. What Does Little-o Mean for Algorithms?

Suppose:

\[
T_A(n)=o(T_B(n))
\]

This means:

> As the input size becomes extremely large, the running time of Algorithm A becomes negligible compared with the running time of Algorithm B in terms of asymptotic growth.

In simpler words:

\[
\boxed{
A\text{ grows strictly slower than }B
}
\]

This is stronger than merely saying:

\[
T_A=O(T_B)
\]

because Big-O also allows the two algorithms to have the same growth rate.

---

# 3. Example: Linear vs Quadratic

Consider:

### Algorithm A

\[
T_A(n)=n
\]

### Algorithm B

\[
T_B(n)=n^2
\]

Then:

\[
\frac{T_A(n)}{T_B(n)}
=
\frac{n}{n^2}
=
\frac1n
\]

Therefore:

\[
\lim_{n\to\infty}\frac1n=0
\]

So:

\[
\boxed{
T_A=o(T_B)
}
\]

Therefore:

\[
\boxed{
O(n)\text{ grows strictly slower than }O(n^2)
}
\]

More precisely, the functions `n` and `n²` satisfy:

\[
n=o(n^2)
\]

---

# 4. Example: `n log n` vs `n²`

Suppose:

\[
T_A(n)=n\log n
\]

and:

\[
T_B(n)=n^2
\]

Then:

\[
\frac{T_A}{T_B}
=
\frac{n\log n}{n^2}
\]

\[
=
\frac{\log n}{n}
\]

Since:

\[
\frac{\log n}{n}\to0
\]

we get:

\[
\boxed{
n\log n=o(n^2)
}
\]

This is why an `O(n log n)` algorithm has asymptotically better growth than an `O(n²)` algorithm.

---

# 5. Example: Logarithmic vs Linear

Consider:

\[
T_A(n)=\log n
\]

and:

\[
T_B(n)=n
\]

Then:

\[
\frac{\log n}{n}\to0
\]

Therefore:

\[
\boxed{
\log n=o(n)
}
\]

This explains the enormous asymptotic advantage of logarithmic growth over linear growth.

For example, binary search has logarithmic search complexity, while a simple linear search has linear complexity.

---

# 6. Example: Linear vs Exponential

Suppose:

\[
T_A(n)=n
\]

and:

\[
T_B(n)=2^n
\]

Then:

\[
\frac{n}{2^n}\to0
\]

Therefore:

\[
\boxed{
n=o(2^n)
}
\]

So exponential growth eventually dominates linear growth enormously.

---

# 7. Example: Polynomial vs Exponential

Suppose:

\[
T_A(n)=n^{100}
\]

and:

\[
T_B(n)=2^n
\]

Even though:

\[
n^{100}
\]

looks extremely large, we still have:

\[
\boxed{
n^{100}=o(2^n)
}
\]

because every fixed polynomial eventually grows more slowly than an exponential with base greater than `1`.

This is an important lesson:

> **The exponent `100` does not change the growth category from polynomial to exponential.**

---

# 8. Space Complexity

Little-o is not limited to time complexity.

Suppose two algorithms use:

\[
S_A(n)=\log n
\]

and:

\[
S_B(n)=n
\]

Then:

\[
\frac{\log n}{n}\to0
\]

Therefore:

\[
\boxed{
S_A=o(S_B)
}
\]

So Algorithm A's auxiliary-space growth is strictly smaller than Algorithm B's.

---

# 9. Auxiliary Space Example

Suppose:

### Algorithm A

Uses:

\[
O(1)
\]

extra space.

### Algorithm B

Uses:

\[
O(n)
\]

extra space.

The constant function `1` satisfies:

\[
1=o(n)
\]

because:

\[
\frac1n\to0
\]

Therefore:

\[
\boxed{
1=o(n)
}
\]

This means constant extra space is strictly smaller in asymptotic growth than linear extra space.

---

# 10. A Crucial Warning About Big-O

Suppose:

\[
T_A(n)=O(n)
\]

and:

\[
T_B(n)=O(n)
\]

Can we say:

\[
T_A=o(T_B)?
\]

**No.**

Big-O classifications alone are not enough.

Both could be:

\[
\Theta(n)
\]

or one could be smaller.

For example:

\[
T_A(n)=n
\]

\[
T_B(n)=n
\]

Then:

\[
T_A\ne o(T_B)
\]

because:

\[
\frac{n}{n}=1
\]

---

# 11. Complexity Classes vs Exact Functions

This distinction is extremely important.

Suppose someone says:

\[
T_A=O(n)
\]

and:

\[
T_B=O(n^2)
\]

It is tempting to conclude:

\[
T_A=o(T_B)
\]

But strictly speaking, the Big-O statements alone do not establish that exact relationship.

Why?

Because:

\[
T_A=O(n)
\]

only gives an upper bound.

And:

\[
T_B=O(n^2)
\]

also only gives an upper bound.

For example, `T_B` could actually be:

\[
T_B(n)=1
\]

which is also:

\[
O(n^2)
\]

So when making a precise little-o claim, compare the **actual functions** or sufficiently tight asymptotic bounds.

---

# 12. Why Θ Is Often Better for Comparing Algorithms

Suppose:

\[
T_A=\Theta(n)
\]

and:

\[
T_B=\Theta(n^2)
\]

Now we know their actual asymptotic growth classes.

Since:

\[
n=o(n^2)
\]

we can conclude:

\[
\boxed{
T_A=o(T_B)
}
\]

under the usual positive-function setting.

This is one reason Θ is useful when describing a tight asymptotic growth rate.

---

# 13. Little-o and Dominant Terms

Consider an algorithm whose operation count is:

\[
T(n)=3n^2+100n+500
\]

We know:

\[
n=o(n^2)
\]

and:

\[
1=o(n^2)
\]

Therefore:

\[
100n=o(n^2)
\]

and:

\[
500=o(n^2)
\]

So:

\[
T(n)
=
3n^2+o(n^2)
\]

Therefore:

\[
\boxed{
T(n)=\Theta(n^2)
}
\]

Little-o gives a mathematical way to describe why the lower-order terms become negligible.

---

# 14. The Meaning of “Ignore Lower-Order Terms”

When we say:

> Ignore lower-order terms.

we are not saying those terms are literally zero.

For example:

\[
n^2+n
\]

does not become:

\[
n^2
\]

exactly.

Instead:

\[
n=o(n^2)
\]

means that relative to `n²`:

\[
\frac{n}{n^2}\to0
\]

Therefore:

\[
n^2+n
\]

has the same asymptotic growth as:

\[
n^2
\]

and:

\[
\boxed{
n^2+n=\Theta(n^2)
}
\]

---

# 15. Little-o Gives a Stronger Statement

Compare:

\[
n^2+n=O(n^2)
\]

This only says the expression is bounded above by a constant multiple of `n²`.

But:

\[
n=o(n^2)
\]

says something stronger:

> The `n` term becomes negligible relative to `n²`.

This is why little-o is useful for understanding the **relationship between individual terms**.

---

# 16. Standard DSA Growth Hierarchy

For many algorithm-analysis problems, remember this hierarchy:

\[
\boxed{
1
\ll
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
\]

Each step represents strictly slower asymptotic growth.

For example:

\[
1=o(\log n)
\]

\[
\log n=o(\sqrt n)
\]

\[
\sqrt n=o(n)
\]

\[
n=o(n\log n)
\]

\[
n\log n=o(n^2)
\]

\[
n^2=o(n^3)
\]

\[
n^3=o(2^n)
\]

\[
2^n=o(n!)
\]

---

# 17. Why This Hierarchy Matters in DSA

Suppose you have three algorithms:

### Algorithm A

\[
O(n)
\]

### Algorithm B

\[
O(n\log n)
\]

### Algorithm C

\[
O(n^2)
\]

The growth relationship is:

\[
n=o(n\log n)
\]

and:

\[
n\log n=o(n^2)
\]

Therefore:

\[
\boxed{
n=o(n\log n)=o(n^2)
}
\]

More precisely, the chain means:

\[
n=o(n\log n)
\]

and:

\[
n\log n=o(n^2)
\]

and by transitivity:

\[
n=o(n^2)
\]

---

# 18. Little-o and Common DSA Algorithms

Here are some familiar complexity relationships.

### Linear vs Binary Search

\[
\log n=o(n)
\]

So logarithmic growth is strictly smaller than linear growth.

### Merge Sort vs Quadratic Sorting

\[
n\log n=o(n^2)
\]

So `n log n` grows strictly slower than `n²`.

### Polynomial vs Brute Force Exponential

\[
n^k=o(2^n)
\]

for any fixed `k`.

So polynomial-time growth is strictly smaller than exponential growth.

---

# 19. Little-o Does Not Mean “Fast”

This is important.

Suppose:

\[
f(n)=n^{100}
\]

and:

\[
g(n)=2^n
\]

We have:

\[
n^{100}=o(2^n)
\]

But `n¹⁰⁰` can still be enormous.

Little-o only tells us:

\[
\boxed{
n^{100}\text{ grows slower than }2^n
}
\]

It does not mean:

> `n¹⁰⁰` is practically fast.

Asymptotic notation describes growth, not absolute performance.

---

# 20. Small Inputs vs Large Inputs

Asymptotic analysis focuses on:

\[
n\to\infty
\]

Therefore, little-o relationships describe behavior for **very large inputs**.

Two algorithms can behave differently for small values of `n`.

For example:

\[
T_A(n)=1000n
\]

and:

\[
T_B(n)=n^2
\]

We have:

\[
1000n=o(n^2)
\]

But for small `n`, the linear algorithm with the large constant may not be faster.

Asymptotic analysis asks:

> What happens as the input becomes arbitrarily large?

---

# 21. Little-o and Constants

Remember:

\[
5n=\Theta(n)
\]

but:

\[
5n\ne o(n)
\]

However:

\[
5n=o(n^2)
\]

Why?

Because:

\[
\frac{5n}{n^2}
=
\frac5n
\to0
\]

So the important question is not:

> “Does the function have a constant?”

The question is:

> **What happens to the ratio between the two functions?**

---

# 22. Little-o and Recursion

Little-o can also help compare recursive algorithm complexities.

Suppose one algorithm has:

\[
T_1(n)=n\log n
\]

and another has:

\[
T_2(n)=n^2
\]

Regardless of how the functions were obtained—loop analysis, recursion, recurrence solving, etc.—we can compare them using:

\[
\frac{T_1(n)}{T_2(n)}
\]

Therefore:

\[
T_1=o(T_2)
\]

Little-o is independent of **how the complexity was derived**.

---

# 23. Little-o Is About Relative Growth

This is perhaps the most important sentence in the entire topic:

> **Little-o does not describe a function by itself; it describes the growth of one function relative to another.**

For example:

\[
n=o(n^2)
\]

The statement is incomplete if we only say:

> “`n` is little-o.”

Little-o always compares:

\[
\boxed{
f\text{ relative to }g
}
\]

---

# 24. Direction Matters

If:

\[
n=o(n^2)
\]

we cannot reverse it.

\[
n^2\ne o(n)
\]

Instead:

\[
n=o(n^2)
\]

means:

\[
\boxed{
n\text{ grows strictly slower than }n^2
}
\]

Think of little-o as a directed relationship:

\[
\text{slower growth}
\quad\longrightarrow\quad
\text{faster growth}
\]

---

# 25. Little-o vs Big-O vs Θ

This is the most important final comparison.

| Notation | Main Meaning | Ratio Behavior |
|---|---|---|
| `f=O(g)` | `f` grows no faster than a constant multiple of `g` | Ratio is eventually bounded |
| `f=Θ(g)` | Same asymptotic growth | Ratio stays between positive constants |
| `f=o(g)` | `f` grows strictly slower | Ratio → `0` |

Examples:

\[
n=O(n)
\]

\[
n=\Theta(n)
\]

but:

\[
n\ne o(n)
\]

And:

\[
n=o(n^2)
\]

therefore:

\[
n=O(n^2)
\]

but:

\[
n\ne\Theta(n^2)
\]

---

# 26. The Ratio Method Unifies Everything

For:

\[
R(n)=\frac{f(n)}{g(n)}
\]

we can think of the result as:

### Ratio → `0`

\[
\boxed{f=o(g)}
\]

`f` is strictly smaller in growth.

### Ratio → positive finite constant

\[
\boxed{f=\Theta(g)}
\]

Same growth scale.

### Ratio → `∞`

\[
\boxed{g=o(f)}
\]

`f` grows strictly faster.

This gives one powerful framework for comparing functions.

---

# 27. Little-o and ε

The limit form is:

\[
\boxed{
f=o(g)
\iff
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

The ε-form is:

\[
\boxed{
\forall\epsilon>0,\exists N>0:
n>N
\Rightarrow
\left|\frac{f(n)}{g(n)}\right|<\epsilon
}
\]

In words:

> No matter how tiny a positive fraction `ε` you choose, eventually `f(n)` becomes smaller than that fraction of `g(n)`.

This is the rigorous meaning of **negligible relative growth**.

---

# 28. Why `f < g` Is Not Enough

Consider:

\[
f(n)=n-1
\]

and:

\[
g(n)=n
\]

For every:

\[
n>1
\]

we have:

\[
n-1<n
\]

But:

\[
\frac{n-1}{n}
=
1-\frac1n
\to1
\]

Therefore:

\[
\boxed{
n-1\ne o(n)
}
\]

The difference is not whether `f` is smaller.

The difference is whether `f` becomes **negligible relative to `g`**.

---

# 29. The Most Important Little-o Examples

Memorize these relationships gradually:

\[
\boxed{1=o(n)}
\]

\[
\boxed{\log n=o(n)}
\]

\[
\boxed{n=o(n\log n)}
\]

\[
\boxed{n\log n=o(n^2)}
\]

\[
\boxed{n^a=o(n^b)\quad(a<b)}
\]

\[
\boxed{n^a=o(c^n)\quad(c>1)}
\]

\[
\boxed{c^n=o(n!)}
\]

These form a large part of the growth hierarchy used in algorithm analysis.

---

# 30. Important Properties — Final Revision

### Property 1

\[
\boxed{
f=o(g)\Rightarrow f=O(g)
}
\]

### Property 2 — Transitivity

\[
\boxed{
f=o(g),\quad g=o(h)
\Rightarrow
f=o(h)
}
\]

### Property 3 — Constant Multiplication

\[
\boxed{
f=o(g)\Rightarrow cf=o(g)
}
\]

for fixed finite `c`.

### Property 4 — Addition

\[
\boxed{
f_1=o(g),\quad f_2=o(g)
\Rightarrow
f_1+f_2=o(g)
}
\]

### Property 5

\[
\boxed{
o(g)+O(g)=O(g)
}
\]

### Property 6

\[
\boxed{
f=o(g)\Rightarrow g+f=\Theta(g)
}
\]

under standard positive-function assumptions.

### Property 7 — Direction

\[
\boxed{
f=o(g)\not\Rightarrow g=o(f)
}
\]

---

# 31. Common Mistakes — Final Revision

## Mistake 1

Thinking:

\[
O(g)=o(g)
\]

Wrong.

---

## Mistake 2

Thinking:

\[
5n=o(n)
\]

Wrong.

Correct:

\[
5n=\Theta(n)
\]

---

## Mistake 3

Thinking:

\[
n-1=o(n)
\]

Wrong.

Correct:

\[
n-1=\Theta(n)
\]

---

## Mistake 4

Thinking:

\[
n^2+n=o(n^2)
\]

Wrong.

Correct:

\[
n^2+n=\Theta(n^2)
\]

---

## Mistake 5

Reversing:

\[
n=o(n^2)
\]

into:

\[
n^2=o(n)
\]

Wrong.

---

## Mistake 6

Thinking `f=o(g)` means:

\[
f(n)\to0
\]

Wrong.

For example:

\[
n=o(n^2)
\]

even though:

\[
n\to\infty
\]

---

## Mistake 7

Thinking little-o guarantees practical speed.

Wrong.

It only describes asymptotic growth.

---

# 32. Complete Little-o Decision Tree

When given:

\[
f(n)\quad\text{and}\quad g(n)
\]

and asked:

\[
f=o(g)?
\]

### Step 1

Form:

\[
\frac{f(n)}{g(n)}
\]

### Step 2

Simplify.

### Step 3

Calculate or recognize the limit:

\[
\lim_{n\to\infty}\frac{f(n)}{g(n)}
\]

### Step 4

Classify.

### If:

\[
0
\]

then:

\[
\boxed{f=o(g)}
\]

### If:

\[
0<C<\infty
\]

then:

\[
\boxed{f=\Theta(g)}
\]

### If:

\[
\infty
\]

then:

\[
\boxed{g=o(f)}
\]

### If the limit does not exist

Investigate further.

---

# 33. Complete Little-o Mental Model

You can now think about little-o in three layers.

## Layer 1 — Intuition

> `f` becomes negligible compared with `g`.

---

## Layer 2 — Mathematical Meaning

\[
\frac{f(n)}{g(n)}\to0
\]

---

## Layer 3 — Rigorous Meaning

\[
\forall\epsilon>0,\exists N:
n>N
\Rightarrow
|f(n)|<\epsilon|g(n)|
\]

These are **three ways of expressing the same idea**.

---

# 34. The Full Asymptotic Picture

Now put the major notations together.

### Big-O

\[
\boxed{
f=O(g)
}
\]

means:

> `f` is asymptotically bounded above by a constant multiple of `g`.

---

### Big-Ω

\[
\boxed{
f=\Omega(g)
}
\]

means:

> `f` is asymptotically bounded below by a constant multiple of `g`.

---

### Θ

\[
\boxed{
f=\Theta(g)
}
\]

means:

> `f` and `g` have the same asymptotic growth order.

---

### Little-o

\[
\boxed{
f=o(g)
}
\]

means:

> `f` grows strictly slower than `g`.

---

### Little-ω

\[
\boxed{
f=\omega(g)
}
\]

means:

> `f` grows strictly faster than `g`.

---

# 35. A Useful Conceptual Map

Think of the relationships like this:

\[
\boxed{
f=o(g)
}
\]

means:

\[
f\text{ is strictly below }g
\]

while:

\[
\boxed{
f=\Theta(g)
}
\]

means:

\[
f\text{ and }g\text{ are at the same growth level}
\]

and:

\[
\boxed{
f=\omega(g)
}
\]

means:

\[
f\text{ is strictly above }g
\]

Big-O and Big-Ω are broader bounds, while little-o and little-ω express **strict asymptotic separation**.

---

# 36. Final Growth Diagram

A useful way to visualize the major growth classes is:

\[
\boxed{
1
\ll
\log n
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
\]

For every neighboring pair:

\[
f=o(g)
\]

For example:

\[
\log n=o(n)
\]

\[
n=o(n\log n)
\]

\[
n\log n=o(n^2)
\]

\[
n^2=o(n^3)
\]

\[
n^3=o(2^n)
\]

\[
2^n=o(n!)
\]

---

# 37. What Little-o Adds to Your DSA Knowledge

Before learning little-o, you might say:

\[
n=O(n^2)
\]

This is correct.

But Big-O does not emphasize **how much slower** `n` grows compared with `n²`.

Little-o lets you say:

\[
\boxed{
n=o(n^2)
}
\]

which explicitly communicates:

> `n` is not merely bounded by `n²`; its growth becomes negligible relative to `n²`.

That is the main reason little-o is useful.

---

# 38. What You Should Remember for Interviews

For normal DSA interviews, you will use Big-O much more frequently than little-o.

However, understanding little-o gives you a much deeper understanding of:

- Growth rates
- Dominant terms
- Complexity comparison
- Mathematical limits
- Why lower-order terms disappear
- Why constant factors do not change Θ
- Why some functions are strictly smaller than others

So do not worry if you don't write `o(...)` frequently in coding interviews.

The **conceptual understanding** is what matters.

---

# 39. Final 10-Part Revision

You have now covered the entire Little-o series.

### Part 1 — Why Little-o Was Introduced

Big-O cannot distinguish:

\[
\text{same growth}
\]

from:

\[
\text{strictly slower growth}
\]

Little-o was introduced to express this strict separation.

---

### Part 2 — What Is Little-o?

\[
\boxed{
f=o(g)
}
\]

means:

> `f` grows strictly slower than `g`.

---

### Part 3 — Limit Definition

\[
\boxed{
f=o(g)
\iff
\lim_{n\to\infty}\frac{f}{g}=0
}
\]

---

### Part 4 — ε Definition

\[
\boxed{
\forall\epsilon>0,\exists N:
n>N\Rightarrow
|f|<\epsilon|g|
}
\]

---

### Part 5 — Equivalence of the Definitions

\[
\boxed{
\text{Limit definition}
\iff
\epsilon\text{-definition}
}
\]

The ε-definition is simply the rigorous meaning of the limit being zero.

---

### Part 6 — Little-o vs Big-O

\[
\boxed{
o(g)\subset O(g)
}
\]

Little-o:

\[
\forall\epsilon
\]

Big-O:

\[
\exists C
\]

---

### Part 7 — Examples and Counterexamples

Examples:

\[
n=o(n^2)
\]

\[
\log n=o(n)
\]

\[
n\log n=o(n^2)
\]

Counterexamples:

\[
5n\ne o(n)
\]

\[
n-1\ne o(n)
\]

\[
n^2+n\ne o(n^2)
\]

---

### Part 8 — Important Properties

\[
o(g)\subset O(g)
\]

\[
f=o(g),g=o(h)\Rightarrow f=o(h)
\]

\[
o(g)+o(g)=o(g)
\]

\[
g+o(g)=\Theta(g)
\]

Little-o is directional.

---

### Part 9 — How to Solve Problems

Use:

\[
\boxed{
\frac{f(n)}{g(n)}
}
\]

then:

\[
\boxed{
\lim_{n\to\infty}\frac{f(n)}{g(n)}
}
\]

and classify the result.

---

### Part 10 — Little-o in DSA

Little-o lets us formally describe:

\[
\boxed{
\text{strictly smaller asymptotic growth}
}
\]

such as:

\[
\log n=o(n)
\]

\[
n=o(n\log n)
\]

\[
n\log n=o(n^2)
\]

\[
n^2=o(2^n)
\]

---

# 40. Ultimate Little-o Cheat Sheet

## Definition

\[
\boxed{
f=o(g)
\iff
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

## ε Definition

\[
\boxed{
\forall\epsilon>0,\exists N:
n>N\Rightarrow
|f(n)|<\epsilon|g(n)|
}
\]

## Meaning

\[
\boxed{
f\text{ grows strictly slower than }g
}
\]

## Relationship with Big-O

\[
\boxed{
f=o(g)\Rightarrow f=O(g)
}
\]

but:

\[
\boxed{
f=O(g)\not\Rightarrow f=o(g)
}
\]

## Relationship with Θ

\[
\boxed{
f=\Theta(g)\Rightarrow f\ne o(g)
}
\]

under the standard positive-function setting.

## Transitivity

\[
\boxed{
f=o(g),\quad g=o(h)
\Rightarrow
f=o(h)
}
\]

## Constant

\[
\boxed{
f=o(g)\Rightarrow cf=o(g)
}
\]

for fixed finite `c`.

## Addition

\[
\boxed{
o(g)+o(g)=o(g)
}
\]

## Dominant Term

\[
\boxed{
g+o(g)=\Theta(g)
}
\]

under standard positive-function assumptions.

## Direction

\[
\boxed{
f=o(g)\not\Rightarrow g=o(f)
}
\]

## Main Problem-Solving Method

\[
\boxed{
\text{Ratio}
\rightarrow
\text{Simplify}
\rightarrow
\text{Limit}
\rightarrow
\text{Classify}
}
\]

## Growth Hierarchy

\[
\boxed{
1
\ll
\log n
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
\]

---

# Final Takeaway

If you remember only **one sentence** from the entire Little-o series, remember this:

> **`f(n) = o(g(n))` means that `f(n)` becomes arbitrarily small relative to `g(n)` as `n` becomes arbitrarily large.**

Mathematically:

\[
\boxed{
\frac{f(n)}{g(n)}\to0
}
\]

And in DSA:

> **Little-o describes strict asymptotic separation between growth rates.**

So when you see:

\[
n\log n=o(n^2)
\]

don't just memorize it.

Understand what it says:

\[
\frac{n\log n}{n^2}
=
\frac{\log n}{n}
\to0
\]

Therefore, relative to quadratic growth, `n log n` becomes negligible as the input size grows.

That is the real meaning of Little-o. 🔥
