# Big-O Notation — Set 3: C, n₀, Eventually, Constants, and Lower-Order Terms

> **Questions covered**
>
> 1. What does the constant `C` mean?
> 2. What does `n₀` mean?
> 3. Why do we say "eventually"?
> 4. Why do we ignore constants?
> 5. Why do we ignore lower-order terms?

---

# 1. What Does the Constant C Mean?

Before understanding `C`, remember the formal definition of Big-O:

```text
f(n) = O(g(n))
```

means there exist constants:

```text
C > 0
n₀ > 0
```

such that:

```text
f(n) ≤ C × g(n)
```

for every:

```text
n ≥ n₀
```

The most important part for this question is:

```text
C × g(n)
```

---

## 1.1 What Is C?

`C` is a **fixed positive constant** used to create an upper bound for `f(n)`.

In simple words:

> **C gives us some fixed amount of "room" above `g(n)` so that `f(n)` can fit underneath it eventually.**

For example:

```text
f(n) = 3n + 10
```

We want to prove:

```text
f(n) = O(n)
```

We need:

```text
3n + 10 ≤ Cn
```

We could choose:

```text
C = 4
```

Then:

```text
3n + 10 ≤ 4n
```

which becomes:

```text
10 ≤ n
```

Therefore it is true for:

```text
n ≥ 10
```

So:

```text
C = 4
n₀ = 10
```

and:

```text
3n + 10 = O(n)
```

---

# 1.2 Why Do We Need C?

This is a very important question.

Suppose Big-O required:

```text
f(n) ≤ g(n)
```

instead of:

```text
f(n) ≤ Cg(n)
```

Then:

```text
3n
```

would NOT be considered:

```text
O(n)
```

because:

```text
3n ≤ n
```

is false.

But `3n` clearly has **linear growth**.

So we allow a constant multiplier:

```text
3n ≤ 3n
```

Therefore:

```text
3n = O(n)
```

The constant `C` allows us to ignore fixed multiplicative differences while still describing the same growth class.

---

# 1.3 C Does Not Depend on n

This is extremely important.

`C` must be a constant.

For example:

```text
C = 5
```

is valid.

But:

```text
C = n
```

is NOT valid.

Why?

Because:

```text
n
```

changes as the input changes.

A constant must remain fixed.

```text
C = 5
```

means:

```text
5, 5, 5, 5, 5, ...
```

It does not become:

```text
5, 10, 15, 20, ...
```

---

# 1.4 C Is Not Necessarily the "Best" Constant

There can be many valid values of `C`.

Suppose:

```text
f(n) = 3n + 10
```

We found:

```text
C = 4
```

works for:

```text
n ≥ 10
```

But perhaps:

```text
C = 5
```

also works.

And:

```text
C = 10
```

also works.

The Big-O definition only asks:

> **Does there exist some positive constant C that makes the inequality true eventually?**

It does not require the smallest possible `C`.

---

# 1.5 Visual Meaning of C

Think of:

```text
g(n)
```

as a curve.

Then:

```text
Cg(n)
```

is the same growth pattern but scaled vertically.

For example:

```text
g(n) = n

Cg(n) = 4n
```

Conceptually:

```text
Growth
  ↑
  │
  │                   4n
  │                 /
  │               /
  │             /
  │           /
  │         /
  │       /     n
  │     /     /
  │   /     /
  │ /     /
  └────────────────→ n
```

The constant `C` changes the scale.

It does **not** change the fundamental growth type.

---

# 1.6 The Mental Model for C

Whenever you see:

```text
f(n) = O(g(n))
```

think:

```text
Can I find some fixed C
such that:

f(n) ≤ Cg(n)

eventually?
```

If yes:

```text
f(n) = O(g(n))
```

---

# 2. What Does n₀ Mean?

Now let's look at the second important constant.

```text
n₀
```

is pronounced:

> "n-zero"

---

## 2.1 Simple Definition

`n₀` is the **threshold input size** from which the Big-O inequality must remain true.

In other words:

> **n₀ tells us from where the asymptotic upper bound starts being guaranteed.**

---

# 2.2 Example

Take:

```text
f(n) = 3n + 10
```

and choose:

```text
C = 4
```

We need:

```text
3n + 10 ≤ 4n
```

Simplify:

```text
10 ≤ n
```

Therefore:

```text
n ≥ 10
```

So we can choose:

```text
n₀ = 10
```

Our complete Big-O proof is:

