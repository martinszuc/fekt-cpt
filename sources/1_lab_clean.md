> Cleaned from Stirling PDF export. Original: 1_lab.md

---

## **Practical Lecture -**

**Cryptography Review**

CPT - Cryptologic Protocol Theory

Dr. Sara Ricci

Brno University of Technology

[ricci@vut.cz](mailto:ricci@vut.cz)

---

## Table of contents

Euler Fuction

Prove by induction

Groups

Generator of a Group

Diffie-Hellman Protocol

DSA Algorithm

RSA Algorithm

---

## Euler Function

ϕ(n)

Definition (Euler function)

If n

= p a₁ 1 ∗ p a₂ 2 ∗ · · · ∗ p a k k

then

ϕ(n) = (p₁ − 1) p a₁ − 1 1 (p₂ − 1) p a₂ − 1 2 . . . (p k − 1) p a k − 1 k

Example

ϕ(19) = 19 − 1 = 18 ϕ(45) = ϕ(3 2 ∗ 5) = 2 ∗ 3 ∗ 4 = 24

---

## Prove by induction

Definition (Induction)

A statement P

(n)

holds for all n

≥ n ′

if it is true for:

(base step) P

(k)

is true for the starting value k

= n ′

, usually k

= 0

or

k = 1 (P(k) ⇒ P(k + 1)

) That is, given that P

(k)

is true, P

(k + 1)

is also true

Example

Show that

3

\|

n₃ −

n for all n

≥ 2

(base step) We want to prove that for k

= 2

is true.

3

\|

2 3 − 2 = 6 (P(k) ⇒ P(k + 1)) 3

\|

k₃ −

k is true. We want to show that

3

\|

(k + 1) 3 − (k + 1)

is true. we resolve the eq.

(k + 1) 3 − (k + 1) = k₃ + 1 + 3 k₂ + 3 k − k − 1 = (k₃ − k)+(1 − 1)+ 3 (k₂ + k)

Note that

3

\|

k₃ −

k by hypothesis,

1 − 1 = 0

and

3

\|

3 (k₂ + k)

by

definition. Since

3

divides any component of the formula,

3

\|

(k + 1) 3 − (k + 1) .

---

## Additive Group:

Z n n

can be prime (p) or composite (p\*q).

Examples

Z₃, Z₈

and

Z 35 .

its elements are

**classes**

of numbers!

Z₆

has elements

\[

0

\]

6,

\[

1

\]

6,

\[

2

\]

6,

\[

3

\]

6,

\[

4

\]

6,

\[

5

\]

6

**Additive group**

, i.e. the operation is "+".

\[

3

\]

6

+ \[

1

\]

6

= \[

4

\]

6

and

\[

3

\]

6

+ \[

5

\]

6

= \[

2

\]

6

**identity**

is "0",

e.g.

\[

0

\]

6

+ \[

a

\]

6

= \[

a

\]

6

+ \[

0

\]

6

= \[

a

\]

6

easier notation: 0

+ a ≡ a + 0 ≡ a mod n

**opposite**

of an element

a

is

− a a + (− a) ≡ 0 mod n

, for example, 3

+ (− 3) ≡ 0 mod 11

---

## Multiplicative Group:

Z ∗ n n

can be prime (p) or composite (p\*q).

Examples

Z ∗ 3, Z ∗ 8

and

Z ∗ 35 .

its elements are

**classes**

of numbers!

Z ∗ 6

has elements

\[

1

\]

6,

\[

5

\]

6 Z ∗ 7

has elements

\[

1

\]

7,

\[

2

\]

7,

\[

3

\]

7,

\[

4

\]

7,

\[

5

\]

7,

\[

6

\]

7

**Multiplicative group**

, i.e. "\*" is the operation.

2 ∗ 3 ≡ 6 ≡ (− 1) mod 7

**identity**

is "1",

e.g. 1 ∗ a ≡ a ∗ 1 ≡ a mod n

**inverse**

of an element

a

is en element

b

such that

