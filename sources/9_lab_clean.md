> Cleaned from Stirling PDF export. Original: 9_lab.md

---

## **Practical Lecture 9 -**

**Advanced Signature Schemes**

CPT - Cryptologic Protocol Theory

Dr. Sara Ricci

Brno University of Technology

[ricci@vut.cz](mailto:ricci@vut.cz)

---

## Table of contents

Blind Signature

Randomizable Signature

---

## Blind RSA signature

User

U

Signer

S n = pq sk ∈ R Z ∗ ϕ(n) pk ≡ sk − 1 mod ϕ(n)

Publish

n, pk m ∈ Z n r ∈ R Z n : gcd(n, r) = 1 m ′ = mr pk mod n m ′

−−−−−−−−−−−−−−−−−−−→

s ′ = m ′ sk mod n s ′

←−−−−−−−−−−−−−−−−−−

s = s ′ r − 1 mod n

Verification:

m

?

≡ s pk

---

## Example: Blind RSA signature

User

U

Signer

S n = pq = 5 ∗ 7 = 35 sk = 5 ∈ R Z ∗ 24 pk ≡ sk − 1 = 5 mod 24

publish

n = 35, pk = 5 m = 2 ∈ Z 35 r = 3 ∈ R Z 35 : gcd(n, r) = 1 m ′ = mr pk = 2 ∗ 3 5 = 31 mod 35 m ′ = 31 −

−−−−−−−−−−−−−−−−−−−−−−

s ′ = m ′ sk = 31 5 = 26 mod 35 s ′ = 26

←−−−−−−−−−−−−−−−−−−−−−−

s = s ′ r − 1 = 26 ∗ 3 − 1 = 26 ∗ 12 = 32 mod 35

Verification:

2 = m

?

≡ s pk = 32 5 = 2 mod 35

---

## Camenisch-Lysyanskaya signature (simplified)

Signer

Receiver

p, q

primes

, n = pq A, B, C ∈ R Z ∗ n m

message

e, s ∈ R Z ϕ(n)

compute

v : v e ≡ A m B s C mod n

Signature

σ = (v, e, s) r ∈ R Z ∗ ϕ(n) v ′ = vB r mod n s ′ = s + er mod ϕ(n)

Randomized Signature:

σ ′ = (v ′, e, s ′) m, σ ′ = (v ′, e, s ′)

−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−→

v ′ e

?

≡ A m B s ′ C mod n

---

## Example: CL signature (simplified)

Signer

Receiver

p = 3, q = 7, n = 21 A = 2, B = 4, C = 5 ∈ R Z ∗ 21 m = 5 ∈ Z ∗ 12

message

e = 5, s = 2 ∈ R Z 12 v = 10

such that

19 = 10 5 = v e = A m B s C = 2 5 4 2 5 = 11 ∗ 16 ∗ 5 = 19

Signature

σ = (v, e, s) = (10, 5, 2) r = 5 ∈ R Z ∗ 12 v ′ = vB r = 10 ∗ 4 5 = 10 ∗ 16 = 13 mod 21 s ′ = s + er = 2 + 5 ∗ 5 = 3 mod 12

Randomized Signature:

σ ′ = (v ′, e, s ′) = (13, 5, 3) m, σ ′ = (v ′, e, s ′) = (13, 5, 3)

−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−→

13 = 13 5 = v ′ e

?

≡ A m B s ′ C = 2 5 4 3 5 = 11 ∗ 1 ∗ 5 = 13 mod 21

---

## Homework 9

Exercise

Compute the CL signature for m

= 17

with parameters A

= 3, B = 5, C = 7, n = 77 .

---

Thank you for attention!

[ricci@vut.cz](mailto:ricci@vut.cz)

<https://axe.vut.cz/>
