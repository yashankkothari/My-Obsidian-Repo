### **Key Aspects of Information Security**

Information security ensures the **protection of data** through **three key principles**: **Confidentiality, Integrity, and Availability** (CIA Triad).

---

### **1. Confidentiality**
- Ensures that **sensitive information is not accessed** by unauthorized individuals.
- Prevents **data leaks** and **unauthorized disclosures**.
- **Examples**:
  - **Military**: Classified documents must remain secret.
  - **Banking**: Customer account details must be confidential.

---

### **2. Integrity**
- Ensures that **data is accurate and unaltered** unless modified by authorized entities.
- Protects against **unauthorized changes** or **corruptions**.
- **Types**:
  - **Data Integrity**: Ensures data remains **accurate** and **consistent**.
    - **Example**: A bank must correctly update a customer’s balance after a transaction.
  - **System Integrity**: Ensures a system **functions correctly** without unauthorized modifications.
    - **Example**: Preventing malware from altering a system’s core operations.

---

### **3. Availability**
- Ensures that **authorized users can access information when needed**.
- Data is useless if it is **not accessible**.
- **Example**:
  - A **banking system outage** prevents customers from **checking balances or making transactions**.

---

### **Conclusion**
The **CIA Triad** (**Confidentiality, Integrity, Availability**) is the foundation of **information security**, ensuring **data protection, reliability, and accessibility**.

### **Three Aspects of Information Security**

Information security consists of **three critical aspects**: **Security Attacks, Security Mechanisms, and Security Services**.

---

### **1. Security Attack**
- Any action that **compromises the security** of an organization's information.
- Can be classified into:
  - **Passive Attack**: Eavesdropping, traffic analysis.
  - **Active Attack**: Data modification, replay attacks, denial-of-service (DoS).

---

### **2. Security Mechanism**
- **Designed to detect, prevent, or recover** from security attacks.
- **Common Mechanisms**:
  1. **Encipherment**: Encrypting data to prevent unauthorized access.
  2. **Digital Signature**: Ensures message authenticity and integrity.
  3. **Access Control**: Restricts unauthorized access to data.

---

### **3. Security Service**
- **Enhances security** in data processing and transfers.
- Protects against **security attacks** by using security mechanisms.
- **Examples**:
  - **Authentication**: Verifies the identity of users.
  - **Confidentiality**: Ensures sensitive data is not exposed.
  - **Data Integrity**: Prevents unauthorized data modifications.
  - **Non-repudiation**: Ensures sender/receiver cannot deny communication.

---

### **Conclusion**
Security attacks threaten data, while **security mechanisms and services** work together to **protect, detect, and prevent unauthorized access**.

### **Threat vs. Attack in Information Security**

#### **1. Threat**
- A **potential security violation** that may exploit a vulnerability.
- Exists when there is a **circumstance, capability, action, or event** that could breach security.
- **Does not always lead to an attack** but represents a possible danger.
- **Example**: A hacker discovering a software vulnerability but not exploiting it.

#### **2. Attack**
- A **deliberate, intelligent act** attempting to violate security.
- Actively **exploits a vulnerability** to breach security policies.
- Can be classified as:
  - **Passive Attack**: Monitoring or eavesdropping on communication (e.g., wiretapping).
  - **Active Attack**: Modifying, disrupting, or destroying data (e.g., malware, denial-of-service).

#### **Key Difference**
| **Aspect**   | **Threat** | **Attack** |
|-------------|-----------|------------|
| **Definition** | Potential danger that could exploit vulnerabilities. | Deliberate attempt to breach security. |
| **Intentional?** | No, just a possibility. | Yes, actively carried out. |
| **Example** | Weak passwords, open network ports. | Brute-force login attempts, malware injection. |

### **Conclusion**
A **threat** represents a possible risk, while an **attack** is an actual attempt to breach security.

### **Types of Security Attacks**

Security attacks can be classified into four general categories based on the aspect of security they compromise.

#### **1. Interruption (Attack on Availability)**
- An asset of the system is **destroyed, unavailable, or unusable**.
- Affects system availability by preventing authorized users from accessing resources.
- **Examples**:
  - Destruction of hardware (e.g., physically damaging a server).
  - Cutting a communication line.
  - Disabling a file management system.
  - **Denial-of-Service (DoS) attacks**.

#### **2. Interception (Attack on Confidentiality)**
- An **unauthorized party gains access** to an asset.
- Can be done by a **person, program, or computer**.
- **Examples**:
  - **Wiretapping** to capture network data.
  - **Illicit copying of files** or **unauthorized access**.
  - Eavesdropping on encrypted communication.

![[Pasted image 20250305150724.png]]

#### **3. Modification (Attack on Integrity)**
- An **unauthorized party gains access and alters data**.
- Tampering with **stored or transmitted information**.
- **Examples**:
  - Changing values in a database.
  - Altering software or system configurations.
  - Modifying messages being sent in a network.

![[Pasted image 20250305150734.png]]

#### **4. Fabrication (Attack on Authenticity)**
- An **unauthorized party inserts counterfeit objects** into the system.
- Leads to falsified records, identity spoofing, or injecting fake data.
- **Examples**:
  - Insertion of **spurious messages** in a network.
  - **Adding fake records** to a database.
  - **Creating fake digital signatures** or authentication tokens.

![[Pasted image 20250305150744.png]]
### **Conclusion**
Each attack category targets a specific aspect of information security:
- **Interruption → Availability**
- **Interception → Confidentiality**
- **Modification → Integrity**
- **Fabrication → Authenticity**

### **Cryptographic Attacks**
Cryptographic attacks are classified into two types based on whether they exploit weaknesses in the encryption algorithm.

#### **1. Cryptanalytic Attacks (Algorithm-Based)**
- Exploit **mathematical weaknesses** in cryptographic algorithms.
- Aim to **recover plaintext or encryption keys** without direct access.
- **Examples**:
  - Brute-force attack
  - Differential cryptanalysis
  - Linear cryptanalysis

#### **2. Non-Cryptanalytic Attacks (Non-Algorithm-Based)**
- Do not exploit mathematical weaknesses but instead **target implementation flaws**.
- Aim to **bypass security mechanisms** or **extract keys indirectly**.
- **Examples**:
  - Side-channel attacks (timing analysis, power analysis)
  - Social engineering
  - Keylogging and malware

---

### **Passive vs. Active Attacks**
Security attacks can be categorized based on whether they **alter system data** or just **observe** it.

#### **1. Passive Attacks**
- **Goal**: **Obtain information** without altering system operations.
- **Targets**: Confidentiality
- **Examples**:
  - **Snooping** → Unauthorized access to data.
  - **Traffic Analysis** → Observing network patterns without intercepting actual data.

#### **2. Active Attacks**
- **Goal**: **Modify, damage, or disrupt system data**.
- **Targets**: Integrity, Availability
- **Examples**:
  - **Modification** → Unauthorized changes to data.
  - **Masquerading** → Impersonating an authorized user.
  - **Replaying** → Capturing and reusing legitimate messages.
  - **Repudiation** → Denying the execution of a legitimate action.
  - **Denial of Service (DoS)** → Overloading a system to make it unavailable.

---

### **Attack Classification Summary**
| **Attack Type** | **Passive/Active** | **Targeted Security Aspect** |
|---------------|----------------|--------------------------|
| **Snooping** | Passive | Confidentiality |
| **Traffic Analysis** | Passive | Confidentiality |
| **Modification** | Active | Integrity |
| **Masquerading** | Active | Integrity |
| **Replaying** | Active | Integrity |
| **Repudiation** | Active | Integrity |
| **Denial of Service (DoS)** | Active | Availability |
### **Taxonomy of Attacks with Respect to Security Goals**

Security attacks can be classified based on the **security goals** they threaten. The three primary security goals are:
- **Confidentiality** → Prevents unauthorized access to data.
- **Integrity** → Ensures data accuracy and trustworthiness.
- **Availability** → Ensures that services remain accessible.

---

### **1. Threats to Confidentiality**
- **Snooping** → Unauthorized access to sensitive data.
- **Traffic Analysis** → Observing communication patterns to infer information.

### **2. Threats to Integrity**
- **Modification** → Unauthorized alteration of data.
- **Masquerading** → Pretending to be an authorized entity to gain access.
- **Replaying** → Reusing captured legitimate messages to gain unauthorized access.
- **Repudiation** → Denying actions performed to avoid accountability.

### **3. Threats to Availability**
- **Denial of Service (DoS)** → Disrupting services to make them inaccessible.

---

### **Attack Classification Table**
| **Security Goal**   | **Attack Type**      | **Description** |
|-----------------|------------------|----------------|
| **Confidentiality** | Snooping | Unauthorized data access. |
| **Confidentiality** | Traffic Analysis | Observing communication to infer details. |
| **Integrity** | Modification | Altering stored or transmitted data. |
| **Integrity** | Masquerading | Impersonating an authorized entity. |
| **Integrity** | Replaying | Reusing legitimate data transmissions. |
| **Integrity** | Repudiation | Denying performed actions. |
| **Availability** | Denial of Service (DoS) | Overloading a system to disrupt services. |
### **Attacks Threatening Security Goals**

