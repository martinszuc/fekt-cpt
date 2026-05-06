> Cleaned from Stirling PDF export. Original: 10_lab.md

---

## **10. Anonymous Attribute-Based**

**Credentials**

CPT - Cryptologic Protocol Theory

Dr. Sara Ricci

Brno University of Technology

[ricci@vut.cz](mailto:ricci@vut.cz)

---

## Table of contents

Algebraic MAC

MAC vs Signature

Algebraic MAC computation

---

## Algebraic MAC

**User (**

U **)**

**Issuer/Verifier (**

V **)**

params

= (G, g, q)

message:

(m₁, . . ., m n) (m₁, . . ., m n) −

−−−−−−−−−−−−−−−−−−−

(x₀, . . ., x n) ∈ R Z ∗ q sk = (x₀, . . ., x n) σ = g₁ xo + P n i = 1 mi xi σ

←−−−−−−−−−−−−−−−−−−−−

Randomization:

r ∈ R Z q h = g r

ˆ

σ = σ r h,

ˆ

σ −

−−−−−−−−−−−−−−−−−−−−−

h

?

≡

ˆ

σ x₀ + P n i = 1 m i x i

---

## Short Boneh-Boyen Signature

**Signer**

S

**Verifier**

V

params

= (G₁, G₂, G T, g₁, g₂, q, e) sk ∈ R Z q

∖

{ 0 } pk = g sk 2 m ∈ Z q σ

g₁ sk + m₁ m, σ

−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−→

e(σ m, g₂) · e(σ, pk)

?

= e(g₁, g₂)

---

## Algebraic MAC vs SBB signature

Structure:

both built on Algebraic Structure.
Normally, MAC is based on hashing.

MAC - symmetric - need to share the sk between Signer and Verifier

Signature - asymmetric - only the Signer knows the sk

Speed:

MAC - symmetric - verification is faster

Signature - asymmetric - need of a pairing in the verification, therefore,
slower

---

## Algebraic MAC: Set-up

Let us understand the notation:

G

is an elliptic curve

E(F p)

of order

n

with

q

\|

n g ∈ G

is a point of order

q

Therefore, given

E(F₅) : y₂ = x₃ − x +

1 of order 8, we consider a point

A = (4, 1)

of order 4

Points

Order

∞ 1 (3, 0) 2 (4, 4), (4, 1) 4 (0, 1), (0, 4), (1, 1), (1, 4) 8 P + Q O A B C O O A B C A A B C O B B C O A C C O A B₂ A = B = (3, 0), 3 A = C = (4, 4), 4 A = ∞

---

## Algebraic MAC: Example

**User (**

U **)**

**Issuer/Verifier (**

V **)**

params

= (G = E(F₅), g = A, q = 4)

message:

(m₁) = (2) ∈ Z₄ (m₁) = (2) ∈ Z₄

−−−−−−−−−−−−−−−−−−−−−−−→

(x₀, x₁) = (1, 1) ∈ R Z ∗ 4 sk = (x₀, x₁) = (1, 1) σ = g₁ x₀ + P n i = 1 mi xi = (x₀ + x₁ m₁) − 1 A = (1 + 2) − 1 A = 3 A = C σ = C

←−−−−−−−−−−−−−−−−−−−−−−−−−

Randomization:

r = 2 ∈ R Z₄ h = g r = 2 A = B

ˆ

σ = σ r = 2 C = B(h,

ˆ

σ) = (B, B)

−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−→

B = h

?

≡

ˆ

σ x₀ + P n i = 1 m i x i = (1 + 2) B = 3 B = O + B = B

---

## Homework 10

Exercise

Compute the Algebraic MAC scheme with q

= 7

and g

=

C and two messsages.

P + Q O A B C D E F O O A B C D E F A A B C D E F O B B C D E F O A C C D E F O A B D D E F O A B C E E F O A B C D F F O A B C D E

---

Thank you for attention!

[ricci@vut.cz](mailto:ricci@vut.cz)

<https://axe.utko.feec.vutbr.cz/>