```text
C = 4
n₀ = 10
```

and:

```text
3n + 10 ≤ 4n
```

for every:

```text
n ≥ 10
```

Therefore:

```text
3n + 10 = O(n)
```

---

# 2.3 Why Do We Need n₀?

Because asymptotic analysis is concerned with **large input sizes**.

We don't require the bound to work from:

```text
n = 1
```

We only require it to work from some point onward.

This allows us to focus on the behavior that matters as the input becomes large.

---

# 2.4 Think of n₀ as a Starting Line

Imagine a race.

```text
n = 1       n = 2       n = 3       ...       n₀
  │           │           │                    │
  ├───────────┴───────────┴────────────────────┤
                                                 ↓
                                      Big-O guarantee starts
```

Before `n₀`:

```text
The inequality may or may not hold.
```

From `n₀` onward:

```text
The inequality must hold.
```

So:

```text
n₀ = starting point of the asymptotic guarantee
```

---

# 2.5 C and n₀ Work Together

The formal definition says:

```text
f(n) ≤ Cg(n)
```

for:

```text
n ≥ n₀
```

So:

```text
C
↓
How much vertical room do we allow?

n₀
↓
From where must the guarantee hold?
```

Together:

```text
        Cg(n)
          │
          │   Upper bound
          │
          ↓
    ─────────────────
         ↑
        n₀
         │
         │
         ↓
   Guarantee starts
```

---

# 3. Why Do We Say "Eventually"?

The word **eventually** is one of the most important words in asymptotic analysis.

---

## 3.1 What Does Eventually Mean?

In Big-O:

> **Eventually means for all sufficiently large values of n.**

Mathematically:

```text
for every n ≥ n₀
```

---

# 3.2 Why Not Require It for Every n?

Because Big-O is designed to study **growth for large inputs**.

Consider:

```text
f(n) = n² + 100n
```

For small `n`, the `100n` term may have a large effect.

For large `n`, the `n²` term dominates.

We care about the long-term growth.

---

# 3.3 Example

Suppose:

```text
f(n) = n + 100
```

We want to show:

```text
f(n) = O(n)
```

Choose:

```text
C = 2
```

Then:

```text
n + 100 ≤ 2n
```

which means:

```text
100 ≤ n
```

Therefore the inequality is guaranteed when:

```text
n ≥ 100
```

So:

```text
n₀ = 100
```

For:

```text
n < 100
```

the inequality might fail.

But that does not matter for this Big-O proof.

From:

```text
n = 100
```

onward, it works.

Therefore:

```text
n + 100 = O(n)
```

---

# 3.4 "Eventually" Does Not Mean "Sometimes"

This is a common misunderstanding.

Big-O does NOT mean:

```text
The inequality works for some large n.
```

It means:

```text
The inequality works for EVERY n ≥ n₀.
```

That distinction is very important.

Correct:

```text
∃ C > 0, ∃ n₀ > 0
such that

∀ n ≥ n₀:

f(n) ≤ Cg(n)
```

The symbol:

```text
∀
```

means:

> for every.

---

# 3.5 Why Large n Is Important

Imagine two functions:

```text
f(n) = n
g(n) = n²
```

At small values:

```text
n = 1

n = n²
```

At:

```text
n = 10
```

we have:

```text
10 < 100
```

At:

```text
n = 1,000
```

we have:

```text
1,000 < 1,000,000
```

The difference becomes increasingly obvious.

Asymptotic analysis is interested in this long-term behavior.

---

# 4. Why Do We Ignore Constants?

This question needs an important clarification.

We don't literally "ignore" constants because they are meaningless.

We ignore them when determining the **asymptotic growth class**.

---

# 4.1 Example

Consider:

```text
f(n) = 5n
```

and:

```text
g(n) = 500n
```

Both grow linearly.

Therefore:

```text
5n = O(n)

500n = O(n)
```

The constants:

```text
5
500
```

change the actual amount of work.

But they do not change the growth category:

```text
linear
```

---

# 4.2 Why Is the Constant Ignored?

Suppose:

```text
f(n) = 5n
```

and:

```text
g(n) = n
```

We can say:

```text
5n ≤ 5n
```

Therefore:

```text
f(n) = O(n)
```

The factor `5` is absorbed into the constant `C`.

That's the mathematical reason.

---

# 4.3 Constants Affect Real Performance

This is extremely important.

Suppose:

```text
Algorithm A:
T(n) = 2n

Algorithm B:
T(n) = 1,000,000n
```

