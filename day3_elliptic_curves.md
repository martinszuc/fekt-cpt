---
tags:
  - cryptography
  - elliptic-curves
  - exam-prep
  - day3
aliases:
  - Day 3
  - Elliptic Curves
  - EC
related:
  - "[[day1_groups_phi_generators]]"
  - "[[day2_DH_ElGamal_RSA_DSA]]"
---

# Day 3 — Elliptic Curves

> [!warning] Prerequisite
> You need modular inverse from [[day1_groups_phi_generators]]. Division in EC arithmetic is **always** modular inverse — there is no actual division.

---

## 1. What is an Elliptic Curve?

The curves in this course have the **short Weierstrass form**:

```
E(Fp) : y² = x³ + a·x + b
```

where `a, b ∈ Fp` and all arithmetic is done **mod p**.

**The set E(Fp)** = all points (x, y) satisfying the equation + the special point **∞ (point at infinity)**.

> [!important] The point at infinity ∞
> ∞ is the **identity element** (like 0 in addition): `P + ∞ = P` for any point P.
> When you compute k·P and get ∞, you've found the order of P.

---

## 2. Is a Point on the Curve?

Substitute (x, y) into the equation and check both sides are equal mod p.

### Worked Example (from the teacher)

**E(F₅): y² = x³ + 2x + 1. Is P = (0, -1) on E(F₅)?**

Left side: `(-1)² = 1`

Right side: `0³ + 2·0 + 1 = 1`

`1 ≡ 1 mod 5` ✓ → **P = (0, -1) is on E(F₅)**

---

**Is T = (3, 1) on E(F₅)?**

Left side: `1² = 1`

Right side: `3³ + 2·3 + 1 = 27 + 6 + 1 = 34 ≡ 34 - 6·5 = 4 mod 5`

`1 ≢ 4 mod 5` → **T = (3, 1) is NOT on E(F₅)**

---

**Is T = (3, 1) on E(F₁₁)?**

Left side: `1² = 1`

Right side: `3³ + 2·3 + 1 = 34 ≡ 34 - 3·11 = 1 mod 11`

`1 ≡ 1 mod 11` ✓ → **T = (3, 1) IS on E(F₁₁)**

> [!warning] The field matters!
> Same point, different answer for different p. Always check which field you're working in.

---

### Exercise 1

**E(F₇): y² = x³ + 2x + 1**

Check whether these points are on the curve:
- A = (3, 3)
- B = (0, 1)
- C = (2, -3)

<details>
<summary>Show answer</summary>

**A = (3, 3):**
Left: 3² = 9 ≡ 2 mod 7
Right: 3³ + 2·3 + 1 = 27+6+1 = 34 ≡ 6 mod 7
2 ≢ 6 → **A is NOT on E(F₇)**

**B = (0, 1):**
Left: 1² = 1
Right: 0+0+1 = 1
1 ≡ 1 mod 7 ✓ → **B IS on E(F₇)**

**C = (2, -3):**
-3 mod 7 = 4, so C = (2, 4)
Left: 4² = 16 ≡ 2 mod 7
Right: 2³ + 2·2 + 1 = 8+4+1 = 13 ≡ 6 mod 7
2 ≢ 6 → **C is NOT on E(F₇)**

</details>

---

## 3. Inverse of a Point

For P = (xp, yp):

```
-P = (xp, -yp mod p)
```

> [!tip] Example
> If P = (2, 3) on E(F₇), then -P = (2, -3 mod 7) = (2, 4).
> Remember: -3 mod 7 = **4** (add p until positive), not -3.

---

## 4. Point Addition: R = P +_E Q

This is the core skill. There are **4 cases** — identify the right one before computing.

---

### Case 1: xp ≠ xq (different x-coordinates)

```
λ = (yq - yp) / (xq - xp) mod p       ← division = modular inverse!

xr = λ² - xp - xq  mod p
yr = λ·(xp - xr) - yp  mod p
```

**R = (xr, yr)**

---

### Case 2: P = Q and yp ≠ 0 (point doubling, 2P)

```
λ = (3·xp² + a) / (2·yp)  mod p        ← a is the curve coefficient

xr = λ² - 2·xp  mod p
yr = λ·(xp - xr) - yp  mod p
```

**R = (xr, yr)**

---

### Case 3: P = Q and yp = 0

```
P +_E P = ∞
```

---

### Case 4: xp = xq but P ≠ Q (same x, different y)

```
P +_E Q = ∞
```

> [!note]
> This happens when Q = -P. They are inverses of each other — their sum is the identity.

> [!important] yr formula is the same for Cases 1 and 2
> ```
> yr = λ·(xp - xr) - yp  mod p
> ```
> Only λ differs between them.

---

### Worked Example 1 — Case 1 (from the teacher)

**E(F₅): y² = x³ + x + 1, P = (0, 1), Q = (2, 1). Compute R = P + Q.**

xp = 0, yp = 1, xq = 2, yq = 1. Since xp ≠ xq → **Case 1**.

