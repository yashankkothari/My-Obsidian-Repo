
# Module 3: Asymmetric Key Cryptography

## Module Overview

This module transitions from symmetric key systems (Module 2) to **Asymmetric Key Cryptography**, also known as **Public Key Cryptography**. Unlike symmetric systems that use a single shared key, asymmetric systems employ a **pair of keys**: a **public key** (shared openly) and a **private key** (kept secret). This paradigm shift enables functionalities like secure key distribution without pre-shared secrets and digital signatures for authentication and non-repudiation.

We will cover:

*   **3.1 Mathematics of Asymmetric Key Cryptography:** The number theory foundations essential for public key algorithms.
    *   Primes and Composite Numbers
    *   Primality Testing
    *   Factorization
    *   Modular Arithmetic Concepts (Congruence, Exponentiation, Logarithm)
    *   Euler's Totient Function
    *   Fermat's Little Theorem and Euler's Theorem
    *   Chinese Remainder Theorem
*   **3.2 Public key cryptography:** Principles, major algorithms, and security considerations.
    *   Principles of Public Key Cryptosystems
    *   The RSA Algorithm
    *   Attacks on RSA
*   **3.3 Key management:** Methods for distributing public keys and establishing shared secrets.
    *   Diffie-Hellman Key Exchange
    *   Man-in-the-Middle Attack

**Additional Concepts Mentioned:**

*   Symmetric vs. Asymmetric Key Cryptography comparison
*   Stream Ciphers vs. Block Ciphers (brief contrast)
*   Elliptic Curve Cryptography (ECC) - mentioned as an example
*   Public Key Infrastructure (PKI) - framework for managing public keys

---

## 3.1 Mathematics of Asymmetric Key Cryptography

The security of most asymmetric cryptographic algorithms relies heavily on the computational difficulty of certain problems in number theory, particularly those involving large prime numbers.

### Primes and Related Concepts

#### Classification of Positive Integers

Positive integers can be categorized based on their divisors:

![[Pasted image 20250506020645.png]]This diagram shows "Positive integers" branching into three categories:
    - *Number 1: Exactly one divisor (itself).*
    - *Primes: Exactly two divisors (1 and itself).*
    - *Composites: More than two divisors.*
*This visually summarizes the fundamental classification based on divisibility.*

1.  **Number 1:** Has exactly one positive divisor (1).
2.  **Prime Number:** A positive integer greater than 1 that has exactly two distinct positive divisors: 1 and itself. (e.g., 2, 3, 5, 7, 11, 13, 17, ...)
3.  **Composite Number:** A positive integer greater than 1 that has more than two positive divisors. It can be factored into smaller integers (excluding 1). (e.g., 4, 6, 8, 9, 10, 12, ...)

#### Coprimes (Relatively Prime Numbers)

-   **Definition:** Two positive integers, $a$ and $b$, are said to be **relatively prime** or **coprime** if their **greatest common divisor (gcd)** is 1.
    -   $gcd(a, b) = 1$
-   *Simplified:* They share no common factors other than 1.
-   **Properties:**
    -   The number 1 is relatively prime to any integer (since $gcd(1, n) = 1$ for any $n$).
    -   If $p$ is a prime number, then all integers from 1 to $p-1$ are relatively prime to $p$. This is because $p$'s only divisors are 1 and $p$, and none of the numbers from 1 to $p-1$ are divisible by $p$.

#### Cardinality and Infinitude of Primes

