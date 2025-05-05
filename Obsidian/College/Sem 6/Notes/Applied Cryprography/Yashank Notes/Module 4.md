
# Module 4: Message Authentication and Digital Signatures

## Module Overview

This module focuses on ensuring the **authenticity** and **integrity** of digital messages. We will explore various techniques to verify that a message truly comes from the claimed sender and has not been altered in transit. This involves understanding hash functions, Message Authentication Codes (MACs), and the cornerstone of non-repudiation: Digital Signatures. We will also look at practical authentication systems like Kerberos and the infrastructure supporting public key usage (X.509).

**Topics Covered:**

*   **4.1 Message Authentication Approaches & Hash Functions:**
    *   Goals: Integrity, Originator Validation, Non-repudiation.
    *   Methods: Hash Functions, Message Encryption, MACs.
    *   **Hash Functions:**
        *   Definition and Purpose (Condensing, Fixed Size).
        *   Cryptographic Requirements (One-way, Collision-free).
        *   Security Properties (Preimage, Second Preimage, Collision Resistance).
        *   Structure and Attacks (Birthday Attack).
        *   Specific Algorithms: SHA family (SHA-1, SHA-2, SHA-3), MD5.
    *   **HMAC:** Hash-based Message Authentication Code.
*   **4.2 Authentication using Symmetric Encryption:**
    *   Using Encryption for Authentication.
    *   **Message Authentication Code (MAC):** Definition, Properties, Uses.
    *   MAC generation using Symmetric Ciphers (e.g., CBC-MAC).
    *   Data Authentication Algorithm (DAA) - Historical context.
    *   CMAC.
*   **4.3 Authentication using Public Key Cryptography:**
    *   **Digital Signatures:**
        *   Concept and Process (Signing with Private Key, Verifying with Public Key).
        *   Properties: Authentication, Integrity, Non-repudiation.
        *   Digital Signature Standard (DSS) and its algorithm (DSA).
        *   RSA Digital Signatures.
    *   **Authentication Applications:**
        *   Kerberos Authentication Protocol.
        *   X.509 Authentication Service (Certificates & PKI).

---

## 4.1 Message Authentication Approaches & Hash Functions

### Message Authentication Goals

**Message Authentication** is concerned with ensuring the trustworthiness of a received message. Key aspects include:

1.  **Integrity:** Protecting the message content from unauthorized modification (accidental or intentional) during transmission. Ensuring the message received is exactly the message sent.
2.  **Authenticity (Origin Validation):** Verifying the identity of the originator or sender of the message. Confirming the message came from the person or entity claimed.
3.  **Non-Repudiation (of Origin):** Providing proof that the claimed sender did indeed send the message, preventing them from later denying it (important for dispute resolution).

### Approaches to Message Authentication

There are three main functions used to achieve message authentication:

1.  **Hash Function:** Creates a fixed-size "digest" or "fingerprint" of the message. Changes to the message result in a different digest. Often combined with other techniques (like encryption or MACs) for full authentication.
2.  **Message Encryption:** Encrypting the entire message can provide authentication *if* a symmetric key is used. The receiver, knowing the shared key, can decrypt the message; successful decryption implies it came from the only other party knowing the key and that the content is likely unaltered (if it decrypts meaningfully). Public key encryption alone does *not* provide sender authentication.
3.  **Message Authentication Code (MAC):** A small, fixed-size block of data generated using the message *and* a secret key shared between sender and receiver. It's appended to the message to verify integrity and authenticity.

### Hash Functions

-   **Core Idea:** A hash function $H$ takes an **arbitrary-length message** $M$ as input and produces a **fixed-size output**, called a **hash value**, **message digest**, or simply **hash**.
    -   $h = H(M)$
-   **Purpose:** To condense the message into a short, representative fingerprint.
-   **Public Nature:** Hash functions themselves are typically public algorithms (like SHA-256, SHA-3); their security does not rely on the secrecy of the algorithm, but on their mathematical properties.
-   **Use Case (Integrity):** The primary use is to detect changes to a message. If $H(M) \neq H(M')$, then $M \neq M'$. Sending a message $M$ along with its hash $h=H(M)$ allows the receiver to recompute the hash on the received message $M'$ and check if $H(M') = h$. If they match, the message likely hasn't been altered.

![[Pasted image 20250506021558.png]]
This shows a variable-length Message M being processed by the Hash function H to produce a fixed-length Hash value h. This visually represents the compression aspect.*

#### Cryptographic Hash Functions

For security applications, we need **cryptographic hash functions**, which must possess specific properties making them resistant to attacks:

1.  **One-Way Property (Preimage Resistance):** Given a hash value $h$, it should be computationally infeasible to find *any* input message $M$ such that $H(M) = h$.
    -   *Analogy:* Easy to compute $h$ from $M$, but hard to compute $M$ from $h$. (Like scrambling an egg - easy to do, hard to reverse).
2.  **Collision-Free Property (Collision Resistance):** It should be computationally infeasible to find *two different* messages, $M_1$ and $M_2$, such that they produce the same hash value: $H(M_1) = H(M_2)$ where $M_1 \neq M_2$.

#### Properties of Hash Functions (General & Cryptographic)

1.  **Compression:** Maps arbitrarily long inputs to fixed-length outputs. 
2.  **Ease of Computation:** Computing $h = H(M)$ must be efficient for any given $M$. 
3.  **One-Way Encryption (Informal Term):** Hashing provides one-way transformation; you cannot "decrypt" a hash to get the original message. It's fundamentally different from encryption. Knowing hash '52' doesn't easily reveal the input 'hello', partly because many other inputs could potentially also hash to '52'. 
4.  **Avalanche Effect:** A small change in the input message (even one bit or character) should cause a drastic, unpredictable change in the output hash digest. 
    ![[Pasted image 20250506021635.png]] It shows slight variations of the "The red fox..." sentence producing vastly different hash outputs, visually demonstrating this property.*
5.  **Collision:** If two different messages $M_1 \neq M_2$ produce the same hash $H(M_1) = H(M_2)$, this is called a **collision**. Cryptographic hash functions aim to make finding collisions computationally infeasible. 
6.  **Fixed Output Length:** The hash digest always has the same length, regardless of the input message length. This prevents leaking information about the message length. 
7.  **Deterministic:** The same input message must always produce the exact same hash output.

#### Cryptographic Hash Function Requirements (Security Criteria)

A secure cryptographic hash function $H$ must satisfy three core resistance properties:

![[Pasted image 20250506021717.png]] 
It shows the three main requirements branching out: Preimage resistance, Second preimage resistance, Collision resistance.*

1.  **Preimage Resistance (One-Way Property):**
    -   *Goal:* Given a hash output $h$, it's computationally infeasible to find *any* input $M$ such that $H(M)=h$.
    -   *Attack Prevented:* Protects against an attacker who only knows the hash value and wants to find the original input. (Page 24)
    -   *Scenario:* If Eve intercepts only the hash $h(M)$, she shouldn't be able to find $M$ (or any $M'$ such that $h(M')=h(M)$). (Pages 22, 23)
    ![[Pasted image 20250506021744.png]] It illustrates an attacker Eve, given only the hash output Y=h(M), trying (and failing, if the function is secure) to find an input M' such that h(M')=Y.*

