# Complexity

## What is Complexity?

In DSA, **complexity means how much time and space are required by an algorithm to solve a problem as the input size increases.**

---

## What is the Meaning of "As Input Size Increases"?

**Input size** means the amount of data given to an algorithm.

For example, if we have an array:

```text
n = 10
```

The input contains 10 elements.

If:

```text
n = 1,000
```

The input contains 1,000 elements.

So, **"as input size increases"** means checking how the time and space required by an algorithm change when the amount of input data becomes larger.

For example:

```text
n = 10
n = 100
n = 1,000
n = 1,000,000
```

We study complexity to understand how an algorithm behaves when the input becomes large.

---

## Why Do We Mention an Algorithm, Not a Program or Data Structure?

An **algorithm** is a set of steps or instructions used to solve a problem.

A **program** is the implementation of an algorithm using a programming language such as C++, Java, or Python.

A **data structure** is a way of organizing and storing data, such as an array, linked list, stack, queue, tree, or hash table.

Complexity is mainly discussed in terms of an **algorithm** because we want to measure how efficiently the steps used to solve a problem perform as the input size increases.

The same algorithm can be implemented in different programming languages, but its fundamental complexity can remain the same.

---

# Time Complexity

## What is Time Complexity?

**Time complexity is the number of operations or the amount of time required by an algorithm to solve a problem as the input size increases.**

In DSA, we usually focus on the **number of operations** rather than actual time in seconds because actual execution time depends on the computer, processor, programming language, compiler, and other factors.

---

## Measuring Algorithm Execution Time

There are two ways to think about how long an algorithm takes.

### Actual Execution Time

We can measure the actual time taken by a program using a timer.

For example:

```text
Algorithm A → 0.5 seconds
Algorithm B → 1.2 seconds
```

But actual execution time is not reliable for analyzing algorithms because it depends on:

* Computer hardware
* Processor speed
* Programming language
* Compiler
* Operating system
* Other running processes

### Counting Operations

Instead of measuring seconds, DSA usually focuses on **counting the number of operations performed by an algorithm**.

For example:

```cpp
for (int i = 0; i < n; i++) {
    cout << i;
}
```

The loop executes approximately `n` times.

Therefore:

```text
Number of operations ≈ n
Time Complexity = O(n)
```

### Important

> **In DSA, we generally analyze time complexity by studying how the number of operations grows with the input size rather than measuring actual execution time in seconds.**

---

## Time Complexity Calculation

To calculate time complexity, we mainly look at **how many times important operations are performed**.

### Example 1 — Constant

```cpp
int sum = a + b;
```

Only a fixed number of operations are performed.

```text
Time Complexity = O(1)
```

### Example 2 — Single Loop

```cpp
for (int i = 0; i < n; i++) {
    cout << i;
}
```

The loop runs `n` times.

```text
Time Complexity = O(n)
```

### Example 3 — Nested Loop

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        cout << i << j;
    }
}
```

The outer loop runs `n` times.

For every outer iteration, the inner loop runs `n` times.

Therefore:

```text
n × n = n²

Time Complexity = O(n²)
```

### Example 4 — Consecutive Loops

```cpp
for (int i = 0; i < n; i++) {
    cout << i;
}

for (int i = 0; i < n; i++) {
    cout << i;
}
```

Total:

```text
n + n = 2n
```

We ignore constants in asymptotic analysis:

```text
O(2n) → O(n)
```

Therefore:

```text
Time Complexity = O(n)
```

### Example 5 — Different Loops

```cpp
for (int i = 0; i < n; i++) {
    // O(n)
}

for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        // O(n²)
    }
}
```

Total:

```text
O(n) + O(n²)
```

The dominant term is `n²`.

Therefore:

```text
Time Complexity = O(n²)
```

### Basic Rules

```text
O(1) + O(n)       → O(n)

O(n) + O(n)       → O(n)

O(n) + O(n²)      → O(n²)

O(n) × O(n)       → O(n²)

O(n) × O(log n)   → O(n log n)
```

The main idea is:

> **Count how the number of operations grows with `n`, then keep the dominant growth term.**

---

## Why Does Time Complexity Matter in Coding?

**Time complexity plays an important role in coding because a problem can be solved in many ways using different algorithms, but some algorithms become slow when the input size becomes large.**

### Simple Example

Suppose you want to search for a number in an array.

### Approach 1 — Linear Search

```cpp
for (int i = 0; i < n; i++) {
    if (arr[i] == target)
        return i;
}
```

**Time Complexity: O(n)**

If:

```text
n = 1,000,000
```

It may need to check up to **1,000,000 elements**.

---

### Approach 2 — Binary Search

If the array is **sorted**, you can use binary search.

**Time Complexity: O(log n)**

For:

```text
n = 1,000,000
```

Binary search needs only around **20 comparisons**.

That's a huge difference.

### Conclusion

Both algorithms solve the **same problem**, but binary search is much more efficient for a sorted array.

Therefore:

> **Time complexity helps us choose an efficient algorithm that can handle large input sizes effectively.**

---

# Space Complexity

## What is Space Complexity?

**Space complexity is the amount of memory (space) required by an algorithm to solve a problem as the input size increases.**

---

## Input Space

**Input space is the memory required to store the input data given to an algorithm.**

For example:

```cpp
int arr[n];
```

If `arr` contains `n` elements, the input requires memory proportional to `n`.

Therefore:

```text
Input Space = O(n)
```

### Example

Suppose:

```text
n = 10
```

The input contains 10 elements.

If:

```text
n = 1,000,000
```

The input contains 1,000,000 elements.

The memory required to store the input grows with `n`.

---

## Auxiliary Space

**Auxiliary space is the extra memory used by an algorithm, excluding the memory required to store the input.**

For example:

```cpp
int sum = 0;

