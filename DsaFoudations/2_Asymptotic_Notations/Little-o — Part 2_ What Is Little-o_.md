# Little-o Notation — Part 2
## What Is Little-o?

---

## 1. What Is Little-o?

**Little-o notation** is an asymptotic notation used to describe when one function grows **strictly slower** than another function as the input size becomes very large.

We write:

\[
\boxed{f(n)=o(g(n))}
\]

and read it as:

> "`f(n)` is little-o of `g(n)`."

The central idea is:

> **`f(n)` becomes negligible compared with `g(n)` as `n` approaches infinity.**

This is stronger than simply saying:

\[
f(n)<g(n)
\]

---

# 2. The Main Idea: Strictly Slower Growth

Suppose:

\[
f(n)=n
\]

and:

\[
g(n)=n^2
\]

As `n` becomes larger, `n²` grows much faster than `n`.

Consider some values:

| `n` | `f(n)=n` | `g(n)=n²` |
|---:|---:|---:|
| 10 | 10 | 100 |
| 100 | 100 | 10,000 |
| 1,000 | 1,000 | 1,000,000 |
| 10,000 | 10,000 | 100,000,000 |

The difference in growth becomes increasingly large.

More importantly, the ratio becomes:

\[
\frac{f(n)}{g(n)}
=
\frac{n}{n^2}
=
\frac1n
\]

and:

\[
\frac1n\rightarrow0
\]

Therefore:

\[
\boxed{n=o(n^2)}
\]

This means that `n` becomes negligible compared with `n²`.

---

# 3. Little-o Is About Relative Growth

This is one of the most important ideas.

Little-o does **not** ask whether `f(n)` itself becomes small.

Instead, it asks:

> **How large is `f(n)` compared with `g(n)`?**

We therefore look at:

\[
\boxed{\frac{f(n)}{g(n)}}
\]

If this ratio approaches zero, then:

\[
\boxed{f(n)=o(g(n))}
\]

---

## Example

Let:

\[
f(n)=n
\]

and:

\[
g(n)=n^2
\]

Then:

\[
\frac{f(n)}{g(n)}
=
\frac1n
\]

As `n` becomes very large:

\[
\frac1n\rightarrow0
\]

Therefore:

\[
n=o(n^2)
\]

Notice:

\[
n\rightarrow\infty
\]

It is **not** becoming zero.

Only its **relative size compared with `n²`** becomes zero.

---

# 4. Little-o Does Not Mean `f(n) → 0`

This is a very common misconception.

Suppose:

\[
f(n)=n
\]

Then:

\[
f(n)\rightarrow\infty
\]

Yet:

\[
n=o(n^2)
\]

Why?

Because:

\[
\frac{n}{n^2}
=
\frac1n
\rightarrow0
\]

Therefore:

> **Little-o does not require `f(n)` to approach zero.**

It requires:

\[
\boxed{\frac{f(n)}{g(n)}\rightarrow0}
\]

---

# 5. Why "Smaller" Is Not Enough

Suppose:

\[
f(n)=n-1
\]

and:

\[
g(n)=n
\]

We always have:

\[
n-1<n
\]

So `f(n)` is strictly smaller than `g(n)`.

But does that mean:

\[
n-1=o(n)?
\]

No.

Let's compare their relative size:

\[
\frac{n-1}{n}
=
1-\frac1n
\]

As:

\[
n\rightarrow\infty
\]

we get:

\[
1-\frac1n\rightarrow1
\]

The ratio approaches `1`, not `0`.

Therefore:

\[
\boxed{n-1\ne o(n)}
\]

---

# 6. What Actually Makes Little-o Different?

Compare these two situations.

### Situation A

\[
f(n)=n
\]

\[
g(n)=n^2
\]

Ratio:

\[
\frac{n}{n^2}
=
\frac1n
\rightarrow0
\]

Therefore:

\[
\boxed{n=o(n^2)}
\]

`f` becomes negligible relative to `g`.

---

### Situation B

\[
f(n)=5n
\]

\[
g(n)=n
\]

Ratio:

\[
\frac{5n}{n}=5
\]