---

### **1. Attacks Threatening Confidentiality**
- **Snooping** → Unauthorized access or interception of data.
  - **Countermeasure** → Encipherment (encryption) techniques to make data unintelligible.
- **Traffic Analysis** → Observing network traffic to infer sensitive details.
  - **Example** → Identifying sender/receiver email IDs or transaction nature.
  - **Countermeasure** → Secure communication protocols (e.g., VPN, Tor).

---

### **2. Attacks Threatening Integrity**
- **Modification** → Altering requests or data.
  - **Example** → Attacker modifies a bank request to redirect funds.
  - **Countermeasure** → Digital signatures, message authentication codes (MAC).
- **Masquerading** → Impersonating an authorized user.
  - **Example** → Using a stolen credit card and PIN.
  - **Countermeasure** → Multi-factor authentication (MFA).
- **Replaying** → Resending a legitimate request to perform unauthorized actions.
  - **Example** → Resending a bank transaction request for duplicate payment.
  - **Countermeasure** → Timestamps, one-time tokens.
- **Repudiation** → Denying an action after performing it.
  - **Example** → A customer denies authorizing a bank transfer.
  - **Countermeasure** → Non-repudiation mechanisms like digital signatures.

---

### **3. Attacks Threatening Availability**
- **Denial of Service (DoS)** → Overloading a system to disrupt services.
  - **Example** → Sending excessive requests to crash a server.
  - **Countermeasure** → Rate limiting, firewalls, load balancing.
- **Distributed Denial of Service (DDoS)** → Multiple compromised systems launch a large-scale attack.
  - **Example** → Botnets flooding a website with traffic.
  - **Countermeasure** → Traffic filtering, anomaly detection.

### **Security Services and Mechanisms**

![[Pasted image 20250305151215.png]]

### **1. Security Services**
- **Data Confidentiality** → Prevents unauthorized disclosure of data.
  - **Protects Against** → Snooping, traffic analysis.
  - **Example Mechanisms** → Encryption, VPN, SSL/TLS.

- **Data Integrity** → Ensures data is not modified, inserted, or replayed.
  - **Protects Against** → Modification, insertion, deletion, replay attacks.
  - **Example Mechanisms** → Checksums, Hash functions (SHA-256), Message Authentication Codes (MAC).

- **Authentication** → Verifies identity of sender or receiver.
  - **Protects Against** → Impersonation, unauthorized access.
  - **Example Mechanisms** → Passwords, Digital Certificates, Biometrics.

- **Non-repudiation** → Prevents sender/receiver from denying actions.
  - **Proof of Origin** → Receiver can prove the sender’s identity.
  - **Proof of Delivery** → Sender can prove the recipient received data.
  - **Example Mechanisms** → Digital Signatures, Audit Logs.

- **Access Control** → Restricts unauthorized access to resources.
  - **Protects Against** → Unauthorized reading, writing, modifying, or executing.
  - **Example Mechanisms** → Role-Based Access Control (RBAC), Firewalls, Multi-Factor Authentication (MFA).

---
### **2. Security Mechanisms**
- **Encryption (Encipherment)** → Protects confidentiality (AES, RSA).
- **Digital Signatures** → Ensures authentication and non-repudiation.
- **Access Control Lists (ACLs)** → Limits access based on user roles.
- **Firewalls & Intrusion Detection Systems (IDS)** → Protects against unauthorized network access.
- **One-Time Passwords (OTP)** → Prevents replay attacks.

### **Security Mechanisms (ITU-T X.800)**
The **International Telecommunication Union-Telecommunication Standardization Sector (ITU-T X.800)** recommends security mechanisms to support security services.

![[Pasted image 20250305151325.png]]
#### **Recommended Security Mechanisms**
1. **Encipherment** → Protects data confidentiality (AES, RSA, DES).
2. **Digital Signatures** → Provides authentication and non-repudiation.
3. **Access Control** → Prevents unauthorized access (ACLs, RBAC).
4. **Data Integrity** → Ensures data accuracy (Checksums, Hash functions).
5. **Authentication Exchange** → Verifies identities (Kerberos, Certificates).
6. **Traffic Padding** → Hides communication patterns.
7. **Routing Control** → Ensures secure communication routes.
8. **Notarization** → Provides third-party verification for transactions.

---

### **Number Theory in Cryptography**
Cryptography relies heavily on **number theory** to ensure data integrity and prevent tampering.

#### **Importance of Number Theory**
- **Prime Numbers & Their Properties** → Used in cryptographic keys.
- **Integer Arithmetic** → Helps in encryption and decryption.
- **Greatest Common Divisor (GCD) & Euclidean Algorithm** → Used in public-key cryptosystems.
- **Extended Euclidean Algorithm** → Finds multiplicative inverses.
- **Modular Arithmetic** → Essential in RSA, Diffie-Hellman.
- **Residue Matrices** → Used in solving congruences.

#### **Key Objectives in Number Theory for Cryptography**
- Study **divisibility** and **GCD computation**.
- Use the **Extended Euclidean Algorithm** for solving linear congruences.
- Understand **modular arithmetic** and its applications.
- Apply **matrices and algebraic structures** to cryptography.

---
### **Mathematical Areas in Cryptography**
- **Number Theory** → Prime numbers, modular arithmetic.
- **Linear Algebra** → Matrices, transformations.
- **Algebraic Structures** → Groups, rings, and fields used in cryptographic protocols.

### Integer Arithmetic

#### Set of Integers
- The set of integers contains all whole numbers (without fractions) extending from negative infinity to positive infinity.  
  $$ Z = \{ \dots, -2, -1, 0, 1, 2, \dots \} $$

#### Binary Operations
- Three binary operations applied to integers: **addition, subtraction, and multiplication**.
- A **binary operation** takes two inputs and produces **one output**.
- If $a$ and $b$ are integers, their result after applying a binary operation is also an integer.

![[Pasted image 20250305151758.png]]

#### Integer Division
- **Division** produces **two outputs**: quotient $(q)$ and remainder $(r)$.
- The relationship between these four integers is:
  $$ a = q \times n + r $$
  where:
  - $a$ = dividend  
  - $q$ = quotient  
  - $n$ = divisor  
  - $r$ = remainder  
- Division is not considered a binary operation since it results in two values instead of one.

#### Divisibility
- If $r = 0$ in the division relation, then $a$ is **divisible** by $n$:
  $$ a \mid n $$
- Otherwise, $a$ is **not divisible** by $n$:
  $$ a \nmid n $$

![[Pasted image 20250305151821.png]]


#### Greatest Common Divisor (GCD)
- Two positive integers may have multiple common divisors, but only **one greatest common divisor (GCD)**.
- Example: Common divisors of 12 and 140 are **1, 2, and 4**, but the **greatest** is:
  $$ \gcd(12,140) = 4 $$
- The GCD of two positive integers is the largest integer that can **divide both numbers without a remainder**.

![[Pasted image 20250305151839.png]]

#### Euclidean Algorithm

- **Finding GCD by listing all common divisors is impractical** for large numbers.
- **Euclid (300 BC)** developed an **efficient algorithm** to compute the **GCD** of two positive integers.
![[Pasted image 20250305152010.png]]
#### Facts:
1. **If the second integer is 0, the GCD is the first integer.**  
   $$ \gcd(a, 0) = a $$
2. **Iteratively replace $(a, b)$ with $(b, a \mod b)$ until $b = 0$**, at which point $a$ is the GCD.

#### Example:
To compute $\gcd(36, 10)$:
$$
\gcd(36, 10) = \gcd(10, 6) = \gcd(6, 4) = \gcd(4, 2) = \gcd(2, 0) = 2
$$

- If **$\gcd(a, b) = 1$**, then **$a$ and $b$ are relatively prime** (i.e., they share no common factors other than 1).

![[Pasted image 20250305152124.png]]
![[Pasted image 20250305152133.png]]
![[Pasted image 20250305152141.png]]

### The Extended Euclidean Algorithm

- **Given two integers** $a$ and $b$, the extended Euclidean algorithm finds integers $s$ and $t$ such that:
  $$
  s \cdot a + t \cdot b = \gcd(a, b)
  $$
- **This algorithm simultaneously computes**:
  - $\gcd(a, b)$
  - The values of $s$ and $t$

- **Applications**:
  - Used extensively in computing **multiplicative inverses** in modular arithmetic.
  - Essential in **cryptographic algorithms** like RSA and ElGamal.

### Extended Euclidean Algorithm to find GCD

![[Pasted image 20250305152716.png]]

![[Pasted image 20250305152723.png]]

![[Pasted image 20250305152737.png]]

### Modular Arithmetic

- **Focuses only on the remainder** $r$ when dividing $a$ by $n$.
- **Quotient** $q$ is **not significant** in modular arithmetic.

#### Modulo Operator
- **Notation**: $a \mod n$
  - The **second input** $n$ is called the **modulus**.
  - The **output** $r$ is called the **residue**.