for (int i = 0; i < n; i++) {
    sum += arr[i];
}
```

Here, `arr` is the input.

The algorithm only uses a few extra variables:

```text
sum
i
```

Their memory does not increase with `n`.

Therefore:

```text
Auxiliary Space = O(1)
```

### Example with Extra Array

```cpp
int temp[n];
```

Here, the algorithm creates an additional array of size `n`.

Therefore:

```text
Auxiliary Space = O(n)
```

### Simple Definition

> **Auxiliary space is the extra memory used by an algorithm apart from the input data.**

---

## Memory Usage Analysis

When analyzing space complexity, we need to look at **how much memory the algorithm uses**.

We can think about:

```text
Total Space
     ↓
┌───────────────┐
│  Input Space  │
│      +        │
│ Auxiliary     │
│    Space      │
└───────────────┘
```

For example:

```cpp
int arr[n];      // Input
int temp[n];     // Extra memory
int sum = 0;     // Extra variable
```

Here:

```text
Input Space      = O(n)
Auxiliary Space  = O(n)
```

The total memory usage grows proportionally with `n`.

### Important Distinction

In DSA, when someone asks:

> **"What is the space complexity of this algorithm?"**

You should check whether they mean **total space** or **auxiliary space**.

In many algorithm problems, **space complexity is discussed mainly in terms of auxiliary space**, especially when the input storage is already given.

---

## Why Does Space Complexity Matter in Coding Even When Using the Best Algorithm?

Even if you choose the best algorithm in terms of time, **space complexity still matters**.

The reason is simple:

> **An algorithm can be very fast but use too much memory.**

### Example

Suppose you have:

```text
n = 1,000,000
```

### Algorithm A

Uses very little extra memory:

```text
Time:  O(n)
Space: O(1)
```

### Algorithm B

Uses an additional array of size `n`:

```text
Time:  O(n)
Space: O(n)
```

Both may take similar time, but **Algorithm B needs much more memory**.

### Why Does That Matter?

#### 1. Memory is Limited

A computer does not have unlimited RAM.

If your algorithm keeps creating large arrays, objects, maps, etc., it can eventually cause:

```text
Memory Limit Exceeded
Out of Memory
```

#### 2. Large Input Makes the Difference Bigger

For example:

```text
n = 10
O(n) → 10 extra units of memory

n = 1,000,000
O(n) → 1,000,000 extra units of memory
```

As the input grows, the memory requirement grows too.

#### 3. Less Memory Can Improve Performance

Using less memory can reduce memory usage and sometimes improve **cache efficiency**, which can make programs faster.

However, using less memory does **not automatically mean** that an algorithm will be faster.

#### 4. Important in Real Applications

Memory matters a lot in things like:

* Mobile applications 📱
* Embedded systems
* Large databases
* Servers
* Operating systems
* Competitive programming

---

## Important Distinction

When choosing an algorithm, we don't look at **only time complexity**.

We usually consider **both time and space complexity**.

```text
              Algorithm
                  ↓
        ┌─────────┴─────────┐
        ↓                   ↓
 Time Complexity      Space Complexity
   "How much work?"    "How much memory?"
```

For example:

| Algorithm | Time | Space |
| --------- | ---- | ----- |
| A         | O(n) | O(1)  |
| B         | O(n) | O(n)  |

If both have the same time complexity, **Algorithm A is generally preferable if its lower memory usage does not introduce another important trade-off.**

### Important Clarification

"Best algorithm" doesn't necessarily mean **the fastest algorithm only**.

A good algorithm should provide a reasonable **time-space trade-off**.

> **Space complexity matters because memory is a limited resource, and an algorithm that uses too much memory may fail even if it is very fast.**

---

# In-Place Algorithms

An **in-place algorithm** is an algorithm that solves a problem using **constant or very small extra memory**, without creating another data structure proportional to the input size.

### Example

Suppose we want to reverse an array.

Instead of creating another array:

```text
Original:
[1, 2, 3, 4, 5]

Extra array:
[5, 4, 3, 2, 1]
```

We can swap elements inside the original array:

```cpp
int left = 0;
int right = n - 1;

