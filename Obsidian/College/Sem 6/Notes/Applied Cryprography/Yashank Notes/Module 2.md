
# Module 2: Symmetric Key Cryptography

## Module Overview

This module delves into the world of **Symmetric Key Cryptography**, where the same key is used for both encryption and decryption. We will explore the mathematical foundations necessary to understand modern ciphers, examine the components and principles of block ciphers, and take a deep dive into two significant standards: the historical Data Encryption Standard (DES) and the current Advanced Encryption Standard (AES).

**Topics Covered:**

*   **2.1 Mathematics of Symmetric Key Cryptography:**
    *   Algebraic Structures
    *   Group
    *   Ring
    *   Field
    *   Galois Fields (GF Fields)
*   **2.2 Modern Block Ciphers:**
    *   Components of Modern Block Ciphers
    *   Product Ciphers
    *   Diffusion and Confusion
    *   Classes of Product Ciphers
    *   **DES (Data Encryption Standard):**
        *   DES Structure
        *   DES Analysis: Properties, Design Criteria
        *   DES Strength and Weaknesses
        *   DES Security
        *   Multiple DES, 3DES
*   **2.3 AES (Advanced Encryption Standard):**
    *   AES Structure
    *   Transformations (SubBytes, ShiftRows, MixColumns, AddRoundKey)
    *   Key Expansion in AES-128, AES-192, and AES-256
    *   Key-Expansion Analysis
    *   Analysis of AES: Security, Implementation, Simplicity, and Cost

---

## 2.1 Mathematics of Symmetric Key Cryptography

### Introduction to Algebraic Structures

-   **Importance in Cryptography:** **Finite fields** and other number theory topics are increasingly crucial in modern cryptography. They form the mathematical bedrock for many algorithms.
    -   Examples: AES (Advanced Encryption Standard), Elliptic Curve Cryptography (ECC), IDEA (International Data Encryption Algorithm), Public Key Cryptosystems.
-   **Foundation:** We begin by exploring fundamental concepts from **abstract algebra**: groups, rings, and fields.
-   **Abstract Algebra:** This branch of mathematics deals with **sets** of elements (which can be numbers, polynomials, or other objects) and **operations** defined on these sets. It studies the properties of these operations and the structures they form.
    -   *Simplified:* Abstract algebra looks at collections of things and rules for combining them (like addition or multiplication), focusing on the underlying patterns and properties.

### Groups

-   **Definition:** A **group** is a fundamental algebraic structure consisting of:
    1.  A **set** of elements or "numbers", denoted as $G$.
    2.  A single **binary operation** (let's denote it generically as `.` which could be +, -, *, /, etc.) such that when the operation is applied to any two elements in the set, the result is also an element within the same set. This property is called **closure**.
-   **Notation:** A group is often denoted as $\{G, .\}$.
-   **Properties (Axioms):** For a set $G$ and operation `.` to form a group, the following conditions must be met:
    1.  **Closure:** For any two elements $a, b$ in $G$, the result $a . b$ must also be in $G$.
        -   *Explanation:* If you combine any two elements using the group's operation, you always stay within the set.
    2.  **Associativity:** For any elements $a, b, c$ in $G$, the equation $(a . b) . c = a . (b . c)$ must hold true.
        -   *Explanation:* The order in which you perform operations doesn't matter if the elements are in sequence. (e.g., (2+3)+4 = 2+(3+4)).
    3.  **Identity Element:** There must exist a unique element $e$ in $G$, called the **identity element**, such that for any element $a$ in $G$, $e . a = a . e = a$.
        -   *Explanation:* There's a special element that doesn't change other elements when combined with them (like 0 for addition or 1 for multiplication).
    4.  **Inverse Element:** For every element $a$ in $G$, there must exist a unique element $a^{-1}$ in $G$, called the **inverse** of $a$, such that $a . a^{-1} = a^{-1} . a = e$.
        -   *Explanation:* Every element has a counterpart that "undoes" it, resulting in the identity element (like -3 is the inverse of 3 for addition, or 1/5 is the inverse of 5 for multiplication).

#### Examples of Groups

-   **Integers under Addition:** The set of all integers ($\mathbb{Z}$) with the addition operation (+) forms a group, denoted as $(\mathbb{Z}, +)$.
    -   *Check:* Closure (integer + integer = integer), Associativity ((a+b)+c = a+(b+c)), Identity (0, since a+0=a), Inverse (for any integer a, -a is its inverse, a+(-a)=0).
-   **Real Numbers under Addition:** The set of all real numbers ($\mathbb{R}$) with the addition operation (+) forms a group, denoted as $(\mathbb{R}, +)$.
    -   *Check:* Properties hold similarly to integers.
-   **Non-Zero Real Numbers under Multiplication:** The set of all real numbers *excluding zero* ($\mathbb{R}^*$) with the multiplication operation ($\times$) forms a group, denoted as $(\mathbb{R}^*, \times)$.
    -   *Check:* Closure (non-zero real * non-zero real = non-zero real), Associativity ((a*b)*c = a*(b*c)), Identity (1, since a*1=a), Inverse (for any non-zero real a, 1/a is its inverse, a*(1/a)=1). *Zero must be excluded because it does not have a multiplicative inverse.*

#### Finite and Infinite Groups

-   **Finite Group:** A group that contains a finite number of elements.
    -   The **order** of a finite group is the number of elements it contains.
-   **Infinite Group:** A group that contains an infinite number of elements.
    -   Infinite groups do not have an "order" in the same sense as finite groups.
    -   Examples: $(\mathbb{Z}, +)$ and $(\mathbb{R}, +)$ are infinite groups. Groups used in cryptography (like those based on modular arithmetic) are often finite.

#### Abelian Group (Commutative Group)

-   **Definition:** An **Abelian group** (named after Niels Henrik Abel) is a group that satisfies all the standard group conditions *plus* one additional condition:
    -   **Commutativity:** For any two elements $a, b$ in the group $G$, the equation $a . b = b . a$ must hold true.
-   *Explanation:* The order in which you combine two elements doesn't affect the result (e.g., 3+5 = 5+3). Not all groups have this property (e.g., matrix multiplication is generally not commutative).
-   **Example:** The additive group of real numbers, $(\mathbb{R}, +)$, is an Abelian group because $a + b = b + a$ for all real numbers $a, b$. All the examples listed previously are Abelian groups.

#### Cyclic Group

-   **Exponentiation:** In the context of groups, **exponentiation** refers to the repeated application of the group's operation on an element with itself.
    -   If the operation is addition, "exponentiation" corresponds to multiplication (e.g., $a^3 = a+a+a$).
    -   If the operation is multiplication, exponentiation is standard power (e.g., $a^3 = a \times a \times a$).
-   **Identity Definition:** The identity element $e$ can be defined as any element $a$ raised to the power of 0: $e = a^0$.
-   **Inverse Definition:** The inverse of an element $a^n$ can be defined as $a^{-n}$. If $a'$ is the inverse of $a$, then $a^{-n} = (a')^n$.
-   **Definition of Cyclic Group:** A group $G$ is called **cyclic** if every element $b$ in $G$ can be expressed as a power ($a^k$) of a *single fixed element* $a$ within the group.
    -   $b = a^k$ for some integer $k$.
-   **Generator:** The fixed element $a$ whose powers generate all elements of the group is called a **generator** of the group. A cyclic group can have more than one generator.
-   **Property:** Every **cyclic group is always an Abelian group**.
    -   *Reason:* Since all elements are powers of a single generator $a$, say $a^m$ and $a^n$, their combination is $a^m . a^n = a^{m+n} = a^{n+m} = a^n . a^m$.
-   **Relevance:** Cyclic groups are extremely important in cryptography, particularly in Diffie-Hellman key exchange and Elliptic Curve Cryptography, where finding discrete logarithms (the exponent $k$) in large cyclic groups is computationally difficult.

### Rings

-   **Definition:** A **ring** is an algebraic structure consisting of:
    1.  A set of elements or "numbers", denoted as $R$.
    2.  **Two binary operations**, typically **addition (+)** and **multiplication (⋅)**.
-   **Properties (Axioms):** For a set $R$ with operations + and ⋅ to be a ring, it must satisfy the following:
    1.  **(R, +) is an Abelian Group:** The set $R$ under the addition operation must form an Abelian group. This means addition must satisfy:
        -   **Closure under addition:** $a + b \in R$.
        -   **Associativity of addition:** $(a + b) + c = a + (b + c)$.
        -   **Additive identity:** There exists an element $0 \in R$ such that $a + 0 = 0 + a = a$.
        -   **Additive inverse:** For every $a \in R$, there exists $-a \in R$ such that $a + (-a) = 0$.
        -   **Commutativity of addition:** $a + b = b + a$.
    2.  **Multiplication Properties:** The multiplication operation (⋅) must satisfy:
        -   **Closure under multiplication:** For all $a, b \in R$, $a ⋅ b \in R$.
        -   **Associativity of multiplication:** $(a ⋅ b) ⋅ c = a ⋅ (b ⋅ c)$ for all $a, b, c \in R$.
    3.  **Distributive Property:** Multiplication must distribute over addition:
        -   **Left distributivity:** $a ⋅ (b + c) = (a ⋅ b) + (a ⋅ c)$ for all $a, b, c \in R$.
        -   **Right distributivity:** $(a + b) ⋅ c = (a ⋅ c) + (b ⋅ c)$ for all $a, b, c \in R$.

-   *Simplified View:* A ring is a set where you can always add, subtract (due to additive inverses), and multiply, and these operations behave nicely together (associativity, distributivity). Division is not guaranteed.

#### Ring Variations

-   **Commutative Ring:** A ring where the multiplication operation is also commutative (i.e., $a ⋅ b = b ⋅ a$ for all $a, b \in R$).
    -   *Example:* The integers $(\mathbb{Z}, +, ⋅)$ form a commutative ring.
-   **Ring with Unity:** A ring that has a **multiplicative identity** element (usually denoted by 1), such that $a ⋅ 1 = 1 ⋅ a = a$ for all $a \in R$.
    -   *Example:* The integers $(\mathbb{Z}, +, ⋅)$ form a ring with unity (the unity is 1).
-   **Integral Domain:** A **commutative ring with unity** that has an additional property: **no zero divisors**.
    -   **No Zero Divisors:** For any two elements $a, b$ in the ring, if $a ⋅ b = 0$, then either $a = 0$ or $b = 0$ (or both).
    -   *Explanation:* You cannot multiply two non-zero elements and get zero. This property holds for integers but might not hold in other rings (e.g., modular arithmetic rings like $\mathbb{Z}_6$, where $2 \times 3 = 0 \pmod 6$).
    -   It also requires the existence of the multiplicative identity element 1, where $a \cdot 1 = 1 \cdot a = a$.

