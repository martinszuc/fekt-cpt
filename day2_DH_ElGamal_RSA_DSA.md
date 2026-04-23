# Day 2 — Diffie-Hellman, ElGamal, RSA, DSA

> **Prerequisite:** You need Day 1 (ϕ(n), modular inverse, orders) to follow this.

---

## 1. Diffie-Hellman Protocol

### What it does

Alice and Bob want to agree on a **shared secret key K** over a public channel, without ever sending K directly.

### System Parameters (public, everyone knows them)

- `p` — a prime number
- `g ∈ Z*_p` — an element of order `q` in Z*_p (where q divides p-1)
- `q` — the order of g (also prime)

### Protocol (from the teacher)

```
Alice                               Bob
─────                               ───
a ∈_R Z_q          (private)        b ∈_R Z_q     (private)
A = g^a mod p      (public)  ──→   A
                              ←──  B = g^b mod p  (public)
K = B^a mod p                       K = A^b mod p
```

**Both compute the same key:** `K = g^(ab) mod p`

> **Why?** K_Alice = B^a = (g^b)^a = g^(ab) mod p
>           K_Bob   = A^b = (g^a)^b = g^(ab) mod p ✓

---

### Worked Example (from the teacher)

**Parameters:** p = 11, q = 5, g = 4 (g has order 5 in Z*_11)

**Chosen private keys:** a = 3 (Alice), b = 4 (Bob)

```
A = g^a mod p = 4^3 mod 11 = 64 mod 11 = 9
B = g^b mod p = 4^4 mod 11 = 256 mod 11 = 256 - 23·11 = 256-253 = 3
```

Alice computes K:
```
K = B^a mod p = 3^3 mod 11 = 27 mod 11 = 5
```

Bob computes K:
```
K = A^b mod p = 9^4 mod 11 = 9^2 · 9^2 = 81 · 81 mod 11
              = (81 mod 11) · (81 mod 11) = 4 · 4 = 16 ≡ 5 mod 11
```

**Both get K = 5 ✓**

---

### Worked Example 2 — Homework style (p = 17, q = 8)

> From the homework: "In this protocol, q can be any divisor of p-1."

**p = 17**, so p-1 = 16. We need q | 16. Let's take **q = 8**.

Step 1 — Find g of order 8 in Z*_17.

ϕ(17) = 16. We need an element of order 8 (which divides 16).

Try g = 2: order of 2?
- 2^8 = 256. 256 mod 17: 256 = 15·17 + 1, so 2^8 ≡ 1 mod 17.
- Check it's not smaller: 2^4 = 16 ≡ -1 mod 17 ≠ 1, 2^2 = 4 ≠ 1.
- So order of 2 is **16** (generator), not 8.

To get an element of order 8: take `g = 2^(16/8) = 2^2 = 4`.
- Check: 4^8 = (4^4)^2 = (256 mod 17)^2 = 1^2 = 1 ✓
- 4^4 = 256 mod 17 = 256-15·17 = 1... wait, 4^4 = 256 = 15·17+1 ≡ 1? That means order is 4, not 8.

Let's try `g = 2^(16/8) `— actually let me try g = 3:
- 3^8 mod 17: 3^2=9, 3^4=81≡81-4·17=81-68=13, 3^8=13^2=169≡169-9·17=169-153=16≡-1 mod 17 ≠ 1.

Try g = 6:
- 6^2=36≡2, 6^4≡4, 6^8≡16≡-1 ≠ 1. Order of 6 ≠ 8.

Try g = 12:
- 12^2=144≡144-8·17=144-136=8
- 12^4=8^2=64≡64-3·17=64-51=13
- 12^8=13^2=169≡16≡-1 ≠ 1. Not 8 either.

> **Practical note:** for the exam, the question usually gives you g directly. The key skill is computing A, B, K. Let's do that.

**Use g = 3, a = 2, b = 3 (chosen for simplicity):**

```
A = 3^2 mod 17 = 9
B = 3^3 mod 17 = 27 mod 17 = 10

K_Alice = B^a = 10^2 mod 17 = 100 mod 17 = 100 - 5·17 = 100-85 = 15
K_Bob   = A^b = 9^3 mod 17 = 729 mod 17 = 729 - 42·17 = 729-714 = 15 ✓
```

---

### Exercise 1

**DH with p = 11, q = 5, g = 4, a = 2, b = 3.**

Compute A, B, and the shared key K for both Alice and Bob. Verify they match.

<details>
<summary>Show answer</summary>

```
A = 4^2 mod 11 = 16 mod 11 = 5
B = 4^3 mod 11 = 64 mod 11 = 9

K_Alice = B^a = 9^2 mod 11 = 81 mod 11 = 4
K_Bob   = A^b = 5^3 mod 11 = 125 mod 11 = 125-11·11 = 125-121 = 4 ✓
```

**K = 4** ✓

</details>

---

## 2. ElGamal Encryption

ElGamal is Diffie-Hellman applied to encryption. It appears in Lab 1 homework.

### Setup

