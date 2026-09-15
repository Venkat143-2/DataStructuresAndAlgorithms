# Little-o Notation — Part 9: How to Determine Little-o in Problems

> **Goal:** Learn a systematic method to determine whether `f(n) = o(g(n))`, especially for functions that appear in mathematics, algorithms, and DSA.

---

# 1. What We Have Learned So Far

We know:

\[
f(n)=o(g(n))
\]

means:

\[
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
\]

In simple words:

> `f(n)` grows strictly slower than `g(n)`.

For example:

\[
n=o(n^2)
\]

because:

\[
\lim_{n\to\infty}\frac{n}{n^2}
=
\lim_{n\to\infty}\frac1n
=0
\]

Now the important question is:

> **When I see two complicated functions, how do I quickly determine whether little-o is true?**

---

# 2. The Universal Method

Whenever you need to determine:

\[
f(n)=o(g(n))?
\]

start with:

\[
\boxed{
\lim_{n\to\infty}\frac{f(n)}{g(n)}
}
\]

Then classify the result.

| Result | Conclusion |
|---|---|
| `0` | `f=o(g)` |
| positive finite constant | `f=Θ(g)` |
| `∞` | `g=o(f)` |
| does not exist | Need further analysis |

This is the **main test**.

---

# 3. Step-by-Step Procedure

Use this process:

### Step 1 — Identify `f(n)`

This is the function you are testing as the potentially smaller function.

### Step 2 — Identify `g(n)`

This is the function you are testing as the potentially larger function.

### Step 3 — Form the ratio

\[
\frac{f(n)}{g(n)}
\]

### Step 4 — Simplify

Cancel common factors and simplify the expression.

### Step 5 — Take the limit

Calculate:

\[
\lim_{n\to\infty}\frac{f(n)}{g(n)}
\]

### Step 6 — Classify

If the result is zero:

\[
\boxed{f=o(g)}
\]

---

# 4. Basic Example

Determine whether:

\[
n=o(n^2)
\]

### Step 1: Form the ratio

\[
\frac{n}{n^2}
\]

### Step 2: Simplify

\[
\frac1n
\]

### Step 3: Limit

\[
\lim_{n\to\infty}\frac1n=0
\]

Therefore:

\[
\boxed{n=o(n^2)}
\]

---

# 5. Example: Logarithm vs Linear

Determine whether:

\[
\log n=o(n)
\]

Calculate:

\[
\lim_{n\to\infty}\frac{\log n}{n}
\]

A logarithm grows much slower than a linear function.

Therefore:

\[
\boxed{
\lim_{n\to\infty}\frac{\log n}{n}=0
}
\]

and:

\[
\boxed{\log n=o(n)}
\]

This is one of the most important relationships in algorithm analysis.

---

# 6. Example: `n log n` vs `n²`

Determine whether:

\[
n\log n=o(n^2)
\]

Form the ratio:

\[
\frac{n\log n}{n^2}
\]

Cancel `n`:

\[
\frac{\log n}{n}
\]

We know:

\[
\frac{\log n}{n}\to0
\]

Therefore:

\[
\boxed{n\log n=o(n^2)}
\]

---

# 7. Example: Same Growth Rate

Determine whether:

\[
5n=o(n)
\]

Ratio:

\[
\frac{5n}{n}=5
\]

Limit:

\[
\lim_{n\to\infty}5=5
\]

The result is not zero.

Therefore:

\[
\boxed{5n\ne o(n)}
\]

Instead:

\[
\boxed{5n=\Theta(n)}
\]

This is an extremely important distinction.

---

# 8. Example: `n²` vs `n`

Determine whether:

\[
n^2=o(n)
\]

Ratio:

\[
\frac{n^2}{n}=n
\]

Limit:

\[
\lim_{n\to\infty}n=\infty
\]

Therefore:

\[
n^2
\]

does **not** grow slower than `n`.

Instead:

\[
\boxed{n=o(n^2)}
\]

---

# 9. The Polynomial Shortcut

For polynomial powers:

\[
n^a
\]

and:

\[
n^b
\]

we have:

\[
\boxed{
a<b\Rightarrow n^a=o(n^b)
}
\]

Why?

\[
\frac{n^a}{n^b}
=
\frac1{n^{b-a}}
\]

Since:

\[
b-a>0
\]

we get:

\[
\frac1{n^{b-a}}\to0
\]

Therefore:

\[
\boxed{n^a=o(n^b)\quad\text{when }a<b}
\]

---

# 10. Polynomial Examples

### Example 1

\[
n^2=o(n^5)
\]

because:

\[
2<5
\]

### Example 2

\[
n^{10}=o(n^{20})
\]

because:

\[
10<20
\]

### Example 3

\[
\sqrt n=o(n)
\]

because:

\[
n^{1/2}=o(n^1)
\]

### Example 4

\[
n^{3/2}=o(n^2)
\]

because:

\[
\frac32<2
\]

---

# 11. Polynomial Dominant-Term Shortcut

Consider:

\[
f(n)=3n^4+7n^2+10
\]

and:

\[
g(n)=n^6
\]

We want to determine whether:

\[
f=o(g)
\]

The dominant term of `f` is:

\[
3n^4
\]

So:

\[
f(n)=\Theta(n^4)
\]

Since:

\[
n^4=o(n^6)
\]

we get:

\[
\boxed{3n^4+7n^2+10=o(n^6)}
\]

---

# 12. Why Dominant Terms Help

Consider:

\[
f(n)=8n^3+5n^2+20n+100
\]

For large `n`, the `n³` term dominates.

Therefore:

\[
f(n)=\Theta(n^3)
\]

So when comparing with `n^5`, we only need to compare:

\[
n^3
\]

with:

\[
n^5
\]

Since:

\[
n^3=o(n^5)
\]

we conclude:

\[
\boxed{
8n^3+5n^2+20n+100=o(n^5)
}
\]

---

# 13. Logarithms vs Powers

A fundamental growth rule is:

\[
\boxed{
(\log n)^k=o(n^c)
}
\]

for any fixed:

\[
k>0,\quad c>0
\]

This means **any fixed power of a logarithm grows slower than any positive power of `n`.**

For example:

\[
\log n=o(n)
\]

\[
(\log n)^2=o(n)
\]

\[
(\log n)^{100}=o(n)
\]

and:

\[
(\log n)^{1000}=o(n^2)
\]

The logarithm can have a very large fixed exponent and still eventually lose to a positive polynomial power.

---

# 14. Example: `(log n)²` vs `n`

Determine:

\[
(\log n)^2=o(n)
\]

Consider:

\[
\lim_{n\to\infty}
\frac{(\log n)^2}{n}
\]

The denominator grows faster than any fixed power of the logarithm.

Therefore:

\[
\boxed{
(\log n)^2=o(n)
}
\]

---

# 15. Powers vs Exponentials

Another fundamental rule:

\[
\boxed{
n^k=o(a^n)
}
\]

for fixed:

\[
k>0,\quad a>1
\]

Therefore:

\[
n=o(2^n)
\]

\[
n^2=o(2^n)
\]

\[
n^{100}=o(2^n)
\]

and:

\[
n^5=o(10^n)
\]

The exponential eventually grows much faster than every fixed polynomial.

---

# 16. Example: `n¹⁰` vs `2ⁿ`

Determine:

\[
n^{10}=o(2^n)
\]

Consider:

\[
\lim_{n\to\infty}\frac{n^{10}}{2^n}
\]

The exponential dominates every fixed polynomial.

Therefore:

\[
\boxed{n^{10}=o(2^n)}
\]

---

# 17. Exponentials vs Factorials

For fixed:

\[
a>0
\]

the factorial eventually dominates the exponential:

\[
\boxed{
a^n=o(n!)
}
\]

Therefore:

\[
2^n=o(n!)
\]

and:

\[
10^n=o(n!)
\]

and even:

\[
100^n=o(n!)
\]

for sufficiently large `n`.

The factorial eventually grows faster.

---

# 18. Important Growth Hierarchy

A useful hierarchy is:

\[
\boxed{
1
\ll
\log n
\ll
(\log n)^k
\ll
n^a
\ll
n^b
\ll
c^n
\ll
n!
}
\]

where:

\[
k>0,\quad 0<a<b,\quad c>1
\]

The symbol `≪` represents a little-o relationship.

For example:

\[
\log n=o(n)
\]

\[
n=o(n^2)
\]

\[
n^2=o(2^n)
\]

\[
2^n=o(n!)
\]

