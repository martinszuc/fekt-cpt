---
tags: [cryptography, asymmetric, encryption]
aliases: [ElGamal]
related: "[[Diffie-Hellman Key Exchange]], [[Generators in Cryptography]]"
---

# ElGamal Encryption

## Overview
ElGamal is an asymmetric key encryption algorithm based on the [[Diffie-Hellman Key Exchange]]. Like DH, its security relies on the Discrete Logarithm Problem.

## Key Generation
1. Choose a large prime $p$ and a generator $g$.
2. Choose a private key $x$ such that $1 < x < p-1$.
3. Compute the public key $h$:
   $$ h = g^x \pmod p $$
   **Public Key:** $(p, g, h)$
   **Private Key:** $x$

## Encryption
To encrypt a message $m$:
1. Choose a random ephemeral key $y$ such that $1 < y < p-1$.
2. Compute the shared secret $s = h^y \pmod p$.
3. Compute the ciphertext pair $(c_1, c_2)$:
   $$ c_1 = g^y \pmod p $$
   $$ c_2 = m \cdot s \pmod p $$

## Decryption
To decrypt the ciphertext $(c_1, c_2)$:
1. Compute the shared secret $s$ using the private key $x$:
   $$ s = c_1^x \pmod p = (g^y)^x \pmod p = h^y \pmod p $$
2. Recover the message $m$:
   $$ m = c_2 \cdot s^{-1} \pmod p $$
   *(Note: $s^{-1}$ is the modular inverse of $s$, found using the Extended [[Greatest Common Divisor (GCD)|Euclidean Algorithm]])*