-   **Cardinality Question:** Given a number $n$, how many primes are smaller than or equal to $n$? This count is given by the **prime-counting function**, denoted $\pi(n)$. Calculating $\pi(n)$ exactly is complex, but it can be approximated (e.g., by $n / \ln(n)$).
-   **Infinitude of Primes (Euclid's Proof Idea):** There are infinitely many prime numbers.
    -   **Proof by Contradiction (Example):**
        1.  Assume there's a finite list of *all* prime numbers, say up to 17: {2, 3, 5, 7, 11, 13, 17}.
        2.  Calculate the product of all these primes: $P = 2 \times 3 \times 5 \times 7 \times 11 \times 13 \times 17 = 510510$.
        3.  Consider the number $P + 1 = 510511$.
        4.  This number $P+1$ must either be prime itself or divisible by some prime.
        5.  However, $P+1$ is not divisible by any of the primes in our original list (2, 3, ..., 17), because dividing $P+1$ by any of these primes leaves a remainder of 1.
        6.  Therefore, $P+1$ must either be a new prime number larger than 17, or it must be divisible by some new prime number larger than 17.
        7.  In this specific example, $510511 = 19 \times 97 \times 277$. These are all primes greater than 17.
        8.  This contradicts the initial assumption that the list {2, ..., 17} contained *all* primes.
        9.  Conclusion: No finite list can contain all prime numbers; therefore, there must be an infinite number of primes.

### Primality Testing

Determining whether a given large number $n$ is prime is crucial for algorithms like RSA.

#### Trial Division Method

-   **Principle:** A number $n$ is composite (not prime) if it has a prime factor less than or equal to its square root ($\sqrt{n}$). If $n$ is not divisible by any prime number $p$ such that $p \le \sqrt{n}$, then $n$ must be prime.
-   **Procedure:** To check if $n$ is prime:
    1. Calculate the floor of $\sqrt{n}$.
    2. Find all prime numbers less than or equal to $\lfloor\sqrt{n}\rfloor$.
    3. Divide $n$ by each of these primes.
    4. If $n$ is divisible by *any* of these primes, then $n$ is **not prime** (it's composite).
    5. If $n$ is not divisible by *any* of these primes, then $n$ **is prime**.
-   **Example 1: Is 97 prime?**
    -   $\lfloor\sqrt{97}\rfloor = 9$.
    -   Primes less than or equal to 9 are: 2, 3, 5, 7.
    -   Check divisibility:
        -   97 / 2 = 48 remainder 1
        -   97 / 3 = 32 remainder 1
        -   97 / 5 = 19 remainder 2
        -   97 / 7 = 13 remainder 6
    -   Since 97 is not divisible by any prime $\le \sqrt{97}$, **97 is prime**.
-   **Example 2: Is 301 prime?**
    -   $\lfloor\sqrt{301}\rfloor = 17$.
    -   Primes less than or equal to 17 are: 2, 3, 5, 7, 11, 13, 17.
    -   Check divisibility:
        -   301 is not divisible by 2 (odd).
        -   301 sum of digits = 4, not divisible by 3.
        -   301 does not end in 0 or 5, not divisible by 5.
        -   $301 / 7 = 43$.
    -   Since 301 is divisible by 7, **301 is not prime**.
-   **Limitation:** Trial division is efficient for small numbers but becomes computationally infeasible for the very large numbers used in modern cryptography (e.g., numbers with hundreds of digits). More sophisticated probabilistic primality tests (like Miller-Rabin) are used in practice.

#### Sieve of Eratosthenes

-   **Purpose:** An ancient algorithm devised by Eratosthenes to find **all** prime numbers less than a given integer $n$.
-   **Method:**
    1.  List all integers from 2 up to $n$.
    2.  Start with the first prime number, $p = 2$. Mark all multiples of $p$ (4, 6, 8, ...) as composite (cross them out), but keep $p$ itself.
    3.  Find the next number in the list greater than $p$ that has not been marked. Set $p$ to this new prime number.
    4.  Repeat step 2: Mark all multiples of this new $p$ (except $p$ itself).
    5.  Continue this process until $p^2 > n$. (Equivalently, continue until $p > \sqrt{n}$, as any larger composite number would have already been marked by a smaller prime factor).
    6.  All the numbers remaining unmarked in the list are prime.
-   **Example: Finding primes less than 100:**
    -   List numbers 2 to 100.
    -   We need to sieve using primes up to $\sqrt{100} = 10$. The primes are 2, 3, 5, 7.
    -   **Step 1 (p=2):** Cross out 4, 6, 8, ..., 100.
    -   **Step 2 (p=3):** Cross out 6, 9, 12, ..., 99 (some are already crossed out).
    -   **Step 3 (p=5):** Cross out 10, 15, 20, ..., 100.
    -   **Step 4 (p=7):** Cross out 14, 21, 28, ..., 98.
    -   The numbers left unmarked are the primes less than 100.
    ![[Pasted image 20250506020704.png]]This image shows a grid of numbers 2-100 with multiples of 2, 3, 5, and 7 shaded or crossed out. The accompanying text outlines the steps: 1. Cross out multiples of 2 (except 2). 2. Cross out multiples of 3 (except 3). 3. Cross out multiples of 5 (except 5). 4. Cross out multiples of 7 (except 7). 5. The remaining numbers are prime. This table visually demonstrates the sieving process.

### Euler's Totient Function ($\phi(n)$)

-   **Context:** Modular arithmetic (arithmetic with remainders). The set of integers modulo $n$ is $\mathbb{Z}_n = \{0, 1, 2, ..., n-1\}$.
-   **Reduced Set of Residues:** A subset of $\mathbb{Z}_n$ containing only those elements that are **relatively prime** to the modulus $n$. This set is often denoted as $\mathbb{Z}_n^*$.
    -   *Example (n=10):*
        -   Complete set $\mathbb{Z}_{10} = \{0, 1, 2, 3, 4, 5, 6, 7, 8, 9\}$.
        -   Numbers relatively prime to 10 (gcd(x, 10)=1) are 1, 3, 7, 9.
        -   Reduced set $\mathbb{Z}_{10}^* = \{1, 3, 7, 9\}$.
-   **Definition:** The **Euler's Totient Function**, denoted $\phi(n)$ (also Euler's phi function), counts the number of positive integers less than or equal to $n$ that are **relatively prime** to $n$.
    -   Equivalently, $\phi(n)$ is the number of elements in the reduced set of residues modulo $n$ (the size of $\mathbb{Z}_n^*$).
-   **Example (n=10):** $\phi(10) = |\mathbb{Z}_{10}^*| = |\{1, 3, 7, 9\}| = 4$.

#### Calculating $\phi(n)$

There are several rules for calculating $\phi(n)$:

1.  **If $n=1$:** $\phi(1) = 1$ (By definition, although the image shows 0, the standard definition counts 1 as coprime to 1, so $\phi(1)=1$). *Note: The image on page 11 states $\phi(1)=0$. While some contexts might define it this way, the standard number-theoretic definition and the one relevant for Euler's Theorem/RSA typically uses $\phi(1)=1$. Let's follow the common definition $\phi(1)=1$.*
2.  **If $p$ is a prime number:** $\phi(p) = p - 1$.
    -   *Reason:* All numbers from 1 to $p-1$ are relatively prime to $p$.
3.  **If $n = p^k$ where $p$ is prime and $k \ge 1$:** $\phi(p^k) = p^k - p^{k-1} = p^{k-1}(p-1)$.
    -   *Reason:* The numbers not relatively prime to $p^k$ are the multiples of $p$: $p, 2p, 3p, ..., p^{k-1}p$. There are $p^{k-1}$ such multiples. So, $\phi(p^k) = (\text{total numbers}) - (\text{multiples of } p) = p^k - p^{k-1}$. *(This corresponds to rule 4 in the image on page 11).*
4.  **If $m$ and $n$ are relatively prime ($gcd(m, n) = 1$):** $\phi(m \times n) = \phi(m) \times \phi(n)$. This property means $\phi$ is a **multiplicative function**. *(This corresponds to rule 3 in the image on page 11).*
5.  **General Formula (using prime factorization):** If the prime factorization of $n$ is $n = p_1^{k_1} p_2^{k_2} \cdots p_r^{k_r}$, then:
    $$ \phi(n) = n \left(1 - \frac{1}{p_1}\right) \left(1 - \frac{1}{p_2}\right) \cdots \left(1 - \frac{1}{p_r}\right) $$
    $$ \phi(n) = (p_1^{k_1} - p_1^{k_1-1}) (p_2^{k_2} - p_2^{k_2-1}) \cdots (p_r^{k_r} - p_r^{k_r-1}) $$
    This follows from rules 3 and 4.

-   **Specific Case (RSA):** If $n = p \times q$ where $p$ and $q$ are distinct primes:
    -   $\phi(n) = \phi(p) \times \phi(q) = (p - 1)(q - 1)$. *(This is a direct application of rules 2 and 4, mentioned on page 11).*

#### Examples of Calculating $\phi(n)$

-   **$\phi(13)$:** Since 13 is prime, $\phi(13) = 13 - 1 = 12$. (Rule 2)
-   **$\phi(10)$:** $10 = 2 \times 5$. Since 2 and 5 are distinct primes (and thus relatively prime), $\phi(10) = \phi(2) \times \phi(5) = (2-1) \times (5-1) = 1 \times 4 = 4$. (Rule 4 & 2)
-   **$\phi(240)$:**
    -   Prime factorization: $240 = 16 \times 15 = 2^4 \times 3^1 \times 5^1$.
    -   Using the general formula (or rules 3 & 4):
        $\phi(240) = \phi(2^4) \times \phi(3^1) \times \phi(5^1)$
        $\phi(2^4) = 2^4 - 2^3 = 16 - 8 = 8$
        $\phi(3) = 3 - 1 = 2$
        $\phi(5) = 5 - 1 = 4$
        $\phi(240) = 8 \times 2 \times 4 = 64$.
        *(Note: The calculation shown on page 12 uses the formula $\phi(p^k) = p^k - p^{k-1}$ directly and seems correct).*
-   **$\phi(49)$:**
    -   Can we say $\phi(49) = \phi(7) \times \phi(7)$? **No.** Rule 4 only applies when the factors are relatively prime. $gcd(7, 7) = 7 \neq 1$.
    -   We must use Rule 3: $49 = 7^2$.
    -   $\phi(49) = \phi(7^2) = 7^2 - 7^1 = 49 - 7 = 42$.
-   **Number of elements in $\mathbb{Z}_{14}^*$ ?**
    -   This is asking for $\phi(14)$.
    -   $14 = 2 \times 7$. Since 2 and 7 are distinct primes, they are relatively prime.
    -   $\phi(14) = \phi(2) \times \phi(7) = (2-1) \times (7-1) = 1 \times 6 = 6$.
    -   The elements are $\{1, 3, 5, 9, 11, 13\}$. These are the numbers less than 14 that are relatively prime to 14.

### Fermat's Little Theorem (FLT)

-   **Importance:** A fundamental theorem in number theory with significant applications in cryptography, particularly for primality testing and modular inverse calculations.
-   **Statement (Version 1):**
    -   If $p$ is a **prime number** and $a$ is an integer **not divisible by $p$** (i.e., $gcd(a, p) = 1$),
    -   Then: $a^{p-1} \equiv 1 \pmod{p}$
    -   *In words:* If you raise $a$ to the power of $(p-1)$ and divide by $p$, the remainder is 1.
-   **Statement (Version 2):**
    -   Removes the condition that $p$ does not divide $a$.
    -   If $p$ is a **prime number** and $a$ is **any integer**,
    -   Then: $a^p \equiv a \pmod{p}$
    -   *Derivation:* If $p$ does not divide $a$, multiply Version 1 by $a$: $a \times a^{p-1} \equiv a \times 1 \pmod{p} \implies a^p \equiv a \pmod{p}$. If $p$ *does* divide $a$, then $a \equiv 0 \pmod{p}$, so $a^p \equiv 0^p \equiv 0 \pmod{p}$, and $a \equiv 0 \pmod{p}$. Thus $a^p \equiv a \pmod{p}$ holds in this case too.

#### Examples Using FLT

-   **Find $6^{10} \pmod{11}$:**
    -   $p = 11$ (prime).
    -   $a = 6$. Since 11 does not divide 6, we can use Version 1.
    -   $p-1 = 10$.
    -   Therefore, $6^{10} \equiv 1 \pmod{11}$.
-   **Find $3^{12} \pmod{11}$:**
    -   $p = 11$ (prime). $a = 3$. $p$ does not divide $a$.
    -   We know $3^{10} \equiv 1 \pmod{11}$ by FLT (Version 1).
    -   We can write $3^{12} = 3^{10} \times 3^2$.
    -   So, $3^{12} \pmod{11} \equiv (3^{10} \pmod{11}) \times (3^2 \pmod{11}) \pmod{11}$
    -   $\equiv (1) \times (9) \pmod{11}$
    -   $\equiv 9 \pmod{11}$.
    -   *(Note: The calculation on page 14 uses $3^{11} \equiv 3 \pmod{11}$ (Version 2) which is also correct: $3^{12} = 3^{11} \times 3^1 \equiv 3 \times 3 \equiv 9 \pmod{11}$)*.

#### Application: Finding Multiplicative Inverses using FLT

-   **Context:** We want to find the multiplicative inverse of $a$ modulo $p$, denoted $a^{-1} \pmod{p}$, where $p$ is prime and $p$ does not divide $a$. This means finding $x$ such that $a \times x \equiv 1 \pmod{p}$.
-   **Derivation:**
    -   From FLT (Version 1), we know $a^{p-1} \equiv 1 \pmod{p}$.
    -   We can rewrite this as $a \times a^{p-2} \equiv 1 \pmod{p}$.
    -   Comparing this to the definition of the inverse ($a \times a^{-1} \equiv 1 \pmod{p}$), we see that:
    -   $a^{-1} \equiv a^{p-2} \pmod{p}$
-   **Result:** Fermat's Little Theorem provides a direct way to compute the modular multiplicative inverse of $a$ modulo a prime $p$, provided $p$ doesn't divide $a$.

-   **Examples:**
    ![[Pasted image 20250506020851.png]]
    - *a. Find $8^{-1} \pmod{17}$. Here $p=17$, $a=8$. Inverse is $8^{17-2} = 8^{15} \pmod{17}$. (Calculation: $8^2=64\equiv13\equiv-4$; $8^4\equiv(-4)^2=16\equiv-1$; $8^8\equiv(-1)^2=1$; $8^{15} = 8^8 \times 8^4 \times 8^2 \times 8^1 \equiv 1 \times (-1) \times (-4) \times 8 = 32 \equiv 15 \pmod{17}$). Result: $15$.*
    - *b. Find $5^{-1} \pmod{23}$. $p=23$, $a=5$. Inverse is $5^{21} \pmod{23}$. Result: $14$.*
    - *c. Find $60^{-1} \pmod{101}$. $p=101$, $a=60$. Inverse is $60^{99} \pmod{101}$. Result: $32$.*
    - *d. Find $22^{-1} \pmod{211}$. $p=211$, $a=22$. Inverse is $22^{209} \pmod{211}$. Result: $48$.*
    *These examples demonstrate the formula $a^{-1} \equiv a^{p-2} \pmod p$. Modular exponentiation (like the method of repeated squaring) is used for efficient calculation.*

### Euler's Theorem

-   **Relation to FLT:** Euler's theorem is a **generalization** of Fermat's Little Theorem. FLT applies only when the modulus is prime, while Euler's theorem applies when the modulus is **any positive integer** $n$.
-   **Statement (Version 1):**
    -   If $a$ and $n$ are positive integers such that **$a$ and $n$ are relatively prime** ($gcd(a, n) = 1$),
    -   Then: $a^{\phi(n)} \equiv 1 \pmod{n}$
    -   *Connection to FLT:* If $n=p$ (a prime), then $\phi(p) = p-1$, and this becomes $a^{p-1} \equiv 1 \pmod p$, which is FLT Version 1.
-   **Statement (Version 2):**
    -   Removes the condition that $a$ and $n$ must be coprime.
    -   If $n = p \times q$ (product of two distinct primes, as in RSA) and $a < n$, and $k$ is any non-negative integer,
    -   Then: $a^{k \times \phi(n) + 1} \equiv a \pmod{n}$
    -   *Note:* This version is particularly useful in proving the correctness of RSA decryption. It holds even if $gcd(a, n) \neq 1$ (i.e., if $a$ is a multiple of $p$ or $q$).

#### Examples Using Euler's Theorem

![[Pasted image 20250506021039.png]]
-   **Example 9.15: Find $6^{24} \pmod{35}$**
    -   $n = 35 = 5 \times 7$. $a = 6$.
    -   Check coprime: $gcd(6, 35) = 1$. Yes.
    -   Calculate $\phi(35) = \phi(5) \times \phi(7) = (5-1) \times (7-1) = 4 \times 6 = 24$.
    -   By Euler's Theorem (Version 1): $6^{\phi(35)} \equiv 6^{24} \equiv 1 \pmod{35}$.
    -   Result: $1$.
-   **Example 9.16: Find $20^{62} \pmod{77}$**
    -   $n = 77 = 7 \times 11$. $a = 20$.
    -   Check coprime: $gcd(20, 77) = 1$. Yes.
    -   Calculate $\phi(77) = \phi(7) \times \phi(11) = (7-1) \times (11-1) = 6 \times 10 = 60$.
    -   We want $20^{62} \pmod{77}$.
    -   Using Euler's Theorem (Version 1): $20^{\phi(77)} = 20^{60} \equiv 1 \pmod{77}$.
    -   Rewrite the exponent: $20^{62} = 20^{60} \times 20^2$.
    -   $20^{62} \pmod{77} \equiv (20^{60} \pmod{77}) \times (20^2 \pmod{77}) \pmod{77}$
    -   $\equiv 1 \times (400 \pmod{77}) \pmod{77}$
    -   $400 = 5 \times 77 + 15$. So, $400 \equiv 15 \pmod{77}$.
    -   Result: $1 \times 15 \equiv 15 \pmod{77}$.
    -   *(Note: The solution on page 18 uses Version 2 with $k=1$: $20^{62} = 20^{1 \times \phi(77) + 2} = 20^{1 \times 60 + 2}$. It incorrectly applies the formula $a^{k\phi(n)+1} \equiv a \pmod n$, which is for exponent $k\phi(n)+1$. The correct application using version 1 is shown above. The direct calculation is $20^{62} \equiv 20^{60} \cdot 20^2 \equiv 1 \cdot 400 \equiv 15 \pmod{77}$.)*

#### Application: Finding Multiplicative Inverses using Euler's Theorem

-   **Context:** Find $a^{-1} \pmod n$ where $gcd(a, n) = 1$.
-   **Derivation:**
    -   From Euler's Theorem (Version 1): $a^{\phi(n)} \equiv 1 \pmod n$.
    -   Rewrite as: $a \times a^{\phi(n)-1} \equiv 1 \pmod n$.
    -   Comparing to $a \times a^{-1} \equiv 1 \pmod n$, we get:
    -   $a^{-1} \equiv a^{\phi(n)-1} \pmod n$.
-   **Result:** Euler's theorem provides a way to compute modular inverses for any modulus $n$, provided $a$ is relatively prime to $n$.

-   **Examples:**
    ![[Pasted image 20250506021102.png]]
    - *a. Find $8^{-1} \pmod{77}$. $n=77$, $a=8$. $gcd(8, 77)=1$. $\phi(77)=60$. Inverse is $8^{\phi(77)-1} = 8^{59} \pmod{77}$. Result: $29$.*
    - *b. Find $7^{-1} \pmod{15}$. $n=15=3\times 5$, $a=7$. $gcd(7, 15)=1$. $\phi(15)=\phi(3)\phi(5)=2\times 4=8$. Inverse is $7^{\phi(15)-1} = 7^7 \pmod{15}$. Result: $13$.*
    - *c. Find $60^{-1} \pmod{187}$. $n=187=11\times 17$, $a=60$. $gcd(60, 187)=1$. $\phi(187)=\phi(11)\phi(17)=10\times 16=160$. Inverse is $60^{\phi(187)-1} = 60^{159} \pmod{187}$. Result: $53$.*
    - *d. Find $71^{-1} \pmod{100}$. $n=100=2^2\times 5^2$, $a=71$. $gcd(71, 100)=1$. $\phi(100)=\phi(2^2)\phi(5^2)=(2^2-2^1)(5^2-5^1)=(2)(20)=40$. Inverse is $71^{\phi(100)-1} = 71^{39} \pmod{100}$. Result: $31$.*
    *(The intermediate steps shown on page 19 ($8^{59} = ...$) are part of the modular exponentiation calculation for the first example).*

### Generating Prime Numbers

Finding large prime numbers is essential for setting up RSA and other public-key systems. While trial division works for small numbers, it's impractical for large ones. Historically, certain formulas were explored:

-   **Mersenne Primes:** Primes of the form $M_p = 2^p - 1$, where $p$ itself must be prime.
    -   Not all numbers of this form are prime. $M_{11} = 2^{11} - 1 = 2047 = 23 \times 89$, so it failed at $p=11$.
    -   Largest known primes are often Mersenne primes. Used in GIMPS (Great Internet Mersenne Prime Search).
-   **Fermat Primes:** Primes of the form $F_n = 2^{2^n} + 1$.
    -   $F_0=3, F_1=5, F_2=17, F_3=257, F_4=65537$ are prime.
    -   Euler showed $F_5 = 2^{32} + 1$ is composite (divisible by 641). It failed at $n=5$. No other Fermat primes are known.
-   **Modern Methods:** Practical generation relies on:
    1.  Picking a large random odd number.
    2.  Using probabilistic primality tests (like Miller-Rabin) to check if it's likely prime with very high probability.
    3.  If it fails, pick another random number and repeat.

### Chinese Remainder Theorem (CRT)

-   **Purpose:** Provides a way to solve a system of simultaneous linear congruences where the moduli are pairwise coprime. It allows reconstruction of a number based on its remainders modulo several different coprime numbers.
-   **Statement:**
    -   Let $n_1, n_2, ..., n_k$ be positive integers that are **pairwise coprime** (i.e., $gcd(n_i, n_j) = 1$ for all $i \neq j$).
    -   Consider the system of congruences:
        $$ x \equiv a_1 \pmod{n_1} $$
        $$ x \equiv a_2 \pmod{n_2} $$
        $$ \vdots $$
        $$ x \equiv a_k \pmod{n_k} $$
    -   This system has a **unique solution** for $x$ modulo $N$, where $N = n_1 \times n_2 \times \cdots \times n_k$.
-   **Solution Formula:**
    -   The unique solution $x \pmod N$ is given by:
        $$ x \equiv \sum_{i=1}^{k} a_i N_i y_i \pmod{N} $$
    -   Where:
        -   $N = n_1 n_2 \cdots n_k$ (the product of all moduli).
        -   $N_i = N / n_i$ (the product of all moduli *except* $n_i$).
        -   $y_i = N_i^{-1} \pmod{n_i}$ (the modular multiplicative inverse of $N_i$ with respect to the modulus $n_i$).

#### Example Using CRT

-   **Problem:** Solve the system:
    -   $x \equiv 2 \pmod{3}$
    -   $x \equiv 3 \pmod{5}$
    -   $x \equiv 2 \pmod{7}$
-   **Solution Steps:**
    1.  **Check Coprime Moduli:** $n_1=3, n_2=5, n_3=7$. They are pairwise coprime ($gcd(3,5)=1, gcd(3,7)=1, gcd(5,7)=1$).
    2.  **Calculate N:** $N = n_1 \times n_2 \times n_3 = 3 \times 5 \times 7 = 105$. The unique solution will be modulo 105.
    3.  **Calculate $N_i$:**
        -   $N_1 = N / n_1 = 105 / 3 = 35$.
        -   $N_2 = N / n_2 = 105 / 5 = 21$.
        -   $N_3 = N / n_3 = 105 / 7 = 15$.
    4.  **Calculate $y_i = N_i^{-1} \pmod{n_i}$:**
        -   $y_1 = N_1^{-1} \pmod{n_1} = 35^{-1} \pmod 3$. Since $35 \equiv 2 \pmod 3$, we need $2^{-1} \pmod 3$. $2 \times 2 = 4 \equiv 1 \pmod 3$. So, $y_1 = 2$.
        -   $y_2 = N_2^{-1} \pmod{n_2} = 21^{-1} \pmod 5$. Since $21 \equiv 1 \pmod 5$, we need $1^{-1} \pmod 5$. $1 \times 1 = 1 \equiv 1 \pmod 5$. So, $y_2 = 1$.
        -   $y_3 = N_3^{-1} \pmod{n_3} = 15^{-1} \pmod 7$. Since $15 \equiv 1 \pmod 7$, we need $1^{-1} \pmod 7$. $1 \times 1 = 1 \equiv 1 \pmod 7$. So, $y_3 = 1$.
    5.  **Calculate x using the formula:**
        $x \equiv \sum a_i N_i y_i \pmod N$
        $x \equiv (a_1 N_1 y_1) + (a_2 N_2 y_2) + (a_3 N_3 y_3) \pmod{105}$
        $x \equiv (2 \times 35 \times 2) + (3 \times 21 \times 1) + (2 \times 15 \times 1) \pmod{105}$
        $x \equiv 140 + 63 + 30 \pmod{105}$
        $x \equiv 233 \pmod{105}$
    6.  **Reduce modulo N:** $233 = 2 \times 105 + 23$. So, $233 \equiv 23 \pmod{105}$.
-   **Unique Solution:** $x = 23$. (Check: $23 \equiv 2 \pmod 3$, $23 \equiv 3 \pmod 5$, $23 \equiv 2 \pmod 7$).

-   **CRT Applicability Note:** The CRT requires the moduli ($n_1, ..., n_k$) to be **pairwise coprime**. The first example on page 23 ($x \equiv 1 \pmod 2, x \equiv 2 \pmod 4, x \equiv 3 \pmod 5$) cannot be solved directly using the standard CRT formula because $gcd(2, 4) = 2 \neq 1$. (Although this specific system has no solution: $x\equiv 2 \pmod 4$ means $x$ is even, but $x\equiv 1 \pmod 2$ means $x$ is odd). The second example ($X \equiv 1 \pmod 3, X \equiv 1 \pmod 4, X \equiv 1 \pmod 5, X \equiv 0 \pmod 7$) can be solved using CRT as 3, 4, 5, 7 are pairwise coprime.

### Section Summary: Mathematics

-   **Primes:** Numbers > 1 divisible only by 1 and themselves. Composites have more divisors. 1 is unique. Infinitely many primes exist.
-   **Coprimes:** Integers with $gcd=1$.
-   **Primality Testing:** Trial division up to $\sqrt{n}$ works for small $n$. Sieve of Eratosthenes finds all primes up to $n$. Probabilistic tests are used for large numbers.
-   **Euler's Totient $\phi(n)$:** Counts numbers $\le n$ coprime to $n$. Multiplicative function. $\phi(p)=p-1$, $\phi(p^k)=p^k-p^{k-1}$, $\phi(pq)=(p-1)(q-1)$.
-   **Fermat's Little Theorem:** If $p$ is prime, $a^{p-1} \equiv 1 \pmod p$ (if $p \nmid a$) or $a^p \equiv a \pmod p$. Used for modular inverse $a^{-1} \equiv a^{p-2} \pmod p$.
-   **Euler's Theorem:** Generalization of FLT. If $gcd(a,n)=1$, then $a^{\phi(n)} \equiv 1 \pmod n$. Used for modular inverse $a^{-1} \equiv a^{\phi(n)-1} \pmod n$.
-   **Chinese Remainder Theorem (CRT):** Solves systems of congruences $x \equiv a_i \pmod{n_i}$ if $n_i$ are pairwise coprime. Has applications in speeding up RSA calculations.

---

## 3.2 Public Key Cryptography

### Symmetric vs. Asymmetric Key Cryptography Recap

| Feature              | Symmetric Cryptography (e.g., DES, AES)                  | Asymmetric Cryptography (e.g., RSA, ECC)                  |
| :------------------- | :----------------------------------------------------- | :------------------------------------------------------ |
| **Keys**             | Single **shared secret key** for encryption & decryption | Pair of keys: **public key** and **private key**         |
| **Key Relationship** | Encryption/Decryption are inverse operations           | Encryption/Decryption may or may not be inverse ops.    |
| **Key Management**   | **Major challenge:** Secure distribution of the shared key. $n(n-1)/2$ keys for $n$ users. | **Simpler distribution:** Public keys shared openly. Private keys kept secret. $2n$ keys for $n$ users (n pairs). |
| **Authentication**   | Authenticates only the pair sharing the key. Cannot prove identity to third parties. | Can authenticate sender to anyone (using digital signatures with private key). |
| **Cipher Types**     | Often **Block Ciphers** (DES, AES), also Stream Ciphers | Often operates mathematically like **Stream Ciphers** (processing large numbers), though structure is different. |
| **Speed**            | Generally **faster**.                                    | Generally **slower**.                                     |
| **Use Cases**        | Bulk data encryption, secure comms in closed systems.    | Key exchange, digital signatures, authentication in open systems. Often used in **hybrid systems** (Asymmetric for key exchange, Symmetric for data). |
| **Security**         | Secure if key managed well & algorithm strong.         | Considered more secure for key distribution/signatures due to separate keys. Relies on computational hardness. |
| **Scalability**      | Key management becomes complex in large networks.        | More scalable for large networks due to public key sharing. |
| **Resources**        | Lower resource usage (computationally faster).         | Higher resource usage (computationally intensive).      |
| **Key Lengths**      | Shorter (e.g., 128, 256 bits for AES).                 | Much longer (e.g., 2048, 3072 bits or more for RSA) for comparable security. |

-   **Number of Keys Calculation:**
    -   **Symmetric:** For a group of $n=100$ users, each pair needs a unique key. Number of pairs = $\binom{n}{2} = \frac{n(n-1)}{2}$.
        $$ \text{No. of keys} = \frac{100 \times (100 - 1)}{2} = \frac{100 \times 99}{2} = 50 \times 99 = 4950 $$
    -   **Asymmetric:** Each user needs one key pair (public + private).
        $$ \text{Total No. of keys} = 2 \times n = 2 \times 100 = 200 $$
        -   Each user needs to know/maintain: Their own private key (1), their own public key (1), the public keys of all other users ($n-1=99$). Total = $1+1+99 = 101$ keys per user (mostly public).

### Public Key Cryptosystems: Principles

-   **Core Idea:** Uses two mathematically related keys. What one key encrypts, only the other key can decrypt (and potentially vice-versa).
-   **Key Pair:**
    -   **Public Key (PU):** Can be shared with anyone without compromising security. Used for:
        -   Encrypting messages intended for the owner of the key pair.
        -   Verifying digital signatures created by the owner.
    -   **Private Key (PR):** Known only to the owner. Must be kept secret. Used for:
        -   Decrypting messages encrypted with the corresponding public key.
        -   Creating digital signatures.
-   **Asymmetry:** The key used for encryption is different from the key used for decryption. Knowing the public key does not (computationally) allow one to determine the private key.
-   **Reliance:** Algorithms rely on one key for encryption and the related, different key for decryption.

#### Terminology & Basic Operation (Encryption for Confidentiality)

-   **Scenario:** Sender A wants to send a confidential message $X$ to Receiver B.
-   **Keys:** Receiver B generates a key pair: Public Key $PU_b$, Private Key $PR_b$. $PR_b$ is kept secret by B; $PU_b$ is made public (e.g., in a directory).
-   **Encryption (by Sender A):**
    1.  Sender A obtains Receiver B's public key $PU_b$.
    2.  A encrypts the plaintext message $X$ using $PU_b$ and the public-key encryption algorithm $E$.
    3.  Ciphertext $Y = E(PU_b, X)$.
    4.  A sends $Y$ to B.
-   **Decryption (by Receiver B):**
    1.  B receives ciphertext $Y$.
    2.  B uses their *private* key $PR_b$ and the public-key decryption algorithm $D$ to recover the message.
    3.  Plaintext $X = D(PR_b, Y)$.
-   **Security:** Only B has $PR_b$, so only B can decrypt the message. Eavesdroppers knowing $PU_b$ and $Y$ cannot compute $X$.

#### Visualizing Public Key Operations

![[Pasted image 20250506021133.png]]Sender (Bob) uses Receiver's (Alice's) Public Key ($PU_a$) to encrypt Plaintext (X) into Ciphertext (Y). Alice uses her Private Key ($PR_a$) to decrypt Y back to X. This provides **confidentiality**.

