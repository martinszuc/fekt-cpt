---
tags: [cryptography, cpt, reference, exam-topic]
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

---

## Bilinear Pairing Properties
→ Full notes: [[Day 4 - Pairings]]

`e : G₁ × G₂ → Gᴛ`  Symmetric if G₁ = G₂.

| # | Property | Formula |
|---|---|---|
| 1 | Identity | `e(P, ∞) = e(∞, Q) = 1` |
| 2 | Inverse | `e(-P, Q) = e(P, Q)⁻¹ = e(P, -Q)` |
| 3 | Scalar | `e(aP, Q) = e(P, Q)ᵃ = e(P, aQ)` |
| 4 | Bilinear | `e(aP, bQ) = e(P, Q)^(ab)` |
| 5 | Additive | `e(P₁+P₂, Q) = e(P₁,Q)·e(P₂,Q)` |
| 6 | Non-degeneracy | `e(P, Q) ≠ 1` for some P, Q — usually `e(g₁, g₂) ≠ 1` |

> [!tip] Most important for exams: Bilinearity (property 4)

---

## MOV Attack
→ Full notes: [[Day 4 - Pairings]]

**Known:** `e(P, P) = g`, `e(P, kP) = x`

**Find k:** compute `g¹, g², g³, …` in Gᴛ until finding `x`. Then `k` is the matching exponent.

Uses: `e(P, kP) = e(P, P)^k = g^k`

---

## Short Boneh-Boyen (SBB) Signature
→ Full notes: [[Day 4 - Pairings]]

**Setup:** `e: G₁×G₂→Gᴛ`, `P ∈ G₁`, `R ∈ G₂`, `sk=a`, `pk=aR`

```
Sign:    S = (a + m)⁻¹ · P          (inverse is mod group order q)
Verify:  e(m·S, R) · e(S, pk) = e(P, R)
```

---

## Pedersen Commitment
→ Full notes: [[Day 5 - Commitments]]

**Parameters:** prime `p`, generators `g₁, g₂` of `Z*_p`, message `w`, randomness `o`

```
Commit:  c = g₁^w · g₂^o mod p
Open:    reveal (w, o); verifier recomputes
```

| Property | Strength | Why |
|---|---|---|
| Hiding | Perfect | linear equation in (w,o) has ∞ solutions |
| Binding | Computational | finding 2 openings ≡ solving DLP |

---

## ElGamal Commitment
→ Full notes: [[Day 5 - Commitments]]

```
c = (c₁, c₂) = (g₁^o, g₁^w · g₂^o) mod p
Open: reveal (w, o), verify pair
```

---

## Schnorr Protocol
→ Full notes: [[Day 7 - Sigma Protocols]]

**Public:** `h = g^w mod p`.  **Private:** `w`.

```
Prover: r ∈_R Zq \ {0};  c = g^r mod p   →  send c
Verifier: send e ∈_R Zq \ {0}
Prover: z = (ew + r) mod q              →  send z
Verifier: check  g^z ≡ h^e · c  mod p
```

> z is computed mod q (subgroup order), NOT mod p

---

## Schnorr AND-Protocol
→ Full notes: [[Day 7 - Sigma Protocols]]

Proves knowledge of both `w₁` and `w₂` (where `h₁=g₁^w₁`, `h₂=g₂^w₂`).

```
Prover sends: c₁=g₁^r₁, c₂=g₂^r₂
Shared challenge: e
Responses: z₁=(ew₁+r₁) mod q,  z₂=(ew₂+r₂) mod q
Verify: g₁^z₁ ≡ h₁^e·c₁  AND  g₂^z₂ ≡ h₂^e·c₂  mod p
Combined: g₁^z₁ · g₂^z₂ ≡ h^e · c  mod p
```

---

## Schnorr OR-Protocol
→ Full notes: [[Day 7 - Sigma Protocols]]

Proves knowledge of one of `w₁`, `w₂` without revealing which.

```
Prover picks z₂,e₂,r₁; computes c₁=g^r₁, c₂=g^z₂·h₂^(-e₂)
Challenge e split: e₁ = e - e₂ mod q
Response: z₁ = (e₁·w₁ + r₁) mod q
Verifier checks: e₁+e₂ ≡ e;  g^z₁≡h₁^e₁·c₁;  g^z₂≡h₂^e₂·c₂
```

