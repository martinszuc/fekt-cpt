---
tags: [cryptography, cpt, moc]
aliases:
  - Start Here
  - Index
---

> [!danger] EXAM INTEL (from classmates)
> **Confirmed this year:** Order of EC · Algebraic MAC · CL signature · Pedersen commitment
> **Also likely:** MOV attack · Schnorr AND protocol · Blind RSA · PK proof of knowledge notation
> **Format:** ~40 min · calculator · short computation tasks · parameters recycled from labs
> **His favourites:** Schnorr, blind RSA, CL signature, MOV attack, Pedersen hiding/binding

# 🔐 Cryptography — Map of Content

> [!tip] How to use this vault
> Start each study session here. Every topic links out to its own note. Use **Graph View** (Ctrl/Cmd+G) to see how concepts connect. For formulas only, go straight to [[Equations and Proofs]].

---

## 📚 Course Days

| Day | Topics | Status |
|---|---|---|
| [[Day 1 - Groups, Phi & Generators]] | ϕ(n), Z\*_n, Orders, Generators, Fast Exponentiation | ✅ |
| [[Day 2 - DH, ElGamal, RSA & DSA]] | Diffie-Hellman, ElGamal, RSA, DSA | ✅ |
| [[Day 3 - Elliptic Curves]] | EC arithmetic, Point Addition, Orders | ✅ |
| [[Day 4 - Pairings]] | Bilinear Pairings, MOV Attack, Boneh-Boyen Signature | ✅ |
| [[Day 5 - Commitments]] | Pedersen Commitment, ElGamal Commitment, Hiding/Binding | ✅ |
| [[Day 6 - Zero Knowledge]] | Graph Isomorphism, Permutations, ZK Protocol | ✅ |
| [[Day 7 - Sigma Protocols]] | Schnorr, AND-Composition, OR-Composition | ✅ |
| [[Day 8 - Signatures]] | Blind RSA, CL Signature, IDEMIX Randomization | ✅ |
| [[Day 9 - Algebraic MAC]] | Algebraic MAC, Randomization, vs SBB Signature | ✅ |

---

## 🧮 Mathematical Foundations

- [[Greatest Common Divisor (GCD)]] — Euclidean Algorithm, coprimality, Z\*_n membership
- [[Group Theory Fundamentals]] — Group axioms, cyclic groups, element orders
- [[Euler's Totient Function (Phi)]] — ϕ(n) formulas, prime powers
- [[Generators in Cryptography]] — Primitive roots, generator test

## 🔑 Public Key Cryptography

- [[Diffie-Hellman Key Exchange]] — Shared secret, DLP security
- [[ElGamal Encryption]] — Randomised encryption, ephemeral key
- [[RSA Algorithm]] — Key generation, modular exponentiation
- [[Digital Signature Algorithm (DSA)]] — Signing, verification

## 📐 Advanced Topics

- [[Elliptic Curve Cryptography (ECC)]] — Curve groups, point addition, ECDLP
- [[Day 4 - Pairings]] — Bilinear maps, MOV attack, SBB signature
- [[Day 5 - Commitments]] — Pedersen, ElGamal, EC ElGamal commitment
- [[Day 6 - Zero Knowledge]] — Graph isomorphism ZK protocol
- [[Day 7 - Sigma Protocols]] — Schnorr AND/OR compositions
- [[Day 8 - Signatures]] — Blind RSA, CL signature (IDEMIX)
- [[Day 9 - Algebraic MAC]] — Algebraic MAC, unlinkable randomization

## 📋 Reference

- [[Equations and Proofs]] — All formulas, Days 1–9, quick lookup

---

## 🔗 Key Concept Map

```
ϕ(n) ──→ Z*_n ──→ Orders ──→ Generators
                                  │
              ┌───────────────────┘
              ↓
    DH ──→ ElGamal
    RSA (uses ϕ(n) directly)
    DSA (uses DH + hashing)
              │
              ↓
    Elliptic Curves (same ideas, different group)
              │
              ↓
    Pairings ──→ MOV Attack
             └──→ Boneh-Boyen Signature
             └──→ Algebraic MAC
              │
    Commitments (Pedersen, ElGamal)
    Zero-Knowledge (Graph Isomorphism)
    Sigma Protocols (Schnorr AND/OR)
    CL Signature / IDEMIX
```

---

## 📝 Exam Cheat Sheet

### Must-know formulas

| Formula | Use |
|---|---|
| `ϕ(p) = p-1` | Prime |
| `ϕ(pq) = (p-1)(q-1)` | Two distinct primes |
| `a·b ≡ 1 mod n` | Modular inverse |
| `K = g^(ab) mod p` | DH shared key |
| `c = m^e mod n` | RSA encrypt |
| `m = c^d mod n` | RSA decrypt |
| `λ = (yq-yp)·(xq-xp)⁻¹` | EC point addition |
| `c = g₁^w·g₂^o mod p` | Pedersen commitment |
| `z = (ew + r) mod q` | Schnorr response |
| `vᵉ ≡ Aᵐ·Bˢ·C mod n` | CL signature |
| `σ = α⁻¹·g` (EC) | Algebraic MAC |

### Common mistakes

> [!warning] Watch out for these
> - `-y mod p` is **NOT** negative — add p: `-3 mod 7 = 4`
> - Division in modular arithmetic = **multiply by inverse**
> - RSA: `d·e ≡ 1 mod ϕ(n)`, NOT mod n
> - EC: check which **case** applies before computing λ
> - Schnorr: `z = (ew+r) mod q`, NOT mod p
> - CL signature: `s'` uses `mod ϕ(n)`, not mod n
> - Algebraic MAC: `α⁻¹` is a scalar inverse mod q, not an EC point inverse