2.  **Second Preimage Resistance (Weak Collision Resistance):**
    -   *Goal:* Given an input message $M_1$, it's computationally infeasible to find a *different* input message $M_2$ ($M_2 \neq M_1$) such that $H(M_1) = H(M_2)$.
    -   *Attack Prevented:* Protects against forgery when the attacker has access to an original message and its hash. Ensures that if Alice sends $(M, H(M))$, Eve cannot find a different message $M'$ with the same hash $H(M')=H(M)$ and substitute $(M', H(M))$ without Bob noticing (assuming Bob verifies the hash). (Pages 25, 27)
    -   *Scenario:* Eve intercepts $(M, h(M))$. If she can find $M' \neq M$ where $h(M')=h(M)$, she can send $(M', h(M))$ to Bob, forging the message. (Page 26)
    ![[Pasted image 20250506021757.png]] 
    It shows Eve having access to M and h(M), then finding a different M' such that h(M')=h(M), and sending (M', h(M)) to Bob.*

3.  **Collision Resistance (Strong Collision Resistance):**
    -   *Goal:* It's computationally infeasible to find *any pair* of distinct inputs $M_1, M_2$ ($M_1 \neq M_2$) such that $H(M_1) = H(M_2)$.
    -   *Difference from Second Preimage:* Here, the attacker can choose *both* messages freely, whereas in second preimage, one message is fixed. Collision resistance is a stronger property and implies second preimage resistance (but not necessarily vice-versa).
    -   *Attack Prevented:* Protects against attacks where the attacker can trick a user into signing the hash of a message ($M_1$) whose content seems harmless, but the attacker has found another message ($M_2$, potentially malicious) that hashes to the same value. The signature for $M_1$ is then also valid for $M_2$. (Birthday Attack exploits this).
    ![[Pasted image 20250506021808.png]]
    It shows Eve's goal: Find any pair M and M' (where M is not equal to M') such that h(M)=h(M'). Notice Eve starts with "Given: none" - she doesn't need a pre-existing message or hash.

-   **Summary of Resistance Properties:**
    ![[Pasted image 20250506021831.png]] It concisely defines the input and goal for each resistance type:
        - *Preimage Resistance: Given H(M), Find M.*
        - *Second Preimage Resistance: Given M, Find M' != M such that H(M') = H(M).*
        - *Collision Resistance: Given Nothing, Find M, M' such that M != M' and H(M) = H(M').*
        
    ![[Pasted image 20250506021845.png]]This table summarizes the basic properties (Variable input, Fixed output, Efficiency) and the three resistance properties (Preimage, Second Preimage, Collision) along with Pseudorandomness.*

#### Attacks on Hash Functions

-   **Brute-Force Attacks:**
    -   **Preimage / Second Preimage:** Given a hash $h$ of length $m$ bits, finding an input $M$ such that $H(M)=h$ requires, on average, trying $2^m$ inputs.
    -   **Collision:** Finding *any* two inputs $M_1, M_2$ that collide ($H(M_1)=H(M_2)$) is significantly easier due to the **Birthday Paradox**. Requires approximately $2^{m/2}$ operations.
    -   **Implication:** To achieve $N$-bit security against collision attacks, a hash function needs an output size of at least $2N$ bits.
        -   128-bit hash (like MD5) has collision resistance strength of only $2^{64}$, which is considered inadequate.
        -   160-bit hash (like SHA-1) has collision resistance strength of $2^{80}$, which is suspect and practically broken.
-   **Birthday Attack:**
    -   Based on the **Birthday Paradox:** In a group of only 23 people, there's a >50% chance that two share the same birthday (out of 365 possibilities). Finding a match is much easier than finding someone with a *specific* birthday.
    -   **Application to Hash Collisions:** Finding two messages that hash to the same value is much easier than finding a message that hashes to a *specific* value.
    -   **Attack Scenario (against signatures):**
        1.  Alice is prepared to sign a legitimate message $x$.
        2.  Attacker Eve generates many variations $x'$ of $x$ that have the same meaning (e.g., by adding spaces, synonyms). Computes $H(x')$ for all variations ($\approx 2^{m/2}$ variations needed).
        3.  Eve also creates a fraudulent message $y$.
        4.  Eve generates many variations $y'$ of $y$ ($\approx 2^{m/2}$ variations). Computes $H(y')$ for all.
        5.  Eve compares the two sets of hashes ($H(x')$ and $H(y')$). Due to the birthday paradox, there's a high probability (>0.5) of finding a pair $(x'_i, y'_j)$ such that $H(x'_i) = H(y'_j)$.
        6.  Eve gives the valid variation $x'_i$ to Alice to sign. Alice signs it, producing a signature $S$ valid for $H(x'_i)$.
        7.  Eve takes the signature $S$ and attaches it to the fraudulent message $y'_j$. Since $H(x'_i) = H(y'_j)$, the signature $S$ is also valid for the fraudulent message $y'_j$.
    -   **Complexity:** Finding a collision takes roughly $O(N^{1/2})$ operations where $N=2^m$ is the number of possible hash outputs. Efficient search involves sorting lists ($O(N \log N)$).
    -   **Conclusion:** Requires hash functions with larger output sizes (e.g., 256 bits or more) to make the $2^{m/2}$ effort infeasible.
-   **Cryptanalytic Attacks:** Exploit specific structural weaknesses or properties of the hash algorithm (e.g., weaknesses in its internal compression function $f$) to find preimages or collisions faster than brute-force. (Page 36)
    ![[Pasted image 20250506021920.png]]Shows message blocks $Y_i$ being processed with the previous state $CV_{i-1}$ by the compression function $f$ to produce the next state $CV_i$. Attacks often focus on finding collisions within $f$.

#### Hash Function Uses (Summary)

-   **Message Integrity Check (MIC):**
    -   Send hash (digest) of message.
    -   Often, the MIC itself is encrypted for protection, message might be optional.
-   **Message Authentication Code (MAC):**
    -   Send a **keyed hash** (hash computed using message and a shared secret key).
    -   Provides integrity *and* authenticity.
    -   MAC and optionally message can be encrypted.
-   **Digital Signature:**
    -   Provides **non-repudiation** in addition to integrity and authenticity.
    -   Process: Hash the message, then **Encrypt** the hash with the sender's **private key**. (This encrypted hash is the signature).
    -   Verification: **Decrypt** the signature with the sender's **public key** to recover the original hash, re-hash the received message, and compare.
-   **Other Uses:**
    -   **Pseudorandom Function (PRF):** Generating session keys, nonces; deriving keys from passwords or master keys.
    -   **Pseudorandom Number Generator (PRNG):** Generating sequences of pseudorandom numbers (e.g., for Vernam cipher/OTP).
    -   **One-way Password Files:** Store hash of password instead of plaintext password (e.g., Unix `/etc/shadow`). **Salting** (adding unique random value per user before hashing) is crucial to deter precomputation attacks (like rainbow tables).
    -   **Intrusion/Virus Detection:** Store hashes of critical system files. Periodically re-hash files and compare to stored values to detect unauthorized modifications (e.g., Tripwire).

#### Simple (Insecure) Hash Examples

(Illustrating concepts, not for real use)

1.  **Bit-by-bit XOR:** Divide message into blocks $B_1, B_2, ..., B_m$. Hash $h = B_1 \oplus B_2 \oplus \dots \oplus B_m$.
    -   Also known as Longitudinal Redundancy Check (LRC).
    -   Reasonably effective for *data integrity* (detecting random errors).
    -   **Insecure:** Easy to find collisions (swap two blocks, result is the same) and preimages. Doesn't provide cryptographic security.
2.  **One-bit Circular Shift + XOR:** Initialize hash $h=0$. For each block $B_i$: rotate $h$ left by 1 bit, then $h = h \oplus B_i$.
    -   Better diffusion than simple XOR.
    -   Still good for data integrity.
    -   **Useless for security:** Easily broken, does not provide required cryptographic properties.

### Specific Hash Algorithms

#### Families

-   **MD Family (Message Digest):** Designed by Ron Rivest at RSA Labs. Includes MD2, MD4, **MD5**.
    -   MD2, MD4, MD5 are considered broken and insecure for cryptographic purposes.
-   **SHA Family (Secure Hash Algorithm):** Developed by NIST/NSA.
    -   SHA-0: Flawed initial version.
    -   SHA-1: 160-bit output. Widely used but now considered insecure (collisions demonstrated). Being phased out.
    -   SHA-2: Family including SHA-224, SHA-256, SHA-384, SHA-512. Based on similar structure to SHA-1 but with larger state/output. Currently considered secure.
    -   SHA-3: New standard (Keccak algorithm) selected via competition (2015). Different internal structure (sponge construction) than SHA-1/SHA-2. Offers same output sizes as SHA-2.
-   **RIPEMD:** Developed in Europe (RACE Integrity Primitives Evaluation). RIPEMD-160 is a common variant.

![[Pasted image 20250506022021.png]]Shows output sizes, input block sizes, rounds, and collision status (MD5 broken, SHA-1 not yet found but suspect).
![[Pasted image 20250506022031.png]]Compares Digest size, Max message size, Block size, Word size, and Number of steps/rounds for SHA-1, SHA-224, SHA-256, SHA-384, SHA-512.

#### MD5 (Message Digest 5)

-   **Purpose:** Cryptographic hash function, widely used historically for verifying data integrity (checksums).
-   **Output:** 128-bit hash value.
-   **Working Steps:**
    1.  **Padding:** Append bits to the message so its total length is 64 bits less than a multiple of 512. Padding starts with a '1' bit, followed by '0' bits.
    2.  **Append Length:** Append the original message length (before padding) as a 64-bit value. The total length is now a multiple of 512 bits.
    3.  **Initialize Buffer (IV):** Uses four 32-bit registers (A, B, C, D) initialized with fixed hexadecimal constants.
        -   A=0x67452301, B=0xEFCDAB89, C=0x98BADCFE, D=0x10325476
    4.  **Process Blocks:** Process the message in 512-bit (64-byte) blocks. Each block undergoes 4 rounds of processing (16 steps per round = 64 steps total).
    5.  **Rounds:** Each round uses a different non-linear function (F, G, H, I) and combines the buffer values (A,B,C,D), a 32-bit message word from the current block, and a round constant. Includes bitwise operations (AND, OR, XOR, NOT) and left rotations.
        ![[Pasted image 20250506022058.png]]Shows the four registers A,B,C,D, the message block Mi, constant Ki, the function F, addition modulo 2^32, and rotation <<<s. Lists the formulas for the four round functions F1-F4.
    6.  **Update Buffer:** After processing a block, the output is added (modulo $2^{32}$) to the initial buffer values for that block.
    7.  **Final Hash:** After processing all blocks, the final values in the A, B, C, D registers are concatenated to form the 128-bit MD5 digest.
    ![[Pasted image 20250506022129.png]]Shows the message padding, blocking, iterative processing with the 128-bit buffer (CVq/HMD5), and final digest.
    ![[Pasted image 20250506022203.png]]Describes the flow of data between registers A,B,C,D and the application of F, G, H, I functions.
-   **Security:** **Broken.** Significant vulnerabilities, especially **collision attacks**, have been demonstrated. Finding two different inputs that produce the same MD5 hash is computationally feasible. **MD5 should NOT be used for security-critical applications** (like digital signatures, password hashing, certificate validation).
-   **Strengths/Current Uses:**
    -   Still sometimes used for non-cryptographic purposes like **checksums** to verify file integrity against accidental corruption (where malicious collision resistance isn't needed).
    -   Relatively **fast**.
    -   Used in some **legacy systems** (though migration is strongly recommended).

#### SHA (Secure Hash Algorithm) Family

-   **SHA-1:**
    -   Designed by NIST/NSA (1995, FIPS 180-1).
    -   Produces a **160-bit** hash value.
    -   Based on MD4 design principles.
    -   **Security:** Considered **insecure**. Practical collision attacks have been demonstrated (e.g., SHAttered attack by Google/CWI in 2017). Should be phased out and replaced by SHA-2 or SHA-3.
-   **SHA-2:**
    -   NIST revision (2002, FIPS 180-2 onwards).
    -   Includes **SHA-224, SHA-256, SHA-384, SHA-512** (and SHA-512/224, SHA-512/256).
    -   Designed for compatibility with AES key sizes (SHA-256 for AES-128, SHA-384 for AES-192, SHA-512 for AES-256).
    -   Similar internal structure to SHA-1 but with larger internal state, more rounds, different constants/shift amounts, making it much stronger.
    -   Currently considered **secure**, with no practical attacks known. Widely used.
-   **SHA-3:**
    -   Result of a NIST competition (started 2007, winner Keccak announced 2012, standard FIPS 202 published 2015).
    -   Motivated by concerns about the long-term security of SHA-2 due to its structural similarity to SHA-1/MD5.
    -   Based on the **Keccak** algorithm, uses a different internal structure (**sponge construction**) than SHA-1/SHA-2 (Merkle-Damgård structure).
    -   Offers same output sizes as SHA-2 (SHA3-224, SHA3-256, SHA3-384, SHA3-512) plus extendable-output functions (SHAKE).
    -   Intended as an alternative, not immediate replacement, for SHA-2.

#### SHA-512 In Detail

-   **Output:** 512 bits (64 bytes).
-   **Purpose:** Cryptographic hashing, password hashing, digital record verification. High resistance to attacks expected due to large output size.
-   **Stages:**
    1.  **Input Formatting:**
        -   Message is padded similar to MD5: append '1', then '0's until length is 128 bits less than a multiple of 1024.
        -   Append original message length as a **128-bit** value.
        -   Total padded message length is a multiple of 1024 bits.
        -   Message is processed in **1024-bit blocks**.
        -   Internal operations use **64-bit words**. (1024 bits = 16 words).
        ![[Pasted image 20250506022259.png]]Shows Original Message + Padding (10...0) + Length (128 bits) = Multiple of 1024 bits.
        ![[Pasted image 20250506022314.png]]Shows a 1024-bit block as 16 x 64-bit words, and the 512-bit digest as 8 x 64-bit words.
    2.  **Hash Buffer Initialization:**
        -   Uses an 8-word (512-bit) buffer (registers a, b, c, d, e, f, g, h).
        -   Initialized with an **Initialization Vector (IV)** derived from the fractional parts of the square roots of the first 8 primes (2, 3, 5, ..., 19).
        ![[Pasted image 20250506022326.png]]Shows the 8 registers and their initial 64-bit hexadecimal values.
    3.  **Message Processing:**
        -   Heart of the algorithm: Processes the 1024-bit message blocks one by one.
        -   Each block is processed through **80 rounds**.
        -   **Message Schedule:** The 16 words (W<sub>0</sub>-W<sub>15</sub>) from the current 1024-bit block are expanded into 80 words (W<sub>0</sub>-W<sub>79</sub>) using a specific mixing formula involving previous words and bitwise operations (rotations, shifts).
        ![[Pasted image 20250506022356.png]]Shows how Wt for t>=16 is calculated from previous W values.
        -   **Round Function:** In each round $t$ (0 to 79):
            -   Inputs: The 8 buffer registers (a-h), the scheduled message word $W_t$, and a round constant $K_t$.
            -   Complex mixing operations involving bitwise functions (Ch, Maj), modular addition (mod $2^{64}$), and bitwise rotations ($\Sigma_0, \Sigma_1$).
            -   Updates the 8 buffer registers.
        ![[Pasted image 20250506022414.png]]
        Shows the 80 rounds operating on the buffer, taking Wt and Kt as input, with final addition.
        
        ![[Pasted image 20250506022435.png]]Shows the flow of data between registers a-h, incorporating Ch, Maj, Sigma functions, Wt, Kt, and modular additions.
        -   **Round Constants $K_t$:** 80 predefined 64-bit constants derived from the fractional parts of the cube roots of the first 80 primes.
        
        ![[Pasted image 20250506022450.png]]
        -   **Output of Block Processing:** After 80 rounds, the resulting buffer values (a-h) are added (modulo $2^{64}$) to the *input* buffer values for that block (which was the output of the *previous* block, or the IV for the first block). This produces the input buffer for the *next* block.
    4.  **Output:**
        -   After processing the final message block, the final 512-bit value in the hash buffer (concatenation of registers a-h) is the SHA-512 digest.
    ![[Pasted image 20250506022600.png]]Provides a good high-level view of the entire process from formatted input to final hash.
    ![[Pasted image 20250506022620.png]]simplified compression function diagram from page 71.
    
    ![[Pasted image 20250506022639.png]]
-   **SHA-512 Security:**
    -   Currently no known practical attacks (preimage, second preimage, collision).
    -   Considered very secure due to its large state and output size.
    -   Often faster than SHA-256 on 64-bit architectures.
-   **Applications:** Secure password hashing (often preferred over SHA-256), digital signatures, integrity verification, blockchain projects (e.g., BitShares, LBRY Credits, Kcash), authentication (e.g., Rwandan genocide archive video).

### Section Summary: Hash Functions

-   **Goal:** Create fixed-size digest of variable-size message for integrity checks.
-   **Cryptographic Properties:** Preimage Resistance (One-Way), Second Preimage Resistance (Weak Collision), Collision Resistance (Strong Collision).
-   **Attacks:** Brute-force (preimage $2^m$, collision $2^{m/2}$), Birthday Attack (exploits $2^{m/2}$ collision probability), Cryptanalysis (exploits algorithm structure).
-   **Algorithms:**
    -   MD5: 128-bit, Fast, **Broken (collisions easy)**. Use only for non-crypto checksums.
    -   SHA-1: 160-bit, **Insecure (collisions demonstrated)**. Phase out.
    -   SHA-2 (SHA-256, SHA-512, etc.): Currently **Secure and Recommended**.
    -   SHA-3 (Keccak): New standard, different structure, **Secure**.
-   **Uses:** Integrity (MIC), Authentication+Integrity (MAC, Digital Sig), Passwords, PRNG/PRF.

---

## 4.2 Using Symmetric Encryption for Message Authentication

While hash functions are common, message authentication can also be achieved using symmetric encryption or dedicated MAC algorithms built from symmetric ciphers.

### Authentication via Symmetric Encryption

-   **Principle:** If a message is encrypted with a symmetric key shared only between Alice and Bob, successful decryption by Bob implies the message likely originated from Alice (authenticity) and hasn't been altered (integrity, assuming it decrypts to something meaningful).
-   **Requirements:**
    -   Receiver (Bob) must know the sender (Alice) is the only other party with the key.
    -   Message needs structure (e.g., known format, error detection code, checksum) so Bob can recognize if decryption yields valid plaintext vs. garbage (detecting alterations).
![[Pasted image 20250506022706.png]]
Shows Alice encrypting M with key K, sending E(K,M). Bob decrypts with K to get M. Implicitly provides confidentiality and authentication.

### Message Authentication Code (MAC)

-   **Definition:** A **MAC** is a small fixed-size block of data (the "tag") generated by a **MAC algorithm** using two inputs: the message $M$ and a **secret key $K$** shared between sender and receiver.
    -   $MAC = C_K(M)$ or $MAC = C(K, M)$
-   **Purpose:** To provide **message integrity** and **data origin authentication**. It does *not* inherently provide confidentiality (the message itself might be sent in plaintext).
-   **Process:**
    1.  **Sender:** Computes $MAC = C_K(M)$ using the shared secret key $K$. Appends the MAC tag to the original message $M$. Sends $(M, MAC)$.
    2.  **Receiver:** Receives $(M', MAC')$. Uses the same shared secret key $K$ and the same MAC algorithm $C$ to compute a new MAC based on the received message $M'$: $MAC_{computed} = C_K(M')$.
    3.  **Verification:** Compares the received $MAC'$ with the computed $MAC_{computed}$.
        -   If $MAC' = MAC_{computed}$, the receiver accepts the message as authentic (from the key holder) and unaltered.
        -   If they don't match, the message is rejected (either altered or not from the expected sender).
![[Pasted image 20250506022742.png]] Shows Sender A computing C(K,M) and sending M || MAC. Receiver B recomputes C(K,M') and compares.

![[Pasted image 20250506022757.png]]Visually contrasts the Sender (Key + Message -> MAC Algo -> MAC) and Receiver (Key + Message -> MAC Algo -> MAC -> Compare) sides.

-   **Properties:**
    -   MAC is a **cryptographic checksum**.
    -   Condenses variable-length message $M$ using secret key $K$ to a fixed-size authenticator tag.
    -   It's a **many-to-one function** (multiple messages could potentially map to the same MAC, but finding such collisions should be hard without the key).
-   **Why use MAC?**
    -   Sometimes only authentication/integrity is needed, not confidentiality (faster than encrypting).
    -   Authentication might need to persist longer than confidentiality (e.g., verifying archived messages).
-   **MAC vs. Digital Signature:**
    -   MAC uses a **symmetric (shared) secret key**.
    -   Digital Signature uses an **asymmetric (private/public) key pair**.
    -   **Crucially, a MAC does NOT provide non-repudiation.** Since both sender and receiver share the same key $K$, either could have generated the MAC. The receiver cannot prove to a third party that the sender *must* have created it. Digital signatures, using the sender's private key, *do* provide non-repudiation.

#### Requirements for MACs

A secure MAC function $C(K, M)$ should satisfy:

1.  **Computational Resistance:** Knowing a message $M$ and its MAC tag $T = C(K, M)$, it should be computationally infeasible to find another message $M' \neq M$ such that $C(K, M') = T$, *without knowing the secret key K*. (This prevents forgery).
2.  **Uniform Distribution:** MAC values should appear randomly distributed. An attacker shouldn't be able to predict MAC values.
3.  **Input Dependence:** The MAC should depend equally on all bits of the message. Changing any bit in $M$ should significantly change the MAC value in an unpredictable way.

#### Security of MACs

-   **Brute-Force Attacks:**
    -   **On the Key:** Attacker has known $(M, T)$ pairs. Can try all possible keys $K'$ until $C_{K'}(M) = T$. Requires $2^k$ effort, where $k$ is the key size.
    -   **On the MAC value:** Attacker tries to guess the MAC value $T$ for a given message $M$. If the MAC length is $m$ bits, this requires $2^m$ attempts on average. However, similar to hash functions, birthday-style attacks can find collisions between MAC outputs (if the attacker can get many messages MACed with the same key) in $\approx 2^{m/2}$ effort.
    -   **Recommendation:** Need a sufficiently large MAC size ($m \ge 128$ bits recommended) and key size ($k$).
