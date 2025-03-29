
### Values of Assets  

Assets in information security refer to anything valuable that needs protection. They can be categorized based on their **replaceability** and **importance**.  

#### Off-the-Shelf Assets  
- **Easily replaceable** with commercially available alternatives.  
- Lower risk in case of loss but may still require effort to restore.  

#### Unique Assets  
- **Irreplaceable** or difficult to recreate.  
- Loss can have significant financial, operational, or emotional impact.  

#### Hardware  
Physical devices required for computing and communication.  
- **Computer** – Personal or enterprise-level machines.  
- **Devices** – Includes storage (disk drives, SSDs), memory modules, printers, and other peripherals.  
- **Network gear** – Routers, modems, and switches essential for connectivity.  

#### Software  
Programs that enable functionality and security of the system.  
- **Operating system (OS)** – Manages hardware resources (Windows, Linux, macOS).  
- **Utilities** – Security and maintenance tools (antivirus, firewalls, backup software).  
- **Commercial applications** – Productivity tools (MS Office, Photoshop, video editing software).  
- **Individual applications** – Custom-developed or specific-use applications.  

#### Data  
The most critical digital asset, often irreplaceable.  
- **Documents** – Personal, work-related, or academic files.  
- **Photos** – Memories and professional work.  
- **Music, videos** – Entertainment and creative assets.  
- **Email** – Personal and business communications.  
- **Class projects** – Academic work that may be crucial for grades or research.  

### Importance of Asset Protection  
Protecting assets ensures **confidentiality, integrity, and availability** (CIA triad). A breach or loss can result in financial loss, identity theft, or operational disruptions. Proper security measures like **backups, encryption, and access control** are essential to mitigate risks.  

### What Is Information Security?  
Information security refers to the **protection of assets** within a computer system to ensure their **confidentiality, integrity, and availability (CIA triad)**. It involves safeguarding **hardware, software, and data** from unauthorized access, damage, or theft.  

#### **Types of Assets in Information Security**  

##### **1. Hardware**  
Physical components of a computing system that store and process information.  
- **Computer** – Laptops, desktops, and servers.  
- **Devices** – Storage drives (HDDs, SSDs), memory modules (RAM), and printers.  
- **Network gear** – Routers, switches, modems, and network cables.  

##### **2. Software**  
Programs and applications that run on hardware, facilitating various functions.  
- **Operating system (OS)** – Manages system resources (Windows, Linux, macOS).  
- **Utilities** – Security and maintenance tools like antivirus software and firewalls.  
- **Commercial applications** – Productivity and creative software (MS Office, Photoshop).  
- **Individual applications** – Custom-built or specific-use programs.  

##### **3. Data**  
Digital information stored, processed, or transmitted by the system.  
- **Documents** – Work files, reports, academic papers.  
- **Photos** – Personal and professional images.  
- **Music & Videos** – Entertainment and creative media.  
- **Email** – Communication records, business correspondences.  
- **Class projects** – Academic assignments and research data.  

### **Why Information Security Matters**  
Protecting these assets ensures:  
- **Confidentiality** – Preventing unauthorized access.  
- **Integrity** – Ensuring data remains unaltered and trustworthy.  

### Threat & Vulnerability  

#### **Key Concepts**  
- **Vulnerability** – A weakness in a system that can be exploited.  
- **Threat** – A potential danger that exploits vulnerabilities to cause harm.  
- **Attack** – An actual attempt to exploit vulnerabilities.  
- **Countermeasure (Control)** – A safeguard or defense mechanism to mitigate threats.  

**Example Analogy:**  
- The **water** is the **threat**.  
- The **crack** in a dam is the **vulnerability**.  
- The **finger plugging the crack** is the **control** (temporary mitigation).  

### **Definition of Computer Security (NIST)**  
According to the **National Institute of Standards and Technology (NIST) Computer Security Handbook**,  
> "Computer Security is the protection afforded to an automated information system in order to attain the applicable objectives of preserving the **integrity, availability, and confidentiality** of information system resources."  

These resources include:  
- **Hardware** (Computers, storage devices, network equipment).  
- **Software** (Operating systems, applications, security tools).  
- **Firmware** (Embedded system software).  
- **Information/Data** (Documents, emails, credentials).  
- **Telecommunications** (Network communication, VoIP, cloud services).  

---

### **The CIA Triad**  
A fundamental model for information security, ensuring:  

#### **1. Confidentiality**  
- **Definition**: Preventing unauthorized access and disclosure of sensitive data.  
- **Ensures**: Protection of personal privacy and proprietary information.  
- **Techniques**: Encryption, access controls, multi-factor authentication (MFA).  

#### **2. Integrity**  
- **Definition**: Protecting data from unauthorized modification, destruction, or falsification.  
- **Ensures**: Data remains accurate and trustworthy (non-repudiation & authenticity).  
- **Techniques**: Checksums, hashing, digital signatures, version control.  

#### **3. Availability**  
- **Definition**: Ensuring reliable and timely access to data and systems.  
- **Ensures**: Systems and information remain operational when needed.  
- **Techniques**: Redundant systems, backups, disaster recovery plans, DDoS protection.  

The **CIA Triad** forms the core principles of cybersecurity, guiding the implementation of security policies and technologies.

### **Confidentiality**  
- Ensures that computer-related assets are accessed **only by authorized parties**.  
- **Access** includes **reading, viewing, printing**, or **knowing** an asset exists.  
- Also referred to as **secrecy** or **privacy**.  

#### **Confidentiality Solutions**  
- **Encryption** – Protects data by converting it into an unreadable format.  
- **Access control & policies** – Restrict access based on user roles.  
- **Authentication** – Verifies user identity (passwords, biometrics, MFA).  
- **Steganography** – Hides data within images, audio, or text.  
- **Covert channels** – Secret communication paths bypassing security.  
- **Cryptographic obfuscation** – Hides the logic of cryptographic algorithms.  
- **Zero knowledge proofs** – Verifies information without revealing actual data.  

---

### **Integrity**  
- Ensures that assets **can only be modified by authorized parties** in **authorized ways**.  
- An asset maintains integrity if it is:  
  - **Precise, accurate, unmodified** (unless authorized).  
  - **Modified only by authorized people or processes**.  
  - **Consistent, meaningful, and usable**.  