Both are:

```text
O(n)
```

But Algorithm B can be dramatically slower in practice.

Therefore:

> **Ignoring constants in Big-O does not mean constants don't matter in real programs.**

It means they don't change the asymptotic growth category.

---

# 4.4 Why Is Growth More Important?

Compare:

```text
A = 1,000,000n
```

and:

```text
B = n²
```

At:

```text
n = 10
```

we get:

```text
A = 10,000,000

B = 100
```

So A is much larger.

But eventually:

```text
n²
```

grows faster than:

```text
1,000,000n
```

Find the crossover:

```text
1,000,000n = n²
```

For:

```text
n > 1,000,000
```

we have:

```text
n² > 1,000,000n
```

This shows why asymptotic analysis focuses on growth.

---

# 4.5 Constants Change the Scale, Not the Growth Type

Think:

```text
n
2n
100n
1,000,000n
```

They all have:

```text
Linear growth
```

Similarly:

```text
n²
10n²
500n²
```

all have:

```text
Quadratic growth
```

Therefore:

```text
5n       → O(n)

500n     → O(n)

10n²     → O(n²)

500n²    → O(n²)
```

---

# 5. Why Do We Ignore Lower-Order Terms?

This is another very important idea.

Consider:

```text
f(n) = n² + 10n + 100
```

We say:

```text
f(n) = O(n²)
```

Why?

Because as `n` becomes large, the `n²` term grows much faster than the lower-order terms.

---

# 5.1 What Is a Lower-Order Term?

In:

```text
n² + 10n + 100
```

the terms have different growth rates:

```text
n²     → quadratic
10n    → linear
100    → constant
```

So:

```text
n²
```

is the dominant term.

The other terms are lower-order terms.

---

# 5.2 Compare Their Growth

Consider:

```text
n = 10
```

Then:

```text
n² = 100
10n = 100
100 = 100
```

All three are significant.

But consider:

```text
n = 1,000
```

Then:

```text
n² = 1,000,000
10n = 10,000
100 = 100
```

Now:

```text
n²
```

is much larger.

At:

```text
n = 1,000,000
```

we get:

```text
n²       = 1,000,000,000,000
10n      = 10,000,000
100      = 100
```

Now the difference is enormous.

---

# 5.3 The Ratio Becomes the Key

Consider:

```text
n² + 10n + 100
```

Compare the linear term to the quadratic term:

```text
10n / n²
```

Simplify:

```text
10/n
```

As:

```text
n → ∞
```

we get:

```text
10/n → 0
```

Similarly:

```text
100/n² → 0
```

Therefore, compared with `n²`, the lower-order terms become relatively insignificant as `n` becomes very large.

---

# 5.4 Why This Does Not Mean the Terms Disappear

This is another important distinction.

When we say:

```text
n² + 10n + 100 = O(n²)
```

we are NOT saying:

```text
10n = 0
```

or:

```text
100 = 0
```

They are still part of the actual function.

We are saying:

> **They do not determine the dominant asymptotic growth.**

---

# 5.5 Example

Suppose:

```text
T(n) = 4n² + 20n + 100
```

The dominant term is:

```text
4n²
```

The constant `4` can be absorbed into the Big-O constant.

Therefore:

```text
T(n) = O(n²)
```

More tightly:

```text
T(n) = Θ(n²)
```

---

# 5.6 Another Example

Consider:

```text
T(n) = 7n³ + 20n² + 100n + 50
```

Growth rates:

```text
n³
↓
n²
↓
n
↓
1
```

The dominant term is:

```text
n³
```

Therefore:

```text
T(n) = O(n³)
```

and more tightly:

```text
T(n) = Θ(n³)
```

---

# 5.7 General Rule

For a polynomial:

```text
f(n) = aₖnᵏ + aₖ₋₁nᵏ⁻¹ + ... + a₁n + a₀
```

the highest power:

```text
nᵏ
```

dominates as `n` becomes large, assuming its coefficient is nonzero.

Therefore:

```text
f(n) = O(nᵏ)
```

and more precisely:

```text
f(n) = Θ(nᵏ)
```

---

# 6. Constants vs Lower-Order Terms

These two ideas are related but different.

## Constants

Example:

```text
5n
```

The `5` is a multiplicative constant.

We classify:

```text
5n → O(n)
```

---

## Lower-Order Terms

Example:

```text
n² + 10n + 100
```

