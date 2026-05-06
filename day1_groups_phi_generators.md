---
tags:
  - cryptography
  - group-theory
  - exam-prep
  - day1
aliases:
  - Day 1
  - Groups and Generators
related:
  - "[[day2_DH_ElGamal_RSA_DSA]]"
  - "[[gcd]]"
---

# Day 1 — Groups, ϕ(n), Orders, Generators

> [!tip] How to use this note
> Read a section, look at the worked example, then try the exercise yourself before checking the answer. Prerequisites: none — this is the foundation for [[day2_DH_ElGamal_RSA_DSA]] and [[day3_elliptic_curves]].

---

## 1. Euler Function ϕ(n)

### Definition

If `n = p₁^a₁ · p₂^a₂ · ... · pₖ^aₖ` then:

```
ϕ(n) = (p₁ - 1) · p₁^(a₁-1) · (p₂ - 1) · p₂^(a₂-1) · ... · (pₖ - 1) · pₖ^(aₖ-1)
```

**Special cases (memorise these):**

| Case | Formula | Example |
|---|---|---|
| n = p (prime) | ϕ(p) = p - 1 | ϕ(7) = 6 |
| n = p·q (two distinct primes) | ϕ(pq) = (p-1)(q-1) | ϕ(15) = 2·4 = 8 |
| n = p^a | ϕ(p^a) = (p-1)·p^(a-1) | ϕ(9) = ϕ(3²) = 2·3 = 6 |

---

### Worked Example 1

**Compute ϕ(45).**

Step 1 — Factor: `45 = 3² · 5`

Step 2 — Apply formula:
```
ϕ(45) = (3 - 1) · 3^(2-1) · (5 - 1) · 5^(1-1)
       = 2 · 3 · 4 · 1
       = 24
```

> [!example] Teacher's example
> This matches the teacher's example exactly.

---

### Worked Example 2

**Compute ϕ(35).**

Step 1 — Factor: `35 = 5 · 7` (two distinct primes, so use shortcut)

Step 2:
```
ϕ(35) = (5 - 1)(7 - 1) = 4 · 6 = 24
```

---

### Exercise 1 — Try it yourself

Compute:
- ϕ(19)
- ϕ(12)
- ϕ(77)

<details>
<summary>Show answer</summary>

**ϕ(19):** 19 is prime → ϕ(19) = 18

**ϕ(12):** 12 = 2² · 3 → ϕ(12) = (2-1)·2^1 · (3-1)·3^0 = 1·2·2·1 = 4

**ϕ(77):** 77 = 7 · 11 → ϕ(77) = (7-1)(11-1) = 6·10 = 60

</details>

---

## 2. The Multiplicative Group Z*_n

### Definition

Z*_n contains all elements `a ∈ Zₙ` such that `gcd(a, n) = 1`.

The **order of Z*_n** (= number of elements) is `ϕ(n)`.

> [!note] How to compute GCD fast
> See [[gcd]] for the full Euclidean algorithm. For n = p·q, just remove multiples of p and q — no computation needed.

---

### Worked Example

**Find all elements of Z*_14.**

Step 1 — List numbers from 1 to 13.

Step 2 — Keep only those where `gcd(a, 14) = 1`:

| a | gcd(a, 14) | In Z*_14? |
|---|---|---|
| 1 | 1 | ✓ |
| 2 | 2 | ✗ |
| 3 | 1 | ✓ |
| 4 | 2 | ✗ |
| 5 | 1 | ✓ |
| 6 | 2 | ✗ |
| 7 | 7 | ✗ |
| 8 | 2 | ✗ |
| 9 | 1 | ✓ |
| 10 | 2 | ✗ |
| 11 | 1 | ✓ |
| 12 | 2 | ✗ |
| 13 | 1 | ✓ |

So **Z*_14 = {1, 3, 5, 9, 11, 13}** → 6 elements.

Check: ϕ(14) = ϕ(2·7) = 1·6 = **6** ✓

---

### Exercise 2

Find all elements of Z*_10 and confirm the count matches ϕ(10).

<details>
<summary>Show answer</summary>

Z*_10 = {1, 3, 7, 9} → 4 elements

ϕ(10) = ϕ(2·5) = 1·4 = 4 ✓

</details>

---

## 3. Modular Inverse

The inverse of `a` in Z*_n is the element `b` such that:
```
a · b ≡ 1 mod n
```

> [!important] Key condition
> The inverse **exists only if gcd(a, n) = 1**. If gcd > 1, there is no inverse — this is why the group is called Z***_n**.

### How to find it (trial method for small numbers)