```
λ = (yq - yp) / (xq - xp) mod 5
  = (1 - 1) / (2 - 0) mod 5
  = 0 / 2 = 0

xr = 0 - 0 - 2 = -2 ≡ 3 mod 5
yr = 0·(0 - 3) - 1 = -1 ≡ 4 mod 5
```

**R = (3, 4)** ✓

---

### Worked Example 2 — Case 1 (with actual division)

**E(F₇): y² = x³ + 2x + 1, P = (1, 2), Q = (0, 1). Compute R = P + Q.**

xp = 1, yp = 2, xq = 0, yq = 1. Since xp ≠ xq → **Case 1**.

```
λ = (1 - 2) / (0 - 1) mod 7 = (-1) / (-1) mod 7 = 6 / 6 mod 7
```

Find 6⁻¹ mod 7: 6·6 = 36 ≡ 1 mod 7 ✓ → **6⁻¹ = 6**

```
λ = 6 · 6 = 36 ≡ 1 mod 7

xr = 1 - 1 - 0 = 0 mod 7
yr = 1·(1 - 0) - 2 = -1 ≡ 6 mod 7
```

**R = (0, 6)**

Verify: 6² = 36 ≡ 1 mod 7. 0³+0+1 = 1 mod 7. ✓

---

### Worked Example 3 — Case 2 (Point Doubling)

**E(F₅): y² = x³ + x + 1, P = (0, 1). Compute 2P.**

P = Q = (0, 1), yp = 1 ≠ 0 → **Case 2** (a = 1).

```
λ = (3·0² + 1) / (2·1) mod 5 = 1 / 2 mod 5
```

Find 2⁻¹ mod 5: 2·3 = 6 ≡ 1 mod 5 → **2⁻¹ = 3**

```
λ = 1 · 3 = 3 mod 5

xr = 9 - 0 = 9 ≡ 4 mod 5
yr = 3·(0 - 4) - 1 = -13 ≡ 2 mod 5
```

**2P = (4, 2)**

---

### Exercise 2

**E(F₇): y² = x³ + 2x + 1, P = (1, 2), Q = (0, 1).**

Compute:
- **2P** (point doubling)
- **-R** where R = (0, 6) from above

<details>
<summary>Show answer</summary>

**2P**, P = (1, 2), a = 2, p = 7 → Case 2:

```
λ = (3·1 + 2) / (2·2) mod 7 = 5 / 4 mod 7
4⁻¹ mod 7: 4·2=8≡1 → 4⁻¹ = 2
λ = 5·2 = 10 ≡ 3 mod 7

xr = 9 - 2 = 7 ≡ 0 mod 7
yr = 3·(1 - 0) - 2 = 1 mod 7
```

**2P = (0, 1)**

**-R where R = (0, 6):**
-R = (0, -6 mod 7) = **(0, 1)**

</details>

---

## 5. Finding All Points of E(Fp) — Counting Algorithm

This is used to find the **order of E(Fp)** (= total number of points including ∞).

### Method (from the teacher, Lab 3)

**Step 1.** Build a **squares table**: for each y ∈ {0, 1, ..., p-1}, compute y² mod p.

**Step 2.** For each x ∈ {0, 1, ..., p-1}, compute `RHS = x³ + ax + b mod p`.

**Step 3.** Check if RHS appears in the squares table:
- If yes → x gives **2 points**: (x, y) and (x, -y mod p)
- If RHS = 0 → x gives **1 point**: (x, 0)
- If no → x gives **0 points**

**Step 4.** Add 1 for the point ∞.

> [!tip] Squares shortcut
> You only need y from 0 to (p-1)/2. Since (-y)² = y², values repeat. E.g. for p=7: only check y = 0,1,2,3.

---

### Worked Example (from the teacher)

**E(F₅): y² = x³ + x + 1**

**Squares table (mod 5):**

| y | y² mod 5 |
|---|---|
| 0 | 0 |
| ±1 | 1 |
| ±2 | 4 |

**Check each x:**

| x | x³+x+1 mod 5 | In squares? | Points |
|---|---|---|---|
| 0 | 1 | Yes (y=±1) | (0,1), (0,4) |
| 1 | 3 | No | — |
| 2 | 11 ≡ 1 | Yes (y=±1) | (2,1), (2,4) |
| 3 | 31 ≡ 1 | Yes (y=±1) | (3,1), (3,4) |
| 4 | 69 ≡ 4 | Yes (y=±2) | (4,2), (4,3) |

**Points:** (0,1), (0,4), (2,1), (2,4), (3,1), (3,4), (4,2), (4,3), ∞

**Order of E(F₅) = 9** ✓

---

### Exercise 3

**Find all points of E(F₇): y² = x³ - x - 1**

<details>
<summary>Show answer</summary>

**Squares mod 7:** {0→0, 1→1, 2→4, 3→2, 4→2, 5→4, 6→1} → distinct values: {0, 1, 2, 4}