#### Examples of Rings

-   **Integers:** The set of integers $\mathbb{Z}$ under standard addition and multiplication $(\mathbb{Z}, +, ⋅)$ is a **commutative ring with unity**. Since it also has no zero divisors, it is an **integral domain**.
-   **Polynomials:** The set of polynomials with real coefficients, denoted $R[x]$, forms a **commutative ring with unity** under the usual addition and multiplication of polynomials.

### Fields

-   **Definition:** A **field** is an algebraic structure consisting of:
    1.  A set of elements, denoted as $F$.
    2.  **Two binary operations**, typically **addition (+)** and **multiplication (⋅)**.
-   **Properties (Axioms):** A field must satisfy all the axioms of an **integral domain** (commutative ring with unity and no zero divisors), plus one additional axiom:
    1.  **(F, +) is an Abelian Group:** (Closure, Associativity, Additive Identity 0, Additive Inverse, Commutativity of +).
    2.  **(F \ {0}, ⋅) is an Abelian Group:** The set of elements *excluding the additive identity (0)* must form an Abelian group under multiplication. This means multiplication (for non-zero elements) must satisfy:
        -   **Closure under multiplication:** $a ⋅ b \in F$ (and if $a,b \neq 0$, then $a \cdot b \neq 0$).
        -   **Associativity of multiplication:** $(a ⋅ b) ⋅ c = a ⋅ (b ⋅ c)$.
        -   **Multiplicative identity:** There exists an element $1 \in F$ (where $1 \neq 0$) such that $a ⋅ 1 = 1 ⋅ a = a$.
        -   **Multiplicative inverse:** For every element $a \in F$ *except* 0, there exists a multiplicative inverse $a^{-1} \in F$ such that $a ⋅ a^{-1} = a^{-1} ⋅ a = 1$.
        -   **Commutativity of multiplication:** $a ⋅ b = b ⋅ a$.
    3.  **Distributive Property:** Multiplication distributes over addition ($a ⋅ (b + c) = (a ⋅ b) + (a ⋅ c)$).

-   *Simplified View:* A field is a set where you can always add, subtract, multiply, and **divide** (by any non-zero element), and these operations interact as expected (associativity, commutativity, distributivity). Fields provide the richest structure among these three.

#### Field Properties (Summary)