while (left < right) {
    swap(arr[left], arr[right]);
    left++;
    right--;
}
```

The array is modified directly.

Only a few variables are used:

```text
left
right
temporary value used by swap
```

Therefore:

```text
Auxiliary Space = O(1)
```

This is an **in-place algorithm**.

### Why Are In-Place Algorithms Useful?

They can:

* Use less extra memory
* Reduce memory usage
* Be useful when memory is limited
* Sometimes improve cache behavior
* Avoid creating additional arrays or data structures

### Important

> **In-place does not mean that the algorithm uses absolutely zero memory.**

It means the algorithm uses **constant or very small extra memory** relative to the input size.

---

# Cache Efficiency

## What is Cache?

The CPU is extremely fast, but **RAM is much slower**.

So the CPU has small, very fast memory called **cache**.

A simplified view:

```text
CPU
 ↓
L1 Cache     ← Very fast, very small
 ↓
L2 Cache     ← Fast, larger
 ↓
L3 Cache     ← Larger
 ↓
RAM          ← Much larger, slower
 ↓
SSD/HDD      ← Much slower
```

When the CPU needs data, it first looks in the cache.

If the required data is already there:

> **Cache Hit** ✅ → Data is obtained quickly.

If it isn't there:

> **Cache Miss** ❌ → CPU has to get it from a slower memory level.

---

## What is Cache Efficiency?

**Cache efficiency means how effectively a program uses the CPU cache so that the CPU can access the data it needs quickly.**

A program has good cache efficiency when it produces many **cache hits** and fewer **cache misses**.

---

## How Can Less Memory Improve Cache Efficiency?

Imagine you have an array:

```cpp
int arr[100];
```

Suppose the CPU needs to process:

```text
arr[0]
arr[1]
arr[2]
arr[3]
...
```

Arrays store elements **next to each other in memory**.

When the CPU loads `arr[0]`, it usually brings a **cache line** containing nearby elements too.

```text
Memory:

arr[0] arr[1] arr[2] arr[3] arr[4] arr[5] ...
  ↑
CPU requests this
```

The cache may load something like:

```text
[ arr[0] arr[1] arr[2] arr[3] ... ]
```

Then when the CPU needs `arr[1]`, it is already in the cache.

That's a **cache hit**.

---

## Smaller Data Can Fit Into Cache

Suppose your program needs to process data.

### Program A

```text
Data size = 10 KB
```

### Program B

```text
Data size = 500 MB
```

The CPU cache is much smaller than 500 MB.

So Program B is more likely to repeatedly move data between cache and RAM.

If you can solve the same problem using significantly less memory, more of the **actively used data** may fit in the cache.

That can reduce cache misses and improve performance.

---

## Important: Less Memory ≠ Automatically Faster

**Space complexity and cache efficiency are related, but they are not the same thing.**

For example:

```text
Algorithm A
Time:  O(n)
Space: O(1)

Algorithm B
Time:  O(n)
Space: O(n)
```

Algorithm A uses less memory, but that **doesn't automatically mean Algorithm A will be faster**.

Cache performance also depends on:

* How data is arranged in memory
* How data is accessed
* Sequential vs. random access
* Size of the working data
* Cache size
* Number of cache misses
* CPU architecture

### Simple Example

Sequential access:

```cpp
for (int i = 0; i < n; i++) {
    sum += arr[i];
}
```

This is usually **cache-friendly** because we access nearby memory locations.

Random access:

```cpp
for (int i = 0; i < n; i++) {
    sum += arr[randomIndex[i]];
}
```

This can be **less cache-friendly** because the CPU may need data from many different memory locations.

---

## The Big Picture

Think of it like a desk:

```text
        CPU
         ↓
   ┌─────────────┐
   │    CACHE    │  ← Small desk, very fast
   └─────────────┘
         ↓
   ┌─────────────┐
   │     RAM     │  ← Huge room, slower to access
   └─────────────┘
```

If you keep the things you're currently working with **on your small desk**, you can grab them quickly.

If your workspace is huge and scattered around the room, you have to keep walking back and forth.

That's roughly the idea behind **cache efficiency**.

### In One Sentence

> **Cache efficiency is how effectively a program uses the CPU cache; using less and more contiguous data can sometimes improve performance because more of the frequently accessed data can stay in the fast cache and reduce cache misses.**

**Important:** Space complexity is primarily about memory usage, while cache efficiency is a lower-level hardware performance consideration. You should not assume that an `O(1)`-space algorithm is always faster than an `O(n)`-space algorithm.

---

# Asymptotic Notations for Time and Space Complexity

1. **Big O** — `O(f(n))`
2. **Big Omega** — `Ω(f(n))`
3. **Big Theta** — `Θ(f(n))`
4. **Small o** — `o(f(n))`
5. **Small Omega** — `ω(f(n))`

> **Note:** These notations are used to represent the time and space complexity of an algorithm. Among them, **Big O notation is the most widely used in practical DSA.**

Here, **`f(n)` represents a function that describes how the algorithm's time or space requirement grows with the input size `n`.**

**Note:** `θ(f(n))` (small theta) is not a standard asymptotic notation. The standard asymptotic notations are **O, Ω, Θ, o, and ω**.