**RHS = x³ - x - 1 mod 7:**

| x | RHS | Square? | Points |
|---|---|---|---|
| 0 | -1 ≡ 6 | No | — |
| 1 | -1 ≡ 6 | No | — |
| 2 | 5 | No | — |
| 3 | 23 ≡ 2 | Yes (y=3,4) | (3,3),(3,4) |
| 4 | 59 ≡ 3 | No | — |
| 5 | 119 ≡ 0 | Yes (y=0) | (5,0) |
| 6 | 209 ≡ 6 | No | — |

**Points:** (3,3), (3,4), (5,0), ∞ → **Order = 4**

</details>

---

## 6. Order of a Point

The **order of a point P** = smallest positive integer k such that `k·P = ∞`.

> [!important] Key rule
> Order of P **divides** order of E(Fp). Only test divisors — same logic as [[day1_groups_phi_generators#4. Order of an Element|element orders in Z\*_n]].

### Worked Example (from the teacher)

**E(F₅): y² = x³ - x + 1, P = (4, 1). Order of E(F₅) = 8.**

Divisors of 8: **1, 2, 4, 8**. Since P ≠ ∞, order > 1. Test 2P:

**Compute 2P** (a = -1, p = 5):
```
λ = (3·16 - 1) / (2·1) mod 5 = 47/2 mod 5 = 2·3 = 6 ≡ 1 mod 5
  (47 ≡ 2 mod 5, 2⁻¹ = 3)

xr = 1 - 8 = -7 ≡ 3 mod 5
yr = 1·(4-3) - 1 = 0 mod 5
```

**2P = (3, 0)**

**Compute 4P = 2·(2P) = 2·(3, 0):**
yp = 0 → **Case 3** → `4P = ∞`

So order divides 4, and 2P ≠ ∞ → **Order of P = 4** ✓

---

### Exercise 4

**E(F₅): y² = x³ + x + 1 (order 9), P = (0, 1).**

Find the order of P. (Hint: divisors of 9 are 1, 3, 9)

<details>
<summary>Show answer</summary>

**2P** (doubling, a=1, p=5):
```
λ = (0 + 1)/2 mod 5 = 1·3 = 3   (2⁻¹=3)
xr = 9 ≡ 4, yr = 3·(0-4)-1 = -13 ≡ 2
2P = (4, 2)
```

**3P = 2P + P = (4,2) + (0,1)**:
```
λ = (1-2)/(0-4) = 1/4 mod 5 = 1·4 = 4   (4⁻¹=4)
xr = 16-4-0 = 12 ≡ 2, yr = 4·(4-2)-2 = 6 ≡ 1
3P = (2, 1)
```

3P ≠ ∞ → order is not 1 or 3 → **Order of P = 9**

P is a generator of E(F₅)!

</details>

---

## 7. Complete Worked Problem (Exam Style)

**E(F₇): y² = x³ + 2x + 1, P = (1, 2), Q = (0, 1).**

**(a)** Are P and Q on the curve?
**(b)** Compute R = P + Q.
**(c)** Find -R.
**(d)** What is the inverse -P?

<details>
<summary>Show answer</summary>

**(a)**
P=(1,2): Left=4, Right=1+2+1=4 mod 7 ✓
Q=(0,1): Left=1, Right=0+0+1=1 mod 7 ✓

**(b)** R = P + Q → **R = (0, 6)** (computed in Worked Example 2)

**(c)** -R = (0, -6 mod 7) = **(0, 1)**

**(d)** -P = (1, -2 mod 7) = **(1, 5)**

</details>

---

## Summary — Point Addition Formula Sheet

| Case | Condition | λ formula |
|---|---|---|
| P + Q, different x | xp ≠ xq | (yq-yp)·(xq-xp)⁻¹ mod p |
| 2P doubling | P=Q, yp≠0 | (3xp²+a)·(2yp)⁻¹ mod p |
| P+P=∞ | yp=0 | — |
| P+Q=∞ | xp=xq, P≠Q | — |

**xr and yr are the same for all non-∞ cases:**
```
xr = λ² - xp - xq  mod p    (use 2·xp for doubling)
yr = λ·(xp - xr) - yp  mod p
```

**Inverse:** -P = (xp, -yp mod p)

**Identity:** P + ∞ = ∞ + P = P

---

## Common Mistakes to Avoid

> [!warning] Top 5 mistakes on EC problems
> 1. **Forgetting -y mod p** → -3 mod 7 = **4**, not -3
> 2. **Division = modular inverse** → `a/b mod p` means `a · b⁻¹ mod p`
> 3. **Wrong field** → always reduce mod p at each step
> 4. **Wrong λ** → Case 1 (P≠Q) vs Case 2 (P=Q) have different numerators
> 5. **Negative intermediate results** → add p to make positive: -5 mod 7 = 2

---

**Previous:** [[day2_DH_ElGamal_RSA_DSA]] | **Back to:** [[Home]]
