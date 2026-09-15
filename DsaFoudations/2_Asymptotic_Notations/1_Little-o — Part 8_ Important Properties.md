# Little-o Notation — Part 8: Important Properties

> **Goal:** Learn the mathematical properties of little-o so that you can combine, simplify, compare, and prove asymptotic relationships confidently.

---

# 1. Where We Are

So far, we know:

\[
f(n)=o(g(n))
\]

means:

\[
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
\]

In simple words:

> **`f(n)` becomes negligible compared with `g(n)` as `n` becomes very large.**

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

Now we want to understand what happens when we **combine** little-o relationships.

---

# 2. Property 1 — Little-o Implies Big-O

This is one of the most important properties.

If:

\[
f(n)=o(g(n))
\]

then:

\[
f(n)=O(g(n))
\]

So:

\[
\boxed{o(g)\subset O(g)}
\]

## Why?

Little-o says:

\[
\forall\epsilon>0,\exists N:
|f(n)|<\epsilon|g(n)|
\]

Choose:

\[
\epsilon=1
\]

Then eventually:

\[
|f(n)|<|g(n)|
\]

Therefore:

\[
|f(n)|\le1|g(n)|
\]

which satisfies the Big-O definition with:

\[
C=1
\]

Therefore:

\[
\boxed{f=o(g)\Rightarrow f=O(g)}
\]

---

# 3. But Big-O Does NOT Imply Little-o

The reverse is false.

For example:

\[
n=O(n)
\]

but:

\[
n\ne o(n)
\]

Why?

Calculate the ratio:

\[
\frac{n}{n}=1
\]

Therefore:

\[
\lim_{n\to\infty}1=1
\]

not zero.

So:

\[
\boxed{n=O(n)\quad\text{but}\quad n\ne o(n)}
\]

This is because Big-O allows functions with the **same growth rate**, while little-o requires **strictly slower growth**.

---

# 4. Property 2 — Transitivity

Little-o is transitive.

If:

\[
f=o(g)
\]

and:

\[
g=o(h)
\]

then:

\[
\boxed{f=o(h)}
\]

## Proof

We know:

\[
\lim_{n\to\infty}\frac{f}{g}=0
\]

and:

\[
\lim_{n\to\infty}\frac{g}{h}=0
\]

Now:

\[
\frac{f}{h}
=
\frac{f}{g}\cdot\frac{g}{h}
\]

Therefore:

\[
\lim_{n\to\infty}\frac{f}{h}
=
\left(\lim_{n\to\infty}\frac{f}{g}\right)
\left(\lim_{n\to\infty}\frac{g}{h}\right)
\]

\[
=0\cdot0
\]

\[
=0
\]

Therefore:

\[
\boxed{f=o(h)}
\]

---

# 5. Example of Transitivity

Suppose:

\[
n=o(n^2)
\]

and:

\[
n^2=o(n^3)
\]

Then immediately:

\[
\boxed{n=o(n^3)}
\]

We do not need to calculate again.

This is extremely useful when dealing with a chain of growth rates.

For example:

\[
\log n=o(n)
\]

\[
n=o(n^2)
\]

\[
n^2=o(n^3)
\]

Therefore:

\[
\boxed{\log n=o(n^3)}
\]

---

# 6. Property 3 — Multiplication by a Constant

Suppose:

\[
f=o(g)
\]

and `c` is a fixed finite constant.

Then:

\[
\boxed{cf=o(g)}
\]

## Why?

Start with:

\[
\lim_{n\to\infty}\frac{f}{g}=0
\]

For `cf`:

\[
\lim_{n\to\infty}\frac{cf}{g}
=
c\lim_{n\to\infty}\frac{f}{g}
\]

\[
=c(0)
\]

\[
=0
\]

Therefore:

\[
cf=o(g)
\]

---

## Example

If:

\[
n=o(n^2)
\]

then:

\[
5n=o(n^2)
\]

and:

\[
1000n=o(n^2)
\]

and:

\[
0.0001n=o(n^2)
\]

All are true.

The constant does not change the fundamental growth relationship.

---

# 7. Important Difference: Constant Multiplication vs Same Growth

Consider:

\[
5n
\]

and:

\[
n
\]

We have:

\[
5n=\Theta(n)
\]

but:

\[
5n\ne o(n)
\]

Why?

\[
\frac{5n}{n}=5
\]

and:

\[
\lim_{n\to\infty}5=5
\]

not zero.

So multiplying a function by a constant preserves its **growth class**.

But if the original function was already little-o of another function, multiplying it by a constant still keeps it little-o of that larger function.

---

# 8. Property 4 — Addition of Little-o Terms

Suppose:

\[
f_1=o(g)
\]

and:

\[
f_2=o(g)
\]

Then:

\[
\boxed{f_1+f_2=o(g)}
\]

## Proof

We know:

\[
\frac{f_1}{g}\to0
\]

and:

\[
\frac{f_2}{g}\to0
\]

Then:

\[
\frac{f_1+f_2}{g}
=
\frac{f_1}{g}+\frac{f_2}{g}
\]

Taking the limit:

\[
\lim\frac{f_1+f_2}{g}
=
0+0
\]

\[
=0
\]

Therefore:

\[
\boxed{f_1+f_2=o(g)}
\]

---

# 9. Example of Addition

Suppose:

\[
n=o(n^3)
\]

and:

\[
n^2=o(n^3)
\]

Therefore:

\[
n+n^2=o(n^3)
\]

Check:

\[
\frac{n+n^2}{n^3}
=
\frac1{n^2}+\frac1n
\]

As:

\[
n\to\infty
\]

both terms approach zero:

\[
0+0=0
\]

Therefore:

\[
\boxed{n+n^2=o(n^3)}
\]

---

# 10. Property 5 — Finite Sums of Little-o Terms

The addition rule extends to any **finite number** of little-o terms.

If:

\[
f_1=o(g)
\]

\[
f_2=o(g)
\]

\[
\cdots
\]

\[
f_k=o(g)
\]

where `k` is fixed, then:

\[
\boxed{
f_1+f_2+\cdots+f_k=o(g)
}
\]

## Example

If:

\[
n=o(n^4)
\]

\[
n^2=o(n^4)
\]

\[
n^3=o(n^4)
\]

then:

\[
\boxed{n+n^2+n^3=o(n^4)}
\]

---

# 11. Property 6 — Adding a Big-O Term

This property is slightly different.

Suppose:

\[
f=o(g)
\]

and:

\[
h=O(g)
\]

Then:

\[
\boxed{f+h=O(g)}
\]

But we **cannot generally say**:

\[
f+h=o(g)
\]

---

## Why?

Consider:

\[
f=n
\]

and:

\[
h=n^2
\]

with:

\[
g=n^2
\]

We have:

\[
n=o(n^2)
\]

and:

\[
n^2=O(n^2)
\]

Therefore:

\[
n+n^2=O(n^2)
\]

But:

\[
n+n^2\ne o(n^2)
\]

because:

\[
\frac{n+n^2}{n^2}
=
\frac1n+1
\to1
\]

So the result is:

\[
\boxed{O(g)}
\]

not necessarily:

\[
o(g)
\]

---

# 12. Very Important Rule

Remember this pattern:

### Little-o + Little-o

\[
\boxed{o(g)+o(g)=o(g)}
\]

### Little-o + Big-O

\[
\boxed{o(g)+O(g)=O(g)}
\]

The second result is not necessarily little-o.

---

# 13. Property 7 — Adding a Little-o Term to the Main Function

Suppose:

\[
f=o(g)
\]

Then:

\[
\boxed{g+f=\Theta(g)}
\]

under the usual asymptotic setting where `g` is eventually positive and nonzero.

This is a very useful idea.

The little-o term is **negligible** compared with `g`.

Therefore:

\[
g+f
\]

still has the same asymptotic growth as:

\[
g
\]

---

## Example

Consider:

\[
n^2+n
\]

We know:

\[
n=o(n^2)
\]

Therefore:

\[
\boxed{n^2+n=\Theta(n^2)}
\]

The `n` term becomes negligible compared with `n²`.

Similarly:

\[
n^3+n^2+n
\]

has:

\[
n^2=o(n^3)
\]

and:

\[
n=o(n^3)
\]

Therefore:

\[
\boxed{n^3+n^2+n=\Theta(n^3)}
\]

---

# 14. Connection to Dominant Terms

This property gives a mathematical explanation for something we frequently do in complexity analysis.

Consider:

\[
f(n)=7n^3+4n^2+100n+50
\]

Relative to `n³`:

\[
n^2=o(n^3)
\]

\[
n=o(n^3)
\]