---

# 19. Comparing Complicated Functions

Suppose:

\[
f(n)=n^2\log n
\]

and:

\[
g(n)=n^3
\]

Determine whether:

\[
f=o(g)
\]

Ratio:

\[
\frac{n^2\log n}{n^3}
\]

Simplify:

\[
\frac{\log n}{n}
\]

We know:

\[
\frac{\log n}{n}\to0
\]

Therefore:

\[
\boxed{
n^2\log n=o(n^3)
}
\]

---

# 20. Another Complicated Example

Consider:

\[
f(n)=n^3+100n
\]

and:

\[
g(n)=n^4+n^2
\]

We want:

\[
f=o(g)?
\]

For large `n`:

\[
f=\Theta(n^3)
\]

and:

\[
g=\Theta(n^4)
\]

Therefore:

\[
\frac{f}{g}
\]

behaves asymptotically like:

\[
\frac{n^3}{n^4}
=
\frac1n
\]

which approaches zero.

Therefore:

\[
\boxed{f=o(g)}
\]

---

# 21. Using Θ to Simplify Little-o Problems

This is a powerful technique.

Suppose:

\[
f=\Theta(F)
\]

and:

\[
g=\Theta(G)
\]

Then, under standard positive-function assumptions, comparing `f` and `g` can often be reduced to comparing `F` and `G`.

For example:

\[
f(n)=7n^3+2n
\]

so:

\[
f=\Theta(n^3)
\]

and:

\[
g(n)=4n^5+10
\]

so:

\[
g=\Theta(n^5)
\]

Since:

\[
n^3=o(n^5)
\]

we conclude:

\[
\boxed{f=o(g)}
\]

This avoids unnecessary algebra.

---

# 22. Cancellation Is Your Friend

Consider:

\[
\frac{n^4\log n}{n^6}
\]

Cancel powers:

\[
\frac{\log n}{n^2}
\]

Now:

\[
\log n=o(n^2)
\]

Therefore:

\[
\boxed{
\frac{n^4\log n}{n^6}\to0
}
\]

and:

\[
\boxed{
n^4\log n=o(n^6)
}
\]

---

# 23. When You Get `∞`

Suppose:

\[
\lim_{n\to\infty}\frac{f(n)}{g(n)}=\infty
\]

Then `f` is growing faster than `g`.

So:

\[
f\ne o(g)
\]

Instead, often:

\[
\boxed{g=o(f)}
\]

### Example

\[
f=n^3
\]

\[
g=n
\]

Then:

\[
\frac{n^3}{n}=n^2\to\infty
\]

Therefore:

\[
\boxed{n=o(n^3)}
\]

---

# 24. When You Get a Nonzero Constant

Suppose:

\[
\lim_{n\to\infty}\frac{f(n)}{g(n)}=C
\]

where:

\[
0<C<\infty
\]

Then `f` and `g` have the same asymptotic growth scale.

Therefore:

\[
\boxed{f=\Theta(g)}
\]

not:

\[
f=o(g)
\]

### Example

\[
f=3n^2
\]

\[
g=n^2
\]

Ratio:

\[
\frac{3n^2}{n^2}=3
\]

Therefore:

\[
\boxed{3n^2=\Theta(n^2)}
\]

but:

\[
\boxed{3n^2\ne o(n^2)}
\]

---

# 25. L'Hôpital's Rule

Sometimes the ratio produces an indeterminate form such as:

\[
\frac{\infty}{\infty}
\]

In calculus, L'Hôpital's rule can help.

For example:

\[
\lim_{n\to\infty}\frac{\ln n}{n}
\]

Treating the variable continuously:

\[
\lim_{x\to\infty}\frac{\ln x}{x}
\]

Differentiate numerator and denominator:

\[
\lim_{x\to\infty}\frac{1/x}{1}
\]

\[
=
\lim_{x\to\infty}\frac1x
\]

\[
=0
\]

Therefore:

\[
\boxed{\ln n=o(n)}
\]

---

# 26. Do Not Use L'Hôpital for Everything

For DSA, you usually do **not** need calculus for simple comparisons.

For example:

\[
n^2=o(n^5)
\]

can immediately be recognized because:

\[
2<5
\]

Likewise:

\[
n\log n=o(n^2)
\]

because:

\[
\frac{n\log n}{n^2}
=
\frac{\log n}{n}
\to0
\]

Use the simplest valid method.

---

# 27. Using Known Relationships

You do not need to calculate every limit from scratch.

If you already know:

\[
\log n=o(n)
\]

and:

\[
n=o(n^2)
\]

then by transitivity:

\[
\boxed{\log n=o(n^2)}
\]

Similarly, if:

\[
n=o(n\log n)
\]

and:

\[
n\log n=o(n^2)
\]

then:

\[
\boxed{n=o(n^2)}
\]

---

# 28. A Fast Decision Process

When you see:

\[
f=o(g)?
\]

ask:

### Question 1

Are they simple powers of `n`?

If yes:

\[
n^a=o(n^b)
\]

when:

\[
a<b
\]

### Question 2

Is there a logarithm?

Remember:

\[
\log n\ll n^a
\]

for every fixed:

\[
a>0
\]

### Question 3

Is there an exponential?

Remember:

\[
n^a\ll c^n
\]

for:

\[
c>1
\]

### Question 4

Is there a factorial?

Remember:

\[
c^n\ll n!
\]

for fixed `c`.

### Question 5

Are there polynomial sums?

Keep the highest power.

### Question 6

Still unsure?

Use:

\[
\boxed{
\lim_{n\to\infty}\frac{f(n)}{g(n)}
}
\]

---

# 29. Example: Full Decision Process

Determine:

\[
f(n)=n^2\log n
\]

and:

\[
g(n)=n^4
\]

Is:

\[
f=o(g)?
\]

### Step 1 — Ratio

\[
\frac{n^2\log n}{n^4}
\]

### Step 2 — Simplify

\[
\frac{\log n}{n^2}
\]

### Step 3 — Compare growth

A logarithm grows slower than any positive power of `n`.

Therefore:

\[
\frac{\log n}{n^2}\to0
\]

### Conclusion

\[
\boxed{
n^2\log n=o(n^4)
}
\]

---

# 30. Example: A False Statement

Determine whether:

\[
n^2+n=o(n^2)
\]

Ratio:

\[
\frac{n^2+n}{n^2}
\]

Simplify:

\[
1+\frac1n
\]

Limit:

\[
1+0=1
\]

Therefore:

\[
\boxed{
n^2+n\ne o(n^2)
}
\]

Instead:

\[
\boxed{
n^2+n=\Theta(n^2)
}
\]

This is a very important example because the lower-order `n` term does not make the whole expression little-o of `n²`.

---

# 31. Why `n² + n` Is Not `o(n²)`

This can feel confusing.

We know:

\[
n=o(n^2)
\]

But:

\[
n^2+n
\]

contains the main term:

\[
n^2
\]

The `n` is negligible.

But the entire expression is **not** negligible compared with `n²`.

In fact:

\[
n^2+n
=
n^2(1+\frac1n)
\]

and:

\[
1+\frac1n\to1
\]

Therefore:

\[
n^2+n
\]

has the same growth rate as:

\[
n^2
\]

So:

\[
\boxed{n^2+n=\Theta(n^2)}
\]

---

# 32. A Very Important Pattern

If:

\[
f=o(g)
\]

then:

\[
\boxed{g+f=\Theta(g)}
\]

But:

\[
\boxed{g+f\ne o(g)}
\]

in the standard nonzero positive setting.

Example:

\[
n=o(n^2)
\]

Therefore:

\[
n^2+n=\Theta(n^2)
\]

but:

\[
n^2+n\ne o(n^2)
\]

---

# 33. Comparing Algorithm Complexities

Little-o becomes useful when comparing algorithms.

Suppose Algorithm A has:

\[
T_A(n)=n\log n
\]

and Algorithm B has:

\[
T_B(n)=n^2
\]

Then:

\[
\frac{T_A(n)}{T_B(n)}
=
\frac{n\log n}{n^2}
=
\frac{\log n}{n}
\to0
\]

Therefore:

\[
\boxed{
T_A(n)=o(T_B(n))
}
\]

This means:

> Algorithm A becomes asymptotically negligible compared with Algorithm B.

So for sufficiently large inputs, the quadratic algorithm grows much faster.

---

# 34. Little-o Does Not Tell You Exact Runtime

Suppose:

\[
T_A=o(T_B)
\]

