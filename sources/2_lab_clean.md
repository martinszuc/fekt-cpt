> Cleaned from Stirling PDF export. Original: 2_lab.md

---

## **Practical Lecture 2 -**

**Elliptic Curve**

CPT - Cryptologic Protocol Theory

Dr. Sara Ricci

Brno University of Technology

[ricci@vut.cz](mailto:ricci@vut.cz)

---

## Table of contents

Recognize an Elliptic Curve

Points of an Elliptic Curve

Point addition/inverse of a point

---

## Elliptic Curves

All the curves can be represented in:

Form (Generalized Weierstrass form)

y₂ + a₁ xy + a₃ y = x₃ + a₂ x₂ + a₄ x + a₆,

where a

1, a₂, a₃, a₄, a₆ ∈ F q .

Question

Is

E i

an Elliptic Curve (in Generalized Weiestrass form)?

E₁ : y₂ − x = x₃ + 2 E₂ : y = x₃ − 3 + xy E₃ : y₂ = x₂ + x − 2 E₄ : y = x₃ − 3 x₂ − y₂

Proof.

For instance,

E₂

is not an elliptic curve because

y₂

is missing

E₄

is an elliptic with

a₁ = a₄ = a₆ = 0, a₃ =

1 and

a₂ = − 3

---

## Points of an Elliptic Curve

Given

E(F p) : y₂ = x₃ + 2 x + 1

The points

P = (0, − 1), Q = (1, 2)

and

T = (3, 1)

belongs to

E(F₅)

?

The points

P = (0, − 1), Q = (1, 2)

and

T = (3, 1)

belongs to

E(F 11)

?

Proof.

It is enough to substituite the points in the equation of

E(F p)

and see if it

holds.

P ∈ E(F₅)

? Yes, because

(− 1) 2 = 0 3 + 0 + 1, i.e. 1 = 1 mod 5. Q ∈ E(F₅)

? Yes, because

2 2 = 1 3 + 2 + 1 ⇒ 4 ≡ 4 mod 5. T ∈ E(F₅)

?

No

, because

1 2 = 3 3 + 6 + 1 ⇒ 1 ̸ = 2 + 2 ≡ 4 mod 5. T ∈ E(F 11)

?

Yes

, because

1 2 = 3 3 + 6 + 1 ⇒ 1 = 5 + 7 ≡ 1 mod 11.

The field is important!

---

## R = P + E Q

Given

P = (x p, y p)

and

Q = (x q, y q)

in

y₂ = x₃ + ax + b .

IF

x p ̸ = x q

, THEN

λ = y q − y p x q − x p

and

R = (λ₂ − x p − x q, λ(x p − x r) − y p)

IF

P = Q

and

y p ̸ =

0, THEN

λ = d x d y = 3 x₂ p + a₂ y p

and

R = (λ₂ − 2 x p, λ(x p − x r) − y p)

IF P=Q and

y p =

0, THEN

P + E P = ∞

IF

x p = x q

and

P ̸ = Q

, THEN

P + Q = ∞

Exercise

Given E

(F₅) : y₂ = x₃ + x + 1

and two its points P

= (0, 1)

and Q

= (2, 1)

. Compute

R = P +

Q and

2 P. λ = 1 − 1 2 − 0 = 0 2 = 0 ∗ 3 = 0 mod 5 R = (0 2 − 0 − 2, 0 (0 + 2) − 1) = (− 2, − 1) = (3, 4) mod 5

---

## The group law

Theorem

The addition of points on an elliptic curve E
satisfies the following properties:

1

Commutativity

: P₁ + P₂ = P₂ + P₁

for all P

1, P₂ ∈ E . 2

Existence of identity

: P + ∞ =

P for all P

∈ E . 3

Existence of inverses

:

Given P on E, there exists P

′

on E with

P + P ′ = ∞

. This point P

′

will usually be

denoted

− P.

The points on E form an

additive abelian group

with

∞

as the identity element.

1 2 −1 −2 1 −1 −2

•

∞ P

P'

Example

If P

= (2, 3)

, who is

− P

=?

Hint: watch the picture.

P = (2, − 3)

---

## Homework 3

Exercise

**Elliptic curve**

Let E

(F₇) : y₂ = x₃ + 2 x + 1

be an elliptic curve in

F₇, 1

Are A

= (3, 3), B = (0, 1), C = (2, − 3)

points of E

(F₇)

?

2

Compute R

= P +

Q, where P

= (x p, y p) = (1, 2), Q = (x q, y q) = (0, 1) . 3

If R

= (0, 1)

, which ones are the coordinates of

− R = (..., ...)

? And why?

Exercise

**Order of an Elliptic Curve**

Find the points of E

(F₇) : y₂ = x₃ − x − 1

with the algorithm explained in class (Theoretical Class 2, Slide 24).

---

Thank you for attention!

[ricci@vut.cz](mailto:ricci@vut.cz)

<https://axe.vut.cz/>
