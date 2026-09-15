# Little-o Notation — Part 6
## Little-o vs Big-O

---

# 1. Why Compare Little-o and Big-O?

Big-O and little-o look very similar:

\[
O(g(n))
\]

and:

\[
o(g(n))
\]

But they express **different strengths of asymptotic relationships**.

The most important difference is:

\[
\boxed{
\text{Big-O: some fixed constant}
}
\]

versus:

\[
\boxed{
\text{Little-o: every arbitrarily small constant}
}
\]

Understanding this difference is essential before moving to other asymptotic notations.

---

# 2. Big-O Definition

Recall the formal definition of Big-O:

\[
\boxed{
f(n)=O(g(n))
}
\]

if there exist constants:

\[
C>0
\]

and:

\[
N>0
\]

such that for all:

\[
n>N
\]

we have:

\[
\boxed{
|f(n)|\le C|g(n)|
}
\]

In short:

\[
\boxed{
\exists C>0,\exists N>0:
n>N\Rightarrow |f(n)|\le C|g(n)|
}
\]

---

# 3. Little-o Definition

Little-o is:

\[
\boxed{
f(n)=o(g(n))
}
\]

if for every:

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
\boxed{
|f(n)|<\epsilon|g(n)|
}
\]

In short:

\[
\boxed{
\forall\epsilon>0,\exists N>0:
n>N\Rightarrow |f(n)|<\epsilon|g(n)|
}
\]

---

# 4. The Most Important Difference

Look only at the quantifiers.

### Big-O

\[
\boxed{
\exists C>0
}
\]

### Little-o

\[
\boxed{
\forall\epsilon>0
}
\]

This is the heart of the difference.

---

# 5. What Does `∃ C` Mean?

Big-O says:

\[
\exists C>0
\]

This means:

> There is **at least one fixed constant** that makes the inequality work.

For example:

\[
5n=O(n)
\]

because we can choose:

\[
C=5
\]

Then:

\[
5n\le5n
\]

So Big-O is satisfied.

We don't need the ratio to become smaller than every possible constant.

We only need **one suitable constant**.

---

# 6. What Does `∀ ε` Mean?

Little-o says:

\[
\forall\epsilon>0
\]

This means:

> No matter how small a positive number you choose, the inequality must eventually work.

For example:

\[
\epsilon=0.1
\]

Then eventually:

\[
f(n)<0.1g(n)
\]

Choose:

\[
\epsilon=0.01
\]

Then eventually:

\[
f(n)<0.01g(n)
\]

Choose:

\[
\epsilon=0.000001
\]

Then eventually:

\[
f(n)<0.000001g(n)
\]

And so on.

This is much stronger than Big-O.

---

# 7. The Simplest Example

Consider:

\[
f(n)=n
\]

and:

\[
g(n)=n
\]

### Big-O

\[
\frac{f(n)}{g(n)}
=
\frac nn
=
1
\]

The ratio is bounded by the constant `1`.

Therefore:

\[
\boxed{
n=O(n)
}
\]

### Little-o

For little-o we need:

\[
\frac nn\rightarrow0
\]

But:

\[
1\rightarrow1
\]

not zero.

Therefore:

\[
\boxed{
n\ne o(n)
}
\]

So:

\[
\boxed{
n=O(n)
\quad\text{but}\quad
n\ne o(n)
}
\]

This single example shows that Big-O does not imply little-o.

---

# 8. Why Big-O Allows the Same Growth Rate

Big-O asks:

> "Can `f(n)` stay below some constant multiple of `g(n)`?"

For:

\[
f(n)=n
\]

and:

\[
g(n)=n
\]

yes.

Choose:

\[
C=1
\]

Then:

\[
n\le n
\]

Therefore:

\[
n=O(n)
\]

Big-O does not require `f` to be strictly smaller asymptotically.

---

# 9. Why Little-o Rejects the Same Growth Rate

Little-o asks something stronger:

> "Can `f(n)` eventually become smaller than **every positive multiple** of `g(n)`?"

For:

\[
f(n)=n
\]

and:

\[
g(n)=n
\]

we would need:

\[
n<\epsilon n
\]

Divide by `n`:

\[
1<\epsilon
\]

But choose:

\[
\epsilon=0.5
\]

Then:

\[
1<0.5
\]

which is impossible.

Therefore:

\[
\boxed{
n\ne o(n)
}
\]

---

# 10. Big-O Allows Constant Factors

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

This is a fixed constant.

Therefore:

\[
\boxed{
5n=O(n)
}
\]

Choose:

\[
C=5
\]

and:

\[
5n\le5n
\]

The Big-O condition is satisfied.

---

