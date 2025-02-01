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



## NP and Decision Problems

### Definition of NP
**NP** stands for *"Nondeterministic Polynomial Time."* This class includes **decision problems** for which a solution can be **verified** (or "guessed" correctly) in polynomial time by a **nondeterministic** computer.

### Decision Problems
A **decision problem** is one where the answer is simply **"yes" or "no."**  
For example:
- Instead of asking *"What is the shortest route that visits all cities?"* (an **optimization problem**),
- You could ask, *"Is there a route that visits all cities and has a total length ≤ L?"* (a **decision problem**).  

This **yes/no formulation** is key to fitting problems into the **NP framework**.

---

## The Satisfiability (SAT) Problem in NP

The **Satisfiability (SAT) problem** is one of the fundamental problems in NP.  
A problem is in NP if, given a **"yes" instance** (i.e., a certificate or solution), we can **verify its correctness quickly** (in polynomial time).

### Polynomial-Time Reductions
- The key idea is that **every other problem in NP** can be **transformed** (or *"reduced"*) into an instance of the **SAT problem** in polynomial time.
- This means there is an **efficient way** to convert any **NP problem** into a **SAT problem** such that solving the SAT problem would give the answer to the original problem.

---

## Implications for Solving NP Problems

### If SAT Can Be Solved Quickly
- Suppose someone finds a **polynomial-time algorithm** for solving SAT.
- Since **every NP problem reduces to SAT**, you could then **solve any NP problem efficiently** by:
  1. **Converting it to SAT**, and
  2. **Applying the efficient SAT algorithm**.

### If Any NP Problem is Intractable
- Conversely, if even **one** problem in NP is truly **intractable** (meaning it **cannot** be solved in polynomial time),
- Then, because **every NP problem reduces to SAT**, the **SAT problem must also be intractable**.
- In other words, **SAT is at least as hard** as the hardest NP problems.

### SAT as the "Hardest" Problem in NP
- Since **every NP problem can be reduced to SAT**, SAT *captures the full difficulty* of NP.
- If SAT can be solved quickly → **all NP problems can be solved quickly**.
- If SAT **cannot** be solved quickly → there exist **NP problems that are inherently hard**.
- This is why **SAT is often called the "hardest" problem in NP** and is central to **NP-completeness**.

---

## 1. Reductions and Their Implications

### Polynomial-Time Reduction
For any problem **P** in NP:
- There exists a **polynomial-time reduction** that transforms any instance of **P** into an instance of **SAT**.
- This means that if we had an **efficient (polynomial-time) algorithm** to solve SAT, we could:

  1. **Transform**: Convert any instance of **P** into an equivalent SAT instance.
  2. **Solve**: Use the efficient SAT algorithm to solve this SAT instance.
  3. **Conclude**: Interpret the result to solve the original problem **P**.

---

## 2. The Consequence of a Fast SAT Algorithm

### Suppose SAT is Tractable
- Imagine that there is a **polynomial-time algorithm for SAT**.
- Because **every NP problem reduces to SAT** in polynomial time, this would mean that **every problem in NP could also be solved in polynomial time**.
- In other words, if SAT were tractable, then **P = NP**.

---

## 3. Assuming Some NP Problem is Intractable

### Intractability of an NP Problem
- Suppose there exists at least **one** NP problem **Q** that is **truly intractable**—meaning that **no polynomial-time algorithm exists** for **Q**.

---

## 4. Arriving at a Contradiction

### Using the Reduction
- Since **every NP problem reduces to SAT**, there exists a **polynomial-time reduction** from **Q** to **SAT**.
- This means that if we could **solve SAT in polynomial time**, then:
  1. **Convert Q to SAT** (using the reduction).
  2. **Solve SAT** in polynomial time.
  3. **Get a polynomial-time solution for Q**.

### Contradiction
- But this **contradicts our assumption** that **Q is intractable** (i.e., **Q cannot be solved in polynomial time**).
- Therefore, our **initial assumption that SAT can be solved in polynomial time must be false**.

---

## 5. Conclusion

### SAT is at Least as Hard as the Hardest NP Problems
- Since **any NP problem** can be **efficiently transformed** into an instance of **SAT**,
- **SAT inherits the "difficulty" of the hardest NP problems**.
- If even **one** NP problem is intractable, then **SAT must also be intractable**.

### Final Thought:
- The **reduction** shows that **SAT is "at least as hard" as any NP problem**.
- If solving SAT **quickly** were possible, it would mean **all NP problems are quickly solvable**.
- Since this contradicts the assumption that **at least one NP problem is intractable**, SAT itself **must be intractable**.


## NP-Complete Problems: "Just as Hard" as SAT

### Definition of NP-Completeness
The class of **NP-complete problems** consists of decision problems that are **"just as hard"** as the **Satisfiability (SAT) problem**. These problems were first identified through a series of polynomial-time reductions by **Richard Karp**, showing that several combinatorial decision problems are equally difficult as SAT.

### Practical Implications

1. **Equivalence in Difficulty**  
   - No matter which **NP-complete problem** you tackle—whether it's **SAT, Traveling Salesman Problem (TSP), or another combinatorial problem**—
   - Solving **one** NP-complete problem **efficiently (in polynomial time)** would allow you to **solve all NP problems efficiently**.

2. **Implications for Intractability**  
   - Most researchers believe that **no polynomial-time algorithm exists for at least one NP problem** (i.e., **NP problems are intractable**).
   - If this assumption is true, then **none** of these NP-complete problems can have a polynomial-time algorithm.
   - In other words, **all NP-complete problems share a common level of computational difficulty**.

---

### Summary
- **NP-complete problems** are the hardest problems in **NP**.
- If **one** NP-complete problem can be solved in **polynomial time**, then **all** NP problems can be solved efficiently.
- However, if **even one** NP problem is intractable, then **all** NP-complete problems are intractable.