#### Representation:
$$
r = a \mod n
$$
![[Pasted image 20250305152907.png]]

### Set of Residues: $Z_n$

- The result of the modulo operation with modulus $n$ is **always** an integer between **$0$ and $n - 1$**.
- **i.e.** $a \mod n$ is always a **nonnegative integer** $< n$.
- The modulo operation **creates a set** called the **set of least residues modulo** $n$, denoted as $Z_n$:
  $$ Z_n = \{ 0, 1, 2, 3, \dots, (n - 1) \} $$

#### Examples:
- $Z_2 = \{ 0, 1 \}$
- $Z_6 = \{ 0, 1, 2, 3, 4, 5 \}$
- $Z_{11} = \{ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 \}$

---

### Congruence

- **Cryptography** uses the concept of **congruence** instead of **equality**.
- **Mapping from $Z$ to $Z_n$** is **not one-to-one**.
- **Infinite members** of $Z$ can map to a **single member** of $Z_n$.

#### Example:
- $2 \mod 10 = 2$, $12 \mod 10 = 2$, $22 \mod 10 = 2$, and so on.
- **Integers like $2, 12,$ and $22$ are congruent mod $10$.**
- **Denoted using the congruence operator** $\equiv$:
  $$ a \equiv b \pmod{n} $$

#### Examples:
- $2 \equiv 12 \pmod{10}$
- $13 \equiv 23 \pmod{10}$
- $34 \equiv 24 \pmod{10}$
- $-8 \equiv 12 \pmod{10}$
- $3 \equiv 8 \pmod{5}$
- $8 \equiv 13 \pmod{5}$
- $23 \equiv 33 \pmod{5}$
- $-8 \equiv 2 \pmod{5}$
![[Pasted image 20250305153015.png]]

### Residue Class

- A **residue class** $[a]$ or $[a]_n$ is the **set of all integers congruent to $a$ modulo $n$**.
- **Mathematically:** The set of all integers $x$ such that:
  $$ x \equiv a \pmod{n} $$

#### Example: $n = 5$
- There are **five residue classes**: $[0], [1], [2], [3],$ and $[4]$.
- Each residue class contains all integers **congruent mod $5$**:

  - $[0] = \{\dots, -15, -10, -5, 0, 5, 10, 15, \dots\}$
  - $[1] = \{\dots, -14, -9, -4, 1, 6, 11, 16, \dots\}$
  - $[2] = \{\dots, -13, -8, -3, 2, 7, 12, 17, \dots\}$
  - $[3] = \{\dots, -12, -7, -2, 3, 8, 13, 18, \dots\}$
  - $[4] = \{\dots, -11, -6, -1, 4, 9, 14, 19, \dots\}$

- The **set of least residues** modulo $5$ is:
  $$ Z_5 = \{0, 1, 2, 3, 4\} $$

- **In general**, the set $Z_n$ consists of all **least residues modulo $n$**.

### Operations in Zn 

•Addition, subtraction, and multiplication can also be defined for the set Zn.

![[Pasted image 20250305153141.png]]

### Example Operations Over $Z_n$

#### 1. Add $7$ to $14$ in $Z_{15}$
$$
(14 + 7) \mod 15 = 21 \mod 15 = 6
$$

#### 2. Subtract $11$ from $7$ in $Z_{13}$
$$
(7 - 11) \mod 13 = (-4) \mod 13 = 9
$$
(*Using additive inverse: $-4 + 13 = 9$*)

#### 3. Multiply $11$ by $7$ in $Z_{20}$
$$
(7 \times 11) \mod 20 = 77 \mod 20 = 17
$$

![[Pasted image 20250305153421.png]]

### Inverses
- Modular arithmetic often requires finding the **inverse** of a number relative to an operation.
- **Types:**
  - **Additive inverse** (relative to addition)
  - **Multiplicative inverse** (relative to multiplication)

### Additive Inverse in $Z_n$
- In $Z_n$, two numbers $a$ and $b$ are **additive inverses** of each other if:
  $$ a + b \equiv 0 \pmod{n} $$
- The additive inverse of $a$ can be calculated as:
  $$ b = n - a $$
- **Example:** The additive inverse of $4$ in $Z_{10}$ is:
  $$ 10 - 4 = 6 $$

### Finding All Additive Inverse Pairs in $Z_{10}$
#### Solution
- The six pairs of additive inverses are:
  $$(0, 0), (1, 9), (2, 8), (3, 7), (4, 6), (5, 5)$$
- **Observations:**
  - $0$ and $5$ are their own additive inverses.
  - **Additive inverses are reciprocal:**
    - If $4$ is the additive inverse of $6$, then $6$ is also the additive inverse of $4$.

### Additive Inverse of a Negative Number
- **Formula:**  
  $$ -n \mod k \equiv k - (n \mod k) $$
- **Examples:**
  - $ -3 \mod 12 = 12 - (3 \mod 12) = 12 - 3 = 9 $
  - $ -34 \mod 23 = 23 - (34 \mod 23) = 23 - 11 = 12 $

#### **Hint for Calculation:**
- If $ n < k $, compute $ k - n $.
- Else, take a **multiple of** $ k $ **just greater than** $ n $, then subtract $ n $ from that multiple.
  - **Example:**  
    - $ 23 \times 2 = 46 > n = 34 $  
    - $ 46 - 34 = 12 $

---

### Multiplicative Inverse
- In $ Z_n $, two numbers $ a $ and $ b $ are **multiplicative inverses** of each other if:
  $$ a \times b \equiv 1 \pmod{n} $$
- **Example:**  
  - If the modulus is **10**, then the **multiplicative inverse** of **3** is **7**:
    $$ (3 \times 7) \mod 10 = 1 $$

#### **Condition for Multiplicative Inverse:**
- A number $ a $ has a **multiplicative inverse** in $ Z_n $ **if and only if**:
  $$ \gcd(n, a) = 1 $$
- This means $ a $ and $ n $ **must be relatively prime**.

### Multiplicative Inverse
- Given two integers $a$ and $m$, find the **modular multiplicative inverse** of $a$ under modulo $m$.
- The **modular multiplicative inverse** is an integer $x$ such that:
  $$ a \times x \equiv 1 \pmod{m} $$

#### **Example:**
- If $a = 3, m = 11$, then $x = 4$.
- Thus, **3 and 4** are **multiplicative inverses** of each other modulo 11.

#### **Condition for Existence:**
- A **modular inverse exists if and only if**:
  $$ \gcd(a, m) = 1 $$  
  *(i.e., $a$ and $m$ are coprime)*

---

### Example: Finding Multiplicative Inverse
**Find $4^{-1} \mod 23$**  
- Solve for $x$ in:
  $$ 4 \times x \equiv 1 \pmod{23} $$
- Testing values:
  - $4 \times 1 \mod 23 = 4$
  - $4 \times 2 \mod 23 = 8$
  - $4 \times 3 \mod 23 = 12$
  - $4 \times 4 \mod 23 = 16$
  - $4 \times 5 \mod 23 = 20$
  - $4 \times 6 \mod 23 = 1$ ✅
- **Answer:** $x = 6$  
  - Hence, **4 and 6** are **multiplicative inverses** modulo 23.

---

### Example: No Multiplicative Inverse
**Find the multiplicative inverse of 8 in $Z_{10}$.**  
- Compute $\gcd(10, 8) = 2 \neq 1$.  
- Since 8 and 10 are **not coprime**, there **is no multiplicative inverse** of 8 in $Z_{10}$.

---

### Finding All Multiplicative Inverses
#### **In $Z_{10}$**
- **Solution:** Multiplicative inverse pairs:
  - **(1, 1), (3, 7), (9, 9)**
- **Numbers with no inverse:** 0, 2, 4, 5, 6, 8.

#### **In $Z_{11}$**
- **Solution:** Multiplicative inverse pairs:
  - **(1, 1), (2, 6), (3, 4), (5, 9), (7, 8), (9, 9), (10, 10)**
- **Note:** In $Z_{11}$, since $\gcd(11, a) = 1$ for all values of $a \neq 0$, **every number from 1 to 10 has a multiplicative inverse**.

### Extended Euclidean Algorithm and Inverse
- The **Extended Euclidean Algorithm** finds the **multiplicative inverse** of $b$ in $Z_n$ when **$\gcd(n, b) = 1$**.
- The **multiplicative inverse** of $b$ is the value of $t$ after being mapped to $Z_n$.

#### **Key Idea:**
- The algorithm finds integers **$x$ and $y$** such that:
  $$ n \times x + b \times y = \gcd(n, b) $$
- Since $\gcd(n, b) = 1$, we rewrite:
  $$ b \times y \equiv 1 \pmod{n} $$
- Here, **$y$ (or $t$)** is the **multiplicative inverse of $b$ mod $n$**.

#### **Steps to Compute the Inverse:**
1. Use the **Extended Euclidean Algorithm** to compute $x, y$ such that:
   $$ n \times x + b \times y = 1 $$
2. The **modular inverse** of $b$ is:
   $$ b^{-1} \equiv y \pmod{n} $$