-   A field satisfies all preceding axioms (it's an integral domain).
-   It adds the requirement of **multiplicative inverses** for all non-zero elements.
-   Effectively, a field is a set where addition, subtraction, multiplication, and division (excluding division by zero) are well-defined and follow familiar rules.
-   **Division Definition:** Division $a / b$ is formally defined as multiplication by the inverse: $a / b = a ⋅ (b^{-1})$.
-   **Familiar Examples:** Rational numbers ($\mathbb{Q}$), real numbers ($\mathbb{R}$), and complex numbers ($\mathbb{C}$) all form fields under standard addition and multiplication.

#### Finite Fields (Galois Fields)

-   Fields can be infinite (like $\mathbb{Q}, \mathbb{R}, \mathbb{C}$) or **finite**.
-   **Finite Fields**, also called **Galois Fields** (GF), are fields containing a finite number of elements.
-   They are denoted as $GF(p^n)$, where $p$ is a prime number (the characteristic) and $n$ is a positive integer. The field has $p^n$ elements.
-   **Crucial for Cryptography:** Finite fields, especially $GF(2^n)$ (fields based on binary operations), are fundamental to algorithms like AES, ECC, and various error-correcting codes. Arithmetic within these fields (addition, multiplication, finding inverses) forms the core of many cryptographic operations.

### Summary Table: Group vs. Ring vs. Field

| Basis                   | Group                                     | Ring                                                    | Field                                                         |
| :---------------------- | :---------------------------------------- | :------------------------------------------------------ | :------------------------------------------------------------ |
| **Operations**          | One (Addition or Multiplication)          | Two (Addition and Multiplication)                       | Two (Addition and Multiplication)                           |
| **Inverse (Mult.)**     | Not Required (except specific element)    | Not Required                                            | Required for all non-zero elements                           |
| **Distributive Law**    | Not Needed                                | Required (Multiplication distributes over Addition)     | Required (just like in rings)                               |
| **Commutativity**       | Only for some groups (Abelian)            | Only required for Addition (Commutative Ring if Mult. too) | Required for Both Addition and Multiplication (by definition) |
| **Example**             | Integers under addition $(\mathbb{Z}, +)$ | Integers with addition and multiplication $(\mathbb{Z}, +, \cdot)$ | Rational numbers with addition and multiplication $(\mathbb{Q}, +, \cdot)$ |

### Section Summary: Algebraic Structures

-   **Groups:** Set + 1 operation (Closure, Associativity, Identity, Inverse). Abelian if commutative. Cyclic if generated by one element.
-   **Rings:** Set + 2 operations (+, ⋅). Forms Abelian group under +. Multiplication is associative and closed. Multiplication distributes over addition. Commutative Ring if ⋅ is commutative. Ring with Unity if ⋅ has identity. Integral Domain if commutative, has unity, and no zero divisors.
-   **Fields:** Set + 2 operations (+, ⋅). Forms Abelian group under +. Non-zero elements form Abelian group under ⋅ (includes multiplicative inverse). Multiplication distributes over addition. Allows Add, Subtract, Multiply, Divide (by non-zero).
-   **Relevance:** These structures define the mathematical environments where cryptographic operations take place. Finite Fields (Galois Fields) are particularly vital for modern symmetric ciphers like AES.

---

## 2.2 Modern Block Ciphers

### Introduction

-   **Block Cipher:** A type of symmetric encryption algorithm that operates on fixed-size chunks (**blocks**) of data (plaintext).
    -   The data is divided into blocks (e.g., 64 bits for DES, 128 bits for AES).
    -   Each block is encrypted individually.
-   **Contrast with Stream Ciphers:** **Stream ciphers** process data continuously, typically bit by bit or byte by byte. They often use a pseudorandom keystream XORed with the plaintext.
-   **Security Principles:** Modern block ciphers rely heavily on two essential properties, introduced by Claude Shannon, to ensure security against attacks:
    1.  **Confusion:** Making the relationship between the ciphertext and the **key** as complex and involved as possible.
        -   *Goal:* Obscure the connection between the key and the resulting ciphertext. Even if an attacker has many plaintext-ciphertext pairs encrypted with the same key, they shouldn't be able to deduce the key easily.
        -   *Achieved by:* **Substitution** operations (like S-boxes).
    2.  **Diffusion:** Spreading the influence of a single plaintext bit (or key bit) over many ciphertext bits.
        -   *Goal:* Ensure that changes in one part of the plaintext affect many parts of the ciphertext, and vice versa. This hides statistical patterns in the plaintext. Flipping one bit of the plaintext should ideally change roughly half the bits of the ciphertext (Avalanche Effect).
        -   *Achieved by:* **Permutation** or **transposition** operations (like P-boxes or linear mixing layers).

### Data Encryption Standard (DES)

-   **Historical Context:** DES was a foundational algorithm in the history of block cipher design, developed in the 1970s.
-   **Vulnerability:** Over time, due to increases in computational power and advances in cryptanalysis, DES (with its relatively short 56-bit key) became vulnerable to brute-force attacks (trying all possible keys).
-   **Successor:** To address these limitations, modern block ciphers like the **Advanced Encryption Standard (AES)** were introduced.
-   **Benefits of Modern Ciphers:** AES and similar algorithms provide significantly **stronger security** (longer keys, more robust design) and often **better performance** on contemporary hardware.

### Components of Modern Block Ciphers

Modern block ciphers, including DES and AES, are typically built using several core components combined in rounds.

#### S-Box (Substitution Box)

-   **Function:** An **S-Box** takes a small block of input bits and **substitutes** it with a different block of output bits.
-   **Mechanism:** This substitution is defined by a fixed **lookup table**. The table maps every possible input value to a unique output value.
-   **Purpose:** The primary goal of the S-Box is to introduce **confusion**. It creates a **non-linear** relationship between the input and output, making the cipher resistant to linear cryptanalysis.
-   **Design:**
    -   S-Boxes are carefully predefined by the algorithm designers.
    -   They are standardized to ensure consistent and secure encryption.
    -   A well-designed S-Box exhibits the **avalanche effect** at a small scale: changing a single input bit should significantly change the output bits in an unpredictable way.
-   **Simple Example:**
    ![[Pasted image 20250506012549.png]]
    This image shows a simple 2-bit input to 2-bit output S-Box lookup table:*
        - *Input 00 -> Output 11*
        - *Input 01 -> Output 10*
        - *Input 10 -> Output 01*
        - *Input 11 -> Output 00*
    *This table illustrates how a 2-bit input is non-linearly transformed into a 2-bit output.*

-   **Role in Encryption:**
    -   Introduces **confusion**, obscuring the key-ciphertext relationship.
    -   Makes it difficult for attackers to deduce the key by analyzing ciphertext alone.
    -   Modern ciphers use multiple S-Boxes across multiple rounds, often combined with other transformations (like permutations/diffusion), to build strong encryption.
    -   This layering makes reversing the encryption process without the key extremely hard.

#### P-Box (Permutation Box)

-   **Function:** A **P-Box** **shuffles** or rearranges the positions of the input bits *without changing their actual values* (0s remain 0s, 1s remain 1s).
-   **Mechanism:** This rearrangement is known as **permutation** and follows a predefined pattern or table that maps input positions to output positions.
-   **Purpose:** The primary goal of the P-Box is to introduce **diffusion**.
-   **Design:**
    -   Like S-Boxes, P-Boxes are predefined by the algorithm designers and standardized.
    -   While S-Boxes change bit *values* (substitution), P-Boxes only change bit *positions* (permutation/transposition).
-   **Simple Example:**
    <!-- Instruct user to paste the table image from page 23 here -->
![[Pasted image 20250506012643.png]] 
This image shows an 8-bit permutation:*
        - *Input position 1 -> Output position 4*
        - *Input position 2 -> Output position 2*
        - *Input position 3 -> Output position 6*
        - *... and so on.*
    
This table shows how bit positions are reordered. For example, the bit originally at position 1 moves to position 4, the bit at position 2 stays at position 2, etc.

-   **Role in Encryption:**
    -   Introduces **diffusion**, spreading the influence of individual plaintext bits across the entire block.
    -   Makes it difficult for attackers to find patterns or exploit statistical weaknesses by ensuring that changes in the input propagate widely in the output.
    -   Modern ciphers often use multiple P-Boxes in conjunction with S-Boxes over several rounds. This combination of substitution (confusion) and permutation (diffusion) makes the overall encryption highly secure and resistant to cryptanalysis.

#### XOR Operation

-   **Function:** The **XOR** (Exclusive OR) operation is a bitwise logical operation. $A \oplus B$ is true (1) if and only if $A$ and $B$ are different.
    -   $0 \oplus 0 = 0$
    -   $0 \oplus 1 = 1$
    -   $1 \oplus 0 = 1$
    -   $1 \oplus 1 = 0$
-   **Key Property: Reversibility:** XOR is crucial in cryptography because it's easily reversible *using the same key*.
    -   If $C = P \oplus K$ (Encryption: Plaintext $P$ XORed with Key $K$ gives Ciphertext $C$)
    -   Then $P = C \oplus K$ (Decryption: Ciphertext $C$ XORed with the same Key $K$ gives back Plaintext $P$)
    -   This works because $P \oplus K \oplus K = P \oplus (K \oplus K) = P \oplus 0 = P$.
-   **Role in Encryption:**
    -   Used extensively for combining data blocks with keys (e.g., in the Feistel structure, AES AddRoundKey).
    -   Its reversibility allows the same structure to be used for both encryption and decryption (with keys applied in reverse order).
    -   Used repeatedly in various stages to ensure that changes in plaintext or key result in unpredictable ciphertext changes, enhancing security (contributing to both confusion and diffusion indirectly).

#### Circular Shift (Rotation)

-   **Function:** A **Circular Shift** (also known as **rotation**) rearranges bits within a block or word by moving them to the left or right.
-   **Mechanism:** Unlike a standard logical/arithmetic shift where bits shifted off one end are lost and zeros are introduced at the other end, a circular shift **wraps** the bits around. Bits shifted off one end reappear at the opposite end, creating a continuous loop.
    -   *Example (Left Shift):* `1101` circularly shifted left by 1 becomes `1011`.
    -   *Example (Right Shift):* `1101` circularly shifted right by 1 becomes `1110`.
-   **Role in Encryption:**
    -   Primarily used to enhance **diffusion**.
    -   Often applied within the **key scheduling algorithm** (e.g., in DES and AES) to generate different round keys from the initial key. By shifting parts of the key differently for each round, it ensures round keys are distinct and complex.
    -   Also used in some cipher operations themselves (e.g., AES ShiftRows involves shifting bytes within rows, contributing to diffusion).
    -   Obscures the relationship between plaintext and ciphertext by ensuring bits from different parts of the key influence different parts of the data transformation in each round.
    -   Applied in multiple rounds for extensive data transformation and enhanced security.

### Product Cipher

-   **Definition:** A **Product Cipher** is an encryption technique that combines **multiple** simpler cryptographic transformations (like substitution and permutation) in sequence to create a stronger, more secure cipher.
-   **Rationale:** By layering different types of operations, the complexity of the overall encryption process increases significantly, making it much more resistant to cryptanalytic attacks than any single component transformation would be on its own.
    -   Think of it like using multiple locks on a door, each requiring a different key or mechanism.
-   **Typical Structure:** Usually involves applying a series of **substitutions** (S-Boxes for confusion) and **permutations** (P-Boxes/Shifts/Mixing for diffusion) in alternating rounds.
-   **Goal:** To effectively obscure the statistical relationship between the plaintext and the ciphertext by leveraging both confusion and diffusion repeatedly. Most modern block ciphers (DES, AES) are product ciphers.

### Feistel Cipher (Feistel Network)

-   **Definition:** The **Feistel cipher** (named after IBM cryptographer Horst Feistel) is a specific structure or design strategy used in many symmetric **block ciphers**. DES is a classic example.
-   **Key Idea:** Breaks the encryption process into multiple **rounds**. Each round uses a **round key** derived from the main key.
-   **Advantages:**
    -   **Efficiency:** The core "round function" doesn't need to be invertible itself.
    -   **Versatility:** The same algorithm (hardware or software) can be used for both **encryption and decryption**, simply by applying the round keys in the reverse order for decryption. This is a major practical advantage.
-   **How it Works (Conceptual):**
    1.  The plaintext block is split into two equal halves (usually Left $L_0$ and Right $R_0$).
    2.  The encryption process involves multiple rounds ($n$ rounds).
    3.  In each round $i$ (from 1 to $n$):
        -   A **round function** $F$ takes the *right half* ($R_{i-1}$) and the *round key* ($K_i$) as input: $F(R_{i-1}, K_i)$.
        -   The output of the round function is **XORed** with the *left half* ($L_{i-1}$). This result becomes the new right half ($R_i$).
        -   The *original right half* ($R_{i-1}$) becomes the new left half ($L_i$).
        -   Mathematically:
            -   $L_i = R_{i-1}$
            -   $R_i = L_{i-1} \oplus F(R_{i-1}, K_i)$
    4.  **Swapping:** The halves $L_i$ and $R_i$ are passed to the next round. After the final round, a final swap of the left and right halves is often performed (though this depends on the specific cipher design).
    5.  The combined $L_n$ and $R_n$ (after the potential final swap) form the ciphertext block.

-   **Steps in Feistel Cipher (Detailed):**
    1.  **Input:** Plaintext block split into $L_0$ and $R_0$.
    2.  **Round Function ($F$):** In each round $i$, the function $F$ processes $R_{i-1}$ and the round key $K_i$. This function often involves S-Boxes and P-Boxes itself to provide confusion and diffusion within the round.
    3.  **XOR Operation:** The output $F(R_{i-1}, K_i)$ is XORed with $L_{i-1}$.
    4.  **Swapping:** The roles of the halves are swapped: $L_i = R_{i-1}$ and $R_i = L_{i-1} \oplus F(R_{i-1}, K_i)$.
    5.  **Repetition:** This process (steps 2-4) is repeated for a specified number of rounds (e.g., 16 rounds in DES).
    6.  **Final Output:** After the last round, the resulting $L_n$ and $R_n$ are combined to produce the final ciphertext block (potentially with a final swap).

-   **Diagram Reference:**
![[Pasted image 20250506012911.png]]

 This diagram visually illustrates the flow described above:
        - *Shows the plaintext block split into L and R.*
        - *Depicts multiple rounds (Round 1, Round 2, ... Round n).*
        - *In each round, it shows the right half feeding into the F function along with the round key (K1, K2, ... Kn).*
        - *Shows the output of F being XORed with the left half.*
        - *Illustrates the swapping of halves between rounds.*
        - *Shows the final combination into the ciphertext block.*
    *This diagram is crucial for understanding the data flow and the repeated application of the round structure.*

### Data Encryption Standard (DES) - Deeper Dive

-   **Type:** **Symmetric key-block cipher**. Uses the same key for encryption and decryption.
-   **Origin:** Published by **NIST** (National Institute of Standards and Technology) in 1977. Based on IBM's Lucifer cipher, modified by the NSA.
-   **Structure:**
    -   **Block Cipher:** Operates on 64-bit blocks of plaintext.
    -   **Key Size:** Uses a 64-bit key, but only **56 bits** are effectively used for encryption; 8 bits are parity bits and are typically discarded.
![[Pasted image 20250506013042.png]]This image shows a table of numbers 1-64, highlighting positions 8, 16, 24, 32, 40, 48, 56, 64. this illustrates that the bits in these positions of the initial 64-bit key are used for parity checking and are dropped before the key scheduling process begins, resulting in the effective 56-bit key.

-   **Rounds:** Uses **16 rounds**, and each round follows the **Feistel structure**.
-   **Popularity:** Became widely used for secure data transmission for many years (e.g., in finance).
-   **Security Concerns:**
    -   As noted before, advances in computing power made the **56-bit key length vulnerable** to brute-force attacks.
    -   Largely **replaced by stronger algorithms like AES**.
    -   However, understanding DES is important for learning cryptographic history and principles.
-   **Core Principles:** DES is based on the fundamental cryptographic attributes:
    -   **Substitution** (Confusion): Primarily achieved through S-boxes within the Feistel round function.
    -   **Transposition** (Diffusion): Achieved through P-boxes (permutations) within the round function and the initial/final permutations.
-   **Overall DES Process:**
    1.  **Initial Permutation (IP):** The 64-bit plaintext block undergoes an initial, fixed permutation (shuffling of bit positions). This has no cryptographic benefit but was likely for hardware implementation ease.
![[Pasted image 20250506013236.png]]This table shows how the initial 64 bits are rearranged. For example, bit 58 of the input becomes bit 1 of the output, bit 50 becomes bit 2, and so on. 

![[Pasted image 20250506013318.png]] This shows the 8x8 input block mapping to the permuted 8x8 output block, reinforcing the concept shown in the table on page 39.
    2.  **Splitting:** The 64-bit permuted block is split into two 32-bit halves: Left Plain Text (LPT) and Right Plain Text (RPT). (These are $L_0$ and $R_0$).
    3.  **16 Rounds:** Each LPT and RPT pair goes through 16 rounds of Feistel encryption. Each round uses a unique 48-bit **round key** derived from the original 56-bit key.
    4.  **Rejoining & Final Permutation (FP):** After 16 rounds, the final LPT ($L_{16}$) and RPT ($R_{16}$) are rejoined. This combined 64-bit block undergoes a **Final Permutation (FP)**, which is the *inverse* of the Initial Permutation (IP).
    5.  **Output:** The result of the FP is the 64-bit ciphertext block.

-   **Broad Level Steps Diagram:**
![[Pasted image 20250506013417.png]] This flowchart clearly shows:
        - *Input: 64-bit Plain Text*
        - *Step 1: Initial Permutation (IP)*
        - *Step 2: Splitting into Left Plain Text (LPT) and Right Plain Text (RPT)*
        - *Step 3: 16 Rounds applied to both halves, using the Key*
        - *Step 4: Rejoining LPT and RPT*
        - *Step 5: Final Permutation (FP)*
        - *Output: 64-bit Cipher Text*
    *This provides a high-level overview before diving into the round details.*

-   **Inside a DES Round (The Mangler Function F):**
    ![[Pasted image 20250506013439.png]]
    (shows Key transformation -> Expansion -> S-box -> P-box -> XOR and Swap). Explain this shows the sequence of operations within the Feistel round function F, applied to the Right Half (RPT).*

    ![[Pasted image 20250506013505.png]]This is a more detailed view of a single Feistel round, showing:
        - *Input halves: Left Half (L i-1) and Right Half (R i-1).*
        - *The "Mangler Function" (brown box) operating on R i-1.*
        - *Inside the Mangler Function: Expansion Permutation (E), Keyed Substitution (S-Boxes), Transposition (P-Box).*
        - *Round Key i being XORed after Expansion (details vary, this diagram might simplify).*
        - *Output of Mangler Function XORed with L i-1 to produce R i.*
        - *R i-1 becoming L i.*
        - *Also shows the parallel key scheduling process generating Round Key i.*
    *This diagram clarifies how the RPT is processed and combined with the LPT.
    
    ![[Pasted image 20250506013526.png]] 
    ($L_i = R_{i-1}$, $R_i = L_{i-1} \oplus F(R_{i-1}, K_i)$).  these two equations mathematically define the core operation of a Feistel round.*

    The core steps within the round function $F(R_{i-1}, K_i)$:
    1.  **Expansion Permutation (E):** The 32-bit RPT ($R_{i-1}$) is expanded to 48 bits using an **Expansion P-box (E)**. This permutation repeats some bits to increase diffusion and match the size of the round key.
        ![[Pasted image 20250506013633.png]]the internal F-function diagram (Expansion E -> XOR with K -> S-Boxes -> Permutation P). This zooms into the Mangler function.*
        
        ![[Pasted image 20250506013706.png]]
        this table defines how the 32 input bits are expanded and permuted to 48 bits. For example, bit 32 of the input becomes bit 1 of the output, bit 1 becomes bit 2, etc., with some input bits being used in multiple output positions.*
        
    2.  **Key Mixing:** The 48-bit expanded block is **XORed** with the 48-bit **Round Key ($K_i$)**.
    3.  **Substitution (S-Boxes):** The 48-bit result is divided into eight 6-bit chunks. Each 6-bit chunk goes into a specific **S-box** (S1 to S8). Each S-box takes 6 bits as input and produces a 4-bit output using a fixed lookup table. This is the main source of confusion and non-linearity.
        ![[Pasted image 20250506013816.png]] the 6 input bits are used: the outer 2 bits select the row, and the inner 4 bits select the column. The 4-bit value at the intersection is the output. Provide the example shown: S1(101010) -> row 10 (binary 2), column 0101 (binary 5) -> value 6 (output 0110).
        
    4.  **Permutation (P-Box):** The eight 4-bit outputs from the S-boxes are combined into a 32-bit block. This block is then permuted using a fixed **P-box**. This step increases diffusion.
        ![[Pasted image 20250506013849.png]] this table shuffles the 32 bits coming out of the S-boxes.
    5.  **Output:** The final 32-bit output of the P-box is the result of the round function $F$. This result is then XORed with the LPT ($L_{i-1}$) to produce the new RPT ($R_i$).

-   **DES Key Scheduling:** The process of generating the 16 unique 48-bit round keys ($K_1$ to $K_{16}$) from the initial 56-bit key.
    ![[Pasted image 20250506013923.png]] 
    This shows the 64-bit key undergoing Permuted Choice 1 (PC-1) to get 56 bits, split into C0 and D0 (28 bits each). Then, for each round, C and D are left-shifted, combined, and put through Permuted Choice 2 (PC-2) to select 48 bits for the round key.
    
    ![[Pasted image 20250506013950.png]]This provides a slightly different view, emphasizing the dropping of parity bits (8, 16, ... 64) and showing the PC-1, left circular shifts, and PC-2 steps.
    
    ![[Pasted image 20250506014030.png]]This diagram clearly shows:*
        - *Input: 64-bit key with parity bits.*
        - *Step 1: Parity drop (using PC-1, implicitly) resulting in 56-bit Cipher Key.*
        - *Step 2: Splitting into two 28-bit halves (C0, D0).*
        - *Step 3 (Loop for 16 rounds):*
            - *Circular Left Shift applied to C and D (by 1 or 2 bits depending on the round).*
            - *Combine shifted C and D.*
            - *Compression P-box (PC-2) selects 48 bits to form the Round Key (K1 to K16).*
    *This is the most complete diagram of the key schedule.*

    1.  **Permuted Choice 1 (PC-1):** The initial 64-bit key has its 8 parity bits discarded, and the remaining 56 bits are permuted according to PC-1.
        ![[Pasted image 20250506014110.png]] table defines the permutation and selection of the 56 effective key bits from the original 64 bits.*
    2.  **Splitting:** The 56-bit result is split into two 28-bit halves, $C_0$ and $D_0$.
    3.  **Circular Left Shifts:** For each of the 16 rounds, $C_{i-1}$ and $D_{i-1}$ are independently shifted left circularly by either one or two positions to produce $C_i$ and $D_i$. The number of shifts depends on the round number (1 bit for rounds 1, 2, 9, 16; 2 bits for all others).
        ![[Pasted image 20250506014132.png]]this table specifies whether to shift by 1 or 2 positions in each of the 16 rounds. number of key bits shifted per round). 
    4.  **Permuted Choice 2 (PC-2 / Compression P-box):** The combined 56 bits ($C_i D_i$) are permuted, and 48 bits are selected according to PC-2 to form the 48-bit round key $K_i$.
        ![[Pasted image 20250506014223.png]]this table defines which 48 of the 56 bits (after shifting) are selected and permuted to form the round key.
        ![[Pasted image 20250506014248.png]](Figure - compression permutation). 

    -   **Key Transformation Summary:**
        ![[Pasted image 20250506014334.png]]
        This lists key parameters:
            - *Type: Symmetric Block Cipher (aka Data Encryption Algorithm)*
            - *Adopted: NIST 1977*
            - *Superseded by: AES in 2001*
            - *Input/Output Block Size: 64 bits*
            - *Main Key Size: 64 bits (nominal)*
            - *Subkey (Effective Key): 56 bits*
            - *Round key: 48 bits*
            - *Number of rounds: 16 rounds*
        *This provides a quick reference for DES parameters.*

