---
tags: [cryptography, cpt, concept, exam-topic, day5]
aliases: [Commitments, Pedersen Commitment, Commitment Scheme]
related: "[[Equations and Proofs]], [[Elliptic Curve Cryptography (ECC)]]"
---

# Commitment Schemes

> [!tip] What this is
> A commitment lets you "lock in" a value $w$ now, and reveal it later — like a sealed envelope. Two properties: the receiver can't learn $w$ until you open it (hiding), and you can't change your mind after committing (binding).

---

## Core Idea

$$c = \text{commit}(w,\, o)$$

- $w$ = message/value being committed to
- $o$ = random opening information (randomness/blinding factor)
- $c$ = the commitment (public, reveal later)

**Hiding:** Given $c$, cannot learn $w$.

**Binding:** Cannot find $(w', o') \neq (w, o)$ such that $\text{commit}(w', o') = c$.

## Security Strengths

| Strength | Meaning |
|---|---|
| **Perfect** | Unbreakable even with infinite computation |
| **Statistical** | Negligible advantage even for an infinite adversary |
| **Computational** | Infeasible for polynomial-time adversaries |

> [!tip] Pedersen is **perfectly hiding**, **computationally binding**

---

## Pedersen Commitment

**Parameters:** prime $p$, generators $g_1, g_2$ of $\mathbb{Z}_p^*$

$$c = g_1^w \cdot g_2^o \bmod p$$

**Protocol:**

| Sender | | Receiver |
|---|---|---|
| $w \in_R \mathbb{Z}_{p-1} \setminus \{0\}$, $o \in_R \mathbb{Z}_{p-1} \setminus \{0\}$ | | |
| $c = g_1^w \cdot g_2^o \bmod p$ | $\xrightarrow{c}$ | Store $c$ |
| Reveal $(w, o)$ | $\xrightarrow{w,\, o}$ | Check: $c \stackrel{?}{=} g_1^w \cdot g_2^o \bmod p$ |

**Worked example:** $p = 11$, $g_1 = 2$, $g_2 = 6$, $w = 3$, $o = 2$

$$c = 2^3 \cdot 6^2 = 8 \cdot 3 = 24 \equiv 2 \pmod{11}$$

---

### Why Perfectly Hiding

Since $g_1$ is a generator, $g_2 = g_1^a$ for some $a$, so:

$$c = g_1^w \cdot g_2^o = g_1^{w + ao}$$

Checking the exponent: $w + ao \equiv b \pmod{p-1}$ — this is a linear equation in two unknowns. It has infinitely many solutions $(w, o)$, so $c$ reveals nothing about $w$.

**Same commitment $c = 2$, different valid openings** ($g_2 = 2^9 \bmod 11$, so $a = 9$):

| $(w, o)$ | Verification |
|---|---|
| $(3, 2)$ | $2^3 \cdot 6^2 = 8 \cdot 3 = 24 \equiv 2$ ✓ |
| $(2, 1)$ | $2^2 \cdot 6^1 = 4 \cdot 6 = 24 \equiv 2$ ✓ |
| $(1, 0)$ | $2^1 \cdot 6^0 = 2$ ✓ |

---

### Why Computationally Binding

Suppose you find two different openings $(w, o) \neq (w', o')$ with the same $c$. Then:

$$g_1^{w-w'} = g_2^{o'-o} \bmod p$$

Since $g_2 = g_1^a$, this gives $a \equiv (w - w')(o' - o)^{-1} \pmod{p-1}$ — solving the DLP of $g_2$ base $g_1$.

Therefore finding two openings = solving a Discrete Logarithm Problem. Hence Pedersen is **computationally binding**.

---

## ElGamal Commitment

$$c = (c_1, c_2) = \bigl(g_1^o,\ g_1^w \cdot g_2^o\bigr) \bmod p$$

Open: reveal $(w, o)$, verifier recomputes the pair.

---

## EC ElGamal Commitment

$$c = (c_1, c_2) = (aP,\ bP + aQ)$$

where $P, Q$ are EC points, $a$ (randomness) and $b$ (message) are scalars.

Verify: recompute $(aP,\ bP + aQ)$ from the opened $(a, b)$.

Hiding/binding rely on the **Elliptic Curve Discrete Logarithm Problem**.

---

> [!warning] Common mistakes
> - $g_1, g_2$ in Pedersen are generators of $\mathbb{Z}_p^*$ — do **not** confuse with EC pairing groups $G_1, G_2$
> - $o$ is the **randomness**, $w$ is the **message**
> - Exponents are computed mod $p-1$ (group order); results are mod $p$
