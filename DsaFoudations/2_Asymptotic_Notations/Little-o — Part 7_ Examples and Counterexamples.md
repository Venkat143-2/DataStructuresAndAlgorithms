# Little-o Notation — Part 7
## Examples and Counterexamples

---

# 1. Why Examples and Counterexamples Matter

Knowing the definition:

\[
f(n)=o(g(n))
\iff
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
\]

is necessary.

But simply memorizing the definition is not enough.

You should also be able to recognize:

- when little-o is true
- when little-o is false
- why it is true
- why it fails
- how Big-O and Θ behave in the same example

This part builds that intuition.

---

# 2. The Main Test

Whenever you want to determine whether:

\[
f(n)=o(g(n))
\]

calculate:

\[
\boxed{
\lim_{n\to\infty}\frac{f(n)}{g(n)}
}
\]

Then:

| Limit | Conclusion |
|---:|---|
| `0` | \(f=o(g)\) |
| Positive finite constant | \(f=\Theta(g)\), not little-o |
| `∞` | `f` grows faster, so \(f\ne o(g)\) |

This is our primary tool.

---

# 3. Example 1 — `n = o(n²)`

Let:

\[
f(n)=n
\]

and:

\[
g(n)=n^2
\]

Calculate:

\[
\frac{f(n)}{g(n)}
=
\frac{n}{n^2}
=
\frac1n
\]

Now take the limit:

\[
\lim_{n\to\infty}\frac1n=0
\]

Therefore:

\[
\boxed{
n=o(n^2)
}
\]

### Interpretation

Linear growth is strictly slower than quadratic growth.

---

# 4. Example 2 — `log n = o(n)`

Let:

\[
f(n)=\log n
\]

and:

\[
g(n)=n
\]

Then:

\[
\frac{\log n}{n}
\]

As `n` grows:

\[
\lim_{n\to\infty}\frac{\log n}{n}=0
\]

Therefore:

\[
\boxed{
\log n=o(n)
}
\]

### Interpretation

Logarithmic growth is strictly slower than linear growth.

---

# 5. Example 3 — `n log n = o(n²)`

Let:

\[
f(n)=n\log n
\]

and:

\[
g(n)=n^2
\]

Then:

\[
\frac{n\log n}{n^2}
=
\frac{\log n}{n}
\]

We know:

\[
\frac{\log n}{n}\rightarrow0
\]

Therefore:

\[
\boxed{
n\log n=o(n^2)
}
\]

---

# 6. Example 4 — `n² = o(n³)`

Let:

\[
f(n)=n^2
\]

and:

\[
g(n)=n^3
\]

Then:

\[
\frac{n^2}{n^3}
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
n^2=o(n^3)
}
\]

---

# 7. Example 5 — `1 = o(n)`

Let:

\[
f(n)=1
\]

and:

\[
g(n)=n
\]

Then:

\[
\frac1n\rightarrow0
\]

Therefore:

\[
\boxed{
1=o(n)
}
\]

Notice something interesting:

`f(n)=1` does not approach zero.

It remains:

\[
1
\]

But relative to `n`, it becomes negligible.

This reinforces:

> Little-o is about **relative growth**, not whether `f(n)` itself approaches zero.

---

# 8. Example 6 — `100n² = o(n³)`

Let:

\[
f(n)=100n^2
\]

and:

\[
g(n)=n^3
\]

Then:

\[
\frac{100n^2}{n^3}
=
\frac{100}{n}
\]

Therefore:

\[
\lim_{n\to\infty}\frac{100}{n}=0
\]

So:

\[
\boxed{
100n^2=o(n^3)
}
\]

A constant factor does not prevent little-o when the growth orders are genuinely different.

---

# 9. Example 7 — `n² + n = o(n³)`

Let:

\[
f(n)=n^2+n
\]

and:

\[
g(n)=n^3
\]

Then:

\[
\frac{n^2+n}{n^3}
=
\frac1n+\frac1{n^2}
\]

Taking the limit:

\[
\frac1n+\frac1{n^2}\rightarrow0
\]

Therefore:

\[
\boxed{
n^2+n=o(n^3)
}
\]

The lower-order terms do not change the final little-o relationship.

---

# 10. Example 8 — `n + 100 = o(n²)`

Consider:

\[
f(n)=n+100
\]

and:

\[
g(n)=n^2
\]

Then:

\[
\frac{n+100}{n^2}
=
\frac1n+\frac{100}{n^2}
\]