#### **Integrity Solutions**  
- **Hash functions** – Generate unique fingerprints for data (ensuring no tampering).  
- **MAC/HMAC** – Message Authentication Codes for verifying data integrity.  
- **SHA (Secure Hash Algorithm)** – A widely used cryptographic hash function.  
- **MD (Message Digest)** – Older cryptographic hash functions like MD5 (now insecure).  

---

### **Availability**  
- Ensures **data, services, and systems** are accessible when needed.  
- A system maintains availability if:  
  - **Responds timely to requests**.  
  - **Fair to all users** (no favoritism in resource allocation).  
  - **Fault-tolerant** (resilient to failures and attacks).  
  - **Manages concurrency and deadlocks** effectively.  

Availability solutions include **load balancing, redundancy, failover systems, and DDoS protection** to ensure continuous operation.  

### **Access Control**  
- Defines **who** can access **what** and **how**.  
- **Policy Formula:**  
  $$ \text{Who} + \text{What} + \text{How} = \text{Yes/No} $$  
- **Key Components:**  
  - **Subject (Who)** – The user or entity requesting access.  
  - **Object (What)** – The resource being accessed.  
  - **Mode of Access (How)** – The type of access (read, write, execute, etc.).  

---

### **Types of Threats**  
Threats can be categorized based on their **cause** and **intent**:  

![[Pasted image 20250303213643.png]]
#### **Natural Causes**  
- **Random** events beyond human control.  
  - **Examples:** Fire, power failure, earthquakes.  

#### **Human Causes**  
- **Benign Intent** – Errors caused unintentionally.  
  - **Example:** Human error (accidental deletion, misconfiguration).  
- **Malicious Intent** – Intentional attacks targeting systems.  
  - **Random Attack:** Malware spreading via general websites.  
  - **Directed Attack:** Impersonation, phishing, or targeted hacking.  

---

### **Advanced Persistent Threat (APT)**  
- **Highly organized, well-funded, and targeted attacks**.  
- **Characteristics:**  
  - **Organized** – Carried out by teams rather than individuals.  
  - **Directed** – Targets specific organizations or individuals.  
  - **Well-financed** – Backed by governments, corporations, or criminal groups.  
  - **Patient & Silent** – Long-term infiltration without immediate detection.  

> Security experts believe that high-priority targets can never be **fully** safe from APTs.  

---

### **Types of Attackers**  
- **Criminal-for-hire** – Hackers working for financial gain.  
- **Organized crime members** – Cybercriminal syndicates.  
- **Individual hackers** – Lone attackers with various motives (financial, political, or personal).  
- **Terrorists** – Cyberattacks with political or ideological goals.  
- **Loosely connected groups** – Hacktivists (e.g., Anonymous).  

> Each attacker type has **different resources, capabilities, and motivations** that influence the threat level.  

---

### **Types of Harm**  
Attacks can cause harm in four primary ways:  

1. **Modification** – Unauthorized changes to data or code.  
2. **Fabrication** – Insertion of false data or malicious code.  
3. **Interception** – Unauthorized access to sensitive data (e.g., eavesdropping, MITM attacks).  
4. **Interruption** – Disrupting services (e.g., DDoS, ransomware, sabotage).  

> Understanding these harm types is crucial for **threat assessment** and **risk mitigation**.  

### **Security Attacks**  
Security attacks target different aspects of the CIA triad:  

1. **Interruption** – Attack on **availability** and **confidentiality**.  
   - **Example:** DDoS (Denial of Service), ransomware, power outages.  
2. **Interception** – Attack on **confidentiality**.  
   - **Example:** Eavesdropping, MITM (Man-in-the-Middle) attacks, packet sniffing.  
3. **Modification** – Attack on **integrity**.  
   - **Example:** Unauthorized changes to files, database tampering, code injection.  
4. **Fabrication** – Attack on **authenticity**.  
   - **Example:** Fake user credentials, counterfeit digital certificates, malware injection.  

---

### **Controls/Countermeasures**  
To mitigate security threats, different **control measures** are implemented:  

#### **Based on CIA Triad Protection**  
- **Confidentiality Controls** – Encryption, access control, VPNs.  
- **Integrity Controls** – Hashing, digital signatures, checksums.  
- **Availability Controls** – Load balancing, redundancy, failover systems.  

#### **Based on Implementation Type**  
1. **Technical Controls** – Firewalls, intrusion detection systems (IDS), cryptographic measures.  
2. **Procedural Controls** – Security policies, employee training, audits.  
3. **Physical Controls** – Biometric authentication, CCTV, restricted access.  

#### **Threat Categorization**  
- **Human vs. Non-Human Threats** – Social engineering vs. malware.  
- **Malicious vs. Non-Malicious Threats** – Intentional hacking vs. accidental misconfigurations.  
- **Directed vs. Non-Directed Threats** – Targeted cyberattacks vs. automated botnet attacks.  
![[Pasted image 20250303213825.png]]

> Understanding controls in these **three dimensions** allows mapping countermeasures to **specific threats**, improving security effectiveness.  

### **Different Types of Controls**  

Security controls can be classified based on their function and where they are applied in a system:  

#### **1. Intrusion Attempts Detection**  
- **Monitors** for unauthorized access or malicious activities.  
- **Example:** Intrusion Detection Systems (IDS), log monitoring.  

#### **2. Prevention Controls**  
- **Internal Prevention** – Prevents unauthorized access **within** the system.  
  - **Example:** User authentication, role-based access control (RBAC).  
- **External Prevention** – Prevents external threats from breaching the system.  
  - **Example:** Firewalls, VPNs, anti-malware solutions.  

#### **3. Deterrence Controls**  
- **Internal Deterrence** – Discourages users **inside** the system from malicious actions.  
  - **Example:** Security policies, user monitoring, access logs.  
- **External Deterrence** – Deters **external** attackers from targeting the system.  
  - **Example:** Legal consequences, honeypots, deception techniques.  

#### **4. Response Controls**  
- **React** to detected security incidents by mitigating damage.  
- **Example:** Incident response teams, automated attack containment, forensic analysis.  