a ∗ b ≡ b ∗ a ≡ 1 mod n₂ ∗ 2 ≡ 1 mod

3, for example, 3

∗ 2 ≡ 1 mod 5

Note

Why did

Z ∗ 6

just have two classes?

The elements of

Z ∗ n

are the elements a

∈ Z n

which are coprime with n, that is

gcd(a, n) = 1

---

## Order of

Z ∗ n

Definition

The

**order**

of a multiplicative

**group**

Z ∗ n

is its number of elements. The order

can be easily computed using the Euler function

ϕ(n) .

Example

Z ∗ 6

has elements

\[

1

\]

6,

\[

5

\]

6

, therefore its order is

2 (= ϕ(6)) . Z ∗ 7

has elements

\[

1

\]

7,

\[

2

\]

7, ...,

\[

6

\]

7

, therefore its order is

6 (= ϕ(7)) .

Definition

The

**order**

of an

**element**

divides the order of the group.

---

## Order of

a ∈ Z ∗ n

Example

The order of

Z ∗ 13

is

12 .

It has elements: 1,2,3,4,5,6,7,8,9,10,11,12.
Possible els. orders are: 1,2,3,4,6 and 12 (divisors of

12).

Which one is the order of a=4?

Try all the

exponents

until we found a congruence equal to 1































4 1 ≡ 4 ̸≡ 1 mod 13 4 2 ≡ 3 ̸≡ 1 mod 13 4 3 ≡ 12 ̸≡ 1 mod 13 4 4 ≡ 9 ̸≡ 1 mod 13 4 5 ≡ 10 ̸≡ 1 mod 13 4 6 ≡ 1 mod 13

The order of a is 6.

---

## Generators of

Z ∗ n

Definition

A generator of a group G is an element of maximum order in G.

Exercise

How many generators does

Z ∗ 10

have?

Proof.

In

Z ∗ 10

, the possible els. orders are: 1,2,4.

Therefore, we search for elements of order 4.

Z ∗ 10

has elements

\[

1

\]

10,

\[

3

\]

10,

\[

7

\]

10,

\[

9

\]

10 . 1 1 ≡ 1 mod 10

3 2 ≡ 9 mod 10 3 4 ≡ 1 mod 10

7 2 ≡ 9 mod 10 7 4 ≡ 1 mod 10 9 2 ≡ 1 mod 10

Therefore, this group has 2 generators: 3 and 7.

---

## Find a generator of

Z ∗ n

Note

In case of

Z ∗ q

with

q prime

, the answer is easy:

ϕ(ϕ(q))

gives you the number

of generators.
For instance,

Z ∗ 11

has

ϕ(ϕ(11)) = ϕ(10) = 4

generators.

Algorithm (generators of

Z ∗ n)

choose a random element g in

Z ∗ n,

compute

ϕ(n)

find all prime divisors of

ϕ(n) = p a₁ 1 p a₂ 2 . . . p a k k,

for each prime divisor p

i

, compute

g ϕ(n) / p i

?

≡ 1 mod q

if g

ϕ(n) / p i ̸≡ 1 mod

q does NOT hold for all p

i -s,

then g is a generator.

---

## Example: find a generator of

Z ∗ 11

Example

Find a generator of

Z ∗ 11

(next step).

choose random element

g = 2

from

Z ∗ 11,

compute

ϕ(11) = 10,

find all prime divisors:

10 = 5 ∗ 2,

compute

2 10 / 2 ≡ 10 (mod 11),

compute

2 10 / 5 ≡ 4 (mod 11), 2 10 / p i ≡ 1 (mod n)

does not hold for all p

i

, thus

g = 2

is a generator

.

---

## Diffie-Hellman Protocol

**Alice**

**Bob**

System parameters:

p =

11 prime (

ϕ(11) = 10), g ∈ Z ∗ 11

of order

q = 5

a,b are of your choice

∈ Z₅ a = 3 ∈ R Z₅ b = 4 ∈ R Z₅ A = 4 3 ≡ 9 mod 11 B = 4 4 ≡ 3 mod 11 A = 9

