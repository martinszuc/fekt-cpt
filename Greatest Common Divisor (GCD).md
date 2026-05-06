---
tags: [cryptography, cpt, concept, day1]
aliases:
  - GCD
  - Greatest Common Divisor
  - Euclidean Algorithm
related:
  - "[[Euler's Totient Function (Phi)]]"
  - "[[RSA Algorithm]]"
  - "[[Group Theory Fundamentals]]"
---

# GCD — How to Compute It

> [!tip] When you need this
> You need GCD for: finding elements of Z\*_n, checking if an inverse exists, RSA key generation. This is a **reference note** — link here from anywhere with `[[gcd]]`.

---

## What is GCD?

`gcd(a, b)` = the **largest number that divides both a and b**.

Examples:
- gcd(6, 14) = 2 — because 2 divides both 6 and 14, and nothing bigger does
- gcd(5, 14) = 1 — only 1 divides both → they are **coprime**
- gcd(9, 6) = 3

> [!important] The key rule for Z\*_n
> - `gcd(a, n) = 1` → a **is** in Z\*_n (has an inverse mod n)
> - `gcd(a, n) > 1` → a is **NOT** in Z\*_n

---

## Method 1 — Trial Division (for tiny numbers)

List divisors of both numbers, pick the biggest common one.

**gcd(8, 14):**
- Divisors of 8: 1, 2, 4, 8
- Divisors of 14: 1, 2, 7, 14
- Common: 1, 2 → **gcd = 2**

> [!warning] Only use this for tiny numbers
> For anything bigger, use the Euclidean Algorithm below.

---

## Method 2 — Euclidean Algorithm (use this one)

Repeatedly divide and take the remainder. Stop when remainder = 0.

```
gcd(a, b):
  divide a by b → get remainder r
  replace: a = b, b = r
  repeat until r = 0
  answer = last non-zero remainder
```

### Worked Example 1

**gcd(48, 18):**

```
48 = 2 · 18 + 12    → remainder 12
18 = 1 · 12 + 6     → remainder 6
12 = 2 · 6  + 0     → remainder 0, stop

gcd(48, 18) = 6
```

---

### Worked Example 2

**gcd(5, 14):**

```
14 = 2 · 5 + 4
 5 = 1 · 4 + 1
 4 = 4 · 1 + 0   → stop

gcd(5, 14) = 1   → 5 ∈ Z*_14 ✓
```

---

### Worked Example 3

**gcd(6, 14):**

```
14 = 2 · 6 + 2
 6 = 3 · 2 + 0   → stop

gcd(6, 14) = 2   → 6 ∉ Z*_14 ✗
```

---

### Exercise — Try these yourself

Compute:
- gcd(3, 14)
- gcd(9, 14)
- gcd(7, 14)
- gcd(11, 14)

<details>
<summary>Show answers</summary>

**gcd(3, 14):**
14 = 4·3 + 2 → 3 = 1·2 + 1 → 2 = 2·1 + 0 → **gcd = 1** → 3 ∈ Z\*_14 ✓

**gcd(9, 14):**
14 = 1·9 + 5 → 9 = 1·5 + 4 → 5 = 1·4 + 1 → 4 = 4·1 + 0 → **gcd = 1** → 9 ∈ Z\*_14 ✓

**gcd(7, 14):**
14 = 2·7 + 0 → **gcd = 7** → 7 ∉ Z\*_14 ✗

**gcd(11, 14):**
14 = 1·11 + 3 → 11 = 3·3 + 2 → 3 = 1·2 + 1 → 2 = 2·1 + 0 → **gcd = 1** → 11 ∈ Z\*_14 ✓

</details>

---

## Quick Shortcut — When One Number is Prime

> [!tip] Prime shortcut
> If `p` is prime, then `gcd(a, p) = 1` for **every** a that is not a multiple of p.
> So for Z\*_p (p prime), just remove 0 and all multiples of p. Everything else is in.

**Example: Z\*_7 = {1, 2, 3, 4, 5, 6}** — all 6 elements, no gcd check needed.

**Example: Z\*_11 = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}** — all 10 elements.

---

## Even Quicker Shortcut — Composite n

For `n = p · q` (two distinct primes), the elements NOT in Z*_n are:
- multiples of p: p, 2p, 3p, ...
- multiples of q: q, 2q, 3q, ...

**Example: Z\*_14, n = 2·7**

Remove multiples of 2: 2, 4, 6, 8, 10, 12
Remove multiples of 7: 7

**Z\*_14 = {1, 3, 5, 9, 11, 13}** — exactly ϕ(14) = 6 elements ✓

No Euclidean algorithm needed at all.

---

## Summary

| Situation | What to do |
|---|---|
| n is prime | Everything from 1 to n-1 is in Z\*_n |
| n = p·q | Remove multiples of p and q |
| General n | Use Euclidean algorithm |
| gcd = 1 | Element is in Z\*_n ✓ |
| gcd > 1 | Element is NOT in Z\*_n ✗ |

---

**Used in:** [[Euler's Totient Function (Phi)]] · [[RSA Algorithm]] · [[Diffie-Hellman Key Exchange]]
