# Little-o Notation — Part 3
## The Limit Definition of Little-o

---

## 1. The Mathematical Definition

The most commonly used mathematical definition of little-o is:

\[
\boxed{
f(n)=o(g(n))
\iff
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

This is the central equation of little-o notation.

It tells us exactly how to determine whether `f(n)` grows strictly slower than `g(n)`.

---

# 2. What Does the Formula Mean?

Consider:

\[
\frac{f(n)}{g(n)}
\]

This ratio tells us:

> **How large is `f(n)` compared with `g(n)`?**

Now let `n` become extremely large.

We ask:

\[
\lim_{n\to\infty}\frac{f(n)}{g(n)}
\]

If the answer is:

\[
0
\]

then `f(n)` becomes negligible compared with `g(n)`.

Therefore:

\[
\boxed{f(n)=o(g(n))}
\]

---

# 3. Why Does the Ratio Need to Approach Zero?

Suppose:

\[
f(n)=n
\]

and:

\[
g(n)=n^2
\]

The ratio is:

\[
\frac{f(n)}{g(n)}
=
\frac{n}{n^2}
=
\frac1n
\]

Consider increasingly large values of `n`:

| `n` | `f(n)=n` | `g(n)=n²` | `f(n)/g(n)` |
|---:|---:|---:|---:|
| 10 | 10 | 100 | 0.1 |
| 100 | 100 | 10,000 | 0.01 |
| 1,000 | 1,000 | 1,000,000 | 0.001 |
| 10,000 | 10,000 | 100,000,000 | 0.0001 |
| 1,000,000 | 1,000,000 | 1,000,000,000,000 | 0.000001 |

The ratio keeps getting closer to zero.

Therefore:

\[
\lim_{n\to\infty}\frac{n}{n^2}=0
\]

and:

\[
\boxed{n=o(n^2)}
\]

---

# 4. Important: `f(n)` Does Not Have to Approach Zero

This is one of the most important points in little-o.

Consider:

\[
f(n)=n
\]

As:

\[
n\to\infty
\]

we have:

\[
f(n)\to\infty
\]

So `f(n)` definitely does **not** approach zero.

But:

\[
n=o(n^2)
\]

because:

\[
\frac{n}{n^2}
=
\frac1n
\rightarrow0
\]

Therefore:

> **Little-o requires the ratio `f(n)/g(n)` to approach zero, not `f(n)` itself.**

---

# 5. The Ratio Is a Relative Measurement

Think of:

\[
\frac{f(n)}{g(n)}
\]

as a measurement of the size of `f` **relative to** `g`.

For example:

\[
\frac{f(n)}{g(n)}=0.5
\]

means `f` is half the size of `g`.

If:

\[
\frac{f(n)}{g(n)}=0.01
\]

then `f` is only 1% of `g`.

If:

\[
\frac{f(n)}{g(n)}=0.000001
\]

then `f` is only 0.0001% of `g`.

If this ratio approaches zero:

\[
\frac{f(n)}{g(n)}\rightarrow0
\]

then `f` becomes negligible compared with `g`.

---

# 6. Example: `log n = o(n)`

Let:

\[
f(n)=\log n
\]

and:

\[
g(n)=n
\]

Calculate the ratio:

\[
\frac{f(n)}{g(n)}
=
\frac{\log n}{n}
\]

A standard limit result is:

\[
\lim_{n\to\infty}\frac{\log n}{n}=0
\]

Therefore:

\[
\boxed{\log n=o(n)}
\]

This tells us that logarithmic growth is strictly slower than linear growth.

---

# 7. Example: `n log n = o(n²)`

Let:

\[
f(n)=n\log n
\]

and:

\[
g(n)=n^2
\]

Calculate:

\[
\frac{f(n)}{g(n)}
=
\frac{n\log n}{n^2}
\]

Simplify:

\[
=
\frac{\log n}{n}
\]

We already know:

\[
\frac{\log n}{n}\rightarrow0
\]

Therefore:

\[
\boxed{n\log n=o(n^2)}
\]

---

# 8. Example: `n² = o(n³)`

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
\frac{f(n)}{g(n)}
=
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
\boxed{n^2=o(n^3)}
\]

---

# 9. Example Where Little-o Is False: `n = o(n)`

Let:

\[
f(n)=n
\]

and:

\[
g(n)=n
\]

Calculate:

\[
\frac{f(n)}{g(n)}
=
\frac nn
=
1
\]

Therefore:

\[
\lim_{n\to\infty}1=1
\]

The result is not zero.

So:

\[
\boxed{n\ne o(n)}
\]

However:

\[
\boxed{n=O(n)}
\]

and:

\[
\boxed{n=\Theta(n)}
\]

This is an important example because it demonstrates that **same growth is not little-o**.

---

# 10. Example: `5n ≠ o(n)`

Consider:

\[
f(n)=5n
\]

and:

\[
g(n)=n
\]

The ratio is:

\[
\frac{5n}{n}=5
\]

Therefore:

\[
\lim_{n\to\infty}5=5
\]

Since:

\[
5\ne0
\]

we conclude:

\[
\boxed{5n\ne o(n)}
\]

But:

\[
\boxed{5n=O(n)}
\]

and:

\[
\boxed{5n=\Theta(n)}
\]

The constant factor does not disappear when comparing the ratio.

---

# 11. Example: `n - 1 ≠ o(n)`

Consider:

\[
f(n)=n-1
\]

and:

\[
g(n)=n
\]

Calculate:

\[
\frac{n-1}{n}
=
1-\frac1n
\]

Taking the limit:

\[
\lim_{n\to\infty}
\left(1-\frac1n\right)
=
1
\]

Therefore:

\[
\boxed{n-1\ne o(n)}
\]

Even though:

\[
n-1<n
\]

for positive `n`.

This proves:

> **Being smaller is not enough for little-o.**

The ratio must approach zero.

---

# 12. What Different Limit Results Tell Us

Suppose:

\[
L=
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
\]

Then the value of `L` gives us useful information.

### Case 1: `L = 0`

\[
\boxed{f=o(g)}
\]

`f` grows strictly slower.

---

### Case 2: `L = c`

where:

\[
0<c<\infty
\]

Then `f` and `g` have the same asymptotic growth scale.

Typically:

\[
\boxed{f=\Theta(g)}
\]

---

### Case 3: `L = \infty`

Then `f` grows faster than `g`.

Therefore:

\[
\boxed{f\ne o(g)}
\]

---

# 13. A Very Useful Comparison Table

| `lim f(n)/g(n)` | Interpretation |
|---:|---|
| `0` | `f` grows strictly slower → \(f=o(g)\) |
| Positive finite constant | Same asymptotic growth → \(f=\Theta(g)\) |
| `∞` | `f` grows faster |
| Does not exist | Cannot directly classify using this simple limit |

For standard positive algorithm-complexity functions, this is an extremely useful first test.

---

# 14. Little-o Is Directional

Suppose:

\[
n=o(n^2)
\]

Now reverse the functions:

\[
\frac{n^2}{n}=n
\]

and:

\[
n\rightarrow\infty
\]

Therefore:

\[
n^2\ne o(n)
\]

So:

\[
\boxed{
f=o(g)
\not\Rightarrow
g=o(f)
}
\]

Little-o describes a **directional growth relationship**.

---

# 15. The Growth Hierarchy Through Limits

Consider:

\[
\log n,\quad n,\quad n\log n,\quad n^2,\quad n^3
\]

We can verify relationships using ratios.

### Logarithm vs linear

\[
\frac{\log n}{n}\rightarrow0
\]

Therefore:

\[
\boxed{\log n=o(n)}
\]

### Linear vs `n log n`

\[
\frac{n}{n\log n}
=
\frac1{\log n}
\rightarrow0
\]

Therefore:

\[
\boxed{n=o(n\log n)}
\]

### `n log n` vs quadratic

\[
\frac{n\log n}{n^2}
=
\frac{\log n}{n}
\rightarrow0
\]

Therefore:

\[
\boxed{n\log n=o(n^2)}
\]

### Quadratic vs cubic

\[
\frac{n^2}{n^3}
=
\frac1n
\rightarrow0
\]

Therefore:

\[
\boxed{n^2=o(n^3)}
\]

---

# 16. A General Polynomial Rule

Suppose:

\[
f(n)=n^a
\]

and:

\[
g(n)=n^b
\]

where:

\[
a<b
\]

Then:

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
\frac1{n^{b-a}}\rightarrow0
\]

