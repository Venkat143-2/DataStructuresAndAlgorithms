# Little-o Notation — Part 4
## The ε-Definition

---

# 1. Why Do We Need an ε-Definition?

In Part 3, we learned the limit definition:

\[
\boxed{
f(n)=o(g(n))
\iff
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

This is easy to use for calculations.

But there is a deeper question:

> What does it **actually mean** when we say that a ratio approaches zero?

For example:

\[
\lim_{n\to\infty}\frac{1}{n}=0
\]

We informally say:

> "`1/n` gets closer and closer to zero."

But mathematics needs a precise meaning for **"closer and closer."**

That is where **ε (epsilon)** comes in.

---

# 2. The Core Idea of ε

The symbol:

\[
\epsilon
\]

is called **epsilon**.

In the ε-definition, ε represents:

> **Any positive amount of error/tolerance, no matter how small.**

For example, we could choose:

\[
\epsilon=0.1
\]

or:

\[
\epsilon=0.001
\]

or:

\[
\epsilon=0.000001
\]

or even:

\[
\epsilon=10^{-100}
\]

The important point is:

\[
\boxed{\epsilon>0}
\]

and we are allowed to choose it **as small as we want**.

---

# 3. The ε-Definition of Little-o

The formal definition is:

\[
\boxed{
f(n)=o(g(n))
}
\]

if and only if:

\[
\boxed{
\forall\epsilon>0,\ \exists N>0
\text{ such that if }n>N,
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
}
\]

An equivalent form is:

\[
\boxed{
\forall\epsilon>0,\ \exists N>0:
n>N
\Rightarrow
|f(n)|<\epsilon|g(n)|
}
\]

This is one of the most important definitions in asymptotic analysis.

---

# 4. Breaking the Definition Into Pieces

The formula looks complicated:

\[
\forall\epsilon>0,\ \exists N>0:
n>N
\Rightarrow
|f(n)|<\epsilon|g(n)|
\]

Let's break it down.

---

## Part 1 — `∀ ε > 0`

\[
\forall\epsilon>0
\]

means:

> **For every positive epsilon.**

It doesn't matter whether ε is:

```text
0.5
0.1
0.01
0.0001
0.0000001
```

The definition must work for **all** of them.

---

## Part 2 — `∃ N > 0`

\[
\exists N>0
\]

means:

> There exists some threshold `N`.

This `N` can depend on the chosen ε.

That is extremely important.

We are **not** required to find one universal `N` that works for every ε.

Instead:

\[
N=N(\epsilon)
\]

may change when ε changes.

---

## Part 3 — `n > N`

\[
n>N
\]

means:

> Once `n` becomes sufficiently large...

We don't care about what happens before the threshold.

Little-o is concerned with the behavior as:

\[
n\to\infty
\]

---

## Part 4 — The Required Inequality

\[
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
\]

means:

> Eventually, the ratio becomes smaller than the chosen ε.

Or equivalently:

\[
|f(n)|<\epsilon|g(n)|
\]

---

# 5. Plain-English Translation

The complete definition:

\[
\forall\epsilon>0,\ \exists N>0:
n>N
\Rightarrow
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
\]

can be translated into:

> **No matter how small a positive number ε you choose, I can find a sufficiently large input size N such that after that point, `f(n)` is less than ε times `g(n)`.**

This is the real meaning of little-o.

---

# 6. The Most Important Phrase: "No Matter How Small"

Suppose:

\[
f(n)=o(g(n))
\]

Then we must be able to make:

\[
\frac{f(n)}{g(n)}
\]

smaller than:

\[
0.1
\]

and:

\[
0.01
\]

and:

\[
0.001
\]

and:

\[
0.000001
\]

and any other positive value.

That is why little-o represents **strictly smaller asymptotic growth**.

---

# 7. Example: Proving `n = o(n²)`

We already know:

\[
n=o(n^2)
\]

because:

\[
\lim_{n\to\infty}\frac{n}{n^2}=0
\]

Now let's prove it using the ε-definition.

We need to show:

\[
\forall\epsilon>0,\exists N:
n>N
\Rightarrow
\frac{n}{n^2}<\epsilon
\]

Simplify:

\[
\frac{1}{n}<\epsilon
\]

We need to find an `N` that guarantees this.

---

## Solve the inequality

Start with:

\[
\frac1n<\epsilon
\]

Multiply by `n`:

\[
1<\epsilon n
\]

Divide by ε:

\[
\frac1\epsilon<n
\]

Therefore:

\[
n>\frac1\epsilon
\]

So choose:

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
n>\frac1\epsilon
\]

which gives:

\[
\frac1n<\epsilon
\]

Therefore:

\[
\boxed{n=o(n^2)}
\]

---

# 8. Understanding the N We Found

We found:

\[
N=\frac1\epsilon
\]

Notice something important.

If:

\[
\epsilon=0.1
\]

then:

\[
N=10
\]

If:

\[
\epsilon=0.01
\]

then:

\[
N=100
\]

If:

\[
\epsilon=0.001
\]

then:

\[
N=1000
\]

So:

| ε | Required N |
|---:|---:|
| 0.1 | 10 |
| 0.01 | 100 |
| 0.001 | 1,000 |
| 0.0001 | 10,000 |

The smaller ε becomes, the larger `N` may need to be.

That is completely valid.

---

# 9. The Relationship Between ε and N

This is a very important concept.

Think of it as:

```text
You choose ε
      ↓
I find N
      ↓
After n > N
      ↓
ratio < ε
```

For example:

```text
ε = 0.01
       ↓
N = 100
       ↓
for every n > 100
       ↓
1/n < 0.01
```

Then:

```text
ε = 0.000001
       ↓
N = 1,000,000
       ↓
for every n > 1,000,000
       ↓
1/n < 0.000001
```

The threshold changes.

That's expected.

---

# 10. ε Does NOT Mean a Fixed Number

A common misunderstanding is:

> "ε is some specific value."

No.

ε is a **variable representing an arbitrary positive tolerance**.

The definition says:

\[
\boxed{\text{For EVERY }\epsilon>0}
\]

not:

\[
\text{For ONE }\epsilon
\]

This difference is fundamental.

---

# 11. Why "For Every ε" Is So Powerful

Suppose someone says:

> "Eventually the ratio becomes smaller than 0.1."

That alone isn't enough to establish little-o.

Maybe the ratio eventually stays around:

\[
0.05
\]

Then it is smaller than `0.1`, but it is not getting arbitrarily close to zero.

Little-o requires:

\[
\frac{f(n)}{g(n)}<0.1
\]

and also:

\[
\frac{f(n)}{g(n)}<0.01
\]

and:

\[
\frac{f(n)}{g(n)}<0.001
\]

and so on.

Therefore:

\[
\boxed{\text{For every }\epsilon>0}
\]

is the key requirement.

---

# 12. Why `n = O(n)` but `n ≠ o(n)`

This becomes very clear using ε.

For little-o we would need:

\[
n<\epsilon n
\]

for sufficiently large `n`.

Divide by `n`:

\[
1<\epsilon
\]

But little-o requires this to work for **every**:

\[
\epsilon>0
\]

Choose:

\[
\epsilon=0.5
\]

Then we would need:

\[
1<0.5
\]

which is impossible.

Therefore:

\[
\boxed{n\ne o(n)}
\]

---

# 13. Why `5n ≠ o(n)`

Suppose:

\[
5n=o(n)
\]

Then the ε-definition would require:

\[
5n<\epsilon n
\]

Divide by `n`:

\[
5<\epsilon
\]

But choose:

\[
\epsilon=1
\]

Then we would need:

\[
5<1
\]

which is impossible.

Therefore:

\[
\boxed{5n\ne o(n)}
\]

---

# 14. Why `n - 1 ≠ o(n)`

Suppose:

\[
n-1=o(n)
\]

Then eventually:

\[
n-1<\epsilon n
\]

Divide by `n`:

\[
1-\frac1n<\epsilon
\]

Choose:

\[
\epsilon=0.5
\]

For sufficiently large `n`:

\[
1-\frac1n
\]

gets close to `1`, not below `0.5`.

Therefore the condition cannot remain true.

So:

\[
\boxed{n-1\ne o(n)}
\]

---

# 15. The "Arbitrarily Small Factor" Interpretation

The ε-definition can be written as:

\[
|f(n)|<\epsilon|g(n)|
\]

This is extremely important.

It says:

> Eventually, `f(n)` can be bounded by **any arbitrarily small constant multiple** of `g(n)`.

For example, we can eventually have:

\[
f(n)<0.1g(n)
\]

Then:

\[
f(n)<0.01g(n)
\]

Then:

\[
f(n)<0.001g(n)
\]

Then:

\[
f(n)<0.000001g(n)
\]

and so on.

This is the heart of little-o.

---

# 16. Compare This With Big-O

Big-O says:

\[
f(n)=O(g(n))
\]

if:

\[
\exists C>0,\exists N:
n>N
\Rightarrow
|f(n)|\le C|g(n)|
\]

Notice the difference.

### Big-O

\[
\boxed{\exists C}
\]

There is **some fixed constant** `C`.

### Little-o

\[
\boxed{\forall\epsilon>0}
\]

It must work for **every arbitrarily small positive constant**.

---

# 17. Side-by-Side Comparison

| Concept | Big-O | Little-o |
|---|---|---|
| Constant | `C` | `ε` |
| Quantifier | `∃ C > 0` | `∀ ε > 0` |
| Meaning | Some fixed multiple | Arbitrarily small multiple |
| Requirement | Eventually bounded | Eventually negligible |
| Same growth allowed? | Yes | No |
| Example | `5n = O(n)` | `5n ≠ o(n)` |
| Example | `n = O(n)` | `n ≠ o(n)` |
| Strictly slower | Not required | Required |

---

# 18. Why Little-o Implies Big-O

Suppose:

\[
f=o(g)
\]

By definition:

\[
\forall\epsilon>0,\exists N:
|f(n)|<\epsilon|g(n)|
\]

Choose just one particular value:

\[
\epsilon=1
\]

Then:

\[
|f(n)|<|g(n)|
\]

for sufficiently large `n`.

This is exactly a Big-O bound with:

\[
C=1
\]

Therefore:

\[
\boxed{
f=o(g)\Rightarrow f=O(g)
}
\]

So every little-o relationship is also a Big-O relationship.

But the reverse is not true.

---

# 19. Visualizing the Difference

### Big-O

```text
f(n) ≤ C · g(n)

       C·g(n)
          /
         /
        /    f(n)
       /    /
      /    /
-----/----/------------→ n
```

The function only needs to stay below **one fixed multiple** of `g(n)`.

---

### Little-o

```text
f(n) < ε · g(n)

ε can be:

0.1
0.01
0.001
0.000001
...
```

The function must eventually fit below **every arbitrarily small multiple** of `g(n)`.

That is much stronger.

---

# 20. The Most Important Quantifier Difference

Remember this:

### Big-O

\[
\boxed{
\exists C>0
}
\]

means:

> "There is **some** constant that works."

### Little-o

\[
\boxed{
\forall\epsilon>0
}
\]

means:

> "No matter how small the constant you give me, I can eventually make it work."

This is the fundamental difference between the two notations.

---

# 21. Why `f(n) < g(n)` Is Not Enough

Suppose:

\[
f(n)<g(n)
\]

You might think:

\[
f=o(g)
\]

But consider:

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

But:

\[
\frac{n-1}{n}
=
1-\frac1n
\rightarrow1
\]

So:

\[
n-1\ne o(n)
\]

The reason is simple:

`f` is smaller than `g`, but it is **not becoming an arbitrarily small fraction of `g`**.

---

# 22. Another Way to Understand ε

Imagine `g(n)` is a large pizza.

If:

\[
f(n)=0.5g(n)
\]

then `f` is half the pizza.

If:

\[
f(n)=0.1g(n)
\]

then it is one-tenth.

If:

\[
f(n)=0.001g(n)
\]

then it is only one-thousandth.

Little-o says:

> As `n` grows, the fraction represented by `f` can be made smaller than **any positive fraction you choose**.

Eventually, `f` becomes negligible compared with `g`.

---

# 23. What "Eventually" Means

The word **eventually** appears throughout asymptotic analysis.

It means:

> There exists some point after which the required condition always holds.

For little-o:

\[
\exists N:
n>N
\Rightarrow
|f(n)|<\epsilon|g(n)|
\]

The condition does **not** need to hold for every small `n`.

It only needs to hold after some sufficiently large threshold.

This is why asymptotic analysis ignores finite initial behavior.

---

# 24. Example With an Initial Failure

Suppose:

\[
f(n)=n
\]

and:

\[
g(n)=n^2
\]

Choose:

\[
\epsilon=0.01
\]

We need:

\[
n<0.01n^2
\]

For positive `n`:

\[
1<0.01n
\]

Therefore:

\[
n>100
\]

So:

\[
N=100
\]

For:

\[
n>100
\]

the condition holds.

It doesn't matter whether it fails for:

\[
n=1,2,3,\ldots,100
\]

Little-o only cares about sufficiently large `n`.

---

# 25. A General Proof Strategy

To prove:

\[
f(n)=o(g(n))
\]

using ε, follow these steps:

### Step 1

Start with:

\[
|f(n)|<\epsilon|g(n)|
\]

### Step 2

Solve the inequality for `n`.

### Step 3

Find an appropriate threshold:

\[
N=N(\epsilon)
\]

### Step 4

Show that whenever:

\[
n>N
\]

the inequality holds.

### Step 5

Since ε was arbitrary:

\[
\boxed{f(n)=o(g(n))}
\]

---

# 26. Limit Definition vs ε-Definition

There are two equivalent ways to define little-o.

### Limit form

\[
\boxed{
\lim_{n\to\infty}
\frac{f(n)}{g(n)}
=0
}
\]

### ε form

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

They express the **same mathematical idea**.

The limit form is usually easier for calculations.

The ε-definition is more precise and rigorous.

---

# 27. Why the Absolute Value Appears

The formal definition uses:

\[
\left|
\frac{f(n)}{g(n)}
\right|<\epsilon
\]

because limits describe closeness to zero regardless of whether the expression approaches zero from the positive or negative side.

For example:

\[
-\frac1n\rightarrow0
\]

and:

\[
\left|-\frac1n\right|
=
\frac1n
\rightarrow0
\]

For algorithmic complexity, functions are normally non-negative, so the absolute value often doesn't change the practical calculation.

---

# 28. The Three Key Words

When reading the ε-definition, focus on these three ideas:

\[
\boxed{\forall\epsilon}
\]

### 1. EVERY ε

You choose any positive tolerance.

---

\[
\boxed{\exists N}
\]

### 2. SOME N

I can find a sufficiently large threshold for that ε.

---

\[
\boxed{n>N}
\]

### 3. EVENTUALLY

After that threshold, the condition always holds.

---

# 29. The Mental Model

Remember:

```text
Little-o
   ↓
Choose ANY ε > 0
   ↓
I must find SOME N
   ↓
After n > N
   ↓
|f(n)| < ε|g(n)|
   ↓
f(n) is an arbitrarily small
fraction of g(n)
   ↓
f(n) grows strictly slower
than g(n)
```

---

# 30. Final Cheat Sheet

### Little-o limit definition

\[
\boxed{
f=o(g)
\iff
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

### Little-o ε-definition

\[
\boxed{
\forall\epsilon>0,\exists N>0:
n>N
\Rightarrow
|f(n)|<\epsilon|g(n)|
}
\]

### Meaning

> `f(n)` eventually becomes an arbitrarily small fraction of `g(n)`.

### Key quantifier

\[
\boxed{\forall\epsilon>0}
\]

### Threshold

\[
\boxed{N=N(\epsilon)}
\]

### Relationship with Big-O

\[
\boxed{o(g)\subseteq O(g)}
\]

### Examples

\[
\boxed{n=o(n^2)}
\]

\[
\boxed{\log n=o(n)}
\]

\[
\boxed{n\log n=o(n^2)}
\]

### Not little-o

\[
\boxed{n\ne o(n)}
\]

\[
\boxed{5n\ne o(n)}
\]

\[
\boxed{n-1\ne o(n)}
\]

---

# 31. The One Sentence to Remember

> **Little-o means that for every positive ε, no matter how small, there is some sufficiently large N after which `f(n)` is smaller than ε times `g(n)`.**

Or even simpler:

\[
\boxed{
\text{Little-o = eventually smaller than EVERY positive fraction of }g(n)
}
\]

---

## What Comes Next?

We now have two definitions:

\[
\boxed{
\lim_{n\to\infty}\frac{f(n)}{g(n)}=0
}
\]

and:

\[
\boxed{
\forall\epsilon>0,\exists N:
|f(n)|<\epsilon|g(n)|
}
\]

The next question is:

> **Why are these two definitions actually equivalent?**

That is the purpose of **Part 5 — Why the Limit Definition and ε-Definition Are Equivalent**.
