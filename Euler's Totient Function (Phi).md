---
tags: [cryptography, cpt, concept, day1]
aliases: [Totient Function, Phi, Euler's Totient]
related: "[[RSA Algorithm]], [[Greatest Common Divisor (GCD)]]"
---

# Euler's Totient Function ($\phi$)

## Overview
Euler's Totient Function, denoted as $\phi(n)$, counts the positive integers up to a given integer $n$ that are relatively prime to $n$. Two numbers are relatively prime if their [[Greatest Common Divisor (GCD)]] is $1$.

## Key Formulas

**1. For a prime number $p$:**
$$ \phi(p) = p - 1 $$

**2. For two distinct prime numbers $p$ and $q$ (Used heavily in [[RSA Algorithm]]):**
$$ \phi(p \cdot q) = (p - 1)(q - 1) $$

**3. General Formula:**
If $n = p_1^{k_1} p_2^{k_2} \dots p_r^{k_r}$, then:
$$ \phi(n) = n \left(1 - \frac{1}{p_1}\right) \left(1 - \frac{1}{p_2}\right) \dots \left(1 - \frac{1}{p_r}\right) $$