3. If $y$ is **negative**, convert it to a **positive** equivalent:
   $$ y_{\text{mod}} = y \mod n $$

#### **Example: Finding $3^{-1} \mod 26$**
- Apply the **Extended Euclidean Algorithm** to solve:
  $$ 3x \equiv 1 \pmod{26} $$
- Using the algorithm:
  - $26 = 8 \times 3 + 2$
  - $3 = 1 \times 2 + 1$
  - $2 = 2 \times 1 + 0$
  - **Back-substituting:**
    - $1 = 3 - 1 \times 2$
    - $2 = 26 - 8 \times 3$
    - $1 = 3 - 1 \times (26 - 8 \times 3) = 9 \times 3 - 1 \times 26$
  - Hence, $x = 9$.

- **Final Answer:**  
  $$ 3^{-1} \equiv 9 \pmod{26} $$
#### Extended Euclidean Algorithm to compute multiplicative inverse

![[Pasted image 20250305154204.png]]

![[Pasted image 20250305190002.png]]
![[Pasted image 20250305190009.png]]
![[Pasted image 20250305190017.png]]

### Addition and Multiplication in Cryptography
- If the **sender** uses an **integer** (as the encryption key), the **receiver** uses the **inverse** of that integer (as the decryption key).
- If the cryptographic operation is **addition**, **$Z_n$** provides a set of **additive inverses**.
- If the cryptographic operation is **multiplication**, **$Z_n^*$** provides a set of **multiplicative inverses**.

#### **Usage:**
- **Use $Z_n$ for additive inverses.**
- **Use $Z_n^*$ for multiplicative inverses.**

#### **Examples of $Z_n$ and $Z_n^*$**
- **$Z_6$** = {0, 1, 2, 3, 4, 5}  
  **$Z_6^*$** = {1, 5}
  
- **$Z_7$** = {0, 1, 2, 3, 4, 5, 6}  
  **$Z_7^*$** = {1, 2, 3, 4, 5, 6}

- **$Z_{10}$** = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}  
  **$Z_{10}^*$** = {1, 3, 7, 9}
### **$Z_p$ and $Z_p^*$ Sets**
- The modulus in **$Z_p$** and **$Z_p^*$** sets is a **prime number**.
- A **prime number** has only two divisors: **1** and **itself**.
- The set **$Z_p$** is the same as **$Z_n$**, except that **$n$ is prime**, i.e., **$Z_p$** contains all integers from **$0$ to $p - 1$**.
- **Each member** in **$Z_p$** has an **additive inverse**.
- **Each member except 0** has a **multiplicative inverse**.

### **$Z_p$ and $Z_p^*$ Sets**
- The set **$Z_p^*$** is the same as **$Z_n^*$**, except that **$n$ is prime**.
- **$Z_p^*$** contains all integers from **$1$ to $p - 1$**.
- Each member in **$Z_p^*$** has both **additive** and **multiplicative** inverses.
- **$Z_p^*$** is an ideal choice when a set supporting both **additive** and **multiplicative** inverses is required.

### **Examples of $Z_p$ and $Z_p^*$**
- **$Z_{13}$** = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}  
- **$Z_{13}^*$** = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}

### **Matrices**
- **Representation in Mathematics**
  - Organized in **rows** and **columns**.
- **Operations**
  - **Addition**, **subtraction**, and **multiplication**.

### **Determinant of a Matrix**
- **Definition**:
  - A square matrix **$A$** of size **$m \times m$** has a **determinant**.
  - Denoted as **$\det(A)$**.
  - A scalar value calculated **recursively**.

- **Formula**:
  1. If **$m = 1$**, then  
     $$ \det(A) = a_{11} $$
  2. If **$m > 1$**, then  
     $$ \det(A) = \sum_{i=1}^{m} (-1)^{i+j} \cdot a_{ij} \cdot \det(A_{ij}) $$
     where **$A_{ij}$** is the matrix obtained by **removing** the **$i^{th}$ row** and **$j^{th}$ column** from **$A$**.

- **Note**: The determinant is **defined only for square matrices**.

### Computing a determinant

![[Pasted image 20250305190249.png]]
![[Pasted image 20250305190256.png]]

### **Inverses of a Matrix**
- Matrices have both **additive** and **multiplicative** inverses.

#### **Additive Inverse of a Matrix**
- If **$A$** is a matrix, its **additive inverse** is another matrix **$B$** such that:
  $$ A + B = 0 $$
- This means **$b_{ij} = -a_{ij}$** for all values of **$i$** and **$j$**.
- The additive inverse of **$A$** is denoted as **$-A$**.

---

### **Multiplicative Inverse of a Matrix**
- Defined **only for square matrices**.
- A square matrix **$A$** has a **multiplicative inverse** **$B$** if:
  $$ A \times B = B \times A = I $$
- The inverse of **$A$** is denoted as **$A^{-1}$**.
- **Existence condition**: The inverse exists **only if** $\det(A)$ has a **multiplicative inverse in the corresponding set**.
- **For real matrices**: The inverse exists **only if** $\det(A) \neq 0$.

#### **Existence of a Multiplicative Inverse**
- **$A^{-1}$ exists if and only if**:
  - **$\det(A)$ has a multiplicative inverse** in the corresponding set.
  - For matrices with **real elements**, the inverse **exists only if**:
    $$ \det(A) \neq 0 $$

---

### **Residue Matrices**
- **Residue matrices**: Matrices where all elements belong to **$Z_n$**.
- All operations (**addition, subtraction, multiplication**) are performed **modulo $n$**.
- **Condition for multiplicative inverse**:
  - A **residue matrix** has an inverse **if** $\det(A)$ has a **multiplicative inverse in $Z_n$**.
  - This means the determinant must be **relatively prime to $n$**:
    $$ \gcd(\det(A), n) = 1 $$

![[Pasted image 20250305190606.png]]

### **Linear Congruence**
- A **single-variable linear equation** in modular arithmetic.
- Involves solving an equation or a set of equations with coefficients in **$Z_n$**.
- **Example**: Solve for **$x$** in the equation:
  $$ ax \equiv b \pmod{n} $$
- **Number of solutions**:
  - If **$\gcd(a, n) = d$**:
    - If **$d \nmid b$** → **No solution**.
    - If **$d \mid b$** → **$d$ solutions** exist.

### **Applications of Linear Congruence**
- Used to solve modular equations in cryptography, computer science, and number theory.
- Example equations:
  1. $$ 10x \equiv 2 \pmod{15} $$
  2. $$ 14x \equiv 12 \pmod{18} $$
  3. $$ 3x + 4 \equiv 6 \pmod{13} $$

- **Extended to multiple variables**:
  - Systems of linear congruences can be solved using **matrices**.
  - Matrix methods are useful in **cryptographic algorithms** and **error correction codes**.

### **Cryptography**
- **Purpose**: Ensures secure communication by transforming data using secret codes and modern mathematics.
- **Applications**:
  1. **Computer Security** – Protects stored data from unauthorized access and hacking.
  2. **Network Security** – Safeguards data during transmission across networks.
  3. **Internet Security** – Protects data traveling over interconnected networks like the internet.

- **Key Concepts**:
  - Encryption & Decryption
  - Symmetric & Asymmetric Cryptography
  - Hash Functions
  - Digital Signatures

### **Basic Concepts of Cryptography**
- **Cryptography** – The science of transforming readable messages (plaintext) into unreadable formats (ciphertext) and back.
- **Plaintext** – The original, readable message.
- **Ciphertext** – The encrypted, unreadable message.
- **Cipher** – An algorithm that transforms plaintext into ciphertext using transposition or substitution.
- **Key** – A secret piece of information used by the cipher, known only to the sender & receiver.

### **Encryption & Decryption**
- **Encipher (Encode)** – Converting plaintext into ciphertext using a cipher and key.
- **Decipher (Decode)** – Converting ciphertext back into plaintext using a cipher and key.

### **Cryptanalysis & Cryptology**
- **Cryptanalysis** – The study of breaking encryption without knowledge of the key (code breaking).
- **Cryptology** – The combined study of cryptography and cryptanalysis.

### **Codes vs. Ciphers**
- **Code** – Uses a codebook to transform messages.
- **Cipher** – Uses mathematical algorithms to encrypt messages.

### **Categories of Cryptographic Systems**
Cryptographic systems are characterized along three independent dimensions:

1. **Type of Operations Used for Encryption**
   - **Substitution Ciphers** – Replace elements of plaintext with other elements.
   - **Transposition Ciphers** – Rearrange the order of elements without changing them.
   - **Hybrid Ciphers** – Combine substitution and transposition methods.

2. **Number of Keys Used**
   - **Symmetric-Key Cryptography (Secret-Key Cryptography)** – Uses a single key for both encryption and decryption.
   - **Asymmetric-Key Cryptography (Public-Key Cryptography)** – Uses a pair of keys (public key for encryption and private key for decryption).