-   **Cryptanalytic Attacks:** Exploit structural weaknesses in the specific MAC algorithm (e.g., based on the underlying hash or block cipher). Goal is to make brute-force the best option. MACs have more variety than hash functions, making general cryptanalysis harder.

#### Combining MACs and Encryption

To achieve both confidentiality and authentication/integrity:

-   Use **separate keys** for encryption ($K_E$) and MAC ($K_M$). Using the same key for both can lead to vulnerabilities.
-   Three main approaches (Generic Composition):
    1.  **Encrypt-then-MAC (EtM):** Encrypt $M$ to get $C=E(K_E, M)$. Compute MAC on ciphertext $T=MAC(K_M, C)$. Send $(C, T)$. **Generally considered the most secure approach.**
    2.  **MAC-then-Encrypt (MtE):** Compute $T=MAC(K_M, M)$. Encrypt both $C=E(K_E, (M \| T))$. Send $C$.
    3.  **Encrypt-and-MAC (E&M):** Encrypt $M$ to get $C=E(K_E, M)$. Compute $T=MAC(K_M, M)$. Send $(C, T)$.
-   While conceptually simple, subtle vulnerabilities can exist depending on the specific algorithms and modes used. **Authenticated Encryption (AE)** modes (like AES-GCM, ChaCha20-Poly1305) are specifically designed to provide both confidentiality and integrity/authentication simultaneously and securely, and are generally preferred.