![[Pasted image 20250506021153.png]]Sender (Bob) uses *his own* Private Key ($PR_b$) to encrypt Plaintext (X) into Ciphertext (Y). Anyone (like Alice) can use Bob's Public Key ($PU_b$) to decrypt Y back to X. This provides **authentication** or a basis for **digital signatures**, as only Bob could have created Y that decrypts correctly with $PU_b$.

![[Pasted image 20250506021209.png]]showing Source A encrypting with $PU_b$ for Destination B, who decrypts with $PR_b$. A cryptanalyst intercepting Y and knowing $PU_b$ cannot get X easily.

![[Pasted image 20250506021227.png]]
showing Source A encrypting with *their own* $PR_a$. Destination B (or anyone) decrypts using $PU_a$. A cryptanalyst intercepting Y cannot forge a message purportedly from A without knowing $PR_a$.

![[Pasted image 20250506021242.png]]
Public-Key Cryptosystem: Authentication and Secrecy). This combines the two operations. Source A first encrypts message X with their *own private key* $PR_a$ (for authentication), then encrypts the result with B's *public key* $PU_b$ (for confidentiality). Destination B first decrypts using *their private key* $PR_b$ (removes confidentiality), then decrypts the result using A's *public key* $PU_a$ (verifies authentication). Provides both services.*