3. **Processing Method of Plaintext**
   - **Block Ciphers** – Process plaintext in fixed-size blocks (e.g., 64-bit or 128-bit).
   - **Stream Ciphers** – Encrypt plaintext one bit or byte at a time.

### **Type of Operations Used for Transforming Plaintext to Ciphertext**
All encryption algorithms are based on two general principles:

1. **Substitution (Replacement)**
   - Each element in the plaintext is replaced with another element.
   - Example: **Caesar Cipher**, **Monoalphabetic Cipher**, **Playfair Cipher**.
   - Maintains the order of elements but changes their values.

2. **Transposition (Rearrangement)**
   - The positions of plaintext elements are shifted according to a fixed pattern.
   - Example: **Rail Fence Cipher**, **Columnar Transposition Cipher**.
   - Maintains the values of elements but changes their order.

🔹 **Modern encryption techniques often combine both substitution and transposition for stronger security.**

### **Substitution & Transposition**
1. **Substitution**
   - Each element in the plaintext (bit, letter, or group of bits/letters) is mapped to another element.
   - Example: **Caesar Cipher**, **Vigenère Cipher**, **AES (Advanced Encryption Standard)**.

2. **Transposition**
   - Elements in the plaintext are rearranged without altering their values.
   - Ensures **no information is lost**, meaning all operations must be reversible.
   - Example: **Rail Fence Cipher**, **Columnar Transposition Cipher**.

🔹 **Most cryptographic systems use multiple rounds of substitutions and transpositions for enhanced security.**

---

### **Categories of Cryptographic Systems**
#### **Based on the Number of Keys Used**
1. **Symmetric Encryption (Single-Key, Secret-Key, Conventional Encryption)**
   - Both sender and receiver share the **same key**.
   - Example: **DES (Data Encryption Standard)**, **AES**, **RC4**.

2. **Asymmetric Encryption (Two-Key, Public-Key Encryption)**
   - Uses a **public key** for encryption and a **private key** for decryption.
   - Example: **RSA**, **Diffie-Hellman**, **ECC (Elliptic Curve Cryptography)**.

🔹 **Symmetric encryption is faster, but asymmetric encryption provides better security for key exchange.**

### **Processing of Plaintext**
1. **Block Cipher**
   - Processes the input **one block at a time**.
   - Produces an **output block** for each **input block**.
   - Example: **AES (Advanced Encryption Standard), DES (Data Encryption Standard), Blowfish**.

2. **Stream Cipher**
   - Processes input **continuously**, producing an output **one element at a time**.
   - Example: **RC4, ChaCha20, Salsa20**.

🔹 **Block ciphers are more secure for large data, while stream ciphers are faster for real-time encryption (e.g., voice & video streaming).**

---

### **Classification of Cryptographic Systems**
1. **Type of Operations Used**
   - **Substitution**: Each plaintext element is replaced with another element.  
     - Example: **Caesar Cipher, Vigenère Cipher**.
   - **Transposition**: Plaintext elements are **rearranged**.  
     - Example: **Rail Fence Cipher, Columnar Transposition**.

2. **Number of Keys Used**
   - **Symmetric Encryption**: Sender & receiver **use the same key**.  
     - Example: **AES, DES, RC4**.
   - **Asymmetric Encryption**: Sender & receiver **use different keys**.  
     - Example: **RSA, Diffie-Hellman, ECC**.

3. **Processing Method**
   - **Block Cipher**: Encrypts data in **fixed-size blocks**.
   - **Stream Cipher**: Encrypts data **one bit at a time**.

🔹 **Modern cryptographic systems often combine block and stream ciphers for optimal security and efficiency.**

### **Symmetric Encryption**
A symmetric encryption scheme consists of **five key components**:

![[Pasted image 20250305191804.png]]

1. **Plaintext**  
   - The original **readable message or data** that needs to be encrypted.

2. **Encryption Algorithm**  
   - The algorithm that **transforms plaintext into ciphertext** using the secret key.  
   - Example: **AES, DES, RC4**.

3. **Secret Key**  
   - A **shared key** used for both encryption and decryption.  
   - Must be **kept confidential** between sender and receiver.

4. **Ciphertext**  
   - The **encrypted message**, which is unintelligible without the key.

5. **Decryption Algorithm**  
   - The process of **converting ciphertext back to plaintext** using the same secret key.

🔹 **Key Properties of Symmetric Encryption:**
- **Fast and efficient** for large data.
- Requires a **secure method** to share the secret key.
- Commonly used in **file encryption, VPNs, and TLS (Transport Layer Security).**

### **Strong Encryption Algorithm**
A **strong encryption algorithm** should ensure that:

- Even if an **attacker knows the encryption algorithm** and has access to ciphertexts, they **cannot decrypt** the message or determine the key.
- Even if an **attacker possesses multiple ciphertexts and their corresponding plaintexts**, they **should still be unable** to determine the encryption key.

### **Symmetric Encryption: Secure Secret Key**
To maintain security, the secret key must be:

1. **Securely Distributed**  
   - The sender and receiver must **securely obtain** the encryption key.  
   - Key exchange should **not be intercepted**.

2. **Confidential**  
   - The key must be **kept secret** to prevent unauthorized decryption.

3. **Protected Against Theft**  
   - If an attacker discovers the key and knows the algorithm, they can **decrypt all communications** encrypted with that key.

🔹 **Key Management is Critical**  
- Secure protocols like **Diffie-Hellman, Kerberos, and TLS** help in safe key distribution.
- Regular **key rotation** and **strong key generation** improve security.

![[Pasted image 20250305191806.png]]

### **Model of Symmetric Cryptosystem**
A symmetric cryptosystem consists of the following components:

![[Pasted image 20250305191950.png]]
#### **1. Plaintext Generation**
- A **source** produces a message in plaintext:
  $$ X = [X_1, X_2, ..., X_M] $$
- The message consists of **M elements**, which can be:
  - **Letters** (e.g., 26 capital letters A-Z)
  - **Binary values** ({0,1})

#### **2. Key Generation**
- A **key K** is generated:
  $$ K = [K_1, K_2, ..., K_J] $$
- The key can be:
  - **Generated at the message source**
  - **Generated by a trusted third party** and securely delivered to the receiver.

#### **3. Ciphertext Generation**
- The ciphertext **Y** is generated using an encryption algorithm **E**:
  $$ Y = [Y_1, Y_2, ..., Y_N] $$
  $$ Y = E(K, X) $$
- The encryption algorithm **transforms** plaintext **X** into ciphertext **Y** using the key **K**.

#### **4. Decryption**
- The receiver, who **possesses the key K**, applies the decryption algorithm **D**:
  $$ X = D(K, Y) $$
- The decryption process **inverts the encryption**, retrieving the original message.

🔹 **Key Security is Crucial**
- If the key **K** is compromised, the system's security is **completely broken**.
- Secure key distribution methods **must be implemented** to prevent interception.

### **Cryptanalysis**
Cryptanalysis is the study and process of analyzing and decrypting ciphers, codes, and encrypted text **without using the actual decryption key**. 

#### **Definition**
- The practice, science, or art of **decrypting encrypted messages**.
- The technique of accessing plaintext **without knowing the key**.

### **Role of Cryptanalysis**
- **Studies** ciphers, cryptosystems, and ciphertext to understand how they function.
- **Develops techniques** to weaken or break encryption.
- **Enhances security** by identifying vulnerabilities.

### **Key Roles in Cryptography**
1. **Cryptographer** – Develops encryption algorithms for cybersecurity.
2. **Cryptoanalyst** – Attempts to break or weaken encryption methods.

These two roles represent **opposing forces in cybersecurity**, constantly innovating **new measures and countermeasures** to outsmart each other.

### **Who Uses Cryptanalysis?**
Cryptanalysis is used by various groups for different purposes, ranging from **cybersecurity testing** to **hacking and espionage**.

#### **1. Hackers**
- Use cryptanalysis to exploit cryptosystem vulnerabilities instead of relying on brute force attacks.

#### **2. Governments**
- Decrypt encrypted messages of other nations for intelligence and national security.

#### **3. Cybersecurity Companies**
- Test security features by identifying weaknesses in cryptographic algorithms.

#### **4. Academic Researchers**
- Study cryptographic protocols to improve encryption methods and identify vulnerabilities.

#### **5. Ethical vs. Malicious Use**
- **Black-hat hackers** use cryptanalysis for cybercrimes.
- **White-hat hackers** use it for penetration testing to strengthen security for organizations.

### **Cryptanalysis Attacks and Techniques**

#### **1. Ciphertext-Only Attack (COA)**
- The attacker **only** has access to **one or more encrypted messages**.
- Does **not** know:
  - The **plaintext** data.
  - The **encryption key**.
  - The **encryption algorithm** used.
- Used by **intelligence agencies** when intercepting encrypted communications.
- **Difficult to execute** due to limited available data.