\[
1=o(n^3)
\]

Therefore all lower-order terms are negligible compared with `n³`.

So:

\[
7n^3+4n^2+100n+50
=
7n^3+o(n^3)
\]

Since:

\[
7n^3=\Theta(n^3)
\]

we get:

\[
\boxed{f(n)=\Theta(n^3)}
\]

This is one of the mathematical foundations behind **dropping lower-order terms** in asymptotic analysis.

---

# 15. Property 8 — Direction Matters

Little-o is directional.

If:

\[
f=o(g)
\]

you generally cannot reverse it to:

\[
g=o(f)
\]

For example:

\[
n=o(n^2)
\]

but:

\[
n^2\ne o(n)
\]

because:

\[
\frac{n^2}{n}=n
\]

and:

\[
n\to\infty
\]

not zero.

Therefore:

\[
\boxed{n=o(n^2)}
\]

does NOT mean:

\[
n^2=o(n)
\]

---

# 16. Think of Little-o Like an Arrow

It is helpful to visualize:

\[
n
\longrightarrow
n^2
\]

meaning:

\[
n=o(n^2)
\]

The arrow points from the **slower-growing function** to the **faster-growing function**.

Another example:

\[
\log n
\longrightarrow
n
\longrightarrow
n^2
\longrightarrow
n^3
\longrightarrow
2^n
\]

Therefore:

\[
\log n=o(n)
\]

\[
n=o(n^2)
\]

\[
n^2=o(n^3)
\]

\[
n^3=o(2^n)
\]

---

# 17. Property 9 — Little-o and Θ

Little-o and Θ describe different situations.

If:

\[
f=o(g)
\]

then `f` grows **strictly slower** than `g`.

If:

\[
f=\Theta(g)
\]

then `f` and `g` have the **same asymptotic growth rate**.

Therefore, under the standard positive-function setting:

\[
\boxed{f=o(g)\Rightarrow f\ne\Theta(g)}
\]

and:

\[
\boxed{f=\Theta(g)\Rightarrow f\ne o(g)}
\]

---

## Example

\[
n=o(n^2)
\]

but:

\[
n\ne\Theta(n^2)
\]

Meanwhile:

\[
5n=\Theta(n)
\]

but:

\[
5n\ne o(n)
\]

---

# 18. Growth Classification Using the Ratio

For many problems, calculate:

\[
L=\lim_{n\to\infty}\frac{f(n)}{g(n)}
\]

Then:

| Limit | Relationship |
|---|---|
| `0` | `f=o(g)` |
| positive finite constant | `f=Θ(g)` |
| `∞` | `g=o(f)` |

For example:

### Case 1

\[
\lim\frac{n}{n^2}=0
\]

Therefore:

\[
\boxed{n=o(n^2)}
\]

### Case 2

\[
\lim\frac{5n}{n}=5
\]

Therefore:

\[
\boxed{5n=\Theta(n)}
\]

### Case 3

\[
\lim\frac{n^2}{n}=∞
\]

Therefore:

\[
\boxed{n=o(n^2)}
\]

---

# 19. Property 10 — Compatibility with Θ

Suppose:

\[
f=o(g)
\]

and:

\[
g=\Theta(h)
\]

Then:

\[
\boxed{f=o(h)}
\]

Why?

If:

\[
g=\Theta(h)
\]

then `g` and `h` differ only by constant factors asymptotically.

Since `f` is negligible compared with `g`, it is also negligible compared with something that has the same growth rate as `g`.

---

## Example

Suppose:

\[
n=o(n^2)
\]

and:

\[
n^2=\Theta(5n^2+10n)
\]

Then:

\[
\boxed{n=o(5n^2+10n)}
\]

---

# 20. Another Useful Θ Relationship

Suppose:

\[
f=\Theta(g)
\]

and:

\[
g=o(h)
\]

Then:

\[
\boxed{f=o(h)}
\]

The reason is similar.

If `f` has the same growth rate as `g`, and `g` is strictly slower than `h`, then `f` is also strictly slower than `h`.

---

## Example

\[
n^2=\Theta(7n^2+3n)
\]

and:

\[
n^2=o(n^3)
\]

Therefore:

\[
\boxed{7n^2+3n=o(n^3)}
\]

---

# 21. Property 11 — Product Rule

There is a useful product rule.

Suppose:

\[
f=o(g)
\]

and:

\[
h=O(k)
\]

Under the usual conditions needed for the ratios to be defined:

\[
\boxed{fh=o(gk)}
\]

## Proof Idea

We can write:

\[
\frac{fh}{gk}
=
\frac{f}{g}\cdot\frac{h}{k}
\]

We know:

\[
\frac{f}{g}\to0
\]

and:

\[
h=O(k)
\]

means:

\[
\left|\frac{h}{k}\right|
\]

is eventually bounded by some constant.

Therefore:

\[
0\times\text{bounded value}=0
\]

so:

\[
\boxed{fh=o(gk)}
\]

---

## Example

Suppose:

\[
n=o(n^2)
\]

and:

\[
\log n=O(n)
\]

Then:

\[
n\log n=o(n^3)
\]

because:

\[
\frac{n\log n}{n^3}
=
\frac1{n^2}\log n
\to0
\]

---

# 22. Property 12 — Little-o Is Not Equality

This is conceptually important.

When we write:

\[
f=o(g)
\]

we are **not saying**:

\[
f=g
\]

We are saying:

> `f` becomes asymptotically negligible compared with `g`.

For example:

\[
n=o(n^2)
\]

does not mean:

\[
n=n^2
\]

Obviously they are different functions.

Little-o describes a **relationship between growth rates**.

---

# 23. Little-o Is Directional, Not an Equivalence Relation

This is worth remembering.

Because:

\[
n=o(n^2)
\]

but:

\[
n^2\ne o(n)
\]

the relationship is not symmetric.

Therefore, little-o behaves differently from equality or Θ.

### Equality

\[
f=g\Rightarrow g=f
\]

### Θ

If:

\[
f=\Theta(g)
\]

then:

\[
g=\Theta(f)
\]

### Little-o

If:

\[
f=o(g)
\]

we generally **cannot** say:

\[
g=o(f)
\]

Therefore:

\[
\boxed{\text{Little-o is directional}}
\]

---

# 24. Standard Growth Chain

A very useful chain to remember is:

\[
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
\]

Here `≪` means “grows strictly slower than.”

So:

\[
1=o(\log n)
\]

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

This chain is extremely useful in DSA.

---

# 25. Transitivity Creates the Entire Chain

Because little-o is transitive:

\[
f=o(g)
\]

and:

\[
g=o(h)
\]

implies:

\[
f=o(h)
\]

Therefore, from:

\[
\log n=o(n)
\]

and:

\[
n=o(n^2)
\]

we immediately know:

\[
\boxed{\log n=o(n^2)}
\]

And because:

\[
n^2=o(2^n)
\]

we also know:

\[
\boxed{\log n=o(2^n)}
\]

without calculating the limits again.

---

# 26. Important Property Summary

| Property | Result |
|---|---|
| Little-o → Big-O | `f=o(g) ⇒ f=O(g)` |
| Transitivity | `f=o(g), g=o(h) ⇒ f=o(h)` |
| Constant multiplication | `f=o(g) ⇒ cf=o(g)` |
| Addition | `f₁=o(g), f₂=o(g) ⇒ f₁+f₂=o(g)` |
| Little-o + Big-O | `o(g)+O(g)=O(g)` |
| Main term + little-o | `g+o(g)=Θ(g)` |
| Direction | `f=o(g)` does not imply `g=o(f)` |
| With Θ | `f=o(g), g=Θ(h) ⇒ f=o(h)` |
| Product | `f=o(g), h=O(k) ⇒ fh=o(gk)` under standard conditions |
| Same growth | `f=Θ(g)` generally means `f≠o(g)` |

---

# 27. The Three Most Important Properties for DSA

You do not need to memorize every theorem immediately.

For DSA, focus especially on these three:

## 1. Little-o implies Big-O

\[
\boxed{o(g)\subset O(g)}
\]

---

## 2. Transitivity

\[
\boxed{
f=o(g),\quad g=o(h)
\Rightarrow
f=o(h)
}
\]

---

## 3. Lower-order terms are negligible

\[
\boxed{
f=o(g)
\Rightarrow
g+f=\Theta(g)
}
\]

These three will appear repeatedly when comparing complexity expressions.

---

# 28. Common Mistakes

## Mistake 1 — Thinking Big-O and little-o are interchangeable

Wrong:

\[
f=O(g)\Rightarrow f=o(g)
\]

Correct:

\[
\boxed{f=o(g)\Rightarrow f=O(g)}
\]

---

## Mistake 2 — Reversing the relationship

Wrong:

\[
n=o(n^2)
\Rightarrow
n^2=o(n)
\]

Correct:

\[
n=o(n^2)
\]

only.

---

## Mistake 3 — Thinking constants create little-o

Wrong:

\[
5n=o(n)
\]

Correct:

\[
5n=\Theta(n)
\]

because:

\[
\frac{5n}{n}=5
\]

---

## Mistake 4 — Adding an `O(g)` term and calling the result `o(g)`

Suppose:

\[
f=o(g)
\]

and:

\[
h=O(g)
\]

You can safely conclude:

\[
f+h=O(g)
\]

but not necessarily:

\[
f+h=o(g)
\]

---

## Mistake 5 — Thinking little-o means the function becomes zero

Wrong:

> `f=o(g)` means `f(n)` eventually becomes zero.

Correct:

> `f=o(g)` means the **ratio** `f(n)/g(n)` approaches zero.

For example:

\[
n=o(n^2)
\]

but `n` obviously does not become zero.

---

# 29. A Powerful Mental Model

Think of little-o as:

> **“This function becomes insignificant compared with that function.”**

For example:

\[
n=o(n^2)
\]

means:

> As `n` becomes huge, `n` becomes insignificant compared with `n²`.

Therefore:

\[
n^2+n
\]

is still essentially governed by:

\[
n^2
\]

because:

\[
n=o(n^2)
\]

Similarly:

\[
n^3+n^2+n+1
\]

is governed by:

\[
n^3
\]

because:

\[
n^2=o(n^3)
\]

\[
n=o(n^3)
\]

\[
1=o(n^3)
\]

---

# 30. Final Mental Picture

Think about the growth hierarchy:

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

Every `≪` represents a little-o relationship.

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
n^2=o(2^n)
\]

Little-o tells us:

> **How far apart two growth rates are in an asymptotic sense.**

---

# 31. Quick Revision

### Definition

\[
\boxed{
f=o(g)
\iff
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

### ε-definition

\[
\boxed{
\forall\epsilon>0,\exists N:
n>N\Rightarrow
|f(n)|<\epsilon|g(n)|
}
\]

### Big-O relationship

\[
\boxed{
f=o(g)\Rightarrow f=O(g)
}
\]

### Transitivity

\[
\boxed{
f=o(g),\ g=o(h)
\Rightarrow f=o(h)
}
\]

### Addition

\[
\boxed{
o(g)+o(g)=o(g)
}
\]

### Little-o + Big-O

\[
\boxed{
o(g)+O(g)=O(g)
}
\]

### Dominant term

\[
\boxed{
f=o(g)\Rightarrow g+f=\Theta(g)
}
\]

### Direction

\[
\boxed{
f=o(g)\not\Rightarrow g=o(f)
}
\]

### Constant multiplication

\[
\boxed{
f=o(g)\Rightarrow cf=o(g)
}
\]

### Core idea

\[
\boxed{
\text{Little-o = strictly smaller asymptotic growth}
}
\]

---

# 32. What You Should Be Able to Do Now

After Part 8, you should be able to look at relationships such as:

\[
n=o(n^2)
\]

\[
n^2=o(n^3)
\]

and immediately conclude:

\[
n=o(n^3)
\]

You should also understand why:

\[
n^2+n=\Theta(n^2)
\]

because:

\[
n=o(n^2)
\]

And you should know the critical distinction:

\[
5n=O(n)
\]

and:

\[
5n=\Theta(n)
\]

but:

\[
5n\ne o(n)
\]

because the ratio is `5`, not `0`.

---

# Final Takeaway

The most important idea from Part 8 is:

> **Little-o relationships can be combined because they describe relative growth.**

The core properties to remember are:

\[
\boxed{o(g)\subset O(g)}
\]

\[
\boxed{
f=o(g),\ g=o(h)
\Rightarrow
f=o(h)
}
\]

\[
\boxed{
o(g)+o(g)=o(g)
}
\]

\[
\boxed{
g+o(g)=\Theta(g)
}
\]

and most importantly:

\[
\boxed{
f=o(g)
\quad\Longleftrightarrow\quad
\frac{f(n)}{g(n)}\to0
}
\]

Once this becomes natural, comparing complicated complexity expressions becomes much easier.