#### **5. Preemption Controls**  
- **Proactively** identify and neutralize threats **before** they cause harm.  
- **Example:** Threat intelligence, anomaly detection, penetration testing.  

#### **6. Deflection Controls**  
- **Redirect attackers** away from valuable assets using decoy systems.  
- **Example:** Honeypots, deceptive DNS responses, sandboxing environments.  

> These controls can be applied at **different levels** of a system, including **system perimeter, internal resources, and environment** to ensure comprehensive security.  


![[Pasted image 20250303213842.png]]

### **Method, Opportunity, and Motive (MOM)**
To successfully carry out an attack, an attacker needs:
- **Method** – Skills, tools, and knowledge required to perform the attack.
- **Opportunity** – Access and time to execute the attack.
- **Motive** – A reason to target a specific system.

> **Denying any one of these three factors can prevent an attack.**

---

### **Methods of Defense**
Security strategies to protect against attacks:
1. **Prevent** – Block the attack or eliminate the vulnerability.
2. **Deter** – Make the attack significantly harder or impossible.
3. **Deflect** – Shift the attacker's focus to a less critical target.
4. **Mitigate** – Reduce the impact of an attack.
5. **Detect** – Identify attacks as they occur or afterward.
6. **Recover** – Restore systems and minimize damage.

---

### **Types of Security Controls**
#### **1. Technical Controls**
- **Encryption** – Protects data confidentiality.
- **Hardware Controls**  
  - Smart card authentication.
  - Physical security (locks, cables).
  - Firewalls and intrusion detection systems.

#### **2. Software Controls**
- **Internal Program Controls** – Input validation, secure coding.
- **OS & Network Controls** – User authentication, access restrictions.
- **Independent Security Programs** – Antivirus, password managers.
- **Development Controls** – Secure software development practices.

#### **3. Administrative Controls**
- **Policies and Procedures** – Security awareness training, incident response plans.
- **Audits and Compliance** – Periodic security reviews and updates.

#### **4. Physical Controls**
- **Access Controls** – Biometric authentication, security personnel.
- **Environmental Security** – CCTV, motion detectors.

---

### **Effectiveness of Security Controls**
1. **Awareness of the Problem** – Educating users about security risks.
2. **Likelihood of Use** – Controls must be **easy, efficient, and practical**.
3. **Layered Security (Defense in Depth)** – Implement multiple security controls.
4. **Periodic Reviews** – Continuous monitoring and improvement.

---

### **Other Exposed Assets**
1. **Networks**
   - Lack of **physical proximity** control.
   - Use of **shared, insecure** media.
   - Difficulty in verifying **remote users**.

2. **Access**
   - **Unauthorized computer usage**.
   - **Malicious access** attempts.
   - **Denial of service (DoS)** attacks against legitimate users.

3. **Key People**
   - Employees with **privileged access** are prime targets.
   - **Social engineering** can be used to manipulate key personnel.

> **Security is an ongoing process requiring continuous improvement and adaptation.**

![[Pasted image 20250303214044.png]]
### **Problems Addressed by Encryption**
When sending a message, an attacker may attempt to:
- **Block the message** – Prevent delivery.
- **Intercept the message** – Eavesdrop on communication.
- **Modify the message** – Alter content.
- **Fabricate an alternate message** – Create a fake message that appears authentic.

---

### **Encryption Terminology**
- **Sender** – The entity that transmits the message.
- **Recipient** – The intended receiver of the message.
- **Transmission Medium** – The communication channel used.
- **Interceptor/Intruder** – The attacker attempting unauthorized access.
- **Encrypt/Encode/Encipher** – Converting plaintext into ciphertext.
- **Decrypt/Decode/Decipher** – Reverting ciphertext back to plaintext.
- **Cryptosystem** – The system used for encryption and decryption.
- **Plaintext** – The original readable message.
- **Ciphertext** – The encrypted unreadable form of the message.

---

### **Encryption/Decryption Process**
1. **Encryption:** Converts plaintext into ciphertext using an algorithm and a key.
2. **Decryption:** Converts ciphertext back into plaintext using a key.
![[Pasted image 20250303214316.png]]

---

### **Symmetric vs. Asymmetric Encryption**
#### **1. Symmetric Encryption**
- **Uses the same key** for encryption and decryption.
- **Fast and efficient** but requires secure key distribution.
- Example: AES, DES, 3DES.

#### **2. Asymmetric Encryption**
- **Uses a pair of keys** (public and private).
- **Slower but more secure** as keys don’t need to be shared.
- Example: RSA, ECC, Diffie-Hellman.

![[Pasted image 20250303214326.png]]

| Feature       | Symmetric Encryption | Asymmetric Encryption |
|--------------|--------------------|--------------------|
| Key Usage    | Single key for both encryption & decryption | Public key encrypts, Private key decrypts |
| Speed        | Fast               | Slower |
| Security     | Less secure (key exchange risk) | More secure (public-private key pair) |
| Use Case     | Encrypting bulk data | Secure key exchange, digital signatures |

---

### **Types of Ciphers**
#### **1. Stream Ciphers**
- Encrypts **one bit at a time**.
- Suitable for **real-time communication** (e.g., voice, video).
- Example: RC4, ChaCha20.

![[Pasted image 20250303214336.png]]
#### **2. Block Ciphers**
- Encrypts **fixed-size blocks** (e.g., 64-bit, 128-bit).
- Suitable for **file encryption** and secure storage.
- Example: AES, DES.

![[Pasted image 20250303214346.png]]

> **Choosing the right encryption method depends on security needs, speed, and use case.**

### **Diffusion**
- **Goal:** Hide the relationship between **ciphertext** and **plaintext**.
- **How it works:**
  - The statistical structure of plaintext is spread across multiple ciphertext characters.
  - Each plaintext digit affects **multiple ciphertext digits**.
- **Effect:** Makes it difficult for attackers to identify patterns in the ciphertext.

---

### **Confusion**
- **Goal:** Hide the relationship between **ciphertext** and **encryption key**.
- **How it works:**
  - Increases the complexity of the relationship between ciphertext and key.
  - Reduces the effectiveness of **cryptanalysis**.
- **Effect:** Makes it hard to reverse-engineer the key from ciphertext.

---

### **Stream Ciphers vs. Block Ciphers**