The terms:

```text
10n
100
```

grow more slowly than:

```text
n²
```

So:

```text
n² + 10n + 100 → O(n²)
```

---

# 7. Why Does Big-O Ignore Both?

Because Big-O is interested in the **asymptotic growth class**.

For example:

```text
2n + 50
```

and:

```text
1,000,000n + 999,999
```

both have:

```text
Linear growth
```

So both are:

```text
O(n)
```

Likewise:

```text
3n² + 100n + 500
```

and:

```text
900n² + 10n + 1
```

both have:

```text
Quadratic growth
```

So both are:

```text
O(n²)
```

---

# 8. The Deeper Reason

The entire idea can be understood as:

```text
Exact function
      ↓
Contains many details
      ↓
Constants
      ↓
Lower-order terms
      ↓
Dominant growth remains
      ↓
Asymptotic classification
```

For example:

```text
T(n) = 500n² + 1000n + 5000
```

Remove only the details that don't determine the dominant growth:

```text
500n²
```

Then absorb the constant:

```text
n²
```

Therefore:

```text
T(n) = O(n²)
```

---

# 9. A Very Important Warning

Do not think:

> "Big-O ignores constants because constants don't matter."

The correct statement is:

> **Big-O ignores multiplicative constants and lower-order terms when describing asymptotic growth because they do not change the dominant growth class.**

They absolutely can matter in real-world performance.

---

# 10. Complete Mental Model

The formal definition:

```text
f(n) = O(g(n))
```

means:

```text
∃ C > 0
∃ n₀ > 0

such that

f(n) ≤ Cg(n)

for every n ≥ n₀
```

Now understand every part:

```text
C
│
└── Fixed multiplier
    Gives g(n) enough room to bound f(n)


n₀
│
└── Starting point
    From here onward the bound must hold


Eventually
│
└── For EVERY n ≥ n₀


Ignore constants
│
└── Fixed multipliers don't change growth class


Ignore lower-order terms
│
└── Slower-growing terms don't determine dominant growth
```

---

# 11. One Complete Example

Consider:

```text
f(n) = 3n² + 10n + 20
```

We want:

```text
f(n) = O(n²)
```

Choose:

```text
C = 4
```

We need:

```text
3n² + 10n + 20 ≤ 4n²
```

Move terms:

```text
10n + 20 ≤ n²
```

For sufficiently large `n`, this becomes true.

For example, at `n = 12`:

```text
10(12) + 20 = 140

12² = 144
```

So the inequality holds from a suitable threshold onward.

Therefore there exist suitable:

```text
C > 0
n₀ > 0
```

such that:

```text
3n² + 10n + 20 ≤ Cn²
```

for every:

```text
n ≥ n₀
```

Therefore:

```text
3n² + 10n + 20 = O(n²)
```

And the reason we finally write only:

```text
O(n²)
```

is that:

```text
3
```

is a constant and:

```text
10n + 20
```

are lower-order compared with:

```text
n²
```

---

# 12. Quick Revision

| Concept                  | Meaning                                                 |
| ------------------------ | ------------------------------------------------------- |
| `C`                      | Fixed positive constant multiplier                      |
| `n₀`                     | Threshold from which the bound must hold                |
| Eventually               | For every `n ≥ n₀`                                      |
| Ignore constants         | Multiplicative constants don't change asymptotic growth |
| Ignore lower-order terms | Slower-growing terms don't determine dominant growth    |

---

# 13. Final Mental Model

Remember this picture:

```text
                 f(n)
                   │
                   │
                   │
                   ↓
            ┌─────────────┐
            │             │
            │   Cg(n)     │
            │             │
            └─────────────┘
                   │
                   │
                   ↓
              n₀ starts
              the guarantee
                   │
                   ↓
        ───────────────────────→ n
```

And remember the sentence:

> **`C` gives the upper bound a constant amount of room, `n₀` tells us where the guarantee starts, and "eventually" means the guarantee must hold for every input size from `n₀` onward.**

Finally:

> **Constants and lower-order terms are ignored only when classifying asymptotic growth, because they do not change the dominant growth rate.**

---

# One-Line Revision

```text
f(n) = O(g(n))
```

means:

> **There exists a fixed constant `C` and a threshold `n₀` such that, for every `n ≥ n₀`, `f(n) ≤ Cg(n)`; Big-O focuses on this eventual growth, so fixed constants and slower-growing terms do not change the asymptotic growth class.**
