---
tags: [cryptography, asymmetric, signatures]
aliases: [DSA]
related: "[[Generators in Cryptography]], [[RSA Algorithm]]"
---

# Digital Signature Algorithm (DSA)

## Overview
DSA is a Federal Information Processing Standard for digital signatures. Unlike [[RSA Algorithm]], which can be used for both encryption and signing, DSA is exclusively used for digital signatures. It relies on the Discrete Logarithm Problem.

## Key Generation
1. Choose a prime $q$ (typically 160 bits) and a prime $p$ (typically 1024 bits) such that $q$ divides $(p-1)$.
2. Choose a generator $g$ of the subgroup of order $q$.
3. Choose a private key $x$ such that $0 < x < q$.
4. Compute the public key $y$:
   $$ y = g^x \pmod p $$

## Signing a Message ($m$)
1. Choose a random per-message integer $k$ such that $0 < k < q$.
2. Compute $r$:
   $$ r = (g^k \pmod p) \pmod q $$
3. Compute $s$ using the hash of the message $H(m)$:
   $$ s = k^{-1} (H(m) + x \cdot r) \pmod q $$
   The signature is the pair $(r, s)$.

## Verification
1. Verify that $0 < r < q$ and $0 < s < q$.
2. Compute $w = s^{-1} \pmod q$.
3. Compute $u_1 = H(m) \cdot w \pmod q$ and $u_2 = r \cdot w \pmod q$.
4. Compute $v$:
   $$ v = ((g^{u_1} \cdot y^{u_2}) \pmod p) \pmod q $$
5. The signature is valid if $v = r$.