#### **Example: Ciphertext-Only Attack (COA)**
- Problem: Decrypt **"DQG D FKLOG UHQWLQJ."**
- Assume the cipher is a **Monoalphabetic Substitution Cipher**.
- Solution:
  - Use **brute force** by trying all possible shifts.
  - If using **Caesar cipher** with a shift of **3**:
    - 'D' → 'A'
    - 'Q' → 'N'
    - 'G' → 'D'
  - Decrypted text: **"AND A CHILD RENTING."**
  - **Successful decryption** with a shift of **3**.

#### **2. Known Plaintext Attack (KPA)**
- **Easier** to execute compared to a **Ciphertext-Only Attack**.
- The attacker has access to **some or all of the plaintext** corresponding to a given ciphertext.
- **Goal**: Discover the encryption **key** used by the target.
- Once the **key is found**, the attacker can decrypt **all messages** encrypted with that key.
- **Approach**:
  - The attacker tries to find or guess part of the **original plaintext**.
  - Even knowing the **format** of the plaintext can help break the encryption.

#### **3. Chosen Plaintext Attack (CPA)**
- The attacker **already knows** the encryption method or has access to the **encryption device**.
- The attacker can **input** chosen plaintexts into the encryption system.
- By analyzing the resulting **ciphertexts**, the attacker gathers **key-related information**.

#### **4. Chosen-Ciphertext Attack (CCA)**
- The **attacker** can analyze **chosen ciphertexts** and their **corresponding plaintexts**.
- **Goal**: Obtain the **secret key** or extract **critical information** about the encryption system.
- **Attack Method**:
  - The attacker can trick the victim (who knows the **secret key**) into **decrypting** any ciphertext.
  - By examining the decrypted **plaintext**, the attacker attempts to infer the **secret key**.
- **Common Usage**:
  - **More effective** against **public key encryption** systems.
  - Less frequently used against **symmetric encryption** systems.
  - **Example**: Early versions of **RSA** were vulnerable to CCA.
  - Some **self-synchronizing stream ciphers** have also been successfully attacked using this method.

### **Brute-Force Attack**
- **Method**: Tries every possible key until an **intelligible plaintext** is found.
- **Average Attempts**: Requires testing **X/2 keys** on average, where **X** is the total number of keys.
- **Effectiveness**: Highly dependent on key length—**longer keys** make brute-force attacks impractical.

---

### **Statistical Attack**
- **Concept**: Exploits **language characteristics** in plaintext to identify key patterns.
- **Example**: In English, the letter **E** is the most frequent. The attacker assumes the most used character in ciphertext corresponds to **E**.
- **Weakness**: If enough letter mappings are found, the **entire key** can be reconstructed.
- **Defense**: Ciphers should **obscure linguistic patterns** to resist statistical attacks.

---

### **Pattern Attack**
- **Concept**: Some ciphers hide language traits but introduce **repeating patterns** in ciphertext.
- **Method**: Cryptanalysts analyze these **repetitions** to infer parts of the key.
- **Defense**: Strong ciphers should ensure **random-looking ciphertext** to avoid pattern exploitation.

### **Cryptanalysis Tools**
1. **Cryptol**  
   - **Open-source** tool initially developed for the **NSA**.  
   - Used to analyze and monitor **cryptographic algorithms** in programs.  
   - Helps verify **correctness** and **security** of ciphers.

2. **CrypTool**  
   - **E-learning** platform for **learning cryptography** and **cryptanalysis**.  
   - Includes interactive tutorials on cryptographic **algorithms** and **attacks**.  
   - Provides a **web portal** for further resources and community discussions.

3. **Ganzua**  
   - **Java-based**, open-source cryptanalysis tool.  
   - Allows defining **custom alphabets** for cracking cryptograms.  
   - Supports **multi-language cryptanalysis**, making it effective for **non-English ciphers**.

### **Kerckhoff's Principle**
- **Encryption algorithm is public** → Assume the adversary (Eve) knows it.  
- **Security relies only on the secrecy of the key**, not the algorithm.  
- **Key guessing must be extremely difficult** to ensure security.  
- **Modern ciphers use only a few algorithms**, but they have **large key spaces**.  
- **A large key domain** ensures that brute-force attacks remain impractical.

### **Asymmetric Cryptography (Public-Key Cryptography)**
- **Uses key pairs:**  
  - **Public key** (shared with others).  
  - **Private key** (kept secret by the owner).  

![[Pasted image 20250305193113.png]]

#### **Essential Steps**
1. **Key Generation** → Each user generates a **public-private key pair**.  
2. **Public Key Distribution** → Public keys are stored in a register or shared with others.  
3. **Private Key Security** → The private key remains secret.  
4. **Encryption Process** → Sender encrypts the message using the **recipient's public key**.  
5. **Decryption Process** → Only the recipient can decrypt the message using their **private key**.  

🔹 **Example:**  
- **Bob** wants to send a message to **Alice**.  
- He encrypts it using **Alice’s public key**.  
- Alice decrypts it with her **private key**.  
- No one else can decrypt it since only Alice knows her private key.  

### **Comparison: Symmetric vs Asymmetric Key Encryption**

| Feature                | **Symmetric Key Encryption** | **Asymmetric Key Encryption** |
|------------------------|----------------------------|--------------------------------|
| **Keys Used**         | Single key for encryption & decryption. | Two keys: **Public key** (encrypts) & **Private key** (decrypts). |
| **Ciphertext Size**   | Same or smaller than plaintext. | Same or larger than plaintext. |
| **Speed**            | **Fast** encryption & decryption. | **Slow** encryption & decryption. |
| **Use Case**         | Efficient for **large** data transfers. | Used for **small** data transfers. |
| **Security Features** | Provides **confidentiality** only. | Ensures **confidentiality, authenticity, and non-repudiation**. |
| **Examples**         | **3DES, AES, DES, RC4** | **Diffie-Hellman, ECC, El Gamal, DSA, RSA** |
| **Resource Usage**   | **Low** computational requirements. | **High** computational requirements. |
### **Classical Encryption Techniques**
1. **Substitution Cipher**
   - Each letter or symbol in the plaintext is **replaced** with another letter, number, or symbol.
   - If plaintext is treated as **bits**, substitution replaces bit patterns with different bit patterns.
   - **Example:** 
     - Caesar Cipher (shifts letters by a fixed number).
     - Monoalphabetic Cipher (one-to-one letter mapping).
     - Playfair Cipher (digraph substitution).

2. **Transposition Cipher**
   - The **position** of plaintext characters is **rearranged** without changing the actual characters.
   - Does **not** alter the original characters, only their order.
   - **Example:**
     - Rail Fence Cipher (zigzag arrangement).
     - Columnar Transposition (reordering based on a key).

### **Substitution Cipher**
1. **Monoalphabetic Cipher**
   - Uses a **fixed substitution** for each letter in the plaintext.
   - More secure than the **Caesar cipher** but still vulnerable to frequency analysis.

#### **Types of Monoalphabetic Ciphers:**
1. **Additive Cipher (Shift / Caesar Cipher)**  
   - Each letter is shifted by a fixed value.  
   - **Formula:**  
     $$ C = (P + k) \mod 26 $$
     $$ P = (C - k) \mod 26 $$
   - Example (Shift by 3): `HELLO → KHOOR`

2. **Multiplicative Cipher**  
   - Each letter is **multiplied** by a key (mod 26).  
   - **Formula:**  
     $$ C = (P \times k) \mod 26 $$
     $$ P = (C \times k^{-1}) \mod 26 $$  
   - Only valid if **k** has an inverse in mod 26 (gcd(k, 26) = 1).
   - Example (Key = 5): `HELLO → AXEEH`

3. **Affine Cipher**  
   - Combination of **Additive and Multiplicative** ciphers.  
   - **Formula:**  
     $$ C = (aP + b) \mod 26 $$
     $$ P = a^{-1} (C - b) \mod 26 $$  
   - Example (a = 5, b = 8): `HELLO → ZEBBW`

### **Caesar Cipher (Additive)**
- One of the **earliest and simplest** substitution ciphers, used by **Julius Caesar**.
- Each letter is replaced by a letter **shifted by a fixed number** down the alphabet.
- Example (Shift by 3):  
  `HELLO → KHOOR`

![[Pasted image 20250305193923.png]]
### **Encryption Formula**  
$$ C = E(k, p) = (p + k) \mod 26 $$  
where:  
- \( C \) = Ciphertext letter  
- \( p \) = Plaintext letter  
- \( k \) = Shift value (1 to 25)

### **Decryption Formula**  
$$ p = D(k, C) = (C - k) \mod 26 $$  
![[Pasted image 20250305194206.png]]
![[Pasted image 20250305194216.png]]
### **Characteristics of Caesar Cipher:**
- **Alphabet wraps around** (e.g., `Z → C` if shifted by 3).
- **General shift** can be **any value from 1 to 25**.
- **Brute-force attack** is easy since there are only **25 possible keys**.

### **Cryptanalysis of Caesar Cipher:**
- **Easy to break** using brute force.
- **Prone to statistical attack** (frequency analysis).
- **Can use digrams/trigrams** (pairs or triplets of letters) for decryption.

### **Caesar Cipher - Key Space & Permutation**
- The **Caesar cipher** has only **25 possible keys**, making it **insecure** against brute-force attacks.
- **Increasing key space** significantly enhances security.

