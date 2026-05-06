---
tags: [cryptography, cpt, concept, exam-topic, day8]
aliases: [Signatures, Blind RSA, CL Signature, IDEMIX]
related: "[[RSA Algorithm]], [[Equations and Proofs]]"
---

# Advanced Signature Schemes

---

## Blind RSA Signature

Lets a user get a message signed without the signer ever seeing the message.

**Setup:** RSA keys: $n = pq$, public key $pk$, private key $sk$ where $sk \cdot pk \equiv 1 \pmod{\phi(n)}$.

| User $U$ | | Signer $S$ |
|---|---|---|
| $m \in \mathbb{Z}_n$; $r \in_R \mathbb{Z}_n$ with $\gcd(n, r) = 1$ | | |
| $m' = m \cdot r^{pk} \bmod n$ | $\xrightarrow{m'}$ | |
| | | $s' = (m')^{sk} \bmod n$ |
| | $\xleftarrow{s'}$ | |
| $s = s' \cdot r^{-1} \bmod n$ | | |
| **Verify:** $m \stackrel{?}{\equiv} s^{pk} \pmod{n}$ | | |

**Why unblinding works:** $(m')^{sk} = (m \cdot r^{pk})^{sk} = m^{sk} \cdot r^{pk \cdot sk} = m^{sk} \cdot r$, so $s' \cdot r^{-1} = m^{sk}$.

**Worked example:** $n=35$, $sk=5$, $pk=5$ (since $5 \cdot 5 = 25 \equiv 1 \pmod{24}$), $m=2$, $r=3$

| Step | Computation | Result |
|---|---|---|
| Blind | $m' = 2 \cdot 3^5 \bmod 35$ | 31 |
| Sign | $s' = 31^5 \bmod 35$ | 26 |
| Unblind | $s = 26 \cdot 3^{-1} \bmod 35 = 26 \cdot 12 \bmod 35$ | 32 |
| Verify | $32^5 \bmod 35$ | $= 2 = m$ ✓ |

> [!warning] Blinding formula
> $m' = m \cdot r^{pk}$ — the blinding factor is $r^{pk}$, not just $r$.

---

## Camenisch-Lysyanskaya (CL) Signature

The core primitive of **IDEMIX** (anonymous credentials). Signs a message over an RSA-like structure.

**Setup:** primes $p, q$; $n = pq$; random $A, B, C \in_R \mathbb{Z}_n^*$

> [!tip] IDEMIX framing
> "Set up $n, A, B, C$" means: choose primes $p, q$, set $n = pq$, pick three random elements from $\mathbb{Z}_n^*$.

**Sign (Signer → Receiver):**
1. Choose random $e, s \in \mathbb{Z}_{\phi(n)}$
2. Find $v$ such that: $\quad v^e \equiv A^m \cdot B^s \cdot C \pmod{n}$
3. Signature: $\sigma = (v, e, s)$

**Verify:** $v^e \stackrel{?}{\equiv} A^m \cdot B^s \cdot C \pmod{n}$

> [!warning] Exponents, not multipliers
> $e, s$ are exponents of $A, B$ — not multipliers. All exponent arithmetic uses $\phi(n)$, not $n$.

---

### CL Signature Randomization (IDEMIX unlinkability)

Hides which signature was originally issued (makes credential presentations unlinkable).

**Randomize with $r \in_R \mathbb{Z}_{\phi(n)}^*$:**

$$v' = v \cdot B^r \bmod n \qquad s' = s + e \cdot r \bmod \phi(n)$$

Randomized signature: $\sigma' = (v', e, s')$

**Verify randomized:** $v'^e \stackrel{?}{\equiv} A^m \cdot B^{s'} \cdot C \pmod{n}$

---

### Worked Example

$p=3$, $q=7$, $n=21$, $\phi(21) = 2 \cdot 6 = 12$, $A=2$, $B=4$, $C=5$, $m=5$, $e=5$, $s=2$

| Step | Computation | Result |
|---|---|---|
| Find $v$ | $v^5 \equiv 2^5 \cdot 4^2 \cdot 5 \pmod{21}$ | $v = 10$ |
| Check | $10^5 = 100000 \equiv 19 \pmod{21}$; $2^5 \cdot 4^2 \cdot 5 = 32 \cdot 16 \cdot 5 = 2560 \equiv 19$ ✓ | |
| $\sigma$ | $(v, e, s)$ | $(10, 5, 2)$ |
| Randomize $r=5$ | $v' = 10 \cdot 4^5 \bmod 21 = 10 \cdot 16 = 160$ | $v' = 13$ |
| | $s' = 2 + 5 \cdot 5 = 27 \bmod 12$ | $s' = 3$ |
| $\sigma'$ | $(v', e, s')$ | $(13, 5, 3)$ |
| Verify $\sigma'$ | $13^5 \equiv 2^5 \cdot 4^3 \cdot 5 \pmod{21}$: $13 \equiv 13$ | ✓ |

> [!warning] $s'$ is mod $\phi(n)$, **not** mod $n$
> Here $s' = 2 + 5 \cdot 5 = 27 \equiv 3 \pmod{12}$, because $\phi(21) = 12$.
