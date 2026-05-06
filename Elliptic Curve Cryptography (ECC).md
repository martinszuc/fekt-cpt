---
tags: [cryptography, cpt, concept, day3]
aliases: [ECC, Elliptic Curves]
related: "[[Group Theory Fundamentals]], [[Digital Signature Algorithm (DSA)]]"
---

# Elliptic Curve Cryptography (ECC)

## Overview
ECC is a form of public-key cryptography based on the algebraic structure of elliptic curves over finite fields. It provides the same level of security as [[RSA Algorithm]] but with significantly smaller key sizes, making it faster and more efficient.

## The Elliptic Curve Equation
Over a field of characteristic $> 3$, an elliptic curve is defined by the Weierstrass equation:
$$ y^2 = x^3 + ax + b $$
where $4a^3 + 27b^2 \neq 0$ (to ensure the curve has no singular points).

## Group Operations on the Curve
ECC takes the concepts of [[Group Theory Fundamentals]] and applies them to the points on this curve.
*   **Point Addition:** $P + Q = R$ (Draw a line through $P$ and $Q$, find the third intersection point, and reflect it across the x-axis).
*   **Point Doubling:** $P + P = 2P$ (Draw a tangent line at $P$, find the intersection, reflect).
*   **Scalar Multiplication:** $kP = P + P + \dots + P$ ($k$ times). This is the foundation of ECC's security.

## The Elliptic Curve Discrete Logarithm Problem (ECDLP)
Given a curve, a generator point $G$, and another point $P = kG$, it is computationally infeasible to find the scalar $k$.

## Common ECC Protocols
*   **ECDH:** Elliptic Curve [[Diffie-Hellman Key Exchange]]
*   **ECDSA:** Elliptic Curve [[Digital Signature Algorithm (DSA)]]