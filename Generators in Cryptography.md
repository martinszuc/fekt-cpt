---
tags: [cryptography, math, groups]
aliases: [Generators, Primitive Roots]
related: "[[Group Theory Fundamentals]], [[Diffie-Hellman Key Exchange]]"
---

# Generators in Cryptography

## Overview
In a cyclic group, a **generator** (or primitive root) is an element $g$ such that every element of the group can be expressed as $g^k$ for some integer $k$.

If the group is $\mathbb{Z}_p^*$ (where $p$ is prime), the group has $\phi(p) = p - 1$ elements.
An element $g$ is a generator if the set:
$$ \{g^1 \pmod p, g^2 \pmod p, \dots, g^{p-1} \pmod p\} $$
generates all numbers from $1$ to $p-1$.

## Finding a Generator
To check if $g$ is a generator of $\mathbb{Z}_p^*$, you must verify that for all prime factors $q$ of $p-1$:
$$ g^{\frac{p-1}{q}} \not\equiv 1 \pmod p $$

## Cryptographic Use Cases
Generators are the foundation of discrete logarithm problems. You will see $g$ used extensively in:
*   [[Diffie-Hellman Key Exchange]]
*   [[ElGamal Encryption]]
*   [[Digital Signature Algorithm (DSA)]]