![[Pasted image 20250506022839.png]](b) shows MAC-then-Encrypt (MAC tied to plaintext). (c) shows Encrypt-and-MAC (MAC tied to plaintext, sent alongside ciphertext).

#### MAC Construction Methods

MACs can be built from two main cryptographic primitives:

1.  **Cryptographic Hash Functions:** e.g., **HMAC**.
2.  **Symmetric Block Ciphers:** e.g., **DAA (CBC-MAC)**, **CMAC**.

#### HMAC (Hash-based MAC)

-   **Concept:** Uses a standard cryptographic hash function (like SHA-256) combined with a secret key to produce a MAC.
-   **Design Objectives:**
    -   Use existing hash functions without modification.
    -   Allow easy replacement of the underlying hash function (e.g., swap SHA-256 for SHA-512).
    -   Maintain performance close to the original hash function.
    -   Handle keys simply.
    -   Have well-understood security properties based on the hash function.
-   **Standard:** RFC 2104.
-   **Structure:** Involves hashing the message twice, incorporating the key in both steps using specific padding constants (`ipad`, `opad`).
    -   `ipad` = Inner padding key (0x36 repeated block size times)
    -   `opad` = Outer padding key (0x5C repeated block size times)
    -   $K^+$ = Secret key $K$ padded with zeros to match the hash function's block size ($b$ bits).
    -   **Formula:**
        $$ HMAC_K(M) = H( (K^+ \oplus opad) \| H( (K^+ \oplus ipad) \| M ) ) $$
        *(Where H is the hash function, $\|$ denotes concatenation, $\oplus$ is XOR)*
