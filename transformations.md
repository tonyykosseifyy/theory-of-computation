![image](https://github.com/user-attachments/assets/13b9ded0-2712-463f-ac2a-ab350eea202d)# Discrete 2

## NP-Completeness and Reductions

If \( A \) reduces to \( B \) and \( A \) is **NP-complete** and \( B \) can be verified in polynomial time, then **\( B \) is NP-complete**.

\( B \) is at least as hard as \( A \), because if you were to find a solution to \( B \), you could transform \( A \) into it and would solve the transformed problem, thus solving \( A \). **We cannot say the inverse**.

If \( A \) reduces to \( B \) and \( B \) reduces to \( A \), then they are **both equally hard**.

---

## Intractability

An **intractable problem** is one for which an efficient polynomial-time algorithm does **not exist yet**.

It is useful to begin by distinguishing between **two different causes** of intractability allowed by our definition:

1. **The first cause**, which is the one we usually have in mind, is that the problem is so difficult that an **exponential amount of time** is needed to discover a solution.
2. **The second cause** is that the solution itself is required to be so **extensive** that it **cannot be described** with an expression having length bounded by a **polynomial function** of the input length.

---

## The Halting Problem

The **halting problem** is **NP-hard**.

### **Problem Statement:**
Given a program and an input to this program, will the program run forever?

---

## NP Definition

**NP** is the class of **decision problems** that can be solved in **polynomial time** by a **non-deterministic machine**, which is equivalent to saying:

- A **class of problems** whose **"yes" instance** can be **verified** in polynomial time.

A **decision problem** is one whose answer is either **"yes" or "no."**

---

## NP-Hard and NP-Complete

- **NP-hard problems** are **at least as hard as the hardest NP problems** because **every problem in NP reduces to it**. Meaning that **if we were to find a polynomial-time solution to the NP-hard problem, we would be able to solve any NP problem** by converting it to this NP-hard problem and solving it.

- **NP-complete problems** are the **hardest problems in NP** because **if you can theoretically find a solution to that problem, you would be able to solve any NP problem**. So, **if you can solve this problem quickly, any other problem can be solved quickly**.

---

## Comparing Problems via Reductions

When reducing **problem \( P \)** to **problem \( Q \)**, we can say that **\( Q \) is at least as hard as \( P \)**.

- **If you were to find a solution for \( Q \)**, you can then **find a solution to \( P \)** by **transforming \( P \) into \( Q \)**.
- **This does not guarantee that \( P \) is as hard as \( Q \)**, but **\( Q \) is at least as hard as \( P \)** because **you are able to convert \( P \) into \( Q \) and solve it**.

---

## Relationship Between P, NP, NP-Hard, and NP-Complete

- Problems belonging to the class **P** are **NP** as well because **you can verify them using a non-deterministic algorithm** that consists of two steps:
  1. **Guessing a "yes" instance** of the problem.
  2. **Verifying the "yes" instance’s certificate in polynomial time**.

  Since **problems in P can skip the guessing phase** and directly proceed to the checking stage, **they are in NP**.

- **P and NP-complete problems are part of NP**.
  - **NP** is the **general set**.
  - **NP-hard and NP** have an **intersection**, which consists of **NP-complete problems**.

- **NP-hard problems are at least as hard as NP-complete problems**; **they could be harder**.

- In the set **NP**, **NP-complete problems are the hardest** because **if you were to find a solution to them, you would find a solution to all other NP problems**.

# From SAT to 3SAT: Proving that 3SAT is NP-Complete

**SAT and 3SAT** are both **exponential in runtime** because we would need to verify every possible combination of truth assignments for the variables. 

- If you had **n variables**, you would have **\( 2^n \)** ways to assign them, hence the **exponential runtime**.

---

## **1) Prove that 3SAT is in NP**
Given a **"yes" instance of 3SAT**, we need to verify if the given **certificate** is a valid one, and this verification must be done in **polynomial time**.

### **Certificate Validation Process**
- Go through **each clause** and **assign** to the literals a truth value depending on the **certificate** that was passed.
- Keep track to see **if each clause has at least one true literal**, so that it evaluates to **true**.
- If **all** clauses have **at least one true literal**, then the certificate is **valid**; otherwise, it is **not valid**.

### **Runtime Complexity Analysis**
This can be done in **\( O(m) \)** where \( m \) is the **number of clauses**.

- **Why \( O(m) \) and not \( O(m \times n) \) like in SAT?**
  - In SAT, we could have up to **\( n \) literals in each clause**.
  - In **3SAT**, it is **restricted**—**each clause has exactly 3 literals (constant size)**.
  - Therefore, the runtime **\( O(3m) \) can be rewritten as \( O(m) \)**.

---

## **2) Transformation from SAT to 3SAT**
To convert **SAT** to **3SAT**, we adjust each clause based on the number of literals it contains.

### **Case 1: Clause with Less than 3 Literals**
- **If a clause has only 1 literal**, duplicate it **twice**.
- **If a clause has 2 literals**, duplicate **one of the already present literals**.
- **Effect**: This does not **alter** the result of the expression. 
  - **If the original clause was true, it remains true.**
  - **If the original clause was false, it remains false.**

### **Case 2: Clause with Exactly 3 Literals**
- **Keep them as they are**.

### **Case 3: Clause with More than 3 Literals**
- Break down the **clause into multiple 3-literal clauses**.
- **Procedure:**
  1. Take the **first two literals** and **add them** to the first clause of **3SAT**.
  2. Add a **free variable** at the end.
  3. For the **second clause**, add the **negation** of the **free variable** used in the previous clause.
  4. If **more than one variable remains**, add **another literal** from the original clause and introduce **a new free variable**.
  5. Continue this **until you reach the last two literals** in the clause.
  6. These will be **included together with a free variable at the start**.

---

## **Transformation Validity**
- The **clauses that had in SAT less than 3 literals** will **remain valid** as discussed.
- For the **case where we are splitting the clauses**, the truth **value** of the original SAT clause will be **correctly carried through all the created clauses in 3SAT** due to the way we added **free variables**.

### **Why Does This Work?**
1. **A "yes" instance of SAT will give a "yes" instance of 3SAT**:
   - Since we maintain **logical equivalence**, if SAT has a **satisfying assignment**, the corresponding **3SAT instance** will also be **satisfiable**.
   
2. **A "yes" instance of 3SAT will give a "yes" instance of SAT**:
   - **Clauses with fewer than 3 literals** remain **true** because we are **adding duplicates**.
   - **For cases where the clause has more than 3 literals**, the newly created clauses come from the **original clause** in SAT.
   - If **all the 3SAT clauses are true**, then at least **one literal** from the original SAT clause must have been **set to true**.
   - The **free variables** will **carry the truth assignment through the created clauses**.
   - If **no true literal was set**, the **last clause added** would evaluate to **false**, leading to a **"no" instance of 3SAT**.

---

## **Complexity of the Transformation**
This transformation can be done in **\( O(n \times m) \)**, which is **polynomial**.

# HC to TSP (Hamiltonian Cycle to Traveling Salesman Problem)

## **Transformation:**
- **Existing edges** in the Hamiltonian Cycle (HC) are **added with a weight of 1**.
- **New edges** (edges not present in the original HC instance) are **added with a weight of 2**.

---

## **Complexity Analysis**
- **Verification of TSP**: \( O(V) \)
- **Transformation of HC into TSP**: \( O(V^2) \)

# **Equivalence of Vertex Cover, Independent Set, and Clique in a Graph**

For any graph **\( G = (V, E) \)** and subset **\( V_C \subseteq V \)**, the following statements are **equivalent**:

1. **\( V_C \) is a vertex cover for \( G \)**.
2. **\( V - V_C \) is an independent set for \( G \)**.
3. **\( V - V_C \) is a clique in the complement \( G^C \) of \( G \)**, where:
   - \( G^C = (V, E^C) \) is the **complement graph** of \( G \).
   - \( E^C = \{(w, v) \mid w, v \in V \text{ and } (w, v) \notin E\} \).

### **Explanation of the Equivalence:**
- A **vertex cover** is a subset of **vertices** such that **every edge in \( G \) has at least one endpoint in \( V_C \)**.
- An **independent set** is a subset of vertices **where no two vertices are adjacent** (i.e., **no edge** exists between them in \( G \)).
- A **clique** in the **complement graph** \( G^C \) means that the corresponding subset of vertices forms an **independent set** in \( G \) because every pair of vertices in the clique are adjacent in \( G^C \), meaning they are **not adjacent** in \( G \).

Thus, **if you have a vertex cover in \( G \), the remaining vertices form an independent set in \( G \), which in turn forms a clique in the complement graph \( G^C \).**

# **Proof by Restriction**

## **Concept**
The idea behind **proof by restriction** is as follows:

- Assume you have a problem **\( A \)** that is **known to be NP-complete**.
- You have another problem **\( B \)** that you need to prove is **NP-complete**.
- To do this **by restriction**, you try to find **similarities** between:
  - **The starting problem \( A \) (which is NP-complete)**.
  - **The problem \( B \) you are trying to prove as NP-complete**.
- The goal is to determine if **problem \( A \) can be seen as a special case of problem \( B \)**.

## **Why Does This Work?**
- If **problem \( A \) (NP-complete) is a special case of problem \( B \)**, and **problem \( B \) is the more general case**, then:
  - **The general case (\( B \)) must also be NP-complete**.
- A **valid transformation** from **problem \( A \) to problem \( B \)** **proves that \( B \) is NP-complete**.

Thus, **this method helps in proving the NP-completeness of problem \( B \) by showing that it encompasses an already known NP-complete problem \( A \)**.

---

### **Key Insight:**
- **Proof by restriction is a way to view transformations**: Instead of constructing a direct reduction, you try to **find structural similarities** between the problems.
- If an NP-complete problem **naturally fits into another problem’s framework**, then the **generalized problem must also be NP-complete**.

X3C (Exact cover by 3 sets) to Minimum Cover (Proof by restriction):

Problem Statement:
•	Input:
o	A finite set S with ∣S∣=3q (i.e., the size of S is a multiple of 3).
o	A collection C of 3-element subsets of S, meaning each subset c∈C satisfies ∣c∣=3|c|.
•	Question:
o	Does there exist a subcollection C′⊆C such that:
	C′ exactly covers S (i.e., the union of the sets in C′ equals S, meaning every element of S appears in exactly one subset in C′).
	∣C′∣=q, meaning the exact number of sets needed to cover S is q=∣S∣/3. 
Input:
S={1,2,3,4,5,6,7,8,9}
 C={{1,2,3},{4,5,6},{7,8,9},{1,4,7},{2,5,8},{3,6,9}}
Solution:
A valid exact cover is:
C′={{1,2,3},{4,5,6},{7,8,9}}
✅ Each element appears exactly once, so the answer is YES.

Minimum cover problem instance: 
Given a set S, and a subset C which contains sets such as in X3C, can you find a minimum cover of size <= k, the minimum cover is the size of C’ which is a subset of C, all these subsets should cover S, so their union = S. 

Here we can see that X3C is a special case of Minimum Cover where we have exactly 3 elements per subset in C, and where the size of S is a multiple of 3 so |S| = 3q, so since we’re saying that it’s a special case of it, we need to transform into Minimum Cover, have a valid transformation for it, proving that Minimum Cover is then NP complete as well. 

So to start things off we need to find what the equivalent K would be, K would be equal to |S|/3, making it equal to q, since S is divisible by 3, so the number of sets needed to cover S would be the size of S divided by 3. 
We then copy the same S and the same C. 

# **Hitting Set**

## **Definition**
A **hitting set** is a **subset** of **\( S \)**, which represents the **universe** containing all elements.

### **Condition for a Hitting Set**
- A subset **\( H \subseteq S \)** is a **hitting set** if, for **every element in \( C \)**, there exists at least **one element from \( H \)** that belongs to it.
- In other words, **at least one element from the hitting set must be present in each subset of \( C \)**.

---

## **Vertex Cover as a Special Case of Hitting Set**
- The idea here is that **Vertex Cover** can be seen as a **special case of the Hitting Set** problem.
- **Mapping between the two problems:**
  - The **vertices** in the **Vertex Cover** problem form the **set \( S \)**.
  - The **edges** in the **Vertex Cover** problem form the **collection of subsets \( C \)**.
  - The value of **\( k \)** remains the **same**.

### **Key Restriction**
- The **restriction in Hitting Set** is on the **size of the elements in \( C \)**.
- In the **Vertex Cover** case, the elements in \( C \) (subsets) are **edges**, which contain exactly **2** elements (the two endpoints of an edge).
- Thus, **Hitting Set with subsets of size exactly 2 corresponds directly to the Vertex Cover problem**.

---

## **Summary**
- A **hitting set** ensures that **every subset in \( C \)** has at least **one selected element**.
- **Vertex Cover** is a **special case** of **Hitting Set**, where:
  - The **vertices** serve as elements of \( S \).
  - The **edges** serve as subsets in \( C \).
  - The restriction on subset size (\( |c| = 2 \)) makes the **Hitting Set equivalent to Vertex Cover**.
 

# **Subgraph Isomorphism**

## **Problem Definition**
### **Instance:**
- Given **two graphs**:
  - \( G = (V_1, E_1) \)  
  - \( H = (V_2, E_2) \)

### **Question:**
- Does **\( G \)** contain a **subgraph** that is **isomorphic** to **\( H \)**?
- Formally, does there exist a **subset** \( V' \subseteq V_1 \) and a **subset** \( E' \subseteq E_1 \) such that:
  - \( |V'| = |V_2| \)
  - \( |E'| = |E_2| \)
  - There exists a **one-to-one function** \( f: V_2 \to V' \) satisfying:  
    \[
    \{u, v\} \in E_2 \iff \{f(u), f(v)\} \in E'
    \]
  
In other words, we are looking for a subgraph in \( G \) that is **identical in structure** to \( H \).

---

## **Proving that Subgraph Isomorphism is NP-Complete**
To prove that **Subgraph Isomorphism** is **NP-complete**, we use **Clique** and apply the **restriction method**.

### **Why is Clique a Special Case of Subgraph Isomorphism?**
- In **Subgraph Isomorphism**, we are checking whether we can **embed \( H \) into \( G \)**, meaning that a subgraph of \( G \) exists that is structurally **identical** to \( H \).
- **Clique** is a special case of **Subgraph Isomorphism**, where:
  - We are looking for a **complete subgraph** (a set of fully connected vertices).
  - The problem **"find a clique of size \( k \) in \( G \)"** can be **reformulated** as:
    - **Does \( G \) contain a subgraph isomorphic to a \( k \)-clique?**

### **Transformation**
1. Construct an instance of **Subgraph Isomorphism** where:
   - Let **\( H \)** be a **\( k \)-clique** (a complete graph of size \( k \)).
   - Let **\( G \)** be the input graph from the **Clique problem**.
2. If a **subgraph isomorphic to \( H \)** exists in \( G \), it means \( G \) contains a **clique of size \( k \)**.

### **Conclusion**
Since **finding a clique of size \( k \)** is **NP-complete**, and **Clique** is a **special case** of **Subgraph Isomorphism**, this proves that **Subgraph Isomorphism is NP-complete**.

# **Bounded Degree Spanning Tree**

## **Why is this problem hard?**
- A **spanning tree** can be found in **polynomial time** using algorithms like **Kruskal’s** or **Prim’s**.
- However, what makes this problem difficult is the **constraint on the degree** of each vertex.
- The challenge:
  - We need to find a **spanning tree** that satisfies a specific **degree constraint**.
  - In the **worst case**, the number of possible spanning trees in a connected graph is **exponential**.
  - This results in **exponential choices**, leading to an **exponential runtime**.

---

## **Problem Definition**
### **Instance:**
- A **graph** \( G = (V, E) \).
- A **positive integer** \( K = |V| - 1 \).

### **Question:**
- **Is there a spanning tree** for \( G \) in which **no vertex** has a degree **exceeding \( K \)**?
- Formally, is there a subset **\( E' \subseteq E \)** such that:
  - \( |E'| = |V| - 1 \) (i.e., it forms a spanning tree).
  - The graph **\( G' = (V, E') \)** is **connected**.
  - **No vertex** in \( V \) is included in more than **\( K \)** edges from \( E' \).

---

## **Proving NP-Completeness**
To prove that **Bounded Degree Spanning Tree** is **NP-complete**, we reduce it from the **Hamiltonian Path Problem**.

### **Why use Hamiltonian Path?**
- The **Hamiltonian Path Problem** is similar to the **Hamiltonian Circuit**, but:
  - Instead of forming a **cycle**, it seeks a **path** that visits **all vertices exactly once**.
- This problem is known to be **NP-complete**.

### **Reduction Idea**
- The **Hamiltonian Path Problem** can be **seen as a restricted version** of the **Bounded Degree Spanning Tree**.
- We introduce a **restriction** on \( K \) by setting **\( K = 2 \)**.
  - This means we are looking for a **spanning tree** where each vertex has a **degree at most 2**.
- **Why does this work?**
  - A **Hamiltonian Path** is a sequence of **connected vertices** with **no repeating edges or vertices**.
  - The **starting and ending vertices** have **degree 1**.
  - All **intermediate vertices** have **degree 2**.
  - This structure **satisfies** the constraints of a **bounded degree spanning tree** when **\( K = 2 \)**.

---

## **Transformation**
- **Copy the input graph** from the **Hamiltonian Path Problem**.
- **Set \( K = 2 \)**.
- If there is a **Hamiltonian Path** in the original graph, then in the transformed instance:
  - The **same path exists**.
  - It forms a **spanning tree** in which **each vertex has a degree of at most 2**.

### **Conclusion**
- Since **Hamiltonian Path** is **NP-complete**, and we have reduced it to the **Bounded Degree Spanning Tree** problem, this proves that **Bounded Degree Spanning Tree is NP-complete**.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/c696c441-5460-40b2-9831-99363210bc61" />

# **Minimum Equivalent Digraph (MED)**

## **Proof: Reduction to Directed Hamiltonian Circuit**
To prove that **Minimum Equivalent Digraph (MED)** is **NP-complete**, we reduce it from the **Directed Hamiltonian Circuit (DHC)** problem.

### **Restriction to Directed Hamiltonian Circuit**
- We **restrict MED to instances where the input graph \( G \) is strongly connected**.
- A **strongly connected** graph means that for **every pair of vertices \( u, v \)**:
  - There exists a **directed path** from \( u \) to \( v \).
  - There exists a **directed path** from \( v \) to \( u \).
- We set **\( K = |V| \)**.

> **Note:** This is actually a **restriction** to the **Directed Hamiltonian Circuit for Strongly Connected Digraphs**. However, the **NP-completeness** of that problem follows immediately from the known constructions for **Hamiltonian Circuit (HC) and Directed HC**.

---

## **Why is DHC a Special Case of Minimum Equivalent Digraph?**
- The **Directed Hamiltonian Circuit problem** asks whether there exists a **cycle** that **visits every vertex exactly once** in a **directed graph**.
- We claim that **DHC is a special case of MED** where **\( K = |V| \)**.

### **Transformation of DHC to MED**
1. If we have a **"yes" instance** of **Directed Hamiltonian Circuit**, then:
   - There exists a **cycle covering all vertices**.
   - This means that **every vertex** is strongly connected to **all other vertices** (because it is part of a **Hamiltonian cycle**).
   - Thus, for every pair **\( u, v \)**, there exists a **directed path from \( u \) to \( v \) and from \( v \) to \( u \)**.
  
2. **Transforming into MED**:
   - **Copy the same graph**.
   - **Set \( K = |V| \)**.
   - The **Hamiltonian circuit is still present** in the transformed graph.
   - To satisfy the **edge constraint** (\( |E'| \leq |V| \)), we construct **\( G' \)**:
     - **Keep the same vertices**.
     - **Include only the edges from the Hamiltonian circuit**.

3. **Why does this satisfy MED constraints?**
   - We ensure **\( |E'| \leq |V| \)**.
   - The graph remains **strongly connected** because:
     - **All vertices were already connected to each other** in the original **DHC instance**.
     - Since we included **only the Hamiltonian circuit edges**, strong connectivity is preserved.

---

## **Key Conclusion**
- If we are allowed at most **\( |V| \) edges** (**\( K = |V| \)**) and still require **strong connectivity**, the only possible structure is a **single cycle** that **includes all vertices**—i.e., a **Hamiltonian Circuit**.
- Thus, the problem reduces to finding a **Directed Hamiltonian Circuit**, which is **NP-complete**.

---

## **Verification of the Certificate**
- To verify the solution efficiently, we use **Breadth-First Search (BFS)**.
- **Verification Process**:
  1. Pick any vertex from \( G \).
  2. Perform **BFS** to record **reachability** (i.e., which vertices are connected).
  3. Perform **BFS** on the same vertex in \( G' \).
  4. Check if the reachability in \( G \) and \( G' \) are the **same**.
- **Complexity of Verification**:
  - BFS runs in **\( O(V + E) \)**.
  - We perform BFS for **each vertex**: \( O(V (V + E)) \).
  - Since this is **polynomial**, verification is efficient.

---

## **Final Conclusion**
- Since **DHC is NP-complete**, and we **transformed it** into an instance of **MED**, this proves that **Minimum Equivalent Digraph is NP-complete**.

# **Knapsack Problem and Its Relation to Partition**

## **Problem Definition**
We are given a **set of elements**, where **each element** has:
- A **value**.
- A **size**.

### **Goal:**
- Select elements such that:
  - Their **total size** \( \leq B \).
  - Their **total value** \( \geq K \).
  - \( B \) and \( K \) are both **integers**.

---

## **Partition Problem as a Special Case of Knapsack**
The **Partition Problem** is defined as follows:

- Given a **set \( S \)** of elements, can we **partition** \( S \) into **two subsets** where the **sum of elements in each subset** is **exactly \( S/2 \)**?

### **Viewing Partition as Knapsack**
- We can think of **Partition** as trying to **pick elements** from \( S \) such that:
  - **Total size = \( S/2 \)**
  - **Total value = \( S/2 \)**.
- This makes **Partition a special case of Knapsack**, where:
  - **\( B = S/2 \) (size constraint)**
  - **\( K = S/2 \) (value constraint)**.

### **Transformation from Partition to Knapsack**
1. **Copy all elements of \( S \)** into the Knapsack instance.
2. **Set the value and size** of each element **to be its own value**.

---

## **Correctness of the Transformation**
### **1. Partition to Knapsack ("Yes" Instance)**
- If we have a **"yes" instance of Partition**, then:
  - We can divide \( S \) into **two subsets**, each summing to **\( S/2 \)**.
  - Since we **copied elements** and **set their size and value** to their value in \( S \), we can:
    - Pick elements with **total value \( S/2 \)** (meeting the **Knapsack value constraint** \( K \)).
    - Pick elements with **total size \( S/2 \)** (meeting the **Knapsack size constraint** \( B \)).

Thus, a **"yes" instance of Partition** implies a **"yes" instance of Knapsack**.

---

### **2. Knapsack to Partition ("Yes" Instance)**
- If we have a **"yes" instance of Knapsack**, then:
  - We can **pick elements** whose **total value** \( \geq S/2 \) and **total size** \( \leq S/2 \).
  - Since the **size and value** of each element are **the same**, the only valid way to satisfy both constraints is to select elements that sum **exactly** to \( S/2 \).
  - These **selected elements** correspond to **one subset** of the **Partition solution**.
  - The **remaining elements** form the **second subset**.

Thus, a **"yes" instance of Knapsack** implies a **"yes" instance of Partition**.

---

## **Final Conclusion**
- Since **Partition is NP-complete**, and we **transformed it** into an instance of **Knapsack**, this proves that **Knapsack is NP-complete** as well.
- This reduction confirms that **Partition is a special case of Knapsack**.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/ceef2c12-46b2-4911-bc39-afd06a460c06" />

# **Multiprocessor Scheduling and Its Relation to Partition**

## **Problem Definition**
- The **Multiprocessor Scheduling Problem** involves:
  - A **set of tasks**, each with a specific **length**.
  - \( m \) **processors** available for scheduling.
  - A **deadline \( D \)** that determines the maximum load any processor can handle.

### **Goal:**
- Assign tasks to **\( m \)** processors such that:
  - The **maximum workload assigned to any processor** does not exceed **\( D \)**.
  - The total execution time is **minimized**.

---

## **Partition as a Special Case of Multiprocessor Scheduling**
The **Partition Problem** is defined as:
- Given a **set \( S \) of numbers**, can we **partition \( S \) into two subsets** where:
  - The **sum of elements in each subset** is **exactly \( S/2 \)**?

### **Restricting Multiprocessor Scheduling to Partition**
To transform **Multiprocessor Scheduling** into **Partition**, we apply the following restrictions:
- **Set \( m = 2 \)** (only two processors).
- **Set \( D = S/2 \)** (deadline is the sum of task lengths divided by 2).
- **Copy the set \( S \)** from the **Partition Problem** and treat it as the **set of tasks**.
- **Associate each task’s length** with the **corresponding element in \( S \)**.

---

## **Correctness of the Transformation**
### **1. Partition to Multiprocessor Scheduling ("Yes" Instance)**
- If we have a **"yes" instance of Partition**, then:
  - We can divide \( S \) into **two subsets**, each summing to **\( S/2 \)**.
  - These subsets **match the two processor workloads** in the scheduling problem.
  - Since the **tasks correspond directly to partition elements**, the tasks can be scheduled such that:
    - The **maximum workload assigned to a processor is \( S/2 \)**, which **respects the constraint \( D \)**.
  - Thus, a **"yes" instance of Partition** implies a **"yes" instance of Multiprocessor Scheduling**.

---

### **2. Multiprocessor Scheduling to Partition ("Yes" Instance)**
- If we have a **"yes" instance of Multiprocessor Scheduling**, then:
  - The **maximum load per processor** is **\( \leq S/2 \)**.
  - Since all tasks come from \( S \), the **only valid way** to respect the constraint is if **each processor gets exactly \( S/2 \)**.
  - The tasks assigned to each processor **form a valid partition** of \( S \).
  - Thus, a **"yes" instance of Multiprocessor Scheduling** implies a **"yes" instance of Partition**.

---

### **3. What Happens in a "No" Instance?**
- If **Partition has a "no" instance**, then:
  - We **cannot** split \( S \) into two subsets **with sum exactly \( S/2 \)**.
  - In the **Multiprocessor Scheduling instance**, this means:
    - At least **one processor** will be **overloaded** beyond \( S/2 \).
  - Thus, the **maximum workload per processor will exceed \( D = S/2 \)**, violating the scheduling constraint.

---

## **Final Conclusion**
- Since **Partition is NP-complete**, and we **transformed it** into an instance of **Multiprocessor Scheduling**, this proves that **Multiprocessor Scheduling is NP-complete**.
- This reduction confirms that **Partition is a special case of Multiprocessor Scheduling**.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/b830bf31-8a24-4984-9bb5-c5faaa17a71e" />

# **Set Packing and Its Relation to Independent Set**

## **Problem Definition**
- The **Set Packing Problem** involves:
  - A **collection of sets \( C \)**.
  - An integer \( K \).

### **Goal:**
- Find **at least \( K \) disjoint sets** from \( C \).
- These **selected sets** should **not share any elements**.

---

## **Independent Set as a Special Case of Set Packing**
The **Independent Set Problem** is defined as:
- Given a **graph \( G = (V, E) \)** and an integer \( K \), can we find a subset of vertices **\( V' \subseteq V \)** such that:
  - **\( |V'| \geq K \) (size constraint)**.
  - **No two vertices in \( V' \) are adjacent** (i.e., they do not share an edge).

### **Restricting Set Packing to Independent Set**
To transform **Set Packing** into **Independent Set**, we apply the following restrictions:
- **Each set in \( C \) represents a vertex’s edges**.
- **Copy the same \( K \) from Independent Set to Set Packing**.

---

## **Correctness of the Transformation**
### **1. Independent Set to Set Packing ("Yes" Instance)**
- If we have a **"yes" instance of Independent Set**, then:
  - There exists a **subset of vertices \( V' \)** of size **\( \geq K \)**.
  - These vertices **do not share an edge**, meaning they are **not adjacent**.
  - The **set of edges for each vertex is copied** into a set in **\( C \)**.
  - Since the **selected vertices do not share edges**, their corresponding **sets in \( C \) must be disjoint**.

Thus, a **"yes" instance of Independent Set** implies a **"yes" instance of Set Packing**.

---

### **2. Set Packing to Independent Set ("Yes" Instance)**
- If we have a **"yes" instance of Set Packing**, then:
  - There exist **at least \( K \) disjoint sets**.
  - This means these sets **do not share any element**.
  - Since each **set in \( C \) corresponds to a vertex’s edges**, this implies that:
    - The vertices linked to these disjoint sets **do not share an edge**.
    - This forms an **Independent Set of size \( \geq K \)**.

Thus, a **"yes" instance of Set Packing** implies a **"yes" instance of Independent Set**.

---

### **Final Conclusion**
- Since **Independent Set is NP-complete**, and we **transformed it** into an instance of **Set Packing**, this proves that **Set Packing is NP-complete**.
- This reduction confirms that **Independent Set is a special case of Set Packing**.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/d94bd71c-e0a6-45de-90e9-04bb1bbf592d" />

# **Partition into Hamiltonian Subgraphs and Its Relation to Hamiltonian Circuit**

## **Problem Definition**
- The **Partition into Hamiltonian Subgraphs Problem** involves:
  - A **graph \( G = (V, E) \)**.
  - An integer \( k \).

### **Goal:**
- Partition \( G \) into **\( k \) subgraphs** such that **each subgraph contains a Hamiltonian circuit**.

---

## **Hamiltonian Circuit as a Special Case of Partition into Hamiltonian Subgraphs**
The **Hamiltonian Circuit Problem** is defined as:
- Given a **graph \( G = (V, E) \)**, is there a **cycle** that **visits every vertex exactly once**?

### **Restricting Partition into Hamiltonian Subgraphs to Hamiltonian Circuit**
To transform **Partition into Hamiltonian Subgraphs** into **Hamiltonian Circuit**, we apply the following restriction:
- **Set \( k = 1 \)**.
- This means that the **entire graph must form a single Hamiltonian subgraph**, which is equivalent to checking if the graph itself **has a Hamiltonian circuit**.

---

## **Correctness of the Transformation**
### **1. Hamiltonian Circuit to Partition into Hamiltonian Subgraphs ("Yes" Instance)**
- If we have a **"yes" instance of Hamiltonian Circuit**, then:
  - There exists a **cycle** that **visits every vertex exactly once**.
  - Setting **\( k = 1 \)** means we must find **one Hamiltonian subgraph**.
  - Since the entire graph already contains a **Hamiltonian circuit**, this requirement is satisfied.

Thus, a **"yes" instance of Hamiltonian Circuit** implies a **"yes" instance of Partition into Hamiltonian Subgraphs (with \( k = 1 \))**.

---

### **2. Partition into Hamiltonian Subgraphs to Hamiltonian Circuit ("Yes" Instance)**
- If we have a **"yes" instance of Partition into Hamiltonian Subgraphs** with **\( k = 1 \)**:
  - This means the entire graph is **one Hamiltonian subgraph**.
  - Since this subgraph must contain a **Hamiltonian circuit**, it follows that the **original graph itself has a Hamiltonian circuit**.

Thus, a **"yes" instance of Partition into Hamiltonian Subgraphs (with \( k = 1 \))** implies a **"yes" instance of Hamiltonian Circuit**.

---

## **Final Conclusion**
- Since **Hamiltonian Circuit is NP-complete**, and we **transformed it** into an instance of **Partition into Hamiltonian Subgraphs**, this proves that **Partition into Hamiltonian Subgraphs is NP-complete**.
- This reduction confirms that **Hamiltonian Circuit is a special case of Partition into Hamiltonian Subgraphs**.

<img width="467" alt="image" src="https://github.com/user-attachments/assets/8dc0d3b6-3a82-456e-a4e4-d21afd53ad43" />

<img width="468" alt="image" src="https://github.com/user-attachments/assets/897abf69-1f26-4d42-8fa1-5c75e1989d79" />

# **Largest Common Subgraph and Its Relation to Subgraph Isomorphism**

## **Problem Definition**
- The **Largest Common Subgraph Problem** involves:
  - **Two graphs**, \( G_1 = (V_1, E_1) \) and \( G_2 = (V_2, E_2) \).
  - An integer \( K \).

### **Goal:**
- Find two **subgraphs**:
  - One in \( G_1 \) and one in \( G_2 \).
  - These subgraphs should be **isomorphic**.
  - They should contain at least **\( K \) edges**.

---

## **Subgraph Isomorphism as a Special Case of Largest Common Subgraph**
The **Subgraph Isomorphism Problem** is defined as:
- Given two graphs, **does \( G_1 \) contain a subgraph that is isomorphic to \( G_2 \)**?

### **Restricting Largest Common Subgraph to Subgraph Isomorphism**
To transform **Largest Common Subgraph** into **Subgraph Isomorphism**, we apply the following restriction:
- **Set \( K = |E_2| \)**.
  - This means we are searching for a **common subgraph with exactly \( |E_2| \) edges**.
  - Effectively, we are asking: **Is there a subgraph in \( G_1 \) that is isomorphic to \( G_2 \)?**

---

## **Correctness of the Transformation**
### **1. Subgraph Isomorphism to Largest Common Subgraph ("Yes" Instance)**
- If we have a **"yes" instance of Subgraph Isomorphism**, then:
  - There exists a **subgraph of \( G_1 \)** that is **isomorphic to \( G_2 \)**.
  - Since **\( G_2 \) contains \( |E_2| \) edges**, the subgraph in \( G_1 \) also contains **exactly \( |E_2| \) edges**.
  - Since we **set \( K = |E_2| \)**, this satisfies the **Largest Common Subgraph condition**.

Thus, a **"yes" instance of Subgraph Isomorphism** implies a **"yes" instance of Largest Common Subgraph (with \( K = |E_2| \))**.

---

### **2. Largest Common Subgraph to Subgraph Isomorphism ("Yes" Instance)**
- If we have a **"yes" instance of Largest Common Subgraph** with **\( K = |E_2| \)**:
  - There exists a **common subgraph between \( G_1 \) and \( G_2 \)** with **exactly \( |E_2| \) edges**.
  - This means a **subgraph in \( G_1 \) is isomorphic to \( G_2 \)**.
  - Since **\( G_2 \) itself is a subgraph with \( |E_2| \) edges**, the isomorphic subgraph in \( G_1 \) must be **exactly \( G_2 \)**.

Thus, a **"yes" instance of Largest Common Subgraph (with \( K = |E_2| \))** implies a **"yes" instance of Subgraph Isomorphism**.

---

## **Final Conclusion**
- Since **Subgraph Isomorphism is NP-complete**, and we **transformed it** into an instance of **Largest Common Subgraph**, this proves that **Largest Common Subgraph is NP-complete**.
- This reduction confirms that **Subgraph Isomorphism is a special case of Largest Common Subgraph**.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/f6c5491b-df75-4456-902c-6620b8d56590" />

# **Minimum Sum of Squares and Its Relation to Partition**

## **Problem Definition**
- The **Minimum Sum of Squares Problem** involves:
  - A **set \( A \)** of elements.
  - An integer **\( K \)** representing the number of subsets.
  - An integer **\( J \)** representing a constraint on the sum of squares.

### **Goal:**
- Partition \( A \) into \( K \) subsets such that:
  - The **sum of the squares of the subset sums** does not exceed **\( J \)**.

---

## **Partition as a Special Case of Minimum Sum of Squares**
The **Partition Problem** is defined as:
- Given a **set \( S \)** of numbers, can we **partition \( S \) into two subsets** such that:
  - The **sum of elements in each subset** is **exactly \( S/2 \)**?

### **Restricting Minimum Sum of Squares to Partition**
To transform **Minimum Sum of Squares** into **Partition**, we apply the following restrictions:
- **Set \( K = 2 \)** (we must partition into two subsets).
- **Set \( J = S^2/2 \)**.
  - This is derived from the partition constraint:
    \[
    (S/2)^2 + (S/2)^2 = S^2/2
    \]
- **Copy the set \( S \)** from the **Partition Problem** into **\( A \)**.
- **Set the length of each element** in \( A \) to be the **value of the corresponding element in \( S \)**.

---

## **Correctness of the Transformation**
### **1. Partition to Minimum Sum of Squares ("Yes" Instance)**
- If we have a **"yes" instance of Partition**, then:
  - We can split \( S \) into **two subsets** with **equal sum \( S/2 \)**.
  - The **sum of their squares** is:
    \[
    (S/2)^2 + (S/2)^2 = S^2/2
    \]
  - Since **this satisfies the constraint \( J = S^2/2 \)**, the solution is valid.

Thus, a **"yes" instance of Partition** implies a **"yes" instance of Minimum Sum of Squares (with \( K = 2, J = S^2/2 \))**.

---

### **2. Why Setting \( J \) Ensures "No" Instances Align?**
- If we have a **"no" instance of Partition**, then:
  - We **cannot** split \( S \) into **two subsets** with exactly **\( S/2 \) each**.
  - Instead, we get one subset with **sum \( S/2 + d \)** and another with **\( S/2 - d \)**.
  - If we compute the **sum of their squares**, we get:
    \[
    (S/2 + d)^2 + (S/2 - d)^2
    \]
  - Expanding the equation:
    \[
    (S/2)^2 + d^2 + (S/2)^2 + d^2 = S^2/2 + 2d^2
    \]
  - This sum is **strictly greater than \( S^2/2 \) because \( 2d^2 > 0 \)**.

Thus, in a **"no" instance of Partition**, the sum of squares **always exceeds \( S^2/2 \)**, which means the **Minimum Sum of Squares constraint is violated**.

---

## **Final Conclusion**
- Since **Partition is NP-complete**, and we **transformed it** into an instance of **Minimum Sum of Squares**, this proves that **Minimum Sum of Squares is NP-complete**.
- This reduction confirms that **Partition is a special case of Minimum Sum of Squares**.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/0c8a70f2-40df-4d8f-99c8-ac9c6fe0e6ec" />

# **Local Replacement: Feedback Vertex Set and Its Relation to Vertex Cover**

## **Problem Definition**
The **Feedback Vertex Set Problem** involves:
- A **graph \( G = (V, E) \)**.
- An integer \( K \).

### **Goal:**
- Find a **subset of vertices** such that **removing them breaks all cycles in the graph**.

---

## **Vertex Cover as a Special Case of Feedback Vertex Set**
The **Vertex Cover Problem** is defined as:
- Given a **graph \( G = (V, E) \)** and an integer \( K \), can we find a subset of vertices **\( V' \subseteq V \)** such that:
  - **Every edge in \( G \) has at least one endpoint in \( V' \)**.

### **Mapping Vertex Cover to Feedback Vertex Set**
- In **Vertex Cover**, the fundamental unit is the **edge**.
- In **Feedback Vertex Set**, we need to **eliminate cycles**.
- To establish an equivalent **Feedback Vertex Set** instance from a **Vertex Cover** instance, we introduce **local modifications**:
  - **For every edge \( (u, v) \) in \( G \)**, we introduce a **corresponding cycle**:
    - Add a **new vertex \( w \)**.
    - Create **directed edges**:
      - \( u \to w \)
      - \( w \to v \)
      - \( v \to u \)

- This transformation **ensures that every edge in the original graph now corresponds to a directed cycle**.

---

## **Correctness of the Transformation**
### **1. Vertex Cover to Feedback Vertex Set ("Yes" Instance)**
- If we have a **"yes" instance of Vertex Cover**, then:
  - There exists a subset **\( V' \)** that covers all edges in the original graph.
  - In the **Feedback Vertex Set instance**, every added cycle contains at least **one vertex from \( V' \)**.
  - **Removing these vertices** eliminates **all cycles**, forming a valid **Feedback Vertex Set**.

Thus, a **"yes" instance of Vertex Cover** implies a **"yes" instance of Feedback Vertex Set**.

---

### **2. Why This Transformation Works?**
- Since **every edge in the original graph is transformed into a cycle**, covering **all edges** in the original graph ensures that:
  - Each **cycle** in the transformed graph contains at least one vertex from the **Feedback Vertex Set**.
  - Removing these vertices **eliminates all cycles**.
  - Thus, the **Feedback Vertex Set** contains the same vertices as the **Vertex Cover**.

---

## **Final Conclusion**
- Since **Vertex Cover is NP-complete**, and we **transformed it** into an instance of **Feedback Vertex Set**, this proves that **Feedback Vertex Set is NP-complete**.
- This reduction confirms that **Vertex Cover is a special case of Feedback Vertex Set**.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/ebe90b15-91ff-42e5-b2a3-ed310c0ba41d" />

# **Dominating Set and Its Relation to Vertex Cover**

## **Problem Definition**
The **Dominating Set Problem** involves:
- A **graph \( G = (V, E) \)**.
- An integer \( K \).

### **Goal:**
- Find a subset of vertices \( D \subseteq V \) such that:
  - Every vertex in \( G \) is either in \( D \) or **adjacent to a vertex in \( D \)**.
  - \( |D| \leq K \).

---

## **Vertex Cover as a Special Case of Dominating Set**
The **Vertex Cover Problem** is defined as:
- Given a **graph \( G = (V, E) \)** and an integer \( K \), can we find a subset of vertices **\( V' \subseteq V \)** such that:
  - **Every edge in \( G \) has at least one endpoint in \( V' \)**.

### **Initial Attempt: Direct Copy of \( G \) and \( K \)**
- One **initial idea** is to **copy the same graph** and **use the same \( K \)**.
- However, this **does not always work** because:
  - There exist cases where **no vertex cover** of size \( \leq K \) can be found.
  - But a **dominating set** satisfying \( K \) **still exists**.

- This means that a **"no" instance of Vertex Cover** could still be a **"yes" instance of Dominating Set**, which **breaks** the transformation.

---

## **Refining the Transformation**
To ensure a **valid reduction**, we introduce a **modification**:
1. **For every edge \( (u, v) \) in \( G \)**:
   - Add a **new vertex \( w \)**.
   - Connect \( w \) to both \( u \) and \( v \).

2. **Effect of this Modification:**
   - Now, in order to form a **valid dominating set**, at least **one of the two endpoints of every edge must be included**.
   - This **matches** the behavior of **Vertex Cover**, where at least **one endpoint of every edge must be selected**.

3. **Copy \( K \) from Vertex Cover to Dominating Set**:
   - Since **Vertex Cover ensures that all edges are covered**, the transformation guarantees:
     - If no **vertex cover** exists for size \( \leq K \), then no **dominating set** can be found either.
     - If a **vertex cover exists**, the corresponding **dominating set** exists.

---

## **Correctness of the Transformation**
### **1. Vertex Cover to Dominating Set ("Yes" Instance)**
- If we have a **"yes" instance of Vertex Cover**, then:
  - There exists a subset **\( V' \)** of size \( \leq K \) that covers **all edges**.
  - In the **transformed Dominating Set instance**, every **added vertex \( w \)** is connected to both endpoints.
  - The **vertex cover ensures that all edges are covered**, meaning all **vertices are either in \( V' \) or adjacent to \( V' \)**.
  - Thus, this subset forms a **valid dominating set**.

Thus, a **"yes" instance of Vertex Cover** implies a **"yes" instance of Dominating Set**.

---

### **2. Why This Transformation Works?**
- Since **every edge in the original graph is now part of a triangle (due to the added vertex \( w \))**, covering **all edges** in the original graph ensures:
  - Each **vertex in \( G \)** is either in the **dominating set** or adjacent to a **vertex in the dominating set**.
  - This satisfies the **Dominating Set condition**.

---

## **Final Conclusion**
- Since **Vertex Cover is NP-complete**, and we **transformed it** into an instance of **Dominating Set**, this proves that **Dominating Set is NP-complete**.
- This reduction confirms that **Vertex Cover is a special case of Dominating Set**.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/4c62ee6a-eb88-469f-8fb9-c5d6b4d3d158" />

# **Steiner Tree in Graphs and Its Relation to Exact Cover by 3-Sets (X3C)**

## **Problem Definition**
The **Steiner Tree Problem in Graphs** involves:
- A **graph \( G = (V, E) \)**.
- A set of **required vertices \( R \subseteq V \)**.
- An integer \( K \).

### **Goal:**
- Find a **subtree** of \( G \) that:
  - **Includes all vertices in \( R \)**.
  - **Has at most \( K \) edges**.

---

## **Exact Cover by 3-Sets (X3C) as a Special Case of Steiner Tree**
The **Exact Cover by 3-Sets (X3C) Problem** is defined as:
- Given:
  - A **finite set \( X \)** where \( |X| = 3q \).
  - A **collection \( C \) of 3-element subsets of \( X \)**.
- Question:
  - Does there exist a subcollection **\( C' \subseteq C \)** such that:
    - \( C' \) **exactly covers** \( X \) (each element appears in exactly one subset in \( C' \)).
    - \( |C'| = q \), meaning the **exact number of subsets needed** to cover \( X \) is \( q \).

### **Transforming X3C to Steiner Tree**
To ensure an equivalent transformation, we must:
1. **Map elements and subsets to vertices and edges**:
   - Create a **vertex for each element** in \( X \).
   - Create a **vertex for each subset** in \( C \).
   - Connect each **subset vertex** to the **three corresponding element vertices**.

2. **Ensure proper connectivity**:
   - Introduce a **central vertex \( V \)**.
   - Connect **\( V \)** to all **subset vertices**.

3. **Handle no instances correctly**:
   - A **"no" instance** in X3C can occur if:
     - There are **not enough subsets** to cover \( X \).
     - Some subsets **overlap** (i.e., elements appear in multiple subsets).
   - These cases must be reflected in the **Steiner Tree instance** by ensuring cycles are introduced when overlap occurs.

4. **Set parameters**:
   - **\( K = 4q \)**:
     - **\( 3q \)** edges from **subset vertices to element vertices**.
     - **\( q \)** edges from the **central vertex \( V \) to subset vertices**.
   - **Set \( R \) to include all vertices**.

---

## **Correctness of the Transformation**
### **1. X3C to Steiner Tree ("Yes" Instance)**
- If we have a **"yes" instance of X3C**, then:
  - We can find **\( q \) subsets** that exactly cover \( X \).
  - These subsets **form a valid Steiner tree** with:
    - **\( 3q \) edges** connecting elements to subsets.
    - **\( q \) edges** connecting subsets to \( V \).
  - The total number of edges used is **\( 4q \)**, satisfying \( K \).

Thus, a **"yes" instance of X3C** implies a **"yes" instance of Steiner Tree (with \( K = 4q \))**.

---

### **2. Why Overlapping Subsets Lead to a "No" Instance**
- If **subsets overlap**, multiple elements may be included in different subsets.
- This causes **extra edges to be introduced** in the Steiner Tree instance.
- These additional edges **create cycles**, increasing the required \( K \) beyond \( 4q \).
- Since the Steiner Tree instance is constrained to **at most \( K = 4q \) edges**, this results in a **"no" instance**.

---

## **Final Conclusion**
- Since **X3C is NP-complete**, and we **transformed it** into an instance of **Steiner Tree**, this proves that **Steiner Tree is NP-complete**.
- This reduction confirms that **X3C is a special case of Steiner Tree**.










