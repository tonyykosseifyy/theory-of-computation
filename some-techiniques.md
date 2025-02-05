## **General Guidelines for Reductions by Restriction**

1. **Identify a Known NP‑Complete Problem:**  
   - Start with a problem \( A \) that is known to be NP‑complete.
   - Example: The Directed Hamiltonian Circuit (DHC) problem is NP‑complete.

2. **Select a Restriction:**  
   - Find a natural, nontrivial subset of instances of \( A \) that still remains NP‑complete.  
   - The restriction should add extra properties or constraints that simplify the structure or make the reduction clearer.
   - Example: Restrict DHC to instances where the input graph is strongly connected. (Note that any graph with a Hamiltonian circuit is necessarily strongly connected, so this restriction does not weaken NP‑completeness.)

3. **Design the Transformation:**  
   - Show that every instance of the restricted version of \( A \) is also an instance of problem \( B \) (the target problem) or can be transformed into one.
   - The transformation must preserve the "yes" and "no" answers.
   - Example: For the MED problem, restrict to instances with parameter \( K = |V| \). In a strongly connected graph, any subgraph that preserves the reachability relation and has fewer than \(|V|\) arcs cannot exist; thus, having exactly \(|V|\) arcs (i.e., a cycle that covers all vertices—a Hamiltonian circuit) is equivalent to a “yes” instance of DHC.

4. **Prove Equivalence:**  
   - Argue that a solution to the restricted instance of \( A \) exists if and only if a solution to the corresponding instance of \( B \) exists.
   - This shows that if you could solve \( B \) efficiently, you could also solve the NP‑complete restricted version of \( A \) efficiently.
   - Example: In our case, if a strongly connected graph \( G \) (with \(|V|\) vertices) has a subgraph with fewer than \(|V|\) edges that preserves reachability, it would contradict the structure required by strong connectivity. Thus, a MED instance with \( K = |V| \) is a “yes” instance if and only if \( G \) has a directed Hamiltonian circuit.

5. **Conclude NP‑Completeness of the Target Problem:**  
   - Since the restricted subset of \( A \) is NP‑complete and every instance of it maps into \( B \), the target problem \( B \) must be NP‑hard.
   - If \( B \) is also in NP, then it is NP‑complete.
   - Example: Since the restricted DHC is NP‑complete and it reduces to MED, the Minimum Equivalent Digraph problem is NP‑complete.

---

## **Example: MED via Restriction from DHC**

- **Starting Point:**  
  The Directed Hamiltonian Circuit (DHC) problem is NP‑complete. We know that a graph has a Hamiltonian circuit only if it is strongly connected.

- **Restriction:**  
  Restrict to instances where the graph \( G \) is strongly connected, and set the parameter \( K = |V| \) (the number of vertices).  
  - In a strongly connected graph, any subgraph that preserves all reachability relationships must have at least \(|V|\) edges.
  - Therefore, a MED instance with \( K = |V| \) will have a “yes” answer if and only if there exists a subgraph with exactly \(|V|\) edges that preserves reachability—which is precisely a directed cycle that visits every vertex (a Hamiltonian circuit).

- **Mapping:**  
  Every strongly connected instance of DHC can be seen as an instance of MED by simply taking the same graph and requiring an equivalent subgraph with fewer than \(|V|\) edges.  
  - If the graph has a Hamiltonian circuit, then that circuit is the minimal equivalent subgraph, and its edge count is \(|V|\).
  - If no Hamiltonian circuit exists, no equivalent subgraph with fewer than \(|V|\) edges can exist.

- **Conclusion:**  
  This reduction by restriction shows that the hard instances of DHC (even when restricted to strongly connected graphs) are embedded within MED. Therefore, MED is NP‑hard (and, given it is in NP, NP‑complete).

---

## **Key Points to Remember**

- **Restriction is Valid:**  
  Proving NP‑hardness for a special (restricted) case is sufficient because if the general problem were easier, it would also solve the hard restricted instances.

- **Preservation of Yes/No Answers:**  
  Ensure that the transformation maintains the original problem’s decision (i.e., an instance of the restricted problem is a “yes” instance if and only if the corresponding transformed instance is a “yes” instance).

- **Clear Mapping:**  
  The transformation should be clear and, if possible, obvious enough that the one-to-one correspondence between the restricted instances and the target problem instances is maintained.

- **Applicability:**  
  Many NP‑completeness proofs use reductions by restriction because they allow us to focus on the “core” difficulty of a problem, often simplifying the reduction by considering only instances that naturally have the necessary properties (such as strong connectivity in this case).

---

This summary encapsulates the general method of reductions by restriction and demonstrates how it is applied in the given example.