-   **Working:**
    1. Pad key $K$ to block size $b$, get $K^+$.
    2. Compute inner hash: $H_{inner} = H( (K^+ \oplus ipad) \| M )$.
    3. Compute outer hash (final HMAC): $HMAC = H( (K^+ \oplus opad) \| H_{inner} )$.
    <!-- Instruct user to paste diagrams from pages 87, 88, 120 here -->
    ![[Pasted image 20250506022906.png]]Shows the two-stage hashing process involving ipad and opad XORed with the padded key.
    
    ![[Pasted image 20250506022929.png]]the HMAC construction diagram. Provides another view of the nested hash structure.

-   **Security:** Proven to be secure if the underlying hash function has certain properties (e.g., collision resistance is desirable but not strictly necessary for HMAC security itself). Much harder to attack than simple `Hash(Key|Message)` due to the two-pass structure preventing length extension attacks. Security depends on key secrecy and hash function strength. Brute force on the key or birthday attacks on the output size are the main concerns.

#### MACs based on Block Ciphers

-   Can use block ciphers (like DES, AES) in a chaining mode to produce a MAC.
-   **DAA (Data Authentication Algorithm):**
    -   Former US standard based on **DES-CBC**.
    -   Process: Encrypt the message using DES in CBC mode with IV=0. The MAC (called DAC - Data Authentication Code) is the final encrypted block (or a truncated portion of it).
    -   Message padded to multiple of 64 bits.
    -   **Security:** Considered **insecure** now due to DES's small block size (64 bits) making the MAC output too short (vulnerable to birthday attacks) and reliance on DES itself. Withdrawn in 2008.
    ![[Pasted image 20250506022949.png]]Shows the standard CBC encryption chain using key K, with the final block O_N being used (possibly truncated) as the DAC.
    
    ![[Pasted image 20250506023006.png]]
    showing the CBC recurrence.
-   **CMAC (Cipher-based MAC):**
    -   Modern standard (NIST SP 800-38B) designed to overcome DAA/CBC-MAC limitations.
    -   Based on CBC mode but with modifications using **two keys** ($K_1, K_2$ derived from the main key $K$) and specific padding handling for the last block (depending on whether it's a full block or partial block).
    -   Can use AES or Triple DES as the underlying block cipher.
    -   Addresses security issues of basic CBC-MAC. Widely used and considered secure.
    ![[Pasted image 20250506023032.png]]Shows two cases: (a) Message length is integer multiple of block size (last block XORed with K1 before final encryption). (b) Message length is not integer multiple (padding applied, last block XORed with K2 before final encryption). The output T is the MAC.

### Section Summary: Symmetric Authentication

-   **Via Encryption:** Possible if key is shared only by two parties and message has structure. Provides confidentiality too.
-   **MAC:** Provides integrity and authenticity using a shared secret key, but not confidentiality or non-repudiation.
    -   $MAC = C_K(M)$. Sender computes and appends; receiver recomputes and compares.
    -   Requires key secrecy, resistance to finding $M'$ with same MAC, uniform distribution, dependency on all message bits.
    -   Vulnerable to key brute force and birthday attacks on MAC output size.
-   **Construction:**
    -   **HMAC:** Uses hash functions (SHA-2, SHA-3). Secure due to nested structure with key. $H((K\oplus opad)\|H((K\oplus ipad)\|M))$.
    -   **Block Cipher MACs:**
        -   DAA (DES-CBC): Old, insecure (64-bit output).
        -   CMAC (AES/TDES-CBC variant): Secure, handles padding properly using derived keys.

---

## 4.3 Using Public Key for Authentication & Digital Signatures

Public key cryptography provides powerful tools for authentication, especially **digital signatures**, which offer properties beyond simple MACs.

### Digital Signatures

-   **Definition:** A cryptographic technique using asymmetric keys to verify the **authenticity**, **integrity**, and crucially, **non-repudiation** of a digital message or document.
-   **Analogy:** The digital equivalent of a handwritten signature, but with much stronger security properties.
-   **Purpose:**
    -   Prove that a message came from the claimed sender (Authentication).
    -   Prove that the message was not altered after being signed (Integrity).
    -   Prevent the sender from falsely denying they sent the message (Non-repudiation).

#### Digital Signature Process

![[Pasted image 20250506023112.png]]
Shows Alice using a Signing Algorithm on Message M to produce Signature S. Sends (M, S). Bob uses a Verifying Algorithm on (M, S) to Accept/Reject.

![[Pasted image 20250506023126.png]]Alice uses her *Private Key* with the Signing Algorithm. Bob uses Alice's *Public Key* with the Verifying Algorithm.

1.  **Signing (by Sender Alice):**
    a.  Alice has a public/private key pair ($PU_a, PR_a$).
    b.  Typically, Alice first **hashes** the message $M$ to get a fixed-size digest $h = H(M)$.
    c.  Alice then uses her **private key $PR_a$** and a signing algorithm (often based on public key encryption, like RSA, or dedicated algorithms like DSA/ECDSA) to "encrypt" or transform the hash $h$. This result is the **digital signature $S$**.
        -   Example (RSA): $S = h^{d_a} \pmod{n_a}$
    d.  Alice sends the original message $M$ along with the signature $S$ to the receiver Bob.
2.  **Verification (by Receiver Bob):**
    a.  Bob receives $M'$ and $S'$.
    b.  Bob obtains Alice's authentic **public key $PU_a$**.
    c.  Bob applies the verification algorithm (the inverse of signing, using $PU_a$) to the received signature $S'$ to recover the original hash value $h'$.
        -   Example (RSA): $h' = (S')^{e_a} \pmod{n_a}$
    d.  Bob independently computes the hash of the received message $M'$ using the same hash function $H$: $h_{computed} = H(M')$.
    e.  **Comparison:** Bob compares the recovered hash $h'$ with the computed hash $h_{computed}$.
        -   If $h' = h_{computed}$, the signature is **valid**. Bob concludes the message genuinely came from Alice and was not altered.
        -   If they don't match, the signature is **invalid**. The message is rejected (either forged or altered).

![[Pasted image 20250506023148.png]]Clearly shows the "Sign the Digest" process: Alice hashes M, then signs H(M) with her private key. Bob verifies by checking if decrypting S with Alice's public key yields the same hash H(M) he computes himself.

![[Pasted image 20250506023255.png]]

![[Pasted image 20250506023201.png]]Shows how to add confidentiality: Alice first signs M (or H(M)) with PR_a, then encrypts the message+signature using Bob's public key PU_b. Bob decrypts with PR_b, then verifies the signature with PU_a.

#### Key Usage Clarification

