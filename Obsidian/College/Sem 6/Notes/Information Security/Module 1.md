
## **1. Understanding Assets in Information Security**

*   **Definition:** An **asset** in information security is anything valuable to an organization or individual that requires protection.
*   Assets encompass **hardware, software, and data**.

### **1.1. Asset Valuation: Replaceability & Importance**
Assets can be categorized based on how easily they can be replaced (**replaceability**) and their value (**importance**).

*   **Off-the-Shelf Assets:**
    *   **Easily replaceable** with commercially available alternatives (e.g., standard desktop PC, common software like Microsoft Word).
    *   Lower risk impact if lost, but replacement still requires time/effort for setup and configuration.
*   **Unique Assets:**
    *   **Irreplaceable** or extremely difficult/costly to recreate (e.g., proprietary research data, unique source code, personal photos).
    *   Loss can have severe financial, operational, reputational, or emotional consequences.

### **1.2. Types of Assets**

*   **Hardware:** Physical components.
    *   **Computer:** Desktops, laptops, servers.
    *   **Devices:** Storage (HDDs, SSDs), Memory (RAM), Printers, Scanners, Mobile Devices.
    *   **Network gear:** Routers, Switches, Modems, Firewalls (hardware), Cables.
*   **Software:** Programs enabling system functionality.
    *   **Operating system (OS):** Windows, Linux, macOS, iOS, Android. Manages hardware.
    *   **Utilities:** Security tools (**Antivirus, Firewalls**), maintenance tools (**Backup software**, disk cleaners).
    *   **Commercial applications:** Productivity suites (MS Office), design software (Adobe Creative Suite), specific business software (CRM, ERP).
    *   **Individual applications:** Custom-developed software for specific needs, scripts.
*   **Data:** The information itself; often the **most critical and irreplaceable** digital asset.
    *   **Documents:** Reports, spreadsheets, personal notes, academic papers.
    *   **Photos:** Personal memories, professional photography portfolios.
    *   **Music, videos:** Entertainment files, creative works.
    *   **Email:** Communications, attachments, contact lists.
    *   **Class projects / Research Data:** Academic work, experimental results, intellectual property.

*   `[Brief Summary]:` Assets are anything valuable needing protection, categorized by replaceability. Hardware is the physical gear, Software runs on it, and Data is the information itself – often the most crucial asset.

*   `❓ Thought-Provoking Question:` How might the valuation of the *same* asset (e.g., a laptop) differ between a student and a large corporation? What factors influence this?
*   `🔗 Connections:` Asset identification and valuation are the first steps in **Risk Management**. The value assigned to an asset directly influences how much effort and budget should be allocated to protect it.
*   `🌍 Real-World Example:` A hospital's **Patient Health Information (PHI)** is a unique, highly valuable data asset requiring stringent protection due to regulations like HIPAA. The computer displaying it is an off-the-shelf asset, but its *access* to the unique data makes its security critical.
*   `🚩 Further Research/Clarification Needed:` Explore formal methodologies for asset valuation in cybersecurity risk assessments (e.g., Qualitative vs. Quantitative assessment).

*   `🔑 **Main Takeaway:** Identifying and valuing assets (hardware, software, data) based on replaceability and importance is fundamental to knowing what needs protection in information security.`

---

## **2. Defining Information Security & Its Goals (The CIA Triad)**

*   **Definition:** **Information Security** is the practice of protecting information and information systems (including **hardware, software, firmware, data, and telecommunications**) from unauthorized access, use, disclosure, disruption, modification, or destruction.
*   **Core Goal:** To preserve the **Confidentiality, Integrity, and Availability (CIA Triad)** of assets.

### **2.1. Importance of Asset Protection**
*   Protecting assets ensures business continuity, protects privacy, maintains trust, and prevents various losses (financial, reputational, operational).
*   Failure to protect assets can lead to financial penalties, identity theft, operational downtime, and loss of competitive advantage.
*   Essential security measures include **backups, encryption, access control, firewalls, and user training**.

### **2.2. NIST Definition of Computer Security**
*   According to the **National Institute of Standards and Technology (NIST)** Computer Security Handbook:
    > "Computer Security is the protection afforded to an automated information system in order to attain the applicable objectives of preserving the **integrity, availability, and confidentiality** of information system resources (includes **hardware, software, firmware, information/data, and telecommunications**)."

### **2.3. The CIA Triad: Core Security Principles**
This is a foundational model guiding information security practices.

*   **1. Confidentiality:**
    *   **Definition:** Preventing the unauthorized disclosure of information. Ensures assets are accessed **only by authorized parties**.
    *   **Ensures:** Privacy, secrecy. Protects sensitive data (personal, proprietary).
    *   **"Access" includes:** Reading, viewing, printing, or even knowing about the existence of an asset.
    *   **Techniques:** **Encryption**, **Access Controls** (like passwords, permissions, ACLs), **Authentication** (including **Multi-Factor Authentication - MFA**), **Steganography** (hiding data within other data), network segregation.
    *   `[Mentioned Advanced Concepts]:` **Covert channels**, **Cryptographic obfuscation**, **Zero knowledge proofs**. (`🚩 Further Research Needed` on practical applications/details of these advanced concepts).
*   **2. Integrity:**
    *   **Definition:** Ensuring data or systems are trustworthy and have not been improperly modified or destroyed. Assets can be modified **only by authorized parties** in **authorized ways**.
    *   **Ensures:** Accuracy, reliability, trustworthiness, **authenticity**, **non-repudiation** (proof that an action occurred).
    *   **An asset has integrity if it is:** Precise, accurate, unmodified (unless authorized), modified only by authorized entities/processes, consistent, meaningful, usable.
    *   **Techniques:** **Hashing** (e.g., **SHA - Secure Hash Algorithm**), **Checksums**, **Digital Signatures**, **Message Authentication Codes (MAC/HMAC)**, Version Control systems, Access Controls.
    *   `[Note]:` Older hashing algorithms like **MD5 (Message Digest)** are considered insecure for many applications due to collision vulnerabilities.
*   **3. Availability:**
    *   **Definition:** Ensuring that systems and data are accessible and usable upon demand by authorized users.
    *   **Ensures:** Reliable and timely access to resources. Systems are operational when needed.
    *   **An asset has availability if:** It responds timely, is fair to all users (resource allocation), is **fault-tolerant**, manages concurrency/deadlocks.
    *   **Techniques:** **Redundancy** (servers, networks, power), **Backups**, **Disaster Recovery Plans (DRP)**, **Load Balancing**, **DDoS Protection**, High-Availability Clusters, **Failover Systems**.

*   `🧠 Mnemonic:` **CIA** = **C**onfidentiality (Keep it secret), **I**ntegrity (Keep it accurate/trustworthy), **A**vailability (Keep it accessible).
*   `📝 Potential Exam Question:` Define the three components of the CIA Triad. For each component, provide a real-world example of a security breach that violates it and a control mechanism used to uphold it.
*   `📖 Glossary:`
    *   **Confidentiality:** Preventing unauthorized disclosure of information.
    *   **Integrity:** Assuring information trustworthiness and accuracy (preventing unauthorized modification).
    *   **Availability:** Ensuring timely and reliable access to information and systems.
    *   **CIA Triad:** The core security goals of Confidentiality, Integrity, and Availability.
    *   **NIST:** National Institute of Standards and Technology (US agency setting standards).
    *   **Encryption:** Converting data into a coded form to prevent unauthorized access.
    *   **Access Control:** Mechanisms restricting access to resources based on identity/permissions.
    *   **Authentication:** Verifying the identity of a user or system.
    *   **MFA (Multi-Factor Authentication):** Using multiple pieces of evidence to verify identity.
    *   **Hashing:** Creating a fixed-size string (hash) from input data for integrity checks.
    *   **SHA (Secure Hash Algorithm):** A family of cryptographic hash functions.
    *   **MAC/HMAC:** Message Authentication Code / Hash-based MAC; used for integrity and authenticity.
    *   **Non-repudiation:** Assurance that someone cannot deny the validity of something.
    *   **Redundancy:** Duplicating critical components to ensure reliability.
    *   **Backup:** A copy of data taken and stored elsewhere for recovery purposes.
    *   **DDoS (Distributed Denial of Service):** An attack aiming to make a service unavailable by overwhelming it with traffic.
    *   **Steganography:** Hiding data within other non-secret files/messages.

*   `🔑 **Main Takeaway:** Information security aims to protect assets by ensuring their Confidentiality (secrecy), Integrity (trustworthiness), and Availability (accessibility), collectively known as the CIA Triad.`

---

## **3. Threats, Vulnerabilities, and Controls**

### **3.1. Key Concepts**

*   **Vulnerability:** A **weakness** in a system, process, or control that could potentially be exploited. (e.g., unpatched software, weak password, unlocked door).
*   **Threat:** A **potential danger** or agent that might exploit a vulnerability to cause harm. (e.g., malware, hacker, fire, human error).
*   **Attack:** An **actual attempt** by a threat agent to exploit a vulnerability.
*   **Countermeasure (Control):** A **safeguard or defense** mechanism put in place to mitigate threats, reduce vulnerabilities, or lessen the impact of an attack.

*   `[Analogy - Dam]:`
    *   **Threat:** The **water** pressure against the dam.
    *   **Vulnerability:** A **crack** in the dam wall.
    *   **Control:** A **finger plugging the crack** (temporary), or repairing the dam (permanent).
    *   **Attack:** Water actively exploiting the crack, potentially leading to a breach.

### **3.2. Types of Threats**