Try b = 1, 2, 3, ... until `a · b mod n = 1`.

### Worked Example

**Find the inverse of 5 in Z*_11.**

Try: 5·1=5, 5·2=10, 5·3=15≡4, 5·4=20≡9, 5·5=25≡3, 5·6=30≡8, 5·7=35≡2, 5·8=40≡7, 5·9=45≡1 ✓

So `5⁻¹ ≡ 9 mod 11`.

**Verify:** 5 · 9 = 45 = 4·11 + 1 ≡ 1 mod 11 ✓

---

### Worked Example 2

**Find the inverse of 3 in Z*_7.**

Try: 3·1=3, 3·2=6, 3·3=9≡2, 3·4=12≡5, 3·5=15≡1 ✓

So `3⁻¹ ≡ 5 mod 7`.

---

### Exercise 3

Find the inverse of:
- 5 in Z*_14 (if it exists)
- 6 in Z*_14 (if it exists)

<details>
<summary>Show answer</summary>

**5 in Z*_14:** gcd(5,14) = 1 → exists.
Try: 5·1=5, 5·2=10, 5·3=15≡1 mod 14 ✓ → **5⁻¹ = 3**

**6 in Z*_14:** gcd(6,14) = 2 ≠ 1 → **inverse does not exist**

</details>

---

## 4. Order of an Element

### Definition

The **order of element a ∈ Z*_n** is the smallest positive integer `k` such that:
```
a^k ≡ 1 mod n
```

> [!important] Key rule (from the teacher)
> **The order of an element always divides the order of the group.**
> 
> So for Z*_n with order ϕ(n), the only possible element orders are the **divisors of ϕ(n)**.
> This saves a lot of work — you only need to test divisors!

---

### Worked Example (from lab)

**Find the order of a = 4 in Z*_13.**

Step 1 — Order of Z*_13 = ϕ(13) = 12.

Step 2 — Divisors of 12: **1, 2, 3, 4, 6, 12**.

Step 3 — Test each (smallest first), stop when you get 1:

```
4^1 ≡ 4      mod 13  ≠ 1
4^2 ≡ 16 ≡ 3 mod 13  ≠ 1
4^3 ≡ 4·3 = 12       mod 13  ≠ 1
4^4 ≡ 4·12 = 48 ≡ 9  mod 13  ≠ 1
4^6 ≡ 4^3·4^3 = 12·12 = 144 ≡ 1 mod 13  = 1 ✓
```

**Order of 4 is 6.**

> [!tip] Computation shortcut
> 4^3 = 64 = 4·13 + 12 ≡ 12 mod 13. Then 4^6 = (4^3)^2 = 12^2 = 144 = 11·13 + 1 ≡ 1 mod 13. ✓

---

### Worked Example 2

**Find the order of a = 3 in Z*_11.**

ϕ(11) = 10. Divisors of 10: **1, 2, 5, 10**.

```
3^1  ≡ 3   mod 11  ≠ 1
3^2  ≡ 9   mod 11  ≠ 1
3^5  ≡ 3^4·3 = 81·3 = 243 ≡ 1 mod 11   (243 = 22·11 + 1)  = 1 ✓
```

**Order of 3 is 5.**

---

### Exercise 4

Find the order of a = 3 in Z*_14.

Hint: ϕ(14) = 6. Divisors of 6 = {1, 2, 3, 6}.

<details>
<summary>Show answer</summary>

```
3^1 ≡ 3   mod 14  ≠ 1
3^2 ≡ 9   mod 14  ≠ 1
3^3 ≡ 27 ≡ 27-14 = 13 mod 14  ≠ 1
3^6 ≡ 13^2 = 169 ≡ 169-12·14 = 169-168 = 1 mod 14  = 1 ✓
```

**Order of 3 is 6.**

</details>

---

## 5. Generators

### Definition (from the teacher)

> [!note] Generator definition
> A **generator of a group G** is an element of **maximum order** in G.
> 
> For Z*_n, a generator g has order ϕ(n).

**Number of generators of Z*_q (q prime):**
```
ϕ(ϕ(q))
```

*Example: Z*_11 has ϕ(ϕ(11)) = ϕ(10) = 4 generators.*

---

## 6. Generator-Finding Algorithm (from the teacher)

Given Z*_n, to check if g is a generator:

**Step 1.** Compute ϕ(n).

**Step 2.** Find all **prime divisors** of ϕ(n). Call them p₁, p₂, ...

**Step 3.** For each prime divisor pᵢ, compute:
```
g^(ϕ(n) / pᵢ) mod n
```