Both terms approach zero:

\[
\frac1n\rightarrow0
\]

and:

\[
\frac{100}{n^2}\rightarrow0
\]

Therefore:

\[
\boxed{
n+100=o(n^2)
}
\]

---

# 11. Counterexample 1 — `n ≠ o(n)`

Let:

\[
f(n)=n
\]

and:

\[
g(n)=n
\]

Then:

\[
\frac nn=1
\]

Therefore:

\[
\lim_{n\to\infty}1=1
\]

Since:

\[
1\ne0
\]

we conclude:

\[
\boxed{
n\ne o(n)
}
\]

However:

\[
n=\Theta(n)
\]

and:

\[
n=O(n)
\]

---

# 12. Counterexample 2 — `5n ≠ o(n)`

Let:

\[
f(n)=5n
\]

and:

\[
g(n)=n
\]

Then:

\[
\frac{5n}{n}=5
\]

Therefore:

\[
\lim_{n\to\infty}5=5
\]

Since the limit is not zero:

\[
\boxed{
5n\ne o(n)
}
\]

But:

\[
\boxed{
5n=\Theta(n)
}
\]

and:

\[
\boxed{
5n=O(n)
}
\]

---

# 13. Counterexample 3 — `n - 1 ≠ o(n)`

Let:

\[
f(n)=n-1
\]

and:

\[
g(n)=n
\]

Then:

\[
\frac{n-1}{n}
=
1-\frac1n
\]

Taking the limit:

\[
1-\frac1n\rightarrow1
\]

Therefore:

\[
\boxed{
n-1\ne o(n)
}
\]

Even though:

\[
n-1<n
\]

for positive `n`.

This is one of the most important counterexamples.

---

# 14. Why `n - 1` Is Not Little-o

The mistake would be:

\[
n-1<n
\]

therefore:

\[
n-1=o(n)
\]

But little-o doesn't ask:

> "Is `f` smaller?"

It asks:

> "Does `f` become an arbitrarily small fraction of `g`?"

Consider:

\[
\frac{n-1}{n}
\]

As `n` grows:

\[
\frac{n-1}{n}\rightarrow1
\]

So `n-1` remains almost the same size as `n`.

Therefore it is not little-o.

---

# 15. Counterexample 4 — `n² ≠ o(n)`

Let:

\[
f(n)=n^2
\]

and:

\[
g(n)=n
\]

Then:

\[
\frac{n^2}{n}=n
\]

and:

\[
n\rightarrow\infty
\]

Therefore:

\[
\boxed{
n^2\ne o(n)
}
\]

In fact, `n²` grows much faster than `n`.

But:

\[
n=o(n^2)
\]

The direction matters.

---

# 16. Counterexample 5 — `n log n ≠ o(n)`

Let:

\[
f(n)=n\log n
\]

and:

\[
g(n)=n
\]

Then:

\[
\frac{n\log n}{n}
=
\log n
\]

and:

\[
\log n\rightarrow\infty
\]

Therefore:

\[
\boxed{
n\log n\ne o(n)
}
\]

Instead:

\[
n=o(n\log n)
\]

---

# 17. Counterexample 6 — `n² + n ≠ o(n²)`

Let:

\[
f(n)=n^2+n
\]

and:

\[
g(n)=n^2
\]

Then:

\[
\frac{n^2+n}{n^2}
=
1+\frac1n
\]

Therefore:

\[
\lim_{n\to\infty}
\left(1+\frac1n\right)
=
1
\]

So:

\[
\boxed{
n^2+n\ne o(n^2)
}
\]

But:

\[
\boxed{
n^2+n=\Theta(n^2)
}
\]

---

# 18. Counterexample 7 — `2n + 10 ≠ o(n)`

Consider:

\[
f(n)=2n+10
\]

and:

\[
g(n)=n
\]

Then:

\[
\frac{2n+10}{n}
=
2+\frac{10}{n}
\]

Taking the limit:

\[
2+\frac{10}{n}\rightarrow2
\]

Therefore:

\[
\boxed{
2n+10\ne o(n)
}
\]

But:

\[
\boxed{
2n+10=\Theta(n)
}
\]

---

# 19. Counterexample 8 — `n ≠ o(2n)`

Consider:

\[
f(n)=n
\]

and:

\[
g(n)=2n
\]

Then:

\[
\frac{n}{2n}
=
\frac12
\]

Therefore:

\[
\lim_{n\to\infty}\frac12
=
\frac12
\]

The limit is not zero.

So:

\[
\boxed{
n\ne o(2n)
}
\]

But:

\[
\boxed{
n=\Theta(2n)
}
\]

and:

\[
\boxed{
n=O(2n)
}
\]

---

# 20. Same Growth Means Not Little-o

Consider:

\[
f(n)=3n^2+5n+10
\]

and:

\[
g(n)=n^2
\]

Calculate:

\[
\frac{3n^2+5n+10}{n^2}
\]

Simplify:

\[
3+\frac5n+\frac{10}{n^2}
\]

Take the limit:

\[
3+0+0=3
\]

Therefore:

\[
\boxed{
3n^2+5n+10\ne o(n^2)
}
\]

Instead:

\[
\boxed{
3n^2+5n+10=\Theta(n^2)
}
\]

---

# 21. A Very Important Pattern

Suppose:

\[
f(n)=an^k+\text{lower-order terms}
\]

and:

\[
g(n)=n^k
\]

where:

\[
a>0
\]

Then:

\[
\frac{f(n)}{g(n)}
\rightarrow a
\]

Since:

\[
a\ne0
\]

we get:

\[
\boxed{
f(n)\ne o(n^k)
}
\]

Instead:

\[
\boxed{
f(n)=\Theta(n^k)
}
\]

---

# 22. Example of the Pattern

Consider:

\[
f(n)=7n^4+3n^2+20
\]

and:

\[
g(n)=n^4
\]

Then:

\[
\frac{f(n)}{g(n)}
=
7+\frac3{n^2}+\frac{20}{n^4}
\]

Taking the limit:

\[
7
\]

Therefore:

\[
\boxed{
7n^4+3n^2+20\ne o(n^4)
}
\]

Instead:

\[
\boxed{
7n^4+3n^2+20=\Theta(n^4)
}
\]

---

# 23. Little-o Between Different Polynomial Powers

For:

\[
a<b
\]

we have:

\[
\boxed{
n^a=o(n^b)
}
\]

because:

\[
\frac{n^a}{n^b}
=
\frac1{n^{b-a}}
\rightarrow0
\]

Examples:

\[
\boxed{
n=o(n^2)
}
\]

\[
\boxed{
n^2=o(n^5)
}
\]

\[
\boxed{
n^3=o(n^{10})
}
\]

---

# 24. The Reverse Is False

If:

\[
a<b
\]

then:

\[
n^a=o(n^b)
\]

But:

\[
n^b\ne o(n^a)
\]

because:

\[
\frac{n^b}{n^a}
=
n^{b-a}
\rightarrow\infty
\]

Therefore:

\[
\boxed{
n^b\ne o(n^a)
}
\]

---

# 25. Logarithms vs Powers

A very important growth relationship is:

\[
\boxed{
\log n=o(n^a)
}
\]

for every:

\[
a>0
\]

For example:

\[
\log n=o(n)
\]

\[
\log n=o(n^2)
\]

\[
\log n=o(\sqrt n)
\]

The logarithm grows extremely slowly compared with any positive polynomial power.

---

# 26. Powers vs Exponentials

Another important relationship:

\[
\boxed{
n^k=o(c^n)
}
\]

for fixed:

\[
c>1
\]

and fixed:

\[
k>0
\]

For example:

\[
n^2=o(2^n)
\]

because:

\[
\frac{n^2}{2^n}\rightarrow0
\]

Similarly:

\[
n^{100}=o(2^n)
\]

although the point where the exponential dominates may be very large.

---

# 27. Exponentials vs Factorials

The standard growth hierarchy continues:

\[
c^n=o(n!)
\]

for fixed:

\[
c>0
\]

under the usual asymptotic setting.

For example:

\[
\boxed{
2^n=o(n!)
}
\]

This means factorial growth eventually dominates exponential growth.

---

# 28. Standard Growth Hierarchy

A useful simplified hierarchy is:

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

Here:

\[
f\ll g
\]

can be read informally as:

\[
f=o(g)
\]

So, for example:

\[
\log n=o(n)
\]

and:

\[
n=o(n\log n)
\]

and:

\[
n\log n=o(n^2)
\]

and:

\[
n^3=o(2^n)
\]

and:

\[
2^n=o(n!)
\]

---

# 29. A Chain of Little-o Relationships

Suppose:

\[
f=o(g)
\]

and:

\[
g=o(h)
\]

Then:

\[
\boxed{
f=o(h)
}
\]

This is called **transitivity**.

For example:

\[
\log n=o(n)
\]

and:

\[
n=o(n^2)
\]

Therefore:

\[
\boxed{
\log n=o(n^2)
}
\]

---

# 30. Why Transitivity Works

Using limits:

\[
\frac{f(n)}{g(n)}\rightarrow0
\]

and:

\[
\frac{g(n)}{h(n)}\rightarrow0
\]

Then:

\[
\frac{f(n)}{h(n)}
=
\frac{f(n)}{g(n)}
\cdot
\frac{g(n)}{h(n)}
\]

Both factors approach zero, so the product approaches zero.

Therefore:

\[
\boxed{
f=o(h)
}
\]

---

# 31. Little-o and Big-O Together

If:

\[
f=o(g)
\]

then automatically:

\[
f=O(g)
\]

For example:

\[
n=o(n^2)
\]

therefore:

\[
n=O(n^2)
\]

But:

\[
n=O(n)
\]

does not imply:

\[
n=o(n)
\]

So always remember:

\[
\boxed{
o(g)\subsetneq O(g)
}
\]

---

# 32. A Comparison Table of Examples

| Relationship | Limit | Result |
|---|---:|---|
| \(n/n^2\) | `0` | \(n=o(n^2)\) |
| \(\log n/n\) | `0` | \(\log n=o(n)\) |
| \(n\log n/n^2\) | `0` | \(n\log n=o(n^2)\) |
| \(n^2/n^3\) | `0` | \(n^2=o(n^3)\) |
| \(n/n\) | `1` | \(n\ne o(n)\) |
| \(5n/n\) | `5` | \(5n\ne o(n)\) |
| \((n-1)/n\) | `1` | \(n-1\ne o(n)\) |
| \(n^2/n\) | `∞` | \(n^2\ne o(n)\) |
| \((n^2+n)/n^2\) | `1` | not little-o |
| \((2n+10)/n\) | `2` | not little-o |

---

# 33. The Most Important Counterexamples

Memorize these because they destroy common misunderstandings.

### Smaller does not mean little-o

\[
\boxed{
n-1<n
\quad\text{but}\quad
n-1\ne o(n)
}
\]

### Same function is not little-o of itself

\[
\boxed{
n\ne o(n)
}
\]

### Constant multiple is not little-o

\[
\boxed{
5n\ne o(n)
}
\]

### Lower-order difference does not automatically create little-o

\[
\boxed{
n^2+n\ne o(n^2)
}
\]

### Direction matters

\[
\boxed{
n=o(n^2)
}
\]

but:

\[
\boxed{
n^2\ne o(n)
}
\]

---

# 34. A Powerful Pattern for Polynomials

Suppose:

\[
f(n)=a_kn^k+a_{k-1}n^{k-1}+\cdots+a_0
\]

and:

\[
g(n)=n^m
\]

There are three useful cases.

### Case 1: `k < m`

Then:

\[
\boxed{
f=o(g)
}
\]

---

### Case 2: `k = m`

Then the ratio approaches:

\[
a_k
\]

assuming:

\[
a_k\ne0
\]

Therefore:

\[
\boxed{
f=\Theta(g)
}
\]

not little-o.

---

### Case 3: `k > m`

Then:

\[
\boxed{
f\ne o(g)
}
\]

because `f` grows faster.

---

# 35. Example Using the Polynomial Rule

Consider:

\[
f(n)=4n^3+2n+7
\]

Compare it with:

\[
g(n)=n^5
\]

Highest power in `f`:

\[
n^3
\]

Highest power in `g`:

\[
n^5
\]

Since:

\[
3<5
\]

we know:

\[
\boxed{
4n^3+2n+7=o(n^5)
}
\]

---

# 36. Another Example

Compare:

\[
f(n)=4n^5+2n
\]

with:

\[
g(n)=n^5
\]

Both have highest power:

\[
n^5
\]

The ratio approaches:

\[
4
\]

Therefore:

\[
\boxed{
f\ne o(g)
}
\]

Instead:

\[
\boxed{
f=\Theta(g)
}
\]

---

# 37. Another Example

Compare:

\[
f(n)=n^7+n
\]

with:

\[
g(n)=n^4
\]

Since:

\[
7>4
\]

`f` grows faster.

Therefore:

\[
\boxed{
f\ne o(g)
}
\]

In fact:

\[
\frac{n^7+n}{n^4}
=
n^3+\frac1{n^3}
\rightarrow\infty
\]

---

# 38. Little-o Is About the Dominant Growth

When comparing functions, the dominant growth term is often enough to predict the result.

For example:

\[
f(n)=n^3+100n^2+5000
\]

has dominant term:

\[
n^3
\]

So when comparing it with:

\[
n^5
\]

we can immediately expect:

\[
f=o(n^5)
\]

because:

\[
n^3=o(n^5)
\]

---

# 39. But Do Not Use "Drop Terms" Blindly

Be careful.

Suppose:

\[
f(n)=n^2+n
\]

and:

\[
g(n)=n^2
\]

Both have dominant term:

\[
n^2
\]

Therefore they have the same asymptotic growth.

So:

\[
f=\Theta(g)
\]

not:

\[
f=o(g)
\]

The presence of a lower-order term does not make the entire function little-o of the dominant term.

---

# 40. The Key Difference

Compare:

\[
n^2+n
\]

with:

\[
n^3
\]

Here the dominant term of `f` is:

\[
n^2
\]

which is strictly smaller than:

\[
n^3
\]

Therefore:

\[
\boxed{
n^2+n=o(n^3)
}
\]

But compare:

\[
n^2+n
\]

with:

\[
n^2
\]

Their dominant terms have the same order.

Therefore:

\[
\boxed{
n^2+n=\Theta(n^2)
}
\]

not little-o.

---

# 41. Final Decision Tree

When asked:

\[
f(n)=o(g(n))?
\]

use:

```text id="z2s1s7"
Calculate:

lim f(n)/g(n)
        ↓
   ┌────┼────┐
   ↓    ↓    ↓
   0    c    ∞
        ↓
   ┌────┴─────────┐
   ↓              ↓
c > 0 finite      ∞
   ↓              ↓
Θ(g)             f grows faster
   ↓
NOT little-o
```

More directly:

```text id="h5nupv"
Ratio → 0
    ↓
f = o(g)

Ratio → positive constant
    ↓
f = Θ(g)
    ↓
f ≠ o(g)

Ratio → ∞
    ↓
f grows faster
    ↓
f ≠ o(g)
```

---

# 42. Final Cheat Sheet

## Little-o is TRUE when:

\[
\boxed{
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

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

\[
n^2=o(n^3)
\]

\[
100n^2=o(n^3)
\]

---

## Little-o is FALSE when:

### Ratio approaches a positive constant

\[
\boxed{
n\ne o(n)
}
\]

\[
\boxed{
5n\ne o(n)
}
\]

\[
\boxed{
n-1\ne o(n)
}
\]

### Ratio approaches infinity

\[
\boxed{
n^2\ne o(n)
}
\]

\[
\boxed{
n\log n\ne o(n)
}
\]

---

# 43. Most Important Patterns to Remember

### Different growth powers

\[
a<b
\Rightarrow
\boxed{
n^a=o(n^b)
}
\]

### Same growth power

\[
\boxed{
n^a\ne o(n^a)
}
\]

### Constant multiple

\[
\boxed{
cn\ne o(n)
\quad(c>0)
}
\]

### Lower-order subtraction

\[
\boxed{
n-1\ne o(n)
}
\]

### Lower-order addition

\[
\boxed{
n^2+n\ne o(n^2)
}
\]

but:

\[
\boxed{
n^2+n=o(n^3)
}
\]

---

# 44. Final Mental Model

Think about the ratio:

\[
\frac{f(n)}{g(n)}
\]

### If it disappears:

\[
\boxed{
\frac{f(n)}{g(n)}\rightarrow0
}
\]

then:

\[
\boxed{
f=o(g)
}
\]

### If it settles at a nonzero constant:

\[
\boxed{
\frac{f(n)}{g(n)}\rightarrow c
}
\]

where:

\[
c>0
\]

then:

\[
\boxed{
f=\Theta(g)
}
\]

and not little-o.

### If it explodes:

\[
\boxed{
\frac{f(n)}{g(n)}\rightarrow\infty
}
\]

then `f` grows faster.

---

# 45. One Sentence to Remember

> **To test little-o, compare the functions through their ratio: if the ratio disappears to zero, little-o is true; if it settles at a nonzero constant or grows without bound, little-o is false.**

The central test remains:

\[
\boxed{
f=o(g)
\iff
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
=0
}
\]

This single rule can solve a huge number of little-o problems.