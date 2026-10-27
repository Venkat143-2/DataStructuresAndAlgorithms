# Recursion Fundamentals — 7 Topics

A beginner-friendly guide to the seven foundations of recursion, with explanations, diagrams, Python examples, and practice questions.

## Table of Contents

1. [What Is Recursion?](#1-what-is-recursion)
2. [Base Condition](#2-base-condition)
3. [Recursive Call](#3-recursive-call)
4. [Call Stack](#4-call-stack)
5. [Stack Memory](#5-stack-memory)
6. [Recursion Tree](#6-recursion-tree)
7. [Recursion Tracing](#7-recursion-tracing)
8. [Quick Revision](#8-quick-revision)

---

## 1. What Is Recursion?

### Description

**Recursion** is a programming technique in which a function calls itself to solve a smaller version of the same problem.

A recursive function usually needs two things:

- **Base condition:** tells the function when to stop.
- **Recursive call:** calls the function again, usually with a smaller or simpler input.

### Example

```python
def count(n):
    if n == 0:
        print(0)
        return

    print(n)
    count(n - 1)

count(3)
```

Output:

```text
3
2
1
0
```

### Flowchart

```text
       Start: count(3)
              |
           Print n
              |
          Is n == 0?
           /      \
         Yes       No
          |         |
        Return   count(n - 1)
                    |
                 Repeat
```

### Key idea

Each call works with its own input value. Here, the values go from `3` to `2`, `1`, and finally `0`.

---

## 2. Base Condition

### Description

A **base condition** (or base case) is the condition that stops recursion. When it is reached, the function stops making further recursive calls.

### Example

```python
def fun(n):
    if n == 0:       # Base condition
        return

    print(n)
    fun(n - 1)

fun(3)
```

Output:

```text
3
2
1
```

When `n == 0`, `return` ends that function call. No further call to `fun(-1)` is made.

### Why is it important?

Without a reachable base condition, recursion may continue until Python raises a `RecursionError`.

```python
def never_stops(n):
    print(n)
    never_stops(n - 1)

# Calling never_stops(3) eventually raises RecursionError.
```

### Checklist

- Is there a base condition?
- Can the function eventually reach it?
- Does the base case stop making recursive calls?

---

## 3. Recursive Call

### Description

A **recursive call** happens when a function calls itself.

### Direct recursion

A function calls itself directly:

```python
def A(n):
    if n == 0:
        return
    A(n - 1)
```

Call pattern:

```text
A(3) -> A(2) -> A(1) -> A(0)
```

### Indirect (mutual) recursion

A function calls another function, which eventually calls the first function again:

```python
def A(n):
    if n <= 0:
        return
    B(n - 1)

def B(n):
    if n <= 0:
        return
    A(n - 1)

A(3)
```

Call pattern:

```text
A(3) -> B(2) -> A(1) -> B(0)
```

### Statements before and after a recursive call

```python
def fun(n):
    if n == 0:
        return

    print("Start", n)
    fun(n - 1)
    print("End", n)

fun(3)
```

Output:

```text
Start 3
Start 2
Start 1
End 1
End 2
End 3
```

The statements before the call run while the calls descend. Statements after the call wait until the deeper call returns.

---

## 4. Call Stack

### Description

The **call stack** is the stack-like structure that tracks function calls that have started but have not yet finished.

Each active function call has its own **stack frame**. A frame generally stores information such as the call's parameters, local-variable information, and where execution should resume. Exact implementation details depend on the language and runtime.

### Example

```python
def fun(n):
    if n == 0:
        return

    print("Start", n)
    fun(n - 1)
    print("End", n)

fun(3)
```

At the deepest point, the active calls are:

```text
TOP
+---------+
| fun(0)  |  <- newest call
+---------+
| fun(1)  |
+---------+
| fun(2)  |
+---------+
| fun(3)  |  <- original call
+---------+
BOTTOM
```

### Push and pop

- **Push:** a new function call is added to the stack.
- **Pop:** a completed call's frame is removed.
- **LIFO:** Last In, First Out. The last call added is the first one to return.

### Call sequence

```text
Calls going down:
fun(3) -> fun(2) -> fun(1) -> fun(0)

Returns coming back:
fun(0) -> fun(1) -> fun(2) -> fun(3)
```

For `fun(5)` calling down through `fun(0)`, there are **6 active calls** at the deepest point: `fun(5)`, `fun(4)`, `fun(3)`, `fun(2)`, `fun(1)`, and `fun(0)`.

---

## 5. Stack Memory

### Description

**Stack memory** is memory used by the runtime to manage active function calls. Each active call generally has a stack frame. The call stack is the structure that organizes these frames.

> Simple distinction: the **call stack** is the structure; **stack memory** is the memory used to hold call-related information.

### Example

```python
def fun(n):
    if n == 0:
        return
    print(n)
    fun(n - 1)

fun(3)
```

When `fun(0)` has just started, before it returns, the calls look like this:

```text
TOP
+---------+
| fun(0)  |  n = 0
+---------+
| fun(1)  |  n = 1
+---------+
| fun(2)  |  n = 2
+---------+
| fun(3)  |  n = 3
+---------+
BOTTOM
```

Each active call has its own parameter value. Returning calls are removed in reverse order:

1. `fun(0)` returns.
2. `fun(1)` resumes and returns.
3. `fun(2)` resumes and returns.
4. `fun(3)` resumes and returns.

### Why it matters

- Every active recursive call requires call-related memory.
- Deeper recursion generally means more active calls and more memory use.
- Very deep recursion can exceed Python's recursion limit and raise `RecursionError`.

---

## 6. Recursion Tree

### Description

A **recursion tree** is a diagram in which each node represents a function call and each branch represents a recursive call made by that function.

### Example A: One recursive call each time

```python
def fun(n):
    if n == 0:
        return
    fun(n - 1)

fun(3)
```

Tree:

```text
fun(3)
  |
fun(2)
  |
fun(1)
  |
fun(0)  <- base case
```

This tree is a straight line because each call makes only one recursive call.

Total calls: **4** (`fun(3)`, `fun(2)`, `fun(1)`, `fun(0)`).

### Example B: Two recursive calls each time

```python
def fun(n):
    if n == 0:
        return

    fun(n - 1)
    fun(n - 1)

fun(2)
```

Tree:

```text
              fun(2)
             /      \
         fun(1)    fun(1)
         /   \      /   \
     fun(0) fun(0) fun(0) fun(0)
```

Each `fun(1)` call is a separate call, even though both have the same argument.

Calls at each level:

```text
Level 0: 1 call
Level 1: 2 calls
Level 2: 4 calls
```

Total calls: `1 + 2 + 4 = 7`.

For this same two-call pattern with `fun(3)`, the levels contain `1, 2, 4, 8` calls, for a total of `15`.

### Important terms

- **Node:** one function call.
- **Edge/branch:** connection showing a call to another function.
- **Root:** the first call.
- **Leaf node:** a node that makes no further recursive calls.
- **Level:** a node's depth in the tree.

---

## 7. Recursion Tracing

### Description

**Recursion tracing** means following a recursive function step by step to determine the order of calls, when the base case is reached, how calls return, and what output is produced.

### Example

```python
def fun(n):
    if n == 0:
        return

    print(n)
    fun(n - 1)
    print(n)

fun(3)
```

### Step 1: Calls descend

The first `print(n)` happens before the recursive call.

```text
fun(3): prints 3
  fun(2): prints 2
    fun(1): prints 1
      fun(0): returns immediately
```

So far, the output is:

```text
3
2
1
```

### Step 2: Calls return

After `fun(0)` returns, the waiting calls continue after their recursive calls:

```text
fun(1): prints 1
fun(2): prints 2
fun(3): prints 3
```

### Final output

```text
3
2
1
1
2
3
```

### A reliable tracing checklist

1. Find the base condition.
2. Follow each recursive call and record its argument.
3. Record statements that run before the recursive call.
4. When the base case returns, continue each paused call.
5. Record statements that run after the recursive call.

### Practice example

Predict the output:

```python
def fun(n):
    if n == 0:
        return

    print(n)
    fun(n - 1)

    if n == 2:
        print("Hello")

fun(3)
```

Answer:

```text
3
2
1
Hello
```

`Hello` prints only when `fun(2)` resumes, after its call to `fun(1)` has completed.

---

## 8. Quick Revision

| Topic | Remember |
|---|---|
| Recursion | A function calls itself to solve a smaller version of a problem. |
| Base condition | Stops further recursive calls. |
| Recursive call | A call made by a function to itself, directly or indirectly. |
| Call stack | Tracks active function calls. |
| Stack memory | Holds call-related information for active calls. |
| Recursion tree | Visualizes how calls branch into other calls. |
| Recursion tracing | Follows calls and returns to determine execution and output. |

### The two journeys of recursion

```text
DESCENDING: calls are made
fun(3) -> fun(2) -> fun(1) -> fun(0)

ASCENDING: calls return
fun(0) -> fun(1) -> fun(2) -> fun(3)
```

**Study tip:** Practise tracing small examples on paper. Write down each call, mark the base case, then trace the returns. Once these fundamentals are clear, move on to learning how to approach recursion problems and recognize patterns.