-   **DES Properties:**
    -   **Avalanche Effect:** A small change in the plaintext or the key should create a significant, unpredictable change in the ciphertext. DES is considered strong regarding this property. Flipping one input bit should, on average, flip about half the output bits after all rounds.
        ![[Pasted image 20250506014357.png]] This shows:
            - *Plaintext 1: 0000...0000, Key: 2223...BB23 -> Ciphertext 1: 4789...A5F1*
            - *Plaintext 2: 0000...0001 (one bit flipped), Key: 2223...BB23 -> Ciphertext 2: 0A4E...FEA3*
        changing just the last bit of the plaintext results in a completely different ciphertext, demonstrating the avalanche effect.*
    -   **Completeness Effect:** Each bit of the ciphertext should depend on many bits of the plaintext (and key). The combination of P-boxes (diffusion) and S-boxes (confusion) in DES provides a very strong completeness effect.

-   **Cryptanalysis of DES:**
    -   **Cryptanalysis:** The study of methods to break cryptographic systems, i.e., decrypt messages without knowing the secret key. The goal is to find weaknesses or vulnerabilities.
    -   **Differential Cryptanalysis:** Exploits how differences in plaintext input pairs propagate through the cipher rounds. By analyzing the probability of certain output differences occurring based on chosen input differences, attackers can deduce information about the key.
        -   **Steps:**
            1.  Choose Plaintext Pairs: Select pairs differing by a specific pattern (e.g., one bit flipped).
            2.  Encrypt Plaintexts: Encrypt both using the unknown key.
            3.  Analyze Differences: Analyze the resulting ciphertext differences, looking for statistically likely patterns ("differentials").
            4.  Guess Part of Key: These patterns can reveal information about the last round key bits.
            5.  Iterate: Repeat with many pairs to recover the full key.
    -   **Linear Cryptanalysis:** Finds linear approximations (equations involving XOR sums) relating plaintext bits, ciphertext bits, and key bits that hold with a probability slightly different from 1/2.
        -   **Steps:**
            1.  Collect Pairs: Gather many known plaintext-ciphertext pairs encrypted with the same key.
            2.  Analyze Data: Search for effective linear approximation equations for the cipher's S-boxes and overall structure.
            3.  Create Equations: Combine approximations for rounds into an overall linear equation for the cipher.
            4.  Count Occurrences: Test how often the linear equation holds true for the collected data. If it holds significantly more or less than 50% of the time, it provides a statistical bias.
            5.  Guess Key Bits: This bias can be exploited to guess certain key bits involved in the linear approximation. Iterate to find the full key.
    -   *Note:* While DES was designed to resist these attacks reasonably well (especially differential cryptanalysis), they are much more effective than brute-force for reduced-round versions. The 16 rounds provide significant protection, but the short key length remains the primary practical weakness.