−−−−−−−−−−−−−−−−−−−−−→

B = 3

←−−−−−−−−−−−−−−−−−−−−−

B a = 3 3 ≡ 5 mod 11 A b = 9 4 ≡ 5 mod 11 A b ≡ B a mod p

---

## Digital Signature Algorithm (DSA)

**Alice**

**Bob**

(Signer)

(Verifier)

System parameters:

q = 5

prime,

p = qz + 1 = 11

prime,

g = 4 ∈ Z ∗ 11

of order

q = 5,

**DSA setup**

x = 2 ∈ R Z ∗ 5 (pk, sk) = (y = 4 2, x = 2) = (5, 2) m, H(m) = 3

**DSA signing**

k = 3 ∈ R Z ∗ 5

where

3 ∗ 2 ≡ 1 mod 5, i.e. k − 1 = 2 r = (4 3 mod 11) mod 5 ≡ (9 mod 11) mod 5 ≡ 4 s = 2 (3 + 2 ∗ 4) ≡ 2 mod 5

Enc

(m), (r, s)

−−−−−−−−−−−−−−−−−−−−−−−−−−−−−→

**DSA verification**

w = s − 1 = 3 mod 5 u₁ = H(m) w = 4 mod 5 u₂ = rw = 2 mod 5 4

?

= (4 4 5 2 mod 11) mod 5

---

## RSA Algorithm (Rivest, Shamir, Adleman)

**Alice**

**Bob**

(Receiver)

(Sender)

**RSA setup**

n = 5 ∗ 7 = 35 m

message

ϕ(35) = 24 = 2 3 3 e = 5

?

5

\< ϕ

(35) = 24

such that

gcd (5, 24) = 1 d

\<

24

such that

5 d ≡ 1 mod 24

, that is

d = 5 (p = 5, q = 7, d = 5)

private

**Alice publishes: (**

n = 35 **,** e = 5 **)**

**RSA protocol**

m = 3 ∈ R Z 35 c ≡ 3 5 ≡ 33 mod 35 c = 33

←−−−−−−−−−−−−−−−−−−−−−−−−

c d ≡ m ed ≡ m mod n 33 5 ≡ 3 mod 35

---

## Homework 2/1

Exercise (Prove by induction)

Prove by induction that

4

\|

9 n + 3

for n

≥ 0 .

Exercise (Fermat's Primality Test)

Let n

= 15 .

Use Fermat's primality test to show either n is prime or n is composite.

Exercise (Moltiplicative group)

1

Write all the elements of

Z ∗ 14 2

Which order has

Z ∗ 14

?

3

Find the inverse of

5

and

6

in

Z ∗ 14

if exists.

4

compute

5 5 mod 14 . 5

find the order of

3

in

Z ∗ 14 .

Exercise (Find a generator)

Find one generator of

Z ∗ 13

with the algorithm explained in class.

---

## Homework 2/2

Exercise

**Diffie-Hellman.**

Alice and Bob use Diffie-Hellman protocol to create K

= A b ≡ B a mod 17

. In this protocol, q can be any divisor

of p

− 1 .

Compute the protocol for q

= 8 .

Exercise

**Brain Teaser 1.**

Suppose to have g

= 6 ∈ Z ∗ 17

. Which one is the order of g? Can you use g to find an element of order

8

?

Exercise

**Brain Teaser 2.**

in Exercise 1, Alice and Bob generate a key K .
Alice use a basic encryption c

=

Enc

K(m) = 2 ∗ m − 3 K mod 19

to send a message m to Bob.

1

Which operation Bob does for decrypting? Dec

K(c) = ... 2

Is this a symmetric cryptosystem? Justify your answer.

Exercise

**ElGamal.**

Compute ElGamal scheme with p

= 11

and m

= 3 .

---

Thank you for attention!

[ricci@vut.cz](mailto:ricci@vut.cz)

<https://axe.vut.cz/>
