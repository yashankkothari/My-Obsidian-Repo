
# Network Security


## **I. Introduction: Network Fundamentals & Vulnerabilities**

*   **Core Idea:** Networks connect systems, enabling communication and resource sharing, but also introduce vulnerabilities. Understanding the physical media and logical structure is key to security.
*   **Network Transmission Media:** Different physical ways data travels.
    *   Cable (e.g., Copper - Coaxial, Twisted Pair)
    *   Optical Fiber
    *   Microwave (Terrestrial point-to-point)
    *   WiFi (Radio waves based on IEEE 802.11 standards)
    *   Satellite Communication
*   **Media Vulnerability:**
    *   **Key Concept:** Each medium has unique **physical properties** that dictate its susceptibility to specific attacks (e.g., tapping, interference, interception).
    *   **Examples of Attack Touchpoints:** Wiretaps (physical connection), Sniffers/Rogue Receivers (passive listening), Interception (unauthorized viewing), Impersonation (pretending to be a legitimate device/user).
    *   `[🌍 Real-World Example]` Tapping into copper lines is relatively easy with physical access. Fiber tapping is harder but possible with specialized equipment. WiFi signals can be intercepted by anyone within range.
    *   `[❓ Thought-Provoking Question]` Which transmission medium offers the best *inherent* physical security against eavesdropping, and why?

*   **The OSI Model (Mentioned but not detailed):**
    *   `[⚠️ Clarification Needed]` The lecture mentions the OSI model but doesn't detail its layers. It's a foundational concept for understanding *where* different security measures operate (e.g., Link Encryption at Layer 1/2, SSL/TLS at Layer 4, Application Proxies at Layer 7). Recommend reviewing the 7 layers if unfamiliar.
    *   `[🔗 Connection]` Understanding OSI layers helps differentiate between Link vs. End-to-End encryption later.

*   **Fundamental Threats to Network Communications:**
    *   **Interception:** Unauthorized viewing/copying of data (Confidentiality breach).
    *   **Modification:** Unauthorized changing of data (Integrity breach).
    *   **Fabrication:** Unauthorized creation of data/packets (Integrity/Authentication breach).
    *   **Interruption:** Preventing authorized access (Availability breach, e.g., DoS).
    *   `[🧠 Mnemonic Suggestion]` Think **"I Must Find Information"** (Interception, Modification, Fabrication, Interruption) for the core threats.

*   **Security Perimeters:**
    *   **Definition:** A **secured boundary** between a controlled/trusted network (internal) and an uncontrolled/untrusted one (e.g., the Internet).
    *   Within the perimeter: Physical controls offer some protection.
    *   Between perimeters: Connections expose vulnerabilities.
    *   **Primary Control:** **Encryption** is crucial for protecting data traversing untrusted networks between perimeters.
    *   `[🖼️ Visual Note]` Slide 7 (Unknown Perimeter) visually represents how network boundaries can be complex and hard to define, especially with mobile devices, cloud services, etc. This makes enforcing a perimeter difficult.
    *   `[🖼️ Visual Note]` Slide 8 (Unknown Path) illustrates that data between two points might traverse many intermediate, potentially untrustworthy networks/routers.

*   **Components of a Network Perimeter:**
    *   **Border Routers:** Direct traffic at the edge of the controlled network.
    *   **Firewalls:** Enforce access control rules (allow/deny traffic).
    *   **Intrusion Detection Systems (IDS):** Monitor for and alert on suspicious activity (like an alarm).
    *   **Intrusion Prevention Systems (IPS):** An IDS that can also *block* detected threats automatically.
    *   **Demilitarized Zones (DMZ) / Screened Subnets:** Small, isolated networks for public-facing services (like web servers), protected by firewalls, separating them from the internal trusted network. `[🔗 Connection]` This relates to the DMZ architecture discussed later.

*   **Why Networks Are Vulnerable (Especially to Interception):**
    *   **Anonymity:** Attackers can launch attacks from afar with less chance of identification.
    *   **Many Points of Attack:** Every connected device/router is a potential entry point.
    *   **Sharing:** Shared resources increase potential exposure.
    *   **System Complexity:** Diverse systems (OSs, applications) increase complexity and potential flaws.
    *   **Unknown Perimeter:** Dynamic nature of networks makes boundaries unclear.
    *   **Unknown Path:** Data travels through potentially insecure intermediate systems.

*   **Data Corruption Sources:**
    *   `[⚠️ Clarification Needed]` Slide 9 mentions "Sources of Data Corruption" but doesn't list specific sources beyond the general threats already covered (modification, fabrication). This might refer to transmission errors or intentional modification attacks.

*   **Simple Replay Attack:**
    *   `[🖼️ Visual Note]` Slide 10 depicts an attacker capturing legitimate traffic (e.g., a login sequence) and re-transmitting it later to gain unauthorized access or disrupt service.
    *   **Key Concept:** Replaying valid, captured messages at a later time.

*   **Interruption: Loss of Service (Availability Threats):**
    *   **Routing Issues:** Misconfigurations can poison routing tables, disrupting traffic flow. `[🌍 Real-World Example]` BGP hijacks where incorrect routes are advertised, diverting traffic.
    *   **Excessive Demand:** Overwhelming network capacity (DoS/DDoS).
    *   **Component Failure:** Hardware/software failures require redundancy planning.

*   **Port Scanning:**
    *   **Definition:** Probing a target system to identify open ports and running services/versions.
    *   **Purpose:** **Reconnaissance** - gathering information before an attack. Not an attack itself, but often a precursor.
    *   `[🖼️ Visual Note]` Slide 11 shows sample output: Port number, Protocol (TCP/UDP), State (Open/Closed/Filtered), Service name (HTTP, FTP), Product/Version. This info reveals potential vulnerabilities.
    *   `[📝 Potential Exam Question]` Explain what port scanning is and why it is a security concern.

---

## **II. Wireless Network Security (WiFi - IEEE 802.11)**

*   **IEEE 802.11 Standard:** Defines specifications for Wireless LANs (WLANs), covering Physical and Data Link layers.

*   **Architecture:**
    *   **Basic Service Set (BSS):** A group of wireless devices communicating with each other.
        *   **Ad hoc network:** Devices connect directly without an Access Point (AP). `[🖼️ Visual Note]` Left side of Fig 14.1.
        *   **Infrastructure network:** Devices connect via a central Access Point (AP), which often connects to a wired network. `[🖼️ Visual Note]` Right side of Fig 14.1.
    *   **Extended Service Set (ESS):** Multiple BSSs connected via a distribution system (usually a wired LAN), allowing roaming between APs. `[🖼️ Visual Note]` Fig 14.2.

