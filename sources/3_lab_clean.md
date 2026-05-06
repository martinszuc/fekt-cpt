> Cleaned from Stirling PDF export. Original: 3_lab.md

---

## **Practical Lecture 3 -**

**EC Cryptography**

CPT - Cryptologic Protocol Theory

Dr. Sara Ricci

Brno University of Technology

[ricci@vut.cz](mailto:ricci@vut.cz)

---

## Table of contents

Summary

Order of EC points

EC Diffie-Hellman protocol

Torsion Points

Bilinear Pairing

---

## Summary: Order of an EC

Let

E

be the curve

y₂ = x₃ + x +

1 over

F₅ .

squares in

F₅ y y₂ 0 0

±

1 1

±

2 4

find the points

(x, y)

in

E(F₅) x x₃ + x + 1 y₂ y

points

0 1 1

±

1 (0, 1), (0, 4) 1 3 − − − 2 1 1

±

1 (2, 1), (2, 4) 3 1 1

±

1 (3, 1), (3, 4) 4 4 4

±

2 (4, 2), (4, 3) ∞ ∞ (∞, ∞) E(F₅)

has order 9.

---

## Summary:

R = P + E Q

Note (

R = P + E Q)

Let P

= (x p, y p)

and Q

= (x q, y q)

be two points of y

2 = x₃ + ax + b.

IF x

p ̸ = x q

, THEN

λ = y q − y p x q − x p

and R

= (λ₂ − x p − x q, λ(x p − x r) − y p) P =

Q and y

p ̸ = 0

, THEN

λ = d x d y = 3 x₂ p + a₂ y p

and R

= (λ₂ − 2 x p, λ(x p − x r) − y p)

IF P = Q and y

p = 0

, THEN

P + E P = ∞

IF x

p = x q

and P

̸ =

Q, THEN

P + E Q = ∞

---

## Order of elements and points

Definition

The order of an element divide the order of the group.

Order of

Z ∗ 11

is

ϕ(11) = 10.

Possible els. orders are: 1,2,5 and 10
(divisors of

ϕ(11)).

A generator is an el. of max. order: 10 (in
our case).

**1.**

Which order has

a =

3 in

Z ∗ 11

?

3 2 ≡ 9 ̸≡ 1 mod 11 3 5 ≡ 81 ∗ 3 ≡ 12 ≡ 1 mod 11

3 has order 5.

**2.**

Find an el. of order 2.

In

Z ∗ 11, g =

2 is a generator, therefore:







2 2 ̸≡ 1 mod 11 2 5 ̸≡ 1 mod 11 2 10 ≡ 1 mod 11

therefore,

(2 5) 2 ≡ 1 mod

11 and 2

5 ≡ 10 mod 11

has order 2.

Order of

E

\[

F p

\]

is

n

(its number of points).

Possible els. orders are the divisor of

n .

A generator is an el. of max. order:

n . **1.**

Which order has

P = (x p, y p) = (4, 1)

in

E(F₅) : y₂ = x₃ − x +

1?

Order of

E(F₅)

is 8, possible order of

P

are

1, 2,

4 and 8.

We have to check: 2

P, 4 P

and 8

P . λ = 3 x₂ p + a₂ y p = 3 ∗ 4 2 − 1 2 ∗ 1 = 1 mod 5 2 P = (λ₂ − 2 x p, λ(x p − x r) − y p) = (3, 0) 4 P = ∞

P has order 4.

---

## EC Diffie-Hellman protocol

Protocol (Diffie-Hellman over

E) H H H H P Q O A B C O O A B C A A B C O B B C O A C C O A B₂ A = B = (3, 0), 3 A = C = (4, 4), 4 A = ∞

If

a = 3, b =

2 and

P = A = (4, 1)

, then

**Alice**

**Bob**

P a = 3 A = 2 A + A P b = 2 A = B = B + A = C P a = C

−−−−−−−−−−−−−−−−−−−−−−→

P b = B

←−−−−−−−−−−−−−−−−−−−−−−

aP b = 3 B = 2 B + B bP a = 2 C = B = O + B = B

---

## Torsion Points

Let

E(F₅) : y₂ = x₃ − x + 1

be the elliptic curve generating

G₁

and

G₂ . E(F₅)

has order 8, i.e. it has

8 points

:

Points

Order

∞ 1 (3, 0) 2 (4, 4), (4, 1) 4 (0, 1), (0, 4), (1, 1), (1, 4) 8

Reminder:

E

\[

n

\] =

{ P ∈ E(K)

\|

nP = ∞}

Example

Which one are the elements of E

\[

4

\]

? In our case:

E

\[

4

\] =

{∞, (3, 0), (4, 4), (4, 1) }

Exercise

Which one are the elements of E

\[

2

\]

?

Note that

A = (4, 1)

generates

E

\[

4

\]

: 2 A = B = (3, 0), 3 A = C = (4, 4), 4 A = ∞

---

## Bilinear Pairing

A Bilinear pairing is a map of the form

e : G₁ × G₂ −→ G T

BUT what can

G₁, G₂

and

G T

be?

In our case:
- G₁

and

G₂

can be

E(F p)

or

E

\[

n

\]

- G T

can be

Z ∗ q

(simplification)

Example

Following the example of the previous slide, we can define the pairing:

e : E

\[

4

\]

× E

\[

4

\]

−→ Z ∗ 5 (A, A) −→ 2

Exercise

Which value will e

(A, 2 A)

take? And e

(3 B, C)

?

---

## Pairing properties

1 e(P, ∞) = e(∞, Q) = 1 2 e(− P, Q) = e(P, Q) − 1 = e(P, − Q) 3 e(a · P, Q) = e(P, Q) a = e(P, a · Q) 4 e(a · P, b · Q) = e(P, Q) a · b₅ e(P₁ + P₂, Q) = e(P₁, Q) · e(P₂, Q)

Example

Is e

(− P, 3 Q)

equal to e

(P, Q) − 3

?

Proof.

Yes, because

e(− P, 3 Q) (2) = e(P, 3 Q) − 1 (3) = e(P, Q) − 3

Exercise

Is e

(aP + bP, cP)

equal to e

(2 cP, P) a + b

?

---

## Homework 6

Exercise

Let E

(F 11)

be an elliptic curve of order

36 .

Which ones are the possible orders of its points? Why?

Which ones are the possible orders of the points of
E

\[

22

\]

? Why?

Exercise

Let E

2 : y₂ = x₃ + 2 x + 1

be an elliptic curve in

F₇ .

Apply Diffie-Hellmann protocol for a

= 2, b = 5

and P

= P₆ .

Exercise

Let S be a point in E

\[

12

\]

of order

12

and g

= 6

be a generator of

Z ∗ 13

If e

: E

\[

12

\]

× E

\[

12

\]

−→ Z ∗ 13

is a symmetric bilinear pairing, such that e

(S, S) = g.

Use the properties of the pairing and compute

e(4 S, 2 S) e(2 ∗ 4 S, ∞)

and e

(∞, S) e(2 S, − 2 S) . e(9 S − S, 3 S + S) ∗ e(3 S + 4 S, S) .

Exercise

Let e

: E

\[

p

\]

× E

\[

p

\]

−→ Z ∗ p

be a symmetric bilinear pairing and P

∈ E

\[

p

\]

.

is it true that e

(3 aP + bP, cP) = e(3 cP, P) a + b

?

---

Thank you for attention!

[ricci@vut.cz](mailto:ricci@vut.cz)

<https://axe.vut.cz/>
