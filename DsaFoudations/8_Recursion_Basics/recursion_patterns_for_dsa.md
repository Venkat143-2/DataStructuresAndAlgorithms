# Recursion Patterns for DSA

A practical guide to the main recursion patterns, with simple explanations, examples, and a recommended learning order.

## 1. Pick / Non-pick (Take / Not Take)

**Idea:** For each element, make two choices:
- **Pick:** include the current element.
- **Non-pick:** skip the current element.

Example: Generate all subsequences of `[1, 2, 3]`.

```text
                    index = 0
                  /         \
              Pick 1       Skip 1
              /    \        /    \
           Pick 2 Skip 2 Pick 2 Skip 2
```

Common problems:
- Generate subsequences
- Generate subsets
- Subset Sum
- 0/1 Knapsack

**Key question:** Should I include this element, or leave it out?

## 2. Choose → Explore → Unchoose (Backtracking)

**Idea:** Make a choice, explore the result recursively, then undo the choice before trying another option.

```text
Choose an option
      ↓
Explore recursively
      ↓
Undo the choice
      ↓
Try another option
```

Common problems:
- Permutations
- Combinations
- N-Queens
- Sudoku
- Maze/path problems

**Key question:** After exploring this choice, how do I restore the previous state?

## 3. Index / Parameter Recursion

**Idea:** Process one element at a time by changing an index or parameter until reaching the base case.

```text
f(0) → f(1) → f(2) → f(3) → stop
```

Common problems:
- Array traversal
- String traversal
- Sum of array elements
- Checking whether an array is sorted
- Reversing a string or array

**Key question:** What smaller part of the input should the next call process?

## 4. Multiple Recursive Calls

**Idea:** A function makes two or more recursive calls to solve smaller parts of a problem.

```text
        f(n)
       /    \
   f(n-1)  f(n-2)
```

Common problems:
- Fibonacci (basic recursive version)
- Tree recursion
- Problems where several recursive outcomes must be considered

**Key question:** What different smaller problems must be solved?

## 5. Target / Constraint-Based Recursion

**Idea:** Make choices while tracking a target or constraint, such as a remaining sum, remaining capacity, or number of items.

Example: Can elements of `[2, 3, 5]` produce a sum of `8`?

Common problems:
- Subset Sum
- Combination Sum
- Finding paths with a target sum
- 0/1 Knapsack

**Key question:** What is the remaining target after making this choice?

## 6. Partition Recursion

**Idea:** Try different ways to split a string or array into smaller parts, then recursively solve each part.

Common problems:
- Palindrome partitioning
- Word segmentation / word break
- Some dynamic programming problems

**Key question:** Where can I place the next split?

## 7. Divide and Conquer

**Idea:** Divide a problem into smaller subproblems, solve them recursively, and combine their results.

```text
          Problem
          /     \
      Smaller  Smaller
          \     /
           Combine
```

Common problems:
- Merge Sort
- Quick Sort
- Binary search

**Key question:** How can I divide the problem, and how do I combine the results?

## 8. Tree Recursion / DFS

**Idea:** Recursively visit child nodes in a tree or explore neighbors in a graph.

Common problems:
- Preorder, inorder, and postorder traversal
- Finding tree height
- Tree path problems
- Graph Depth-First Search (DFS)

**Key question:** What should I do at the current node before or after visiting its children?

---

## Recommended Learning Order

1. **Basic recursion and base cases**
   - Print numbers
   - Factorial
   - Sum of the first `n` numbers
2. **Index / parameter recursion**
   - Arrays and strings
   - Reverse an array/string
   - Check whether an array is sorted
3. **Pick / non-pick**
   - Subsequences
   - Subsets
4. **Target-based recursion**
   - Subset Sum
   - Combination Sum
5. **Backtracking**
   - Permutations
   - Combinations
   - Maze problems
6. **Multiple calls and tree recursion**
   - Fibonacci
   - Binary tree traversals
   - DFS
7. **Partition recursion**
   - Palindrome partitioning
8. **Divide and conquer**
   - Binary search
   - Merge Sort
   - Quick Sort

## Important Differences

| Pattern | Main idea |
|---|---|
| Pick / non-pick | Make two choices for each element: include or skip |
| Backtracking | Choose, explore, and undo |
| Divide and conquer | Split into smaller problems and combine |
| Target-based recursion | Track a target or remaining constraint |
| Tree recursion / DFS | Explore child nodes or graph neighbors |

## A General Way to Think About Recursion

For every recursive problem, ask:

1. **What is the state?** What information does the function need (for example, an index or remaining target)?
2. **What is the base case?** When should the recursion stop?
3. **What are the choices?** Is there one next step, or several choices?
4. **What changes in the next call?** Make sure the problem gets smaller or moves toward stopping.
5. **Do I need to undo a choice?** This is often necessary in backtracking.
6. **How do I combine or return the results?** Does the function return a value, update a shared result, or record a solution?

## Final Advice

Start with basic recursion and learn to trace calls by hand. Then practise **pick/non-pick** until you can draw its recursion tree and explain each branch. Next, move to target-based recursion and backtracking.

You do not need to memorize every problem. Learn to recognize the pattern, define the state, identify the base case, and make the recursive transition.