*   `[VISUAL: Diagram showing Threat Sources - Branching from Natural (Random) and Human (Benign Intent - Error; Malicious Intent - Random Attack, Directed Attack)]`
*   **Based on Cause & Intent:**
    *   **Natural Causes:** Random events beyond human control.
        *   *Examples:* Fire, flood, earthquake, power failure.
    *   **Human Causes:**
        *   **Benign Intent (Errors):** Unintentional mistakes.
            *   *Example:* Accidental deletion of files, misconfiguration of a server.
        *   **Malicious Intent (Attacks):** Deliberate actions to cause harm.
            *   *Random Attack:* Affects victims indiscriminately (e.g., mass phishing emails, malware on a general website).
            *   *Directed Attack:* Targets a specific individual or organization (e.g., spear phishing, targeted hacking).

### **3.3. Advanced Persistent Threat (APT)**

*   **Definition:** **Highly organized, well-funded, sophisticated, and targeted attacks**, often state-sponsored or run by large criminal groups.
*   **Characteristics:**
    *   **Organized:** Conducted by skilled teams.
    *   **Directed:** Specifically targets high-value organizations/individuals.
    *   **Well-financed:** Significant resources available.
    *   **Patient & Silent:** Operate over long periods, avoiding detection.
*   **Quote:** "Security experts believe that high-priority targets can never be **fully** safe from APTs."
*   `🌍 Real-World Example:` State-sponsored cyber-espionage groups targeting government agencies or critical infrastructure.
*   `🔗 Connections:` APTs often combine multiple attack vectors and exploit zero-day vulnerabilities. Defending against them requires advanced, multi-layered security (Defense in Depth).

### **3.4. Types of Attackers**

*   **Criminals-for-hire:** Mercenaries motivated by financial gain.
*   **Organized crime members:** Syndicates involved in large-scale cybercrime (ransomware, fraud).
*   **Individual hackers:** Motivated by various factors (money, ideology, challenge, revenge).
*   **Terrorists:** Use cyberattacks for political/ideological disruption or destruction.
*   **Loosely connected groups (Hacktivists):** Ideologically motivated groups (e.g., Anonymous).
*   **Note:** Each attacker type possesses **different resources, capabilities, and motivations**, influencing the threat landscape.

*   `❓ Thought-Provoking Question:` How would security defenses differ when protecting against a script kiddie using known tools versus a well-funded APT group?
*   `🚩 Further Research/Clarification Needed:` Look into specific APT groups (e.g., APT28, APT29) and their known tactics, techniques, and procedures (TTPs).

*   `🔑 **Main Takeaway:** Security involves understanding vulnerabilities (weaknesses), threats (potential dangers like attackers or nature), and implementing controls (safeguards) to prevent attacks. Threats can range from accidental errors to highly sophisticated APTs.`

---

## **4. Types of Harm and Security Attacks**

### **4.1. Types of Harm**
Attacks aim to cause harm by impacting assets in one or more of these ways:

1.  **Interception (Loss of Confidentiality):** Unauthorized access to or disclosure of information.
    *   *Examples:* Eavesdropping, packet sniffing, Man-in-the-Middle (MITM) attacks, shoulder surfing.
2.  **Interruption (Loss of Availability):** Making assets unusable or unavailable.
    *   *Examples:* **Denial of Service (DoS/DDoS)**, ransomware encrypting files, hardware destruction, power outage.
3.  **Modification (Loss of Integrity):** Unauthorized alteration of data or system configuration.
    *   *Examples:* Changing data in a database, defacing a website, modifying system logs, code injection.
4.  **Fabrication (Loss of Authenticity/Integrity):** Creating counterfeit objects or inserting false data into a system.
    *   *Examples:* Impersonation, sending emails pretending to be someone else (spoofing), injecting malicious code or fake transactions, creating fake user credentials.

*   `[Brief Summary]:` Harm involves unauthorized viewing (Interception), blocking access (Interruption), changing data (Modification), or creating fake data/identities (Fabrication).

### **4.2. Security Attacks (Mapping Harm to CIA)**

*   **Interruption:** Attack on **Availability** (and potentially Confidentiality if disruption reveals info).
    *   *Examples:* DDoS, Ransomware, Cutting a network cable.
*   **Interception:** Attack on **Confidentiality**.
    *   *Examples:* Eavesdropping, MITM, Packet Sniffing, Wiretapping.
*   **Modification:** Attack on **Integrity**.
    *   *Examples:* Tampering with files, Database manipulation, Code injection (e.g., SQL injection).
*   **Fabrication:** Attack on **Authenticity** (a component of Integrity).
    *   *Examples:* Spoofing identities, Inserting fake records, Counterfeit certificates, Malware injection.

*   `🔗 Connections:` Understanding these harm types is crucial for **Threat Modeling** and **Risk Assessment** – determining what bad things could happen and how likely/impactful they are.
*   `📝 Potential Exam Question:` Describe the four main types of security harm (Interruption, Interception, Modification, Fabrication) and provide a specific attack example for each, linking it to the affected CIA principle(s).

*   `🔑 **Main Takeaway:** Attacks aim to cause harm by intercepting, interrupting, modifying, or fabricating information/system access, directly violating the principles of Confidentiality, Integrity, or Availability.`

---

## **5. Controls and Countermeasures**

*   **Definition:** Controls are the measures implemented to **prevent, detect, deter, or respond** to threats and mitigate risks.

### **5.1. Control Categorization**

![[Pasted image 20250428230006.png]]

*   **Based on CIA Triad Protection:**
    *   **Confidentiality Controls:** Encryption, Access Control Lists (ACLs), VPNs.
    *   **Integrity Controls:** Hashing, Digital Signatures, Checksums, File Integrity Monitoring (FIM).
    *   **Availability Controls:** Load Balancing, Redundancy (RAID, server clusters), Backups, DDoS Mitigation Services.
*   **Based on Implementation Type:**
    *   **1. Technical Controls:** Implemented using technology.
        *   *Examples:* **Firewalls**, **Intrusion Detection Systems (IDS)** / Intrusion Prevention Systems (IPS), **Encryption**, Antivirus Software, Authentication Systems (e.g., Smart Cards), Hardware Locks.
        *   *Software Controls:* Input validation, secure coding practices, OS access restrictions, Password Managers.
        *   *Development Controls:* Secure Software Development Lifecycle (SSDLC) practices.
    *   **2. Administrative (or Procedural) Controls:** Implemented through policies, procedures, and guidelines.
        *   *Examples:* **Security Policies**, **Employee Training & Awareness**, **Audits**, Background Checks, Incident Response Plans, Compliance Regulations.
    *   **3. Physical Controls:** Protect physical access to systems and infrastructure.
        *   *Examples:* Locks, **Biometric Authentication** (fingerprint, retina scan), **CCTV Cameras**, Security Guards, Fences, Mantraps, Environmental Controls (fire suppression, HVAC).
*   **Based on Threat Interaction (Where the threat comes from):**
    *   *Human vs. Non-Human Threats:* User training vs. Antivirus.
    *   *Malicious vs. Non-Malicious Threats:* IDS vs. Backup procedures.
    *   *Directed vs. Non-Directed Threats:* Threat intelligence vs. General firewall rules.

### **5.2. Functional Types of Controls**

![[Pasted image 20250428231556.png]]

*   **1. Prevention Controls:** Stop an incident from occurring.
    *   *Internal Prevention:* User Authentication, Role-Based Access Control (RBAC), Permissions.
    *   *External Prevention:* Firewalls, VPNs, Anti-Malware, Network Segmentation.
*   **2. Detection Controls:** Identify that an incident has occurred or is in progress.
    *   *Examples:* **Intrusion Detection Systems (IDS)**, Security Information and Event Management (SIEM) systems, Log Monitoring, Security Cameras.
*   **3. Deterrence Controls:** Discourage potential attackers.
    *   *Internal Deterrence:* Security Policies, User Monitoring, Access Logs, Warnings.
    *   *External Deterrence:* Warning banners (e.g., on login screens), Visible security measures (cameras, guards), Threat of legal consequences.
*   **4. Response (Corrective) Controls:** React to and mitigate the impact of an incident.
    *   *Examples:* **Incident Response Teams (IRT)**, Automated attack containment, Forensic analysis tools, Backup restoration.
*   **5. Preemption (Proactive) Controls:** Identify and neutralize threats *before* they can cause harm.
    *   *Examples:* **Threat Intelligence** feeds, Vulnerability scanning, **Penetration testing**, Anomaly detection.
*   **6. Deflection Controls:** Redirect attackers away from critical assets, often to decoys.
    *   *Examples:* **Honeypots**, Honeynets, Deceptive DNS responses, Sandboxing environments.

*   `🌍 Real-World Example:` A bank uses:
    *   *Prevention:* Strong passwords (Technical), ID checks (Physical), login firewalls (Technical).
    *   *Detection:* Security cameras (Physical), Fraud detection algorithms (Technical), Log analysis (Technical/Procedural).
    *   *Deterrence:* Warning signs about surveillance (Physical), Prosecution policies (Administrative).
    *   *Response:* Incident response plan (Administrative), Freezing accounts (Procedural).

### **5.3. Attack Requirements: Method, Opportunity, Motive (MOM)**
For an attack to succeed, the attacker typically needs:

*   **Method:** The skills, tools, knowledge, and techniques required to perform the attack.
*   **Opportunity:** The time and access needed to exploit a vulnerability.
*   **Motive:** The reason or goal driving the attack (e.g., financial gain, espionage, disruption).
*   **Note:** **Denying any one of these three factors can prevent or thwart an attack.** Controls often aim to eliminate or reduce one or more of these.
*   `🧠 Mnemonic:` Think **MOM** – an attacker needs all three to succeed.