-   **Signing:** Uses the **SIGNER's PRIVATE KEY**. Only the owner of the private key can create the signature.
-   **Verification:** Uses the **SIGNER's PUBLIC KEY**. Anyone can verify the signature if they have the correct public key.
-   **Why not Symmetric Keys?**
    -   Key sharing limits applicability (can't easily verify with third parties).
    -   No non-repudiation (either party sharing the key could have created the "signature").
    -   Using signatures for session key setup creates circular dependencies.

#### Key Benefits

1.  **Authentication:** Verifies the sender's identity (only the holder of the private key could create a valid signature).
2.  **Data Integrity:** Ensures the message hasn't been tampered with since signing (any change invalidates the hash comparison).
3.  **Non-Repudiation:** Provides strong evidence that the sender created the message, preventing them from denying it later (crucial legally).

#### Limitations

-   **Does Not Provide Confidentiality:** Signing a message doesn't hide its content. If confidentiality is needed, the message (and potentially the signature) must be encrypted separately, typically using the receiver's public key or a symmetric session key.

#### Digital Signatures vs. Digital Certificates

-   **Related but Different:** Both use public key crypto, but serve distinct roles.
-   **Digital Signature:** A cryptographic value attached to a message to prove **authenticity, integrity, and non-repudiation** of that *specific message*. Created by the *sender* using their private key.
-   **Digital Certificate:** An electronic document issued by a trusted **Certificate Authority (CA)** that **binds a public key to an identity** (person, server, organization). Its purpose is to allow others to reliably obtain and trust someone's public key. The certificate *itself* is digitally signed by the CA.
![[Pasted image 20250506023310.png]]Contrasts conventional vs digital signatures on Inclusion, Verification Method, Relationship, Duplicity.

![[Pasted image 20250506023325.png]]Highlights Purpose, Components, Process, Usage, Issuer, Application, Example for both.

### Digital Signature Standard (DSS)

-   **Origin:** A US Federal Information Processing Standard (FIPS 186) published by NIST (originally 1991, revised 1993, 1994 adopted).
-   **Purpose:** Provides a standard for generating and verifying digital signatures, but **not** for encryption or key exchange.
-   **Algorithm:** Specifies the **Digital Signature Algorithm (DSA)**.
    -   DSA is based on the mathematical difficulty of the **Discrete Logarithm Problem (DLP)**, similar to Diffie-Hellman and ElGamal. It incorporates ideas from ElGamal and Schnorr signature schemes.
    -   Uses the **Secure Hash Algorithm (SHA)** (originally SHA-1, now typically SHA-2) to hash the message before signing.
-   **Components:** A digital signature scheme involves three algorithms:
    1.  **Key Generation (G):** Creates a public/private key pair (pk, sk).
    2.  **Signing (S):** Takes the private key (sk) and a message (or hash) (x) to produce a signature tag (t). $t = S(sk, x)$.
    3.  **Verifying (V):** Takes the public key (pk), the message (or hash) (x), and the tag (t). Outputs 'accept' or 'reject'. $V(pk, x, t)$.
-   **DSA Specifics:**
    -   **Key Generation:** Involves selecting primes $p$ (large, e.g., 1024-3072 bits) and $q$ (smaller, e.g., 160-256 bits) such that $q$ divides $p-1$. Also involves a generator $g$ (related to $e_1$ in notes) and computing public/private key components ($y=e_2, x=d$). Public key: $(p, q, g, y)$. Private key: $x$.
    -   **Signing:** Requires generating a **per-message random secret $k$**. Produces a two-part signature $(r, s)$ (corresponding to $S_1, S_2$ in notes). $r = (g^k \pmod p) \pmod q$. $s = [k^{-1}(H(M) + xr)] \pmod q$.
    -   **Verification:** Takes message $M$, signature $(r, s)$, and public key $(p, q, g, y)$. Involves several calculations, including computing $w = s^{-1} \pmod q$, $u_1 = (H(M)w) \pmod q$, $u_2 = (rw) \pmod q$, and finally $v = ((g^{u_1} y^{u_2}) \pmod p) \pmod q$. Accepts if $v=r$.
    
    ![[Pasted image 20250506023359.png]]![[Pasted image 20250506023414.png]] 
    Shows the signing and verification steps involving hash H, signing function Sig (using private key d, random k), verification function Ver (using public key PU), and comparison.

    ![[Pasted image 20250506023438.png]]Shows the three functions f1, f2, f3 and the use of moduli p and q.
-   **DSS vs RSA Signatures:**
    -   DSS signing is generally faster than RSA signing (for comparable security levels).
    -   RSA verification is generally faster than DSS verification.
    -   DSS signatures are typically smaller than RSA signatures (e.g., 320-512 bits for DSS vs 2048+ bits for RSA).
-   **Criticisms:** Initial concerns about secrecy of design process and small prime size (originally fixed 512-bit $p$), though later versions allow larger sizes.

### RSA Digital Signature Scheme

-   **Mechanism:** Leverages the standard RSA algorithm, but "reverses" the key usage.
    -   **Signing:** Sender computes $h = H(M)$, then uses their **private key** $(d, n)$ to compute the signature $S = h^d \pmod n$.
    -   **Verification:** Receiver computes $h' = S^e \pmod n$ using the sender's **public key** $(e, n)$, recomputes $H(M)$, and checks if $h' = H(M)$.
    ![[Pasted image 20250506023514.png]]
    ![[Pasted image 20250506023524.png]]
    Shows the signing function $f(M,d,n)=S$ and verification $f(S,e,n)=M'$, comparing M' to M.
    
    ![[Pasted image 20250506023603.png]]Shows the preferred method: Hash M first, then sign the digest $D=H(M)$ using the private key: $S = D^d \pmod n$. Verification decrypts $S$ with public key to get $D'$, computes $H(M)$, and checks $D' == H(M)$.
-   **Note:** As with RSA encryption, using **padding schemes** (like RSASSA-PSS) is crucial for security.

### Other Signature Concepts

-   **Time-Stamped Signatures:** Adding a trusted timestamp to a signature to prevent replay attacks and establish time of signing.
-   **Blind Signatures:** Allow a user to get a message signed by an authority *without revealing the message content* to the authority. Useful for privacy-preserving applications like digital cash. (Invented by David Chaum).
-   **Undeniable Signatures:** (Chaum/Van Antwerpen) A type where the signer must actively participate in the verification process (using a challenge-response protocol). This prevents offline verification and duplication but requires the signer to be online. Includes a disavowal protocol for the signer to prove a signature is forged.

### Section Summary: Public Key Authentication & Signatures

-   **Digital Signatures:** Provide Authentication, Integrity, Non-Repudiation using asymmetric keys. Signer uses private key, verifier uses public key. Usually sign the hash of the message. Does not provide confidentiality.
-   **DSS:** US standard for digital signatures (FIPS 186), uses DSA algorithm based on DLP. Requires per-message random number.
-   **RSA Signatures:** Use RSA algorithm with reversed key roles ($S=H(M)^d \pmod n$). Requires padding (e.g., PSS).
-   **Comparison:** Digital signatures are distinct from digital certificates (which bind keys to identities).

---

## 4.4 Authentication Applications

### X.509 Authentication Service (PKI)

*(This builds upon previous concepts related to certificates)*

-   **X.509 Standard:** Defines the format for **public key certificates**, Certificate Revocation Lists (CRLs), and related procedures. It's the foundation for most **Public Key Infrastructure (PKI)** implementations.
-   **PKI:** The set of roles, policies, hardware, software, and procedures needed to create, manage, distribute, use, store, and revoke digital certificates and manage public-key encryption.
-   **Goal:** To enable secure use of public key cryptography by providing a trustworthy way to associate public keys with identities.

#### Key Components of X.509 / PKI

1.  **Digital Certificates:** Bind identity to a public key, signed by a CA. (Format shown on page 180). Contains:
    -   Version Number
    -   Serial Number (unique per CA)
    -   Signature Algorithm ID (used by CA to sign)
    -   Issuer Name (the CA)
    -   Validity Period (Not Before, Not After dates)
    -   Subject Name (the certificate holder)
    -   Subject Public Key Info (the key itself + algorithm)
    -   Optional Fields (Issuer/Subject Unique IDs, Extensions)
    -   CA's Digital Signature
2.  **Certification Authorities (CAs):** Trusted entities that issue and manage certificates.
    -   **Hierarchy:** Often structured hierarchically. A **Root CA** is implicitly trusted (its public key is often pre-installed in browsers/OS). Root CAs sign certificates for **Intermediate CAs**, who in turn can sign certificates for other intermediates or for **End-Entities** (users, servers).
    -   **Trust Chain:** To verify an end-entity certificate, a user traces the signatures back up the chain to a trusted root CA.
    ![[Pasted image 20250506023634.png]]
    ![[Pasted image 20250506023649.png]]shows cross-certification between roots.
    
3.  **Registration Authorities (RAs):** Optional entities that can verify identity information on behalf of a CA before a certificate is issued.
4.  **Certificate Revocation Lists (CRLs):** Lists containing the serial numbers of certificates that have been revoked by the CA *before* their scheduled expiration date.
    -   **Reasons for Revocation:** Private key compromise, user affiliation change, CA compromise, etc. (Page 183)
    -   **Process:** CAs periodically issue signed CRLs. Relying parties should check the relevant CRL before trusting a certificate. (Page 184)
    -   **Format:** Similar structure to certificates, lists revoked serial numbers and revocation dates. (Page 182)
    -   **Delta CRLs:** Smaller, more frequent updates containing only changes since the last full CRL. (Page 181)
    -   **Importance:** Ensure users don't rely on compromised/invalid certificates. (Page 185)
    -   **Alternative:** Online Certificate Status Protocol (OCSP) provides real-time revocation checks.
5.  **Certificate Management Protocols:** Standards for handling certificates (e.g., requesting, renewing).

#### Trust in X.509

-   Trust originates from **Root CAs**. Users/systems must have a list of trusted root CA public keys.
-   **Certificate Chains** (paths) allow verification of certificates issued by unknown intermediate CAs by tracing back to a trusted root. (Page 171 Example).
-   **Revocation Checking** (CRL/OCSP) is essential to handle compromised certificates.

#### Applications of X.509 Infrastructure

-   **SSL/TLS:** Securing web traffic (HTTPS). Server presents certificate to browser.
-   **S/MIME:** Secure email (signing and encryption).
-   **Code Signing:** Authenticating software publishers and ensuring code integrity.
-   **VPNs:** Establishing secure network connections.
-   IPSec

#### Challenges

-   **Security:** Protecting CA private keys is paramount. Ensuring proper identity verification.
-   **Trust Management:** Which CAs to trust? How is trust established/revoked?
-   **Scalability:** Managing millions or billions of certificates and timely revocation information.
-   **Compliance:** Meeting legal and industry standards.
-   **Future:** Impact of quantum computing, need for post-quantum certificates, improving PKI usability.

### Kerberos

-   **Purpose:** A network **authentication protocol** designed to provide strong authentication for client/server applications using **secret-key (symmetric) cryptography**.
-   **Goal:** Allow users (clients) to prove their identity to servers, and servers to prove their identity to clients, across an insecure network, without sending passwords over the network.
-   **Origin:** Developed at MIT in the 1980s. Widely used (e.g., in Microsoft Windows Active Directory). Named after the three-headed dog from Greek mythology (representing Client, Server, KDC).
-   **Architecture:** Relies on a **trusted third party**, the **Key Distribution Center (KDC)**. The KDC consists of two logical parts:
    1.  **Authentication Server (AS):** Handles initial client authentication. Verifies user credentials (usually password-derived key). Issues Ticket-Granting Tickets (TGTs).
    2.  **Ticket-Granting Server (TGS):** Issues tickets (Service Tickets) for specific services on behalf of users who present a valid TGT.
-   **Key Concepts:**
    -   **Tickets:** Encrypted data structures containing credentials (like session keys) that allow a client to access a service. Cannot be easily read or forged by others.
    -   **Authenticator:** Time-stamped data, encrypted with a shared session key, used to prove the client's identity recently and prevent replay attacks.
    -   **Session Keys:** Temporary symmetric keys shared between client-KDC or client-server for securing communication during a session.
    -   **Realms:** Kerberos domains. KDCs manage keys for principals within their realm. Cross-realm authentication is possible.

#### Kerberos Protocol Flow (Simplified - v4/v5)

![[Pasted image 20250506023730.png]]Shows User interacting with Kerberos (AS/TGS) and then the Server.

![[Pasted image 20250506023747.png]]
![[Pasted image 20250506023759.png]]
Shows the numbered steps between User(Alice), KDC(AS/TGS), and Server(Bob).

![[Pasted image 20250506023823.png]]
Shows Client Auth, Service Auth, and Service Request phases with message contents.

1.  **Initial Authentication (Client -> AS):**
    -   User logs in (e.g., enters password on workstation). Client derives a secret key from the password.
    -   Client sends username to AS (cleartext). [Msg 1, Pg 199]
    -   AS verifies username. Looks up user's long-term secret key (derived from password, stored securely).
    -   AS generates a **Client/TGS Session Key** ($K_{C,TGS}$).
    -   AS creates a **Ticket-Granting Ticket (TGT)** containing: $K_{C,TGS}$, Client ID, Client Address, Timestamp, Lifetime. Encrypts TGT with the **TGS's secret key** ($K_{TGS}$). [Part of Msg B, Pg 206]
    -   AS sends back to Client: [Msg 2, Pg 199]
        -   $K_{C,TGS}$ encrypted with the **Client's secret key** ($K_C$). [Msg A, Pg 206]
        -   The encrypted TGT. [Msg B, Pg 206]
    -   Client decrypts Msg A using their password-derived key to get $K_{C,TGS}$. Client cannot decrypt the TGT itself.
2.  **Service Request (Client -> TGS):**
    -   Client wants to access a specific service (e.g., file server).
    -   Client creates an **Authenticator** containing: Client ID, Timestamp. Encrypts Authenticator with the Client/TGS Session Key ($K_{C,TGS}$). [Msg D, Pg 207]
    -   Client sends to TGS: [Msg 3, Pg 199]
        -   The encrypted TGT obtained from AS. [Part of Msg C, Pg 207]
        -   ID of the requested service (SPN). [Part of Msg C, Pg 207]
        -   The encrypted Authenticator. [Msg D, Pg 207]
3.  **Service Ticket Granting (TGS -> Client):**
    -   TGS decrypts the TGT using its own secret key ($K_{TGS}$) to get $K_{C,TGS}$ and client info.
    -   TGS decrypts the Authenticator using $K_{C,TGS}$. Checks timestamp/client ID for validity (prevents replay).
    -   If valid, TGS generates a **Client/Server Session Key** ($K_{C,S}$).
    -   TGS creates a **Service Ticket** containing: $K_{C,S}$, Client ID, Client Address, Timestamp, Lifetime. Encrypts Service Ticket with the **Service's secret key** ($K_S$). [Msg E, Pg 207]
    -   TGS sends back to Client: [Msg 4, Pg 199]
        -   $K_{C,S}$ encrypted with the **Client/TGS Session Key** ($K_{C,TGS}$). [Msg F, Pg 207]
        -   The encrypted Service Ticket. [Msg E, Pg 207]
4.  **Service Access (Client -> Server):**
    -   Client decrypts Msg F using $K_{C,TGS}$ to get the Client/Server Session Key ($K_{C,S}$).
    -   Client creates a *new* Authenticator containing: Client ID, Timestamp. Encrypts this Authenticator with the **Client/Server Session Key** ($K_{C,S}$). [Msg G, Pg 208]
    -   Client sends to the target Service Server (SS): [Msg 5, Pg 199]
        -   The encrypted Service Ticket obtained from TGS. [Msg E, Pg 208]
        -   The new encrypted Authenticator. [Msg G, Pg 208]
5.  **Server Verification & Response (Server -> Client):**
    -   Server decrypts the Service Ticket using its own secret key ($K_S$) to get $K_{C,S}$ and client info.
    -   Server decrypts the Authenticator using $K_{C,S}$. Checks timestamp/client ID for validity.
    -   (Optional Mutual Authentication) Server may send back a confirmation (e.g., timestamp from authenticator + 1, encrypted with $K_{C,S}$) to prove its identity to the client. [Msg H, Pg 208] [Msg 6, Pg 199]
    -   Client and Server now share $K_{C,S}$ and can communicate securely.

#### Kerberos Advantages

-   **Password Security:** User password never transmitted over the network. Client derives key locally. Password guessing harder (needs KDC interaction).
-   **Single Sign-On (SSO):** User logs in once to AS, gets TGT. Can then access multiple services using the TGT to get service tickets without re-entering password.
-   **Ticket Security:** Stolen tickets are hard to reuse because they are tied to client address and require a fresh Authenticator (with timestamp) encrypted with a session key that the attacker doesn't have initially.
-   **Centralized Administration:** User accounts managed centrally at the KDC. Easier to secure fewer KDC machines.

#### Kerberos Drawbacks & Limitations

-   **Time Synchronization:** Relies heavily on timestamps in Tickets and Authenticators to prevent replay attacks. Clocks of all involved machines (client, KDC, server) must be synchronized within a small tolerance (e.g., 5 minutes). Requires NTP or similar.
-   **KDC Single Point of Failure/Target:** KDC holds all user/service secret keys. Compromise of KDC is catastrophic. Requires high availability and security for KDC.
-   **Administration Protocol:** Not standardized, varies between implementations.
-   **Key Management:** Each service needs its own long-term secret key registered with the KDC. Complicates setup for virtual hosting/clusters.
-   **Client Trust:** Requires clients to trust the KDC and potentially have Kerberos-aware software. Can be complex in staged or multi-domain environments.
-   **Password Guessing Vulnerability:** Initial request to AS can still be vulnerable to offline password guessing if weak passwords are used (attacker captures AS reply, tries hashing passwords offline to decrypt $K_{C,TGS}$).

#### Hacking Kerberos

Despite its strengths, Kerberos can be attacked, often exploiting vulnerabilities, weak passwords, or malware:

-   **Pass-the-Ticket:** Stealing valid TGTs or Service Tickets from memory/network and re-using them (bypassing need for password).
-   **Golden Ticket:** Forged TGT created using the KDC's TGS key ($K_{TGS}$, often `krbtgt` account hash). Grants domain admin access effectively. Requires prior compromise of KDC.
-   **Silver Ticket:** Forged Service Ticket created using a specific service's key ($K_S$). Grants access to that *specific* service. Requires compromise of the service account key.
-   **Credential Stuffing / Brute Force:** Standard password guessing against user accounts.
-   **Kerberoasting:** Attacker requests service tickets for accounts associated with SPNs, extracts the encrypted portion (using service key), and attempts to crack the service account's password offline.
-   **Encryption Downgrade (Skeleton Key):** Malware that forces use of weaker encryption, potentially bypassing Kerberos checks (needs admin access).
-   **DCShadow Attack:** Attacker with sufficient privileges registers a rogue Domain Controller to manipulate AD data, potentially creating backdoors.

### Section Summary: Authentication Applications

-   **X.509 / PKI:** Standard framework for managing public keys using digital certificates issued by trusted CAs. Enables trustworthy public key distribution and authentication in systems like TLS/HTTPS, S/MIME, etc. Relies on certificate chains and revocation checking (CRLs/OCSP).
-   **Kerberos:** Network authentication protocol using symmetric keys and a trusted KDC (AS+TGS). Provides strong authentication and SSO via tickets (TGT, Service Tickets) and authenticators. Avoids sending passwords over the network but requires time sync and secure KDC.

---

## Module 4 Glossary

-   **Message Authentication:** The process of verifying that received messages come from the alleged source and have not been altered.
-   **Integrity:** Ensuring data has not been modified without authorization.
-   **Authenticity:** Verifying the identity of the source of data.
-   **Non-Repudiation:** Providing proof that prevents a sender from denying they sent a message.
-   **Hash Function:** A function mapping arbitrary-size data to a fixed-size output (hash value or digest).
-   **Cryptographic Hash Function:** A hash function with specific security properties: Preimage Resistance, Second Preimage Resistance, Collision Resistance.
-   **Message Digest:** The output of a hash function.
-   **Preimage Resistance (One-Way):** Hard to find input M given output H(M).
-   **Second Preimage Resistance (Weak Collision Resistance):** Given M1, hard to find M2 != M1 such that H(M2) = H(M1).
-   **Collision Resistance (Strong Collision Resistance):** Hard to find any pair M1 != M2 such that H(M1) = H(M2).
-   **Collision:** Two different inputs producing the same hash output.
-   **Avalanche Effect:** Small input change causes significant output change.
-   **Birthday Attack:** Attack exploiting the mathematics of the Birthday Paradox to find hash collisions much faster than $2^m$. Requires $\approx 2^{m/2}$ operations.
-   **MD5 (Message Digest 5):** 128-bit hash function, now considered broken (insecure for cryptographic use).
-   **SHA (Secure Hash Algorithm):** Family of hash functions standardized by NIST.
-   **SHA-1:** 160-bit hash function, considered insecure (collisions found).
-   **SHA-2:** Family (SHA-224, SHA-256, SHA-384, SHA-512), currently secure.
-   **SHA-3 (Keccak):** Newest standard, based on sponge construction, secure.
-   **MAC (Message Authentication Code):** A short piece of information used to authenticate a message using a shared secret key. Provides integrity and authenticity, but not non-repudiation. $MAC = C_K(M)$.
-   **HMAC (Hash-based MAC):** Standard method for constructing a MAC using a cryptographic hash function and a secret key.
-   **DAA (Data Authentication Algorithm):** Outdated MAC standard based on DES-CBC. Insecure.
-   **DAC (Data Authentication Code):** The output tag produced by DAA.
-   **CMAC (Cipher-based MAC):** Secure MAC standard based on block ciphers (AES or TDES) using CBC mode with specific keying and padding.
-   **Authenticated Encryption (AE):** Cryptographic modes that provide confidentiality and integrity/authentication simultaneously (e.g., AES-GCM).
-   **Digital Signature:** Asymmetric cryptography technique providing authentication, integrity, and non-repudiation. Sign with private key, verify with public key.
-   **DSS (Digital Signature Standard):** US standard specifying the DSA algorithm.
-   **DSA (Digital Signature Algorithm):** Algorithm based on DLP used in DSS.
-   **X.509:** ITU-T standard defining formats for public key certificates, CRLs, etc., forming the basis for PKI.
-   **PKI (Public Key Infrastructure):** System for managing public keys and certificates.
-   **CA (Certification Authority):** Trusted entity that issues and signs digital certificates.
-   **Digital Certificate:** Electronic document binding a public key to an identity, signed by a CA.
-   **CRL (Certificate Revocation List):** List of certificates revoked by a CA before expiration.
-   **OCSP (Online Certificate Status Protocol):** Protocol for real-time certificate revocation checks.
-   **Kerberos:** Network authentication protocol using symmetric keys, tickets, and a trusted KDC (AS+TGS) for SSO.
-   **KDC (Key Distribution Center):** Trusted third party in Kerberos (contains AS and TGS).
-   **AS (Authentication Server):** Part of KDC, performs initial user authentication.
-   **TGS (Ticket-Granting Server):** Part of KDC, issues tickets for specific services.
-   **TGT (Ticket-Granting Ticket):** Issued by AS, allows client to request service tickets from TGS without re-authenticating.
-   **Service Ticket:** Issued by TGS, allows client to access a specific service.
-   **Authenticator (Kerberos):** Time-stamped data encrypted with a session key to prove timeliness and identity.
-   **Session Key:** Temporary symmetric key used for communication between client/TGS or client/server.
-   **SPN (Service Principal Name):** Unique identifier for a service instance in Kerberos.

---

## Further Reading / Resources

-   **Stallings, "Cryptography and Network Security":** Chapters on Hash Functions, MACs, Digital Signatures, Kerberos, X.509.
-   **Paar & Pelzl, "Understanding Cryptography":** Chapters on Hash Functions, MACs, Digital Signatures.
-   **RFCs:** RFC 2104 (HMAC), RFC 4120 (Kerberos V5), RFC 5280 (X.509 Certificates and CRL Profile).
-   **NIST Standards:** FIPS 180 series (SHA), FIPS 186 (DSS), SP 800-38B (CMAC), SP 800-57 (Key Management).
-   **Kerberos Website:** [web.mit.edu/kerberos/](https://web.mit.edu/kerberos/)

## Concept Map Idea

*   **Central Node:** Message Authentication & Digital Signatures
*   **Main Branches:**
    *   **Goals:** Integrity, Authenticity, Non-Repudiation
    *   **Mechanisms Overview:** Hash Functions, Encryption, MACs, Signatures
    *   **Cryptographic Hash Functions:**
        *   Properties (Fixed size, Easy compute, One-way, Collision Resist, Avalanche)
        *   Requirements (Preimage, 2nd Preimage, Collision Resist)
        *   Attacks (Birthday, Cryptanalysis)
        *   Algorithms -> MD5 (Broken), SHA-1 (Broken), SHA-2 (Secure), SHA-3 (Secure)
        *   Uses (Integrity Check, Passwords, PRF/PRNG, Component in MAC/Sig)
    *   **Message Authentication Codes (MACs):**
        *   Goal (Integrity, Authenticity) - Symmetric Key based
        *   vs Digital Sig (No Non-repudiation)
        *   Requirements
        *   Constructions -> HMAC (Hash-based), Block Cipher Based (DAA - Insecure, CMAC - Secure)
        *   Security
    *   **Digital Signatures:**
        *   Goal (Integrity, Authenticity, Non-Repudiation) - Asymmetric Key based
        *   Process (Sign w/ Private, Verify w/ Public) -> Usually Sign Hash
        *   Algorithms -> RSA Signatures, DSS (DSA)
        *   vs MACs
        *   vs Certificates
    *   **Authentication Systems & Infrastructure:**
        *   **Kerberos:** Symmetric Key, KDC (AS/TGS), Tickets (TGT, Service), Authenticators, SSO, Time Sync issue, MITM if no auth.
        *   **X.509 / PKI:** Public Key Management, CAs, Certificates (Binding Identity<->Key), Hierarchy/Trust Chains, CRLs/OCSP (Revocation), Used in TLS/S-MIME etc.