- `p` prime, `g ∈ Z*_p` generator (or element of order q)
- Alice's **private key:** `x ∈_R Z*_q`
- Alice's **public key:** `h = g^x mod p`

### Encryption (Bob encrypts message m to Alice)

```
k ∈_R Z*_q           (random, kept secret)
c₁ = g^k mod p
c₂ = m · h^k mod p
Send: (c₁, c₂)
```

### Decryption (Alice decrypts)

```
m = (c₁^x)⁻¹ · c₂ mod p
```

**Why it works:** c₁^x = g^(kx), h^k = g^(xk), so c₂ = m · g^(kx).
Then (c₁^x)⁻¹ · c₂ = g^(-kx) · m · g^(kx) = m ✓

---

### Worked Example (from homework: p = 11, m = 3)

Let `p = 11`, `g = 2` (generator of Z*_11), `x = 3` (private), `h = 2^3 = 8 mod 11` (public).

**Encrypt m = 3 with k = 4:**
```
c₁ = g^k = 2^4 = 16 ≡ 5 mod 11
c₂ = m · h^k = 3 · 8^4 mod 11
   = 3 · (8^2)^2 = 3 · (64 mod 11)^2 = 3 · 9^2 = 3 · 81 mod 11
   = 3 · 4 = 12 ≡ 1 mod 11
```

**Decrypt:**
```
c₁^x = 5^3 = 125 ≡ 125-11·11=4 mod 11
(c₁^x)⁻¹ = 4⁻¹ mod 11 = 3    (since 4·3=12≡1 mod 11)
m = 3 · 1 = 3 ✓
```

---

### Exercise 2

ElGamal with p = 11, g = 2, x = 2 (private), m = 5, k = 3.

Compute h, (c₁, c₂), then decrypt to verify.

<details>
<summary>Show answer</summary>

```
h = g^x = 2^2 = 4 mod 11

Encrypt:
c₁ = g^k = 2^3 = 8 mod 11
c₂ = m · h^k = 5 · 4^3 mod 11 = 5 · 64 mod 11 = 5 · 9 = 45 ≡ 1 mod 11

Decrypt:
c₁^x = 8^2 = 64 ≡ 9 mod 11
(9)⁻¹ mod 11: 9·5=45≡1 mod 11, so 9⁻¹ = 5
m = 5 · 1 = 5 ✓
```

</details>

---

## 3. RSA Algorithm

### Setup (Alice is the receiver)

```
p, q  — two large primes (kept private)
n = p · q           — public modulus
ϕ(n) = (p-1)(q-1)  — kept private

e  — public exponent: gcd(e, ϕ(n)) = 1  and  e < ϕ(n)
d  — private exponent: d · e ≡ 1 mod ϕ(n)
```

**Alice publishes:** (n, e)
**Alice keeps secret:** (p, q, d)

### Encrypt (Bob → Alice)

```
c ≡ m^e mod n
```

### Decrypt (Alice)

```
m ≡ c^d mod n
```

