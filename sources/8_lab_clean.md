> Cleaned from Stirling PDF export. Original: 8_lab.md

---

## **Practical Lecture 8 -**

Σ

**-Protocols**

CPT - Cryptologic Protocol Theory

Dr. Sara Ricci

Brno University of Technology

[ricci@vut.cz](mailto:ricci@vut.cz)

---

## Table of contents

Order of elements

Schnorr Protocol

EQ-Composition of Schnorr Protocol

OR-Composition of Schnorr Protocol

---

## Order of elements

Definition

The order of an element divides the order of the group.

Order of

Z ∗ 13

is

ϕ(13) = 12.

Possible els. orders are: 1,2,3,4,6 and 12 (divisors of

ϕ(13)).

A generator is an el. of max. order: 12 (in our case).

**1.**

Find a generator?

ϕ(13) = 2 2 ∗ 3.

I try with

g = 2.

2 ϕ(13) / 3 ≡ 2 4 ≡ 3 ̸≡ 1 mod 13 2 ϕ(13) / 2 ≡ 2 6 ≡ 12 ̸≡ 1 mod 13

2 is a generator.

**2.**

Find an el. of order 2.

In

Z ∗ 13, g =

2 is a generator, therefore

(2 6) 2 ≡ 1 mod

13 and 2

6 ≡ 12 mod

13 has order 2.

---

## Schnorr Protocol

**Prover (**

P **)**

**Verifier (**

V **)** p

prime,

q

\|

ϕ(p)

prime,

g

has order

q

in

Z ∗ p, h

public key of

P w

private key, i.e.

h = g w r ∈ R Z q

∖

{ 0 } c = g r mod p c −

−−−−−−−−−−−−−−−−−−−

e ∈ R Z q

∖

{ 0 } e

−−−−−−−−−−−−−−−−−−−

− z = (ew + r) mod q z −

−−−−−−−−−−−−−−−−−−−

g z

?

≡ h e c mod p

---

## Example: Schnorr Protocol

**Prover (**

P **)**

**Verifier (**

V **)** p =

23 prime,

q =

11 prime,

g =

9 has order 11 in

Z 23, h

public key of

P w = 4 ∈ Z 11

∖

{ 0 }, h = 9 4 ≡ 6 mod 23 r = 2 ∈ R Z 11

∖

{ 0 } c = 9 2 ≡ 12 mod 23 c = 12

−−−−−−−−−−−−−−−−−−−−−−−−→

e = 3 ∈ R Z 11

∖

{ 0 } e

−−−−−−−−−−−−−−−−−−−

− z = (3 ∗ 4 + 2) ≡ 3 mod 11 z −

−−−−−−−−−−−−−−−−−−−

9 3 ≡ 16 mod 23

?

≡ 6 3 ∗ 12 ≡ 9 ∗ 12 ≡ 16 mod 23

---

## AND-Composition of Schnorr Protocol

**Prover (**

P **)**

**Verifier (**

V **)** p

prime,

q

\|

ϕ(p)

prime,

g₁, g₂

has order

q

in

Z ∗ p, h₁, h₂

public keys of

P(h₁ = g w₁, h₂ = g w₂) r ∈ R Z q

∖

{ 0 } c₁ = g r₁ mod p c₂ = g r₂ mod p c₁, c₂ −

−−−−−−−−−−−−−−−−−−−−−−−−

e ∈ R Z q

∖

{ 0 } e

←−−−−−−−−−−−−−−−−−−−−−−−−−

z = (ew + r) mod q z

−−−−−−−−−−−−−−−−−−−−−→

g z₁

?

≡ h e₁ c₁ mod p g z₂

?

≡ h e₂ c₂ mod p

HW. Try to compute And-Schnorr for p=11 and q=5.

---

## OR-Composition of Schnorr Protocol

**Prover (**

P **)**

**Verifier (**

V **)** p

prime,

q

\|

ϕ(p)

prime,

g

has order

q

in

Z ∗ p, h₁, h₂

public keys of

P(h₁ = g w₁ ∨ h₂ = g w₂) z₂, e₂, r₁ ∈ R Z q

∖

{ 0 } c₁ = g r₁ mod p c₂ = g z₂ h − e₂ 2 mod p c₁, c₂ −

−−−−−−−−−−−−−−−−−−−−−−−−

e ∈ R Z q

∖

{ 0 } e

←−−−−−−−−−−−−−−−−−−−−−−−−−

e₁ = e − e₂ mod q z₁ = (e₁ w₁ + r₁) mod q e₁, e₂, z₁, z₂

−−−−−−−−−−−−−−−−−−−−−−−−−−→

e₁ + e₂

?

≡ e mod q g z₁

?

≡ h e₁ 1 c₁ mod p, g z₂

?

≡ h e₂ 2 c₂ mod p

---

## Example: OR-Schnorr Protocol

**Prover (**

P **)**

**Verifier (**

V **)**

23 prime, 11

\|

ϕ(23)

prime,

g =

9 has order

q =

11 in

Z ∗ 23, h₁, h₂

public keys of

P(w₁ = 2, h₁ = g w₁ = 9 2 = 12 ∨ h₂ = g w₂ = 2) z₂ = 3, e₂ = 4, r₁ = 5 ∈ R Z q

∖

{ 0 } c₁ = g r₁ mod p ≡ 9 5 ≡ 8 mod 23 c₂ = g z₂ h − e₂ 2 mod p ≡ 9 3 2 − 4 ≡ 16 ∗ 13 ≡ 1 mod 23 c₁, c₂ −

−−−−−−−−−−−−−−−−−−−−−−−−

e = 6 ∈ R Z 11

∖

{ 0 } e

←−−−−−−−−−−−−−−−−−−−−−−−−−

e₁ = e − e₂ mod q = 6 − 4 = 2 mod 11 z₁ = e₁ w₁ + r₁ mod q = 2 ∗ 2 + 5 = 9 mod 11 e₁, e₂, z₁, z₂

−−−−−−−−−−−−−−−−−−−−−−−−−−→

e₁ + e₂ = 2 + 4 = 6

?

≡ e mod q mod 11 2 ≡ 9 9 ≡ g z₁

?

≡ h e₁ 1 c₁ mod p ≡ 12 2 ∗ 8 ≡ 2 mod 23 16 ≡ 9 3 ≡ g z₂

?

≡ h e₂ 2 c₂ mod p ≡ 2 4 ∗ 1 ≡ 16 mod 23

---

## Homework 8

Exercise

**Schnorr protocol**

in

Z p

. Let t

= 5

be a generator of

Z ∗ 23 (p = 23

prime).

Choose (wisely) the rest of parameters and apply the protocol.

If a cheating Verifier

V

sends e

= 0

. Can

V

obtain something? If yes, what? If not, why?

Exercise

**Another Sigma Protocol**

How is the checking equation of

V

in this case?

That is, what would you put in the place of the question mark in the protocol above?
Help: g

?

1 g

?

2

=?

---

Thank you for attention!

[ricci@vut.cz](mailto:ricci@vut.cz)

<https://axe.vut.cz/>