*   **MAC Sublayer (Data Link Layer):**
    *   `[🖼️ Visual Note]` Fig 14.3 shows the MAC layer structure within 802.11.
    *   **Key Mechanism: CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)**
        *   **Goal:** Prevent collisions in the shared wireless medium (unlike Ethernet's CSMA/CD - Collision *Detection*).
        *   **Process:**
            1.  **Listen Before Talking (Carrier Sense):** Check if the channel is idle.
            2.  **If Idle:** Wait a random backoff time (Interframe Space - IFS + random slots) before transmitting.
            3.  **If Busy:** Wait until idle, then start the backoff process.
            4.  **Collision Avoidance:** Use acknowledgements (ACKs) to confirm successful reception. If no ACK received, assume collision and retransmit after a longer backoff.
            5.  **NAV (Network Allocation Vector):** A timer mechanism. Stations hearing an RTS or CTS frame set their NAV, indicating how long the medium will be busy, preventing them from transmitting.
        *   `[🖼️ Visual Note]` Fig 14.4 shows the CSMA/CA flowchart.
        *   `[🖼️ Visual Note]` Fig 14.5 illustrates NAV usage.
    *   **Frame Format:**
        *   `[🖼️ Visual Note]` Fig 14.7 shows the general 802.11 frame structure. Key fields include Frame Control (FC), Duration/ID, Addresses (up to 4), Sequence Control, Frame Body, FCS (checksum).
        *   `[🖼️ Visual Note]` Table 14.1 details the subfields within the Frame Control (FC) field (e.g., Protocol Version, Type, Subtype, To DS, From DS, More Frag, Retry, Power Mgmt, More Data, Protected Frame, Order).
        *   `[🖼️ Visual Note]` Fig 14.8 & Table 14.2 show Control Frames (e.g., RTS, CTS, ACK) used for coordination.
        *   `[🖼️ Visual Note]` Table 14.3 & Fig 14.9 explain the different addressing mechanisms depending on whether traffic is going to/from the Distribution System (DS - wired network).
    *   **Hidden Station Problem:**
        *   **Problem:** Two stations can hear the AP, but not each other. They might transmit simultaneously, causing a collision at the AP.
        *   `[🖼️ Visual Note]` Fig 14.10 illustrates this. A hears AP, C hears AP, but A and C don't hear each other.
        *   **Solution:** **RTS/CTS Handshake (Request to Send / Clear to Send).** Station A sends RTS to AP. AP broadcasts CTS. Station C hears CTS and knows to wait (sets NAV).
        *   `[🖼️ Visual Note]` Fig 14.11 shows RTS/CTS solving the problem.
    *   **Exposed Station Problem:**
        *   **Problem:** A station (e.g., B) is within range of a transmitting station (A sending to AP) but wants to transmit to a different station (C) that is *not* in A's range. B incorrectly thinks the medium is busy due to hearing A's transmission.
        *   `[🖼️ Visual Note]` Fig 14.12 illustrates this. B hears A talking to AP, wants to talk to C, but holds back unnecessarily.
        *   **Solution:** Handshaking helps. If B hears RTS from A but not CTS from AP, it knows its own transmission to C won't interfere at the AP.
        *   `[🖼️ Visual Note]` Fig 14.13 shows handshaking resolving this.

*   **Physical Layers (Examples):**
    *   `[🖼️ Visual Note]` Table 14.4 lists various 802.11 physical layer standards (original, a, b, g, n, ac, ax, etc.) with different frequencies and data rates.
    *   Operate in unlicensed bands like the **ISM (Industrial, Scientific, and Medical)** band. `[🖼️ Visual Note]` Fig 14.14 shows ISM bands (e.g., 2.4 GHz, 5 GHz).
    *   Examples:
        *   **FHSS (Frequency Hopping Spread Spectrum):** Original standard, hops between frequencies. `[🖼️ Visual Note]` Fig 14.15.
        *   **DSSS (Direct Sequence Spread Spectrum):** Original standard, spreads signal over a wider band. `[🖼️ Visual Note]` Fig 14.16.
        *   **Infrared:** Short range, line-of-sight. `[🖼️ Visual Note]` Fig 14.17.
        *   **802.11b (HR-DSSS):** Popular early standard, 2.4 GHz, up to 11 Mbps. `[🖼️ Visual Note]` Fig 14.18.

*   **Vulnerabilities in Wireless Networks:**
    *   **Confidentiality:** Broadcast nature means unencrypted data is easily intercepted by anyone in range.
    *   **Integrity:** Attackers can potentially spoof legitimate devices (if signal is stronger) and forge sessions.
    *   **Availability:** Jamming (flooding frequency), forced disassociation, session hijacking.
    *   **Unauthorized WiFi Access:** Need cryptographic controls to prevent free-riding or malicious access.
    *   **SSID Issues:**
        *   *Picking up the beacon:* Hidden SSIDs are easily found by monitoring client probe requests.
        *   *SSID in all frames:* Once connected, SSID is in plaintext in frame headers.
        *   *Association issues:* Devices auto-connect to known SSIDs (e.g., "attwifi", "xfinitywifi"). Attackers can create **rogue access points** with these common names to trick devices (**Evil Twin Attack**). `[🔗 Connection]` Related to Spoofing.

*   **Failed Countermeasure: WEP (Wired Equivalent Privacy)**
    *   **Goal:** Intended to provide confidentiality equivalent to a wired network. Released with original 802.11 standard.
    *   **How it Worked (Simplified):**
        1.  Client & AP share a **pre-shared static key**.
        2.  AP sends challenge (random number) to client.
        3.  Client encrypts challenge with key, sends back.
        4.  AP decrypts, verifies challenge.
        5.  Subsequent communication encrypted with the shared key.
    *   **Why WEP Failed (CRITICAL FLAWS - Identified by 2001):**
        1.  **Weak Encryption Algorithm Usage:** Used **RC4** stream cipher, but the way WEP implemented it was severely flawed.
        2.  **Short/Weak Keys:** Keys were 64-bit or 128-bit, but **24 bits** were used for the **Initialization Vector (IV)**, leaving only 40 or 104 effective bits. Keys often derived from easy-to-guess passphrases (**Dictionary Attacks**).
        3.  **Predictable/Small Initialization Vectors (IVs):** The 24-bit IV space is too small, causing IVs to repeat frequently on busy networks. Attackers collect packets with the same IV to deduce the key (**Related-Key Attacks**).
        4.  **Static Keys:** Keys were manually configured and rarely changed. One key used for potentially months/years of traffic.
        5.  **Weak Key Scheduling Algorithm:** Vulnerable to statistical attacks (e.g., FMS attack) allowing key recovery by observing enough traffic.
        6.  **No Effective Integrity Check:** Used a simple checksum (CRC-32) easily defeated by attackers modifying packets.
        7.  **No Real Authentication:** Knowing the SSID and key was often enough; no robust device/user authentication.
        8.  **Vulnerable to Packet Injection/Replay:** No protection against these.
        9.  **Poor Key Management:** Manual distribution is insecure and difficult to scale.
    *   **Result:** WEP can be cracked in **minutes** with readily available tools. **Considered completely insecure.**
    *   `[Brief Summary]` WEP failed due to fundamental design flaws: weak RC4 implementation, short effective key lengths because of small IVs that repeated, static keys, poor integrity checks, and no real authentication.
    *   `[🧠 Mnemonic Suggestion]` **WEP's IV R S**ucks: **I**Vs repeat, **V**ery short keys, **R**C4 broken implementation, **S**tatic keys.

*   **Stronger Protocol Suite: WPA/WPA2 (WiFi Protected Access)**
    *   **WPA (2003):** Interim solution designed to run on hardware that supported WEP (used RC4 with **TKIP - Temporal Key Integrity Protocol**). TKIP fixed many WEP flaws but still had RC4 weaknesses.
    *   **WPA2 (2004):** Full standard, requires newer hardware. **Mandated AES (Advanced Encryption Standard)** encryption, which is much stronger. This is the current standard.
    *   **Key Improvements over WEP:**
        1.  **Strong Encryption:** WPA2 uses **AES** (typically in CCMP mode), a modern, strong block cipher. WPA used TKIP as a wrapper around RC4.
        2.  **Dynamic Key Generation:** Uses **TKIP** (WPA) or **CCMP** (WPA2) to generate *unique* encryption keys for each packet (**non-static keys**). Uses a key hierarchy.
        3.  **Robust Authentication:**
            *   **WPA/WPA2-Personal (PSK - Pre-Shared Key):** Uses a passphrase (should be long and complex) for home use.
            *   **WPA/WPA2-Enterprise (802.1X/EAP):** Uses an authentication server (e.g., RADIUS) for individual user logins (usernames/passwords, certificates, tokens). Much more secure for organizations.
        4.  **Message Integrity Check (MIC):** WPA/WPA2 include a cryptographic **MIC** (called "Michael" in WPA/TKIP, part of CCMP in WPA2/AES) to detect tampering. Much stronger than WEP's CRC-32.
        5.  **Session Initiation:** Uses a **4-way handshake** to authenticate and establish fresh session keys (PTK, GTK) for encryption and integrity.
    *   **Security Status:** WPA2 with AES (CCMP) is considered secure if configured properly (**strong passphrase** for PSK, proper setup for Enterprise). Some attacks exist (e.g., KRACK against handshake, attacks against weak PSKs), but it's vastly superior to WEP. WPA3 is the latest iteration with further improvements.
    *   `[📌 Key Takeaway(s)]` WEP is broken and must not be used. WPA2 (or WPA3) with AES encryption and a strong passphrase (or Enterprise authentication) is the minimum standard for securing WiFi networks.

*   **Bluetooth Security (Briefly mentioned in slides 14.27-14.34)**
    *   **Purpose:** Short-range, ad-hoc wireless connection between diverse devices (phones, headsets, keyboards, etc.).
    *   **Architecture:**
        *   **Piconet:** One master device, up to 7 active slave devices. `[🖼️ Visual Note]` Fig 14.19.
        *   **Scatternet:** Interconnected piconets (a device can be a slave in one and master in another). `[🖼️ Visual Note]` Fig 14.20.
    *   **Layers:** Defines its own stack including Baseband (physical/MAC like), L2CAP (Logical Link Control), etc. `[🖼️ Visual Note]` Fig 14.21.
    *   `[⚠️ Clarification Needed]` The slides introduce Bluetooth architecture but don't detail its specific security vulnerabilities or mechanisms (e.g., pairing methods, encryption). This would require further information. Common threats include eavesdropping on unencrypted links, bluesnarfing (stealing data), bluejacking (sending unsolicited messages).

---

## **III. Denial of Service (DoS) & Distributed DoS (DDoS) Attacks**

*   **Goal:** To make a system or service **unavailable** to legitimate users by overwhelming its resources or exploiting a flaw.
*   **DoS (Denial of Service):** Attack originating from a **single source**.
*   **DDoS (Distributed Denial of Service):** Attack originating from **multiple compromised systems** (often a **Botnet**), coordinated by an attacker. Much harder to block due to distributed nature. `[🖼️ Visual Note]` Slide 26 provides a clear visual distinction.
*   **Botnet:** A network of compromised computers ("bots" or "zombies") controlled remotely by an attacker (via a **Command and Control - C&C** server). Often used for DDoS, spam, etc. Bots can be difficult to detect and trace back to the attacker. `[🖼️ Visual Note]` Slide 30 explains Botnets and their role in DDoS.

*   **How DDoS Works (General Steps):**
    1.  **Compromise:** Attacker infects many machines with malware (creating bots). `[🌍 Real-World Example]` The DYNDNS attack (Slide 31) used compromised IoT devices (WiFi cameras with default passwords).
    2.  **Control:** Bots connect to a C&C server awaiting instructions.
    3.  **Attack Initiation:** Attacker commands the botnet to flood the target.
    4.  **Overwhelm Target:** Target's resources (bandwidth, CPU, memory, connection table) are exhausted, causing slowdown or crash.
    *   `[🖼️ Visual Note]` Slide 28 & 29 visually depict this process.

*   **Types of DoS/DDoS Attacks:**
    1.  **Volumetric Attacks:** Overwhelm the target's **bandwidth** with sheer volume of traffic.
        *   **Goal:** Clog the pipe.
        *   **Examples:**
            *   **UDP Flood:** Sends large numbers of UDP packets, often to random ports. The server checks for applications, sends back ICMP "Destination Unreachable," consuming resources. `[🖼️ Visual Note]` Slide 3, bottom right.
            *   **ICMP Flood (Ping Flood):** Overwhelms target with ICMP Echo Request packets (pings). Target uses resources responding with Echo Replies. Requires knowing target IP. `[🖼️ Visual Note]` Slides 39, 40.
                *   *Types of Ping Flood:* Targeted Local, Router Disclosed, Blind Ping (recon first). (Slide 41)
            *   **Amplification Attacks (Reflected DoS):** Attacker sends requests to legitimate servers (**reflectors**) with the source IP **spoofed** to be the victim's IP. The servers send large replies back to the victim, amplifying the attack volume. `[🖼️ Visual Note]` Slide 4 (Reflected DoS concept).
                *   **Smurf Attack (ICMP Amplification):** Sends ICMP Echo Requests to network broadcast addresses with victim's spoofed IP. All hosts on that network reply to the victim. (Largely mitigated today by disabling broadcast forwarding). `[🖼️ Visual Note]` Slides 42, 43.
                *   **DNS Amplification:** Sends small DNS queries (with spoofed source IP) to open DNS resolvers, requesting large records (e.g., TXT records). Resolvers send large replies to the victim. `[🖼️ Visual Note]` Slide 37, 38 mentions this concept.
    2.  **Protocol Attacks (State-Exhaustion Attacks):** Consume server resources by exploiting network protocols (often at Layers 3 & 4).
        *   **Goal:** Overwhelm connection state tables in servers, firewalls, load balancers.
        *   **Examples:**
            *   **SYN Flood:** Exploits the TCP 3-way handshake (SYN, SYN-ACK, ACK). Attacker sends many SYN packets (often with spoofed source IPs). Server replies with SYN-ACK and waits for ACK, allocating resources for each half-open connection. If ACKs never arrive, the server's connection table fills up, preventing legitimate connections. `[🖼️ Visual Note]` Slide 3 (top right), Slide 36.
            *   **Ping of Death:** (Older attack) Sending a malformed, oversized ICMP packet that could crash older systems upon reassembly. (Not the same as Ping Flood).
            *   **Teardrop Attack:** Sending fragmented IP packets with overlapping/conflicting offset fields. Target system crashes trying to reassemble them. `[🖼️ Visual Note]` Slide 44.
    3.  **Application Layer Attacks (Layer 7 Attacks):** Target specific application vulnerabilities or resource usage. Can be harder to detect as traffic may look legitimate.
        *   **Goal:** Exhaust application/server resources (CPU, memory, disk I/O).
        *   **Examples:**
            *   **HTTP Flood:** Overwhelms a web server with seemingly legitimate HTTP GET or POST requests. Can be simple floods or requests that require complex server-side processing (database lookups, large file generation). `[🖼️ Visual Note]` Slide 33, 34.
            *   **Slowloris:** Attacker opens many connections to a web server and keeps them open by sending partial HTTP requests very slowly, never completing them. Ties up server connection slots, preventing legitimate users from connecting. Uses low bandwidth (Stealthy). `[🖼️ Visual Note]` Slide 5.
            *   Other Slow attacks (Slow Read, etc.)

*   **Other Related Network Attacks:**
    *   **DNS Spoofing (DNS Cache Poisoning):** Attacker provides false DNS information, redirecting users to malicious sites or causing DoS by sending traffic to the wrong place. `[🖼️ Visual Note]` Slide 45. `[🔗 Connection]` Integrity attack.
    *   **Rerouting Routing:** Maliciously altering routing tables (e.g., BGP hijacking) to divert traffic (potential DoS or Man-in-the-Middle). `[🖼️ Visual Note]` Slide 46 shows normal routing advertisement; malice would involve false advertisements. `[🔗 Connection]` Related to Routing Issues under Interruption.
    *   **Session Hijacking (TCP Session Hijacking):** Attacker takes over an established TCP session between two parties, impersonating one of them. Involves predicting/spoofing sequence numbers. `[🖼️ Visual Note]` Slide 47. `[🔗 Connection]` Related to Impersonation/Spoofing.

*   **DoS/DDoS Countermeasures:**
    1.  **Infrastructure/Network Level:**
        *   **Over-provisioning Bandwidth:** Having more capacity than normally needed.
        *   **Traffic Scrubbing Centers / DDoS Mitigation Services:** Specialized providers (e.g., Cloudflare, Akamai, AWS Shield, Azure DDoS Protection) analyze incoming traffic, filter malicious packets, and forward legitimate traffic. `[🌍 Real-World Example]` Many large websites use these services. `[🖼️ Visual Note]` Slide 6 (Cloud-based protection).
        *   **Rate Limiting:** Restricting the number of requests a source IP can make in a given time. `[🖼️ Visual Note]` Slide 6 (Router/FW rate limiting).
        *   **Firewalls (Network & WAF):** Block known bad IPs, enforce protocol standards, filter malicious application requests (Web Application Firewalls).
        *   **Load Balancers:** Distribute traffic across multiple servers, increasing capacity and resilience.
        *   **Content Delivery Networks (CDNs):** Distribute content geographically closer to users, absorbing traffic spikes and filtering some attacks.
        *   **IP Reputation Filtering:** Blocking traffic from known malicious IP addresses or botnets.
        *   **Reverse Path Filtering (uRPF):** Router feature to help prevent IP spoofing by checking if the source IP of an incoming packet is reachable via the interface it arrived on. (Mentioned on Slide 7, Linux Mitigations).
    2.  **Server/Application Level:**
        *   **SYN Cookies:** Server responds to SYN with a cryptographically generated cookie in the SYN-ACK, instead of storing state. If a valid ACK (with cookie info) returns, state is recreated. Mitigates SYN floods. (Mentioned on Slide 7, Linux Mitigations). `[🖼️ Visual Note]` Slide 7 diagram.
        *   **Application-Level Filtering:** Tuning web servers/applications to reject malformed requests, limit resource-intensive operations.
        *   **Challenge-Response Tests (CAPTCHA):** Distinguish humans from bots for application-layer attacks.
    3.  **Planning & Architecture:**
        *   **Scalable Architecture:** Ability to dynamically add resources (cloud auto-scaling).
        *   **Incident Response Plan:** Predefined steps to identify, mitigate, and recover from an attack.
        *   **Regular Security Audits & Patching:** Close vulnerabilities exploited by attackers.
    *   `[📝 Potential Exam Question]` Describe three different types of DDoS attacks and a potential countermeasure for each.

---

## **IV. Network Security Controls & Essentials**

*   **Core Goal:** Protect Confidentiality, Integrity, and Availability (CIA Triad) of network communications.
*   **Key Tools & Techniques:** Encryption, Protocols, Secure Routing, VPNs, Firewalls, DMZs, IDS/IPS.

*   **1. Encryption:** Making data unreadable without the correct key.
    *   **Link Encryption:**
        *   **Where:** Encrypts data on the **physical link** between two adjacent nodes (e.g., router-to-router, device-to-AP). Operates at **Layer 1 (Physical) or 2 (Data Link)**.
        *   **How:** Each node decrypts upon receipt, potentially re-encrypts for the next hop.
        *   **Pros:** Can encrypt entire packet including headers (sometimes). Transparent to end users. High performance.
        *   **Cons:** Data is **plaintext** inside intermediate nodes (routers, switches). Vulnerable if intermediate nodes are compromised.
        *   **Use Cases:** Securing physical media (satellite links, fiber, some wireless hops), situations where intermediate nodes are trusted or physical security is paramount.
        *   `[🖼️ Visual Note]` Slide 52 & 53 depict encryption only between adjacent nodes.
        *   `[🌍 Real-World Example]` MACsec (IEEE 802.1AE) for Ethernet links, some satellite uplinks.
    *   **End-to-End Encryption:**
        *   **Where:** Encrypts data at the **source application**, decrypted only by the **destination application**. Operates typically at **Layer 4 (Transport) or 7 (Application)**.
        *   **How:** Intermediate nodes (routers) cannot decrypt the payload (though headers might be visible depending on implementation, e.g., IP addresses).
        *   **Pros:** Data remains **confidential** even through untrusted intermediate networks (like the Internet). Protects against compromised intermediate nodes.
        *   **Cons:** Can be more complex to implement. Doesn't typically encrypt all header information (like IP addresses, needed for routing). Performance overhead might be higher.
        *   **Use Cases:** Secure web browsing (HTTPS/TLS), secure email (PGP/SMIME), secure messaging apps, VPNs.
        *   `[🖼️ Visual Note]` Slide 56 & 57 show encryption spanning from original sender to final receiver.
        *   `[🌍 Real-World Example]` WhatsApp messages, Signal calls, HTTPS websites, ProtonMail emails.
    *   **Link vs. End-to-End Comparison:**
        *   `[🖼️ Visual Note]` Slide 62 provides a direct visual comparison. Link protects hops; End-to-End protects the entire path's content from source application to destination application. They can be used together.
        *   `[📌 Key Takeaway(s)]` Link encryption protects data over specific physical segments. End-to-End encryption protects data content across the entire journey between communicating applications, regardless of the intermediate networks.

*   **2. Cryptographic Protocols:** Standardized methods using cryptography to secure communications.
    *   **SSL/TLS (Secure Sockets Layer / Transport Layer Security):**
        *   **Purpose:** Provides secure communication (authentication, confidentiality, integrity) primarily between web browsers and servers (HTTPS), but also used for email, VPNs, etc.
        *   **History:** SSL (Netscape, deprecated due to flaws) -> **TLS** (IETF standard, current versions 1.2, 1.3 are secure). Often still called SSL colloquially.
        *   **Layer:** Operates at **Layer 4 (Transport)**, though sometimes seen as Layer 5/6 shim.
        *   **Provides:**
            *   **Server Authentication:** Client verifies server's identity using its **digital certificate**. `[🖼️ Visual Note]` Slide 67 shows certificate details (domain, owner, issuer CA, dates, signature algorithm). Chain of trust relies on pre-trusted Root CAs in browser/OS.
            *   **Client Authentication (Optional):** Server can verify client identity (less common for web, used in B2B).
            *   **Encrypted Communication:** Confidentiality for data exchanged.
            *   **Integrity:** Protects data from tampering using hash algorithms (MACs).
        *   **Handshake & Cipher Suites:**
            1.  Client connects, offers list of supported **Cipher Suites** (combinations of key exchange algorithm, encryption algorithm, hash algorithm).
            2.  Server chooses one suite from the list it also supports.
            3.  They perform key exchange (e.g., RSA, Diffie-Hellman) and authenticate (using certificates).
            4.  Establish shared session keys for encryption/integrity.
        *   **Vulnerability:** **Cipher Suite Negotiation Downgrade.** If server supports weak/broken cipher suites for compatibility, a Man-in-the-Middle attacker could force the client/server to negotiate a weak suite that the attacker can break. **Best practice:** Disable weak cipher suites on servers.
        *   **Applications:** HTTPS (web), SMTPS/IMAPS/POP3S (email), FTPS, VPNs (OpenVPN), VoIP, Secure APIs, IoT.
    *   **IPSec (Internet Protocol Security):**
        *   `[⚠️ Clarification Needed / Reading Assignment]` Mentioned but not detailed.
        *   **Purpose:** Provides security (authentication, confidentiality, integrity) at the **IP Layer (Layer 3)**. Often used for **VPNs**.
        *   **Modes:** Transport mode (encrypts payload) and Tunnel mode (encrypts entire original IP packet, adds new IP header - used for VPN gateways).
        *   **Protocols:** Authentication Header (AH) for integrity/auth, Encapsulating Security Payload (ESP) for confidentiality (+ optional integrity/auth). Key management via IKE (Internet Key Exchange).
        *   `[📚 Additional Resources]` RFC 4301 (IPSec Architecture).
    *   **SSH (Secure Shell):**
        *   `[⚠️ Clarification Needed / Reading Assignment]` Mentioned but not detailed.
        *   **Purpose:** Secure replacement for insecure remote login/command execution tools like Telnet, rlogin. Also used for secure file transfer (SFTP, SCP) and tunneling other protocols (port forwarding).
        *   **Provides:** Authentication (password, public key), confidentiality, integrity for interactive sessions and file transfers.
        *   **Layer:** Operates at the **Application Layer (Layer 7)**.
        *   `[🌍 Real-World Example]` System administrators connecting remotely to Linux/Unix servers.

*   **3. Secure Routing Approaches:** Techniques to protect routing information or anonymize traffic paths.
    *   **Onion Routing (e.g., Tor - The Onion Router):**
        *   **Goal:** Provide **anonymity** for the source of communication, preventing eavesdroppers from easily linking source and destination. Also provides confidentiality along the path.
        *   **How:**
            1.  Client software obtains list of **Onion Routers** (nodes in the Tor network).
            2.  Client chooses a path through multiple routers (e.g., 3 hops: Entry -> Middle -> Exit).
            3.  Client encrypts data in **multiple layers**, like an onion. Outermost layer encrypted for Exit node, next layer for Middle node, innermost for Entry node.
            4.  Each router decrypts only its layer, revealing the address of the *next* hop (not the original source or final destination).
            5.  Exit node sends data to the final destination (destination sees Exit node's IP, not original client's).
        *   **Properties:** Intermediate nodes don't know both source and destination. Destination doesn't know source. Entry node knows source but not destination (unless it's also exit).
        *   **Pros:** Strong anonymity against network surveillance.
        *   **Cons:** Increased latency. Exit node can see unencrypted traffic if the destination protocol isn't encrypted (e.g., plain HTTP). Vulnerable to timing analysis if attacker controls entry and exit nodes.
        *   **Use Cases:** Anonymous web browsing, circumventing censorship, protecting whistleblowers.
        *   `[🖼️ Visual Note]` Slides 70, 71, 73 depict the layered encryption and path.
    *   **Traffic Padding:**
        *   **Goal:** Obfuscate real traffic patterns (volume, timing) to hinder **traffic analysis**. Enhances privacy/anonymity.
        *   **How:** Adding extra, meaningless data (padding) to network packets or sending dummy packets during idle times. Makes it harder to infer activity levels or packet sizes.
        *   **Use Cases:** Often used within anonymity networks like Tor.

*   **4. Virtual Private Networks (VPNs):**
    *   **Definition:** Creates a **secure, encrypted tunnel** over a public network (like the Internet), connecting a user device or remote network to a private network.
    *   **Purpose:** Provides confidentiality, integrity, and authentication for traffic as if it were on a private network.
    *   **How:** Uses cryptographic protocols like **IPSec** or **SSL/TLS** (e.g., OpenVPN) to encapsulate and encrypt the original traffic.
    *   **Scenarios:**
        *   **Remote Access:** Teleworker connecting securely to the office network. `[🖼️ Visual Note]` Slide 76.
        *   **Site-to-Site:** Connecting two office networks securely over the Internet. `[🖼️ Visual Note]` Slide 75.
    *   **Benefits/Uses:**
        *   **Encryption:** Protects data from eavesdropping on public networks (e.g., public WiFi).
        *   **Privacy:** Hides user's real IP address from visited websites (they see the VPN server's IP).
        *   **Security:** Can protect against some network-based attacks.
        *   **Bypass Geo-restrictions:** Appear to be connecting from the VPN server's location.
        *   **Circumvent Censorship:** Access blocked content by tunneling through servers in uncensored locations.
    *   `[🌍 Real-World Example]` NordVPN, ExpressVPN, ProtonVPN (commercial services); OpenVPN, WireGuard (protocols/software); corporate VPNs for remote work.
    *   `[📝 Potential Exam Question]` What is a VPN, and describe two common scenarios where it is used?

*   **5. Firewalls:**
    *   **Definition:** A network security device (hardware or software) that **monitors and filters** incoming and outgoing network traffic based on a defined set of **security rules (policy)**. Acts as a barrier between a trusted internal network and untrusted external networks.
    *   **Goal:** Enforce access control, prevent unauthorized access.
    *   **Reference Monitor Characteristics:** Ideally, a firewall should be:
        *   **Always Invoked:** Cannot be bypassed.
        *   **Tamperproof:** Resistant to modification by attackers.
        *   **Small/Simple:** Verifiable for correctness. (Often a challenge in practice).
    *   **Firewall Environments:** Can range from simple single firewall setups to complex multi-firewall architectures with DMZs, VPNs, Intranets, Extranets.
        *   **Intranet:** Private network using Internet protocols/apps internally.
        *   **Extranet:** Intranet extended securely to business partners/remote users (often via VPN).
    *   **Types of Firewalls:**
        1.  **Packet Filtering Gateways (Stateless):**
            *   **Layer:** Network (Layer 3) / Transport (Layer 4).
            *   **How:** Examines packet headers (Source/Dest IP, Source/Dest Port, Protocol). Makes decisions based on static rules (ACLs). Does *not* track connection state.
            *   **Pros:** Fast, low overhead, relatively simple.
            *   **Cons:** Cannot detect application-specific attacks, vulnerable to IP spoofing, struggles with protocols requiring dynamic ports (e.g., FTP active mode).
            *   `[🖼️ Visual Note]` Slide 83 shows filtering based on protocol (Telnet vs. HTTP) and source IP.
        2.  **Stateful Inspection Firewalls:**
            *   **Layer:** Network (Layer 3) / Transport (Layer 4), with connection state tracking.
            *   **How:** Tracks the state of active connections (e.g., TCP handshake status). Allows return traffic automatically if it matches an established connection. More intelligent than packet filters.
            *   **Pros:** More secure than stateless, handles dynamic ports better, offers better protection against some scans/spoofing.
            *   **Cons:** Higher overhead than stateless, can still miss application-layer attacks.
            *   `[🖼️ Visual Note]` Slide 85 shows an example of tracking connections from an external IP and potentially blocking after a threshold.
        3.  **Application-Level Gateways (Proxies):**
            *   **Layer:** Application (Layer 7).
            *   **How:** Acts as an **intermediary** for specific applications (e.g., HTTP proxy, FTP proxy). Client connects to proxy, proxy connects to destination server. Can inspect application protocol commands and data.
            *   **Pros:** Deep inspection capabilities, can filter malicious commands/content, provide logging, caching.
            *   **Cons:** Slower than lower-layer firewalls, requires a separate proxy for each protocol, can break some applications.
            *   `[🌍 Real-World Example]` Web proxies used by companies to filter employee internet access.
            *   `[🖼️ Visual Note]` Slide 86 depicts the proxy acting as middleman.
        4.  **Circuit-Level Gateways:**
            *   **Layer:** Session (Layer 5).
            *   **How:** Monitors TCP/UDP session establishment (handshakes). Once session is approved, allows packets to flow without further content inspection. Often used for **VPNs** or in conjunction with NAT. Validates sessions rather than individual packets or application content.
            *   **Pros:** Hides internal network structure, faster than application proxies.
            *   **Cons:** No application-layer inspection.
            *   `[🖼️ Visual Note]` Slide 87 describes its function as a virtual gateway between networks.
        5.  **Stateful Multilayer Inspection Firewalls (Next-Generation Firewalls - NGFW):**
            *   **Layer:** Combines features across multiple layers (Network, Transport, Application).
            *   **How:** Integrates stateful inspection, application awareness/control, often includes Intrusion Prevention (IPS) capabilities, user identity integration, threat intelligence feeds.
            *   **Pros:** Most comprehensive protection, granular control over applications and users.
            *   **Cons:** Most complex, highest cost and overhead.
            *   `[🖼️ Visual Note]` Slide 89 compares types based on layer and functionality.
        6.  **Guards:** Specialized high-assurance firewalls, often used in classified environments. (Not detailed).
        7.  **Personal / Host-Based Firewalls:**
            *   **Where:** Software running on an individual computer (workstation/server).
            *   **How:** Filters traffic to/from that specific host. Can often control which *applications* are allowed network access.
            *   **Pros:** Protects host even if network firewall is breached, good for mobile devices.
            *   **Cons:** Needs to be managed on each host, consumes host resources.
            *   `[🌍 Real-World Example]` Windows Defender Firewall, macOS Firewall.
            *   `[🖼️ Visual Note]` Slide 88 shows Windows Firewall configuration allowing specific apps/protocols.
    *   **Firewall Limitations:**
        *   Only effective if they control the *entire* perimeter (no backdoors).
        *   Don't protect against threats *inside* the perimeter (insider attacks, malware brought in on USB).
        *   Don't protect data *outside* the perimeter (e.g., on mobile devices, cloud services unless tunneled).
        *   Are themselves targets of attack.
        *   Require correct configuration and ongoing maintenance.
        *   May have limited control over malicious content within allowed traffic (need other defenses like AV, IPS).
    *   **Network Address Translation (NAT):**
        *   **Purpose:** Translates private, non-routable IP addresses (used internally) to a public IP address (often the firewall's) for communication with the internet.
        *   **How:** Firewall maintains a translation table mapping internal IP:Port to external IP:Port.
        *   **Benefits:** Conserves public IP addresses, hides internal network structure (security by obscurity).
        *   **Not primarily a security feature, but often implemented on firewalls.**
        *   `[🖼️ Visual Note]` Slide 91 illustrates NAT changing the source IP.

*   **6. Demilitarized Zones (DMZs) / Screened Subnets:**
    *   **Concept:** A small, isolated network segment placed between the internal private network and the external untrusted network (Internet).
    *   **Purpose:** Host public-facing services (web servers, email servers, DNS servers) that need to be accessible from the outside, while protecting the internal network.
    *   **Architecture:** Typically uses one or two firewalls.
        *   *Two-firewall DMZ:* External firewall allows limited traffic to DMZ. Internal firewall allows very limited traffic from DMZ to internal network (if any), and potentially allows internal users to access DMZ services.
    *   **Benefit:** If a DMZ server is compromised, the attacker does not have direct access to the internal network due to the second firewall.
    *   `[🖼️ Visual Note]` Slide 97 shows a typical two-firewall DMZ architecture.

*   **7. Intrusion Detection Systems (IDS) & Intrusion Prevention Systems (IPS):**
    *   **IDS:** **Monitors** network traffic or system activity for suspicious patterns or known malicious signatures. **Alerts** administrators upon detection. (Like a burglar alarm).
    *   **IPS:** An IDS with the additional capability to **block or prevent** the detected malicious activity automatically. (Like a security guard who can intervene).
    *   **Purpose:** Detect attacks that bypass firewalls or originate internally. Complement preventative controls.
    *   **Functions:** Monitor activity, audit configs, check file integrity, pattern matching, anomaly detection, log analysis, operate honeypots/traps.
    *   **Types of IDS/IPS:**
        *   **Detection Method:**
            *   **Signature-Based:** Looks for known attack patterns (like AV signatures). Needs frequent updates. Misses zero-day attacks.
            *   **Anomaly-Based (Heuristic/Behavioral):** Establishes a baseline of normal activity and flags deviations. Can detect novel attacks but prone to false positives.
        *   **Location:**
            *   **Network-Based (NIDS/NIPS):** Sensor(s) placed on the network (e.g., near firewall, on critical segments) monitor traffic passing through.
            *   **Host-Based (HIDS/HIPS):** Agent runs on individual hosts, monitoring OS activity, logs, file changes.
        *   **Response (Capability):**
            *   **Passive (IDS):** Alerting only.
            *   **Active (IPS):** Takes action (e.g., block IP, terminate session, modify firewall rule).
    *   `[📝 Potential Exam Question]` Explain the difference between signature-based and anomaly-based IDS. What are the pros and cons of each?

*   **8. Other Security Tools/Concepts:**
    *   **Honeypots:** Decoy systems designed to attract and trap attackers, allowing defenders to study their methods and gather intelligence without risking production systems. `[🖼️ Visual Note]` Slide 94 depicts a honeypot diverting an attacker.
    *   **Security Information and Event Management (SIEM):**
        *   **Purpose:** Collects, aggregates, and correlates log data from various security devices (firewalls, IDS, servers, etc.) into a central platform.
        *   **Benefits:** Provides unified visibility, enables alerting, reporting, correlation of events across systems for faster threat detection and response.
        *   `[🖼️ Visual Note]` Slide 95 shows SIEM consolidating logs.
    *   **Data Loss Prevention (DLP):**
        *   **Purpose:** Detect and potentially block attempts to exfiltrate sensitive data from the network.
        *   **How:** Monitors network traffic or endpoint activity for keywords, patterns (credit card numbers, SSNs), encoding, encryption suggesting sensitive data transfer. Can be agent-based or network-based (guard).
        *   **Effectiveness:** Better at preventing *accidental* data loss; determined attackers may find ways around it.

*   **Intelligence Gathering Methods (Attacker Perspective):**
    *   **Social Engineering:** Tricking people into revealing sensitive info (passwords, network details).
    *   **Dumpster Diving:** Finding sensitive info in discarded trash.
    *   **Eavesdropping (Oral):** Listening to conversations.
    *   **Google Hacking (Dorking):** Using advanced search queries to find sensitive information unintentionally exposed on the internet.

*   **Web Site Vulnerabilities (Brief Overview):**
    *   **Defacement:** Unauthorized modification of website appearance.
    *   **Malicious URL Crafting:** Exploiting vulnerabilities via URL parameters (e.g., buffer overflows, directory traversal "../", SQL injection).
    *   **State Manipulation:** Modifying cookies or URL parameters to gain unauthorized access or elevate privileges.
    *   **Cross-Site Scripting (XSS):** Injecting malicious scripts (e.g., JavaScript) into a legitimate website, which then get executed by other users' browsers. Can steal cookies, redirect users, etc. `[🔗 Connection]` Active Code risk.

*   **Active Code Risks:**
    *   Code executed on the client-side (Java applets, JavaScript, ActiveX).
    *   **Risks:** Resource exhaustion (CPU/memory), display manipulation, potential access to local files or network resources (depending on security model/permissions).
    *   **Sandboxing:** Restricting code execution environment (Java, JavaScript attempt this).
    *   **ActiveX:** Less restricted, relies on digital signatures for trust (often problematic).
    *   **Third-Party Applications:** Invoked by browser (Word, PDF readers) can have their own vulnerabilities exploited.

---

## **V. Summary & Key Takeaways**

*   Networks are inherently vulnerable due to their distributed, complex, and shared nature.
*   Threats target Confidentiality (Interception), Integrity (Modification, Fabrication), and Availability (Interruption/DoS).
*   Understanding physical media (cable, fiber, wireless) reveals specific vulnerabilities (tapping, interception).
*   Wireless (WiFi) requires strong security (**WPA2/WPA3 with AES**) due to its broadcast nature; **WEP is completely insecure**. CSMA/CA and RTS/CTS manage wireless collisions and hidden stations.
*   **DoS/DDoS attacks** aim to deny service via Volumetric, Protocol, or Application-Layer techniques. Botnets amplify DDoS impact. Mitigation involves layered defenses (scrubbing, firewalls, rate limiting, specific techniques like SYN cookies).
*   **Encryption** is fundamental: **Link** encryption protects hops, **End-to-End** protects content across the entire path.
*   Key **Cryptographic Protocols** include **SSL/TLS** (web, email), **IPSec** (VPNs), **SSH** (remote admin).
*   **Firewalls** are critical perimeter controls, with types ranging from stateless Packet Filters to Application Proxies and Stateful NGFWs. **DMZs** isolate public services.
*   **IDS/IPS** detect/prevent intrusions missed by firewalls, using signature or anomaly-based methods.
*   Other important tools include **VPNs** (secure tunnels), **SIEM** (log correlation), **DLP** (data exfiltration prevention), **Honeypots** (decoys).
*   Be aware of intelligence gathering, web vulnerabilities (XSS), and active code risks.

---

## **VI. Glossary**</h2>

*   **AES (Advanced Encryption Standard):** Strong, modern symmetric block cipher standard used in WPA2/WPA3.
*   **AP (Access Point):** Device connecting wireless clients to a wired network in infrastructure mode.
*   **Botnet:** A network of compromised computers controlled remotely for malicious purposes (e.g., DDoS).
*   **BSS (Basic Service Set):** A group of wireless devices communicating; can be ad hoc or infrastructure.
*   **CIA Triad:** Confidentiality, Integrity, Availability - core security principles.
*   **Cipher Suite:** Combination of algorithms (key exchange, encryption, integrity) used in protocols like TLS.
*   **CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance):** MAC protocol for WiFi to prevent collisions.
*   **CTS (Clear to Send):** Control frame used in WiFi handshake to grant permission to send.
*   **DDoS (Distributed Denial of Service):** DoS attack launched from multiple sources.
*   **DMZ (Demilitarized Zone):** Isolated network segment for public-facing servers.
*   **DNS (Domain Name System):** Resolves human-readable hostnames to IP addresses.
*   **DoS (Denial of Service):** Attack to make a service unavailable.
*   **DSSS (Direct Sequence Spread Spectrum):** A physical layer technique for wireless communication.
*   **End-to-End Encryption:** Encryption where only the original sender and final receiver can decrypt the content.
*   **ESS (Extended Service Set):** Multiple BSSs connected to form a larger WLAN.
*   **FHSS (Frequency Hopping Spread Spectrum):** A physical layer technique for wireless communication.
*   **Firewall:** Network security device that filters traffic based on rules.
*   **Honeypot:** Decoy system to attract and study attackers.
*   **HTTP (Hypertext Transfer Protocol):** Protocol used for web browsing.
*   **HTTPS (HTTP Secure):** HTTP over SSL/TLS.
*   **ICMP (Internet Control Message Protocol):** Network layer protocol used for error reporting and diagnostics (e.g., ping).
*   **IDS (Intrusion Detection System):** Monitors for and alerts on malicious activity.
*   **IPS (Intrusion Prevention System):** An IDS that can also block threats.
*   **IPSec (Internet Protocol Security):** Suite of protocols for securing IP communications, often used for VPNs.
*   **ISM Band (Industrial, Scientific, Medical):** Unlicensed radio frequency bands used by WiFi, Bluetooth, etc.
*   **IV (Initialization Vector):** Random value used with encryption keys; WEP's small, predictable IVs were a major flaw.
*   **Link Encryption:** Encryption applied only between adjacent nodes on a communication path.
*   **MAC (Media Access Control):** Sublayer of Data Link layer; MAC address is a unique hardware identifier.
*   **MIC (Message Integrity Check):** Cryptographic checksum to detect data tampering (used in WPA/WPA2).
*   **NAT (Network Address Translation):** Technique to map private IP addresses to public ones.
*   **NAV (Network Allocation Vector):** Timer used in CSMA/CA to indicate medium reservation.
*   **NGFW (Next-Generation Firewall):** Advanced firewall with multi-layer inspection and integrated features.
*   **Onion Routing:** Anonymity technique using layered encryption through multiple relays (e.g., Tor).
*   **OSI Model:** 7-layer conceptual model for network communication.
*   **Packet Filtering:** Firewall type operating at Layer 3/4 based on headers.
*   **Port Scanning:** Probing ports to identify open services.
*   **Proxy (Application Gateway):** Firewall type acting as an intermediary for specific applications (Layer 7).
*   **PSK (Pre-Shared Key):** Authentication method using a shared secret passphrase (WPA/WPA2-Personal).
*   **RC4:** Stream cipher used in WEP (flawed implementation) and older TLS versions (now insecure).
*   **RTS (Request to Send):** Control frame used in WiFi handshake to request permission to send.
*   **SIEM (Security Information and Event Management):** System for collecting and correlating security logs.
*   **Smurf Attack:** DDoS amplification attack using ICMP echo requests to broadcast addresses.
*   **Spoofing:** Masquerading as another entity (IP address, MAC address, user, website).
*   **SSH (Secure Shell):** Protocol for secure remote login, file transfer, and tunneling.
*   **SSID (Service Set Identifier):** Name of a WiFi network.
*   **SSL (Secure Sockets Layer):** Predecessor to TLS; now deprecated/insecure.
*   **Stateful Inspection:** Firewall type that tracks connection state.
*   **SYN Flood:** DDoS attack exploiting the TCP handshake by sending many SYN packets.
*   **TCP (Transmission Control Protocol):** Connection-oriented transport layer protocol providing reliable delivery.
*   **TKIP (Temporal Key Integrity Protocol):** Encryption protocol used in WPA as an improvement over WEP (based on RC4).
*   **TLS (Transport Layer Security):** Standard protocol for securing communications (successor to SSL).
*   **UDP (User Datagram Protocol):** Connectionless transport layer protocol; faster but less reliable than TCP.
*   **VPN (Virtual Private Network):** Secure, encrypted tunnel over a public network.
*   **WEP (Wired Equivalent Privacy):** Early, flawed, and insecure WiFi encryption standard.
*   **WPA/WPA2/WPA3 (WiFi Protected Access):** Security protocols designed to replace WEP; WPA2/WPA3 with AES are secure.
*   **XSS (Cross-Site Scripting):** Web vulnerability allowing injection of malicious scripts into websites.

---

## **VII. Potential Exam Questions**

1.  Compare and contrast Link Encryption and End-to-End Encryption, discussing their operational layers, advantages, disadvantages, and typical use cases.
2.  Explain why WEP failed as a security mechanism for WiFi networks. List at least four distinct major weaknesses.
3.  Describe the difference between WPA and WPA2, focusing on the encryption algorithms typically used. Why is WPA2 considered significantly more secure?
4.  What is a DDoS attack? Explain the difference between a Volumetric attack (give an example) and a Protocol attack (give an example).
5.  Describe the TCP SYN Flood attack. How does it work, and what resource does it target? What is a common mitigation technique?
6.  List and briefly describe three different types of firewalls based on their operational layer and filtering mechanism (e.g., Packet Filter, Stateful, Application Proxy).
7.  What is the purpose of a DMZ in network architecture? How does it enhance security?
8.  Explain the difference between an Intrusion Detection System (IDS) and an Intrusion Prevention System (IPS).
9.  What is the Hidden Station Problem in WiFi, and how does the RTS/CTS mechanism help mitigate it?
10. Define Onion Routing and explain how it aims to provide user anonymity.

---

## **VIII. Further Research / Clarification Needed**

*   Details of the **OSI Model** layers and their relevance to specific security controls.
*   Specific implementation details and vulnerabilities of **IPSec** and **SSH**.
*   Modern attacks against **WPA2/WPA3** (e.g., KRACK, Dragonblood) and their practical impact.
*   Advanced **Botnet C&C** architectures and takedown challenges.
*   Deep dive into **Web Application Firewall (WAF)** functionalities.
*   Details on specific **routing security protocols** (e.g., RPKI for BGP security).

---

## **IX. Additional Resources**</h2>

*   **Textbook:** Security in Computing, Fifth Edition by Pfleeger, Pfleeger, and Margulies.
*   **NIST Special Publications:** SP 800 series (e.g., SP 800-41 on Firewalls, SP 800-94 on IDS/IPS, SP 800-113 on SSL/TLS).
*   **OWASP (Open Web Application Security Project):** Resources on web vulnerabilities like XSS, SQL Injection. (owasp.org)
*   **Cloudflare Learning Center:** Explanations of DDoS, CDN, TLS, etc. (cloudflare.com/learning/)
*   **Wireshark Wiki:** Protocol information and packet analysis. (wiki.wireshark.org)
*   **Tor Project Website:** Information on Onion Routing. (torproject.org)

---

## **X. Mind Map Concept (Text Outline)**

```
Network Security
├── Fundamentals
│   ├── Transmission Media (Cable, Fiber, WiFi, Microwave, Satellite) -> Physical Vulnerabilities
│   ├── Network Threats (Interception, Modification, Fabrication, Interruption - CIA)
│   ├── Network Vulnerabilities (Anonymity, Complexity, Unknown Perimeter/Path)
│   └── Security Perimeters (Firewall, Router, IDS/IPS, DMZ)
├── Wireless Security (IEEE 802.11 - WiFi)
│   ├── Architecture (BSS, ESS, Ad hoc, Infrastructure)
│   ├── MAC Layer (CSMA/CA, NAV, Hidden/Exposed Station, RTS/CTS)
│   ├── Physical Layers (ISM Bands, FHSS, DSSS, 802.11b/g/n/ac/ax)
│   ├── Vulnerabilities (Eavesdropping, Rogue APs, SSID issues)
│   ├── WEP (Failed Standard - IVs, RC4 flaws, Static Keys)
│   └── WPA/WPA2/WPA3 (Secure Standards - AES, TKIP, PSK, Enterprise Auth, MIC, 4-way Handshake)
│── Bluetooth (Briefly: Piconet, Scatternet)
├── DoS / DDoS Attacks
│   ├── Definitions (DoS vs DDoS, Botnets, C&C)
│   ├── Types
│   │   ├── Volumetric (UDP Flood, ICMP Flood, Amplification - Smurf, DNS Amp)
│   │   ├── Protocol (SYN Flood, Teardrop, Ping of Death)
│   │   └── Application Layer (HTTP Flood, Slowloris)
│   ├── Related Attacks (DNS Spoofing, Rerouting, Session Hijacking)
│   └── Mitigation (Scrubbing Centers, Rate Limiting, Firewalls, SYN Cookies, CDN, IPS)
└── Network Security Controls
    ├── Encryption
    │   ├── Link Encryption (Layer 1/2, Hop-by-hop)
    │   └── End-to-End Encryption (Layer 4/7, Source-to-Dest App)
    ├── Cryptographic Protocols
    │   ├── SSL/TLS (HTTPS, Handshake, Cipher Suites, Certificates)
    │   ├── IPSec (Layer 3, VPNs)
    │   └── SSH (Secure Remote Access)
    ├── Secure Routing / Anonymity
    │   ├── Onion Routing (Tor)
    │   └── Traffic Padding
    ├── VPNs (Secure Tunnels, Remote Access, Site-to-Site)
    ├── Firewalls
    │   ├── Types (Packet Filter, Stateful, App Proxy, Circuit, NGFW, Personal)
    │   ├── Concepts (Policy, Reference Monitor, NAT)
    │   └── Limitations
    ├── DMZ (Isolating Public Services)
    ├── IDS / IPS (Detection vs Prevention, Signature vs Anomaly, Host vs Network)
    ├── Other Tools (Honeypots, SIEM, DLP)
    ├── Web Vulnerabilities (XSS, etc.)
    └── Active Code Risks (Java, JavaScript, ActiveX)
```

---

I hope these structured notes are helpful! Let me know when you have more lecture content.