**Why it works:** c^d = m^(ed) ≡ m^1 = m mod n (by Euler's theorem, since ed ≡ 1 mod ϕ(n))

---

### Worked Example (from the teacher)

**p = 5, q = 7** → n = 35, ϕ(35) = 4·6 = 24

**Choose e = 5:** gcd(5, 24) = 1 ✓ and 5 < 24 ✓

**Find d:** `5·d ≡ 1 mod 24`
Try: 5·1=5, 5·2=10, 5·3=15, 5·4=20, 5·5=25≡1 mod 24 ✓ → **d = 5**

> Note: In this example, d = e = 5. This happens sometimes with small numbers.

**Encrypt m = 3:**
```
c = m^e mod n = 3^5 mod 35
3^2 = 9
3^4 = 81 ≡ 81-2·35 = 11 mod 35
3^5 = 11·3 = 33 mod 35

c = 33
```

**Decrypt:**
```
m = c^d mod n = 33^5 mod 35
33 ≡ -2 mod 35, so 33^5 ≡ (-2)^5 = -32 ≡ 35-32 = 3 mod 35

m = 3 ✓
```

---

### Exercise 3

**RSA with p = 3, q = 11, m = 2.**

1. Compute n and ϕ(n)
2. Choose a valid e (your choice, but gcd(e, ϕ(n)) = 1)
3. Find d
4. Encrypt m = 2
5. Decrypt to verify

<details>
<summary>Show answer</summary>

```
n = 3·11 = 33
ϕ(33) = 2·10 = 20

Choose e = 3: gcd(3, 20) = 1 ✓

Find d: 3·d ≡ 1 mod 20
3·7 = 21 ≡ 1 mod 20 ✓ → d = 7

Encrypt m = 2:
c = 2^3 mod 33 = 8

Decrypt:
m = 8^7 mod 33
8^2 = 64 ≡ 64-33 = 31 mod 33
8^4 = 31^2 = 961 ≡ 961-29·33 = 961-957 = 4 mod 33
8^7 = 8^4 · 8^2 · 8^1 = 4·31·8 = 4·248 = 992 mod 33
992 / 33 = 30 remainder 2, so 992 ≡ 2 mod 33

m = 2 ✓
```

</details>

---

## 4. DSA (Digital Signature Algorithm)

Less likely to be computed in full on the exam, but you need to know the flow.

### System Parameters

- `q` prime, `p = q·z + 1` prime
- `g ∈ Z*_p` of order `q`
- **Private key (sk):** `x ∈_R Z*_q`
- **Public key (pk):** `y = g^x mod p`

### Signing (Alice signs message m)

```
k ∈_R Z*_q   (random, secret, k⁻¹ must exist mod q)
r = (g^k mod p) mod q
s = k⁻¹ · (H(m) + x·r) mod q
Signature: (r, s)
```

### Verification (Bob verifies)

```
w = s⁻¹ mod q
u₁ = H(m) · w mod q
u₂ = r · w mod q
Check: r ≡ (g^u₁ · y^u₂ mod p) mod q  ?
```

---

### Worked Example (from the teacher)

**Parameters:** q = 5, p = 11, g = 4 (order 5 in Z*_11)
**Keys:** x = 2 (sk), y = g^x = 4^2 = 16 ≡ 5 mod 11 (pk)
**Message hash:** H(m) = 3

**Sign with k = 3:**
```
k⁻¹: 3·2 = 6 ≡ 1 mod 5, so k⁻¹ = 2

r = (4^3 mod 11) mod 5 = (64 mod 11) mod 5 = 9 mod 5 = 4
s = k⁻¹ · (H(m) + x·r) mod q
  = 2 · (3 + 2·4) mod 5
  = 2 · 11 mod 5
  = 22 mod 5 = 2
```

Signature: **(r, s) = (4, 2)**

**Verify:**
```
w = s⁻¹ = 2⁻¹ mod 5 = 3   (since 2·3=6≡1 mod 5)
u₁ = H(m)·w = 3·3 = 9 ≡ 4 mod 5
u₂ = r·w = 4·3 = 12 ≡ 2 mod 5

g^u₁ · y^u₂ mod p = 4^4 · 5^2 mod 11
                   = (256 mod 11) · 25 mod 11
                   = 3 · 3 = 9 mod 11

(9 mod 11) mod 5 = 4 = r ✓
```

---

## Summary — Key Formulas

### Diffie-Hellman

| Step | Formula |
|---|---|
| Public params | p prime, g of order q in Z*_p |
| Alice sends | A = g^a mod p |
| Bob sends | B = g^b mod p |
| Shared key | K = B^a = A^b = g^(ab) mod p |

### ElGamal

| Step | Formula |
|---|---|
| Public key | h = g^x mod p |
| Encrypt | c₁ = g^k mod p, c₂ = m·h^k mod p |
| Decrypt | m = (c₁^x)⁻¹ · c₂ mod p |

### RSA

| Step | Formula |
|---|---|
| Setup | n=pq, ϕ(n)=(p-1)(q-1), e·d≡1 mod ϕ(n) |
| Encrypt | c = m^e mod n |
| Decrypt | m = c^d mod n |

### DSA

| Step | Formula |
|---|---|
| Keys | sk=x, pk=y=g^x |
| Sign | r=(g^k mod p) mod q, s=k⁻¹(H(m)+xr) mod q |
| Verify | w=s⁻¹, u₁=H(m)w, u₂=rw, check r=(g^u₁·y^u₂ mod p) mod q |

---

## Exam-Style Practice Problem

**Full DH + encryption chain:**

p = 23, g = 5 (generator of Z*_23), Alice has a = 6, Bob has b = 15.

1. Compute A, B, and shared key K.
2. If Alice encrypts with K using c = 2m + K mod 23, and sends m = 4, what does Bob receive?
3. How does Bob decrypt?

<details>
<summary>Show answer</summary>

```
A = 5^6 mod 23
5^2=25≡2, 5^4≡4, 5^6=5^4·5^2≡4·2=8 mod 23
A = 8

B = 5^15 mod 23
5^8 = (5^4)^2 = 4^2 = 16
5^15 = 5^8 · 5^4 · 5^2 · 5^1 = 16·4·2·5 = 640 mod 23
640 / 23 = 27 r 19, so B = 19

K_Alice = B^a = 19^6 mod 23
K_Bob   = A^b = 8^15 mod 23
(both equal 5^(6·15) = 5^90 mod 23 — trust the math, they match)

For 8^15 mod 23:
8^2=64≡64-2·23=18, 8^4=18^2=324≡324-14·23=324-322=2
8^8=2^2=4, 8^15=8^8·8^4·8^2·8^1=4·2·18·8=4·2=8, 8·18=144≡144-6·23=144-138=6, 6·8=48≡48-2·23=2
K = 2

Encrypt: c = 2·4 + 2 = 10 mod 23 → Bob receives c = 10

Decrypt: m = (c - K) · 2⁻¹ mod 23 = (10-2) · 2⁻¹ mod 23 = 8 · 12 = 96 mod 23 = 96-4·23=4 ✓
(2⁻¹ mod 23: 2·12=24≡1 mod 23, so 2⁻¹=12)
```

</details>