# 11. Little-o Does Not Allow a Fixed Positive Ratio

For little-o:

\[
\frac{5n}{n}=5
\]

We need:

\[
\frac{5n}{n}\rightarrow0
\]

But:

\[
5\rightarrow5
\]

Therefore:

\[
\boxed{
5n\ne o(n)
}
\]

The constant factor does not disappear here.

---

# 12. Important Clarification About Constants

You may have learned in Big-O:

> "We ignore constants."

That statement needs to be understood carefully.

For example:

\[
5n=O(n)
\]

and:

\[
n=O(n)
\]

because Big-O intentionally ignores constant-factor differences in growth classification.

But when testing little-o:

\[
\frac{5n}{n}=5
\]

and the ratio must approach:

\[
0
\]

It doesn't.

Therefore:

\[
5n\ne o(n)
\]

So:

> **Constants are harmless for Big-O classification, but a nonzero constant ratio prevents a little-o relationship.**

---

# 13. The Ratio View

There is an extremely useful way to compare the two notations.

Look at:

\[
R(n)=\frac{|f(n)|}{|g(n)|}
\]

### Big-O

We need:

\[
\boxed{
R(n)\le C
}
\]

for some fixed constant `C`, eventually.

So the ratio only needs to be **bounded**.

---

### Little-o

We need:

\[
\boxed{
R(n)\rightarrow0
}
\]

So the ratio must become **arbitrarily small**.

---

# 14. Visual Comparison

Think of the ratio:

\[
R(n)=\frac{f(n)}{g(n)}
\]

### Big-O

```text
R(n)

 C ─────────────────────── fixed upper bound
       ╲
        ╲
         ╲
          ╲
           ╲____________
────────────────────────────→ n
```

The ratio is allowed to remain around a positive constant.

---

### Little-o

```text
R(n)

       ╲
        ╲
         ╲
          ╲
           ╲
            ╲____________  → 0
────────────────────────────→ n
```

The ratio must approach zero.

---

# 15. Little-o Is Strictly Stronger

Because little-o requires:

\[
\frac{f(n)}{g(n)}\rightarrow0
\]

it automatically gives us a Big-O relationship.

Therefore:

\[
\boxed{
f=o(g)\Rightarrow f=O(g)
}
\]

But:

\[
\boxed{
f=O(g)\not\Rightarrow f=o(g)
}
\]

This is one of the most important relationships to remember.

---

# 16. Proof: `o(g) ⊆ O(g)`

Suppose:

\[
f=o(g)
\]

By the ε-definition:

\[
\forall\epsilon>0,\exists N:
|f(n)|<\epsilon|g(n)|
\]

Choose:

\[
\epsilon=1
\]

Then there exists some `N` such that:

\[
|f(n)|<|g(n)|
\]

for all:

\[
n>N
\]

Therefore:

\[
|f(n)|\le1|g(n)|
\]

So choose:

\[
C=1
\]

This satisfies the Big-O definition.

Therefore:

\[
\boxed{
f=o(g)\Rightarrow f=O(g)
}
\]

---

# 17. Why the Reverse Is False

To prove that:

\[
O(g)\not\subseteq o(g)
\]

we need a counterexample.

Take:

\[
f(n)=n
\]

and:

\[
g(n)=n
\]

We know:

\[
n=O(n)
\]

But:

\[
n\ne o(n)
\]

Therefore:

\[
\boxed{
O(g)\not\subseteq o(g)
}
\]

So little-o is a **proper subset** of Big-O.

---

# 18. Set Relationship

We can visualize the relationship as:

```text
          O(g)
┌───────────────────────────────┐
│                               │
│        ┌──────────────┐       │
│        │    o(g)      │       │
│        │              │       │
│        └──────────────┘       │
│                               │
└───────────────────────────────┘
```

Therefore:

\[
\boxed{
o(g)\subsetneq O(g)
}
\]

The symbol:

\[
\subsetneq
\]

means **proper subset**.

---

# 19. Examples

## Example 1

\[
n=o(n^2)
\]

Therefore:

\[
n=O(n^2)
\]

Both are true.

---

## Example 2

\[
\log n=o(n)
\]

Therefore:

\[
\log n=O(n)
\]

Both are true.

---

## Example 3

\[
n\log n=o(n^2)
\]

Therefore:

\[
n\log n=O(n^2)
\]

Both are true.

---

## Example 4

\[
n=O(n)
\]

but:

\[
n\ne o(n)
\]

Only Big-O is true.

---

## Example 5

\[
5n=O(n)
\]

but:

\[
5n\ne o(n)
\]

Again, only Big-O is true.

---

# 20. `Θ` Helps Complete the Picture