Therefore:

\[
\boxed{
n^a=o(n^b)
\quad\text{when }a<b
}
\]

### Example

\[
n^3=o(n^7)
\]

because:

\[
\frac{n^3}{n^7}
=
\frac1{n^4}
\rightarrow0
\]

---

# 17. A General Constant-Factor Rule

Suppose:

\[
f(n)=cn^a
\]

and:

\[
g(n)=n^b
\]

where `c` is a fixed positive constant and:

\[
a<b
\]

Then:

\[
\frac{cn^a}{n^b}
=
\frac{c}{n^{b-a}}
\rightarrow0
\]

Therefore:

\[
\boxed{cn^a=o(n^b)}
\]

For example:

\[
100n^2=o(n^5)
\]

because:

\[
\frac{100n^2}{n^5}
=
\frac{100}{n^3}
\rightarrow0
\]

---

# 18. Little-o and Algorithm Complexity

Suppose:

\[
T_1(n)=n
\]

and:

\[
T_2(n)=n^2
\]

Then:

\[
\frac{T_1(n)}{T_2(n)}
=
\frac1n
\rightarrow0
\]

Therefore:

\[
\boxed{T_1(n)=o(T_2(n))}
\]

This means:

> The running time of the first algorithm becomes negligible compared with the running time of the second as the input size grows.

