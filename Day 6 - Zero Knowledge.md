---
tags: [cryptography, cpt, concept, day6]
aliases: [Zero Knowledge, ZK Proof, Graph Isomorphism, ZKP]
related: "[[Day 7 - Sigma Protocols]]"
---

# Zero-Knowledge Proofs

> [!tip] Core idea
> A zero-knowledge proof lets a Prover convince a Verifier they know a secret — **without revealing anything about the secret itself**.

---

## Graphs

A **graph** $G = (V, E)$ is a set of vertices $V$ and a set of edges $E$ (unordered pairs of vertices).

**Example:**
- Vertices: $V = \{1, 2, 3, 4\}$
- Edges: $E = \{(1,2), (2,3), (3,4)\}$
- Written: $G = (\{1,2,3,4\},\ \{(1,2),(2,3),(3,4)\})$

---

## Graph Isomorphism

Two graphs are **isomorphic** if there is a permutation $\pi$ that maps one to the other: $G_2 = \pi(G_1)$.

**Quick checks before finding the permutation:**

| Check | Must be equal |
|---|---|
| Number of vertices | $|V_1| = |V_2|$ |
| Number of edges | $|E_1| = |E_2|$ |
| Degree sequence | sorted list of vertex degrees |

If any check fails → **not isomorphic**. If all pass → search for the permutation.

---

## Permutations

A **permutation** $\pi$ is a bijective map on an ordered set. Written as:

$$\pi = \begin{pmatrix} 1 & 2 & 3 & 4 \\ 1 & 4 & 2 & 3 \end{pmatrix}$$

means: $1 \to 1$, $2 \to 4$, $3 \to 2$, $4 \to 3$.

**Apply $\pi$ to a graph:** remap each vertex, then remap each edge's endpoints.

$$\pi(\{(1,2),(2,3),(3,4)\}) = \{(1,4),(4,2),(2,3)\}$$

**Inverse $\pi^{-1}$:** sort the output row in ascending order, then swap rows.

$$\pi^{-1} = \begin{pmatrix} 1 & 2 & 3 & 4 \\ 1 & 3 & 4 & 2 \end{pmatrix}$$

**Composition** $\pi \circ \phi$: apply $\phi$ first, then $\pi$.

---

## ZK Protocol: Graph Isomorphism

**Public:** Graphs $G_0$ and $G_1$. Prover claims they are isomorphic ($G_1 = \pi(G_0)$), but does not reveal $\pi$.

| Prover | | Verifier |
|---|---|---|
| Choose random permutation $\phi$ | | |
| $G_2 = \phi(G_0)$ | $\xrightarrow{G_2}$ | |
| | $\xleftarrow{b}$ | $b \in_R \{0, 1\}$ |
| If $b=0$: $\psi = \phi^{-1}$ | | |
| If $b=1$: $\psi = \pi \circ \phi^{-1}$ | $\xrightarrow{\psi}$ | |
| | | Check: $G_b \stackrel{?}{=} \psi(G_2)$ |

Repeat $k$ times. Cheating probability after $k$ rounds: $\leq (1/2)^k$.

**Why zero-knowledge:** $G_2$ is a random re-labelling of $G_0$; the response $\psi$ only reveals the relationship between $G_2$ and one of $\{G_0, G_1\}$ — nothing about $\pi$ itself.

---

## Worked Example

$G_0 = (\{1,2,3,4\}, \{(1,2),(2,3),(3,4)\})$

$G_1 = (\{1,2,3,4\}, \{(1,2),(1,3),(3,4)\})$

Prover's secret: $\pi = \begin{pmatrix}1&2&3&4\\4&3&1&2\end{pmatrix}$ (so $G_1 = \pi(G_0)$)

Prover picks: $\phi = \begin{pmatrix}1&2&3&4\\1&4&2&3\end{pmatrix}$

$G_2 = \phi(G_0) = (\{1,2,3,4\}, \{(1,4),(4,2),(2,3)\})$

Verifier sends $b = 0$ → Prover sends $\psi = \phi^{-1} = \begin{pmatrix}1&2&3&4\\1&3&4&2\end{pmatrix}$

Verifier checks: $\psi(G_2) = G_0$ ✓

---

> [!warning] Common mistakes
> - When $b=1$, response is $\psi = \pi \circ \phi^{-1}$, **not** just $\pi$
> - Composition $\pi \circ \phi^{-1}$: apply $\phi^{-1}$ **first**, then $\pi$
> - A cheating Prover who does not know $\pi$ can only answer one bit correctly (50% chance per round)
