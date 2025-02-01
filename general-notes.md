# Theory of Computation Notes

## Problem Reduction

When we say that problem **A** is *"at least as hard as"* problem **B**, we mean that **B** can be reduced to **A** in polynomial time.

## Complexity Classes

### NP (Nondeterministic Polynomial Time)

A problem being in **NP** means that if someone hands you a candidate solution, you can verify its correctness in polynomial time. However, this class includes both:

- Problems that can be solved efficiently (i.e., problems in **P**).
- Problems that might be very hard and not efficiently solvable.

### NP-Complete

Proving a problem is **NP-complete** shows that it is as difficult as the hardest problems in **NP**. More formally:

- Every problem in **NP** can be reduced to an **NP-complete** problem in polynomial time.
- This implies that if you could solve an **NP-complete** problem quickly (in polynomial time), then every **NP** problem could also be solved quickly.
- However, it is widely believed that **P ≠ NP**, meaning that no polynomial-time solution exists for NP-complete problems.


## Time Complexity

The **time complexity function** for an algorithm expresses its time requirements by giving, for each possible input length, the largest amount of time needed by the algorithm to solve a problem instance of that size.

### Big-O Notation

Let us say that a function **f(n)** is **O(g(n))** whenever there exists a constant **c** such that:

\[
| f(n) | < c \cdot | g(n) | \quad \text{for all } n > 0
\]

### Polynomial Time Algorithms

A **polynomial-time algorithm** is defined as one whose time complexity function is **O(p(n))** for some polynomial function **p(n)**, where **n** denotes the input length.

### Exponential Time Algorithms

Any algorithm whose time complexity function cannot be bounded by a polynomial function is called an **exponential-time algorithm**. However, this definition may also include certain non-polynomial time complexity functions (such as \( n^{\log n} \)), which are not typically regarded as exponential functions.

### Intractability

This reflects the viewpoint that **exponential-time algorithms** should not be considered "good" algorithms, which is usually the case. There is broad agreement that a problem has not been *well-solved* until a **polynomial-time algorithm** is known for it. 

Thus, we refer to a problem as **intractable** if it is so hard that no polynomial-time algorithm can possibly solve it.



## Understanding Intractability

Of course, this formal use of *"intractable"* should be viewed only as a rough approximation of its dictionary meaning. The distinction between **efficient** polynomial-time algorithms and **inefficient** exponential-time algorithms has many exceptions, especially when the problem instances of interest have limited size.

For example, even in **Figure 1.2**, the \( 2^n \) algorithm is faster than the \( n^3 \) algorithm for \( n \leq 20 \). More extreme examples can be constructed easily.

### Theoretical Framework of Intractability

Our definition of **intractability** provides a theoretical framework of considerable generality and power. The intractability of a problem is **essentially independent** of the particular encoding scheme and computer model used for determining time complexity.

### Encoding Schemes and Input Length

Let us first consider **encoding schemes**. Suppose we are dealing with a problem in which each instance is a **graph** \( G = (V, E) \), where:

- \( V \) is the set of **vertices**.
- \( E \) is the set of **edges**, each being an unordered pair of vertices.

An instance of this problem could be described using different representations:

1. **Listing all the vertices and edges**.
2. **Listing the rows of the adjacency matrix** for the graph.
3. **Using a neighbor list**, where each vertex lists the other vertices it shares an edge with.

Each of these encodings can yield a different input length for the same graph. However, it is easy to verify (see **Figure 1.5**) that the input lengths differ **at most polynomially** from one another. This means that:

- If an algorithm has **polynomial time complexity** under one encoding scheme, it will have **polynomial time complexity** under all the others.
- In practice, the standard encoding schemes for a given problem always seem to differ **at most polynomially** from one another.