### **Permutation Concept**
- A **permutation** of a finite set \( S \) is an ordered arrangement of all elements in \( S \).
- Example:  
  If \( S = \{a, b, c\} \), possible permutations are:
  - **abc, acb, bac, bca, cab, cba**
- The total number of permutations for a set of **\( n \)** elements is:
  $$ n! = n \times (n-1) \times (n-2) \times ... \times 1 $$
![[Pasted image 20250305194515.png]]
### **Permutation in Monoalphabetic Ciphers**
- **Instead of shifting letters**, any **random permutation of the 26 letters** can be used as the cipher alphabet.
- The number of possible keys increases to:
  $$ 26! \approx 4 \times 10^{26} $$
- This approach is called a **monoalphabetic substitution cipher** because it **uses a single fixed substitution** for an entire message.

### **Monoalphabetic Cipher**
- A **monoalphabetic cipher** is a substitution cipher where **each plaintext character is mapped to a fixed ciphertext character**.
- Unlike the **Caesar cipher**, which uses a **fixed shift**, monoalphabetic ciphers allow **any random substitution** of letters.
- **Example:** The **Caesar cipher** (a basic form of monoalphabetic cipher).

![[Pasted image 20250305194950.png]]
![[Pasted image 20250305195000.png]]
![[Pasted image 20250305195014.png]]

### **Cryptanalysis of Monoalphabetic Cipher**
- **Comparing letter frequencies** with typical English letter frequencies helps in breaking monoalphabetic ciphers.
- **Example observations**:
  - Cipher letters **P and Z** correspond to **E and T**, but it's uncertain which is which.
  - High-frequency letters **S, U, O, M, H** likely correspond to common letters like **A, H, I, N, O, R, S**.
  - Low-frequency letters **A, B, G, Y, I, J** likely correspond to **B, J, K, Q, V, X, Z**.

### **Approach to Deciphering**
1. **Tentative Assignments**:
   - Start assigning plaintext letters based on frequency analysis.
   - Check if the message forms recognizable English words.

2. **Identifying Regularities**:
   - Look for **common words** that might be in the text.
   - Identify **repeating cipher sequences** to deduce possible plaintext patterns.

3. **Using Digram Frequency**:
   - **Digrams (two-letter combinations) are useful in breaking ciphers**.
   - The most common **English digram is "TH"**.
   - In the given ciphertext, the **most common digram is "ZW" (appears three times)**.
   - Hypothesis: **Z → T, W → H**.

4. **Refining the Mapping**:
   - Apply digram and trigram analysis to refine the letter substitutions.
   - Continue decrypting by **matching common word patterns**.

![[Pasted image 20250305195430.png]]
![[Pasted image 20250305195525.png]]
![[Pasted image 20250305195543.png]]

### **Final Steps**
- **Cross-check word structures** using contextual clues.
- **Iterate through the decryption process**, refining based on newly uncovered letters.
- **Use additional cryptographic techniques** like **known-plaintext attacks** or dictionary analysis.

### **Conclusion**
- Monoalphabetic ciphers are **weak against frequency analysis**.
- The **use of digrams and trigrams** significantly aids in breaking such ciphers.
- **Modern encryption methods** avoid simple substitution ciphers in favor of more secure approaches like **polyalphabetic or asymmetric encryption**.

![[Pasted image 20250305195627.png]]![[Pasted image 20250305195633.png]]

### **Polyalphabetic Cipher**
- **Definition**: Uses multiple substitution alphabets instead of a single one.
- **Key Features**:
  - **One-to-many mapping**: A single plaintext letter can map to different ciphertext letters.
  - **Hides letter frequency occurrences**, making frequency analysis harder.
  - **Uses a key stream**: Defined as \( k = \{k_1, k_2, k_3, \dots\} \).

### **Autokey Cipher**
- **Definition**: A variation of the polyalphabetic cipher where the key is a stream of subkeys.
- **Working Mechanism**:
  1. **First subkey**: A predetermined secret value agreed upon by Alice and Bob.
  2. **Subsequent subkeys**:
     - **Second subkey**: Value of the first plaintext character (converted to a number between 0-25).
     - **Third subkey**: Value of the second plaintext character.
     - **Continues for the entire plaintext**.

- **Purpose**: Increases security by dynamically changing the key stream, making cryptanalysis more difficult.

### **Advantages of Polyalphabetic Ciphers**
- **Resists frequency analysis attacks** compared to monoalphabetic ciphers.
- **Autokey ensures key randomness**, reducing repetition patterns.
- **More secure than simple substitution ciphers** but still vulnerable to known-plaintext attacks.

### **Comparison to Other Substitution Ciphers**
| Cipher Type          | Key Used | Security Level | Example |
|----------------------|---------|----------------|---------|
| **Monoalphabetic**   | Fixed single alphabet | Weak (frequency analysis) | Caesar, Simple Substitution |
| **Polyalphabetic**   | Multiple alphabets | Stronger (hides frequency patterns) | Vigenère, Autokey |
| **Autokey Cipher**   | Dynamic key stream (plaintext-dependent) | Even stronger | Variant of Vigenère |

- **Modern encryption methods** like AES use more advanced cryptographic techniques to ensure security.

![[Pasted image 20250305195848.png]]

### **Cryptanalysis of Autokey Cipher**
- **Strengths**:
  - **Hides single-letter frequency**: Since the key changes dynamically, frequency analysis is less effective.
  - **Reduces repeating patterns**: Unlike traditional Vigenère, which repeats the key, Autokey generates a unique sequence.

- **Weaknesses**:
  - **Vulnerable to brute-force attacks**: Since the first key is a fixed secret, attackers can try all possible starting keys.
  - **Additive cipher weakness**: If part of the plaintext is known, the key stream can be partially reconstructed.
  - **Known-plaintext attacks**: If an attacker gets enough plaintext-ciphertext pairs, they can deduce parts of the key and decrypt the message.

### **Countermeasures**
- **Use a stronger key schedule**: Instead of a simple additive scheme, modern encryption uses complex key expansion.
- **Apply more advanced encryption methods**: Combining polyalphabetic substitution with transposition or block ciphers enhances security.
- **Increase key randomness**: Ensuring that the initial key is sufficiently long and unpredictable reduces vulnerabilities.

**Conclusion**: While the Autokey Cipher improves upon simple substitution methods, it is still susceptible to modern cryptanalysis techniques and is not secure for contemporary use.

![[Pasted image 20250305200058.png]]![[Pasted image 20250305200106.png]]
![[Pasted image 20250305200117.png]]
![[Pasted image 20250305200125.png]]![[Pasted image 20250305200134.png]]
![[Pasted image 20250305200143.png]]
![[Pasted image 20250305200152.png]]

### **Cryptanalysis of Playfair Cipher**
- **Strengths**:
  - **Brute-force attack is difficult**: The keyspace is **25! (≈ \(10^{25}\))**, making exhaustive key search infeasible.
  - **Hides single-letter frequency**: Since Playfair operates on digrams (pairs of letters), single-letter frequency analysis is ineffective.

- **Weaknesses**:
  - **Still retains plaintext structure**: The cipher does not completely randomize letter patterns, making statistical analysis possible.
  - **Digram frequency analysis**: Common digrams (e.g., "th", "he", "in") remain partially predictable, making cryptanalysis possible.
  - **Ciphertext-only attack**: Given **a few hundred letters**, an attacker can use **digram frequency tests** to deduce key patterns.
  - **Key recovery is feasible**: If part of the key matrix is reconstructed, the entire key can often be determined.

### **Countermeasures**
- **Use larger key sizes**: A longer and more complex key matrix increases resistance to cryptanalysis.
- **Combine with transposition**: Mixing Playfair with transposition methods enhances security.
- **Increase ciphertext complexity**: Introducing additional encryption layers (e.g., double encryption) strengthens resistance against frequency analysis.

**Conclusion**: While Playfair is stronger than simple monoalphabetic ciphers, it remains vulnerable to frequency-based cryptanalysis, making it unsuitable for modern encryption needs.

### Polyalphabetic Cipher-Vignere Cipher

![[Pasted image 20250305200437.png]]

### **Strengths of Vigenère Cipher**
- **Polyalphabetic substitution**: Each plaintext letter can map to multiple ciphertext letters, making frequency analysis more difficult.
- **Obscures letter frequency**: Since the same plaintext letter can be encrypted differently based on the key, single-letter frequency analysis is ineffective.
- **Resists simple brute-force attacks**: Unlike Caesar cipher, the keyspace is significantly larger due to the use of multiple shifts.
- **Harder to detect common digrams/trigrams**: Since the shifting pattern repeats based on the key length, the direct recognition of common English digrams (e.g., "th", "he") is disrupted.
- **More secure than monoalphabetic ciphers**: The use of multiple substitution alphabets increases resistance against basic cryptanalysis techniques.