### **5.4. Methods of Defense (Control Strategies)**
These align with the functional types of controls:

1.  **Prevent:** Block the attack or fix the vulnerability (e.g., patching, strong authentication).
2.  **Deter:** Make the attack harder or less attractive (e.g., warnings, visible security).
3.  **Deflect:** Redirect the attack (e.g., honeypot).
4.  **Mitigate:** Reduce the impact if an attack succeeds (e.g., backups, incident response).
5.  **Detect:** Identify the attack occurring or after the fact (e.g., IDS, logs).
6.  **Recover:** Restore systems and data after an attack (e.g., backups, DRP).

### **5.5. Effectiveness of Security Controls**
Controls are only effective if:

1.  **Awareness of the Problem:** Users and administrators understand the risks.
2.  **Likelihood of Use:** Controls are **easy, efficient, and practical** (users won't bypass overly cumbersome security).
3.  **Layered Security (Defense in Depth):** Multiple, overlapping controls are implemented (no single point of failure).
4.  **Periodic Reviews:** Controls are regularly reviewed, tested, and updated.

*   `🚩 Further Research/Clarification Needed:` Explore specific control frameworks like the NIST Cybersecurity Framework or ISO 27001.
*   `📝 Potential Exam Question:` Explain the concept of "Defense in Depth" and provide an example of how multiple control types (technical, administrative, physical) could be layered to protect a sensitive database server.

*   `🔑 **Main Takeaway:** Controls are essential defenses categorized by CIA goal, implementation type, and function (prevent, detect, etc.). Effective security uses layered controls (Defense in Depth) and considers the attacker's Method, Opportunity, and Motive (MOM).`

---

## **6. Additional Vulnerabilities**

### **6.1. Network and Access Vulnerabilities**

*   **Networks:**
    *   Lack of **physical proximity** control (remote attackers).
    *   Often use **shared, potentially insecure** transmission media (e.g., public Wi-Fi, the Internet).
    *   Difficulty in reliably verifying **remote user identities**.
*   **Access:**
    *   Risk of **unauthorized computer usage**.
    *   Potential for **malicious access** attempts (hacking).
    *   Vulnerability to **Denial of Service (DoS)** attacks against legitimate users.

### **6.2. Human Element Vulnerabilities**

*   **Key People:** Employees with **privileged access** (admins, executives) are high-value targets.
*   **Social Engineering:** Manipulating people to bypass security controls or divulge sensitive information (e.g., phishing, pretexting).

*   **Quote:** "**Security is an ongoing process requiring continuous improvement and adaptation.**"

---

## **7. Fundamentals of Encryption**

*   **Purpose:** Encryption transforms readable data (**Plaintext**) into an unreadable format (**Ciphertext**) to protect it from unauthorized parties.
*   **Problems Addressed:** Helps prevent attackers who might try to:
    *   **Intercept (Eavesdrop):** Read the message content.
    *   **Modify:** Alter the message content without detection (when combined with integrity checks).
    *   **Fabricate:** Create fake messages appearing authentic (when combined with authentication).
    *   *(Note: Encryption alone doesn't prevent blocking/interruption, which affects Availability).*

### **7.1. Encryption Terminology**

*   **Plaintext:** The original, readable message or data.
*   **Ciphertext:** The encrypted, unreadable (scrambled) message or data.
*   **Encrypt / Encode / Encipher:** The process of converting plaintext to ciphertext.
*   **Decrypt / Decode / Decipher:** The process of converting ciphertext back to plaintext.
*   **Algorithm (Cipher):** The mathematical rules or procedures used for encryption and decryption.
*   **Key:** A piece of secret information (like a password) used by the algorithm to encrypt or decrypt. The security of most modern systems relies on the secrecy of the key, not the algorithm.
*   **Cryptosystem:** The complete system including the algorithm, key(s), and procedures for use.
*   **Sender:** The entity transmitting the message.
*   **Recipient:** The intended receiver of the message.
*   **Transmission Medium:** The channel used for communication (e.g., internet, radio waves).
*   **Interceptor / Intruder / Attacker:** An unauthorized party attempting to access/modify the message.

### **7.2. Encryption/Decryption Process**

*   `[VISUAL: Diagram showing: Plaintext -> ENCRYPT (using Key) -> Ciphertext -> TRANSMIT -> Ciphertext -> DECRYPT (using Key) -> Plaintext]`
1.  **Encryption:** `Ciphertext = Encrypt(Key, Plaintext)`
2.  **Decryption:** `Plaintext = Decrypt(Key, Ciphertext)`

### **7.3. Symmetric vs. Asymmetric Encryption**

*   **1. Symmetric Encryption (Secret Key Cryptography):**
    *   Uses the **same single key** for both encryption and decryption.
    *   **Key must be kept secret** and shared securely between sender and recipient beforehand.
    *   **Advantages:** Very **fast** and efficient. Good for encrypting large amounts of data.
    *   **Disadvantages:** **Secure key distribution** is a major challenge. The number of keys needed grows rapidly with the number of users (`n*(n-1)/2` keys for `n` users).
    *   **Examples:** **DES, 3DES, AES**, RC4, Blowfish.
*   **2. Asymmetric Encryption (Public Key Cryptography):**
    *   Uses a **pair of mathematically related keys:** a **Public Key** and a **Private Key**.
    *   **Public Key:** Can be shared freely with anyone. Used to encrypt data or verify signatures.
    *   **Private Key:** Must be kept **strictly secret** by the owner. Used to decrypt data or create signatures.
    *   **How it works:** Data encrypted with the public key can *only* be decrypted with the corresponding private key (and vice-versa in some algorithms).
    *   **Advantages:** Solves the **key distribution problem** (public keys can be shared openly). Enables **digital signatures** for authentication and non-repudiation.
    *   **Disadvantages:** Much **slower** than symmetric encryption (thousands of times slower).
    *   **Examples:** **RSA, ECC (Elliptic Curve Cryptography), Diffie-Hellman** (key exchange).

| **Symmetric Key Encryption**                                                                                                                                                                                       | **Asymmetric Key Encryption**                                                                                                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| It only requires a single key for both encryption and decryption.                                                                                                                                                  | It requires two keys, a public key and a private key, one to encrypt and the other to decrypt.                                                                                                                                              |
| The size of ciphertext is the same or smaller than the original plaintext.                                                                                                                                         | The size of ciphertext is the same or larger than the original plaintext.                                                                                                                                                                   |
| The encryption process is very fast.                                                                                                                                                                               | The encryption process is slow.                                                                                                                                                                                                             |
| It is used when a large amount of data needs to be transferred.                                                                                                                                                    | It is used to transfer small amount of data.                                                                                                                                                                                                |
| It only provides confidentiality.                                                                                                                                                                                  | It provides confidentiality, authenticity, and non-repudiation.                                                                                                                                                                             |
| The length of key used is 128 or 256 bits                                                                                                                                                                          | The  length of key used is 2048 or higher                                                                                                                                                                                                   |
| In symmetric key encryption, resource utilization is low compared to asymmetric key encryption.                                                                                                                    | In asymmetric key encryption, resource utilization is high.                                                                                                                                                                                 |
| It is efficient as it is used for handling large amount of data.                                                                                                                                                   | It is comparatively less efficient as it can handle a small amount of data.                                                                                                                                                                 |
| Security is lower as only one key is used for both encryption and decryption purposes.                                                                                                                             | Security is higher as two keys are used, one for encryption and the other for decryption.                                                                                                                                                   |
| The Mathematical Representation is as follows-  <br>P = D (K, E(K, P))<br><br>where K –> encryption and decryption key  <br>P –> plain text  <br>D –> Decryption   <br>E(K, P) –> Encryption of plain text using K | The Mathematical Representation is as follows-  <br>P = D(Kd, E (Ke,P))  <br>where Ke –> encryption key<br><br>Kd –> decryption key  <br>D –> Decryption  <br>E(Ke, P) –> Encryption of plain text using encryption key Ke. P –> plain text |
| ****Examples:**** 3DES, AES, DES and RC4                                                                                                                                                                           | ****Examples:**** Diffie-Hellman, ECC, El Gamal, DSA and RSA                                                                                                                                                                                |

| Feature          | Symmetric Encryption              | Asymmetric Encryption             |
| :--------------- | :-------------------------------- | :-------------------------------- |
| **Key Usage**    | **Single shared secret key**      | **Pair of keys (Public/Private)** |
| **Key Sharing**  | Difficult, must be secure         | Easy (share Public Key)           |
| **Speed**        | **Fast**                          | **Slow**                          |
| **Primary Use**  | **Confidentiality** (bulk data)   | **Key Exchange, Digital Signatures, Authentication** |
| **Examples**     | **AES, DES, 3DES**                | **RSA, ECC, Diffie-Hellman**      |

*   `🚩 Clarification Needed:` Why exactly is asymmetric encryption so much slower? (Relates to the complex mathematical operations involved, often based on large prime numbers).
*   `📝 Potential Exam Question:` Compare and contrast symmetric and asymmetric encryption, discussing their key characteristics, advantages, disadvantages, and typical use cases.
*   `📖 Glossary:`
    *   **Plaintext:** Original readable data.
    *   **Ciphertext:** Encrypted unreadable data.
    *   **Encrypt/Decrypt:** Processes of converting between plaintext and ciphertext.
    *   **Algorithm (Cipher):** Rules for encryption/decryption.
    *   **Key:** Secret value used with the algorithm.
    *   **Symmetric Encryption:** Uses one shared secret key.
    *   **Asymmetric Encryption:** Uses a public/private key pair.
    *   **Public Key:** Key shared openly in asymmetric crypto.
    *   **Private Key:** Secret key kept by owner in asymmetric crypto.
    *   **DES, 3DES, AES:** Examples of symmetric algorithms.
    *   **RSA, ECC, Diffie-Hellman:** Examples of asymmetric algorithms/protocols.

*   `🔑 **Main Takeaway:** Encryption scrambles data for confidentiality using algorithms and keys. Symmetric uses one shared key (fast, key distribution issue), while Asymmetric uses a public/private key pair (slower, solves key distribution, enables signatures).`

---

## **8. Cipher Types and Cryptographic Principles**

### **8.1. Stream Ciphers vs. Block Ciphers**

*   **1. Stream Ciphers:**
    *   Encrypt data **one bit or one byte at a time**.
    *   Often use a pseudorandom keystream XORed with the plaintext.
    *   **Suitable for:** Real-time communication where data arrives continuously (e.g., voice calls, video streaming).
    *   **Examples:** RC4 (dated), ChaCha20, A5/1 (GSM).

![[Pasted image 20250428233550.png]]

*   **2. Block Ciphers:**
    *   Encrypt data in **fixed-size blocks** (e.g., 64 bits for DES, 128 bits for AES).
    *   Plaintext is padded to a multiple of the block size if necessary.
    *   Operate in different *modes* (e.g., ECB, CBC, CTR) to handle multiple blocks securely.
    *   **Suitable for:** Encrypting files, database fields, network packets where data size is known or can be buffered.
    *   **Examples:** **DES, AES**, Blowfish, Twofish.

![[Pasted image 20250428233557.png]]



### **8.2. Core Cryptographic Principles: Diffusion & Confusion**
These concepts, introduced by Claude Shannon, are essential for making ciphers resistant to cryptanalysis.

*   **1. Diffusion:**
    *   **Goal:** To **spread the influence of plaintext bits** over many ciphertext bits. Hides statistical patterns in the plaintext.
    *   **How it works:** Changing a single plaintext bit should ideally change roughly half the ciphertext bits (Avalanche Effect). Achieved through permutations (shuffling bits).
    *   **Effect:** Makes it difficult for attackers to find relationships between plaintext and ciphertext.
*   **2. Confusion:**
    *   **Goal:** To **obscure the relationship between the ciphertext and the key**.
    *   **How it works:** Makes the encryption process highly non-linear using complex substitutions.
    *   **Effect:** Makes it hard to deduce the key even if an attacker has large amounts of plaintext/ciphertext pairs. Achieved through substitution boxes (S-Boxes).

*   `🧠 Mnemonic:` **D**iffusion **S**preads (plaintext influence). **C**onfusion **C**onceals (key relationship).

### **8.3. Stream vs. Block Cipher Comparison**

![[Pasted image 20250428233536.png]]

| Feature           | **Stream Ciphers**                     | **Block Ciphers**                            |
| :---------------- | :------------------------------------- | :------------------------------------------- |
| **Advantages**    | ✅ **Fast**                             | ✅ **High Diffusion** (good mixing)           |
|                   | ✅ Low error propagation (bit errors don't spread far) | ✅ More resistant to insertions/modifications |
| **Disadvantages** | ❌ **Low Diffusion** (simpler mixing)   | ❌ **Slower** than stream ciphers           |
|                   | ❌ Vulnerable to modifications (if keystream reused) | ❌ Error propagation (in some modes)        |
|                   |                                        | ❌ Requires padding for partial blocks        |

*   `📖 Glossary:`
    *   **Stream Cipher:** Encrypts data bit-by-bit or byte-by-byte.
    *   **Block Cipher:** Encrypts data in fixed-size blocks.
    *   **Diffusion:** Spreading plaintext influence across ciphertext.
    *   **Confusion:** Obscuring the relationship between ciphertext and key.
    *   **Avalanche Effect:** Small change in input (plaintext/key) causes large change in output (ciphertext).

*   `🔑 **Main Takeaway:** Ciphers can process data as streams (bit-by-bit, fast) or blocks (fixed chunks, better diffusion). Strong ciphers rely on Diffusion (spreading plaintext effect) and Confusion (hiding key relationship) to resist attacks.`

### **9. Data Encryption Standard (DES)**

*   **Type:** **Symmetric block cipher**. Think of DES as a recipe (algorithm) for scrambling data. It's **symmetric**, meaning you use the exact same secret key to both scramble (encrypt) and unscramble (decrypt) your message. It's a **block cipher**, which means it works on fixed-size chunks of data – in DES's case, chunks of **64 bits** (8 bytes) at a time.
*   **History:** Developed by IBM in the 1970s, adopted as a standard by **NIST** in **1976**. It was widely used for many years.
*   **Specifications:**
    *   Operates on **64-bit blocks** of plaintext/ciphertext.
    *   Uses a **56-bit key**. The key is technically 64 bits long, but 8 of those bits are just for error checking (parity bits) and aren't used in the actual encryption process. So, the *effective* key strength comes from these 56 bits.
        $\text{Key Size:} \quad 64 \text{ bits (8 parity) } \rightarrow 56 \text{ effective bits}$
        $\text{Block Size:} \quad 64 \text{ bits}$

*   **Current Status:** **Considered insecure and obsolete**. The primary reason is the small 56-bit key size. With modern computers, trying out all $2^{56}$ possible keys (**brute-force attack**) is quite feasible. It's like having a combination lock with too few numbers – someone can just sit there and try all the combinations relatively quickly.

### **9.1. DES Variants**

Because plain DES became too weak, people developed ways to apply it multiple times to increase security.

| Form                            | Operation Explained                                                                        | Effective Key Size (Bits) | Real-World Security (Approx. Effort to Break) | Notes                                                                                                                                    |
| :------------------------------ | :----------------------------------------------------------------------------------------- | :------------------------ | :-------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------- |
| **DES**                         | Basic encryption with one key (K1). $C = E_{K1}(P)$                                        | **56**                    | $~2^{56}$ (Very Weak)                           | Vulnerable to brute-force. Easily broken today.                                                                                          |
| **Double DES (2DES)**           | Encrypt with K1, then encrypt the result *again* with K2. $C = E_{K2}(E_{K1}(P))$           | **112** (56+56)           | $~2^{57}$ (Still Weak)                          | **Vulnerable to Meet-in-the-Middle attack.** This clever attack means it's only slightly harder to break than single DES ($2^{56+1}$), not $2^{112}$ harder. Rarely used because it offers little benefit over DES. |
| **Two-key Triple DES (3DES)**   | Encrypt (K1) -> **Decrypt** (K2) -> Encrypt (K1). $C = E_{K1}(D_{K2}(E_{K1}(P)))$         | **112** (56+56, K1 reused)  | $~2^{112}$ (Stronger)                           | Using Decrypt in the middle provides backward compatibility (if K1=K2, it's just DES) and avoids certain attacks. This was a very common standard. Security is generally considered equivalent to attacking a 112-bit key cipher ($~2^{112}$ effort). |
| **Three-key Triple DES (3DES)** | Encrypt (K1) -> **Decrypt** (K2) -> Encrypt (K3). $C = E_{K3}(D_{K2}(E_{K1}(P)))$         | **168** (56+56+56)        | $~2^{112}$ (Strongest DES variant)              | Uses three independent keys. Although the key length is 168 bits, the most effective attacks still require effort around $~2^{112}$. This is the most secure 3DES version. |

*   **Security Concerns:**
    *   **DES:** Broken easily by brute force. Do not use.
    *   **3DES:** Significantly slower than modern ciphers like AES. Its 64-bit block size also makes it vulnerable to attacks like "Sweet32" when encrypting very large amounts of data (terabytes) under the same key. It is being deprecated and phased out.
    *   **AES (Advanced Encryption Standard):** The **recommended modern replacement**. It supports larger key sizes (128, 192, 256 bits), uses a 128-bit block size, is faster, and is more secure.

### **9.2. DES Structure and Process**

DES scrambles data using a structured approach called a **Feistel Network**.

![[Pasted image 20250428233642.png]]
![[Pasted image 20250430193058.png]]

*   **Overall Structure:** Uses a **Feistel Network** structure.
    1.  **Initial Permutation (IP):** The input 64-bit block of data has its bits shuffled around according to a fixed table. Think of it like rearranging a deck of cards in a specific, predefined way. This step doesn't add cryptographic security itself but was likely useful for hardware implementation or loading data efficiently back in the 1970s.
    2.  **16 Rounds of Processing:** This is where the core scrambling happens. Th e 64-bit block goes through 16 identical rounds of complex operations (substitution and permutation). Each round uses a different *subkey* derived from the main 56-bit key.
    3.  **Final Permutation (FP):** After the 16 rounds, the bits are shuffled one last time using another fixed table. This FP is the exact inverse of the Initial Permutation (IP), undoing the initial shuffle. 

*   **Key Schedule:**
    *   You don't use the same 56-bit key directly in each of the 16 rounds. Instead, DES has a process called the **key schedule** that generates **16 different 48-bit "round keys"** (or subkeys), $K_1, K_2, ..., K_{16}$, from your original 56-bit key.
    *   This involves several steps:
        *   An initial permutation of the 56 effective key bits (using a table called Permuted Choice 1, PC-1).
        *   Splitting the result into two 28-bit halves (denoted $C_0$ and $D_0$).
        *   For each round $i$ from 1 to 16:
            *   Rotating each half ($C_{i-1}$, $D_{i-1}$) left by 1 or 2 bit positions (the number of shifts depends on the round number). This gives $C_i, D_i$.
            *   Combining the shifted halves ($C_i D_i$) and then selecting and permuting 48 bits using another table (Permuted Choice 2, PC-2) to produce the 48-bit round key $K_i$.
    *   The goal is to ensure each round uses a different, seemingly unrelated piece of the original key information, adding complexity.
    *   `[VISUAL: Diagram illustrating the key schedule process: 56-bit Key -> PC-1 -> Split C0/D0 -> 16 rounds of (Left Shift + PC-2 -> 48-bit Round Key)]` *(Your note implies a diagram here)*

### **9.3. DES Rounds and Feistel Cipher**

![[Pasted image 20250428233721.png]]

The beauty of the Feistel structure is how each of the 16 rounds works and how it naturally allows decryption using the same algorithm.

*   **Structure of Each Round (i = 1 to 16):**
    1.  **Input:** Take the 64-bit block output from the previous round (or from IP for round 1). Split it into two equal halves: a 32-bit Left half $L_{i-1}$ and a 32-bit Right half $R_{i-1}$.
    2.  **Apply Round Function (f):** The core of the round. This function $f$ takes the Right half $R_{i-1}$ and the specific 48-bit round key for this round $K_i$ as input. It performs a series of expansions, XORs, substitutions (S-Boxes), and permutations (P-Box) to produce a 32-bit output. (More details on function $f$ in section 9.4).
    3.  **XOR:** The 32-bit output of the function $f(R_{i-1}, K_i)$ is XORed with the *original* Left half $L_{i-1}$. The XOR operation ($\oplus$) is a bitwise exclusive OR.
    4.  **Swap:** The *original* Right half $R_{i-1}$ becomes the *new* Left half $L_i$ for the next round. The result of the XOR operation becomes the *new* Right half $R_i$ for the next round.
        *   In formula terms:
            $L_i = R_{i-1}$
            $R_i = L_{i-1} \oplus f(R_{i-1}, K_i)$

    ![[Pasted image 20250430193414.png]]

    5.  **Exception:** The **swap is *not* performed** after the final round (Round 16). The output of round 16 ($L_{16}, R_{16}$) goes directly to the Final Permutation (FP). (Some diagrams might show a swap after round 16 followed by another swap immediately after FP, which mathematically cancels out, achieving the same result). 

*   **Decryption:** The elegance of the Feistel network is that decryption uses the *exact same algorithm* as encryption. The only difference is that you must apply the **round keys $K_1, ..., K_{16}$ in the reverse order** ($K_{16}$ in the first decryption round, $K_{15}$ in the second, ..., down to $K_1$ in the last decryption round). The structure ensures that the XOR operations effectively cancel out the encryption process when the keys are reversed.

### **9.4. The DES Function (f)**

![[Pasted image 20250428233756.png]]

This is the complex "mangler" function inside each round, labeled $f$. It takes the 32-bit Right half ($R_{i-1}$) and the 48-bit round key ($K_i$) and produces a 32-bit output. Its primary job is to provide **confusion** (making the relationship between the key and the ciphertext obscure) and **diffusion** (spreading the influence of a single plaintext bit across many ciphertext bits).

*   **Purpose:** Provides the core **confusion and diffusion** within each round. Operates on the 32-bit Right half $R_{i-1}$ using the 48-bit Round Key $K_i$.
*   **Steps:**
    1.  **Expansion (P-Box):** The 32-bit input $R_{i-1}$ is expanded to **48 bits**. This is done using a fixed table called the **Expansion Permutation (E)**. This table rearranges the bits and *duplicates* 16 of them, ensuring each input bit affects multiple S-Boxes in the next step. The expansion is necessary to match the size of the 48-bit round key.

       ${E-Box (Expansion):} \quad R_{i-1} (32 \text{ bits}) \rightarrow \text{Expanded } R'_{i-1} (48 { bits})$

        ![[Pasted image 20250428234030.png]]

    2.  **Key Mixing (Whitener):** The 48-bit expanded block $R'_{i-1}$ is **XORed** ($\oplus$) with the 48-bit **Round Key $K_i$**. This step directly mixes the secret key material into the data being processed.

        $\text{Result}_1 = R'_{i-1} \oplus K_i \quad (48 \text{ bits})$
        
        ![[Pasted image 20250430194021.png]]
    

    3.  **Substitution (S-Boxes):** This is the most critical step for DES's security and its **only non-linear element**. Non-linearity makes the cipher resistant to simpler mathematical attacks.
        *   The 48-bit result ($\text{Result}_1$) is divided into **eight 6-bit blocks**.
        *   Each 6-bit block goes into a *different*, specific **Substitution Box (S-Box)**. There are 8 unique S-Boxes defined in the standard (S1, S2, ..., S8).
        *   Each S-Box is a predefined lookup table. It takes a **6-bit input** and produces a **4-bit output**.
        *   **Input interpretation for an S-Box:** For a 6-bit input (let's label the bits $b_1 b_2 b_3 b_4 b_5 b_6$):
            *   The outer two bits ($b_1$ and $b_6$) combine to form a 2-bit number that selects the **row** of the lookup table (Row 0, 1, 2, or 3).
            *   The middle four bits ($b_2 b_3 b_4 b_5$) form a 4-bit number that selects the **column** of the lookup table (Column 0 to 15).
            *   The value found in the S-Box table at the selected row and column is the 4-bit output.
        *   The 8 S-Boxes together produce a total of $8 \times 4 = 32$ bits of output.
        *   The specific values within the S-Boxes were carefully chosen (though controversially kept secret initially) to resist attacks known at the time (like differential cryptanalysis).

        $\text{S-Boxes:} \quad \text{Result}_1 (48 \text{ bits}) \rightarrow 8 \times S_j(\text{6-bit chunk}_j) \rightarrow \text{Result}_2 (32 \text{ bits})$

        ![[Pasted image 20250430193822.png]]
        ![[Pasted image 20250430193837.png]]
        ![[Pasted image 20250430193850.png]]
    4.  **Permutation (P-Box):** The resulting 32 bits ($\text{Result}_2$) from the S-Boxes are then passed through *another* fixed permutation table, simply called **Permutation (P)**. This P-box rearranges the order of the 32 bits, ensuring that the output bits from one S-Box in this round are spread out and affect different S-Boxes in the next round. This provides **diffusion**.

        $\text{P-Box (Permutation):} \quad \text{Result}_2 (32 \text{ bits}) \rightarrow \text{Output of } f \text{ function } (32 \text{ bits})$

        ![[Pasted image 20250428233958.png]]

The final 32-bit output of this P-Box is the result of the entire round function $f(R_{i-1}, K_i)$.

Below is the Entire process for DES

![[Pasted image 20250430193921.png]]
### **9.5. DES Examples and Strength**

*   **S-Box Calculation Examples:**

    ![[Pasted image 20250428234128.png]]
    *   *Input `100011` to S-Box 1:*
        *   Outer bits `11` form binary `11`, which is decimal 3. This selects **Row 3**.
        *   Middle bits `0001` form binary `0001`, which is decimal 1. This selects **Column 1**.
        *   Look up the value in the S1 table (Table 6.3 in your notes) at Row 3, Column 1. The value is 12.
        *   Convert 12 to a 4-bit binary number: `1100`.
        *   So, input `100011` to S1 yields output `1100`.

    *   *Input `000000` to S-Box 8:*
        *   Outer bits `00` form binary `00`, which is decimal 0. This selects **Row 0**.
        *   Middle bits `0000` form binary `0000`, which is decimal 0. This selects **Column 0**.
        *   Look up the value in the S8 table (Table 6.10 in your notes) at Row 0, Column 0. The value is 13.
        *   Convert 13 to a 4-bit binary number: `1101`.
        *   So, input `000000` to S8 yields output `1101`.

*   **Full Encryption/Decryption Examples:**
    *   `[VISUAL: Table 6.15 Trace of Data for Example 6.5 Encryption]` (Plaintext `12...`, Key `AA...`, Ciphertext `C0...`) *(Your note refers to a specific trace table)*
    *   `[VISUAL: Trace Table for Example 6.6 Decryption (implied)]` (Ciphertext `C0...`, Key `AA...`, Plaintext `12...`) *(Your note refers to a specific trace table)*

*   **Strength Analysis:**
    *   **Key Size (56 bits):** This is the **main weakness** and why DES is obsolete. The number of possible keys is $2^{56}$, which is approximately $7.2 \times 10^{16}$ (72 quadrillion). While huge, this number is vulnerable to **brute-force attacks** with modern computing power.
        *   Specialized hardware ("DES crackers") demonstrated this feasibility:
            *   1997: Cracked in months (distributed.net).
            *   1998: Cracked in days (EFF's "Deep Crack" machine).
            *   1999: Cracked in under 24 hours (Deep Crack + distributed.net).
        *   Today, brute-forcing DES is even faster and cheaper, possibly achievable with cloud computing resources or FPGAs/ASICs relatively easily.
    *   **Analytic Attacks:** These attacks try to exploit the internal structure of the algorithm rather than just trying all keys.
        *   **Differential Cryptanalysis:** Discovered publicly by Biham and Shamir around 1990 (though known earlier to IBM/NSA). It analyzes how differences in plaintext inputs propagate through the cipher rounds to affect ciphertext outputs. DES's S-Boxes were specifically designed to be resistant to this. While theoretically breaking DES faster than brute-force (requires $2^{47}$ chosen plaintexts), it's often impractical due to the large data requirement.
        *   **Linear Cryptanalysis:** Discovered by Matsui in 1993. It finds probabilistic linear equations (approximations) relating plaintext, ciphertext, and key bits. It can break DES with $2^{43}$ known plaintexts. While requiring less data than differential cryptanalysis, it's still a massive amount, often making brute-force more practical for attackers.
    *   **Timing Attacks:** Proposed by Kocher in 1996. This is a **side-channel attack** that exploits variations in the *time* it takes for a cryptographic implementation (e.g., on a smartcard or server) to perform encryption/decryption operations. If the time depends subtly on the key or data bits being processed, an attacker making precise timing measurements might deduce key information. This attacks the *implementation*, not the theoretical algorithm, and can be mitigated by careful programming (e.g., ensuring constant-time operations).



### DES Design Weaknesses

These are potential issues related to how DES was constructed, specifically the internal components (S-Boxes and P-Boxes) and certain "unlucky" keys.

*   **S-Box / P-Box Concerns:**
    *   The S-Boxes (Substitution Boxes) and P-Boxes (Permutation Boxes) are the core components that create confusion and diffusion in DES, making the relationship between the key/plaintext and the ciphertext complex.
    *   When DES was designed (largely in secret by IBM and NSA), the exact *reasons* for choosing the specific S-Box values were not made public. This led to suspicion that perhaps there were hidden "backdoors" or weaknesses known only to the designers.
    *   Later, techniques like *Differential Cryptanalysis* were discovered (publicly). It turned out the DES S-Boxes were surprisingly resistant to this specific attack *at the time*, suggesting the designers likely knew about such attacks and designed DES to counter them.
    *   However, the lack of transparency and the possibility of other, perhaps still unknown, analytical attacks related to these specific design choices remain a point of discussion, even if not a practical exploit used today. It's more of a theoretical or historical concern about trusting secret designs.

*   **Problematic Keys:**
    Imagine you have a huge bag with trillions of possible keys for your DES lock. It turns out a very, very small number of these keys have weird properties that make the lock behave strangely or weakly.

    *   **Weak Keys (4 keys):**
        *   **What they are:** These are specific keys where the process of encryption is *identical* to the process of decryption.
        *   **Analogy:** Think of a light switch. Flipping it once turns the light on (encrypts). Flipping it *again* with the same "weak" action turns it off (decrypts) – you're back where you started.
        *   **The Problem:** If you use a weak key `K` to encrypt a message `P` to get ciphertext `C`, encrypting `C` *again* with the *same key* `K` will give you back the original plaintext `P`.
            $$
            E_K(E_K(P)) = P \quad (\text{if K is a weak key})
            $$
        *   This property (`E_K(E_K(P)) = P`) is called an *involution*. For encryption, this is very bad! You want encryption to be hard to reverse without the key, not something that reverses itself on a second application.
        *   There are only **4** such keys out of the vast number of possible DES keys.
        * ![[Pasted image 20250428234635.png]]

    *   **Semi-Weak Keys (6 pairs = 12 keys):**
        *   **What they are:** These keys come in pairs. Let's call a pair (K1, K2). They have a reciprocal relationship.
        *   **Analogy:** Imagine two special keys. Key K1 locks a door. Key K2 doesn't lock it again, instead, it *unlocks* the door that K1 just locked. And vice-versa: if K2 encrypts (locks), K1 decrypts (unlocks).
        *   **The Problem:** If you encrypt a message `P` with key `K1` to get ciphertext `C`, then encrypting `C` with key `K2` will give you back the original plaintext `P`.
            $$
            E_{K2}(E_{K1}(P)) = P \quad (\text{if K1, K2 is a semi-weak key pair})
            $$
            Similarly:
            $$
            E_{K1}(E_{K2}(P)) = P
            $$
        *   This means one key in the pair undoes the encryption performed by the other key in the pair.
        *   There are **6** such pairs, meaning **12** keys in total are semi-weak keys.

    *   **Possible Weak Keys (48 keys):**
        *   **What they are:** DES works in 16 rounds, and for each round, it generates a different "round key" from the main key. Normal keys generate 16 distinct round keys. These "Possible Weak Keys" are keys that generate a much smaller set of round keys – specifically, they only generate **two** distinct round keys, which then repeat throughout the 16 rounds.
        *   **The Problem:** Having fewer unique round keys simplifies the internal workings of the cipher for those specific keys. While not as dramatic as the weak or semi-weak keys, this reduction in internal complexity *might* make the cipher slightly easier to analyze or attack if one of these keys happens to be chosen.
        *   There are **48** such keys.

![[Pasted image 20250428234500.png]]

*   **Probability and Mitigation:**
    *   In total, there are 4 (weak) + 12 (semi-weak) + 48 (possible weak) = **64** problematic keys identified.
    *   DES uses a 56-bit key. The total number of possible keys is $2^{56}$, which is roughly 72 quadrillion (72,057,594,037,927,936).
    *   The chance of randomly picking one of these 64 bad keys is extremely small:
        $$
        \frac{64}{2^{56}} \approx \frac{64}{7.2 \times 10^{16}} \approx 8.8 \times 10^{-16}
        $$
    *   This probability is incredibly low. You're vastly more likely to win the lottery multiple times than to randomly generate one of these keys.
    *   **However:** Because these keys *are* known and *do* cause problems, any well-designed system using DES (or its successor, Triple DES, which can also be affected) should explicitly **check if the chosen key is one of these 64 known weak/semi-weak/possible weak keys**. If it is, the system should reject the key and generate a new one. This is a standard security practice.

### DES Key Complement Property

This is a different kind of weakness, related to symmetry in the algorithm.

*   **What it is:** There's a direct relationship between encrypting a plaintext `P` with a key `K`, and encrypting the *bitwise complement* of the plaintext (`P'`) with the *bitwise complement* of the key (`K'`). The bitwise complement means flipping all the bits (0s become 1s, 1s become 0s).
*   **The Property:** If encrypting plaintext `P` with key `K` results in ciphertext `C`:
    $$
    C = E(K, P)
    $$
    Then, if you take the complement of the key (`K'`) and the complement of the plaintext (`P'`), the resulting ciphertext (`C'`) will be the exact complement of the original ciphertext (`C`):
    $$
    C' = E(K', P')
    $$
*   **The Effect (Why it's a weakness):** This property is useful for attackers performing a *brute-force attack*. A brute-force attack involves trying every possible key until the correct one is found.
    *   Normally, to find a 56-bit DES key, an attacker would need to try up to $2^{56}$ keys in the worst case.
    *   With the complement property, the attacker can be clever. They pick a known plaintext `P` (like a standard header) and the corresponding target ciphertext `C`.
    *   When they test a key `K`, they calculate $E(K, P)$. If it equals `C`, they've found the key.
    *   *But*, using the complement property, they *also* know that $E(K', P')$ will produce $C'$. If they were *also* looking for the key `K'` (which corresponds to encrypting `P'` to get `C'`), testing `K` automatically gives them the result for `K'` as well!
    *   This effectively means that for every key `K` they test, they simultaneously get information about its complement `K'`. This cuts the number of keys they need to actively test in half.
    *   **Result:** The effective key space for a brute-force attack is reduced from $2^{56}$ to $2^{55}$. This halves the time required for a brute-force attack. While halving a huge number still leaves a huge number, it's a significant reduction in the required effort.

### Summary

*   DES has a few specific, known **weak/semi-weak/possible weak keys** (64 in total) that behave badly. The chance of picking one randomly is minuscule, but implementations should check for and reject them.
*   DES has a **Key Complement Property** which means testing one key effectively gives you information about its bitwise complement, reducing the effort for a brute-force key search by half (from $2^{56}$ to $2^{55}$ effort).
*   **Crucially:** The *biggest* weakness of DES today isn't any of these specific flaws, but rather its **short key length (56 bits)**. $2^{56}$ (or even $2^{55}$) computations is well within the reach of modern computing power (and has been for decades), making DES easily breakable by brute force regardless of these other issues. These design/key weaknesses are more like interesting structural flaws compared to the fundamental problem of the key size being too small for modern security needs.


*   `📖 Glossary:`
    *   **DES (Data Encryption Standard):** Obsolete 64-bit symmetric block cipher with 56-bit key.
    *   **Feistel Network:** Cipher structure where data is split, processed in rounds with swaps. Allows using the same algorithm for encryption/decryption.
    *   **Round Key (Subkey):** Key derived from the main key, used in a specific round.
    *   **Key Schedule:** Algorithm generating round keys from the main key.
    *   **IP/FP (Initial/Final Permutation):** Bit rearrangement steps in DES.
    *   **E-Box (Expansion P-Box):** Expands 32 bits to 48 bits in DES function.
    *   **S-Box (Substitution Box):** Non-linear lookup table providing confusion in DES (6-bit input, 4-bit output).
    *   **P-Box (Permutation):** Bit shuffling providing diffusion in DES function.
    *   **Brute-Force Attack:** Trying every possible key.
    *   **Meet-in-the-Middle Attack:** Attack applicable to double encryption schemes like 2DES.
    *   **Differential/Linear Cryptanalysis:** Advanced analytical attacks exploiting cipher properties.
    *   **Weak Key:** A key causing undesirable cryptographic behavior (e.g., encryption = decryption).
    *   **Key Complement Property:** Relationship between encryption with a key and its complement in DES.
    *   **3DES (Triple DES):** Applying DES three times with 2 or 3 keys for stronger security (now also deprecated).

*   `🔑 **Main Takeaway:** DES is a foundational but now insecure 64-bit block cipher with a 56-bit key, based on a Feistel structure. Its small key size makes it vulnerable to brute-force attacks. While its internal design (S-Boxes) resisted early analytic attacks well, it has known weaknesses (weak keys, complement property) and is superseded by AES.`

---

## **10. Advanced Encryption Standard (AES)**

*   **Type:** **Symmetric block cipher**.
*   **History:** Developed by Joan Daemen and Vincent Rijmen (Belgian cryptographers) as "Rijndael". Selected by **NIST** in **2001** after an open competition to replace DES.
*   **Usage:** **Current global standard**, widely used in hardware and software (e.g., WPA2/WPA3 Wi-Fi security, TLS/SSL, file encryption).
*   **Specifications:**
    *   Fixed **block size of 128 bits**.
    *   Variable **key lengths: 128, 192, or 256 bits**.
    *   Number of **Rounds** depends on key length: 10 (128-bit key), 12 (192-bit key), 14 (256-bit key).
    *   Uses **Substitution-Permutation Network** structure (unlike DES's Feistel network).

### **10.1. DES vs. AES Comparison**

| Feature             | **DES**                         | **AES (Rijndael)**                 |
| :------------------ | :------------------------------ | :--------------------------------- |
| **Date Designed**   | 1976                            | 1998-1999 (selected 2001)        |
| **Block Size**      | 64 bits                         | **128 bits**                       |
| **Key Length(s)**   | 56 bits (effective)             | **128, 192, 256 bits**             |
| **Structure**       | **Feistel Network**             | **Substitution-Permutation Network** |
| **Rounds**          | 16                              | 10, 12, or 14                      |
| **Encryption Prims**| Substitution, Permutation       | Substitution, ShiftRows, MixColumns, AddRoundKey |
| **Crypto Prims**    | Confusion, Diffusion            | Confusion, Diffusion             |
| **Design Rationale**| Closed (NSA influence concerns) | **Open** (public design & analysis)|
| **Selection Process**| Secret                          | **Open Competition** (public review)|
| **Source**          | IBM / NSA                       | Independent Belgian cryptographers |
| **Current Status**  | **Insecure, Obsolete**          | **Secure, Widely Deployed Standard** |

*   `📚 Additional Resources:`
    *   NIST FIPS 197: The official AES standard document.
    *   Videos explaining AES rounds (e.g., Computerphile AES explanation).
*   `🚩 Further Research/Clarification Needed:` Explore the specific steps within an AES round (SubBytes, ShiftRows, MixColumns, AddRoundKey).

*   `🔑 **Main Takeaway:** AES is the modern, secure symmetric block cipher standard, replacing DES. It offers larger key sizes (128, 192, 256 bits) and a 128-bit block size, using a different internal structure (Substitution-Permutation Network) developed through an open, public process.`

---

## **11. Public Key (Asymmetric) Cryptography**

*   **Concept:** Uses **two mathematically related keys** per user instead of one shared secret key.
    *   **Public Key:** Shared openly with anyone.
    *   **Private Key:** Kept strictly secret by the owner.
*   **Asymmetry:** The key used for encryption is different from the key used for decryption.
*   **Foundation:** Based on difficult mathematical problems (e.g., factoring large numbers, discrete logarithms).
*   **Role:** **Complements**, rather than replaces, symmetric cryptography.

### **11.1. How Public-Key Cryptography Works**

*   **Confidentiality (Encryption):**
    *   Sender encrypts the message using the **Recipient's Public Key**.
    *   Only the **Recipient** can decrypt the message using their **Private Key**.
![[Pasted image 20250428234829.png]]
*   **Authentication/Digital Signatures:**
    *   Sender "signs" a message (or its hash) by encrypting it with their **own Private Key**.
    *   Anyone can verify the signature by decrypting it with the **Sender's Public Key**. If successful, it proves the message came from the sender and wasn't altered.
    *   `[VISUAL: Diagram showing digital signature: Sender -> Sign (Own Private Key) -> Signature -> Verify (Sender's Public Key) <- Recipient]`

### **11.2. Secret Key vs. Public Key Comparison**


| Feature             | **Secret Key (Symmetric)**     | **Public Key (Asymmetric)**                     |
| :------------------ | :--------------------------- | :---------------------------------------------- |
| **Number of Keys**  | 1 (Shared Secret)            | 2 per user (**Public** & **Private**)           |
| **Key Protection**  | Must keep the shared key secret | Must keep **Private Key** secret; Public key is open |
| **Key Distribution**| **Major challenge** (secure channel needed) | **Easy** (Public keys can be shared openly)   |
| **Speed**           | **Fast**                     | **Very Slow** (100x - 10,000x slower)           |
| **Primary Uses**    | **Bulk data encryption** (Confidentiality) | **Key Exchange, Digital Signatures, Authentication** |
| **Key Size**        | 128-256 bits (AES)           | 2048 bits or more (RSA), 256+ bits (ECC)        |

### **11.3. Why Public-Key Cryptography?**

*   **Solves Key Distribution:** Eliminates the need for pre-shared secret keys via insecure channels. Enables secure communication between parties who have never met.
*   **Enables Digital Signatures:** Provides **authenticity** (proof of origin), **integrity** (proof of no modification), and **non-repudiation** (sender cannot deny sending).
*   **History:** Publicly introduced by **Whitfield Diffie & Martin Hellman** (1976), though known earlier in classified communities (e.g., GCHQ in the UK). A **major cryptographic advancement**.

### **11.4. Public-Key Characteristics**

*   **Security:** Computationally **infeasible** to derive the Private Key from the Public Key.
*   **Efficiency:** Encryption and decryption are (relatively) **easy** *if* you have the correct key.
*   **Reversibility (sometimes):** \( D_{Private}(E_{Public}(M)) = M \) and \( D_{Public}(E_{Private}(M)) = M \). This property enables both confidentiality and digital signatures with algorithms like RSA. 

### **11.5. Public-Key Applications**

1.  **Encryption/Decryption (Confidentiality):** Encrypt message with recipient's public key.
2.  **Digital Signatures (Authentication, Integrity, Non-repudiation):** Sign hash with sender's private key.
3.  **Key Exchange:** Securely establish a shared secret key (typically for *symmetric* encryption) over an insecure channel. (e.g., Diffie-Hellman key exchange, or encrypting a symmetric key with the recipient's public key).

*   `[Brief Summary]:` Often, asymmetric crypto is used to securely exchange a *symmetric* key (due to speed), and then the faster symmetric crypto is used for the bulk data encryption (Hybrid Approach).

### **11.6. Public Key for Secret Key Exchange (Hybrid Cryptosystem)**

*   Steps
    1.  Alice wants to send an encrypted message to Bob.
    2.  Alice generates a random **session key** (for symmetric encryption, e.g., AES).
    3.  Alice encrypts the session key using **Bob's Public Key**.
    4.  Alice encrypts her actual message using the **session key** (symmetric encryption).
    5.  Alice sends the encrypted session key and the encrypted message to Bob.
    6.  Bob decrypts the encrypted session key using his **Private Key**.
    7.  Bob uses the recovered session key to decrypt the actual message.

*   `🌍 Real-World Example:` TLS/SSL (used in HTTPS) uses asymmetric cryptography during the initial handshake to authenticate the server and securely exchange session keys, then uses symmetric encryption for the actual web traffic.

*   `📖 Glossary:`
    *   **Public Key Cryptography (Asymmetric):** Uses public/private key pairs.
    *   **Public Key:** Shared key for encryption or signature verification.
    *   **Private Key:** Secret key for decryption or signing.
    *   **Digital Signature:** Encrypted hash providing authenticity, integrity, non-repudiation.
    *   **Key Exchange:** Process of establishing a shared secret key.
    *   **Diffie-Hellman:** A key exchange algorithm (not for encryption/signatures itself).
    *   **RSA:** Common algorithm for both encryption and digital signatures.
    *   **ECC (Elliptic Curve Cryptography):** More efficient alternative to RSA, providing same security with smaller key sizes.
    *   **Hybrid Cryptosystem:** Combines asymmetric crypto (for key exchange/signatures) with symmetric crypto (for bulk data).

*   `🔑 **Main Takeaway:** Public key (asymmetric) cryptography uses public/private key pairs to solve key distribution and enable digital signatures, complementing faster symmetric encryption, often used together in hybrid systems.`

---

## **12. Ensuring Data Integrity and Authenticity**

### **12.1. Error Detecting Codes**
Used to detect accidental modifications during transmission or storage.

*   **Simple Codes:**
    *   **Parity Checks:** Detect single-bit errors. Simple, limited.
    *   **Cyclic Redundancy Checks (CRC):** Detect common burst errors caused by noise. Used in networking (Ethernet) and storage. Not cryptographically secure.
*   **Cryptographic Integrity Codes:** Designed to detect *intentional* modifications.
    *   **One-Way Hash Functions (Cryptographic Hash Functions):** See below.
    *   **Cryptographic Checksums / MACs:** Hash functions combined with a secret key.
    *   **Digital Signatures:** Asymmetric cryptography applied to hashes.

### **12.2. (Cryptographic) Hash Functions**

*   **Purpose:** Create a fixed-size "fingerprint" or **message digest** of arbitrary-size input data.
*   **Properties:**
    *   **One-way:** Computationally infeasible to find the input data given only the hash output.
    *   **Deterministic:** Same input always produces the same output hash.
    *   **Collision Resistant:** Computationally infeasible to find two different inputs that produce the same hash output.
    *   **Avalanche Effect:** Small change in input results in a large, unpredictable change in the output hash.
*   **Use:** Verify data integrity. If the hash of received data matches the original hash, the data hasn't been altered.
*   **Examples:** **SHA-256, SHA-3**, MD5 (broken), SHA-1 (weakened).

### **12.3. Digital Signatures (Revisited)**

*   **Definition:** A cryptographic mechanism used to verify the **authenticity, integrity, and non-repudiation** of digital data.
*   **Process:**
    1.  **Sender:** Computes the **hash (message digest)** of the document/message.
    2.  **Sender:** Encrypts the hash using their **Private Key**. This encrypted hash is the **digital signature**.
    3.  **Sender:** Sends the original document + the digital signature.
    4.  **Receiver:** Decrypts the signature using the **Sender's Public Key** to recover the original hash (Hash A).
    5.  **Receiver:** Computes the hash of the received document independently (Hash B).
    6.  **Verification:** If **Hash A == Hash B**, the signature is valid (authentic sender, data unmodified).
![[Pasted image 20250428235238.png]]

*   `🔗 Connections:` Digital signatures combine hash functions (for integrity) with asymmetric cryptography (for authenticity and non-repudiation).

*   `📖 Glossary:`
    *   **Error Detecting Code:** Algorithm to detect accidental data errors.
    *   **Parity Check:** Simple error detection for single bit errors.
    *   **CRC (Cyclic Redundancy Check):** Common error detection for burst errors.
    *   **Hash Function (Cryptographic):** Creates a fixed-size, one-way digest of data for integrity checks.
    *   **Message Digest:** The output of a hash function.
    *   **Collision Resistance:** Property of hash function making it hard to find two inputs with the same hash.
    *   **Digital Signature:** Encrypted hash using sender's private key, ensuring authenticity, integrity, non-repudiation.

*   `🔑 **Main Takeaway:** Cryptographic hash functions create unique data fingerprints for integrity checks. Digital signatures combine hashes with asymmetric encryption to prove who sent the data and that it wasn't tampered with.`

---

## **13. Certificates and Trust Infrastructure**

### **13.1. Certificates: Binding Identity to Keys**

*   **Problem:** How do you trust that a public key actually belongs to the person/entity claimed?
*   **Solution:** **Digital Certificate**.
*   **Definition:** A **digital certificate** is an electronic document that uses a digital signature to bind a **Public Key** with an **Identity** (information such as name, organization, email address).
*   **Issuer:** Certificates are issued and digitally signed by a trusted third party called a **Certificate Authority (CA)**.


### **13.2. Certificate Authority (CA)**

*   **Role:** A trusted entity that **verifies the identity** of individuals or organizations before issuing a certificate.
*   **Trust Anchor:** Users' systems (browsers, OS) typically have a pre-installed list of trusted **Root CAs**.

### **13.3. Certificate Signing and Hierarchy (Chain of Trust)**

*   CAs can be organized hierarchically. A Root CA can issue certificates for Intermediate CAs, which can then issue certificates for end-entities (like websites or users).
*   **Verification:** To verify a certificate, the system checks the signature of the issuing CA. If that CA is not a Root CA, it checks the certificate of the *issuing* CA, following the chain up until a trusted Root CA is reached.
*   **Example:**
    *   **Edward (Root CA)** signs **Diana's (Intermediate CA) certificate**.
    *   **Diana** signs **Delwyn's (End-entity) certificate**.
    *   Delwyn's certificate is presented. To trust it, the system verifies Diana's signature using Diana's public key (found in *her* certificate). Then, it verifies Diana's certificate using Edward's public key (trusted Root CA).

![[Pasted image 20250428235333.png|500]]

*   `🌍 Real-World Example:` When you visit an HTTPS website, your browser verifies the website's SSL/TLS certificate by checking the signature chain back to a trusted Root CA stored in your browser/OS.

*   `📖 Glossary:`
    *   **Digital Certificate:** Document binding a public key to an identity, signed by a CA.
    *   **Certificate Authority (CA):** Trusted entity that issues and signs certificates.
    *   **Root CA:** Top-level CA trusted implicitly by systems.
    *   **Intermediate CA:** CA whose certificate is signed by another CA.
    *   **Chain of Trust:** Hierarchical relationship of certificates back to a Root CA.
    *   **SSL/TLS Certificate:** Certificate used to secure website communication (HTTPS).

*   `🔑 **Main Takeaway:** Digital certificates, issued by trusted Certificate Authorities (CAs), solve the problem of trusting public keys by securely binding them to verified identities, forming a chain of trust.`

---

## **14. Web Security Example: HTTPS and Browser Tracking**

*   **HTTPS (HTTP Secure):** Uses SSL/TLS to encrypt communication between browser and web server.
    *   Provides **Confidentiality** and **Integrity** for web traffic.
    *   Uses certificates for server **Authentication**.
    *   **Limitation:** While encrypting *content*, HTTPS **does not inherently prevent tracking** based on *metadata* or browser characteristics.
*   **Browser Fingerprinting:** Websites can identify and track users (even across sessions) by collecting a unique combination of browser/system attributes (e.g., installed fonts, screen resolution, browser plugins, OS version, time zone). This can occur even over HTTPS.
*   **Mitigation:**
    *   Tools like the **"HTTPS Everywhere"** browser extension help enforce HTTPS connections, reducing opportunities for some passive network eavesdropping but not directly stopping fingerprinting.
    *   Other techniques (VPNs, Tor Browser, privacy-focused browsers, disabling scripts) can help reduce fingerprinting.
*   `🚩 Further Research/Clarification Needed:` Explore specific browser fingerprinting techniques and more advanced countermeasures (e.g., Canvas Fingerprinting, AudioContext Fingerprinting).

---

## **15. Summary of Cryptographic Tools**


| Tool                             | Primary Uses                                                    | Type         |
| :------------------------------- | :-------------------------------------------------------------- | :----------- |
| **Secret key encryption**        | Confidentiality, Integrity (of bulk data)                       | Symmetric    |
| **Public key encryption**        | Key exchange, Digital signatures (Authentication, Non-repudiation) | Asymmetric   |
| **Error detection codes (CRC)**  | Detect *accidental* changes                                     | N/A          |
| **Hash functions (Crypto)**      | Integrity checking (detect *intentional* changes)              | N/A          |
| **Message Auth. Codes (MACs)**   | Integrity + Authentication (using shared secret key)            | Symmetric    |
| **Digital signatures**           | Authentication, Integrity, Non-repudiation (using private key) | Asymmetric   |
| **Digital certificates**         | Bind identity to public key, Enable trust                       | Asymmetric   |
| *(Error correction codes)*      | *Detect and repair errors*                                      | *N/A*        |

---

## **16. Overall Module Summary**

*   Information security protects valuable **Assets** (Hardware, Software, Data) by ensuring **Confidentiality, Integrity, and Availability (CIA Triad)**.
*   Security faces **Threats** (attackers, errors, nature) exploiting **Vulnerabilities** (weaknesses); **Controls** are implemented to mitigate risk.
*   **Encryption** is a key control for Confidentiality, using **Symmetric** (fast, one key) or **Asymmetric** (slower, public/private keys) algorithms.
*   **DES** is obsolete; **AES** is the modern symmetric standard.
*   **Asymmetric (Public Key) Cryptography** enables secure **Key Exchange** and **Digital Signatures**.
*   **Hash functions** provide **Integrity** checks.
*   **Digital Signatures** provide **Authenticity, Integrity, and Non-repudiation**.
*   **Certificates** issued by **CAs** bind identities to public keys, establishing **Trust**.
*   Security requires **Layered Defenses (Defense in Depth)** and is an **ongoing process**.

---

## **🧠 Mind Map / Concept Diagram Structure**

*   **Central Topic:** Information Security
    *   **Branch: Assets**
        *   Hardware
        *   Software
        *   Data
        *   Valuation (Replaceable/Unique)
    *   **Branch: Core Goals (CIA Triad)**
        *   Confidentiality (Techniques: Encryption, Access Control)
        *   Integrity (Techniques: Hashing, Signatures, MACs)
        *   Availability (Techniques: Redundancy, Backups)
    *   **Branch: Threats & Vulnerabilities**
        *   Threat Sources (Natural, Human-Error, Human-Malicious)
        *   Vulnerability (Weakness)
        *   Attack (Exploit)
        *   Harm Types (Intercept, Interrupt, Modify, Fabricate)
        *   Attackers (Types, APTs)
    *   **Branch: Controls & Defenses**
        *   Definition (Countermeasure)
        *   Categorization (Technical, Admin, Physical)
        *   Functional Types (Prevent, Detect, Deter, Respond, etc.)
        *   MOM (Method, Opportunity, Motive)
        *   Defense Strategies (Prevent, Deter, Deflect, etc.)
        *   Defense in Depth
    *   **Branch: Encryption**
        *   Purpose (Confidentiality)
        *   Terminology (Plaintext, Ciphertext, Key)
        *   Symmetric (DES, 3DES, AES)
            *   Stream vs. Block Ciphers
            *   DES Details (Structure, Feistel, Rounds, f-function, S-Boxes, Weaknesses)
            *   AES (Standard, vs DES)
        *   Asymmetric (RSA, ECC)
            *   Public/Private Keys
            *   Applications (Key Exchange, Signatures)
            *   Hybrid Systems
        *   Principles (Diffusion, Confusion)
    *   **Branch: Integrity & Authenticity**
        *   Hash Functions (Properties, Examples)
        *   Digital Signatures (Process, Benefits)
        *   MACs
    *   **Branch: Trust Infrastructure**
        *   Digital Certificates (Purpose, Components)
        *   Certificate Authority (CA)
        *   Chain of Trust / Hierarchy

---

# **Made by Yashank**