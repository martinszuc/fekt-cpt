---
tags: [cryptography, cpt, concept, exam-topic, day7]
aliases: [Sigma Protocols, Schnorr, Schnorr AND, Schnorr OR]
related: "[[Day 5 - Commitments]], [[Equations and Proofs]]"
---

# Σ-Protocols (Sigma Protocols)

> [!tip] Structure of every Sigma Protocol
> 1. **Commit** — Prover sends commitment $c$
> 2. **Challenge** — Verifier sends random challenge $e$
> 3. **Response** — Prover sends response $z$
> 4. **Verify** — Verifier checks an equation

---

## Schnorr Protocol

Prover knows private key $w$ where public key $h = g^w \bmod p$.

**Parameters:** prime $p$, prime $q \mid \phi(p)$, $g$ has order $q$ in $\mathbb{Z}_p^*$.

| Prover | | Verifier |
|---|---|---|
| $r \in_R \mathbb{Z}_q \setminus \{0\}$ | | |
| $c = g^r \bmod p$ | $\xrightarrow{c}$ | |
| | $\xleftarrow{e}$ | $e \in_R \mathbb{Z}_q \setminus \{0\}$ |
| $z = (ew + r) \bmod q$ | $\xrightarrow{z}$ | |
| | | Check: $g^z \stackrel{?}{\equiv} h^e \cdot c \pmod{p}$ |

> [!warning] $z$ is computed mod $q$ (subgroup order), **not** mod $p$

**Worked example:** $p=23$, $q=11$, $g=9$, $w=4$, $h = 9^4 \equiv 6 \pmod{23}$

| Step | Value |
|---|---|
| $r = 2$, $c = 9^2 = 81 \equiv 12 \pmod{23}$ | commit |
| Challenge $e = 3$ | |
| $z = (3 \cdot 4 + 2) = 14 \equiv 3 \pmod{11}$ | respond |
| $9^3 = 729 \equiv 16 \pmod{23}$ | |
| $6^3 \cdot 12 = 216 \cdot 12 \equiv 9 \cdot 12 = 108 \equiv 16 \pmod{23}$ ✓ | verify |

---

## AND-Composition (Prover knows **both** $w_1$ and $w_2$)

Proves knowledge of $w_1$ AND $w_2$ where $h_1 = g_1^{w_1}$ and $h_2 = g_2^{w_2}$.

| Prover | | Verifier |
|---|---|---|
| $r_1, r_2 \in_R \mathbb{Z}_q \setminus \{0\}$ | | |
| $c_1 = g_1^{r_1} \bmod p$, $c_2 = g_2^{r_2} \bmod p$ | $\xrightarrow{c_1,\, c_2}$ | |
| | $\xleftarrow{e}$ | $e \in_R \mathbb{Z}_q \setminus \{0\}$ |
| $z_1 = (e \cdot w_1 + r_1) \bmod q$ | | |
| $z_2 = (e \cdot w_2 + r_2) \bmod q$ | $\xrightarrow{z_1,\, z_2}$ | |
| | | Check: $g_1^{z_1} \stackrel{?}{\equiv} h_1^e \cdot c_1 \pmod{p}$ |
| | | Check: $g_2^{z_2} \stackrel{?}{\equiv} h_2^e \cdot c_2 \pmod{p}$ |

**Combined check** for commitment $h = g_1^{w_1} \cdot g_2^{w_2}$ (Pedersen-style):

$$g_1^{z_1} \cdot g_2^{z_2} \stackrel{?}{\equiv} h^e \cdot c \pmod{p}$$

> [!tip] Exam question
> "Fill $z_1$, $z_2$ and what is $g_1^{z_1} \cdot g_2^{z_2} = ?$" → use the combined check above.

---

## OR-Composition (Prover knows **one of** $w_1, w_2$, doesn't reveal which)

Prover knows $w_1$ (not $w_2$). Key idea: **simulate** the unknown branch first.

| Prover | | Verifier |
|---|---|---|
| Pick $z_2, e_2, r_1 \in_R \mathbb{Z}_q \setminus \{0\}$ | | |
| $c_1 = g^{r_1} \bmod p$ | | |
| $c_2 = g^{z_2} \cdot h_2^{-e_2} \bmod p$ | $\xrightarrow{c_1,\, c_2}$ | |
| | $\xleftarrow{e}$ | $e \in_R \mathbb{Z}_q \setminus \{0\}$ |
| $e_1 = e - e_2 \bmod q$ | | |
| $z_1 = (e_1 \cdot w_1 + r_1) \bmod q$ | $\xrightarrow{e_1,\, e_2,\, z_1,\, z_2}$ | |
| | | Check: $e_1 + e_2 \stackrel{?}{\equiv} e \pmod{q}$ |
| | | Check: $g^{z_1} \stackrel{?}{\equiv} h_1^{e_1} \cdot c_1 \pmod{p}$ |
| | | Check: $g^{z_2} \stackrel{?}{\equiv} h_2^{e_2} \cdot c_2 \pmod{p}$ |

**Worked example:** $p=23$, $q=11$, $g=9$, $w_1=2$, $h_1=9^2=12$; simulated: $z_2=3$, $e_2=4$, $r_1=5$

| Step | Computation | Result |
|---|---|---|
| $c_1$ | $9^5 \bmod 23$ | 8 |
| $c_2$ | $9^3 \cdot h_2^{-4} \bmod 23 = 16 \cdot 13$ | 1 |
| Challenge | | $e = 6$ |
| $e_1$ | $6 - 4 \bmod 11$ | 2 |
| $z_1$ | $(2 \cdot 2 + 5) \bmod 11$ | 9 |
| Verify $e_1+e_2$ | $2 + 4 = 6 \equiv e$ | ✓ |
| Verify $c_1$ branch | $9^9 \equiv 2 \equiv 12^2 \cdot 8 \pmod{23}$ | ✓ |
| Verify $c_2$ branch | $9^3 \equiv 16 \equiv h_2^4 \cdot 1 \pmod{23}$ | ✓ |

---

## Quick Reference

| Protocol | Prover proves | Key formulas |
|---|---|---|
| Schnorr | Knows $w$ for $h = g^w$ | $z = ew + r \bmod q$; check $g^z \equiv h^e c$ |
| Schnorr AND | Knows $w_1$ **and** $w_2$ | Two responses $z_1, z_2$; two checks |
| Schnorr OR | Knows $w_1$ **or** $w_2$ | Split challenge $e = e_1 + e_2$; three checks |

> [!warning] Key differences AND vs OR
> - **AND:** both secrets known; single shared challenge $e$; two responses $z_1, z_2$
> - **OR:** one secret known; split $e = e_1 + e_2$; simulate the unknown branch before seeing $e$
