# Little-o Notation — Part 5
## Why the Limit Definition and ε-Definition Are Equivalent

---

# 1. Where We Are

We have already learned two definitions of little-o.

### Limit definition

\[
\boxed{
f(n)=o(g(n))
\iff
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

### ε-definition

\[
\boxed{
\forall\epsilon>0,\exists N>0:
n>N
\Rightarrow
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
}
\]

At first, they look completely different.

One uses a **limit**.

The other uses:

- `ε`
- `N`
- `∀`
- `∃`
- inequalities

So the natural question is:

> **Why are these two definitions equivalent?**

The answer is fundamental to understanding asymptotic analysis.

---

# 2. The Main Idea

The two definitions are not two different concepts.

They are two different ways of saying exactly the same thing:

> **The ratio `f(n)/g(n)` can be made arbitrarily close to zero by taking `n` sufficiently large.**

The limit notation is the **short mathematical language**.

The ε-definition is the **fully precise logical meaning**.

---

# 3. First Understand What a Limit Means

Suppose:

\[
\lim_{n\to\infty}h(n)=0
\]

where:

\[
h(n)=\frac{f(n)}{g(n)}
\]

What does this statement actually mean?

It means:

> No matter how close to zero you want `h(n)` to become, we can choose `n` sufficiently large so that `h(n)` is that close to zero.

This is exactly what ε describes.

---

# 4. What Does "Close to Zero" Mean?

Suppose we want:

\[
h(n)
\]

to be close to zero.

Choose:

\[
\epsilon=0.1
\]

We want:

\[
|h(n)-0|<0.1
\]

which simplifies to:

\[
|h(n)|<0.1
\]

Now choose an even smaller tolerance:

\[
\epsilon=0.01
\]

We want:

\[
|h(n)|<0.01
\]

Choose:

\[
\epsilon=0.000001
\]

We want:

\[
|h(n)|<0.000001
\]

The limit definition says that this is possible for **every positive ε**, provided we take `n` sufficiently large.

---

# 5. General Definition of a Limit

The formal definition of:

\[
\lim_{n\to\infty}h(n)=L
\]

is:

\[
\boxed{
\forall\epsilon>0,\exists N>0:
n>N
\Rightarrow
|h(n)-L|<\epsilon
}
\]

Now notice something.

For little-o:

\[
h(n)=\frac{f(n)}{g(n)}
\]

and:

\[
L=0
\]

Substitute them into the general limit definition:

\[
\forall\epsilon>0,\exists N:
n>N
\Rightarrow
\left|
\frac{f(n)}{g(n)}-0
\right|<\epsilon
\]

Simplify:

\[
\boxed{
\forall\epsilon>0,\exists N:
n>N
\Rightarrow
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
}
\]

And that is exactly the ε-definition of little-o.

Therefore:

\[
\boxed{
\text{Little-o limit definition}
=
\text{Little-o ε-definition}
}
\]

---

# 6. This Is the Entire Connection

The connection can be summarized as:

```text
General limit:

lim h(n) = L
        ↓
For every ε > 0
        ↓
There exists N
        ↓
For n > N
        ↓
|h(n) - L| < ε
```

For little-o:

```text
h(n) = f(n)/g(n)
L = 0
        ↓
lim f(n)/g(n) = 0
        ↓
For every ε > 0
        ↓
There exists N
        ↓
For n > N
        ↓
|f(n)/g(n)| < ε
        ↓
f(n) = o(g(n))
```

That's the whole reason the definitions are equivalent.

---

# 7. Why Does ε Represent "Arbitrarily Close"?

Suppose:

\[
\lim_{n\to\infty}h(n)=0
\]

Imagine drawing a tiny interval around zero:

\[
(-\epsilon,\epsilon)
\]

For example, if:

\[
\epsilon=0.1
\]

then:

\[
(-0.1,0.1)
\]

The limit says that eventually `h(n)` enters this interval and stays there.

If we make the interval smaller:

\[
\epsilon=0.01
\]

we get:

\[
(-0.01,0.01)
\]

The limit says that eventually `h(n)` enters this smaller interval too.

No matter how tiny we make the interval, eventually `h(n)` enters it.

That is what:

\[
\lim h(n)=0
\]

means.

---

# 8. Example: `1/n → 0`

Consider:

\[
h(n)=\frac1n
\]

We know:

\[
\lim_{n\to\infty}\frac1n=0
\]

Let's understand this using ε.

We need:

\[
\left|\frac1n-0\right|<\epsilon
\]

So:

\[
\frac1n<\epsilon
\]

Solve for `n`:

\[
n>\frac1\epsilon
\]

Therefore choose:

\[
\boxed{
N=\frac1\epsilon
}
\]

Then whenever:

\[
n>N
\]

we have:

\[
\frac1n<\epsilon
\]

This works for **every ε > 0**.

Therefore:

\[
\boxed{
\lim_{n\to\infty}\frac1n=0
}
\]

---

# 9. Connecting This to Little-o

Consider:

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

We know:

\[
\lim_{n\to\infty}\frac1n=0
\]

Therefore:

\[
\boxed{
n=o(n^2)
}
\]

Using the ε-definition, we need:

\[
\frac1n<\epsilon
\]

which gives:

\[
n>\frac1\epsilon
\]

So:

\[
N=\frac1\epsilon
\]

Therefore both definitions lead to exactly the same conclusion.

---

# 10. The Two Directions of the Equivalence

When mathematicians say two definitions are equivalent, logically we need both directions:

### Direction 1

\[
\boxed{
\text{Limit definition}
\Rightarrow
\text{ε-definition}
}
\]

### Direction 2

\[
\boxed{
\text{ε-definition}
\Rightarrow
\text{Limit definition}
}
\]

Let's understand both.

---

# 11. Direction 1: Limit → ε

Suppose:

\[
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
\]

By the formal definition of a limit:

For every:

\[
\epsilon>0
\]

there exists some:

\[
N>0
\]

such that:

\[
n>N
\]

implies:

\[
\left|
\frac{f(n)}{g(n)}-0
\right|<\epsilon
\]

Simplify:

\[
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
\]

Therefore:

\[
\boxed{
\forall\epsilon>0,\exists N:
n>N
\Rightarrow
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
}
\]

which is the ε-definition of:

\[
f=o(g)
\]

Therefore:

\[
\boxed{
\lim\frac{f}{g}=0
\Rightarrow
f=o(g)
}
\]

---

# 12. Direction 2: ε → Limit

Now suppose:

\[
\forall\epsilon>0,\exists N:
n>N
\Rightarrow
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
\]

Let:

\[
h(n)=\frac{f(n)}{g(n)}
\]

Then we have:

\[
\forall\epsilon>0,\exists N:
n>N
\Rightarrow
|h(n)|<\epsilon
\]

But this is precisely the formal definition of:

\[
\lim_{n\to\infty}h(n)=0
\]

Therefore:

\[
\boxed{
f=o(g)
\Rightarrow
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

---

# 13. Therefore They Are Equivalent

Since both directions are true:

\[
\text{Limit definition}
\Rightarrow
\text{ε-definition}
\]

and:

\[
\text{ε-definition}
\Rightarrow
\text{Limit definition}
\]

we conclude:

\[
\boxed{
\text{Limit definition}
\iff
\text{ε-definition}
}
\]

Therefore:

\[
\boxed{
f=o(g)
\iff
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
\iff
\forall\epsilon>0,\exists N:
n>N\Rightarrow
\left|\frac{f(n)}{g(n)}\right|<\epsilon
}
\]

This is one of the most important formulas in your little-o notes.

---

# 14. Why We Usually Use the Limit Definition

If both definitions are equivalent, why don't we always use ε?

Because the limit form is much easier for calculations.

Suppose:

\[
f(n)=n\log n
\]

and:

\[
g(n)=n^2
\]

Using the limit form:

\[
\frac{n\log n}{n^2}
=
\frac{\log n}{n}
\]

and:

\[
\lim_{n\to\infty}\frac{\log n}{n}=0
\]

Therefore:

\[
\boxed{
n\log n=o(n^2)
}
\]

Very short.

The ε-definition would require solving inequalities and explicitly finding an `N`.

---

# 15. Why We Still Learn the ε-Definition

Even though the limit form is easier, the ε-definition is important because it tells us what the limit **really means**.

Without ε, you might think:

> "The ratio gets closer to zero."

But ε tells us exactly what that means:

> For **every** positive tolerance, there is a point after which the ratio stays within that tolerance of zero.

So:

### Limit notation

is the **compact form**.

### ε-definition

is the **precise logical form**.

---

# 16. A Common Misunderstanding About N

A very important point:

\[
N
\]

can depend on:

\[
\epsilon
\]

We can write:

\[
\boxed{N=N(\epsilon)}
\]

For example, for:

\[
\frac1n
\]

we found:

\[
N=\frac1\epsilon
\]

Therefore:

| ε | N |
|---:|---:|
| 0.1 | 10 |
| 0.01 | 100 |
| 0.001 | 1,000 |
| 0.000001 | 1,000,000 |

This is perfectly valid.

The definition does **not** require one single `N` to work for every ε.

---

# 17. Why the Order of Quantifiers Matters

Look carefully:

\[
\boxed{
\forall\epsilon>0,\exists N>0
}
\]

The order is:

```text
First: you choose ε
        ↓
Then: I choose N
```

This is different from:

\[
\exists N>0,\forall\epsilon>0
\]

which would mean:

```text
First: choose one fixed N
        ↓
Then: it must work for every ε
```

That is not how limits work.

For most functions approaching zero, the required threshold becomes larger as ε becomes smaller.

---

# 18. Example Showing Why N Depends on ε

Take:

\[
h(n)=\frac1n
\]

For:

\[
\epsilon=0.1
\]

we need:

\[
n>10
\]

For:

\[
\epsilon=0.001
\]

we need:

\[
n>1000
\]

For:

\[
\epsilon=10^{-6}
\]

we need:

\[
n>10^6
\]

So there cannot generally be one small fixed threshold that works for every possible ε.

Instead:

\[
\boxed{N=N(\epsilon)}
\]

---

# 19. Another Intuitive Interpretation

Imagine you are challenging someone:

> "Show me that `f(n)` becomes negligible compared with `g(n)`."

You choose a challenge:

\[
\epsilon=0.01
\]

They respond:

> "After `N=1000`, the ratio is below 0.01."

You make the challenge harder:

\[
\epsilon=0.000001
\]

They respond:

> "Okay. After some larger `N`, the ratio is below 0.000001."

No matter how small your ε is, they can find an appropriate `N`.

That is little-o.

---

# 20. Why `n = o(n²)` Passes the Challenge

Suppose you challenge:

\[
\epsilon=0.0001
\]

We need:

\[
\frac{n}{n^2}<0.0001
\]

which means:

\[
\frac1n<0.0001
\]

Therefore:

\[
n>10000
\]

So choose:

\[
N=10000
\]

After that:

\[
\frac{n}{n^2}<0.0001
\]

The challenge works.

And this works for **every ε**.

Therefore:

\[
\boxed{n=o(n^2)}
\]

---

# 21. Why `n ≠ o(n)` Fails the Challenge

Now consider:

\[
\frac nn=1
\]

Suppose you choose:

\[
\epsilon=0.5
\]

The condition would require:

\[
1<0.5
\]

which is impossible.

No matter how large `N` is, the ratio remains:

\[
1
\]

Therefore there is no suitable `N`.

Hence:

\[
\boxed{n\ne o(n)}
\]

This demonstrates why the ε-definition is powerful.

---

# 22. Limit Definition vs ε-Definition — Complete Comparison

| Feature | Limit Definition | ε-Definition |
|---|---|---|
| Form | \(\lim f/g=0\) | \(\forall\epsilon,\exists N\) |
| Main idea | Ratio approaches zero | Ratio eventually becomes smaller than every ε |
| Easy for calculations | Yes | Usually harder |
| Mathematical precision | Precise | More explicit |
| Shows meaning of limit | Less directly | Very clearly |
| Used in proofs | Often | Very often |
| Used in everyday complexity calculations | Very often | Less often |

---

# 23. The Deep Mathematical Picture

The two definitions describe the same process:

```text
n becomes larger
       ↓
f(n)/g(n) becomes smaller
       ↓
choose a smaller ε
       ↓
go far enough in n
       ↓
ratio becomes smaller than ε
       ↓
choose an even smaller ε
       ↓
go farther in n
       ↓
ratio becomes smaller again
       ↓
...
       ↓
ratio approaches 0
```

So:

\[
\boxed{
\text{Approaches zero}
=
\text{Eventually below every positive tolerance}
}
\]

---

# 24. Little-o in One Complete Statement

The following three statements mean the same thing:

### Statement 1

\[
\boxed{
f(n)=o(g(n))
}
\]

### Statement 2

\[
\boxed{
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
=0
}
\]

### Statement 3

\[
\boxed{
\forall\epsilon>0,\exists N>0:
n>N
\Rightarrow
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
}
\]

They are simply three levels of expressing the same relationship.

---

# 25. Three Levels of Understanding

You can think about little-o at three levels.

### Level 1 — Intuition

> `f(n)` grows strictly slower than `g(n)`.

---

### Level 2 — Limit

\[
\frac{f(n)}{g(n)}
\rightarrow0
\]

---

### Level 3 — Formal ε-definition

\[
\forall\epsilon>0,\exists N:
n>N
\Rightarrow
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
\]

These are not competing definitions.

They are different ways of expressing the same mathematical idea.

---

# 26. Connection to Big-O

The same style of reasoning appears in Big-O.

### Big-O

\[
f=O(g)
\]

means:

\[
\exists C>0,\exists N:
|f(n)|\le C|g(n)|
\]

There only needs to be **one fixed constant `C`**.

### Little-o

\[
f=o(g)
\]

means:

\[
\forall\epsilon>0,\exists N:
|f(n)|<\epsilon|g(n)|
\]

It must work for **every positive ε**.

This is why:

\[
\boxed{o(g)\subseteq O(g)}
\]

but:

\[
\boxed{O(g)\not\subseteq o(g)}
\]

---

# 27. Final Mental Model

Remember this chain:

```text
Little-o
   ↓
f grows strictly slower than g
   ↓
f(n)/g(n) becomes negligible
   ↓
f(n)/g(n) → 0
   ↓
For every ε > 0
   ↓
There exists N
   ↓
After n > N
   ↓
|f(n)/g(n)| < ε
```

The most important connection is:

\[
\boxed{
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

and:

\[
\boxed{
\forall\epsilon>0,\exists N:
n>N\Rightarrow
\left|\frac{f(n)}{g(n)}\right|<\epsilon
}
\]

are **exactly equivalent**.

---

# 28. Final Cheat Sheet

## Little-o

\[
\boxed{
f=o(g)
}
\]

### Limit form

\[
\boxed{
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

### ε-form

\[
\boxed{
\forall\epsilon>0,\exists N>0:
n>N
\Rightarrow
\left|\frac{f(n)}{g(n)}\right|<\epsilon
}
\]

### Why equivalent?

Because this is simply the formal definition of:

\[
\lim_{n\to\infty}h(n)=0
\]

with:

\[
h(n)=\frac{f(n)}{g(n)}
\]

### Key quantifiers

\[
\boxed{\forall\epsilon>0,\exists N>0}
\]

### Important relationship

\[
\boxed{
N\text{ may depend on }\epsilon
}
\]

### Core interpretation

> **No matter how small ε is, we can go far enough in `n` so that `f(n)` is less than ε times `g(n)`.**

---

# 29. One Sentence to Remember

> **The limit definition says the ratio approaches zero; the ε-definition explains exactly what "approaches zero" means.**

Therefore:

\[
\boxed{
f=o(g)
\iff
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
\iff
\forall\epsilon>0,\exists N:
n>N\Rightarrow
\left|\frac{f(n)}{g(n)}\right|<\epsilon
}
\]

---

## Next Part

Now that we understand the mathematical foundation of little-o, the next important topic is:

**Part 6 — Little-o vs Big-O**

We will deeply compare:

- `∃ C` vs `∀ ε`
- fixed constant vs arbitrarily small factor
- `O(g)` vs `o(g)`
- why `o(g) ⊂ O(g)`
- why the reverse is false
- examples and counterexamples
- the meaning of constant factors in both notations.
