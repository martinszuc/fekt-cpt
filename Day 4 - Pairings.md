---
tags: [cryptography, cpt, concept, exam-topic, day4]
aliases: [Pairings, Bilinear Pairing, MOV Attack, Boneh-Boyen]
related: "[[Elliptic Curve Cryptography (ECC)]], [[Equations and Proofs]]"
---

# Bilinear Pairings

> [!tip] What this is
> A pairing maps two EC groups into a third (target) group. It enables the MOV attack, 3-party key exchange, and advanced signatures like Boneh-Boyen. Symmetric pairings ($G_1 = G_2$) are the key case for the exam.

---

## Definition

A **bilinear pairing** is a map:

$$e : G_1 \times G_2 \to G_T$$

- **Symmetric:** $G_1 = G_2$ (same group on both sides)
- **Asymmetric:** $G_1 \neq G_2$ (different groups or different fields)

---

## The 5 Pairing Properties

| # | Property | Formula |
|---|---|---|
| 1 | Identity | $e(P, \mathcal{O}) = e(\mathcal{O}, Q) = 1$ |
| 2 | Inverse | $e(-P, Q) = e(P, Q)^{-1} = e(P, -Q)$ |
| 3 | Scalar | $e(aP, Q) = e(P, Q)^a = e(P, aQ)$ |
| 4 | Bilinear | $e(aP, bQ) = e(P, Q)^{ab}$ |
| 5 | Additive | $e(P_1 + P_2, Q) = e(P_1, Q) \cdot e(P_2, Q)$ |

> [!warning] Most tested property
> Property 4: $e(aP, bQ) = e(P,Q)^{ab}$. Memorise this.

**Example:** Is $e(-P, 3Q) = e(P, Q)^{-3}$?

$$e(-P, 3Q) \stackrel{(2)}{=} e(P, 3Q)^{-1} \stackrel{(3)}{=} e(P, Q)^{-3} \checkmark$$

---

## MOV Attack

Reduces the **ECDLP** to a standard DLP in $G_T$ (which is often easier to solve).

**Setup:** Symmetric pairing $e : G \times G \to G_T$, $P \in G$ is a generator.

**Known:** $e(P, P) = g$ (generator of $G_T$) and $e(P, kP) = x$.

**Goal:** Find $k$.

**Procedure:**
1. Note: $e(P, kP) = e(P, P)^k = g^k$ (by property 3)
2. Brute-force: compute $g^1, g^2, g^3, \ldots$ in $G_T$ until finding $x$
3. The matching exponent is $k$

**Worked example:** $e(P,P) = 2$, $e(P, aP) = 5$ in $\mathbb{Z}_{11}^*$

| $i$ | $2^i \bmod 11$ |
|---|---|
| 1 | 2 |
| 2 | 4 |
| 3 | 8 |
| **4** | **5** ← match |

Therefore $a = 4$.

### More Worked Cases

| Setup                                     | Generator powers (stop when match found) | Answer |
| ----------------------------------------- | ---------------------------------------- | ------ |
| $g=6$ in $\mathbb{Z}_{17}^*$, target $13$ | $6,2,12,5,\mathbf{13}$                   | $k=5$  |
| $g=6$ in $\mathbb{Z}_{17}^*$, target $11$ | $6,2,12,5,13,10,9,3,\mathbf{11}$         | $k=9$  |
| $g=5$ in $\mathbb{Z}_{23}^*$, target $11$ | $5,2,10,4,20,8,17,16,\mathbf{11}$        | $k=9$  |
|                                           |                                          |        |

> [!tip] Exam pattern
> The exam gives you $e(P,P)$ and $e(P,kP)$ and asks for $k$. Just compute powers of the generator in $G_T$ until you hit the target. The matching exponent is $k$.

> [!warning] MOV only works with symmetric pairings

### Practice Problem

$e(P,P) = 6$ and $e(P, kP) = 13$ in $\mathbb{Z}_{17}^*$. Find $k$.

> [!info]- Solution
> Compute powers of 6 in $\mathbb{Z}_{17}^*$:
>
> | $i$ | $6^i \bmod 17$ |
> |---|---|
> | 1 | 6 |
> | 2 | 2 |
> | 3 | 12 |
> | 4 | 5 |
> | **5** | **13** ← match |
>
> Therefore $k = 5$.

---

## Short Boneh-Boyen (SBB) Signature

**Setup:** Asymmetric pairing $e : G_1 \times G_2 \to G_T$, $P \in G_1$, $R \in G_2$.

| Parameter | Value |
|---|---|
| Secret key | $sk = a$ |
| Public key | $pk = aR \in G_2$ |
| Message | $m \in \mathbb{Z}_q$ |

**Sign:**

$$S = (a + m)^{-1} \cdot P$$

Compute $(a + m)^{-1} \bmod q$ (modular inverse of the scalar), then EC-multiply by $P$.

**Verify:**

$$e(m \cdot S,\ R) \cdot e(S,\ pk) \stackrel{?}{=} e(P,\ R)$$

**Why it works** (using properties 3 and 5):

$$e(mS, R) \cdot e(S, aR) = e\!\left(\tfrac{m}{a+m}P, R\right) \cdot e\!\left(\tfrac{a}{a+m}P, R\right) = e\!\left(\tfrac{m+a}{a+m}P, R\right) = e(P, R) \checkmark$$

**Worked example** (group order $q = 4$, $a = 2$, $m = 1$, $e(P,R) = 2$):

1. $a + m = 3$; \quad $3^{-1} \bmod 4 = 3$ (since $3 \cdot 3 = 9 \equiv 1 \bmod 4$)
2. $S = 3P = M$
3. Verify: $e(1 \cdot M,\, R) \cdot e(M,\, T) = 3 \cdot 4 = 12 \equiv 2 \pmod 5 = e(P,R)$ ✓

> [!warning] Common mistakes
> - $(a + m)^{-1}$ is the modular inverse mod the **group order** $q$, not mod $p$
> - $S = (a+m)^{-1} \cdot P$ is EC scalar multiplication, not modular exponentiation
