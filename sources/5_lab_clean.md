> Cleaned from Stirling PDF export. Original: 5_lab.md

---

## **Practical Lecture 5 -**

**Commitment Schemes**

CPT - Cryptologic Protocol Theory

Dr. Sara Ricci

Brno University of Technology

[ricci@vut.cz](mailto:ricci@vut.cz)

---

## Table of contents

Pedersen Commitment (Simplified)

Public Key Encryption as Commitment

---

## Commitments: Basic Properties

Commitment

A commitment scheme allows a sender to

**commit**

to a value

w

while

keeping it hidden until it is revealed.

c =

commit

(w, o)

where

o

is random

opening information

.

Security Properties

Hiding - protect the Sender

Given

c =

commit

(w, o)

, it should be

**hard to learn**

w .

Binding - protect the Receiver

It should be

**hard to open it in two different ways**

:

commit

(w, o) =

commit

(w ′, o ′)

---

## Strength of Security Properties

The hiding and binding properties can hold with different strengths.

Perfect security

: the property cannot be broken by any kind of machine

or algorithm, including

infinitely powerful

adversaries.

Statistical security

: breaking the property is possible only with

negligible

probability

, even for an infinitely powerful adversary.

Computational security

: breaking the property is infeasible for

polynomial-time

adversaries.

Note

Most cryptographic commitments are:

computationally binding

statistically or perfectly hiding

---

## Pedersen Commitment (Simplified)

**Sender**

**Receiver**

11 prime,

g₁ = 2, g₂ =

6 generators of

Z ∗ 11 w = 3 ∈ R Z 10

∖

{ 0 } o = 2 ∈ R Z 10

∖

{ 0 } c = g w₁ g o₂ = 2 3 6 2 = 8 ∗ 3 = 2 mod 11 c = 2

−−−−−−−−−−−−−−−−−−−−−−−→

- - - - - - - - - - - - - - - - - - - - - - - - - - -

w = 3, o = 2 −

−−−−−−−−−−−−−−−−−−−−−−−−−−−

3 = c

?

= g w₁ g o₂ = 2 3 6 2 = 8 ∗ 3 = 2 mod 11

---

## Pedersen Commitment: Hiding

Fact

For a linear equation in the form

ax +

by

= c

, where

a, b, c

are constants are

constants and

a, b ̸ =

0. There are infinitely many pairs

(x, y)

that satisfy the

equation.

Scheme

c = g w₁ g o₂ mod p

It is perfectly hiding.

Since

g₁

is a generator, there exists

a : g₂ = g a₁

and also

c = g b₁

for some

b .

Then

c = g w₁ g o₂ = g w₁ (g a₁) o = g w + ao 1 mod p

so checking the exponents

w + ao ≡ b(mod p − 1)

This is a linear equation in two unkowns, there are many pairs

(o, w)

that

satisfy the equation. Thi implies that

c

does not reveal

w .

---

## Perfectly Hiding Example

Exercise

Using the same parameters

p = 11, g₁ = 2, g₂ =

6. Show that the same

commitment

c =

2 can correspond to different pairs

(w, o) .

Solution

We need 6

= g₂ = g a₁ ≡ 2 9 mod

11 (brute-force).

Also 2

= c = g b = 2 1 mod 11.

Therefore, 2

w₆ o =

2 becomes 2

w(2 9) o = 2 1

and

w + 9 o ≡ 1 mod 10

This equation has many solutions.
Examples:

(w, o) = (3, 2), (2, 1), (1, 0)

We commit to

w =

3 with randomness

o = 2. c = g w₁ g o₂ = 2 3 · 6 2 = 8 · 3 = 24 ≡ 2 mod 11

---

## Pedersen Commitment: Binding

It is computationally binding

Suppose we find two different openings

(w, o) ̸ = (w ′, o ′)

such that

g w₁ g o₂ = g w ′ 1 g o ′ 2 mod p .

Then

g w − w ′ 1 = g o ′ − o₂ mod p .

Since

g₂ = g a₁

, we have

g w − w ′ 1 = g a(o ′ − o) 1,

and

w − w ′ ≡ a(o ′ − o) (mod p − 1) .

If

o ̸ = o ′

, we can compute

a ≡ (w − w ′)(o ′ − o) − 1 (mod p − 1),

that is, we need to recover the discrete logarithm of

g₂

in base

g₁ .

Therefore, finding two different openings would solve a DLP. Hence Pedersen
commitment is

computationally binding

.

---

## Computationally Binding Example

Exercise

Using the same parameters

p = 11, g₁ = 2, g₂ =

6, we found two

openings of the same commitment

c = 2: (3, 2)

and

(2, 1)

. Which

assumption did we use?

Solution

To find different openings, we solved the DLP

mod

11 and found

6 = g₂ = g a₁ ≡ 2 9 mod 11

and found

a = 9

Therefore,

c = g w₁ g o₂ = 2 w + 9 o

Therefore different pairs

(w, o)

satisfying

w + 9 o ≡ 1 (mod 10)

produce the same commitment.
So computing

a

requires solving the discrete logarithm problem and

Pedersen commitment is

computationally binding

.

---

## Public Key Encryption as Commitment

Any asymmetric encryption scheme can be transformed into a commitment scheme.

Example (ElGamal)

Alice has key

(x, h = g x)

and broadcasts h

Bob sends c

= (c₁, c₂) = (g k, m ∗ h k)

to Alice, where

k ∈ R Z ∗ n

Alice

decrypts

m = (c x₁) − 1 c₂ = m

becomes:

**Sender**

**Receiver**

g₁, g₂

generators of

Z ∗ n w ∈ Z ϕ(n)

∖

{ 0 } o ∈ R Z ϕ(n)

∖

{ 0 } c = (c₁, c₂) = (g o₁, g w₁ g₂ o) mod p c − −−−−−

Store

c(w, o) −−−−−−−−−→

Verify

: c

?

= (g o₁, g w₁ g o₂) mod p

---

## EC ElGamal Scheme

**Sender**

**Receiver**

P, Q

points of E(

F p) a, b ∈ Z ∗ p c = (c₁, c₂) = (aP, bP + E aQ) c − −−−−−

Store

c(a, b) −−−−−−−−−→

Verify:

c

?

= (aP, bP + E aQ) mod p

---

## Homework 5

Exercise

**ElGamal Commitment.**

Consider the ElGamal commitment scheme with p

= 23, g₁ = 5, g₂ = 7

generators of

Z ∗ 23

. Let w

= 3

and o

= 4 .

compute the commitment c

= (c₁, c₂)

;

show that the opening

(w, o) = (3, 4)

is valid;

explain why, in this example, the scheme is perfectly binding.

Exercise

**EC ElGamal Commitment.**

Any asymmetric scheme can be transformed into a commitment scheme.

tranform EC ElGamal scheme (Slide 11) in a commitment scheme.

is it computational or perfectly hiding?

is it computational or perfectly binding?

which hard problem is EC ElGamal referred to? Why? (EC Discrete logarithm problem or EC Integer
factorization)

---

Thank you for attention!

[ricci@vut.cz](mailto:ricci@vut.cz)

<https://axe.vut.cz/>