| Feature        | **Stream Ciphers**          | **Block Ciphers**          |
|---------------|----------------------------|----------------------------|
| **Advantages** | ✅ Fast encryption/decryption | ✅ High diffusion (complex ciphertext) |
|               | ✅ Low error propagation    | ✅ Resists symbol insertions |
| **Disadvantages** | ❌ Low diffusion (weak mixing) | ❌ Slower than stream ciphers |
|               | ❌ Vulnerable to modifications | ❌ Requires padding, error propagation |

> **Diffusion & Confusion** are essential principles in strong cryptographic algorithms to enhance security. 🚀

### **Data Encryption Standard (DES)**
- **Symmetric block cipher**
- Developed in **1976** by IBM for **NIST**
- Operates on **64-bit blocks** using a **56-bit key** (excluding 8 parity bits)
- **Vulnerable to brute-force attacks** due to increased computing power

### **Comparison of DES and Its Variants**
| **Form** | **Operation** | **Properties** | **Strength** |
|----------|--------------|---------------|-------------|
| **DES** | Encrypt with one key | **56-bit key** | **Weak** for modern security due to brute-force attacks |
| **Double DES** | Encrypt with first key, then encrypt result with second key | **Two 56-bit keys** | **Doubles strength** but vulnerable to **meet-in-the-middle attack** |
| **Two-key Triple DES** | Encrypt (or decrypt) with first key, then encrypt/decrypt with second key, then encrypt with first key (E-D-E) | **Two 56-bit keys** | Equivalent to **80-bit security**, **16 million times** stronger than DES |
| **Three-key Triple DES** | Encrypt with first key, then encrypt/decrypt with second key, then encrypt with third key (E-E-E) | **Three 56-bit keys** | Equivalent to **112-bit security**, **72 quintillion** times stronger than DES |

### **Security Concerns**
- **DES is outdated** and **easily broken** using brute-force attacks.
- **Triple DES (3DES) is deprecated** due to its vulnerability to attacks.
- **AES (Advanced Encryption Standard)** is now the **standard replacement** for DES.

### **DES Encryption and Decryption Process**
- **DES is a block cipher** that processes **64-bit blocks** of plaintext.
- It uses a **56-bit key** (excluding 8 parity bits) for encryption and decryption.

![[Pasted image 20250303221920.png]]
#### **Encryption Process**
1. **Input:** 64-bit **plaintext**
2. **DES Cipher:** Encrypts using a **56-bit key**
3. **Output:** 64-bit **ciphertext**

#### **Decryption Process**
1. **Input:** 64-bit **ciphertext**
2. **DES Reverse Cipher:** Decrypts using the **same 56-bit key**
3. **Output:** 64-bit **plaintext**

The encryption and decryption processes are **symmetric**, meaning the **same key** is used for both.

### **Triple DES (3DES) with Two Keys**
- **Triple DES (3DES)** enhances security by applying the **DES algorithm three times**.
- It can operate with **two keys (2-key 3DES)** or **three keys (3-key 3DES)**.

![[Pasted image 20250303222048.png]]
#### **Encryption Process (E-D-E Mode)**
1. **First encryption:** Encrypt plaintext using **Key 1**.
2. **Decryption step:** Decrypt the result using **Key 2**.
3. **Final encryption:** Encrypt again using **Key 1**.

#### **Decryption Process**
1. **First decryption:** Decrypt ciphertext using **Key 1**.
2. **Encryption step:** Encrypt the result using **Key 2**.
3. **Final decryption:** Decrypt again using **Key 1**.

- **Security Strength:** Equivalent to an **80-bit key**, providing **16 million times** more security than **single DES**.
- **Backward Compatibility:** Can decrypt **DES-encrypted data** when using identical keys.

### **General Structure of DES**
- **DES (Data Encryption Standard)** is a **symmetric block cipher** that encrypts **64-bit plaintext blocks** into **64-bit ciphertext blocks** using a **56-bit key**.
- It follows a **Feistel network** structure with **16 rounds of encryption**.

![[Pasted image 20250303222142.png]]
#### **Steps in DES Encryption**
1. **Initial Permutation (IP)**  
   - Rearranges the bits of the plaintext.
![[Pasted image 20250303222216.png]]

2. **16 Rounds of Feistel Network**
   - Each round consists of:
     - Splitting data into **Left (L) and Right (R) halves**.
     - Applying the **Feistel function (F)** to the **Right half** using a **round key**.
     - XORing the **Left half** with the **Feistel function output**.
     - Swapping the halves.

3. **Final Permutation (FP)**
   - Inverse of the **Initial Permutation**, producing the **64-bit ciphertext**.
   
![[Pasted image 20250303222230.png]]
#### **Key Schedule**
- A **56-bit key** is expanded into **16 round keys (48 bits each)** using **permutations and bit shifts**.

- **Security Concerns:**  
  - **Vulnerable** to **brute force attacks** due to modern computing power.  
  - **Triple DES (3DES)** was introduced to enhance security.

### **DES Rounds and Feistel Cipher**
- **DES uses 16 rounds**, each being a **Feistel cipher**, meaning the data is split into two halves and processed iteratively.

#### **Structure of Each DES Round**
1. **Input Split:**  
   - The **64-bit block** is divided into:
     - **Left half (L)**
     - **Right half (R)**

2. **Round Function (F):**  
   - The **Right half (R)** is expanded to **48 bits** using an **Expansion Permutation (E)**.
   - XOR with a **48-bit round key**.
   - The result is passed through **S-Boxes** (Substitution Boxes), reducing it back to **32 bits**.
   - A **Permutation (P)** further shuffles the bits.