**Step 4.** If `g^(ϕ(n)/pᵢ) ≢ 1 mod n` for **all** pᵢ → **g is a generator**.

If even one gives 1 → g is NOT a generator, try another g.

---

### Worked Example (from the teacher)

**Is g = 2 a generator of Z*_11?**

Step 1 — ϕ(11) = 10.

Step 2 — Prime divisors of 10: **2 and 5**.

Step 3 — Compute:
```
2^(10/2) = 2^5 = 32 ≡ 10 mod 11  ≠ 1 ✓
2^(10/5) = 2^2 = 4               ≠ 1 ✓
```

Step 4 — Neither is 1 → **g = 2 is a generator of Z*_11**. ✓

---

### Worked Example 2

**Find a generator of Z*_13.**

ϕ(13) = 12. Prime divisors of 12 = **2, 3**.

Try g = 2:
```
2^(12/2) = 2^6 = 64 ≡ 64 - 4·13 = 64-52 = 12 mod 13  ≠ 1 ✓
2^(12/3) = 2^4 = 16 ≡ 16-13 = 3  mod 13               ≠ 1 ✓
```

Neither is 1 → **g = 2 is a generator of Z*_13**. ✓

---

### Exercise 5

Check if g = 3 is a generator of Z*_7.

Hint: ϕ(7) = 6. Prime divisors of 6 = {2, 3}.

<details>
<summary>Show answer</summary>

```
3^(6/2) = 3^3 = 27 ≡ 27-3·7 = 27-21 = 6 mod 7  ≠ 1 ✓
3^(6/3) = 3^2 = 9  ≡ 9-7 = 2  mod 7             ≠ 1 ✓
```

Neither is 1 → **g = 3 is a generator of Z*_7**. ✓

</details>

---

### Exercise 6 (Exam-style)

Find how many generators Z*_11 has. Then verify that g = 2 is one and find the order of g = 3.

<details>
<summary>Show answer</summary>

**How many generators:** ϕ(ϕ(11)) = ϕ(10) = ϕ(2·5) = 1·4 = **4 generators**

**Is g = 2 a generator:** Already shown above — yes.

**Order of g = 3 in Z*_11:**
Divisors of ϕ(11) = 10: {1, 2, 5, 10}
```
3^1  = 3       ≠ 1
3^2  = 9       ≠ 1
3^5  = 243 ≡ 1 mod 11  (243 = 22·11 + 1)
```
**Order of 3 is 5** (not a generator since 5 ≠ 10).

</details>

---

## 7. Fast Exponentiation (Square-and-Multiply)

For computing `a^k mod n` with large k, repeated squaring is your friend.

**Method:** Write k in binary, then square and multiply.

### Worked Example

**Compute 5^5 mod 14.**

5 in binary = 101₂

```
5^1  = 5   mod 14
5^2  = 25  ≡ 11  mod 14
5^4  = 11^2 = 121 ≡ 121 - 8·14 = 121-112 = 9  mod 14
5^5  = 5^4 · 5^1 = 9 · 5 = 45 ≡ 45 - 3·14 = 45-42 = 3  mod 14
```

**5^5 ≡ 3 mod 14**

---

## Summary — What to Remember for the Exam

| Formula | What it is |
|---|---|
| `ϕ(p) = p - 1` | Euler function for prime |
| `ϕ(pq) = (p-1)(q-1)` | Euler function for two primes |
| `ϕ(p^a) = (p-1)·p^(a-1)` | Euler function for prime power |
| Elements of Z*_n | all a with gcd(a,n) = 1 → see [[gcd]] |
| Order of Z*_n | ϕ(n) |
| Order of element a | smallest k s.t. a^k ≡ 1 mod n |
| Order of element divides | order of the group |
| Generator = element of | maximum order = ϕ(n) |
| Number of generators of Z*_q | ϕ(ϕ(q)) |
| Generator test | g^(ϕ(n)/pᵢ) ≢ 1 for all prime divisors pᵢ |

---

## Fermat's Little Theorem (bonus — useful shortcut)

If p is prime and gcd(a, p) = 1:
```
a^(p-1) ≡ 1 mod p
```

> [!tip] Exam shortcut
> This lets you reduce exponents mod (p-1) when working mod p.
> 
> **Example:** Compute 3^100 mod 7.
> ϕ(7) = 6 → 100 mod 6 = 4 → 3^100 ≡ 3^4 = 81 ≡ **4 mod 7**.

---

**Next:** [[day2_DH_ElGamal_RSA_DSA]] — Diffie-Hellman, ElGamal, RSA, DSA
