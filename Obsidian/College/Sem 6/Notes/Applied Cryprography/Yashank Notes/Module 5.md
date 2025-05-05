
# Modern Cryptography

## Module Outline

This module explores advanced and emerging areas within cryptography, moving beyond traditional symmetric and asymmetric schemes. Topics include:

*   **Quantum Cryptography:** Leveraging quantum mechanics for cryptographic tasks, primarily key distribution.
*   **Homomorphic Encryption:** Performing computations directly on encrypted data without decryption.
*   **Secure Multi-Party Computation (MPC):** Enabling multiple parties to jointly compute a function over their private inputs without revealing those inputs.
*   **Zero-Knowledge Proofs (ZKP):** Proving knowledge or the truth of a statement without revealing the underlying information.
*   **Cryptographic Obfuscation:** Making code or data difficult to understand or reverse-engineer.

---

## Quantum Cryptography

### Definition and Core Idea

-   **Quantum Cryptography** is the science of using **quantum mechanical properties** to perform cryptographic tasks.
-   The most prominent application is **Quantum Key Distribution (QKD)**, which allows secure key exchange by leveraging quantum phenomena.
-   It often uses individual particles of light (**photons**) transmitted over fiber optic wire to represent binary bits (0s and 1s).
-   The security fundamentally relies on the principles of quantum mechanics, not just computational difficulty like classical cryptography.

### Key Quantum Mechanical Principles

Quantum cryptography exploits several counter-intuitive properties of quantum systems:

1.  **Superposition & Uncertainty:** Particles (like photons) can exist in multiple states or places simultaneously (**superposition**) until measured. Their properties (like polarization state) are inherently uncertain before measurement (**Heisenberg's Uncertainty Principle**). One cannot assume or precisely know the state before measuring.
2.  **Observer Effect:** The act of measuring a quantum property inevitably **changes or disturbs** that property. It's impossible to observe the state of a quantum system without altering it.
3.  **No-Cloning Theorem:** It is impossible to create an identical copy of an arbitrary unknown quantum state. While some properties might be cloned, the *entire* state cannot be perfectly duplicated.
4.  **Wave Function Collapse:** Measurement forces a particle out of superposition into a single definite state.
5.  **Randomness:** Some quantum events, like the polarization state chosen when generating a photon in QKD, can be truly random.

![[Pasted image 20250506023949.png]]This image illustrates different polarization states (Vertical, Diagonal, Horizontal, Diagonal) potentially representing binary bits (e.g., Vertical=1, Horizontal=0, Right Diagonal=1, Left Diagonal=0).

### Implications for Security

-   **Eavesdropping Detection:** Because measuring a quantum state (like a photon's polarization) disturbs it (Observer Effect), any attempt by an eavesdropper (Eve) to intercept and read the quantum information transmitted between the sender (Alice) and receiver (Bob) will inevitably introduce detectable errors.
-   **Impossibility of Copying:** The No-Cloning Theorem prevents Eve from simply copying the quantum state (e.g., the photons carrying the key bits) and measuring her copy while forwarding the original undisturbed.
-   **Result:** Data encoded in a quantum state cannot be copied or viewed secretly without altering the state, thereby alerting the legitimate sender and receiver. This forms the basis for secure key distribution in QKD.

### Quantum Key Distribution (QKD)

QKD is the most developed application, aiming to establish a shared secret key between two parties (Alice and Bob) with security guaranteed by quantum mechanics. The BB84 protocol is a common example.

#### How QKD Works (BB84 Analogy)

1.  **Alice Prepares Photons:** Alice wants to send a secret key (a sequence of random bits) to Bob. For each bit, she randomly chooses one of two *bases* (encoding schemes) to use:
    *   Rectilinear Basis (+): Encodes 0 as Horizontal polarization (|), 1 as Vertical polarization (—).
    *   Diagonal Basis (x): Encodes 0 as 45° Left polarization (\), 1 as 45° Right polarization (/).
    She sends a stream of single photons, each prepared in a state corresponding to her chosen bit and basis, through an optical fiber.
2.  **Bob Measures Photons:** Bob receives the photons one by one. For each photon, he *doesn't know* which basis Alice used. He randomly chooses a basis (Rectilinear + or Diagonal x) to measure the photon's polarization using a **beam splitter** and detectors.
    *   If Bob chooses the *same* basis Alice used, he gets the correct bit value with certainty.
    *   If Bob chooses the *different* basis, the quantum measurement forces the photon into one of the states of *his* basis, yielding a random result (50% chance 0, 50% chance 1). His result is uncorrelated with Alice's original bit.
3.  **Basis Reconciliation (Public Discussion):** After Bob has measured all photons, Alice and Bob communicate over a *classical* (non-quantum, but authenticated) channel. They **compare the sequence of bases** they used for each photon. They do **not** reveal the measurement results (the bits).
4.  **Sifting the Key:** They **discard** all the measurement results where they used *different* bases. The remaining sequence of bits, where they happened to use the same basis, forms the **sifted key**. This key should be identical for both Alice and Bob (in the absence of errors or eavesdropping).
5.  **Error Checking / Eavesdropping Detection:** Alice and Bob sacrifice a random subset of their sifted key bits and compare them publicly. If the error rate is higher than expected (due to channel noise or Eve's intervention), they conclude an eavesdropper was present and **discard the entire key**, starting the process over.
6.  **Privacy Amplification:** If the error rate is low, they use classical error correction and privacy amplification techniques on the remaining sifted key bits to remove any partial information Eve might have gained and distill a shorter, secure final key.

<!-- Instruct user to paste diagrams from pages 12, 13, 14, 15, 16, 17, 18, 19, 20 here -->
![[Pasted image 20250506024009.png]]showing Rectilinear (Horizontal/Vertical) and Diagonal schemes.

![[Pasted image 20250506024020.png]]illustrating measurement outcomes when bases match or mismatch.

![[Pasted image 20250506024036.png]]

![[Pasted image 20250506024056.png]]Ahyan sends bits/bases, Hibba measures with random bases, they compare bases.

![[Pasted image 20250506024113.png]]where Alice tells Bob the bases, not the bits.

![[Pasted image 20250506024134.png]]the Eavesdropper scenario showing Eve guessing a basis, potentially different from Alice and Bob.

![[Pasted image 20250506024147.png]]the error introduction scenario showing Eve's wrong guess potentially causing Bob to get the wrong bit even if Bob's basis matches Alice's later.

![[Pasted image 20250506024219.png]] "Quantum Cryptography Explained" diagram showing Alice's polarizers, Bob's beam splitters, and the sifting process.

![[Pasted image 20250506024238.png]] "How it works?" diagram showing the full BB84 process flow with photon states, random choices, and public discussion.

#### Eavesdropping Scenario

-   If Eve intercepts a photon sent by Alice, she must measure it to learn its state (the bit).
-   Like Bob, Eve doesn't know Alice's basis choice, so Eve must guess a basis for her measurement.
-   Measuring disturbs the photon's state (**Observer Effect**).
-   Eve then must re-send a photon to Bob (she can't clone the original - **No-Cloning Theorem**). She sends a photon based on *her* measurement result and *her* basis choice.
-   There's a high probability (50% if Alice and Eve chose different bases) that the photon Eve sends to Bob is now in a different state than the one Alice originally sent.
-   When Alice and Bob compare bases and later check for errors in their sifted key, Eve's intervention will introduce a detectable error rate (around 25% on average for BB84), alerting them to her presence. They discard the compromised key.

### Advantages of Quantum Cryptography

-   **Provable Security (for QKD):** Security relies on fundamental laws of physics (quantum mechanics), not on assumptions about computational difficulty (like factoring or discrete logs).
-   **Eavesdropping Detection:** Built-in mechanism to detect eavesdropping attempts.
-   **Future-Proof (against quantum computers):** QKD provides secure key exchange even in the era of quantum computers, which threaten classical public-key algorithms.
-   **Potential for Long-Term Encryption:** Keys established via QKD can be used with theoretically secure methods like the One-Time Pad (OTP).
-   Provides secure communication channels.
-   Protects sensitive data (medical, government, military).
-   Can operate over noisy channels (with error correction).

### Limitations of Quantum Cryptography

-   **Range:** QKD is typically limited by photon loss and decoherence in optical fibers, often to a few hundred kilometers (though research, repeaters, and satellite links aim to extend this).
-   **Expense & Infrastructure:** Requires specialized hardware (single-photon sources/detectors, polarizers, specific fibers, potentially repeaters) which is currently expensive and often requires dedicated infrastructure.
-   **Point-to-Point:** Basic QKD establishes keys between two specific points. Creating secure networks (Number of destinations) is more complex (requiring trusted nodes or quantum repeaters).
-   **Error Rates:** Photons can naturally change polarization or get lost, introducing errors unrelated to eavesdropping, requiring robust error correction.
-   **Denial of Service:** An attacker can simply disrupt the quantum channel (e.g., by shining light into it) to prevent key exchange, though they cannot learn the key.

### Implementations and Status

-   QKD systems are commercially available from companies like ID Quantique, Toshiba, MagiQ Technologies, etc.
-   Various research networks and government projects exist (e.g., DARPA Quantum Network, Quantum Xchange in US, networks in Europe, China).
-   While demonstrated to work, **not yet widely deployed** due to limitations (cost, range, infrastructure needs). Primarily used in niche high-security applications.

### Comparison: Traditional vs. Quantum Cryptography

| Feature              | Traditional Cryptography                      | Quantum Cryptography (mainly QKD)              |
| :------------------- | :-------------------------------------------- | :--------------------------------------------- |
| **Security Basis**   | Computational Hardness (Math problems)        | Laws of Physics (Quantum Mechanics)            |
| **Key Distribution** | Symmetric (Needs secure channel) or Asymmetric (RSA, DHKE - vulnerable to quantum computers) | QKD provides secure key exchange, resistant to quantum computers |
| **Eavesdropping**    | Undetectable (passive listening)              | Detectable (causes disturbances/errors)      |
| **Data Encryption**  | Algorithms like AES, RSA encrypt data        | Primarily focuses on **Key Distribution**. Data usually encrypted classically using QKD-derived key. |
| **Range**            | Unlimited (relies on classical comms)         | Limited by physical constraints (fiber loss)   |
| **Infrastructure**   | Uses existing networks                        | Often requires dedicated quantum channels      |
| **Maturity**         | Mature, widely deployed                       | Emerging, limited deployment                 |
| **Cost**             | Relatively low                                | Currently high                               |

### Other Quantum Cryptography Applications

Besides QKD, research explores other quantum cryptographic protocols:

-   **Mistrustful Quantum Cryptography:** Protocols where parties don't trust each other but use quantum mechanics to ensure fairness or prevent cheating (e.g., both sides get the result or neither does).
-   **Quantum Coin Flipping:** Allows two distrustful parties to remotely agree on a random coin flip outcome.
-   **Quantum Commitment:** Allows Alice to commit to a value (like a bit) that she cannot change later, but Bob cannot learn the value until Alice reveals it.
-   **Bounded/Noisy Quantum Storage Model:** Security assumptions based on limitations of an adversary's quantum storage capabilities.
-   **Position-Based Quantum Cryptography:** Using geographical location as a credential, leveraging quantum limits on information transfer.
-   **Device-Independent Quantum Cryptography:** Protocols whose security doesn't rely on trusting the internal workings of the quantum devices used.

### Q&A Summary

-   **Used Today?** QKD works but is **not widely used** due to technological limits (range, cost).
-   **Can it be hacked?** The *protocol* (like BB84) is theoretically secure against eavesdropping on the *quantum channel*. Attacks typically target **implementation vulnerabilities** (e.g., imperfections in photon sources/detectors, side-channel attacks on hardware) or the classical communication channel used for basis reconciliation. Advanced device-independent protocols aim to mitigate hardware attacks.

### Section Summary: Quantum Cryptography

-   Uses quantum mechanics (superposition, observer effect, no-cloning) for crypto tasks.
-   **QKD** is the main application: Secure key exchange by sending polarized photons. Eavesdropping introduces detectable errors.
-   **Advantages:** Security based on physics, eavesdropping detection, quantum-computer resistant key exchange.
-   **Limitations:** Range, cost, infrastructure, point-to-point nature.
-   Not a replacement for *all* classical crypto, but a secure method for key distribution.

---

## Homomorphic Encryption (HE)

### Concept

-   **Homomorphic Encryption (HE)** allows computations (like addition or multiplication) to be performed **directly on encrypted data** (ciphertexts) without needing to decrypt it first.
-   **Result:** The result of the computation remains encrypted. When decrypted (by the owner of the secret key), it matches the result of performing the same operations on the original plaintext data.
-   **Goal:** Enables processing of sensitive data by untrusted environments (like third-party cloud services) while maintaining data confidentiality.

### Example: Cloud-Based Health Data Analysis

***Scenario:** A hospital wants a cloud service to calculate the average blood pressure of its patients but cannot share raw patient data due to privacy regulations (HIPAA, GDPR).*

<!-- Instruct user to paste the solution steps from pages 33, 35, 36, 37 here -->
***Solution using HE:**
1.  **Encryption (Hospital):** Hospital encrypts patient records (including ID, Age, Blood Pressure (BP), Heart Rate (HR)) using an HE scheme before uploading.
    *   Record 1: `E(ID1), E(34), E(120), E(80)`
    *   Record 2: `E(ID2), E(45), E(130), E(85)`
    ![[Pasted image 20250506024325.png]]
    
2.  **Computation (Cloud):** Hospital requests the average BP. Cloud provider receives encrypted BP values `E(120)` and `E(130)`. Using the homomorphic properties of the scheme (assuming it supports addition and division by a constant):
    *   Cloud computes `E(sum) = E(120) '+' E(130) = E(120 + 130) = E(250)` (where '+' denotes the homomorphic addition operation on ciphertexts).
    *   Cloud computes `E(average) = E(250) '/' 2 = E(250 / 2) = E(125)` (where '/' denotes homomorphic division by a public constant).
    *   **Crucially, the cloud performs these operations *without* knowing the actual BP values (120, 130, 250, 125).** It only manipulates ciphertexts.

3.  **Return Encrypted Result (Cloud -> Hospital):** Cloud sends `E(125)` back to the hospital.
4.  **Decryption (Hospital):** Hospital uses its private decryption key to decrypt the result: `D(E(125)) = 125`. The hospital obtains the correct average BP without ever exposing raw patient data to the cloud.


### Why HE Works

-   **Mathematical Operations Preserved:** HE schemes are designed such that specific operations (like + or ×) on ciphertexts correspond directly to the same operations on the underlying plaintexts. $Op_{ciphertext}(E(a), E(b)) = E(Op_{plaintext}(a, b))$.
-   **Field Meanings Hidden:** Encryption obscures the actual values and context. The cloud sees only opaque encrypted data and cannot distinguish "Age" from "Blood Pressure". It just follows instructions on which encrypted columns to compute.
-   **Zero Knowledge (for Processor):** Unlike traditional methods requiring decryption before computation, HE allows computation while the processor remains completely blind to the underlying data.

### Definition and Properties

-   **Homomorphism:** Term comes from algebra, signifying a structure-preserving map between two algebraic structures. In HE, encryption/decryption functions act like homomorphisms between plaintext and ciphertext spaces regarding certain operations.
-   **Data Structure:** Encrypted data often retains a similar structure, allowing operations.
-   **Equivalent Results:** Performing the same operation on plaintexts or ciphertexts yields equivalent results after decryption.

### Types of Homomorphic Encryption

HE schemes vary in the types and number of operations they support on ciphertexts:

1.  **Partially Homomorphic Encryption (PHE):** Supports *either* addition *or* multiplication indefinitely, but not both.
    -   **Additive HE:** Allows $E(a) '+' E(b) = E(a+b)$. Example: Paillier cryptosystem.
    -   **Multiplicative HE:** Allows $E(a) '*' E(b) = E(a \times b)$. Example: Unpadded RSA ($E(p1) \times E(p2) = (p1^e)(p2^e) = (p1 \times p2)^e = E(p1 \times p2) \pmod n$).
2.  **Somewhat Homomorphic Encryption (SHE):** Supports a *limited* number of *both* addition and multiplication operations. The noise introduced by operations grows, eventually making decryption impossible after too many computations.
3.  **Leveled Fully Homomorphic Encryption:** Supports arbitrary computations (circuits) up to a *predefined depth*. Parameters are set based on the required circuit depth.
4.  **Fully Homomorphic Encryption (FHE):** The "holy grail". Supports an *unlimited* number of *both* additions and multiplications. Requires techniques like "bootstrapping" to manage noise accumulation, which adds significant overhead.

### Standardization and Implementations

-   **Standardization:** The Homomorphic Encryption Standardization Consortium (HE.org), formed by IBM, Microsoft, Intel, NIST etc., works on community standards. [homomorphicencryption.org](https://homomorphicencryption.org/)
-   **Libraries:**
    -   **SEAL (Simple Encrypted Arithmetic Library):** Developed by Microsoft. Supports FHE.
    -   **HElib:** Developed by IBM. Supports FHE (first library released in 2016).
    -   **OpenFHE:** Leading open-source FHE library, integrating contributions including Google's FHE Transpiler (built using XLS SDK).
    -   **Private Join and Compute (Google):** Open-source tool using cryptographic techniques (possibly including HE or related ideas like Private Set Intersection) for analyzing data without revealing it.

### Advantages

-   **Enhanced Data Security & Privacy:** Allows processing sensitive data in untrusted environments (cloud) without exposure.
-   **Enables New Applications:** Facilitates privacy-preserving data analysis, machine learning on encrypted data, secure cloud services.
-   **Use Cases:** Cloud workload protection, privacy-preserving data aggregation/analytics (e.g., medical research, financial services), secure information supply chains, secure automation/orchestration.

### Limitations

-   **Performance (Major Hurdle):** HE, especially FHE, is **extremely slow**. Computations on encrypted data can be many orders of magnitude (trillions of times, as mentioned for early HElib) slower than on plaintext. This currently limits practical large-scale deployment. Performance is improving with new schemes and hardware acceleration research.
-   **Ciphertext Expansion:** Encrypted data is typically much larger than the original plaintext.
-   **Complexity:** Schemes are mathematically complex and harder to implement correctly than traditional encryption.
-   **Limited Functionality (for PHE/SHE):** Non-FHE schemes support only limited types or numbers of operations.
-   **Limited Multi-User Support:** Managing keys and computations involving multiple data owners can be complex.

### Q&A Summary

-   **Can HE be broken/hacked?** The *encryption itself* (based on hard math problems like Learning With Errors - LWE) is generally considered secure, potentially even against quantum computers. Attacks might target the *process* (implementation flaws, side channels, protocol attacks) rather than the core encryption.
-   **Google's Use:** Google is involved in FHE research and development, contributing to libraries like OpenFHE and developing tools like Private Join and Compute.

### Section Summary: Homomorphic Encryption

-   Allows computations (e.g., +, x) directly on encrypted data.
-   Result remains encrypted; decrypting gives the result of computation on plaintexts.
-   Enables privacy-preserving outsourcing (e.g., cloud computing).
-   **Types:** PHE (one operation type), SHE (limited mixed ops), FHE (unlimited mixed ops).
-   **Major Limitation:** Extremely slow performance, especially for FHE.
-   Active area of research with libraries like SEAL, HElib, OpenFHE.

---

## Secure Multi-Party Computation (MPC / SMPC)

### Concept

-   **Secure Multi-Party Computation (MPC)** is a cryptographic technique enabling multiple parties, who do not necessarily trust each other, to **jointly compute a function** over their **private inputs** in such a way that **no party learns anything about the other parties' inputs beyond what can be inferred from the final output**.
-   **Goal:** Allow collaboration and data analysis without centralizing sensitive data or revealing individual inputs.

### Examples

1.  **Millionaires' Problem (Yao's Problem):** Two (or more) millionaires want to determine who is richer without revealing their actual net worths. MPC protocols allow them to learn the comparison result (e.g., "Alice is richer" or "They are equal") without learning the specific amounts.
    *   *(Note: The 3-millionaire example on page 57 using a calculator is a simplified illustration but flawed; Jane learns information, and others can lie. Real MPC protocols are more complex and secure against such issues).*
2.  **Average Salary Calculation:** A group of employees wants to compute their average salary without revealing individual salaries.
    *   **Protocol Idea (page 60):** Each employee $i$ holds salary $s_i$. Employee 1 picks a large random number $R$.
        -   Emp 1 computes $v_1 = s_1 + R$. Passes $v_1$ to Emp 2.
        -   Emp 2 computes $v_2 = v_1 + s_2$. Passes $v_2$ to Emp 3.
        -   ...
        -   Emp N computes $v_N = v_{N-1} + s_N$. Passes $v_N$ back to Emp 1.
        -   Emp 1 computes final sum $S = v_N - R = (s_1 + ... + s_N + R) - R = \sum s_i$.
        -   Emp 1 computes Average = $S / N$.
    *   **Privacy:** The large random $R$ hides $s_1$. Intermediate sums hide individual salaries from others (unless parties collude). The final sum $S$ doesn't reveal individual $s_i$ to Emp 1 if $N \ge 3$.
    *   **Vulnerability:** Collusion (e.g., Emp 2 and Emp 4 colluding can find Emp 3's salary by $v_3 - v_2 = s_3$). Robust MPC protocols address collusion.
3.  **Collaborative Fraud Detection (Banks):** Multiple banks jointly analyze transaction data to detect cross-bank fraud patterns (e.g., money laundering) without sharing customer data, using MPC to compute risk scores or flag suspicious activity based on combined (encrypted/shared) data. (Pages 62-64)
4.  **Medical Research:** Hospitals collaborate on studies (e.g., treatment efficacy) using encrypted patient data via MPC to get aggregate results without revealing individual patient records. (Page 65)
5.  **Private Market Analysis:** Competitors analyze overlapping trends (customer behavior, supply chain) using MPC without revealing sensitive internal business data. (Page 66)
6.  **Private Voting/Bidding:** Conduct elections or sealed-bid auctions where individual votes/bids remain private, but the final tally/winner is correctly and verifiably computed. (Page 67)
7.  **Genomic Data Collaboration:** Perform joint statistical analysis on sensitive genomic data across institutions without revealing individual genomes. (Page 68)
8.  **Cross-Border Tax Fraud Detection:** Governments compare encrypted income/asset data using MPC to find evasion patterns without violating national secrecy laws. (Page 69)

### Core Properties

Secure MPC protocols aim to guarantee:

1.  **Input Privacy:** No party learns anything about other parties' private inputs beyond what is revealed by the function output itself.
2.  **Correctness:** The output of the computation is correct, even if some parties are malicious (adversarial) and try to disrupt the protocol. Malicious parties should not be able to force an incorrect output for honest parties.

### MPC Techniques

Various techniques are used to build MPC protocols, often depending on assumptions about the majority of parties (honest vs. dishonest) and the adversary model (semi-honest vs. malicious).

1.  **Shamir Secret Sharing (SSS):** A **threshold secret sharing** scheme. A secret $s$ is split into $n$ shares given to $n$ parties. Any $t+1$ (where $t$ is the threshold) parties can combine their shares to reconstruct $s$, but $t$ or fewer parties learn nothing about $s$. Based on polynomial interpolation. Often used for input sharing in MPC protocols, especially those assuming an **honest majority** (less than half the parties are malicious/colluding).
2.  **Honest Majority MPC:** Protocols designed assuming more than half the parties follow the protocol honestly. Often based on secret sharing (like SSS) and evaluating circuits gate-by-gate on shared values. Can handle both Boolean and arithmetic circuits (using finite fields like $\mathbb{Z}_p$). These protocols are often **Turing complete** (can compute any function).
3.  **Input Sharing:** The phase where parties distribute shares of their private inputs to other participants using a scheme like SSS.
4.  **Circuit Evaluation:** The phase where parties jointly compute the function (represented as a circuit of gates like AND, XOR, ADD, MULT) on the shared inputs, gate by gate, without revealing intermediate values. Requires protocols for secure addition and multiplication of shares.
5.  **Private Set Intersection (PSI):** A specific MPC task where two (or more) parties want to find the intersection of their private sets without revealing any elements not in the intersection. Efficient protocols exist for this specific problem.
6.  **Threshold Cryptography:** Techniques allowing a group of parties to perform a cryptographic operation (like decryption or signing) jointly, requiring a minimum number (threshold) of parties to cooperate, without any single party knowing the full secret key. Related to MPC and secret sharing. (Example: Threshold RSA signature).
7.  **Dishonest Majority MPC:** Protocols designed to be secure even if a majority of parties are malicious or colluding (up to $n-1$ colluding parties). These are generally more complex and less efficient than honest majority protocols. Techniques include:
    *   **Garbled Circuits (Yao's Protocol):** Primarily for two-party computation (2PC). One party "garbles" the circuit representing the function, the other evaluates it obliviously.
    *   **Oblivious Transfer (OT):** A protocol where a sender transmits one of potential pieces of information to a receiver, but remains oblivious as to which piece (if any) the receiver obtained. A fundamental building block for many MPC protocols, especially in the dishonest majority setting.
    *   **GMW Protocol:** Based on oblivious transfer.
    *   (Tiny oz is likely a reference to a specific protocol family/implementation).

### Advantages of MPC

-   **Promotes Privacy and Data Utility:** Enables valuable computations on combined datasets without compromising individual privacy. Overcomes the typical privacy-utility tradeoff. Eliminates need for trusted third parties holding raw data.
-   **Reveals Only Final Result:** Intermediate computations remain hidden/encrypted/shared, protecting sensitive intermediate information. Can offer higher security than approaches like Federated Learning where model parameters (which can leak information) are shared.
-   **Less Resource-Intensive (than FHE):** While still computationally intensive, MPC can often be significantly more efficient than FHE for many practical tasks, especially regarding computational power (though communication overhead can be high).
-   **No Single Trusted Third Party:** Security relies on distributing trust among the participants (or assumptions about non-collusion) rather than a central authority.
-   **High Accuracy:** Computations are cryptographically guaranteed to be correct (under the protocol's security assumptions).
-   **Quantum Safe (Potentially):** Security of many MPC protocols relies on symmetric crypto or assumptions not known to be broken by quantum computers (depends on specific building blocks used).

### Disadvantages of MPC

-   **Communication Overhead:** MPC protocols typically require significant communication (multiple rounds of interaction) between the participating parties, which can be a bottleneck, especially with high latency or many parties.
-   **Computational Cost:** While potentially better than FHE, MPC can still be computationally expensive compared to plaintext computation.
-   **Vulnerability to Collusion:** Security often relies on assumptions about how many parties might collude. If more parties collude than the protocol's threshold allows, they may be able to learn private inputs or manipulate the output. Designing protocols secure against arbitrary collusion is challenging and costly.
-   **Complexity:** Designing and implementing secure and efficient MPC protocols is complex.

### MPC vs. Alternatives

Compared to other privacy-preserving techniques:

-   **Homomorphic Encryption (HE):** HE allows one party (e.g., cloud) to compute on another party's encrypted data. MPC involves multiple parties computing on their *own* distributed private data. MPC avoids giving encrypted data to one central compute node. MPC often more efficient currently, HE simpler communication.
-   **Zero-Knowledge Proofs (ZKP):** ZKP proves a statement *about* data without revealing the data. MPC *computes a function* on private data without revealing the data. They address different (though sometimes related) problems.
-   **Differential Privacy:** Adds noise to query results on a dataset to protect individual privacy while allowing aggregate statistics. MPC protects the inputs *during* computation. Differential privacy protects outputs *after* computation. Can be used together.
-   **Synthetic Data:** Creates artificial data mimicking real data's properties. MPC works directly on real (shared/encrypted) data.
-   **Federated Learning:** Trains ML models locally on distributed data, sharing only model updates, not raw data. MPC can be used *within* federated learning to further protect the updates or the aggregation process.

### Section Summary: Secure Multi-Party Computation

-   **Goal:** Allow multiple parties to jointly compute `f(x1, x2, ..., xn)` where each party `i` only knows `xi`, without revealing `xi` to others.
-   **Properties:** Input Privacy, Correctness.
-   **Applications:** Privacy-preserving data analysis (finance, health, marketing), voting, auctions, machine learning.
-   **Techniques:** Secret Sharing (Shamir), Garbled Circuits, Oblivious Transfer, Threshold Cryptography. Security models vary (honest vs. dishonest majority).
-   **Tradeoffs:** High communication overhead, computational cost, vulnerability to collusion above threshold vs. strong privacy and correctness guarantees without a central trusted party.

---

## Zero-Knowledge Proofs (ZKP)

### Concept

-   **Zero-Knowledge Proof (ZKP):** A cryptographic protocol where one party, the **Prover (Peggy)**, can convince another party, the **Verifier (Victor)**, that a specific statement is true, **without revealing any information whatsoever beyond the fact that the statement is true**.
-   **Zero-Knowledge Proof of Knowledge:** A special case where the statement being proved is simply "I know a secret" (e.g., a password, a private key, a solution to a puzzle) without revealing the secret itself.
-   **Essence:** It's easy to prove knowledge by revealing the secret. The challenge is to prove possession of the knowledge *without* revealing it or any related information.

### Properties of a ZKP

A protocol must satisfy three properties to be a ZKP:

1.  **Completeness:** If the statement is true, an honest Prover following the protocol can always convince an honest Verifier.
2.  **Soundness:** If the statement is false, a cheating Prover cannot convince an honest Verifier that it is true, except possibly with a very small, negligible probability (the "soundness error").
3.  **Zero-Knowledge:** If the statement is true, the Verifier learns *nothing* other than the truth of the statement itself. Any information the Verifier gains during the protocol could have been generated by the Verifier alone (or a "simulator") without interacting with the Prover, just by knowing the statement is true.

*(Completeness and Soundness are properties of general interactive proofs; Zero-Knowledge is the distinguishing feature).*

### Illustrative Examples

1.  **Ali Baba Cave (Fiat-Shamir):**
    -   **Scenario:** Peggy wants to prove to Victor she knows the secret phrase to open a magic door inside a ring-shaped cave (paths A & B meet at the door). She doesn't want to reveal the phrase.
    -   **Protocol:**
        1. Peggy enters the cave and randomly goes down path A or B. Victor waits outside.
        2. Victor enters the entrance and randomly shouts "Come out via path A!" or "Come out via path B!".
        3. Peggy hears Victor. If she's already on the requested path, she walks out. If she's on the *other* path, she uses the secret phrase to open the magic door, passes through, and comes out the requested path.
    -   **Analysis:**
        -   **Completeness:** If Peggy knows the secret, she can always satisfy Victor's request.
        -   **Soundness:** If Peggy *doesn't* know the secret, she can only succeed if Victor happens to ask for the path she initially chose (50% chance). By repeating the protocol many times (e.g., 20 times), the probability of her succeeding every time by luck becomes negligibly small ($1/2^{20} \approx 1/\text{million}$). If she succeeds repeatedly, Victor becomes convinced she knows the secret.
        -   **Zero-Knowledge:** Victor learns nothing about the secret phrase itself. He only sees Peggy emerge from the path he requested.
        -   **Non-Transferability:** This interactive proof is not convincing to a third party watching a recording, as Peggy and Victor could have pre-arranged the sequence of Victor's requests to make it look like she knows the secret.
        
    ![[Pasted image 20250506024452.png]]the Ali Baba cave diagram series, illustrating Peggy entering, Victor choosing an exit path, and Peggy emerging.

2.  **Two Balls and the Color-Blind Friend:**
    -   **Scenario:** You (Prover) have a red ball and a green ball (identical otherwise). Your friend (Verifier) is red-green color-blind and skeptical they are different colors. You want to prove they are different without revealing which is red and which is green.
    -   **Protocol:**
        1. Friend takes both balls behind their back.
        2. Friend reveals one ball. You see it.
        3. Friend puts it back. Then, randomly chooses to either switch the balls' positions or not.
        4. Friend reveals one ball again.
        5. Friend asks, "Did I switch the balls?"
    -   **Analysis:**
        -   **Completeness:** Since you can see the colors, you can always correctly answer if they switched or not.
        -   **Soundness:** If the balls were the same color, you would only guess correctly 50% of the time. Repeating the protocol makes your consistent success convince the friend they must be different colors.
        -   **Zero-Knowledge:** The friend never learns *which* ball is red and which is green, only that they *are* different. They gain no ability to distinguish them afterwards.

3.  **Finding Waldo:**
    -   **Scenario:** Peggy has found Waldo in a large picture and wants to prove this to Victor without revealing Waldo's location.
    -   **Protocol Idea:** Peggy takes a large piece of cardboard, cuts a small hole in it just big enough to see Waldo, and places it over the picture such that only Waldo is visible through the hole. She shows this to Victor. Victor sees Waldo but doesn't learn his location relative to the rest of the picture (which is covered).

### Types of ZKP

-   **Interactive ZKP:** Requires back-and-forth communication (challenges and responses) between the Prover and Verifier (like the Ali Baba example). Can be complex to scale and requires parties to be online simultaneously.
-   **Non-Interactive ZKP (NIZK):** The Prover generates a single proof string that can be verified by anyone at any time without further interaction. Often requires a trusted setup phase (e.g., generating a Common Reference String - CRS) or relies on cryptographic hash functions (using the Fiat-Shamir heuristic to make interaction non-interactive). NIZKs are more suitable for decentralized systems like blockchains.
    -   **Fiat-Shamir Heuristic:** A technique to convert interactive proofs into non-interactive ones by replacing the verifier's random challenges with the output of a cryptographic hash function applied to the prover's previous messages.

### Applications

ZKP has diverse applications, especially where privacy is paramount:

-   **Authentication:** Prove knowledge of a password or secret key without revealing it (Zero-Knowledge Password Proofs, Sigma protocols). Used by Cloudflare for private web verification.
-   **Blockchain Privacy:** Enable confidential transactions on public blockchains. Users can prove transaction validity (e.g., sufficient funds, no double spending) without revealing sender, receiver, or amount.
    -   Examples: Zerocoin (used ZKPs, later flawed), Zcash (uses zk-SNARKs), Monero (uses Bulletproofs, Ring Signatures), Firo (uses Sigma, Lelantus).
-   **Ethical Behavior/Compliance:** Prove adherence to rules or protocols without revealing private strategies or data (e.g., proving tax compliance without revealing full financial details).
-   **Nuclear Disarmament Verification:** Allow inspectors to verify an object is a nuclear weapon (or has been dismantled) without revealing sensitive design secrets.
-   **Secure Computation:** Can be used as a building block within MPC protocols.

### Advantages

-   **Privacy:** Protects sensitive information (secrets, inputs) while still allowing verification of claims.
-   **Security:** Strengthens authentication and verification methods.
-   **Simplicity (Conceptually):** Doesn't always require complex encryption underneath (though practical implementations can be complex).
-   **Scalability (NIZK):** Non-interactive proofs are easily verifiable by many parties asynchronously.

### Disadvantages

-   **Limited Scope:** Typically proves mathematical statements or knowledge related to specific algebraic structures. Translating real-world problems can be complex.
-   **Computational Cost:** Generating ZKPs (especially NIZKs like zk-SNARKs) can be computationally intensive for the prover. Verification is often faster.
-   **Restricted Use:** Proving knowledge requires the prover to actually possess it. If information is lost, proof is impossible.
-   **Potential Vulnerabilities:** Security relies on underlying cryptographic assumptions (e.g., hardness of discrete log, hash function properties). Quantum computers could potentially break some assumptions. Trusted setup for some NIZKs can be a point of failure/mistrust if not done correctly.

### Section Summary: Zero-Knowledge Proofs

-   **Goal:** Prove a statement is true without revealing any extra information.
-   **Properties:** Completeness, Soundness, Zero-Knowledge.
-   **Types:** Interactive (requires interaction), Non-Interactive (single proof string).
-   **Applications:** Authentication, Blockchain Privacy, Compliance Verification.
-   **Key Idea:** Leverages probability and cryptography to provide proof without disclosure.

---

## Cryptographic Obfuscation

### Definition

-   **Obfuscation:** The process of transforming code or data (e.g., human-readable source code, executable file) into a version that is **difficult for humans to understand or reverse-engineer**, while **preserving its original functionality**.
-   **Analogy:** Camouflage for code/data.
-   **Contrast with Encryption:**
    -   **Encryption:** Transforms data into an unreadable format *unless* a secret key is used for decryption. Goal is confidentiality via key secrecy.
    -   **Obfuscation:** Aims to make understanding the logic difficult, even if the obfuscated code is fully accessible. Often does **not** rely on a cryptographic key for its primary effect (the "secret" is the complexity of the transformation). Security through obscurity.
-   **Contrast with Encoding:** Encoding (like Base64) is a reversible transformation using a publicly known algorithm, primarily for data transmission or storage, not for security/obscurity.

### Use Cases

-   **Legitimate:**
    -   **Intellectual Property (IP) Protection:** Making it harder for competitors to copy algorithms or software logic, especially for code distributed to users (e.g., mobile apps, client-side JavaScript).
    -   **Preventing Tampering:** Making it harder for users or attackers to modify software behavior.
    -   **Deterring Reverse Engineering:** Making analysis of software functionality more time-consuming and difficult.
-   **Malicious:**
    -   **Malware Evasion:** Used heavily by malware authors to hide malicious code from detection by antivirus (AV) software and security analysts. Obfuscation changes the code's signature without changing its malicious behavior.

### Real-Life Examples

1.  **SolarWinds Attack (Sunburst Malware):** Attackers used sophisticated obfuscation combined with other techniques (ML/AI) to hide a backdoor within legitimate software updates. They also altered logs and faked network activity to blend in, remaining undetected for over a year. (Pages 108-109)
2.  **Carbanak Malware:** This infamous banking malware used extensive obfuscation, making its source code (discovered on VirusTotal) very difficult to analyze. Techniques included complex control flow, hidden function pointers/parameters across multiple files and layers. Analysis required significant effort, even reverse engineering parts before the source was found. It also adapted evasion based on the target's AV. (Pages 126-129)
3.  **Multi-Step Obfuscated Malware (nslookup example):** (Pages 135-149)
    *   **Event:** Legitimate tool `nslookup.exe` makes suspicious connection to malicious URL.
    *   **Trace:** Execution traced back to `certutil.exe` (used to decode data hidden in certificate files).
    *   **Origin:** User executed a disguised file (`setup_x86_x64_install.exe`) supposedly signed by "AO Kaspersky Lab" (invalid signature). This file was an SFX (Self-Extracting) CAB archive.
    *   **SFX Action:** Extracts `Roccia.xltm` (obfuscated) and executes `cmd /c certutil -decode Roccia.xltm Fu.mp4 & cmd < Fu.mp4`.
    *   **Decoding:** `certutil` decodes `Roccia.xltm` into `Fu.mp4` (which contains obfuscated batch script commands).
    *   **Execution:** `cmd < Fu.mp4` executes the script.
    *   **Script Actions:**
        *   Checks for AV emulators (e.g., `C:\aaa_TouchMeNot_.txt`) or specific computer names; exits if found.
        *   Extracts content from `Agolo.mid` to create `rundll32.com` (AutoIt compiler).
        *   Decodes `Custodiva.ppt` (obfuscated AutoIt script).
        *   Runs the AutoIt script using the compiler.
    *   **AutoIt Script:** Contains junk code and string decryption. Spawns `nslookup.exe`. Uses **process hollowing** to replace the code of the running `nslookup.exe` process with malicious payload extracted from `Attesa.docm`.
    *   **Payload:** Information stealer (browser cookies/credentials, crypto wallets, system info, screenshots). Detected as TrojanSpy.Win32.PRETSTEAL.A.
    *   **Takeaways:** Single alerts need investigation; legitimate tools can be abused; good sensors needed for analysis. Multi-stage obfuscation makes analysis hard.

### Obfuscation Techniques

Techniques aim to make code harder to read and analyze automatically or manually:

1.  **Renaming:** Change meaningful variable/function names to meaningless ones (e.g., `a`, `b`, `c`) or even unprintable/invisible characters.
2.  **Packing/Compressing:** Compressing the executable/script. Requires unpacking before execution, hindering static analysis.
3.  **Control Flow Obfuscation:** Making the program's execution path hard to follow.
    *   Inserting "spaghetti logic" (unnecessary jumps, opaque predicates).
    *   Flattening: Transforming structured code into a large switch statement.
4.  **Instruction Pattern Transformation:** Replacing standard instruction sequences with equivalent but more complex or unusual ones.
5.  **Dummy Code Insertion:** Adding code that doesn't affect the program's outcome but adds noise and complexity for analysis.
6.  **Metadata/Unused Code Removal:** Stripping comments, debugging information, and dead code that might help an analyst.
7.  **Opaque Predicate Insertion:** Adding conditional branches (`if` statements) whose conditions always evaluate to true or always false in a way that's hard for static analysis to determine, leading analysis tools down dead ends or through unnecessary code paths.
8.  **Anti-Debugging:** Code includes checks to detect if it's running under a debugger. If detected, it might crash, change behavior, or erase itself.
9.  **String Encryption:** Encrypting string literals within the code. They are only decrypted at runtime when needed, hiding important strings (URLs, commands, messages) from static analysis.
10. **Code Transposition:** Reordering functions or code blocks without affecting execution logic, confusing analysis.

![[Pasted image 20250506024518.png]] the Code Obfuscation example. Shows a simple JavaScript `hello` function before and after obfuscation (using renaming and possibly string encoding/hex representation).

### Security Goals and Obfuscation

-   **Achieved:**
    -   **Confidentiality (of logic/secrets within code):** Hides algorithms, proprietary logic, embedded keys/URLs.
-   **Not Achieved Directly:**
    -   **Integrity:** Obfuscation doesn't prevent modification of the obfuscated code itself.
    -   **Availability:** Not relevant.
    -   **Authenticity:** Doesn't prove the origin of the code.
    -   **Non-repudiation:** Not relevant.

### Measuring Obfuscation Success

How effective is an obfuscation technique?

-   **Strength:** How well does it resist automated deobfuscation tools and manual analysis? (More effort/time needed = stronger).
-   **Differentiation:** How much does the obfuscated code differ structurally from the original? (More different = potentially more effective). Metrics might include predicate count, code complexity (e.g., DIT).
-   **Expense:** Cost of the obfuscation tool/process, impact on performance, scalability.
-   **Complexity:** More layers/types of obfuscation applied can increase effectiveness but also cost/performance impact.

### Advantages

-   **Secrecy:** Hides valuable code/logic from competitors/attackers. Can hide malicious code from AV.
-   **Efficiency:** Some techniques (like dead code removal) can slightly shrink programs.
-   **Security (Application Self-Protection):** Acts as a built-in defense layer, especially for apps in untrusted environments (e.g., client-side).

### Disadvantages

-   **Used by Malware:** Primary use case today is often malware evasion, complicating defense. Techniques like XOR and ROT-13 are common simple methods used by malware.
-   **Readability:** Makes code difficult to read/debug *for developers* too, increasing maintenance costs.
-   **Performance:** Some techniques (string decryption, complex control flow) can slow down execution.
-   **Not Foolproof:** Obfuscation is not true security like encryption. Determined attackers with the right tools (decompilers, deobfuscators, debuggers) can often reverse-engineer obfuscated code. It primarily raises the bar and cost for attackers.

### Section Summary: Cryptographic Obfuscation

-   **Goal:** Make code/data hard to understand/reverse-engineer, while preserving functionality. Used for IP protection and malware evasion.
-   **Vs Encryption:** Obfuscation focuses on obscurity, not confidentiality via keys. Reversible if method known.
-   **Techniques:** Renaming, packing, control flow modification, dummy code, anti-debug, string encryption, etc.
-   **Effectiveness:** Raises bar for analysis but not impossible to break. Measured by strength, differentiation, cost, complexity.
-   **Downsides:** Used by malware, hinders debugging, performance impact, not true security.

---

## Module Glossary (Modern Cryptography)

-   **Quantum Cryptography:** Using quantum mechanics for cryptographic tasks (e.g., QKD).
-   **Photon:** Fundamental unit (quantum) of light, used in QKD.
-   **Quantum Mechanics Principles:** Superposition, Uncertainty Principle, Observer Effect, No-Cloning Theorem.
-   **Quantum Key Distribution (QKD):** Protocol (like BB84) for secure key exchange using quantum properties. Detects eavesdropping.
-   **Polarization:** Property of photons (e.g., vertical, horizontal, diagonal) used to encode bits in QKD.
-   **Polarizer / Beam Splitter:** Optical components used to prepare/measure photon polarization.
-   **Basis (QKD):** An encoding/measurement scheme (e.g., Rectilinear +, Diagonal x).
-   **Sifted Key:** Raw key bits remaining after Alice and Bob reconcile bases in QKD.
-   **Homomorphic Encryption (HE):** Encryption allowing computation on ciphertexts.
-   **Partially Homomorphic Encryption (PHE):** Supports only addition OR multiplication indefinitely.
-   **Fully Homomorphic Encryption (FHE):** Supports unlimited addition AND multiplication. Requires techniques like bootstrapping. Extremely slow currently.
-   **Secure Multi-Party Computation (MPC / SMPC):** Protocol allowing multiple parties to jointly compute a function on private inputs without revealing them.
-   **Input Privacy (MPC):** Parties learn nothing but the output.
-   **Correctness (MPC):** Output is correct even with adversarial parties (up to a threshold).
-   **Shamir Secret Sharing (SSS):** Threshold secret sharing scheme based on polynomials.
-   **Garbled Circuits:** Technique (often for 2PC) where one party encrypts/garbles a circuit for the other to evaluate obliviously.
-   **Oblivious Transfer (OT):** Protocol where receiver gets one of sender's secrets, sender doesn't know which; receiver doesn't learn others. Building block for MPC.
-   **Zero-Knowledge Proof (ZKP):** Proving a statement is true without revealing any information beyond its truth.
-   **Prover / Verifier:** Roles in a ZKP protocol.
-   **Completeness (ZKP):** True statement is accepted.
-   **Soundness (ZKP):** False statement is rejected (with high probability).
-   **Zero-Knowledge Property:** Verifier learns nothing extra.
-   **Interactive / Non-Interactive ZKP (NIZK):** Whether interaction is required for proof/verification.
-   **Fiat-Shamir Heuristic:** Method to convert interactive proofs to non-interactive using hash functions.
-   **Cryptographic Obfuscation:** Making code/data hard to understand/reverse-engineer while preserving functionality.
-   **Reverse Engineering:** Analyzing software to understand its design and functionality.
-   **Deobfuscation:** Tools/techniques to reverse obfuscation.
-   **Obfuscation Techniques:** Renaming, Packing, Control Flow Obfuscation, Dummy Code, Anti-Debug, String Encryption, etc.
-   **Sunburst / Carbanak:** Examples of malware using advanced obfuscation.
-   **Process Hollowing:** Malware technique replacing code of a legitimate running process with malicious code.

---

## Further Reading / Resources

*(References are included within each section's notes based on the provided slides)*

-   Consider searching for surveys or tutorials on each topic (Quantum Cryptography, Homomorphic Encryption, MPC, ZKP, Obfuscation) from reputable sources like IACR ePrint Archive, security conference proceedings (CCS, S&P, USENIX Security, CRYPTO, Eurocrypt), or university course websites.