The ratio does not approach zero.

Therefore:

\[
\boxed{5n\ne o(n)}
\]

Even though Big-O allows:

\[
5n=O(n)
\]

---

# 7. Little-o and the Growth Rate

Little-o describes a **strict difference in asymptotic growth rates**.

For example:

\[
\log n=o(n)
\]

because:

\[
\frac{\log n}{n}\rightarrow0
\]

Similarly:

\[
n=o(n^2)
\]

because:

\[
\frac{n}{n^2}\rightarrow0
\]

And:

\[
n^2=o(n^3)
\]

because:

\[
\frac{n^2}{n^3}
=
\frac1n
\rightarrow0
\]

---

# 8. Common Growth Hierarchy

A useful general growth hierarchy is:

\[
\boxed{
1
<
\log n
<
n
<
n\log n
<
n^2
<
n^3
<
2^n
<
n!
}
\]

The `<` symbol here represents increasing asymptotic growth, not simply numerical comparison for every possible input.

For many standard functions, these relationships can be expressed using little-o:

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
\boxed{n^2=o(n^3)}
\]

\[
\boxed{n^3=o(2^n)}
\]

and:

\[
\boxed{2^n=o(n!)}
\]

for sufficiently large `n`.

---

# 9. Little-o Is Directional

Little-o has a direction.

If:

\[
n=o(n^2)
\]

you cannot reverse the relationship.

It is **not** true that:

\[
n^2=o(n)
\]

Check the ratio:

\[
\frac{n^2}{n}=n
\]

and:

\[
n\rightarrow\infty
\]

not zero.

Therefore:

\[
\boxed{n^2\ne o(n)}
\]

So:

\[
\boxed{f=o(g)\not\Rightarrow g=o(f)}
\]

---

# 10. Same Growth Is Not Little-o

Consider:

\[
f(n)=n
\]

and:

\[
g(n)=2n
\]

Their ratio is:

\[
\frac{n}{2n}
=
\frac12
\]

The ratio approaches:

\[
\frac12
\]

not zero.

Therefore:

\[
\boxed{n\ne o(2n)}
\]

But:

\[
n=O(2n)
\]

and:

\[
n=\Theta(2n)
\]

This shows why little-o specifically represents **strictly slower growth**, rather than merely "smaller."

---

# 11. The Central Mathematical Definition

Everything we have discussed can now be summarized mathematically.

For appropriate functions `f(n)` and `g(n)`:

\[
\boxed{
f(n)=o(g(n))
}
\]

if:

\[
\boxed{
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
=0
}
\]

This is the most important mathematical definition of little-o.

---

# 12. Understanding the Ratio

The ratio:

\[
\frac{f(n)}{g(n)}
\]

can be thought of as:

> **How large is `f(n)` compared with `g(n)`?**

### If the ratio approaches `0`

\[
\frac{f(n)}{g(n)}\rightarrow0
\]

then:

\[
f=o(g)
\]

`f` becomes negligible relative to `g`.

---

### If the ratio approaches a positive constant

For example:

\[
\frac{f(n)}{g(n)}\rightarrow5
\]

then `f` and `g` have the same asymptotic growth scale.

Typically:

\[
f=\Theta(g)
\]

---

### If the ratio approaches infinity

\[
\frac{f(n)}{g(n)}\rightarrow\infty
\]

then `f` grows faster than `g`.

Therefore:

\[
f\ne o(g)
\]

---

# 13. Little-o Compared with Big-O

This distinction should be completely clear before moving forward.

### Big-O

\[
f(n)=O(g(n))
\]

means:

> `f(n)` is eventually bounded above by some constant multiple of `g(n)`.

For example:

\[
5n=O(n)
\]

because:

\[
5n\le5n
\]

---

### Little-o

\[
f(n)=o(g(n))
\]

means:

> `f(n)` eventually becomes smaller than **every positive fraction** of `g(n)`.

For example:

\[
n=o(n^2)
\]

because eventually:

\[
n<0.1n^2
\]

and eventually:

\[
n<0.001n^2
\]

and eventually:

\[
n<0.000001n^2
\]

and this remains possible no matter how small the positive fraction becomes.

---

# 14. The Key Relationship Between Them

Every little-o relationship is also a Big-O relationship:

\[
\boxed{
f=o(g)\Rightarrow f=O(g)
}
\]

Therefore:

\[
\boxed{
o(g)\subseteq O(g)
}
\]

But the reverse is not necessarily true.

For example:

\[
n=O(n)
\]

but:

\[
n\ne o(n)
\]

Therefore:

\[
\boxed{
O(g)\not\subseteq o(g)
}
\]

---

# 15. A Powerful Mental Model

Think of Big-O and little-o as answering different questions.

### Big-O asks:

> **"Can I find some fixed constant that can bound `f` relative to `g`?"**

\[
|f(n)|\le C|g(n)|
\]

for some `C`.

---

### Little-o asks:

> **"Can `f` eventually become an arbitrarily tiny fraction of `g`?"**

\[
|f(n)|<\epsilon|g(n)|
\]

for every positive `ε`.

---

# 16. Examples to Remember

### Example 1

\[
\boxed{n=o(n^2)}
\]

because:

\[
\frac{n}{n^2}
=
\frac1n
\rightarrow0
\]

---

### Example 2

\[
\boxed{\log n=o(n)}
\]

because:

\[
\frac{\log n}{n}
\rightarrow0
\]

---

### Example 3

\[
\boxed{n\log n=o(n^2)}
\]

because:

\[
\frac{n\log n}{n^2}
=
\frac{\log n}{n}
\rightarrow0
\]

---

### Example 4

\[
\boxed{n\ne o(n)}
\]

because:

\[
\frac nn=1
\]

---

### Example 5

\[
\boxed{5n\ne o(n)}
\]

because:

\[
\frac{5n}{n}=5
\]

---

### Example 6

\[
\boxed{n-1\ne o(n)}
\]

because:

\[
\frac{n-1}{n}
\rightarrow1
\]

---

# 17. Little-o in Algorithm Analysis

Suppose two algorithms have running times:

\[
T_1(n)=n
\]

and:

\[
T_2(n)=n^2
\]

Then:

\[
\boxed{T_1(n)=o(T_2(n))}
\]

This tells us something stronger than simply:

\[
T_1(n)=O(T_2(n))
\]

It tells us:

> As the input becomes very large, the growth of `T₁` becomes negligible compared with the growth of `T₂`.

This is useful for comparing algorithms with genuinely different growth rates.

---

# 18. Important Vocabulary

When you see:

\[
f=o(g)
\]

you should associate it with these phrases:

- Strictly slower growth
- Negligible relative growth
- Ratio approaches zero
- Arbitrarily small fraction
- Stronger than Big-O
- Asymptotically smaller

Avoid describing it simply as:

- "Always smaller"
- "Less than"
- "Smaller for every `n`"

Those descriptions are not precise enough.

---

# 19. Quick Decision Process

When asked whether:

\[
f(n)=o(g(n))
\]

you can use this process:

### Step 1

Form the ratio:

\[
\frac{f(n)}{g(n)}
\]

### Step 2

Take the limit:

\[
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
\]

### Step 3

Check the result.

If:

\[
\boxed{0}
\]

then:

\[
\boxed{f=o(g)}
\]

If it is a non-zero finite constant, they have the same asymptotic growth scale.

If it goes to infinity, `f` grows faster.

---

# 20. Final Mental Model

The entire concept can be remembered with one question:

> **"Does `f(n)` eventually become an arbitrarily small fraction of `g(n)`?"**

If YES:

\[
\boxed{f(n)=o(g(n))}
\]

Mathematically:

\[
\boxed{
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
=0
}
\]

Remember:

```text
f(n) < g(n)
       ↓
Not enough
       ↓
Compare their growth
       ↓
f(n) / g(n)
       ↓
Does the ratio → 0?
       ↓
      YES
       ↓
f(n) = o(g(n))
```

---

## One-Sentence Definition

> **Little-o notation describes a function whose growth becomes negligible compared with another function as the input size approaches infinity.**