This is a statement about **asymptotic growth**, not necessarily about the actual measured runtime for every input.

---

# 19. Common Mistakes

### Mistake 1: Thinking `f(n) < g(n)` is enough

Wrong:

\[
f(n)<g(n)
\Rightarrow
f=o(g)
\]

Counterexample:

\[
n-1<n
\]

but:

\[
n-1\ne o(n)
\]

---

### Mistake 2: Thinking `f(n)` must approach zero

Wrong:

\[
f(n)\rightarrow0
\]

is not required.

Example:

\[
n=o(n^2)
\]

even though:

\[
n\rightarrow\infty
\]

---

### Mistake 3: Ignoring constant factors

Wrong:

\[
5n=o(n)
\]

because:

\[
\frac{5n}{n}=5
\]

not zero.

---

### Mistake 4: Reversing the relationship

From:

\[
n=o(n^2)
\]

you cannot conclude:

\[
n^2=o(n)
\]

---

### Mistake 5: Confusing Big-O with little-o

Correct:

\[
5n=O(n)
\]

Incorrect:

\[
5n=o(n)
\]

Correct:

\[
n=o(n^2)
\]

---

# 20. The Limit Test — Your Main Tool

When you need to determine whether:

\[
f(n)=o(g(n))
\]

follow these steps.

### Step 1: Form the ratio

\[
\frac{f(n)}{g(n)}
\]

### Step 2: Simplify

Cancel common factors and simplify the expression.

### Step 3: Take the limit

\[
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
\]

### Step 4: Check the result

If:

\[
\boxed{0}
\]

then:

\[
\boxed{f=o(g)}
\]

---

# 21. The Core Idea Behind the Limit

The statement:

\[
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
=0
\]

means:

> As `n` becomes arbitrarily large, `f(n)` becomes an arbitrarily small fraction of `g(n)`.

This is the precise mathematical meaning of:

> **`f(n)` grows strictly slower than `g(n)`.**

---

# 22. Connection to the ε-Definition

The limit definition:

\[
\boxed{
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
=0
}
\]

will later give us the formal ε-definition.

The statement:

> "The ratio approaches zero"

means:

> "No matter how small a positive number `ε` you choose, eventually the ratio becomes smaller than `ε`."

That gives:

\[
\boxed{
\left|
\frac{f(n)}{g(n)}
\right|
<\epsilon
}
\]

for sufficiently large `n`.

Equivalently:

\[
\boxed{
|f(n)|<\epsilon|g(n)|
}
\]

This is the foundation of the next part.

---

# 23. Final Mental Model

Remember the entire limit definition using this sequence:

```text
Compare f(n) and g(n)
        ↓
Form the ratio
        ↓
     f(n)
     ────
     g(n)
        ↓
Take n → ∞
        ↓
Does the ratio → 0?
        ↓
      YES
        ↓
   f(n) = o(g(n))
        ↓
f grows strictly slower
than g
```

The central formula is:

\[
\boxed{
f(n)=o(g(n))
\iff
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
=0
}
\]

And the most important interpretation is:

> **Little-o does not mean that `f(n)` becomes zero. It means that `f(n)` becomes negligible relative to `g(n)`.**