### **Limitations**
- **Key repetition weakness**: If the key is short or repeats frequently, the cipher becomes vulnerable to **Kasiski examination** and **index of coincidence analysis**.
- **Still retains plaintext structure**: Although improved over simple substitution, statistical techniques can still reveal key length and aid in decryption.
- **Vulnerable to frequency analysis if the key is short**: If the key length is small relative to the plaintext, repeating patterns emerge in the ciphertext.

### **Countermeasures**
- **Use a long, non-repeating key**: A long, unpredictable key (such as a one-time pad) eliminates periodicity.
- **Combine with additional encryption techniques**: Using transposition or modern cryptographic methods enhances security.

![[Pasted image 20250305200755.png]]![[Pasted image 20250305200803.png]]
![[Pasted image 20250305200812.png]]
![[Pasted image 20250305201108.png]]![[Pasted image 20250305201112.png]]
![[Pasted image 20250305201128.png]]

### **Cryptanalysis of Vigenère Cipher**
- **Does not preserve character frequency**: Unlike monoalphabetic ciphers, the same plaintext letter can be encrypted differently, making frequency analysis harder.
- **Focuses on key length discovery**: The main attack strategy involves determining the length of the key, which then allows for breaking the cipher as multiple Caesar ciphers.

### **Kasiski Examination**
- **Repetitions in ciphertext**: Identifying repeated sequences of three or more characters helps estimate the key length.
- **Distance analysis**: If a repeated sequence appears at distances **d₁, d₂, ..., dₙ**, the key length **m** is likely a factor of **gcd(d₁, d₂, ..., dₙ)**.
- **Avoiding misleading segments**: A three-letter segment is used instead of two-letter to reduce false positives where the key letters are coincidentally the same.

### **Index of Coincidence (IC)**
- **Measures character distribution**: The IC for English plaintext is **~0.068**, while random text has **~0.038**.
- **If key length is known**: The ciphertext can be split into separate Caesar ciphers, making frequency analysis possible on each segment.

### **Vulnerability**
- **Short keys**: A small key repeats frequently, making periodic patterns detectable.
- **Long ciphertexts**: The longer the ciphertext, the more likely repeated segments will reveal the key length.

### **Countermeasures**
- **Using a long, unpredictable key**: A long non-repeating key (e.g., one-time pad) eliminates periodicity.
- **Key management**: Ensuring keys are complex and not easily guessable mitigates cryptanalysis attempts.

![[Pasted image 20250305201242.png]]
![[Pasted image 20250305201350.png]]

### **Vernam Cipher (One-Time Pad)**
- **Ultimate defense against cryptanalysis**: If implemented correctly, it provides **perfect secrecy**.
- **Random, non-repeating key**: The key must be as long as the plaintext and have no statistical relationship to it.
- **Invented by Gilbert Vernam in 1918**: Originally designed for telegraph encryption.

### **Working Principle**
- **Binary XOR operation**:
  - Ciphertext:  
    $$ c_i = p_i \oplus k_i $$
  - Decryption:  
    $$ p_i = c_i \oplus k_i $$
  - Where:
    - \( p_i \) = \( i \)th bit of plaintext
    - \( k_i \) = \( i \)th bit of key
    - \( c_i \) = \( i \)th bit of ciphertext
    - \( \oplus \) = XOR operation

### **Security Considerations**
- **Perfect secrecy** (Shannon’s theorem) **if**:
  - The key is **truly random**.
  - The key is **at least as long as the plaintext**.
  - The key is **never reused**.
  - The key is **kept secret**.

### **Vulnerability of Repeating Keys**
- **Vernam originally used a long but repeating key**: This made it vulnerable to cryptanalysis with sufficient ciphertext and known plaintext attacks.
- **Modern one-time pad (OTP) corrects this**: Ensuring **no key reuse** eliminates the risk.

### **Challenges & Limitations**
- **Key distribution**: Securely sharing a key as long as the message is impractical for large-scale communication.
- **Key storage**: Storing large, random keys securely is a major challenge.
- **Impractical for general use**: Used only in highly secure communication (e.g., diplomatic or military).

### **Conclusion**
- **When used properly, the Vernam cipher (OTP) is unbreakable**.
- **Key management is the biggest challenge**.
- **Not practical for everyday encryption but still theoretically the most secure encryption method**.

### **Hill Cipher Algorithm**
- **Encryption method**: Uses **matrix multiplication** to substitute plaintext letters.
- **Processes \( m \) successive plaintext letters**: Converts them into \( m \) ciphertext letters.
- **Key-based substitution**: Determined by \( m \) linear equations.

### **Character Mapping**
- Each character is assigned a numerical value:  
  - \( a = 0, b = 1, c = 2, ..., z = 25 \).

### **Encryption Process (for \( m = 3 \))**
- Plaintext is represented as a **row vector** \( P \) of length \( m \).
- Ciphertext is represented as a **row vector** \( C \) of length \( m \).
- **Key matrix** \( K \) is an \( m \times m \) matrix.
- **Encryption formula**:  
  $$
  C = P K \mod 26
  $$
  Where:
  - \( C \) = Ciphertext vector
  - \( P \) = Plaintext vector
  - \( K \) = Key matrix (invertible mod 26)
  - Modulo 26 ensures results stay within the range of letters.

![[Pasted image 20250305202044.png]]
![[Pasted image 20250305202054.png]]
### **Decryption Process**
- Requires the **inverse of the key matrix** (\( K^{-1} \)).
- **Decryption formula**:  
  $$
  P = C K^{-1} \mod 26
  $$
  - \( K^{-1} \) must exist in **mod 26 arithmetic** for decryption to be possible.

### **Key Considerations**
- **Key matrix \( K \) must be invertible mod 26**: This means **det(K) must have a modular inverse mod 26**.
- **If \( K \) is not invertible, decryption is impossible**.
- **Hill cipher is vulnerable to known-plaintext attacks** due to its linear nature.

### **Hill Cipher Algorithm - Example**
#### **Encryption Process**
- Consider the plaintext **"paymoremoney"**.
- Given encryption key \( K \), we take the first three letters:
  - **"pay"** → Numerical vector:  
    $$ P = (15, 0, 24) $$  ![[Pasted image 20250305202251.png]]

- Multiply with the key matrix \( K \):
  $$
  (15, 0, 24)K = (303, 303, 531) \mod 26
  $$
  - Resulting ciphertext vector: \( (17, 17, 11) \)
  - Corresponding ciphertext letters: **"RRL"**.


- Repeating this process for the entire plaintext, we get:
  - **Ciphertext for "paymoremoney"** = **"RRLMWBKASPDH"**.

#### **Decryption Process**

![[Pasted image 20250305202303.png]]

- Decryption requires the **inverse of matrix \( K \)**.
- Take the first three letters of the ciphertext **"RRL"**:
  - **"RRL"** → Numerical vector:
    $$ C = (17, 17, 11) $$
- Multiply with the inverse of the key matrix \( K^{-1} \):
  $$
  (17, 17, 11) K^{-1} \mod 26 = (15, 0, 24)
  $$
  - Corresponding plaintext letters: **"pay"**.

- Repeating this process for the entire ciphertext, we recover:
  - **Plaintext for "RRLMWBKASPDH"** = **"paymoremoney"**.

### **Strength and Weakness of the Hill Cipher**
#### **Strengths:**
- **Hides single-letter frequencies**: Unlike simple substitution ciphers, Hill cipher completely obscures individual character distributions.
- **Larger matrices enhance security**: A \( 3 \times 3 \) Hill cipher hides **both single-letter and two-letter** frequency patterns.
- **Stronger than Playfair cipher**: It improves upon Playfair by increasing the complexity of character substitution.

#### **Weaknesses:**
- **Vulnerable to known plaintext attacks**: If an attacker knows a few plaintext-ciphertext pairs, they can solve for the encryption matrix.
- **Matrix inversion dependency**: Decryption requires computing  $K^{-1} \mod 26$, which exists only if **det(K) is coprime to 26**.
- **Susceptible to linear algebra techniques**: Since encryption relies on linear transformations, solving for \( K \) is feasible with enough data.

### **One-Time Pad (OTP)**
#### **Concept:**
- **Developed by Joseph Mauborgne** as an improvement to the Vernam cipher.
- Uses a **truly random key** as long as the message, ensuring **no repetition**.
- The **key is used only once** and then discarded.

#### **Advantages:**
- **Perfect secrecy**: Unbreakable if used correctly (i.e., truly random key, used once, and kept secret).
- **Each plaintext symbol is encrypted with a different random key**.

#### **Disadvantages:**
- **Key distribution problem**: A new key as long as the message must be securely shared for each communication.
- **Impractical for large-scale use**: Requires a secure method to exchange long random keys.

### **Strengths of One-Time Pad**
- **Perfect secrecy**: The ciphertext has **no statistical relationship** to the plaintext.
- **Unbreakable**: Since the ciphertext carries **zero information** about the plaintext, cryptanalysis is impossible.
- **Truly random encryption**: If the key is **truly random, as long as the message, and never reused**, it provides **absolute security**.

![[Pasted image 20250305202725.png]]
![[Pasted image 20250305202733.png]]