### Requirements for Public Key Cryptography

For a public-key scheme involving keys ($PU_b, PR_b$) for user B, message M, ciphertext C:

1.  **Easy Key Generation:** It must be computationally easy for party B to generate their key pair ($PU_b, PR_b$).
2.  **Easy Encryption:** It must be computationally easy for a sender A, knowing B's public key $PU_b$ and the message $M$, to compute the ciphertext $C = E(PU_b, M)$.
3.  **Easy Decryption:** It must be computationally easy for the receiver B, using their private key $PR_b$, to decrypt the ciphertext $C$ and recover the original message $M = D(PR_b, C)$. So, $M = D(PR_b, E(PU_b, M))$.
4.  **Hard to Find Private Key:** It must be computationally **infeasible** for an adversary, knowing the public key $PU_b$, to determine the corresponding private key $PR_b$. This is the core security assumption.
5.  **Hard to Recover Message:** It must be computationally **infeasible** for an adversary, knowing the public key $PU_b$ and the ciphertext $C$, to recover the original message $M$. (This usually follows from #4, but is a distinct requirement).
6.  **(Optional but Useful):** The encryption and decryption functions can be applied in either order (often needed for digital signatures):
    $M = D(PR_b, E(PU_b, M)) = E(PU_b, D(PR_b, M))$ (Note: The second equality shown on page 41, $M = D[PU_b, E(PR_b, M)]$, is the typical signature process: encrypt/sign with private, decrypt/verify with public).

### RSA Algorithm

-   **Origin:** Named after its inventors: Ron **R**ivest, Adi **S**hamir, and Leonard **A**dleman. Publicly described in 1977/1978.
-   **Type:** The most widely used **public-key cryptosystem**. Can be used for both encryption and digital signatures.
-   *(Note: Calling it a "Stream cipher system" on page 42 is unusual. RSA operates on blocks of data interpreted as large integers, not typically bit-by-bit like a stream cipher.)*
-   **Core Operation:** Relies on **modular exponentiation**.
-   **Security Basis:** Relies on the presumed computational difficulty of **factoring large integers**. Specifically, factoring the modulus $n$ into its prime factors $p$ and $q$.
-   **Attacker's Problem:** To break RSA encryption without the private key, an attacker essentially needs to compute the $e$-th root of the ciphertext modulo $n$, which is believed to be as hard as factoring $n$. ($M \equiv C^{1/e} \pmod n$, related to $M \equiv C^d \pmod n$).

#### RSA Algorithm Steps

![[Pasted image 20250506021330.png]]
    - *Key Generation:* Select primes p, q; compute n=pq, phi(n)=(p-1)(q-1); select e (coprime to phi(n)); compute d (inverse of e mod phi(n)); Public Key KU={e,n}, Private Key KR={d,n}.*
    - *Encryption:* Plaintext M < n; Ciphertext C = M^e mod n.*
    - *Decryption:* Ciphertext C; Plaintext M = C^d mod n.*
*This provides a concise overview of the entire process.*

1.  **Key Generation (performed by the receiver, say Bob):**
    a.  **Select Primes:** Choose two distinct large prime numbers, $p$ and $q$. (These must be kept secret).
    b.  **Compute Modulus:** Calculate the modulus $n = p \times q$. ($n$ is made public).
    c.  **Compute Euler's Totient:** Calculate $\phi(n) = (p - 1)(q - 1)$. ($\phi(n)$ must be kept secret).
    d.  **Select Public Exponent:** Choose an integer $e$ such that:
        -   $1 < e < \phi(n)$
        -   $gcd(e, \phi(n)) = 1$ (i.e., $e$ and $\phi(n)$ are relatively prime).
        (Common choices for $e$ are small primes like 3, or often $65537 = 2^{16}+1$). ($e$ is made public).
    e.  **Compute Private Exponent:** Calculate the integer $d$ such that:
        -   $d \times e \equiv 1 \pmod{\phi(n)}$
        -   $d$ is the **modular multiplicative inverse** of $e$ modulo $\phi(n)$. (Can be found using the Extended Euclidean Algorithm). ($d$ must be kept secret).
    f.  **Publish/Keep Keys:**
        -   **Public Key:** $KU = \{e, n\}$
        -   **Private Key:** $KR = \{d, n\}$ (or just $d$, since $n$ is public. Often $p, q, \phi(n)$ are also kept private for efficiency/security).

2.  **Encryption (performed by the sender, say Alice, using Bob's public key):**
    a.  Obtain Bob's public key $\{e, n\}$.
    b.  Represent the plaintext message $M$ as an integer such that $0 \le M < n$. (If M is longer, break it into blocks).
    c.  Compute the ciphertext $C$:
        $$ C = M^e \pmod{n} $$

3.  **Decryption (performed by the receiver, Bob, using his private key):**
    a.  Receive the ciphertext $C$.
    b.  Use the private key exponent $d$.
    c.  Compute the original message $M$:
        $$ M = C^d \pmod{n} $$
    d.  **Why it works:** $C^d \equiv (M^e)^d = M^{ed} \pmod n$. Since $ed \equiv 1 \pmod{\phi(n)}$, we can write $ed = k \times \phi(n) + 1$ for some integer $k$. By Euler's Theorem (Version 2), $M^{k \times \phi(n) + 1} \equiv M \pmod n$.

#### RSA Examples

-   **Example 1 (page 45):**
    -   $p=3, q=5 \implies n = 3 \times 5 = 15$.
    -   $\phi(n) = (3-1)(5-1) = 2 \times 4 = 8$.
    -   Choose $e$ such that $1 < e < 8$ and $gcd(e, 8)=1$. Possible values: {3, 5, 7}. Let $e=3$.
    -   Find $d$ such that $d \times 3 \equiv 1 \pmod 8$. By inspection or Extended Euclidean Algorithm, $d=3$ works (since $3 \times 3 = 9 \equiv 1 \pmod 8$).
    -   Public Key: $\{e, n\} = \{3, 15\}$. Private Key: $\{d, n\} = \{3, 15\}$. (Note: $d=e$ here, this is unusual and only happens for very small numbers).
    -   Let message $M=4$.
    -   Encryption: $C = M^e \pmod n = 4^3 \pmod{15} = 64 \pmod{15}$. $64 = 4 \times 15 + 4$. So, $C=4$.
    -   Decryption: $M = C^d \pmod n = 4^3 \pmod{15} = 64 \pmod{15}$. $M=4$. (Works, but M=C is coincidental here).
-   **Example 2 (page 46):**
    -   $p=11, q=3 \implies n = 11 \times 3 = 33$.
    -   $\phi(n) = (11-1)(3-1) = 10 \times 2 = 20$.
    -   Choose $e$ such that $1 < e < 20$ and $gcd(e, 20)=1$. Possible values: {3, 7, 9, 11, 13, 17, 19}. Let $e=3$.
    -   Find $d$ such that $d \times 3 \equiv 1 \pmod{20}$. Using Extended Euclidean Algorithm or inspection: $7 \times 3 = 21 \equiv 1 \pmod{20}$. So, $d=7$.
    -   Public Key: $\{e, n\} = \{3, 33\}$. Private Key: $\{d, n\} = \{7, 33\}$.
    -   Let message $M=7$.
    -   Encryption: $C = M^e \pmod n = 7^3 \pmod{33} = 343 \pmod{33}$. $343 = 10 \times 33 + 13$. So, $C=13$.
    -   Decryption: $M = C^d \pmod n = 13^7 \pmod{33}$. (Calculation needed, e.g., repeated squaring).
        $13^1 \equiv 13$
        $13^2 = 169 = 5 \times 33 + 4 \equiv 4 \pmod{33}$
        $13^4 \equiv 4^2 = 16 \pmod{33}$
        $13^7 = 13^4 \times 13^2 \times 13^1 \equiv 16 \times 4 \times 13 = 64 \times 13 \pmod{33}$
        $64 \equiv -2 \pmod{33}$
        $\equiv (-2) \times 13 = -26 \equiv 7 \pmod{33}$. So, $M=7$. (Matches original).

### Applications, Advantages, Disadvantages of RSA

#### Applications

RSA is highly versatile and used in numerous security applications:

-   **Secure Communications:** Encrypting data over insecure networks (SSL/TLS for HTTPS, SSH, S/MIME email).
-   **Digital Signatures:** Verifying authenticity (sender identity) and integrity (message unchanged) of documents/messages.
    -   **Sign:** Sender encrypts a hash of the message with their **private key**.
    -   **Verify:** Receiver decrypts the signature with the sender's **public key** and compares the result to a hash of the received message.
-   **Key Exchange:** Securely exchanging symmetric keys (e.g., session keys for TLS) between parties. Often used within protocols like Diffie-Hellman or directly encrypting a symmetric key with the recipient's public key.
-   **Secure Email:** PGP and S/MIME use RSA for encrypting email content and verifying sender identity via digital signatures.
-   **Secure File Transfer:** Encrypting files during transmission (e.g., SFTP built on SSH).
-   **Digital Certificates (PKI):** The foundation of Public Key Infrastructure. Certificate Authorities (CAs) use RSA to sign digital certificates, binding a public key to an identity (website, organization, individual). Browsers use these certificates to verify website identity in HTTPS.
-   **Authentication:** Secure login (SSH key pairs), two-factor authentication systems.
-   **Secure E-commerce:** Protecting credit card details and online banking transactions during transmission.
-   **VPNs:** Establishing secure, encrypted connections over the internet.
-   **Data Integrity:** Verifying software updates/downloads haven't been tampered with using RSA signatures.
-   **Secure Messaging Apps:** Encrypting conversations and verifying user identities.
-   **IoT Security:** Securing communication between devices and servers.
-   **Secure Cloud Storage:** Encrypting data stored in the cloud, ensuring only authorized users can access it.

#### Advantages

-   **Security:** High level of security when using sufficiently long keys (e.g., 2048 bits or more), based on the difficulty of factoring large numbers.
-   **Public/Private Key Pair:** Eliminates the need for pre-sharing a secret key, simplifying key distribution in open environments. Enables communication between parties who haven't met before.
-   **Digital Signatures:** Provides a robust mechanism for authentication, integrity, and non-repudiation (sender cannot deny sending the message).
-   **Key Exchange:** Facilitates secure establishment of shared secrets (e.g., symmetric keys) over insecure channels.
-   **Mathematical Soundness:** Based on a well-understood, hard mathematical problem (factoring).
-   **Standardization:** Widely adopted and standardized (e.g., PKCS#1), supported by numerous libraries and implementations.

#### Disadvantages

-   **Key Length & Performance:** Requires much longer keys than symmetric algorithms for equivalent security. Longer keys lead to:
    -   **Computational Intensity:** Encryption and especially decryption (using the larger private exponent $d$) are computationally expensive (slow) compared to symmetric ciphers.
    -   **Performance Overhead:** Can be a bottleneck in high-throughput systems (e.g., busy web servers). Often mitigated using **hybrid encryption** (RSA to encrypt/exchange a fast symmetric key, then use the symmetric key for bulk data).
    -   **Storage Overhead:** Longer keys and associated certificates require more storage.
-   **Key Management:** While distribution is simpler than symmetric keys, managing public/private keys securely (especially private keys) is critical and can be complex in large systems. Loss/compromise of a private key is catastrophic. Ensuring authenticity of public keys is crucial (addressed by PKI/Certificates).
-   **Vulnerability to Quantum Computing:** Shor's algorithm, executable on a sufficiently powerful quantum computer, can factor large numbers efficiently, breaking RSA's core security assumption. This motivates research into **post-quantum cryptography**.
-   **Lack of Forward Secrecy (inherently):** If an attacker records encrypted traffic and later compromises the long-term private key, they can decrypt *all* past messages encrypted with that key. Protocols like TLS often use ephemeral Diffie-Hellman on top of RSA/certificates to achieve forward secrecy for session keys.

### Attacks on RSA

RSA's security relies on the difficulty of factoring $n$ and the related difficulty of computing the $e$-th root modulo $n$. Various attacks target different aspects of the algorithm or its implementation.

#### Main Attack Categories

1.  **Brute Force Key Search:** Trying all possible private keys ($d$). Impractical due to the large size of $d$.
2.  **Factorization Attack:** Try to factor the modulus $n$ into its primes $p$ and $q$. If successful, the attacker can compute $\phi(n)=(p-1)(q-1)$ and then compute the private key $d$ from the public key $e$. **This is the most significant threat to RSA's mathematical foundation.** Algorithms like Pollard's Rho, and especially the General Number Field Sieve (GNFS), are used. Security relies on choosing $n$ large enough to make factorization computationally infeasible.
3.  **Timing Attacks (Side-Channel):** Exploit variations in the time it takes to perform RSA decryption ($M = C^d \pmod n$). The time taken by modular exponentiation algorithms (like square-and-multiply) can depend on the bits of the private exponent $d$. By precisely measuring decryption times for many ciphertexts, an attacker might deduce bits of $d$. Requires insecure implementation. Mitigation involves **blinding** (randomizing intermediate values) or ensuring constant-time execution.
4.  **Chosen Plaintext Attack (CPA):** Attacker chooses plaintexts, gets them encrypted with the target's public key, and observes ciphertexts. In basic RSA ("textbook RSA"), this doesn't directly reveal $d$. However, textbook RSA is deterministic ($M^e \pmod n$ always gives same $C$ for same $M$), which is insecure. **Padding schemes** (like OAEP) are essential in real-world RSA to make encryption probabilistic and resist CPA.
5.  **Ciphertext-Only Attack:** Attacker only has ciphertexts. Generally very hard for properly implemented RSA with large keys, unless there are specific vulnerabilities (like small $e$ with unpadded small messages).
6.  **Common Modulus Attack:** If multiple users share the same modulus $n$ but use different key pairs $(e_1, d_1), (e_2, d_2)$, and the same message $M$ is encrypted with both public keys ($C_1 = M^{e_1} \pmod n$, $C_2 = M^{e_2} \pmod n$), an attacker intercepting $C_1$ and $C_2$ can potentially recover $M$ if $gcd(e_1, e_2)=1$. **Moral: Never share the modulus $n$.**
7.  **Quantum Computing Attacks:** Shor's algorithm on a quantum computer breaks RSA by factoring $n$ efficiently. This is a future threat motivating post-quantum cryptography.

#### Specific Attack Details & Examples

-   **Common Modulus Attack (Detail - page 59):**
    -   If $C_1 = M^{e_1} \pmod n$ and $C_2 = M^{e_2} \pmod n$.
    -   If $gcd(e_1, e_2) = 1$, the attacker can find integers $a$ and $b$ (using Extended Euclidean Algorithm) such that $ae_1 + be_2 = 1$.
    -   Then $C_1^a \times C_2^b \equiv (M^{e_1})^a \times (M^{e_2})^b = M^{ae_1 + be_2} = M^1 = M \pmod n$.
    -   The attacker computes $M$ from the two ciphertexts and public exponents without needing to factor $n$ or find $d$.
-   **Short Message Attack / Small Exponent Attack (pages 60-63):**
    -   Applies when **small messages** ($M$) are encrypted with textbook RSA using a **small public exponent** ($e$, e.g., $e=3$) **without padding**.
    -   If $M^e < n$, then $C = M^e \pmod n$ simply becomes $C = M^e$.
    -   An attacker can compute the integer $e$-th root of $C$ to find $M$. (e.g., if $e=3$, compute $\sqrt[3]{C}$).
    -   **More General Idea (Precomputation - page 60):** Even if $M^e \ge n$, if the space of possible messages is small (e.g., symmetric keys, Social Security Numbers), an attacker (Darth) knowing the public key $(e, n)$ can pre-compute a table:
        1. Encrypt *all possible plausible messages* $M_i$ using the public key: $C_i = M_i^e \pmod n$.
        2. Store pairs $(M_i, C_i)$ in a table.
        3. Intercept an actual encrypted message $C$.
        4. Look up $C$ in the precomputed table. If a match $C = C_j$ is found, the attacker recovers the plaintext $M_j$.
    -   **SSN Example (pages 61-63):** Darth knows Bob will send Alice her 9-digit SSN encrypted with her public key $K_{PU}$. Darth gets Alice's public key. Since there are "only" a billion possible 9-digit SSNs, Darth encrypts all of them with Alice's public key and stores the results. When Bob sends the actual encrypted SSN, Darth intercepts it, looks it up in his table, finds the match, and recovers Alice's SSN without needing Alice's private key.
    -   **Mitigation:** Use **padding schemes** (e.g., OAEP) which add randomness to the message before encryption, making the output different each time and preventing precomputation attacks. Never use textbook RSA directly.
-   **Timing Attack (Details - pages 64-67):**
    -   **Basis:** The standard "square and multiply" algorithm for computing $M = C^d \pmod n$ processes the bits of the private exponent $d$ one by one.
        ```
        result = 1
        C_squared = C
        for i = 0 to number_of_bits_in_d - 1 {
          if (i-th bit of D == 1) {
            result = (result * C_squared) mod n  // Extra multiplication if bit is 1
          }
          C_squared = (C_squared * C_squared) mod n // Always perform squaring
        }
        return result
        ```
    -   **Leakage:** If the multiplication `(result * C_squared)` takes a measurably different amount of time depending on the values involved, or if it's only performed when the bit of $d$ is 1, an attacker measuring the *total time* for decryption might infer how many '1' bits are in $d$, or potentially the bit pattern itself.
    -   **Conditions (page 65):** Attacker needs intercepted ciphertext $C$, ability to measure total decryption time precisely, and ideally knows how long the modular multiplication takes.
    -   **Information Gained:** Can reveal the Hamming weight (number of 1s) of $d$, or more detailed information with sophisticated analysis.
    -   **Mitigation (page 67):**
        -   **Blinding:** Multiply the ciphertext $C$ by a random value before decryption, and adjust the result afterwards. This randomizes intermediate values, obscuring the correlation between timing and the bits of $d$.
        -   **Constant-Time Implementation:** Ensure all operations (especially the conditional multiplication) take the *exact same amount of time* regardless of the bit value. This might involve always performing a multiplication but discarding the result if the bit is 0 ("padding" the algorithm).
-   **Cycling Attack (pages 68-69):**
    -   **Idea:** Repeatedly encrypting a ciphertext $C$ with the public key $e$. Since the message space modulo $n$ is finite, this sequence $C_0=C, C_1=C_0^e \pmod n, C_2=C_1^e \pmod n, ...$ must eventually repeat. Sometimes, it might cycle back to the original message $M$.
    -   The attack assumes $M = (C_k)^e \pmod n$ for some $k$, meaning the previous ciphertext $C_k$ must be the original message $M$.
    -   **Procedure:** Attacker intercepts $C$. Computes $C_1=C^e, C_2=C_1^e, ...$ until they compute some $C_{k+1} = (C_k)^e \equiv C \pmod n$. The attacker then guesses that $M = C_k$.
    -   **Example (page 69):** Key {7, 77}. Ciphertext $C=37$.
        $C_1 = 37^7 \pmod{77} = 16$
        $C_2 = 16^7 \pmod{77} = 58$
        $C_3 = 58^7 \pmod{77} = 9$
        $C_4 = 9^7 \pmod{77} = 37 (= C)$
        The cycle returns to $C=37$. The value encrypted just before this was $C_3 = 9$. Attacker concludes $M=9$.
    -   **Effectiveness:** Generally considered **ineffective** against properly chosen RSA parameters. The cycle length is usually very large.
-   **Factoring Small Modulus Attack (Insecure Key Lengths) (pages 70-71):**
    -   If the modulus $n$ is too small, it can be factored easily, revealing $p$ and $q$.
    -   Once $p$ and $q$ are known, $\phi(n)=(p-1)(q-1)$ can be calculated.
    -   With $\phi(n)$ and the public exponent $e$, the private exponent $d$ can be computed using the Extended Euclidean Algorithm ($d \equiv e^{-1} \pmod{\phi(n)}$).
    -   **Example (page 70):** Key {3, 187}. Factor $187 = 11 \times 17$. $p=11, q=17$. $\phi(187) = (11-1)(17-1) = 10 \times 16 = 160$. Find $d$ such that $3d \equiv 1 \pmod{160}$. $d=107$. Private key is {107, 187}.
    -   **Example (page 71):** Key {3, 33}. Factor $33 = 3 \times 11$. $p=3, q=11$. $\phi(33) = (3-1)(11-1) = 2 \times 10 = 20$. Find $d$ such that $3d \equiv 1 \pmod{20}$. $d=7$. Private key is {7, 33}.
    -   **Moral:** Use large moduli (2048 bits or more) to make factorization infeasible.
-   **Chosen Plaintext Attack (Theoretical Example - page 72):**
    -   This example seems flawed. It shows an attacker choosing P1=10, P2=20 and getting C1=37, C2=77 using $e=3$. It then tries to find $d$ by solving $37^{d1} \equiv 10 \pmod n$ and $77^{d2} \equiv 20 \pmod n$. This is the discrete logarithm problem, which is hard, not how CPA usually works. CPA typically aims to exploit weaknesses revealed by encrypting *chosen* related inputs, not directly solving for $d$. Real CPA resistance comes from padding.

#### How to Make RSA Strong

(Summarizing page 73 and mitigation points)

1.  **Use Strong Key Lengths:** Choose a large modulus $n$ (e.g., 2048 bits, 3072 bits, or 4096 bits) to make factorization computationally infeasible.
2.  **Employ Secure Padding Schemes:** **Crucial.** Use standardized padding like OAEP (Optimal Asymmetric Encryption Padding) for encryption and PSS (Probabilistic Signature Scheme) for signatures. Padding adds randomness and structure, preventing textbook attacks like small message attacks, chosen plaintext attacks, and certain cryptographic attacks. **Never use raw/textbook RSA.**
3.  **Secure Implementation:** Use well-vetted, updated cryptographic libraries that protect against side-channel attacks (like timing attacks) using techniques like blinding or constant-time operations.
4.  **Proper Key Management:** Protect the private key rigorously. Use secure methods for key generation and storage. Ensure authenticity of public keys (e.g., via certificates in a PKI).
5.  **Avoid Common Modulus:** Never allow multiple entities to share the same RSA modulus $n$.
6.  **Consider Post-Quantum Alternatives:** Be aware of the threat from quantum computers and monitor the development and standardization of post-quantum cryptographic algorithms.

### Section Summary: Public Key Cryptography & RSA

-   **Asymmetric (Public Key) Crypto:** Uses key pairs (public, private). Enables confidentiality without pre-shared keys and digital signatures. Slower than symmetric but solves key distribution. Often used in hybrid systems.
-   **Requirements:** Easy key gen/encrypt/decrypt; hard to find private key from public; hard to find message from public+ciphertext.
-   **RSA:** Most popular public-key system. Security based on factoring difficulty.
    -   **Key Gen:** Choose primes $p,q$; $n=pq$; $\phi(n)=(p-1)(q-1)$; choose $e$ coprime to $\phi(n)$; find $d \equiv e^{-1} \pmod{\phi(n)}$. $KU=\{e,n\}, KR=\{d,n\}$.
    -   **Encrypt:** $C = M^e \pmod n$.
    -   **Decrypt:** $M = C^d \pmod n$.
-   **RSA Applications:** Wide range (TLS, SSH, PGP, Signatures, Certificates, etc.).
-   **RSA Attacks:** Factorization (main threat), Timing, Common Modulus, attacks on poor implementation (no padding, small $e$ with small $M$), future Quantum attacks.
-   **RSA Security:** Requires large keys (2048+ bits), secure padding (OAEP/PSS), side-channel resistant implementation, proper key management.

---

## 3.3 Key Management and Exchange

While public key cryptography simplifies key distribution compared to symmetric systems (no need to secretly share the key used for encryption), managing and distributing **public keys** securely still presents challenges. How does Alice know the public key she obtained really belongs to Bob and not an imposter?

### Approaches to Public Key Distribution

1.  **Public Announcement:** Users broadcast their public keys.
    -   *Problem:* Highly vulnerable to **forgery**. Anyone can announce a public key claiming to be someone else.
2.  **Publicly Available Directory:** A central trusted entity (like a Key Distribution Center - KDC, but for public keys) maintains and provides public keys upon request.
    -   *Problem:* Directory must be trustworthy and secure. Subject to **tampering** (if attacker can modify entries) or denial of service. Requires users to trust and interact with the directory.
3.  **Public Key Authority (PKA):** Similar to a directory, but potentially more involved. The PKA might perform stronger checks before listing a key.
    -   *Problem:* Can become a **bottleneck** if heavily used. Still requires trust in the PKA. PKA needs its own public/private key pair for secure communication.
4.  **Public Key Certificates (PKC):** The most common approach, forming the basis of **Public Key Infrastructure (PKI)**.
    -   Removes the need to always contact a central authority directly to get a key.
    -   The trusted entity becomes a **Certification Authority (CA)**.
    -   **Certificate:** A data structure containing a user's public key, identity information (name, organization, etc.), validity period, and other details, all **digitally signed** by the CA using the CA's private key.
    -   **Verification:** Anyone can verify the signature on the certificate using the CA's trusted public key. If the signature is valid, they can trust that the public key in the certificate genuinely belongs to the identified entity.
    -   *Benefit:* Decentralizes trust somewhat. Users only need to trust a limited number of root CAs.

### Diffie-Hellman Key Exchange (DHKE)

-   **Purpose:** Allows two parties (Alice and Bob) who have never met before to securely establish a **shared secret key** over an insecure communication channel, without sending the key itself. This shared secret can then be used, for example, as a key for symmetric encryption (like AES).
-   **History:** The first practical public-key *type* scheme proposed (by Whitfield Diffie and Martin Hellman in 1976), alongside their conceptualization of public-key cryptography.
-   **Nature:** It's a **key distribution / key agreement** scheme, **not** a general encryption or digital signature algorithm. It cannot be used directly to encrypt arbitrary messages.
-   **Security Basis:** Relies on the difficulty of the **Discrete Logarithm Problem (DLP)** in a finite group.

#### Discrete Logarithm Problem (DLP)

-   **Context:** Arithmetic modulo a large prime $p$.
-   **Primitive Root (Generator):** An integer $\alpha$ is a **primitive root** modulo $p$ if its powers $\alpha^1, \alpha^2, \alpha^3, ..., \alpha^{p-1} \pmod p$ generate all the integers from $1$ to $p-1$ exactly once (in some order). The set $\mathbb{Z}_p^* = \{1, ..., p-1\}$ forms a cyclic group under multiplication modulo $p$, and $\alpha$ is a generator of this group.
-   **Modular Exponentiation (Easy):** Given a generator $\alpha$, a prime $p$, and an exponent $x$, it is computationally **easy** to calculate $y = \alpha^x \pmod p$.
-   **Discrete Logarithm (Hard):** Given a generator $\alpha$, a prime $p$, and a value $y$ (where $y = \alpha^x \pmod p$), it is computationally **hard** to find the original exponent $x$. This $x$ is called the **discrete logarithm** (or index) of $y$ to the base $\alpha$, modulo $p$.
-   **Analogy:** Similar difficulty relationship as multiplication (easy) vs. factoring (hard) for RSA.

#### Diffie-Hellman Algorithm

![[Pasted image 20250506021422.png]]\
This clearly outlines the steps:*
    - *Global Public Elements: Prime q, primitive root alpha.*
    - *User A Key Generation: Select private XA (<q), Calculate public YA = alpha^XA mod q.*
    - *User B Key Generation: Select private XB (<q), Calculate public YB = alpha^XB mod q.*
    - *Calculation of Secret Key by User A: K = (YB)^XA mod q.*
    - *Calculation of Secret Key by User B: K = (YA)^XB mod q.*
*This is the core mathematical process.*

1.  **Setup (Global Parameters):**
    -   Alice and Bob (and everyone else) agree on two public parameters:
        -   A large prime number $q$.
        -   An integer $\alpha$ that is a primitive root modulo $q$.
2.  **Alice's Actions:**
    -   Chooses a secret random integer $X_A$ such that $1 \le X_A < q$. This is Alice's **private key**.
    -   Computes her **public key** $Y_A = \alpha^{X_A} \pmod q$.
    -   Sends $Y_A$ to Bob over the insecure channel.
3.  **Bob's Actions:**
    -   Chooses a secret random integer $X_B$ such that $1 \le X_B < q$. This is Bob's **private key**.
    -   Computes his **public key** $Y_B = \alpha^{X_B} \pmod q$.
    -   Sends $Y_B$ to Alice over the insecure channel.
4.  **Shared Secret Calculation:**
    -   **Alice computes:** $K = (Y_B)^{X_A} \pmod q$.
    -   **Bob computes:** $K = (Y_A)^{X_B} \pmod q$.
5.  **Result:** Both Alice and Bob now possess the same shared secret key $K$.
    -   **Why?**
        -   Alice calculates $K = (Y_B)^{X_A} = (\alpha^{X_B})^{X_A} = \alpha^{X_B X_A} \pmod q$.
        -   Bob calculates $K = (Y_A)^{X_B} = (\alpha^{X_A})^{X_B} = \alpha^{X_A X_B} \pmod q$.
        -   Since $X_A X_B = X_B X_A$, both compute the same value.
    -   An eavesdropper intercepting $q, \alpha, Y_A, Y_B$ cannot easily compute $K$ because doing so would require solving the DLP to find either $X_A$ (from $Y_A$) or $X_B$ (from $Y_B$).

#### Diffie-Hellman Example (page 82)

-   **Global Parameters:** $q = 353$ (prime), $\alpha = 3$ (primitive root mod 353).
-   **Alice:** Chooses private key $X_A = 97$. Computes public key $Y_A = 3^{97} \pmod{353} = 40$.
-   **Bob:** Chooses private key $X_B = 233$. Computes public key $Y_B = 3^{233} \pmod{353} = 248$.
-   **Exchange:** Alice sends 40 to Bob. Bob sends 248 to Alice.
-   **Shared Secret Calculation:**
    -   Alice computes $K = (Y_B)^{X_A} \pmod{353} = 248^{97} \pmod{353} = 160$.
    -   Bob computes $K = (Y_A)^{X_B} \pmod{353} = 40^{233} \pmod{353} = 160$.
-   **Result:** Both Alice and Bob agree on the shared secret key $K=160$.
-   **Attacker View:** An attacker knows $q=353, \alpha=3, Y_A=40, Y_B=248$. To find $K$, they need to solve either $3^x \equiv 40 \pmod{353}$ (to find $X_A=97$) or $3^x \equiv 248 \pmod{353}$ (to find $X_B=233$). This is the DLP. For large $q$, this is infeasible. (The example notes brute force finds $X_A=97$ quickly for this small $q$).

#### Vulnerability: Man-in-the-Middle (MITM) Attack

-   **Problem:** Basic Diffie-Hellman provides **no authentication**. Alice doesn't know if the $Y_B$ she received really came from Bob, and Bob doesn't know if $Y_A$ really came from Alice.
-   **Attack Scenario:** An attacker, Eve (or Darth), sits between Alice and Bob.
    1.  Alice chooses $X_A$, computes $Y_A = \alpha^{X_A} \pmod q$. Sends $Y_A$ towards Bob.
    2.  **Eve intercepts $Y_A$.** Eve chooses her *own* private key $X_E$ (or $X_v$ page 84), computes $Y_E = \alpha^{X_E} \pmod q$. Eve sends **$Y_E$ to Bob**, pretending it's from Alice.
    3.  Bob receives $Y_E$ (thinking it's $Y_A$). Bob chooses $X_B$, computes $Y_B = \alpha^{X_B} \pmod q$. Sends $Y_B$ towards Alice.
    4.  **Eve intercepts $Y_B$.** Eve chooses another private key $X_F$ (or $X_w$ page 84), computes $Y_F = \alpha^{X_F} \pmod q$. Eve sends **$Y_F$ to Alice**, pretending it's from Bob.
    5.  **Alice computes secret:** $K_1 = (Y_F)^{X_A} = (\alpha^{X_F})^{X_A} = \alpha^{X_F X_A} \pmod q$. Alice thinks this is her shared key with Bob.
    6.  **Bob computes secret:** $K_2 = (Y_E)^{X_B} = (\alpha^{X_E})^{X_B} = \alpha^{X_E X_B} \pmod q$. Bob thinks this is his shared key with Alice.
    7.  **Eve computes both secrets:**
        -   Key with Alice: $K_1' = (Y_A)^{X_F} = (\alpha^{X_A})^{X_F} = \alpha^{X_A X_F} \pmod q$. (Matches Alice's $K_1$).
        -   Key with Bob: $K_2' = (Y_B)^{X_E} = (\alpha^{X_B})^{X_E} = \alpha^{X_B X_E} \pmod q$. (Matches Bob's $K_2$).
-   **Outcome:** Eve has established two separate secure channels. She shares $K_1$ with Alice and $K_2$ with Bob. Alice and Bob think they are communicating securely with each other, but Eve can intercept messages, decrypt them (using the appropriate key), read/modify them, and re-encrypt them (using the other key) to forward them. Alice and Bob have no shared key between them.

    ![[Pasted image 20250506021443.png]]
    This visually shows Darth intercepting communications between Alice and Bob, substituting his own public keys ($Y_{D1}, Y_{D2}$) and establishing separate secret keys (K1 with Bob, K2 with Alice).*

#### Defending Against MITM in DHKE

MITM attacks exploit the lack of authentication of the public keys ($Y_A, Y_B$). Defenses involve adding authentication:

1.  **Pre-existing Shared Secret:** If Alice and Bob already share some secret (e.g., a password), they can use it to authenticate the exchanged public keys (e.g., by encrypting or MACing the keys).
2.  **Public Key Certificates:** Alice and Bob can have their long-term DH public keys signed by a trusted CA. They exchange certificates along with their ephemeral public keys. Each verifies the signature on the other's certificate before computing the shared secret. This ensures they are talking to the legitimate owner of the private key corresponding to the certified public key.
3.  **Published Keys / Digital Phonebook:** Using somewhat permanent, authenticated public keys stored in a trusted directory or phonebook (as mentioned on page 85).

#### DHKE and Safe Primes

-   **Basic Requirement:** DH works with any large prime $p$ (or $q$ in notation used) and a primitive root $\alpha$.
-   **Enhanced Security:** The security is improved if the prime $p$ has additional properties.
-   **Safe Prime:** A prime $p$ is called a **safe prime** if $(p-1)/2$ is also prime. Let $p = 2q' + 1$ where $q'$ is prime.
    -   *Benefit:* Using a safe prime $p$ makes the group $\mathbb{Z}_p^*$ more resistant to certain attacks on the DLP (like the Pohlig-Hellman algorithm), as the largest subgroup order is large ($q'$).
-   **Generator Choice:** It's also often recommended to choose a generator $\alpha$ such that it generates a large subgroup, ideally the subgroup of quadratic residues (size $(p-1)/2 = q'$ when $p$ is a safe prime). The condition $\alpha^{(p-1)/2} \equiv -1 \pmod p$ mentioned on page 87 relates to $\alpha$ *not* being a quadratic residue, which is sometimes preferred. Choosing $\alpha$ with order $q'$ is common.

### Section Summary: Key Management & DHKE

-   **Public Key Distribution:** Challenges include ensuring authenticity. Methods: Public announcement (insecure), Directory (needs trust, tamper-proof), PKA (bottleneck), Certificates/PKI (standard approach, relies on trusted CAs).
-   **Diffie-Hellman Key Exchange:** Allows two parties to agree on a shared secret key over an insecure channel without prior shared secrets. Security relies on the difficulty of the Discrete Logarithm Problem (DLP).
-   **DHKE Process:** Agree on public $(q, \alpha)$. Alice chooses $X_A$, sends $Y_A=\alpha^{X_A}$. Bob chooses $X_B$, sends $Y_B=\alpha^{X_B}$. Shared secret $K = (Y_B)^{X_A} = (Y_A)^{X_B}$.
-   **MITM Attack:** DHKE is vulnerable if keys aren't authenticated. Eve intercepts, substitutes her own keys, establishes separate keys with Alice and Bob.
-   **MITM Defense:** Authenticate exchanged public keys (e.g., using certificates or prior shared secrets).
-   **Safe Primes:** Using a prime $p$ where $(p-1)/2$ is also prime enhances DHKE security against certain DLP attacks.

---

## Glossary (Module 3 Additions)

-   **Asymmetric Key Cryptography:** Cryptography using a pair of keys (public and private) for encryption/decryption or signing/verification.
-   **Public Key:** The key in an asymmetric pair that can be shared openly. Used for encryption or signature verification.
-   **Private Key:** The key in an asymmetric pair that must be kept secret. Used for decryption or signature creation.
-   **Prime Number:** Integer > 1 divisible only by 1 and itself.
-   **Composite Number:** Integer > 1 that is not prime.
-   **Relatively Prime (Coprime):** Two integers whose greatest common divisor (gcd) is 1.
-   **Primality Testing:** Determining if a number is prime.
-   **Trial Division:** Primality test method checking divisibility by primes up to $\sqrt{n}$.
-   **Sieve of Eratosthenes:** Algorithm to find all primes up to a limit $n$.
-   **Euler's Totient Function ($\phi(n)$):** Counts positive integers $\le n$ that are relatively prime to $n$.
-   **Reduced Set of Residues ($\mathbb{Z}_n^*$):** The set of integers modulo $n$ that are relatively prime to $n$. Its size is $\phi(n)$.
-   **Multiplicative Function:** A number-theoretic function $f(n)$ such that $f(mn) = f(m)f(n)$ whenever $gcd(m,n)=1$. ($\phi(n)$ is multiplicative).
-   **Fermat's Little Theorem (FLT):** If $p$ is prime and $p \nmid a$, then $a^{p-1} \equiv 1 \pmod p$.
-   **Euler's Theorem:** If $gcd(a, n)=1$, then $a^{\phi(n)} \equiv 1 \pmod n$. Generalization of FLT.
-   **Modular Multiplicative Inverse:** For $a$ and $n$, the integer $x$ such that $ax \equiv 1 \pmod n$. Denoted $a^{-1} \pmod n$. Can be found using Extended Euclidean Algorithm, FLT (if n is prime), or Euler's Theorem.
-   **Mersenne Prime:** A prime of the form $2^p - 1$.
-   **Fermat Prime:** A prime of the form $2^{2^n} + 1$.
-   **Chinese Remainder Theorem (CRT):** Theorem for solving systems of simultaneous linear congruences with pairwise coprime moduli.
-   **Public Key Cryptosystem:** A system based on asymmetric key pairs (e.g., RSA, ECC).
-   **RSA:** Public-key cryptosystem based on the difficulty of factoring large integers. Used for encryption and digital signatures.
-   **Modulus (RSA):** The number $n=pq$ used in RSA calculations.
-   **Public Exponent (RSA):** The exponent $e$ used for encryption or signature verification.
-   **Private Exponent (RSA):** The exponent $d$ used for decryption or signature generation.
-   **Padding Scheme (RSA):** Method (e.g., OAEP, PSS) applied to messages before RSA operation to enhance security against various attacks. **Essential for secure use.**
-   **Factorization Attack:** Attack aiming to break RSA by factoring the modulus $n$.
-   **Timing Attack:** Side-channel attack exploiting time variations in cryptographic operations.
-   **Common Modulus Attack:** Attack on RSA when the same modulus $n$ is used with different exponents for different users.
-   **Cycling Attack:** Attack involving repeated encryption, generally impractical against RSA.
-   **Short Message Attack:** Attack on textbook RSA with small messages, often combined with small exponents or precomputation. Prevented by padding.
-   **Quantum Computing Attack:** Attack using algorithms like Shor's on a quantum computer to break underlying mathematical problems (factoring for RSA, DLP for DHKE).
-   **Hybrid Encryption:** Using asymmetric crypto to exchange a key for a faster symmetric cipher, which then encrypts the bulk data.
-   **Forward Secrecy:** Property ensuring that compromise of long-term keys does not compromise past session keys. RSA lacks this inherently; DHKE can provide it if used ephemerally.
-   **Key Management:** Processes for handling cryptographic keys (generation, distribution, storage, revocation).
-   **Public Key Infrastructure (PKI):** Framework (policies, CAs, certificates) for managing public keys and enabling trust.
-   **Certification Authority (CA):** Trusted entity that issues and signs digital certificates.
-   **Digital Certificate:** Digitally signed document binding a public key to an identity.
-   **Diffie-Hellman Key Exchange (DHKE):** Protocol for two parties to establish a shared secret over an insecure channel.
-   **Primitive Root (Generator):** Element $\alpha$ in $\mathbb{Z}_p^*$ whose powers generate all elements of the group.
-   **Discrete Logarithm Problem (DLP):** The hard problem of finding exponent $x$ given base $\alpha$, result $y$, and prime modulus $p$ in $y \equiv \alpha^x \pmod p$. Underlies DHKE security.
-   **Man-in-the-Middle (MITM) Attack:** Attack where adversary secretly relays and possibly alters communication between two parties who believe they are communicating directly. Affects unauthenticated DHKE.
-   **Safe Prime:** A prime $p$ such that $(p-1)/2$ is also prime. Using safe primes can enhance DHKE security.

---

## Further Reading / Resources

-   **"Cryptography and Network Security: Principles and Practice" by William Stallings:** Chapters on Number Theory, Public Key Cryptography, RSA, Diffie-Hellman, Key Management.
-   **"Understanding Cryptography" by Christof Paar and Jan Pelzl:** Sections on number theory, asymmetric cryptography, RSA, DLP, DHKE.
-   **RFCs:** Search for RFCs related to RSA (PKCS#1), TLS, Diffie-Hellman for protocol details.
-   **Online Number Theory Resources:** Khan Academy, Brilliant.org for basic concepts.
-   **RSA Laboratories Website:** Historical FAQs and technical notes.

## Concept Map Idea

*   **Central Node:** Asymmetric Key Cryptography
*   **Main Branches:**
    *   **Mathematical Foundations:**
        *   Number Theory -> Primes, Composites, Coprimes, gcd
        *   Primality -> Testing (Trial Div, Sieve), Infinitude
        *   Modular Arithmetic -> Congruence, Exponentiation
        *   Key Theorems -> $\phi(n)$, FLT, Euler's Thm -> Finding Inverses
        *   DLP (Hard Problem) -> Basis for DHKE
        *   Factoring (Hard Problem) -> Basis for RSA
        *   CRT -> Solving Congruences
    *   **Principles:**
        *   Key Pair (Public/Private)
        *   Operations -> Encrypt(PU), Decrypt(PR) (Confidentiality) | Encrypt(PR), Decrypt(PU) (Authentication/Signature)
        *   Requirements (Easy Gen/Enc/Dec, Hard Invert/Break)
    *   **RSA Algorithm:**
        *   Originators (Rivest, Shamir, Adleman)
        *   Key Generation (p, q, n, phi(n), e, d)
        *   Encryption ($C=M^e \pmod n$)
        *   Decryption ($M=C^d \pmod n$)
        *   Applications (List major ones)
        *   Advantages/Disadvantages
        *   Attacks -> Factoring, Timing, Padding issues (Short Msg), Common Modulus, Quantum
        *   Security Measures -> Key Length, Padding (OAEP/PSS), Implementation
    *   **Diffie-Hellman Key Exchange:**
        *   Purpose (Shared Secret Agreement)
        *   Basis (DLP difficulty)
        *   Algorithm (Global params q, alpha; Private X; Public Y; Shared K)
        *   MITM Attack -> Lack of Authentication
        *   Defenses -> Authentication (Certs, Shared Secret)
        *   Enhancements -> Safe Primes
    *   **Key Management:**
        *   Problem (Authentic Public Key Distribution)
        *   Approaches (Announcement, Directory, PKA, Certificates)
        *   PKI / CAs