3. **XOR and Swap:**  
   - The **output of (F)** is XORed with the **Left half (L)**.
   - The new **Right half (R')** becomes the previous **Left half (L)**.
   - The **Left half (L')** becomes the new XORed result.

4. **Final Output:**  
   - After 16 rounds, the halves are recombined.
   - A **Final Permutation (FP)** produces the **64-bit ciphertext**.

![[Pasted image 20250303222329.png]]

- **Security Impact:**  
   - The **16 rounds ensure strong diffusion and confusion**, making decryption without the key computationally infeasible.

### **DES Function**
- The **heart of DES** is the **DES function**, which is applied in each of the **16 rounds**.
- **Purpose:**  
  - It **processes the rightmost 32 bits** of the data block.
  - Uses a **48-bit round key** to produce a **32-bit output**.

![[Pasted image 20250303222407.png]]
#### **Steps in the DES Function**
1. **Expansion (E-Permutation):**  
   - Expands the **32-bit right half** to **48 bits** using a fixed expansion table.
   - This ensures that bits are mixed and repeated.

2. **Key Mixing (XOR Operation):**  
   - The expanded 48-bit data is XORed with the **48-bit round key**.

3. **Substitution (S-Boxes):**  
   - The result is split into **8 groups of 6 bits**.
   - Each group is passed through an **S-Box** (Substitution Box), reducing it to **4 bits**.
   - The **8 S-Boxes collectively produce a 32-bit output**.

4. **Permutation (P-Permutation):**  
   - The 32-bit output is rearranged using a **fixed permutation table** to improve diffusion.

- **Final Output:**  
   - The 32-bit result is sent back for XOR with the **left half** of the data block in that round.
   - This ensures **strong confusion and diffusion**.

### **Expansion P-Box**
- The **Expansion P-Box** is used in **DES function** to expand the **32-bit** right half (Rᵢ₋₁) to **48 bits**.
- This is required because the **round key (Kᵢ) is 48 bits**, and both must be XORed.

![[Pasted image 20250303222504.png]]
#### **How the Expansion Works**
1. **Expansion Table:**  
   - The 32-bit input (Rᵢ₋₁) is **rearranged and expanded** to **48 bits**.
   - Some bits are **duplicated** to increase diffusion.

2. **Output of Expansion:**  
   - The output is **48 bits**, which can now be XORed with the **48-bit round key (Kᵢ)**.

3. **Purpose of Expansion:**  
   - Ensures that **each bit in the original 32-bit Rᵢ₋₁ affects multiple bits** in the next step.
   - Helps in **strengthening security** by making the relationship between plaintext and ciphertext more complex.

- **Next Step:**  
   - The 48-bit expanded data is XORed with the **48-bit round key (Kᵢ)** before substitution (S-Boxes).

### **Expansion P-Box in DES**
- The relationship between **input (32-bit Rᵢ₋₁) and output (48-bit expanded data)** can be defined **mathematically**.
- However, **DES does not use a mathematical function** for this transformation.
- Instead, a predefined lookup table is used to define how the bits are expanded and rearranged.

![[Pasted image 20250303222620.png]]

### **Whitener (XOR) in DES**
- After the **Expansion P-Box**, DES performs an **XOR operation** between:
  - The **48-bit expanded right section (Rᵢ₋₁)**  
  - The **48-bit round key (Kᵢ)**
  
#### **Key Points**
1. **Purpose of XOR in DES:**
   - Introduces **key-dependent randomness** in every round.
   - Ensures that **even minor key changes** result in major encryption differences (**avalanche effect**).
   - The **round key (Kᵢ) is used only for this XOR operation**.

2. **Why XOR?**
   - **Simple & efficient** bitwise operation.
   - Easily reversible:  
     - XORing the **same key twice cancels out the effect**.
   - **Provides security against cryptanalysis** by making each round output **appear random**.

---

### **S-Boxes (Substitution Boxes) in DES**
- **After XOR**, the **48-bit result** is divided into **8 chunks of 6 bits each**.
- Each **6-bit block** is **substituted** using a corresponding **S-Box**.
- DES uses **8 S-Boxes**, labeled **S1, S2, ..., S8**.
![[Pasted image 20250303222907.png]]
#### **How S-Boxes Work**
1. **Each S-Box takes a 6-bit input** and produces a **4-bit output**.
2. The **first and last bit (outer bits)** determine the **row** in the S-Box table.
3. The **middle 4 bits** determine the **column** in the S-Box table.
4. The **corresponding 4-bit value** is taken from the S-Box and replaces the 6-bit input.
![[Pasted image 20250303222915.png]]
#### **Purpose of S-Boxes**
- **Main source of confusion** in DES (hides the relationship between plaintext, ciphertext, and key).
- **Non-linear transformation** makes cryptanalysis significantly harder.
- **Fixed S-Box tables (Figure 6.7)** are carefully designed to resist known attacks.

![[Pasted image 20250303222927.png]]
---

- **Next Step:**  
  - After substitution, the 32-bit output is passed through the **P-Box permutation**, which shuffles bits for further diffusion.

### S-Boxes Calculation

To determine the output of **S-Box 1** for the input **100011**:

1. **Extract Row Index:**  
   - The **first** and **sixth** bits: **1 and 1** → `11` (binary) = **3** (decimal).

2. **Extract Column Index:**  
   - The **middle four bits**: `0001` (binary) = **1** (decimal).

3. **Look up Table 6.3 (S-Box 1):**  
   - **Row 3, Column 1** → **12** (decimal) = `1100` (binary).

### **Final Result:**  
- **Input:** `100011`  
- **Output:** `1100`

### S-Boxes Calculation (S-Box 8)

To determine the output of **S-Box 8** for the input **000000**:

1. **Extract Row Index:**  
   - The **first** and **sixth** bits: **0 and 0** → `00` (binary) = **0** (decimal).

2. **Extract Column Index:**  
   - The **middle four bits**: `0000` (binary) = **0** (decimal).

3. **Look up Table 6.10 (S-Box 8):**  
   - **Row 0, Column 0** → **13** (decimal) = `1101` (binary).

### **Final Result:**  
- **Input:** `000000`  
- **Output:** `1101`

### Cipher and Reverse Cipher

Using **mixers** and **swappers**, we can create both the **cipher** and **reverse cipher**, each consisting of **16 rounds**.

#### **First Approach**
- The **last round (Round 16) is different** from the others.
- It **only includes a mixer** and **no swapper**.
- **Note:** In this approach, there is **no swapper** in the last round.
![[Pasted image 20250303223622.png]]
#### **Alternative Approach**
- **All 16 rounds remain the same** by including a **swapper in the 16th round**.
- An **extra swapper is added after the last round**.
- **Effect:** The two swappers **cancel each other out**.

---

### **Key Generation**
- The **round-key generator** produces **sixteen 48-bit keys** from a **56-bit cipher key**

![[Pasted image 20250303223645.png]]
![[Pasted image 20250303223657.png]]![[Pasted image 20250303223705.png]]

### **Random Plaintext and Key Selection**
We choose:
- A **random plaintext block** (in hexadecimal).
- A **random key** (in hexadecimal).
- Determine the **ciphertext block** using the **DES encryption process**.

#### **Process:**
1. **Input:** Random **64-bit plaintext** (Hex)
2. **Key:** Random **56-bit key** (Hex)
3. **Encryption:** Apply **DES algorithm**
4. **Output:** Resulting **64-bit ciphertext** (Hex)

This process ensures encryption using a **secure, symmetric** approach.

### **Example 6.5: DES Encryption Process**
#### Plaintext: `123456ABCD132536`  
#### Key: `AABB09182736CCDD`  
#### Ciphertext: `C0B7A8D05F3A829C`  

#### **Table 6.15: Trace of Data for Example 6.5**

| Step                        | Left       | Right      | Round Key      |
|-----------------------------|------------|------------|---------------|
| **After Initial Permutation** | `14A7D678` | `18CA18AD` |               |
| **After Splitting**          | `L0=14A7D678` | `R0=18CA18AD` |               |
| **Round 1**                 | `18CA18AD` | `5A78E394` | `194CD072B9BC` |
| **Round 2**                 | `5A78E394` | `4A1210F6` | `4568581ABCCE` |
| **Round 3**                 | `4A1210F6` | `B8089591` | `06EDA4ACF5E3` |
| **Round 4**                 | `B8089591` | `236779C2` | `DA2D32B6BEC3` |

#### **Continued Rounds**
| Step         | Left       | Right      | Round Key      |
| ------------ | ---------- | ---------- | -------------- |
| **Round 5**  | `236779C2` | `A15A4B87` | `69A629FEC913` |
| **Round 6**  | `A15A4B87` | `26FEC629` | `C1948A877656` |
| **Round 7**  | `26FEC629` | `29D6E21C` | `708AD02CEAB8` |
| **Round 8**  | `29D6E21C` | `A0B3D5F7` | `84B48A79D5CC` |
| **Round 9**  | `A0B3D5F7` | `3ACC7961` | `0A5DDBFC56F4` |
| **Round 10** | `3ACC7961` | `A63D464F` | `CB3D8D3EBE37` |
| **Round 11** | `A63D464F` | `011C3C58` | `8307B1300A86` |
| **Round 12** | `011C3C58` | `39B725D8` | `C3281D1D0CE1` |
| **Round 13** | `39B725D8` | `C2F2DABA` | `F3F796D5F066` |
| **Round 14** | `C2F2DABA` | `C912C2F8` | `F53C6D66F8A2` |
| **Round 15** | `C912C2F8` | `292DAA28` | `13C053D95D66` |
| **Round 16** | `292DAA28` | `CP26B472` | `133DC3B5666D` |

#### **Final Combination:** `19BA0212FCB6472`
#### Ciphertext (After Final Permutation): `C0B7A8D05F3A829C`

### **Example 6.6: DES Decryption Process**
#### Ciphertext: `C0B7A8D05F3A829C`
#### Key: `AABB09182736CCDD`
#### Recovered Plaintext: `123456ABCD132536`

#### Decryption Steps

| Step                        | Left       | Right      | Round Key      |
|-----------------------------|------------|------------|---------------|
| **After Initial Permutation** | `19BA0212` | `FCB6472`  |               |
| **After Splitting**          | `L0=19BA0212` | `R0=FCB6472` |               |
| **Round 1**                 | `FCB6472`  | `CP26B472` | `133DC3B5666D` |
| **Round 2**                 | `CP26B472` | `292DAA28` | `13C053D95D66` |
| **... (Rounds 3-15 omitted for brevity) ...** | | | |
| **Round 16**                | `14A7D678` | `18CA18AD` | `194CD072B9BC` |

#### **Final Combination:** `123456ABCD132536`
#### Recovered Plaintext (After Final Permutation): `123456ABCD132536`

### **Strength of DES – Key Size**
- **56-bit keys** have **\(2^{56} = 7.2 \times 10^{16}\)** possible values.
- **Brute force search** seems difficult but has been broken:
  - **1997:** Cracked over the Internet in a few months.
  - **1998:** Cracked using dedicated hardware (EFF) in a few days.
  - **1999:** Combined approach cracked it in **22 hours**.
- **Challenge:** Even if cracked, plaintext recognition is required.
- **Current Status:** DES is considered weak, and alternatives like **AES** are now used.

### **Strength of DES – Timing Attacks**
- **Targets actual cipher implementation** rather than algorithm.
- **Exploits variations in computation time** to extract subkey bits.
- **Smartcards are particularly vulnerable** to this attack.
- **Key Insight:** Different input values cause variations in processing time.

### **Strength of DES – Analytic Attacks**
- Exploit **deep structural properties** of DES.
- Involve **gathering encryption data** to derive sub-key bits.
- If partial key bits are found, an **exhaustive search** can complete the attack.
- **Statistical techniques** are commonly used.

#### **Types of Analytic Attacks:**
1. **Differential Cryptanalysis** – Analyzes how differences in input affect output.
2. **Linear Cryptanalysis** – Uses linear approximations of the cipher to extract key bits.
3. **Related Key Attacks** – Exploits relationships between different encryption keys.

🔒 **Conclusion:** Due to these vulnerabilities, DES is no longer considered secure, and **Triple DES (3DES) and AES** have replaced it in most applications.

### **DES Weaknesses**

#### **Weaknesses in Cipher Design**
1. **Weaknesses in S-boxes** – Some S-boxes exhibit patterns that make them susceptible to cryptanalysis.
2. **Weaknesses in P-boxes** – Certain P-box arrangements can reduce diffusion, making attacks easier.
3. **Weaknesses in Key** – Specific weak keys cause encryption to behave predictably.
![[Pasted image 20250303224308.png]]
#### **Impact of Weak Keys**
- Some **keys are weak** because they **reproduce the original plaintext** after two encryptions.
- This occurs when using the **same key for both encryptions** (not encryption followed by decryption).
- Table 6.18 lists such **weak keys**, which should be avoided in secure implementations.

![[Pasted image 20250303224337.png]]
🔴 **Key Takeaway:**  
- Weak keys **compromise encryption security** by failing to properly obscure plaintext.
- Cryptographers avoid these keys by using **key scheduling algorithms** or **stronger cipher designs** like **AES**.

### **Double Encryption and Decryption with a Weak Key in DES**

#### **Understanding Weak Keys in DES**
- A **weak key** in DES is a key that results in **ciphertext repeating** after **double encryption**.
- If a weak key is used, **encrypting a plaintext twice results in the original plaintext**.
- This happens because the **DES cipher and its inverse cipher cancel each other out** when applied twice.

![[Pasted image 20250303224734.png]]
#### **Process of Double Encryption with a Weak Key**
1. **First Encryption (DES Cipher)**
   - Apply **DES encryption** to the plaintext using a **weak key**.
   - The **output is intermediate ciphertext**.

2. **Second Encryption (DES Cipher Again)**
   - Apply **DES encryption** to the intermediate ciphertext **with the same weak key**.
   - The **resulting output is the original plaintext**.

![[Pasted image 20250303224745.png]]
#### **Process of Double Decryption with a Weak Key**
1. **First Decryption (DES Inverse Cipher)**
   - Apply **DES decryption** to the ciphertext using the **same weak key**.
   - The **output is intermediate plaintext**.

2. **Second Decryption (DES Inverse Cipher Again)**
   - Apply **DES decryption** again with the same weak key.
   - The **resulting output is the original ciphertext**.

![[Pasted image 20250303224754.png]]
#### **Key Observation**
- Normally, encryption does not reverse itself upon a second encryption.
- However, in the case of **weak keys**, the relationship between the **DES cipher and inverse cipher** leads to **plaintext recovery after two encryptions**.
- This makes **double encryption useless** for security when weak keys are used.

![[Pasted image 20250303224806.png]]
#### **Implications**
- Weak keys **should never be used in DES**.
- A secure encryption scheme should **not allow** an encryption operation to behave as a decryption operation under any circumstances.
- This is one of the reasons why DES was **replaced by stronger encryption algorithms** like **Triple DES (3DES) and AES**.

### **Probability of Selecting a Weak, Semi-Weak, or Possible Weak Key**
- DES has a total **key domain** of \( 2^{56} \).
- The total number of weak, semi-weak, and possible weak keys = **64** (4 weak + 12 semi-weak + 48 possible weak).
- The probability of randomly selecting one of these keys:

$$
8.8 \times 10^{-16}
$$

- This probability is **extremely low**, making accidental selection of a weak key almost **impossible**.

---

### **Key Complement Property in DES**
- In DES, every **key has a complement**.
- A **key complement** is created by flipping all bits (changing 0s to 1s and 1s to 0s).
- This property **reduces** the number of keys an attacker needs to test.

#### **Effect on Cryptanalysis**
- Instead of testing **\( 2^{56} \)** possible keys, an attacker only needs to check **\( 2^{55} \)** keys.
- This is because:

$$
C = E(K, P) \Rightarrow C' = E(K', P')
$$

where:
  - \( C' \) is the complement of the ciphertext,
  - \( K' \) is the complement of the key,
  - \( P' \) is the complement of the plaintext.

- Thus, an attacker can **halve the search space** by only testing half of the key domain and then complementing the result.

### **AES: Advanced Encryption Standard**
- **Type:** Symmetric block cipher
- **Developed:** 1999 by independent Dutch cryptographers
- **Usage:** Still widely used

---

### **DES vs. AES Comparison**

| Feature            | **DES**            | **AES**                          |
|--------------------|-------------------|----------------------------------|
| **Date Designed**  | 1976              | 1999                             |
| **Block Size**     | 64 bits           | 128 bits                         |
| **Key Length**     | 56 bits (effective); up to 112 bits with multiple keys | 128, 192, 256 bits (or more) |
| **Rounds**        | 16                 | 10, 12, 14 (based on key length) |
| **Encryption Primitives** | Substitution, permutation | Substitution, shift, bit mixing |
| **Cryptographic Primitives** | Confusion, diffusion | Confusion, diffusion |
| **Design**        | Open               | Open                             |
| **Design Rationale** | Closed          | Open                             |
| **Selection Process** | Secret         | Secret, but open to public comments & criticisms |
| **Source**        | IBM, enhanced by NSA | Independent Dutch cryptographers |

---

### **Public Key (Asymmetric) Cryptography**
- Instead of two users sharing a single **secret key**, each user has:
  - **Public key** (shared with others)
  - **Private key** (kept secret)

### **Public Key (Asymmetric) Cryptography**
- Instead of two users sharing a single **secret key**, each user has:
  - **Public Key:** Can be shared freely.
  - **Private Key:** Must be kept secret.
- **Encryption & Decryption:**  
  - A message encrypted using the **public key** can only be decrypted using the **private key**, and vice versa.

---

### **Secret Key vs. Public Key Encryption**

| Feature            | **Secret Key (Symmetric)**     | **Public Key (Asymmetric)**  |
|--------------------|------------------------------|------------------------------|
| **Number of Keys** | 1                              | 2 (public & private)         |
| **Key Size (bits)** | 56-112 (DES), 128-256 (AES)  | Typically **≥ 256**, often **1000-2000** bits |
| **Key Protection** | Must be kept secret          | **Private key** must be secret, but **public key** can be shared freely |
| **Best Uses**      | General encryption: secrecy & integrity for data, messages, files | **Key exchange, authentication, digital signatures** |
| **Key Distribution** | Must be shared **out-of-band** | **Public key** can be used for secure key distribution |
| **Speed**         | Fast                          | **Much slower** (up to **10,000×** slower than symmetric encryption) |
### **Public-Key Cryptography**
- **Most significant advancement** in cryptography over the past **3000 years**.
- Uses **two keys**: a **public key** and a **private key**.
- **Asymmetric**: The sender and receiver **do not use the same key**.
- Based on **number theoretic principles**.
- **Does not replace** symmetric cryptography but rather **complements it**.

---

### **How Public-Key Cryptography Works**
- **Public-Key**:  
  - **Known to everyone**.
  - Used to **encrypt** messages and **verify** digital signatures.
- **Private-Key**:  
  - **Kept secret** by the recipient.
  - Used to **decrypt** messages and **create** digital signatures.

#### **Asymmetry of Public-Key Cryptography**
- **Encryption & Verification**:  
  - Anyone can encrypt a message or verify a signature.
- **Decryption & Signing**:  
  - Only the owner of the **private key** can decrypt messages or generate valid signatures.
  
![[Pasted image 20250303225934.png]]

### **Keys in Asymmetric Cryptography**
- **Uses two separate keys**:  
  - **Public Key**: Used for encryption or signature verification.
  - **Private Key**: Used for decryption or signing.

![[Pasted image 20250303230127.png]]
![[Pasted image 20250303230203.png]]

### **Why Public-Key Cryptography?**
- **Key Distribution**:  
  - Secure communication without trusting a **Key Distribution Center (KDC)**.
- **Digital Signatures**:  
  - Ensures messages come **intact from the claimed sender**.
- **First Publicly Introduced**:  
  - By **Whitfield Diffie & Martin Hellman** (Stanford University, 1976).
  - Previously known in classified research.

---

### **Public-Key Characteristics**
- **Security Property**:  
  - **Computationally infeasible** to derive the **private key** from the **public key**.
- **Efficiency Property**:  
  - **Easy** to encrypt and decrypt with the corresponding key.
- **Reversibility**:  
  - Either key can be used for **encryption**, with the **other used for decryption** (in some systems).
![[Pasted image 20250303230326.png]]

---

### **Public-Key Applications**
- **Encryption/Decryption** → Provides **secrecy**.
- **Digital Signatures** → Ensures **authentication & integrity**.
- **Key Exchange** → Securely shares **session keys**.

- **Some algorithms support all three**, while others are **optimized for specific functions**.

### **Public Key to Exchange Secret Keys**

![[Pasted image 20250303230410.png]]
![[Pasted image 20250303230417.png]]![[Pasted image 20250303230429.png]]![[Pasted image 20250303230441.png]]
![[Pasted image 20250303230449.png]]
### **Error Detecting Codes**
- Used to **detect** if a block of data has been **modified**.
- **Simple error detecting codes**:
  - **Parity checks** → Detects single-bit errors.
  - **Cyclic redundancy checks (CRC)** → Detects burst errors.
- **Cryptographic error detecting codes**:
  - **One-way hash functions** → Generates a unique hash for integrity verification.
  - **Cryptographic checksums** → Ensures data authenticity.
  - **Digital signatures** → Provides authenticity and integrity.

![[Pasted image 20250303230704.png]]
![[Pasted image 20250303230709.png]]

---

### **Digital Signatures**
- A **unique mark** that only the sender can create.
- **Authentic & Unforgeable**.
- Fixed to the document to verify its integrity.

#### **One-Way Hash Function in Digital Signatures**
1. Compute **message digest** using a **hash function**.
2. Encrypt digest using the sender’s **private key** to create a **digital signature**.
3. The receiver:
   - Decrypts the signature using the **sender’s public key**.
   - Computes the hash of the received message.
   - Compares the computed hash with the decrypted hash → **Ensures authenticity**.

---

### **Certificates: Trustable Identities and Public Keys**
- A **certificate** = **Public Key + Identity**, signed by a **Certificate Authority (CA)**.
- **Certificate Authority (CA)**:
  - A trusted third party that verifies **identities** before issuing certificates.

![[Pasted image 20250303230721.png]]
---

### **Certificate Signing and Hierarchy**
- **Chain of Trust**:
  - **Edward (Root CA)** issues a certificate for **Diana**.
  - **Diana** issues a certificate for **Delwyn**, appending her certificate.
  - **Delwyn’s certificate** is **linked to Diana’s**, which is linked to **Edward’s**, ensuring **trust propagation**.
![[Pasted image 20250303230735.png]]
#### **Example Hierarchy**
1. **Diana’s Certificate**:
   - **Name**: Diana
   - **Position**: Division Manager
   - **Public Key**: `17EF83CA...`
   - **Signed by**: Edward (Root CA)
   - **Hash Value**: `128C4`
   
2. **Delwyn’s Certificate**:
   - **Name**: Delwyn
   - **Position**: Dept Manager
   - **Public Key**: `3AB3882C...`
   - **Signed by**: Diana
   - **Includes Diana’s Certificate**
   - **Hash Value**: `48CFA`

- **Why?**  
  - **Delwyn’s certificate includes Diana’s certificate**, ensuring it can be traced back to **Edward**, forming a **trust chain**.

---

### **HTTPS and Browser Security**
- **HTTPS**:
  - Encrypts communication, reducing data leakage.
  - **Does not prevent tracking**.
- **Browser Fingerprinting**:
  - Even with HTTPS, websites can track users using **browser-specific attributes**.
- **Mitigation**:
  - **"HTTPS Everywhere" Extension**:
    - Enforces **HTTPS** usage wherever possible.
    - **Reduces fingerprinting techniques**.

### **Cryptographic Tool Summary**

| **Tool**                        | **Uses** |
|---------------------------------|----------------------------------------------------------------|
| **Secret key (symmetric) encryption** | Protects **confidentiality** and **integrity** of data at rest or in transit. |
| **Public key (asymmetric) encryption** | - Exchanges **symmetric encryption keys**.  <br> - Signs data to prove **authenticity** and **origin**. |
| **Error detection codes** | Detects **changes** in data. |
| **Hash codes and functions** | Detects **changes** in data (as a form of error detection code). |
| **Cryptographic hash functions** | Detects **changes** in data using a function only the **data owner** can compute. <br> - Prevents attackers from modifying both data and hash to hide modifications. |
| **Error correction codes** | Detects and **repairs** errors in data. |
| **Digital signatures** | **Authenticates** data and ensures **non-repudiation**. |
| **Digital certificates** | **Verifies identities** and allows secure exchange of cryptographic keys. |

### **Summary**
- **Encryption** helps prevent attackers from **revealing, modifying, or fabricating** messages.
- **Symmetric and asymmetric encryption** have **complementary strengths and weaknesses**.
- **Certificates** bind **identities** to **digital signatures** for authentication and trust.

## Made By Yashank