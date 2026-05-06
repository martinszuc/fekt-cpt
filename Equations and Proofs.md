---
tags:
  - reference
  - equations
  - cheatsheet
aliases:
  - Equations
  - Formulas
  - Cheatsheet
  - eq
---

# 📐 Equations — Master Reference

> [!tip] How to use this
> This is a **pure reference file** — no exercises, no explanations. When you're mid-problem and need a formula fast, come here. For full explanations and worked examples, follow the links.

---

## ϕ(n) — Euler's Totient Function
→ Full notes: [[Euler's Totient Function (Phi)]]

| Case | Formula | When to use |
|---|---|---|
| n = p (prime) | `ϕ(p) = p - 1` | n is a prime number |
| n = p · q | `ϕ(pq) = (p-1)(q-1)` | n is product of two distinct primes |
| n = p^a | `ϕ(p^a) = (p-1) · p^(a-1)` | n is a prime power |
| General | `ϕ(n) = ∏ (pᵢ-1) · pᵢ^(aᵢ-1)` | Full factored form |

---

## GCD — Greatest Common Divisor
→ Full notes: [[Greatest Common Divisor (GCD)]]

```
Euclidean algorithm:
  a = q·b + r  →  replace a=b, b=r  →  repeat until r=0
  answer = last non-zero r
```

| Result | Meaning |
|---|---|
| gcd(a, n) = 1 | a ∈ Z\*_n → inverse exists |
| gcd(a, n) > 1 | a ∉ Z\*_n → no inverse |

**Shortcut — n = p (prime):** everything in {1, ..., p-1} is in Z\*_p

**Shortcut — n = p·q:** remove multiples of p and multiples of q

---

## Z\*_n — Multiplicative Group

| Property | Formula |
|---|---|
| Elements | all a where gcd(a, n) = 1 |
| Order (size) | ϕ(n) |
| Inverse of a | smallest b s.t. a·b ≡ 1 mod n |

---

## Orders
→ Full notes: [[Group Theory Fundamentals]]

```
Order of element a = smallest k s.t.  a^k ≡ 1 mod n
```

| Rule | Statement |
|---|---|
| Divisor rule | ord(a) always divides ord(group) = ϕ(n) |
| Only test | divisors of ϕ(n), smallest first |
| Generator | element with maximum order = ϕ(n) |
| # generators of Z\*_q | ϕ(ϕ(q)) |

---

## Generator Test
→ Full notes: [[Generators in Cryptography]]

```
g is a generator of Z*_n  ⟺
  g^(ϕ(n)/pᵢ) ≢ 1 mod n   for ALL prime divisors pᵢ of ϕ(n)
```

**Steps:**
1. Compute ϕ(n)
2. Find prime divisors of ϕ(n)
3. Test each — if any gives 1, g is NOT a generator

---

## Fast Exponentiation (Square-and-Multiply)
→ Full notes: [[Group Theory Fundamentals]]

```
To compute a^k mod n:
  1. Write k in binary
  2. Start with result = 1
  3. For each bit (left to right): square, then multiply if bit = 1
```

**Fermat's Little Theorem shortcut** (p prime, gcd(a,p) = 1):
```
a^(p-1) ≡ 1 mod p   →   reduce exponent mod (p-1) first
```

---

## Diffie-Hellman
→ Full notes: [[Diffie-Hellman Key Exchange]]

**Public parameters:** prime p, element g of order q in Z\*_p

```
Alice: A = g^a mod p          Bob: B = g^b mod p
Shared key: K = B^a mod p  =  A^b mod p  =  g^(ab) mod p
```

---

## ElGamal Encryption
→ Full notes: [[ElGamal Encryption]]

**Setup:** p prime, g generator, private x, public h = g^x mod p

```
Encrypt (with random k):
  c₁ = g^k mod p
  c₂ = m · h^k mod p

Decrypt:
  m = (c₁^x)⁻¹ · c₂ mod p
```

---

## RSA
→ Full notes: [[RSA Algorithm]]

**Setup:** n = p·q, ϕ(n) = (p-1)(q-1)

```
Public key:  (n, e)   where gcd(e, ϕ(n)) = 1
Private key: d        where d·e ≡ 1 mod ϕ(n)

Encrypt:  c = m^e mod n
Decrypt:  m = c^d mod n
```

> [!warning] Common mistake
> d is computed mod **ϕ(n)**, not mod n.

---

## DSA — Digital Signature Algorithm
→ Full notes: [[Digital Signature Algorithm (DSA)]]

**Setup:** q prime, p = q·z+1 prime, g of order q, private x, public y = g^x mod p

```
Sign (with random k):
  r = (g^k mod p) mod q
  s = k⁻¹ · (H(m) + x·r) mod q
  → Signature: (r, s)

Verify:
  w  = s⁻¹ mod q
  u₁ = H(m)·w mod q
  u₂ = r·w mod q
  → Check: r ≡ (g^u₁ · y^u₂ mod p) mod q
```

---

## Elliptic Curves — Basics
→ Full notes: [[Elliptic Curve Cryptography (ECC)]]

**Curve form:** `E(Fp): y² = x³ + a·x + b  (mod p)`

**Point on curve:** substitute (x,y) → check LHS = RHS mod p

**Inverse of point:** `-P = (xp, -yp mod p)`

---

## EC Point Addition: R = P + Q
→ Full notes: [[Elliptic Curve Cryptography (ECC)#Group Operations on the Curve]]

**Pick your case first:**

| Case | Condition | λ |
|---|---|---|
| Addition | xp ≠ xq | `(yq - yp) · (xq - xp)⁻¹ mod p` |
| Doubling | P = Q, yp ≠ 0 | `(3·xp² + a) · (2·yp)⁻¹ mod p` |
| Result = ∞ | P = Q and yp = 0 | — |
| Result = ∞ | xp = xq but P ≠ Q | — |

**Then always:**
```
xr = λ² - xp - xq  mod p      (use 2·xp for doubling)
yr = λ·(xp - xr) - yp  mod p
```

---

## EC — Finding All Points

```
1. Build squares table: y² mod p for y = 0 … p-1
2. For each x: compute RHS = x³ + ax + b mod p
3. RHS in squares table → 2 points (x, ±y)
   RHS = 0             → 1 point  (x, 0)
   RHS not a square    → 0 points
4. Add 1 for ∞
```

---

## EC — Order of a Point

```
Order of P = smallest k s.t.  k·P = ∞
```

| Rule | Statement |
|---|---|
| Divisor rule | ord(P) divides ord(E(Fp)) |
| Only test | divisors of |E(Fp)|, smallest first |
| Generator | point with order = |E(Fp)| |