This does **not** tell us:

- exact runtime,
- exact number of operations,
- hardware performance,
- constant factors,
- which algorithm is faster for every small input.

It only tells us about **asymptotic relative growth**.

This distinction is important in real algorithm engineering.

---

# 35. Time Complexity Example

Consider:

### Algorithm A

\[
T_A(n)=1000n
\]

### Algorithm B

\[
T_B(n)=n^2
\]

Calculate:

\[
\frac{1000n}{n^2}
=
\frac{1000}{n}
\]

Therefore:

\[
\lim_{n\to\infty}\frac{1000}{n}=0
\]

So:

\[
\boxed{1000n=o(n^2)}
\]

Even though Algorithm A has a large constant, its growth is still strictly slower than quadratic.

---

# 36. Space Complexity Example

Suppose:

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
S_A(n)=o(S_B(n))
}
\]

So the first algorithm's extra space becomes negligible compared with the second's linear extra space.

---

# 37. Important Distinction: Little-o vs “Better Algorithm”

Be careful with statements like:

> `f=o(g)`, therefore algorithm A is always better.

That conclusion is too strong.

Little-o tells us:

\[
f
\]

has strictly smaller asymptotic growth than:

\[
g
\]

It does not automatically mean A is faster for every input.

For example, constants and lower-order behavior can dominate for small inputs.

The correct statement is:

> **Algorithm A has strictly better asymptotic growth than Algorithm B with respect to these functions.**

---

# 38. Common Mistakes

## Mistake 1 — Only checking whether `f < g`

Wrong reasoning:

\[
n-1<n
\]

therefore:

\[
n-1=o(n)
\]

Wrong.

Calculate:

\[
\frac{n-1}{n}
=
1-\frac1n
\to1
\]

Therefore:

\[
\boxed{n-1\ne o(n)}
\]

---

## Mistake 2 — Ignoring constant factors incorrectly

You may know that:

\[
5n=\Theta(n)
\]

but that does not mean:

\[
5n=o(n)
\]

The ratio is:

\[
5
\]

not zero.

---

## Mistake 3 — Thinking lower-order terms make the whole expression little-o

We know:

\[
n=o(n^2)
\]

But:

\[
n^2+n\ne o(n^2)
\]

because the entire expression still contains the dominant `n²` term.

---

## Mistake 4 — Reversing the direction

If:

\[
n=o(n^2)
\]

do not write:

\[
n^2=o(n)
\]

---

## Mistake 5 — Forgetting to simplify the ratio

Always try to simplify:

\[
\frac{f(n)}{g(n)}
\]

before doing complicated mathematics.

---

# 39. The Ultimate Problem-Solving Checklist

Whenever you see:

\[
f(n)=o(g(n))?
\]

follow this checklist:

### Step 1

Write:

\[
\frac{f(n)}{g(n)}
\]

### Step 2

Simplify.

### Step 3

Look for a known growth pattern.

Examples:

\[
n^a/n^b
\]

\[
\log n/n
\]

\[
n^a/c^n
\]

### Step 4

Calculate:

\[
\lim_{n\to\infty}\frac{f(n)}{g(n)}
\]

### Step 5

Classify.

#### If:

\[
L=0
\]

then:

\[
\boxed{f=o(g)}
\]

#### If:

\[
0<L<\infty
\]

then:

\[
\boxed{f=\Theta(g)}
\]

#### If:

\[
L=\infty
\]

then:

\[
\boxed{g=o(f)}
\]

#### If the limit does not exist

Do additional analysis.

---

# 40. Quick Growth Rules

Memorize these gradually:

### Logarithm vs polynomial

\[
\boxed{\log n=o(n^a)}
\]

for every fixed:

\[
a>0
\]

### Polynomial vs polynomial

\[
\boxed{n^a=o(n^b)}
\]

when:

\[
a<b
\]

### Polynomial vs exponential

\[
\boxed{n^a=o(c^n)}
\]

for:

\[
c>1
\]

### Exponential vs factorial

\[
\boxed{c^n=o(n!)}
\]

for fixed `c>0`.

---

# 41. One More Powerful Trick: Factor Out the Dominant Term

Consider:

\[
\frac{n^3+5n^2+10}{n^5}
\]

Instead of handling every term separately, divide each term:

\[
\frac{n^3}{n^5}
+
\frac{5n^2}{n^5}
+
\frac{10}{n^5}
\]

which becomes:

\[
\frac1{n^2}
+
\frac5{n^3}
+
\frac{10}{n^5}
\]

Every term approaches zero.

Therefore:

\[
\boxed{
n^3+5n^2+10=o(n^5)
}
\]

---

# 42. Another Trick: Divide by the Largest Power

Consider:

\[
\frac{4n^5+2n^3+n}{n^5}
\]

Divide everything by `n⁵`:

\[
4+\frac2{n^2}+\frac1{n^4}
\]

The limit is:

\[
4
\]

Therefore:

\[
4n^5+2n^3+n=\Theta(n^5)
\]

and:

\[
\boxed{
4n^5+2n^3+n\ne o(n^5)
}
\]

This is a very useful technique for polynomial comparisons.

---

# 43. The Big Picture

Little-o problems are fundamentally about one question:

> **Does the ratio between the two functions disappear to zero?**

Everything comes back to:

\[
\boxed{
\lim_{n\to\infty}\frac{f(n)}{g(n)}
}
\]

You can think of the ratio as asking:

> “What fraction of `g(n)` is `f(n)` when `n` becomes extremely large?”

If the answer approaches:

\[
0
\]

then:

\[
f=o(g)
\]

---

# 44. Final Mental Model

Imagine two runners.

If Runner A's speed/growth becomes an increasingly tiny fraction of Runner B's speed/growth, then:

\[
A=o(B)
\]

For functions:

\[
\frac{f(n)}{g(n)}\to0
\]

means:

> `f` becomes insignificant compared with `g`.

For example:

\[
\frac{n}{n^2}
=
\frac1n
\to0
\]

so:

\[
n=o(n^2)
\]

---

# 45. Final Cheat Sheet

## Main Definition

\[
\boxed{
f=o(g)
\iff
\lim_{n\to\infty}\frac{f}{g}=0
}
\]

## Limit Classification

\[
\boxed{
\begin{array}{c|c}
\text{Limit} & \text{Relationship}\\
\hline
0 & f=o(g)\\
C,\ 0<C<\infty & f=\Theta(g)\\
\infty & g=o(f)
\end{array}
}
\]

## Polynomial Rule

\[
\boxed{
a<b\Rightarrow n^a=o(n^b)
}
\]

## Logarithm Rule

\[
\boxed{
(\log n)^k=o(n^a)
}
\]

for fixed positive `k` and `a`.

## Exponential Rule

\[
\boxed{
n^a=o(c^n)
}
\]

for fixed `a>0`, `c>1`.

## Factorial Rule

\[
\boxed{
c^n=o(n!)
}
\]

for fixed `c>0`.

## Dominant-Term Rule

If:

\[
f=\Theta(n^a)
\]

and:

\[
g=\Theta(n^b)
\]

with:

\[
a<b
\]

then:

\[
\boxed{f=o(g)}
\]

---

# 46. What You Should Be Able to Do Now

You should now be able to determine relationships such as:

\[
n=o(n^2)
\]

\[
\log n=o(n)
\]

\[
n\log n=o(n^2)
\]

\[
n^3=o(2^n)
\]

\[
2^n=o(n!)
\]

and reject statements such as:

\[
5n=o(n)
\]

\[
n^2+n=o(n^2)
\]

\[
n-1=o(n)
\]

by using the ratio test.

The most important habit is:

\[
\boxed{
\text{Form the ratio}
\rightarrow
\text{Simplify}
\rightarrow
\text{Take the limit}
\rightarrow
\text{Classify}
}
\]

---

# Final Takeaway

When you face a little-o problem, **do not guess from the visual appearance of the functions**.

Use:

\[
\boxed{
\lim_{n\to\infty}\frac{f(n)}{g(n)}
}
\]

Then:

\[
\boxed{
0\Rightarrow f=o(g)
}
\]

\[
\boxed{
C>0\Rightarrow f=\Theta(g)
}
\]

\[
\boxed{
\infty\Rightarrow g=o(f)
}
\]

And as you gain experience, you will recognize standard growth patterns without calculating the limit every time.

> **Little-o is ultimately a comparison of relative growth, and the ratio test is the universal tool for making that comparison precise.**
