---
tags: [cryptography, cpt, concept, day2]
aliases: [RSA]
related: "[[Euler's Totient Function (Phi)]], [[Greatest Common Divisor (GCD)]]"
---

# RSA Algorithm

## Overview

RSA (Rivest–Shamir–Adleman) is an asymmetric encryption and signature scheme. Its security rests on the **integer factorisation problem**: given $n = pq$, finding $p$ and $q$ is computationally hard when they are large primes.

---

## Key Generation

| Step | Action | Example |
|---|---|---|
| 1 | Choose distinct primes $p, q$ | $p = 5,\ q = 7$ |
| 2 | $n = p \cdot q$ | $n = 35$ |
| 3 | $\phi(n) = (p-1)(q-1)$ | $\phi(35) = 4 \cdot 6 = 24$ |
| 4 | Choose $e$ with $1 < e < \phi(n)$ and $\gcd(e, \phi(n)) = 1$ | $e = 5$ |
| 5 | Find $d = e^{-1} \bmod \phi(n)$, i.e. $d \cdot e \equiv 1 \pmod{\phi(n)}$ | $d = 5$ (since $5 \cdot 5 = 25 \equiv 1 \bmod 24$) |

**Public key:** $(n, e)$ — shared openly.

**Private key:** $d$ (keep secret; also $p, q, \phi(n)$ must stay secret).

---

## Encryption & Decryption

$$c = m^e \bmod n \qquad m = c^d \bmod n$$

**Worked example:** $n=35$, $e=5$, $d=5$, message $m=3$

$$c = 3^5 = 243 \equiv 33 \pmod{35}$$
$$m = 33^5 \bmod 35 = 3 \checkmark$$

---

## Digital Signatures with RSA

| Operation | Formula |
|---|---|
| Sign | $s = m^d \bmod n$ (sign with private key) |
| Verify | $m \stackrel{?}{\equiv} s^e \pmod{n}$ (verify with public key) |

Note the reversal: encryption uses $e$ (public), signing uses $d$ (private).

---

## Why It Works

By Euler's theorem, $m^{\phi(n)} \equiv 1 \pmod{n}$ when $\gcd(m, n) = 1$.

Since $d \cdot e \equiv 1 \pmod{\phi(n)}$, we have $d \cdot e = k \cdot \phi(n) + 1$ for some integer $k$, so:

$$c^d = (m^e)^d = m^{ed} = m^{k\phi(n)+1} = (m^{\phi(n)})^k \cdot m \equiv 1^k \cdot m = m \pmod{n}$$

---

> [!warning] Common mistakes
> - $d$ is computed mod $\phi(n)$, **not** mod $n$
> - $e$ must be coprime to $\phi(n)$ — not just any odd number
> - Encryption: public key $(n, e)$; Decryption: private key $d$ — never confuse the direction

**See also:** [[Euler's Totient Function (Phi)]] · [[Greatest Common Divisor (GCD)]] · [[Equations and Proofs]]