-   **DES Weaknesses:**
    1.  **Cipher Design Weaknesses:**
        -   **S-Boxes:**
            -   *S-Box 4 Property:* Output bits 1, 2, 3 can be derived from output bit 0 by complementing certain input bits (a linearity property).
            -   *Input Collisions:* Some pairs of inputs to an S-box array can produce the same output.
            -   *Neighboring S-boxes:* Possible to get the same output in a round by changing bits affecting only three adjacent S-boxes.
        -   **P-Boxes:**
            -   *Initial/Final Permutations (IP/FP):* Offer no security benefit; purely implementational.
            -   *Expansion Permutation (E):* Repeats the first and fourth bits of every 4-bit input series, creating some redundancy.
    2.  **Cipher Key Weaknesses:**
        -   **Key Size (56 bits):** The most serious weakness. Makes DES vulnerable to **brute-force attacks** with modern hardware.
            -   $2^{56}$ possible keys.
            -   Checking 1 million keys/sec => $2^{56} / 10^6 \approx 7.2 \times 10^7$ seconds $\approx$ 830 days (single processor).
            -   Parallel Processing: A machine with 1 million chips could test the key space in approx. 20 hours.
            -   Distributed Computing: In 1997, 3500 internet-connected computers found a challenged key in 120 days. A larger network (42,000) could potentially do it in 10 days. Dedicated hardware (like EFF's Deep Crack in 1998) broke DES in days.
        -   **Weak Keys:** A small set of keys (4 out of $2^{56}$) that have a specific property making them insecure.
            -   **Definition:** A key is **weak** if, after the initial parity drop (PC-1), the key consists of all 0s, all 1s, or has identical 28-bit halves ($C_0 = D_0$ which are all 0s or all 1s). This results in the same round key being generated for all 16 rounds ($K_1 = K_2 = ... = K_{16}$).
            ![[Pasted image 20250506014429.png]]This shows the four 64-bit keys (before parity drop) and the corresponding 56-bit actual keys (all 0s, all Fs, alternating 0s/Fs halves).
            -   **Disadvantage:** Encryption is **self-inverse**. Encrypting plaintext $P$ twice with a weak key $K_W$ returns the original plaintext: $E_{K_W}(E_{K_W}(P)) = P$.
            ![[Pasted image 20250506014455.png]]This shows Plaintext -> DES(Kw) -> Intermediate -> DES(Kw) -> Plaintext. Explain that this illustrates the self-inverse property. An attacker intercepting ciphertext C can try encrypting C with each weak key; if $E_{K_W}(C) = C$, they might have found the key (though this check isn't quite right - they should *decrypt* C twice, or encrypt P twice). The text below the diagram clarifies: try decrypting twice; if the result is the original ciphertext, the weak key is found. Weak keys should be avoided.
        -   **Semi-Weak Keys:** Pairs of keys (6 pairs, so 12 keys total) where encrypting with one key ($K_1$) and then encrypting the result with the other key ($K_2$) returns the original plaintext: $E_{K_2}(E_{K_1}(P)) = P$.
            -   **Property:** Each semi-weak key generates only **two** distinct round keys, each repeated eight times throughout the 16 rounds. The round keys generated by one key in the pair are the same as those generated by the other, but in a different order.
            ![[Pasted image 20250506014519.png]]This lists the 6 pairs of keys.
            
            ![[Pasted image 20250506014533.png]] the round key generation example for a semi-weak key pair. This table shows that only two round key values (e.g., 9153...BD and 6EAC...42) are generated, alternating throughout the 16 rounds.
            
            ![[Pasted image 20250506014616.png]]
            This shows Plaintext -> DES(K1) -> Intermediate -> DES(K2) -> Plaintext, illustrating the property $E_{K_2}(E_{K_1}(P)) = P$.*
        -   **Possible Weak Keys:** 48 keys that generate only **four** distinct round keys. The 16 round keys fall into four groups, with each group containing four identical round keys.
        -   **Key Complement Property:**
            -   Given a key $K$, its complement $K'$ is obtained by flipping every bit (0->1, 1->0).
            -   Given a plaintext $P$, its complement is $P'$.
            -   DES has the property that if $C = E_K(P)$, then the complement of the ciphertext $C'$ is equal to the encryption of the complement plaintext $P'$ with the complement key $K'$: $C' = E_{K'}(P')$.
            -   **Impact on Brute-Force:** This means an attacker only needs to test half the key space ($2^{55}$ keys). If they test key $K$ and it doesn't work, they implicitly also know that $K'$ won't work for the complement relationship they might try to exploit. It slightly reduces the theoretical brute-force effort but doesn't fundamentally change the vulnerability.

### Multiple DES (Enhancing DES Security)

-   **Motivation:** To overcome the key size vulnerability of single DES while leveraging existing DES implementations.
-   **Method:** Apply the DES encryption process multiple times using different keys.
-   **Implementations:**
    1.  **Double DES (2DES):**
        -   **Process:** Encrypt plaintext $P$ twice using two *different* 56-bit keys, $K_1$ and $K_2$.
            -   $C = E_{K_2}(E_{K_1}(P))$
        -   **Goal:** Increase effective key length from 56 bits to 112 bits ($56 + 56$).
        -   **Decryption:** Reverse the process: $P = D_{K_1}(D_{K_2}(C))$.
            ![[Pasted image 20250506014638.png]] Shows: Plain Text -> DES Algo (K1) -> Cipher Text 1 -> DES Algo (K2) -> Cipher Text 2 (Final Output).
        -   **Advantage:** Increases nominal key length to 112 bits.
        -   **Disadvantage:** Vulnerable to the **Meet-in-the-Middle (MITM) Attack**.
            -   **MITM Attack:** An attacker with a known plaintext-ciphertext pair ($P, C$) can break 2DES much faster than brute-forcing $2^{112}$ keys.
                1. Encrypt $P$ with all $2^{56}$ possible keys for $K_1$ and store the intermediate results ($I = E_{K_1}(P)$) along with $K_1$.
                2. Decrypt $C$ with all $2^{56}$ possible keys for $K_2$ ($D_{K_2}(C)$).
                3. Look for a **match** where $E_{K_1}(P) = D_{K_2}(C)$. A match gives a candidate pair $(K_1, K_2)$.
            -   **Complexity:** Requires roughly $2 \times 2^{56}$ operations and significant storage ($2^{56}$ intermediate values), but this is drastically better than $2^{112}$. The effective key length is reduced to around $2^{57}$ (due to filtering false positives), only marginally better than single DES.
            -   **Conclusion:** 2DES does **not** provide a significant security improvement over single DES due to MITM.
    2.  **Triple DES (3DES / TDES):**
        -   **Motivation:** Designed to overcome the MITM attack vulnerability of 2DES.
        -   **Process (EDE - Encrypt-Decrypt-Encrypt):** Uses two or three distinct keys ($K_1, K_2, K_3$).
            -   $C = E_{K_3}(D_{K_2}(E_{K_1}(P)))$
        -   **Why EDE?** The Encrypt-Decrypt-Encrypt sequence makes 3DES backward compatible with single DES if $K_1=K_2=K_3$.
        -   **Keying Options:**
            -   **3 Keys:** $K_1, K_2, K_3$ are all independent (168-bit effective key length: $3 \times 56$). Most secure variant.
            -   **2 Keys:** $K_1$ and $K_2$ are independent, but $K_3 = K_1$ (112-bit effective key length: $2 \times 56$). $C = E_{K_1}(D_{K_2}(E_{K_1}(P)))$. Still widely used.
        -   **Decryption:** Reverse the process: $P = D_{K_1}(E_{K_2}(D_{K_3}(C)))$.
            ![[Pasted image 20250506014658.png]]Shows: Plain Text -> DES Algo (Encrypt with K1) -> Cipher Text 1 -> DES Algo (Decrypt with K2) -> Cipher Text 2 -> DES Algo (Encrypt with K3) -> Cipher Text 3 (Final Output).
        -   **Advantages:**
            -   Significantly increases key length (to 112 or 168 bits), making brute-force attacks infeasible.
            -   Resistant to the basic MITM attack that breaks 2DES. Provides much stronger security than DES or 2DES. (Effective security generally considered $2^{112}$).
        -   **Disadvantages:**
            -   **Slow:** Performs DES three times, making it significantly slower than single DES and much slower than modern ciphers like AES.
            -   Still uses a 64-bit block size, which can be inefficient and have security implications in some modes of operation compared to AES's 128-bit block.
            -   While much stronger, still vulnerable to certain advanced attacks, especially if large amounts of data are processed with the same key.

### Section Summary: Modern Block Ciphers & DES

-   **Block Ciphers:** Encrypt fixed-size blocks using symmetric keys. Rely on **Confusion** (obscuring key relationship - S-Boxes) and **Diffusion** (spreading plaintext influence - P-Boxes, permutations).
-   **Core Components:** S-Boxes (Substitution), P-Boxes (Permutation), XOR (Mixing, Reversibility), Circular Shifts (Key Scheduling, Diffusion).
-   **Product Ciphers:** Combine multiple transformations (Substitution, Permutation) in rounds for strength (e.g., DES, AES).
-   **Feistel Cipher:** A structure using rounds, splitting data, a round function F, XOR, and swapping. Allows same algorithm for encryption/decryption (e.g., DES).
-   **DES:** 64-bit block, 56-bit key, 16 Feistel rounds. Foundational but outdated due to short key length (vulnerable to brute-force). Has known design and key weaknesses (weak/semi-weak keys).
-   **Multiple DES:**
    -   **2DES:** $E_{K_2}(E_{K_1}(P))$. Broken by Meet-in-the-Middle (MITM) attack, little security gain.
    -   **3DES:** $E_{K_3}(D_{K_2}(E_{K_1}(P)))$ (usually $K_3=K_1$ or all unique). Much stronger, resists MITM, but slow. Was a common replacement for DES before AES.

---

## 2.3 Advanced Encryption Standard (AES)

### Introduction

-   **Definition:** AES is the current de facto **symmetric key encryption** algorithm standard, widely used globally to secure sensitive data.
-   **Origin:** Selected by NIST in 2001 after a public competition. The winning algorithm was **Rijndael**, developed by Belgian cryptographers Joan Daemen and Vincent Rijmen.
-   **Key Features:** Known for its combination of **security, speed, and efficiency** in both hardware and software implementations, making it the preferred standard for modern encryption.
-   **Structure:**
    -   AES is a **block cipher**.
    -   Operates on fixed-size blocks of **128 bits**.
    -   Applies multiple **rounds** of encryption transformations.
    -   **Key Length Options:** Supports key sizes of **128, 192, or 256 bits**.
    -   **Number of Rounds:** The number of rounds depends on the key length:
        -   10 rounds for 128-bit keys
        -   12 rounds for 192-bit keys
        -   14 rounds for 256-bit keys
        *(More rounds generally provide higher security at the cost of slight performance decrease).*

-   **Comparison with DES:**
    -   **Key Length:** 128/192/256 bits (AES) vs. 56 bits (DES) -> Much stronger against brute-force.
    -   **Block Size:** 128 bits (AES) vs. 64 bits (DES) -> More efficient for bulk encryption, some security benefits in certain modes.
    -   **Speed & Efficiency:** AES is significantly faster than DES (and especially 3DES), designed for modern processors.
    -   **Security:** Provides excellent security against all known practical cryptographic attacks (when implemented correctly). Considered highly reliable.
    -   **Design:** AES is **not** based on the Feistel network. It uses a **Substitution-Permutation Network (SPN)** structure.

### AES Structure and Design Philosophy

-   **Feistel vs. Non-Feistel:**
    1.  **Feistel Ciphers (e.g., DES):** Use a round function that may mix invertible (like XOR) and non-invertible components (like S-boxes that reduce bits). The Feistel structure itself ensures decryptability.
    2.  **Non-Feistel Ciphers (e.g., AES):** Typically use **only invertible components** throughout the main encryption rounds. Decryption requires explicitly using the inverse of each transformation.
-   **AES Terminology:**
    -   The AES encryption algorithm is called **Cipher**.
    -   The AES decryption algorithm is called **Inverse Cipher**. It's similar in structure but uses the inverse of the round transformations and applies round keys in reverse order.
-   **Round Keys:**
    -   Generated by a **Key Expansion** algorithm (key schedule).
    -   Round keys are always **128 bits** long, matching the block size (state size), regardless of the original cipher key size (128, 192, or 256 bits).
    -   The number of round keys generated is always **one more** than the number of rounds ($N_r$). (There are $N_r + 1$ round keys, indexed $K_0$ to $K_{N_r}$).
        -   $N_r=10$ for AES-128 -> 11 round keys (44 words)
        -   $N_r=12$ for AES-192 -> 13 round keys (52 words)
        -   $N_r=14$ for AES-256 -> 15 round keys (60 words)
    -   Round Keys Notation: $K_0, K_1, K_2, ..., K_{N_r}$.

### Steps of AES Encryption

AES encryption transforms a 128-bit plaintext block into a 128-bit ciphertext block through a series of structured steps.

1.  **Key Expansion:** The original cipher key (128, 192, or 256 bits) is expanded into $N_r+1$ round keys, each 128 bits long.
2.  **Initial Round (Pre-Round Transformation):**
    -   **AddRoundKey:** The 128-bit plaintext block is XORed with the first round key ($K_0$).
3.  **Main Rounds ($N_r - 1$ rounds):** Each of the main rounds (Round 1 to $N_r-1$) involves four distinct transformation steps applied in sequence:
    -   **SubBytes:** A non-linear **byte substitution** step. Each byte of the 128-bit state is replaced with another byte according to a fixed lookup table (the AES S-box). *Provides confusion.*
    -   **ShiftRows:** A **permutation** step. The bytes in the last three rows of the state matrix are shifted cyclically to the left by different offsets (1, 2, or 3 bytes). The first row is not shifted. *Provides diffusion across columns.*
    -   **MixColumns:** A **mixing** step using linear algebra (matrix multiplication in $GF(2^8)$). Each column of the state matrix is transformed into a new column. *Provides diffusion within columns.*
    -   **AddRoundKey:** The current state is XORed with the corresponding round key ($K_1$ for round 1, $K_2$ for round 2, etc.).
4.  **Final Round (Round $N_r$):** The final round is slightly different and **omits the MixColumns step**. It consists of:
    -   SubBytes
    -   ShiftRows
    -   AddRoundKey (using the last round key, $K_{N_r}$)

-   **Output:** The 128-bit state after the final round is the ciphertext.

-   **AES Overview Diagram:**
    ![[Pasted image 20250506014729.png]] This diagram shows:
        - *Input: 128-bit plaintext.*
        - *Initial Step: Pre-round transformation (AddRoundKey with K0).*
        - *Rounds 1 to Nr-1: Each containing the four transformations (SubBytes, ShiftRows, MixColumns, AddRoundKey with K1 to K(Nr-1)).*
        - *Round Nr (slightly different): Contains SubBytes, ShiftRows, AddRoundKey with KNr (Missing MixColumns).*
        - *Output: 128-bit ciphertext.*
        - *Parallel Process: Key Expansion generating Round Keys (K0...KNr) from the Cipher Key.*
        - *Table relating Key Size (128, 192, 256) to Number of Rounds Nr (10, 12, 14).*
    *This visual flow is essential for understanding the overall AES process.*

### AES Data Units

AES processes data using specific units of measurement:

-   **Bit:** The smallest atomic unit (0 or 1).
-   **Byte:** A group of **8 bits**. Often represented as a 2-digit hexadecimal number (e.g., `A3`). Can be viewed as a row matrix (1x8) or column matrix (8x1) of bits. Represented by lowercase bold **b**.
    ![[Pasted image 20250506014814.png]]
    Shows a Byte `b` as 8 bits $b_0..b_7$ in a row, and also as an 8x1 column matrix.
-   **Word:** A group of **32 bits** (4 bytes). Can be viewed as a row matrix (1x4) or column matrix (4x1) of bytes. Represented by lowercase bold **w**.
    ![[Pasted image 20250506014830.png]]
    Shows a Word `w` as 4 bytes $b_0..b_3$ in a row, and also as a 4x1 column matrix.
-   **Block:** The fixed size of data processed by AES, which is **128 bits** (16 bytes). Can be represented as a row matrix of 16 bytes. AES encrypts and decrypts data one block at a time.
    ![[Pasted image 20250506014855.png]] Shows a Block as 16 bytes $b_0..b_{15}$ in a row.
-   **State:** An intermediate form of the 128-bit data block within the AES algorithm rounds.
    -   The **State** is represented as a **4x4 matrix of bytes**.
    -   Each element is denoted $S_{r,c}$, where $r$ is the row index (0 to 3) and $c$ is the column index (0 to 3).
    -   Occasionally treated as a 1x4 row matrix of words, where each word corresponds to a column of the 4x4 state matrix.
    -   Represented by uppercase bold **S**. A temporary state during transformations might be denoted **T**.
    -   **Block-to-State Conversion:** At the beginning of the cipher, the 16 bytes of the input block ($b_0..b_{15}$) are loaded into the 4x4 state matrix **column by column**.
        -   Column 0: $b_0, b_1, b_2, b_3$
        -   Column 1: $b_4, b_5, b_6, b_7$
        -   Column 2: $b_8, b_9, b_{10}, b_{11}$
        -   Column 3: $b_{12}, b_{13}, b_{14}, b_{15}$
        $$
        \mathbf{State} = \begin{bmatrix}
        b_0 & b_4 & b_8 & b_{12} \\
        b_1 & b_5 & b_9 & b_{13} \\
        b_2 & b_6 & b_{10} & b_{14} \\
        b_3 & b_7 & b_{11} & b_{15}
        \end{bmatrix}
        = \begin{bmatrix}
        S_{0,0} & S_{0,1} & S_{0,2} & S_{0,3} \\
        S_{1,0} & S_{1,1} & S_{1,2} & S_{1,3} \\
        S_{2,0} & S_{2,1} & S_{2,2} & S_{2,3} \\
        S_{3,0} & S_{3,1} & S_{3,2} & S_{3,3}
        \end{bmatrix}
        $$
    -   **State-to-Block Conversion:** At the end of the cipher, the bytes are extracted from the final state matrix using the same column-by-column order to form the output block.

    ![[Pasted image 20250506014917.png]]Shows the 4x4 matrix S and its relation to 4 words (columns).
    ![[Pasted image 20250506014949.png]]This visually clarifies how the linear 16-byte block is mapped to the 4x4 state matrix column-by-column, and extracted in the same way. The small inset shows the column-major insertion/extraction flow.
    ![[Pasted image 20250506015001.png]] This summarizes the visual representations of Byte, Word, Block, and State.


### AES Transformations (In Detail)

AES uses four main types of transformations within its rounds to provide security: substitution, permutation (shifting), mixing, and key-adding.

#### Structure of Each Round

-   **Encryption Site:**
    -   Each round (except the last) uses 4 invertible transformations: SubBytes, ShiftRows, MixColumns, AddRoundKey.
    -   The last round has only 3 transformations (omits MixColumns).
    -   Each transformation takes an input state and produces an output state.
    -   The **pre-round** section uses only one transformation: AddRoundKey.
-   **Decryption Site:**
    -   Uses the **inverse transformations** in reverse order:
        -   InvShiftRows
        -   InvSubBytes
        -   AddRoundKey (self-inverse)
        -   InvMixColumns
    -   The AddRoundKey transformation is its own inverse (since XORing twice with the same key cancels out).
    -   The MixColumns transformation is omitted in the *first* step of decryption (corresponding to the last round of encryption).

-   **Round Structure Diagrams:**
    ![[Pasted image 20250506015844.png]]
    "Structure of each round" diagram. This flowchart shows the sequence: State -> SubBytes -> State -> ShiftRows -> State -> MixColumns -> State -> AddRoundKey -> State. The notes indicate AddRoundKey is applied before round 1, and MixColumns is missing in the last round.
    
    ![[Pasted image 20250506015126.png]]
    Shows Plaintext + K0 -> AddRoundKey -> [Round 1 Box: SubBytes, ShiftRows, MixColumns, AddRoundKey + K1] -> ...

#### 1. Substitution (SubBytes / InvSubBytes)

-   **Similarity to DES:** Like DES, AES uses substitution.
-   **Difference:** The mechanism is different. Substitution is done byte-by-byte, independently for each of the 16 bytes in the state.
-   **S-Box:** A single, fixed 16x16 lookup table (the AES S-Box) is used for all byte substitutions in **SubBytes**.
    -   **Lookup:** To substitute a byte, interpret it as two hexadecimal digits. The first digit ($h_1$) specifies the **row** (0-F) and the second digit ($h_2$) specifies the **column** (0-F) in the S-Box table. The byte found at that row/column intersection in the table is the substituted output byte.
    -   If two input bytes are the same, their output after SubBytes will also be the same.
    -   Provides **non-linearity** and **confusion**.
-   **Transformation:** Changes the *content* of each byte but not their *position* in the state matrix. Involves 16 independent byte-to-byte transformations.
-   **InvSubBytes:** The corresponding inverse transformation used in decryption. It uses a different lookup table (the Inverse S-Box) which reverses the SubBytes mapping.

-   **Diagrams & Tables:**
    ![[Pasted image 20250506015237.png]] Shows one byte `ab` (hex) from the input State being used to index the S-Box Table (row `a`, col `b`) to produce output byte `cd`, which goes into the corresponding position in the output State.
    ![[Pasted image 20250506015253.png]] Highlight the example: Input `5A` (row 5, col A) -> Output `BE`. Input `5B` (row 5, col B) -> Output `39`. Note how a 1-bit input difference (`A`=1010 vs `B`=1011) leads to a 4-bit output difference (`BE`=10111110 vs `39`=00111001), illustrating the confusion/avalanche property of the S-box.
    ![[Pasted image 20250506015334.png]]this table reverses the SubBytes lookup.
    
    ![[Pasted image 20250506015403.png]]
    ![[Pasted image 20250506015421.png]]
    ![[Pasted image 20250506015437.png]]
    Shows a full 4x4 State matrix being transformed by SubBytes, and the result being transformed back to the original by InvSubBytes, demonstrating the byte-wise application and reversibility.*

#### 2. Permutation (ShiftRows / InvShiftRows)

-   **Purpose:** To permute the byte data within the state, providing diffusion across the columns. AES performs permutation at the **byte level**, unlike DES which permutes bits. The order of bits *within* a byte is not changed.
-   **ShiftRows (Encryption):**
    -   Operates independently on each of the **rows** (0, 1, 2, 3) of the state matrix.
    -   Shifts are **circularly to the left**.
    -   The number of shifts depends on the row number:
        -   **Row 0:** No shift (0 bytes).
        -   **Row 1:** Shifted left by **1 byte**.
        -   **Row 2:** Shifted left by **2 bytes**.
        -   **Row 3:** Shifted left by **3 bytes**.
-   **InvShiftRows (Decryption):**
    -   Reverses the ShiftRows operation.
    -   Shifts are **circularly to the right** by the same offsets (0, 1, 2, 3 bytes for rows 0, 1, 2, 3 respectively).
    -   ShiftRows and InvShiftRows are inverses of each other.

-   **Algorithm/Diagrams:**
    ![[Pasted image 20250506015516.png]]Shows the 4x4 state matrix with arrows indicating the left circular shifts for rows 1, 2, and 3.
    
    ![[Pasted image 20250506015536.png]] Illustrates the logic of iterating through rows 1-3 and performing the circular shift.
    
    ![[Pasted image 20250506015551.png]] Shows a specific state matrix being transformed by ShiftRows and then transformed back by InvShiftRows.

#### 3. Mixing (MixColumns / InvMixColumns)

-   **Purpose:** Provides **diffusion** at the bit level *within* each column. It's an "inter-byte" transformation that changes bits inside a byte based on bits in neighboring bytes within the same column.
-   **Mechanism:**
    -   Operates independently on each **column** (0, 1, 2, 3) of the state matrix.
    -   Treats each column as a 4-byte vector (or a polynomial over $GF(2^8)$).
    -   Each column is transformed by **multiplying** it by a fixed **constant matrix** in the finite field $GF(2^8)$.
    -   Takes 4 bytes as input (one column) and outputs 4 completely new bytes, combining the input bytes.
    -   Even if all 4 input bytes in a column are the same, the 4 output bytes will generally be different.
-   **MixColumns (Encryption):** Uses a specific constant matrix $C$.
-   **InvMixColumns (Decryption):** Uses the inverse constant matrix $C^{-1}$ in $GF(2^8)$.
-   **Mathematical Detail:** The matrix multiplication involves addition and multiplication operations defined in the finite field $GF(2^8)$, which correspond to XOR and a special polynomial multiplication modulo an irreducible polynomial, respectively. (This level of detail might be beyond the scope if GF fields weren't covered extensively, but it's the underlying mechanism).
-   **Omission:** MixColumns (and InvMixColumns) is **skipped** in the very last round of encryption (and the first step of decryption).

-   **Diagrams/Matrices:**
    ![[Pasted image 20250506015642.png]]Shows matrix multiplication of an old column vector by a constant matrix to produce a new column vector.
    
    ![[Pasted image 20250506015659.png]] constant matrices C and C^{-1} used for MixColumns and InvMixColumns from page 118. Show the hexadecimal values (e.g., 02, 03, 01, 01 for the first row of C).
    
    ![[Pasted image 20250506015713.png]]MixColumns transformation diagram (Figure 7.13). Shows the operation taking one column, multiplying by the constant matrix, and producing a new column.
    
    ![[Pasted image 20250506015754.png]]Shows a specific state matrix being transformed column-by-column using MixColumns, and then transformed back using InvMixColumns.

#### 4. Key Adding (AddRoundKey)

-   **Purpose:** The most critical step for security, as it incorporates the **secret key** material into the state. Without this step, the cipher would be easily breakable regardless of the other transformations.
-   **Mechanism:**
    -   A simple **bitwise XOR** operation.
    -   The 128-bit state matrix is XORed with the current 128-bit round key.
    -   The 128-bit round key is viewed as a 4x4 matrix of bytes, similar to the state.
    -   The XOR is performed byte-by-byte between the state matrix and the round key matrix. (Equivalently, word-by-word between state columns and round key words).
-   **Invertibility:** AddRoundKey is its **own inverse**. XORing with the same key twice cancels the operation ($State \oplus K_{round} \oplus K_{round} = State$). This simplifies decryption.
-   **Frequency:** Applied once before the first round (using $K_0$) and once at the end of *every* round (using $K_1$ to $K_{N_r}$).

-   **Algorithm/Diagrams:**
    ![[Pasted image 20250506015918.png]]Shows the state matrix being XORed element-wise with the Key word matrix (representing the round key).
    
    ![[Pasted image 20250506015932.png]] Shows the column-wise XOR operation $s_c \leftarrow s_c \oplus w_{round+4c}$.
    
    ![[Pasted image 20250506015953.png]]

### AES Key Expansion (Key Schedule)

-   **Purpose:** To generate the required $N_r+1$ round keys (each 128 bits / 4 words) from the original cipher key (which can be 128, 192, or 256 bits).
-   **General Idea:** The key expansion routine creates round keys **word by word** (where a word is 32 bits). It generates a total of $4 \times (N_r+1)$ words, denoted $w_0, w_1, ..., w_{4(N_r+1)-1}$.
    -   AES-128 (10 rounds): Needs 11 round keys = 44 words ($w_0$ to $w_{43}$).
    -   AES-192 (12 rounds): Needs 13 round keys = 52 words ($w_0$ to $w_{51}$).
    -   AES-256 (14 rounds): Needs 15 round keys = 60 words ($w_0$ to $w_{59}$).
-   **Round Key Formation:** Each 128-bit round key $K_i$ is formed by concatenating four consecutive words from the expanded key sequence.
    -   $K_0 = w_0 || w_1 || w_2 || w_3$
    -   $K_1 = w_4 || w_5 || w_6 || w_7$
    -   ...
    -   $K_{N_r} = w_{4N_r} || w_{4N_r+1} || w_{4N_r+2} || w_{4N_r+3}$
    ![[Pasted image 20250506020030.png]]Shows how words $w_0..w_3$ form the pre-round key, $w_4..w_7$ form the key for round 1, etc., up to round $N_r$. Also notes $W40, W41, W42, W43$ for the last round of AES-128.

#### Key Expansion in AES-128 (Nk=4, Nr=10)

-   **Input:** 128-bit cipher key = 16 bytes ($k_0$ to $k_{15}$) = 4 words.
-   **First 4 Words:** The first four words of the expanded key ($w_0, w_1, w_2, w_3$) are simply the original cipher key.
    -   $w_0 = k_0 || k_1 || k_2 || k_3$
    -   $w_1 = k_4 || k_5 || k_6 || k_7$
    -   $w_2 = k_8 || k_9 || k_{10} || k_{11}$
    -   $w_3 = k_{12} || k_{13} || k_{14} || k_{15}$
-   **Remaining Words ($w_4$ to $w_{43}$):** Generated iteratively. For $i$ from 4 to 43:
    -   **Case 1: If $i \pmod 4 \neq 0$:**
        -   The word $w_i$ is calculated by XORing the previous word $w_{i-1}$ with the word four positions back $w_{i-4}$.
        -   $w_i = w_{i-1} \oplus w_{i-4}$
    -   **Case 2: If $i \pmod 4 = 0$:** (i.e., for the first word of each round key: $w_4, w_8, w_{12}, ...$)
        -   A more complex calculation involving a temporary word $t$.
        -   $w_i = t \oplus w_{i-4}$
        -   Where $t$ is calculated from the previous word $w_{i-1}$ as follows:
            1.  **RotWord:** Perform a circular left shift on the bytes of $w_{i-1}$. If $w_{i-1} = (b_0, b_1, b_2, b_3)$, then $RotWord(w_{i-1}) = (b_1, b_2, b_3, b_0)$.
            2.  **SubWord:** Apply the AES S-Box substitution to each of the 4 bytes in the rotated word.
            3.  **Rcon XOR:** XOR the result with a **Round Constant**, $Rcon[i/4]$. The round constant is different for each round and prevents symmetries. It's a 4-byte value where the rightmost three bytes are always zero.
            -   $t = SubWord(RotWord(w_{i-1})) \oplus Rcon[i/4]$
-   **Components for $t$ Calculation:**
    -   **RotWord:** Rotates the 4 bytes of a word one position to the left.
    -   **SubWord:** Applies the S-Box to each byte of a word.
    -   **Round Constants (Rcon):** Predefined values used in the key schedule. $Rcon[j] = (RC_j, 00, 00, 00)$, where $RC_j$ is typically $x^{j-1}$ in $GF(2^8)$ (using polynomial representation $x \equiv 02$).
        ![[Pasted image 20250506020111.png]]
        Shows the hexadecimal values for $Rcon[1]$ to $Rcon[10]$.

-   **Key Expansion Diagrams & Pseudocode:**
    
    ![[Pasted image 20250506020157.png]]
    ![[Pasted image 20250506020220.png]]
    ![[Pasted image 20250506020236.png]]
    ![[Pasted image 20250506020254.png]]
     Shows the initial cipher key forming $w_0..w_3$. Shows the iterative calculation of subsequent words $w_i$, highlighting the dependency on $w_{i-1}$ and $w_{i-4}$. The box at the bottom shows the complex calculation for $w_i$ when $i \pmod 4 = 0$, involving $w_{i-1}$, RotWord, SubWord, Rcon[i/4] to create $t_i$, which is then XORed with $w_{i-4}$.*
     
    ![[Pasted image 20250506020328.png]] Zooms in on the $t = SubWord(RotWord(w_{i-1})) \oplus Rcon[i/4]$ calculation.
    
    ![[Pasted image 20250506020355.png]]Provides the precise logic for calculating all words $w_0$ to $w_{43}$.
    
    ![[Pasted image 20250506020408.png]] Shows the calculated round key words for a specific 128-bit key.
    
    ![[Pasted image 20250506020509.png]] the non-linear dependency between round keys due to SubWord and the difference guaranteed by Rcon.
    
    ![[Pasted image 20250506020525.png]] Shows that changing just one bit in the cipher key results in significantly different round keys after a few rounds, demonstrating diffusion in the key schedule.
    
    ![[Pasted image 20250506020541.png]] Discusses why AES doesn't have weak keys like DES, showing that even with an all-zero key, the round keys become different after the second round due to Rcon and SubWord.

#### Key Expansion in AES-192 (Nk=6, Nr=12) and AES-256 (Nk=8, Nr=14)

-   **Similarity:** The algorithms are very similar to AES-128's expansion.
-   **Differences:**
    -   **AES-192 (Nk=6):**
        -   Input key is 192 bits (6 words). These form $w_0$ to $w_5$.
        -   Words are generated in groups of **six**. Need 52 words total ($w_0$ to $w_{51}$).
        -   Calculation for $i \ge 6$:
            -   If $i \pmod 6 \neq 0$: $w_i = w_{i-1} \oplus w_{i-6}$
            -   If $i \pmod 6 = 0$: $w_i = SubWord(RotWord(w_{i-1})) \oplus Rcon[i/6] \oplus w_{i-6}$ (using $t$ notation: $w_i = t \oplus w_{i-6}$)
    -   **AES-256 (Nk=8):**
        -   Input key is 256 bits (8 words). These form $w_0$ to $w_7$.
        -   Words are generated in groups of **eight**. Need 60 words total ($w_0$ to $w_{59}$).
        -   Calculation for $i \ge 8$:
            -   If $i \pmod 8 \neq 0$ AND $i \pmod 4 \neq 0$: $w_i = w_{i-1} \oplus w_{i-8}$
            -   If $i \pmod 8 \neq 0$ BUT $i \pmod 4 = 0$: An extra SubWord step is applied: $w_i = SubWord(w_{i-1}) \oplus w_{i-8}$
            -   If $i \pmod 8 = 0$: $w_i = SubWord(RotWord(w_{i-1})) \oplus Rcon[i/8] \oplus w_{i-8}$ (using $t$ notation: $w_i = t \oplus w_{i-8}$)

#### Key Expansion Analysis

-   **Design Goals:** The key expansion mechanism is designed to thwart cryptanalysts:
    -   **Diffusion:** Changing even one bit of the cipher key rapidly affects bits in multiple round keys across several rounds.
    -   **Non-linearity:** The use of **SubWord** (which uses the S-box) makes the relationship between the cipher key and the round keys highly non-linear. This prevents simple linear attacks on the key schedule.
    -   **Symmetry Breaking:** The **Round Constants (Rcon)** ensure that round keys are different even if the cipher key has symmetries (like all zeros or all ones). This prevents weak keys similar to those found in DES.
-   **Security Implications:**
    -   **No Serious Weak Keys:** Due to the design, AES does not suffer from known weak, semi-weak, or possibly weak keys like DES.
    -   **Resistance to Related-Key Attacks:** The complexity makes it hard to predict how changes in the cipher key relate to changes in round keys.
    -   **Difficulty from Partial Knowledge:** Even if an attacker (Eve) knows some round key words, the non-linearity makes it computationally difficult to recover the original cipher key or other round keys without significant effort.
-   **Implementation:** The key expansion process can be implemented efficiently on various platforms.

### Security Strength of AES

-   **Overall:** AES is considered highly secure when implemented correctly. Its strength comes from:
    -   **Longer Key Lengths:** 128, 192, 256 bits make brute-force attacks computationally infeasible with current and foreseeable technology.
    -   **Sufficient Rounds:** The number of rounds (10, 12, 14) provides a large security margin against known analytical attacks like linear and differential cryptanalysis.
    -   **Strong Round Transformations:** SubBytes (non-linearity), ShiftRows & MixColumns (diffusion) work together effectively.
    -   **Robust Key Schedule:** Diffuses key bits well and resists attacks.
-   **Resistance to Attacks:**
    -   **Brute-Force Attacks:** Impractical due to key length.
    -   **Linear and Differential Cryptanalysis:** AES was specifically designed with mathematical properties (e.g., properties of the S-box and MixColumns over $GF(2^8)$) to resist these attacks effectively. The best known attacks require amounts of data or computation far beyond practical limits.
    -   **Side-Channel Attacks:** While the AES algorithm *itself* is secure, *implementations* can be vulnerable. Attackers might measure timing, power consumption, or electromagnetic radiation during encryption/decryption to deduce information about the key. Protecting implementations against side-channel attacks is crucial in practice (e.g., using constant-time operations, masking).

### Advantages of AES

Compared to older algorithms like DES/3DES:

-   **Security:** Significantly stronger due to longer keys, more rounds, and robust design against modern cryptanalysis. Harder for attackers to break or intercept data via brute-force.
-   **Cost:** AES is an open, publicly available standard (royalty-free). Its widespread adoption means plenty of well-tested libraries and hardware implementations are available, making it cost-effective.
-   **Implementation:** Designed to be efficient in both hardware (compact logic) and software (using byte-oriented operations suitable for modern processors). Flexible and relatively simple to implement compared to some other ciphers.
-   **Speed:** Much faster than 3DES and generally faster than DES on modern hardware.

### Why AES Replaced DES

-   **Primary Reason:** DES's 56-bit key length became insufficient against brute-force attacks due to increasing computing power.
-   **NIST Process:** Recognizing DES's vulnerability, NIST initiated a public competition (1997-2000) to find a replacement.
-   **Selection:** Rijndael was selected as AES in 2001 because it offered the best combination of security, performance, efficiency, and flexibility among the finalists. It uses longer key lengths and is mathematically designed to be much harder to break than DES.

---

## Glossary of New Terms

-   **Abstract Algebra:** The study of algebraic structures like groups, rings, and fields.
-   **Group:** A set with one binary operation satisfying closure, associativity, identity, and inverse properties.
-   **Abelian Group:** A group where the operation is also commutative.
-   **Cyclic Group:** A group where all elements are powers of a single generator element.
-   **Generator:** An element in a cyclic group whose powers produce all elements of the group.
-   **Ring:** A set with two operations (usually + and ⋅) where it forms an Abelian group under +, multiplication is associative and closed, and multiplication distributes over addition.
-   **Commutative Ring:** A ring where multiplication is also commutative.
-   **Ring with Unity:** A ring with a multiplicative identity element (1).
-   **Integral Domain:** A commutative ring with unity that has no zero divisors.
-   **Field:** An integral domain where every non-zero element has a multiplicative inverse. Allows division by non-zero elements.
-   **Finite Field (Galois Field - GF):** A field with a finite number of elements, crucial for cryptography (e.g., $GF(2^n)$).
-   **Block Cipher:** An encryption algorithm that processes data in fixed-size blocks.
-   **Stream Cipher:** An encryption algorithm that processes data continuously (e.g., bit by bit).
-   **Confusion:** A cryptographic property making the relationship between ciphertext and key complex (achieved via substitution/S-Boxes).
-   **Diffusion:** A cryptographic property spreading the influence of plaintext/key bits across the ciphertext (achieved via permutation/P-Boxes/mixing).
-   **S-Box (Substitution Box):** A component performing non-linear substitution via a lookup table to provide confusion.
-   **P-Box (Permutation Box):** A component performing permutation (reordering) of bits/bytes to provide diffusion.
-   **XOR (Exclusive OR):** A bitwise operation used for mixing key material, easily reversible.
-   **Circular Shift (Rotation):** Shifting bits where they wrap around, used for diffusion, especially in key schedules.
-   **Product Cipher:** A cipher built by combining multiple simpler transformations (e.g., substitution, permutation) in rounds.
-   **Feistel Cipher/Network:** A specific structure for block ciphers involving splitting data, rounds, a round function, XOR, and swapping (e.g., DES). Allows easy decryption.
-   **DES (Data Encryption Standard):** Older block cipher standard (64-bit block, 56-bit key, 16 Feistel rounds). Now insecure due to key size.
-   **Round Key:** A key derived from the main cipher key used in a specific round of encryption/decryption.
-   **Initial Permutation (IP) / Final Permutation (FP):** Bit permutations at the start/end of DES (no security benefit).
-   **Expansion Permutation (E):** P-box in DES round function expanding 32 bits to 48 bits.
-   **Key Scheduling:** The algorithm used to generate round keys from the cipher key.
-   **Avalanche Effect:** Property where a small input change (1 bit) causes large output changes (approx. half the bits).
-   **Completeness Effect:** Property where each output bit depends on many input bits.
-   **Cryptanalysis:** The science of analyzing and breaking cryptographic systems.
-   **Differential Cryptanalysis:** Attack exploiting propagation of differences through a cipher.
-   **Linear Cryptanalysis:** Attack exploiting linear approximations of a cipher's behavior.
-   **Weak Key (DES):** Key causing encryption to be self-inverse (only 1 round key generated).
-   **Semi-Weak Key (DES):** Pair of keys $(K_1, K_2)$ where $E_{K_2}(E_{K_1}(P)) = P$ (only 2 round keys generated per key).
-   **Key Complement Property (DES):** $C=E_K(P) \implies C'=E_{K'}(P')$.
-   **Multiple DES (2DES, 3DES):** Applying DES multiple times to increase security. 2DES is broken by MITM. 3DES is much stronger but slow.
-   **Meet-in-the-Middle (MITM) Attack:** Attack reducing the effective key space of multiple encryptions (breaks 2DES).
-   **AES (Advanced Encryption Standard):** Current block cipher standard (Rijndael algorithm). 128-bit block, 128/192/256-bit keys, 10/12/14 rounds. Uses SPN structure.
-   **SPN (Substitution-Permutation Network):** Cipher structure using alternating layers of substitution (S-boxes) and linear transformations (permutations/mixing like ShiftRows, MixColumns). AES is an SPN.
-   **State (AES):** Internal 4x4 byte matrix representation of the data block during AES rounds.
-   **SubBytes (AES):** Byte substitution using the AES S-box.
-   **ShiftRows (AES):** Cyclical byte shift within rows of the state.
-   **MixColumns (AES):** Mixing operation within columns using $GF(2^8)$ matrix multiplication.
-   **AddRoundKey (AES):** XORing the state with the round key.
-   **Key Expansion (AES):** Process generating round keys in AES, involving RotWord, SubWord, and Rcon.
-   **RotWord (AES Key Schedule):** Circular left shift of bytes within a word.
-   **SubWord (AES Key Schedule):** Application of S-box to all bytes of a word.
-   **Rcon (AES Key Schedule):** Round constants used to break symmetry in key expansion.
-   **Side-Channel Attack:** Attack exploiting information leaked from the physical implementation (timing, power) rather than the algorithm itself.

---

## Further Reading / Resources

-   **"Cryptography and Network Security: Principles and Practice" by William Stallings:** A comprehensive textbook covering these topics in detail.
-   **"Understanding Cryptography" by Christof Paar and Jan Pelzl:** Another excellent textbook with a practical approach.
-   **NIST Publications:** Official standards documents for DES (FIPS 46-3) and AES (FIPS 197).
-   **Online Resources:** Websites like Wikipedia, Cryptography Stack Exchange, and various university course pages offer detailed explanations of these concepts.
-   **Interactive Animations:** Search for "AES animation" or "DES animation" online to find visual tools that help understand the data flow.

## Concept Map Idea

*   **Central Node:** Symmetric Key Cryptography
*   **Main Branches:**
    *   Mathematical Foundations
        *   Group -> Properties, Abelian, Cyclic, Examples (Z,+), Finite Groups
        *   Ring -> Properties, Commutative, Unity, Integral Domain, Examples (Z,+,*), Polynomials
        *   Field -> Properties, Multiplicative Inverse, Examples (Q,R,C), Finite Fields (GF) -> Importance for AES
    *   Block Cipher Principles
        *   Definition (vs. Stream Cipher)
        *   Confusion -> S-Boxes
        *   Diffusion -> P-Boxes, Permutation, Mixing
        *   Product Ciphers
        *   Feistel Network -> Structure (Split, Round Func, XOR, Swap), DES Example, Decryption Property
    *   DES
        *   Specs (Block, Key Size, Rounds)
        *   Structure (IP, 16 Rounds, FP, Key Schedule)
        *   Round Detail (Expansion, Key XOR, S-Boxes, P-Box)
        *   Key Schedule (PC-1, Shifts, PC-2)
        *   Properties (Avalanche, Completeness)
        *   Weaknesses (Key Size, Weak/Semi-Weak Keys, Complement)
        *   Cryptanalysis (Brute-Force, Differential, Linear)
        *   Multiple DES (2DES -> MITM, 3DES -> EDE)
    *   AES (Rijndael)
        *   Specs (Block, Key Sizes, Rounds)
        *   Structure (SPN, Not Feistel) -> Cipher vs Inverse Cipher
        *   Data Units (Bit, Byte, Word, Block, State - 4x4 Matrix)
        *   Transformations -> SubBytes, ShiftRows, MixColumns (GF(2^8)), AddRoundKey
        *   Key Expansion (Word-based, Nk/Nr dependence, RotWord, SubWord, Rcon) -> AES-128, 192, 256 differences
        *   Security (vs Brute-Force, Linear/Differential, Side-Channel consideration)
        *   Advantages (Security, Speed, Cost, Flexibility)

