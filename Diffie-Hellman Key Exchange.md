---
tags: [cryptography, cpt, concept, day2]
aliases: [Diffie-Hellman, DH]
related: "[[Generators in Cryptography]], [[Group Theory Fundamentals]]"
---

# Diffie-Hellman Key Exchange

## Overview
Diffie-Hellman (DH) is a method for securely exchanging cryptographic keys over a public channel. It relies on the difficulty of the Discrete Logarithm Problem (DLP) in [[Group Theory Fundamentals|finite cyclic groups]].

## The Protocol

**1. Public Parameters:**
Alice and Bob agree on a large prime $p$ and a generator $g$ of $\mathbb{Z}_p^*$.
*   Reference: [[Generators in Cryptography]]

**2. Key Generation & Exchange:**
*   **Alice** chooses a private random integer $a$ and sends Bob:
    $$ A = g^a \pmod p $$
*   **Bob** chooses a private random integer $b$ and sends Alice:
    $$ B = g^b \pmod p $$

**3. Shared Secret Calculation:**
*   **Alice** computes the shared secret $K$:
    $$ K = B^a \pmod p = (g^b)^a \pmod p $$
*   **Bob** computes the shared secret $K$:
    $$ K = A^b \pmod p = (g^a)^b \pmod p $$

Both arrive at the exact same shared secret $K$ without ever transmitting $a$ or $b$ across the network.