---

## CL Signature (IDEMIX)
→ Full notes: [[Day 8 - Signatures]]

**Setup:** `n=pq`, random `A,B,C ∈ Z*_n`

```
Sign:       find v s.t.  vᵉ ≡ Aᵐ·Bˢ·C  mod n    → σ=(v,e,s)
Verify:     vᵉ ≡ Aᵐ·Bˢ·C  mod n
Randomize:  v'=v·Bʳ mod n;  s'=s+e·r mod φ(n)  → σ'=(v',e,s')
Verify σ':  v'ᵉ ≡ Aᵐ·Bˢ'·C  mod n
```

> s' uses φ(n) not n

---

## Blind RSA Signature
→ Full notes: [[Day 8 - Signatures]]

**Setup:** RSA `(n, pk, sk)`.

```
Blind:    m' = m · r^pk  mod n      (user, r random)
Sign:     s' = m'^sk     mod n      (signer)
Unblind:  s  = s' · r⁻¹ mod n      (user)
Verify:   m  ≡ s^pk      mod n
```

---

## Algebraic MAC
→ Full notes: [[Day 9 - Algebraic MAC]]

**Setup:** EC group `G`, generator `g` of order `q`, `sk=(x₀,x₁,…,xₖ)`

```
α = x₀ + Σ mᵢxᵢ  mod q
σ = α⁻¹ · g                        (EC scalar multiplication)

Randomize: h = r·g,  σ̂ = r·σ
Verify:    α · σ̂  =  h              (EC scalar multiplication)
```

> All operations are EC scalar multiplication — not modular exponentiation

---

## ECDH — Elliptic Curve Diffie-Hellman
→ Full notes: [[Elliptic Curve Cryptography (ECC)]]

**Public parameters:** curve $E$, base point $G$ of order $q$

```
Alice: A = a·G          Bob: B = b·G
Shared key: K = a·B = b·A = (ab)·G
```

---

## ECDSA — Elliptic Curve Digital Signature Algorithm
→ Full notes: [[Elliptic Curve Cryptography (ECC)]]

**Setup:** curve $E$, base point $G$ of order $q$, private key $d$, public key $Q = d \cdot G$

```
Sign (message m, random k ∈ Zq \ {0}):
  R = k·G = (x_R, y_R)
  r = x_R mod q
  s = k⁻¹ · (H(m) + d·r) mod q
  → Signature: (r, s)

Verify:
  w  = s⁻¹ mod q
  u₁ = H(m)·w mod q
  u₂ = r·w mod q
  X  = u₁·G + u₂·Q
  → Check: x_X mod q == r
```

---

## Euler's Theorem (general)

```
If gcd(a, n) = 1, then  a^ϕ(n) ≡ 1 mod n
```

Special case (Fermat's Little Theorem, p prime): `a^(p-1) ≡ 1 mod p`

**Use:** reduce large exponents — replace `a^k` with `a^(k mod ϕ(n)) mod n`

---

## Extended Euclidean Algorithm — Modular Inverse

```
Finds x, y such that:  ax + ny = gcd(a, n)

If gcd(a, n) = 1  →  x ≡ a⁻¹ mod n
```

**Quick check:** the inverse of $a$ mod $n$ exists **iff** $\gcd(a, n) = 1$.

---

## Chinese Remainder Theorem (CRT)

If $n = p \cdot q$ with $p, q$ distinct primes and

```
x ≡ a  mod p
x ≡ b  mod q
```

then there is a **unique** solution $x \bmod n$.

**RSA use:** compute $m = c^d \bmod n$ faster by working mod $p$ and mod $q$ separately, then combining with CRT.

---

## EC Curve — Non-Singularity Condition

```
Δ = -16(4a³ + 27b²) ≢ 0  mod p
```

If $\Delta = 0$, the curve has a singular point (cusp or self-intersection) and is **not** an elliptic curve.

---

## EC — Hasse Bound (Group Order Estimate)

```
| #E(Fp) - (p + 1) | ≤ 2√p
```

The number of points on $E(\mathbb{F}_p)$ is always close to $p + 1$. Useful for sanity-checking a computed group order.
