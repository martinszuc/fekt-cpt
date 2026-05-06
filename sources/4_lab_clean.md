> Cleaned from Stirling PDF export. Original: 4_lab.md

---

## **Practical Lecture 4 -**

**Pairing-based Protocols**

CPT - Cryptologic Protocol Theory

Dr. Sara Ricci

Brno University of Technology

[ricci@vut.cz](mailto:ricci@vut.cz)

---

## Table of contents

Symmetric vs Asymmetric

MOV attack

3-Way Diffie-Hellman

Short Boneh-Boyen Signature

---

## Symmetric vs Asymmetric

e : G₁ × G₂ −→ Z ∗ p

A pairing is symmetric if

G₁ = G₂ .

Let

E₁, E₂

two different elliptic curves. Is the following pairing symmetric?

1 e : E₁ (F₇) × E₂ (F₇)

F ∗ 13 2 e : E₂ (F₇) × E₂ (F 11)

F ∗ 11 3 e : E₁ (F 13) × E₁ (F 13)

F ∗ 11

In Case 1,

e

is asymmetric since

E₁ ̸ = E₂ .

In Case 2,

e

is asymmetric since

E₂

is on two different fields

F₇ ̸ = F 11

and the

points (EC) depends on the fields and on the equation considered.
In Case 3,

e

is symmetric.

---

## (Simplified) MOV attack simulation 1/2

Let

e

be a symmetric pairing,

e : G × G −→ Z ∗ p(P, P) −→ g

Definition (Bilinear Assumption)

Let e

: G × G

G T

be a symmetric bilinear map where G

= G₁ = G₂

then

the ECDL problem in G

1, G₂

is no harder than the DL problem in G

T .

But if is it not true?

If the problem is easier in

G T

, we can try to recover

a

, given

P

and

aP .

But how?

---

## (Simplified) MOV attack simulation 2/2

Knowledge

: we know that

E(F 23)

has order 10, therefore we can consider the

map

e : E

\[

10

\]

× E

\[

10

\]

−→ Z ∗ 11

and we also know that

e(P, P) =

2 and

e(P, aP) = 5.

Note that 2 is a generator of

Z ∗ 11 .

MOV attack

we compute the powers of our generator 2 in

F 11

until we find 5

2 1 ≡ 2, 2 2 ≡ 4, 2 3 ≡ 8, 2 4 ≡ 5 e(P, aP) = 5 ≡ 2 4 mod 11,

that is

e(P, aP) = e(P, P) a = 2 4,

and

e(P, P) =

2, therefore

a = 4.

Remember: MOV attack works only with symmetric pairing.

---

## 3-way Diffie-Hellman

P + Q O P T S O O P T S P P T S O T T S O P S S O P T e(P, Q) O P T S O₁ 1 1 1 P₁ 2 4 3 T₁ 4 1 4 S₁ 3 4 2 g =

2 is a generator of

F₅

, that is

e(P, P) =

2, where

deg(P) =

4 and

e : E

\[

4

\]

× E

\[

4

\]

−→ F₅

Protocol (3-Way DH key agreement)

1

Alice: chooses a

∈ R F₅

, generates the key pair

(2, A = 2 P = T)

and broadcasts T

2

Bob: chooses b

∈ R F₅

, generates the key pair

(3, B = 3 P = S)

and broadcasts S

3

Charlie: chooses c

∈ R F₅

, generates the key pair

(2, A = 2 P = T)

and broadcasts P

4

Alice computes k

= e(B, C) a = g

abc

, Bob computes k

= e(A, C) b = g

abc

, and

Charlie computes k

= e(A, B) c = g

abc

. e(S, T) 2 ≡ e(T, T) 3 ≡ e(T, S) 2 4 2 ≡ 1 3 ≡ 4 2 mod 5

---

## Short Boneh-Boyen Signature

e(P, Q) O P₂ P = Q₃ P = M O₁ 1 1 1 R₁ 2 4 3 2 R = T₁ 4 1 4 3 R = V₁ 3 4 2 e : E₁

\[

4

\]

× E₂

\[

4

\]

−→ F₅

and

e(P, R) = 2

Signer

S

Verifier

V

System parameters:

e : G₁ × G₂

G T, P ∈ G₁, R ∈ G₂, q(sk, P k) = (a = 2, aR = T) P k = T m = 1 ∈ Z₄

∖

{ 0 } S = (a + m) − 1 P = (2 + 1) − 1 P = (3) − 1 P = 3 P = M mod 4 m = 1, S = M −

−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−

e(mS, R) · e(S, P k) = e(M, R) · e(M, T) = 3 ∗ 4 = 12 = 2 mod 5 e(P, R) = 2

---

## Homework 4

Exercise

Mov attack simulation.

Let P be a point in E

\[

16

\]

of order

16, e : E

\[

16

\]

× E

\[

16

\]

−→ Z ∗ 17

be a symmetric bilinear pairing, such that e

(P, P) = 6 .

If e

(P, kP) = 13,

find k .

---

Thank you for attention!

[ricci@vut.cz](mailto:ricci@vut.cz)

<https://axe.vut.cz/>
