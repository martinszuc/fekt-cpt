> Cleaned from Stirling PDF export. Original: 7_lab.md

---

## **Practical Lecture 7 -**

**Zero-knowledge Protocols**

CPT - Cryptologic Protocol Theory

Dr. Sara Ricci

Brno University of Technology

[ricci@vut.cz](mailto:ricci@vut.cz)

---

## Table of contents

Isomorphic graphs

Permutations

Zero-knowledge protocol

---

## Graph

Definition

A

graph

G = (V, E)

is an ordered pair consisting of a set V of vertices and a

set E of edges, which are unordered pairs of elements of V.

Example

We can try to write the figure in
formula.

We have:
- vertices V

= { 1, 2, 3, 4 },

- edges: E

= { (1, 2), (2, 3), (3, 4) } .

Therefore, the graph can be written as
G = (V, E) = ({ 1, 2, 3, 4 }, { (1, 2), (2, 3), (3, 4) }) .

---

## Isomorphic graphs

Two graphs are

isomorphic

means that they are "the same". More formally it

means that there exists a "label" permutation that bring one graph

G j

to

another

G i . **G** **1** **G** **2** **G** **3**

In order to check if two graphs are isomorphic, we can see if they have:

the same

#

of vertices

the same

#

of edges

the same degree

the same "connections" (we
need a permutation or find
differences in the degree of the
vertices)

---

## Isomorphic graphs: first check

**G** **1** **G** **2** **G** **3** G 1 G 2 G 3 #

Vertices

4 4 4 #

Edges

3 3 3

Degree

3 2 2

Connection

-

?

?

G₁

has degree 3 because Vertex 2 belongs to 3 edges.

If we find the permutation between

G₂

and

G₃

, then they are isomorphic.

---

## Isomorphic graphs: permutation

Definition

A

permutation

is a bijective map which rearranges the elements of an

ordered set V .

The following graphs are isomorphic.

**G** **2** **G** **3**

The permutation between

G₂

and

G₃

is:

π =

1 2 3 4 1 4 2 3

---

## How to apply a permutation

We can check

π(G₂)

?

= G₃ .

Exercise

We apply

π =

1 2 3 4 1 4 2 3

to G

2 = { 1, 2, 3, 4 }, { (1, 2), (2, 3), (3, 4) } . π(V) = π({ 1, 2, 3, 4 }) = { 1, 4, 2, 3 } = { 1, 2, 3, 4 } . π(E) = π({ (1, 2), (2, 3), (3, 4) })

that is:

π((1, 2)) = (1, 4) π((2, 3)) = (4, 2) π((3, 4)) = (2, 3)

Therefore,

π(G₂) = ({ 1, 2, 3, 4 }, { (1, 4), (4, 2), (2, 3) }) = G₃ .

---

## Inverse of a permutation

Given a permutation

π =

1 2 3 4 1 4 2 3

it is easy to compute the inverse. We need to:

write the vertices in order (a)

switching the "rows" (b)

π − 1 =

1 2 3 4 1 4 2 3

− 1 (a) =

1 3 4 2 1 2 3 4

(b) =

1 2 3 4 1 3 4 2

In fact,

π

◦

π − 1 =

1 2 3 4 1 4 2 3

◦

1 2 3 4 1 3 4 2





1 2 3 4 1 3 4 2 1 2 3 4





Exercise:

Try to invert

ϕ =

1 2 3 4 4 3 1 2

---

## Zero-knowledge protocol: Graph Isomorphism

**Prover**

**Verifier**

System parameters:

G₀, G₁

graphs,

k

iterations.

claims that

G₀, G₁

are isomorphic,

i.e. G₁ = π(G₀)

generates a random permutation

ϕ

of

G₀, i.e. G₂ = ϕ(G₀) G₂ −−−−−−−−−−−−→

chooses a bit

b ∈ R { 0, 1 } b ←−−−−−−−−−−−

sends back

ψ = ϕ − 1

if

b = 0

sends back

ψ = π

◦

ϕ − 1

if

b = 1 ψ −−−−−−−−−−−→

checks

G b

?

= ψ(G₂)

---

## Zero-knowledge protocol: Example

**Prover**

**Verifier**

System parameters:

G₀ = ({ 1, 2, 3, 4 }, { (1, 2), (2, 3), (3, 4) }), G₁ = ({ 1, 2, 3, 4 }, { (1, 2), (1, 3), (3, 4) })

graphs,

k

iterations.

G₁ = π(G₀), π =

1 2 3 4 4 3 1 2

ϕ =

1 2 3 4 1 4 2 3

G₂ = ϕ(G₀) = ({ 1, 2, 3, 4 }, { (1, 4), (4, 2), (2, 3) }) G₂ −−−−−−−−−−−−−→

chooses a bit

b = 0 ∈ R { 0, 1 } b ←−−−−−−−−−−−−

sends back

ψ = ϕ − 1 =

1 2 3 4 1 3 4 2

if

b = 0

sends back

ψ = π

◦

ϕ − 1

if

b = 1 ψ −−−−−−−−−−−−→

checks

G₀

?

= ϕ − 1 (G₂)

---

## Homework 7

Exercise

write G

1

in formula.

draw G

3

, where

G₃ = ({ 1, 2, 3, 4, 5 }, { (1, 3), (2, 4), (2, 3), (1, 4), (4, 5) })

are G

1

and G

3

isomorphic? Justify your answer.

Exercise

Let G

0 = {{ 1, 2, 3, 4 }, { (1, 2), (1, 3), (2, 4), (3, 4), (1, 4) }},

where

ϕ =

1 2 3 4 2 3 4 1

write a permutation different from

ϕ

and identity,

π =

1 2 3 4 ... ... ... ...

compute G

1 = π(G₀)

in formula.

compute

ϕ − 1 .

compute

π

◦

ϕ − 1 =

1 2 3 4 ... ... ... ...

apply Zero-Knowledge Protocol for one iteration.

---

Thank you for attention!

[ricci@vut.cz](mailto:ricci@vut.cz)

<https://axe.vut.cz/>