Big-O alone doesn't distinguish between:

- same growth
- strictly slower growth

For example:

\[
n=O(n)
\]

and:

\[
n=o(n^2)
\]

Both are Big-O relationships.

But `Θ` tells us when two functions have the same asymptotic growth:

\[
n=\Theta(n)
\]

while:

\[
n\ne\Theta(n^2)
\]

Little-o tells us the opposite kind of relationship:

\[
n=o(n^2)
\]

So:

- `Θ` → same asymptotic growth
- `o` → strictly slower growth
- `O` → upper bound

---

# 21. Three Important Relationships

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
\boxed{
n=o(n^2)
}
\]

and therefore:

\[
\boxed{
n=O(n^2)
}
\]

But:

\[
\boxed{
n\ne\Theta(n^2)
}
\]

because they do not have the same growth rate.

---

# 22. A Complete Comparison

| Property | Big-O | Little-o | Θ |
|---|---|---|---|
| Meaning | Upper bound | Strictly slower | Same growth |
| Ratio behavior | Bounded above | → 0 | → positive constant |
| Constant factor allowed | Yes | No positive constant ratio | Yes |
| Same growth allowed | Yes | No | Yes |
| Example | `n = O(n)` | `n = o(n²)` | `n = Θ(n)` |
| Strictly slower allowed | Yes | Yes | No |
| Strength | Weakest of these | Stronger | Different purpose |

---

# 23. The Ratio Classification

For positive functions, consider:

\[
L=
\lim_{n\to\infty}\frac{f(n)}{g(n)}
\]

The result gives a powerful classification.

### If:

\[
L=0
\]

then:

\[
\boxed{
f=o(g)
}
\]

---

### If:

\[
0<L<\infty
\]

then:

\[
\boxed{
f=\Theta(g)
}
\]

---

### If:

\[
L=\infty
\]

then `f` grows faster than `g`.

Therefore:

\[
\boxed{
f\not=o(g)
}
\]

---

# 24. Why Little-o Is Called "Strict"

Suppose:

\[
f=O(g)
\]

This only tells us:

> `f` doesn't grow faster than a constant multiple of `g`.

It does not tell us whether:

\[
f
\]

and:

\[
g
\]

grow at the same rate.

Little-o removes that ambiguity.

If:

\[
f=o(g)
\]

then we know:

\[
\boxed{
f\text{ grows strictly slower than }g
}
\]

There is no possibility of them having the same asymptotic growth.

---

# 25. Another Important Example

Consider:

\[
f(n)=n^2+n
\]

and:

\[
g(n)=n^2
\]

First:

\[
\frac{f(n)}{g(n)}
=
\frac{n^2+n}{n^2}
\]

Simplify:

\[
=1+\frac1n
\]

Take the limit:

\[
\lim_{n\to\infty}
\left(1+\frac1n\right)
=
1
\]

Therefore:

\[
\boxed{
n^2+n=\Theta(n^2)
}
\]

and:

\[
\boxed{
n^2+n=O(n^2)
}
\]

but:

\[
\boxed{
n^2+n\ne o(n^2)
}
\]

Why?

Because the ratio approaches `1`, not `0`.

---

# 26. Example of Genuine Little-o

Consider:

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
\frac1n+\frac1{n^2}
\rightarrow0
\]

Therefore:

\[
\boxed{
n^2+n=o(n^3)
}
\]

and consequently:

\[
\boxed{
n^2+n=O(n^3)
}
\]

---

# 27. A Useful Mental Model

Think of the three notations like this:

### Big-O

> "Stay within some fixed multiple."

\[
\boxed{
f\le Cg
}
\]

---

### Little-o

> "Eventually become smaller than every positive fraction."

\[
\boxed{
f<\epsilon g
}
\]

for every:

\[
\epsilon>0
\]

---

### Θ

> "Stay between two fixed positive multiples."

\[
\boxed{
c_1g\le f\le c_2g
}
\]

for suitable positive constants.

---

# 28. The Constant-Factor Difference

This is worth memorizing.

### Big-O

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
5n\ne o(n)
\]

because:

\[
\frac{5n}{n}=5\ne0
\]

---

### Θ

\[
5n=\Theta(n)
\]

because they have the same growth rate.

Therefore:

\[
\boxed{
5n=\Theta(n)=O(n)
}
\]

but:

\[
\boxed{
5n\ne o(n)
}
\]

---

# 29. Direction Matters

If:

\[
f=o(g)
\]

then:

\[
f=O(g)
\]

But we cannot reverse the functions.

For example:

\[
n=o(n^2)
\]

does not mean:

\[
n^2=o(n)
\]

In fact:

\[
\frac{n^2}{n}=n\rightarrow\infty
\]

Therefore:

\[
n^2\ne o(n)
\]

So little-o is directional.

---

# 30. Common Mistakes

## Mistake 1

Thinking:

\[
O(g)=o(g)
\]

Wrong.

Little-o is strictly stronger.

---

## Mistake 2

Thinking:

\[
f<g
\Rightarrow
f=o(g)
\]

Wrong.

Example:

\[
n-1<n
\]

but:

\[
n-1\ne o(n)
\]

---

## Mistake 3

Thinking:

> "Constants are ignored, so `5n=o(n)`."

Wrong.

The ratio is:

\[
5
\]

not:

\[
0
\]

---

## Mistake 4

Thinking:

\[
f=O(g)
\Rightarrow
f=o(g)
\]

Wrong.

Counterexample:

\[
n=O(n)
\]

but:

\[
n\ne o(n)
\]

---

## Mistake 5

Thinking:

\[
f=o(g)
\]

means:

\[
f(n)\rightarrow0
\]

Wrong.

Example:

\[
n=o(n^2)
\]

while:

\[
n\rightarrow\infty
\]

---

# 31. Quick Decision Method

When comparing `f(n)` and `g(n)`:

### Step 1

Calculate:

\[
\frac{f(n)}{g(n)}
\]

### Step 2

Find:

\[
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
\]

### Step 3

Interpret the result.

| Limit | Conclusion |
|---:|---|
| `0` | \(f=o(g)\) |
| Positive finite constant | \(f=\Theta(g)\) |
| `∞` | `f` grows faster |
| Does not exist | Need further analysis |

---

# 32. Big-O vs Little-o in One Example

Consider:

\[
f(n)=n
\]

and:

\[
g(n)=n^2
\]

Ratio:

\[
\frac{n}{n^2}
=
\frac1n
\]

Limit:

\[
\frac1n\rightarrow0
\]

Therefore:

\[
\boxed{
n=o(n^2)
}
\]

Since little-o implies Big-O:

\[
\boxed{
n=O(n^2)
}
\]

So one calculation establishes both.

---

# 33. The Deepest Difference

Big-O asks:

> **Is `f` eventually no more than some fixed multiple of `g`?**

Little-o asks:

> **Does `f` eventually become smaller than every positive multiple of `g`, no matter how tiny that multiple is?**

That is why little-o is stronger.

---

# 34. Final Relationship Diagram

```text
                Asymptotic Relationships

                       O(g)
              ┌───────────────────┐
              │                   │
              │     o(g)          │
              │   ┌─────────┐     │
              │   │         │     │
              │   │  o(g)   │     │
              │   │         │     │
              │   └─────────┘     │
              │                   │
              └───────────────────┘

          o(g) ⊂ O(g)
```

And separately:

```text
f = o(g)
    ↓
f grows strictly slower than g
    ↓
f = O(g)

BUT

f = O(g)
    ✘
does NOT imply
f = o(g)
```

---

# 35. Final Cheat Sheet

## Big-O

\[
\boxed{
f=O(g)
\iff
\exists C>0,\exists N:
|f(n)|\le C|g(n)|
}
\]

Meaning:

> `f` is eventually bounded by **some fixed multiple** of `g`.

---

## Little-o

\[
\boxed{
f=o(g)
\iff
\forall\epsilon>0,\exists N:
|f(n)|<\epsilon|g(n)|
}
\]

Meaning:

> `f` is eventually smaller than **every arbitrarily small multiple** of `g`.

---

## Ratio View

### Big-O

\[
\boxed{
\frac{f(n)}{g(n)}
\text{ is eventually bounded}
}
\]

### Little-o

\[
\boxed{
\frac{f(n)}{g(n)}
\rightarrow0
}
\]

---

## Relationship

\[
\boxed{
o(g)\subsetneq O(g)
}
\]

or:

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

---

## Examples

\[
\boxed{
n=o(n^2)
}
\]

\[
\boxed{
n=O(n^2)
}
\]

\[
\boxed{
n=O(n)
}
\]

\[
\boxed{
n\ne o(n)
}
\]

\[
\boxed{
5n=O(n)
}
\]

\[
\boxed{
5n\ne o(n)
}
\]

\[
\boxed{
5n=\Theta(n)
}
\]

---

# 36. One Sentence to Remember

> **Big-O says "some fixed multiple is enough"; little-o says "no matter how small a positive multiple you demand, eventually it is enough."**

Or even shorter:

\[
\boxed{
\text{Big-O = bounded}
\qquad
\text{Little-o = approaches zero}
}
\]

That distinction is the foundation for understanding the rest of asymptotic notation.
