---
tags: [cryptography, cpt, moc]
aliases:
  - Start Here
  - Index
---

# 🔐 Cryptography — Map of Content

> [!tip] How to use this vault
> Start each study session here. Every topic links out to its own note. Use **Graph View** (Ctrl/Cmd+G) to see how concepts connect.

---

## 📚 Course Days

| Note | Topics | Status |
|---|---|---|
| [[Day 1 - Groups, Phi & Generators]] | ϕ(n), Z\*_n, Orders, Generators, Fast Exponentiation | ✅ |
| [[Day 2 - DH, ElGamal, RSA & DSA]] | Diffie-Hellman, ElGamal, RSA, DSA | ✅ |
| [[Day 3 - Elliptic Curves]] | EC arithmetic, Point Addition, Orders | ✅ |

---

## 🧰 Reference Notes

- [[Greatest Common Divisor (GCD)]] — Euclidean Algorithm, coprimality, Z\*_n membership

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

### Common mistakes

> [!warning] Watch out for these
> - `-y mod p` is **NOT** negative — add p: `-3 mod 7 = 4`
> - Division in modular arithmetic = **multiply by inverse**
> - RSA: `d·e ≡ 1 mod ϕ(n)`, NOT mod n
> - EC: check which **case** applies before computing λ
