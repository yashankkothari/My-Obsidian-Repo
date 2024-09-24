## 1.1 Types of Networks: LAN, WAN, MAN. Network Topology (types)

### What is networking 
Networking is the process of connecting computers or devices using hardware and software to share resources, data, and applications. A **network** can be defined as a collection of computers or devices connected, either physically or logically, to exchange data. This can be achieved through cables, wireless connections, routers, and switches. The field of **networking** focuses on designing, implementing, and managing these networks efficiently and securely.
### Introduction to Communication System
A **communication system** refers to the process of transferring data between two or more devices through a transmission medium. It includes the following:

- **Hardware Components**:
    - **Sender**: The device or computer that initiates the data transfer.
    - **Receiver**: The device that receives the data.
    - **Intermediate Devices**: Devices such as routers and switches that help route the data.
- **Software Components**:
    - **Protocols**: A set of rules or standards that define how data is transmitted and received over the network. Protocols ensure devices communicate properly, even if they use different hardware or software architectures.
### Components of Data Communication
- **Message**: The information or data to be communicated.
- **Sender**: The device that sends the data (e.g., a computer, smartphone).
- **Receiver**: The device that receives the data.
- **Transmission Medium**: The physical path through which data is transmitted, such as cables (guided media) or airwaves (unguided media).
- **Protocols**: The rules that govern data communication, ensuring the correct format, timing, and error checking are applied.

![[{4F151582-4BA1-4AA3-AD55-18E00432C3E5}.png]]

### Elements Of Communication System
A communication system involves both **hardware** and **software** components. The diagram can be used to illustrate the relationship between sender, receiver, medium, and protocols.
![[{2B2DF307-488E-45A2-BC6C-3432A9C52043}.png]]

### Data Flow
- **Simplex**: Communication in only one direction (e.g., from a keyboard to a monitor).
- **Half-Duplex**: Communication in both directions, but not at the same time (e.g., walkie-talkies).
- **Full Duplex**: Simultaneous two-way communication (e.g., telephone conversations).

![[{31CE748B-70A8-4209-B035-C306D9D192F2}.png]]

### Network Criteria
Networks are evaluated based on:

- **Performance**:
    - **Transit Time**: The amount of time data takes to travel from one point to another.
    - **Response Time**: How quickly the system reacts to a request.
    - Performance is often measured by **throughput** (amount of data transferred) and **delay** (time taken to transfer data).
- **Reliability**:
    - Refers to how consistently a network performs without failure.
    - Measured by **frequency of failure**, **time to recover**, and **robustness** during disasters.
- **Security**:
    - Protecting data from unauthorized access and damage.
    - Involves data encryption, secure protocols, and recovery measures in case of breaches.

### Physical Structures
#### Types of Connections
- **Point-to-Point**: A direct connection between two devices, ensuring that no other device can interfere with the communication.
    - This type provides dedicated capacity, making it reliable and secure.

- **Multipoint (Multidrop)**: A single connection shared by multiple devices.
    - Can be **spatially** shared (simultaneous access) or **time-shared** (access alternates between devices).

![[{0F385EF6-F253-4DA1-8C8B-C1EB66BF2573}.png]]

### Physical Topology
**Physical Topology** refers to a way in which network is laid out physically. 
**Physical topology** describes how devices are arranged in a network and how they connect to each other.
Topology is geometric representation of relationship of all the links and linking devices (also called nodes) to one another. 

There are Four basic Topologies: 
• Mesh 
• Star 
• Bus 
• Ring

#### Mesh Topology
- **Point-to-Point Links:**  
    Every device in the network has a dedicated point-to-point link to all other devices, ensuring direct communication with no intermediate devices.
    - Each link only carries traffic between the two connected devices.
- **Redundancy & Reliability:**  
    High level of redundancy and fault tolerance as data can travel through multiple paths.
- **Number of Links:**  
    For a network with **n** devices:
    - Total physical links = **n(n - 1)**
    - For duplex communication (both directions):  
        **n(n - 1) / 2** duplex links.
- **I/O Ports:**  
    Each device must have **(n - 1)** input/output ports to connect to all other devices.

![[{232B2B90-C5EC-4732-AEB6-16447C66E324}.png]]

#####  Advantages
- **No Traffic Issues:**  
    As each link is dedicated, there are no collisions or traffic congestion.
- **Highly Robust:**  
    Multiple paths provide redundancy, ensuring that even if one link fails, data can be rerouted through others.
- **Enhanced Security & Privacy:**  
    Since links are direct, data between two devices remains private and secure.
- **Easy Fault Isolation:**  
    Each link being independent allows for easy identification and isolation of faults in the network.
##### Disadvantages
- **Complex Installation:**  
    Installing and managing the network is difficult due to the large number of interconnections.
- **High Wiring Requirements:**  
    A fully connected mesh requires extensive wiring, making physical layout cumbersome.
- **Costly Hardware:**  
    Requires many I/O ports and cables, increasing the hardware cost substantially.

#### Star Topology
- **Point-to-Point Links to Hub:**  
    Each device connects directly to a central controller, known as the **hub**. Devices are not directly linked to one another.
- **Centralized Data Exchange:**  
    The hub acts as a switch, relaying data between devices. There is no direct communication between devices.
- **Use Case:**  
    Commonly used in **Local Area Networks (LANs)** for its simplicity and centralized control.

![[{DD364968-6010-4154-9375-92E11003BB7C}.png]]

#####  Advantages
- **Cost-Effective Compared to Mesh:**  
    Requires fewer cables and connections compared to a fully connected mesh network.
- **Easy Installation and Reconfiguration:**  
    Adding or removing devices is straightforward without affecting the rest of the network.
- **Robustness:**  
    Failure of a single device does not affect the overall network, as long as the hub is functioning.
- **Simplified Fault Identification:**  
    Problems are easily isolated to a single link or device, as long as the hub is operational.

##### Disadvantages
- **Single Point of Failure:**  
    The hub is a critical component; if it fails, the entire network is down.
- **Higher Cabling Requirements (Except for Mesh):**  
    Each device requires a separate cable to the hub, leading to more cabling than bus or ring topologies, though less than a mesh network.
#### Bus Topology

- **Multipoint Connection:**  
    All devices in the network share a single communication line, known as a **bus**, which acts as the backbone.
- **Structure:**  
    Devices connect to the bus using **drop lines** (connections between devices and the main cable) and **taps** (connectors that splice or puncture the cable to access the metallic core).
- **Communication:**  
    The bus topology does not allow direct communication between devices. Data sent by one device travels through the backbone and can be accessed by all other devices, but only the intended recipient processes the data.

![[{0971D5EA-5C99-4BB4-81B4-B2139BDD97C3}.png]]
#####  Advantages
- **Ease of Installation:**  
    Less cabling is required compared to **mesh** and **star** topologies, which simplifies setup.
- **Cost-Efficient:**  
    It uses fewer cables and connectors than mesh or star, making it an economical choice.
##### Disadvantages
- **Difficult to Add New Devices:**  
    Adding more devices to the network can disturb the system and requires halting the transmission.
- **Challenging Reconfiguration and Fault Isolation:**  
    Troubleshooting issues in the network can be complex, as it is hard to isolate faults in a shared backbone.
- **Single Point of Failure:**  
    A fault in the backbone cable halts all network communication, making it a vulnerable point.
- **Limited Cable Length and Number of Nodes:**  
    Bus topology can only support a limited number of devices and cable length, making it unsuitable for larger networks.

#### Ring Topology
- **Point-to-Point Connections:**  
    Each device has a direct point-to-point connection with two neighboring devices—one on either side.
- **Data Transmission:** 
    Data moves in one direction (unidirectional) around the ring. A signal passes from one device to the next until it reaches its destination.
- **Repeaters in Devices:**  
    Every device in the ring includes a repeater to regenerate signals, ensuring data can travel over longer distances without degradation.
\
![[{C0351689-9235-4E2D-9673-60344CF8AEE1}.png]]
#####  Advantages
- **Easy Installation and Reconfiguration:**  
    Simple to set up and modify as devices are added or removed from the ring.
- **Effortless Addition and Deletion of Devices:**  
    Devices can be added or removed without disrupting the entire network.
- **Simplified Fault Isolation:**  
    If a device encounters an issue, it can send an alert to notify the network, making it easier to identify and fix problems.

##### Disadvantages
- **Unidirectional Traffic:**  
    Data can only travel in one direction, which can delay transmission if the destination is located on the opposite side of the ring.
- **Single Point of Failure:**  
    A failure in any part of the ring can bring down the entire network unless a dual-ring system or redundant links are used.

### Types of Networks

• Local Area Network (LAN) 
• Metropolitan Area Network(MAN) 
• Wide Area Network(WAN)

####  Local Area Network (LAN) 
- **Definition:**  
    A LAN is a computer network that spans a relatively small geographic area, typically within a single building, office, or campus.
- **Ownership:**  
    Usually privately owned, allowing for greater control over network resources.
- **Coverage:**  
    LANs typically cover distances from **10 meters to 1 kilometer** and are limited to a few kilometers in size.
- **Resource Sharing:**  
    Designed to facilitate sharing of resources such as hardware (printers, servers) and software among personal computers or workstations.
- **Server-Client Model:**  
    One or more computers may function as servers, providing resources (e.g., file storage) to client devices.
- **Transmission Media and Topology:**  
    LANs are characterized by specific transmission media (like Ethernet cables) and network topologies (like star, bus, or ring).
- **Speed:**  
    Commonly operates at speeds of **100 Mbps** or **1 Gbps**.

####  Metropolitan Area Networks(YA MAN)
- **Definition:**  
    A MAN is designed to cover a larger geographic area than a LAN, typically spanning a town or city.
- **Purpose:**  
    It provides high-speed connectivity for customers, often connecting various LANs and providing access to the Internet.
- **Coverage:**  
    MANs can extend up to **30-40 kilometers**.
- **Example:**  
    Commonly used for services like cable TV networks and municipal wireless networks.
- **Speed:**  
    Operates at speeds ranging from **34 Mbps to 155 Mbps**.
- **Media Types:**  
    MANs can utilize both guided media (like fiber optics) and unguided media (like wireless connections).

![[Pasted image 20240923181738.png]]

####  Wide Area Networks

- **Definition:**  
    A WAN provides long-distance transmission of data, images, audio, and video across large geographic areas, which can span countries, continents, or even the entire globe.
- **Geographical Independence:**  
    Unlike LANs and MANs, WANs connect computers and network devices without being limited by geographical boundaries.
- **Example:**  
    The **Internet** is the most prominent example of a WAN.
- **Connectivity:**  
    WANs connect multiple LANs, enabling communication and resource sharing across different locations.
- **Speed Variability:**  
    WAN speeds can vary significantly based on the geographical location of servers and the type of connection used. Typical connection speeds can range from **10 Mbps** to **100 Mbps**.
- **Transmission Media:**  
    WANs primarily utilize both guided media (such as fiber optics and leased lines) and unguided media (such as satellite and wireless communication).

![[Pasted image 20240923182006.png]]

###  Switching
- **Definition:**  
    An internet is a switched network where a switch connects at least two links together, facilitating communication between devices.

- **Types of Switched Networks:**  
    The two most common types of switched networks are:
    1. **Circuit-Switched Network**
        - **Definition:** Establishes a dedicated communication path between two devices for the duration of the connection.
        - **Characteristics:**
            - Resources are reserved for the entire call duration.
            - Suitable for applications requiring continuous transmission, such as voice calls.
            - Example: Traditional telephone networks.
    2. **Packet-Switched Network**
        - **Definition:** Divides data into packets that are sent independently over the network and reassembled at the destination.
        - **Characteristics:**
            - More efficient use of network resources as multiple packets from different sources can share the same path.
            - Suitable for applications that can tolerate delays, such as email and web browsing.
            - Example: The Internet.

![[{7C5AFFFC-1FCF-48BF-950F-E3329D9B8138}.png]]


## 1.2 Network Software: Protocol hierarchy, Design Issues for layers, Connection oriented and connectionless services, Reliable and Un-reliable services

###  Network Models
Network Models Protocol Layering: 
- **ISO OSI Model**
- **TCP/IP Model**
###  Design Issues for Layers
- **Addressing:**  
    How do we identify senders and receivers? This involves assigning unique identifiers to ensure communication between specific devices.
- **Rules for Data Transfer:**
    - **Simplex:** One-way communication (e.g., keyboard to computer).
    - **Half-Duplex:** Two-way communication, but not simultaneously (e.g., walkie-talkies).
    - **Full Duplex:** Simultaneous two-way communication (e.g., phone calls).
- **Logical Channels:**  
    Typically, there are at least two channels: one for regular communication and another for urgent messages.
- **Reconstituting Messages:**  
    Out-of-order messages must be numbered for proper sequencing (flow control).
- **Error Control:**  
    Addresses communication over imperfect channels, focusing on error detection and correction. Common issues include:
    - **Attenuation:** Signal loss over distance.
    - **Delay Distortion:** Variability in signal transmission time.
    - **Noise:** Interference that affects data integrity.
- **Large Messages:**  
    Procedures for disassembling, transmitting, and reassembling messages. Special handling may be required for very small messages compared to packets.
- **Multiplexing:**  
    Managing multiple connections over a single physical line. Essential in the physical layer, where limited lines are available.
- **Routing:**  
    Determining the best path for data when multiple routes exist between communicating devices.
###  Connection Less Services
- **Definition:**  
    No established session connection between sender and receiver.
- **Characteristics:**
    - No reliability guarantees.
    - Suitable for short messages.
    - Does not maintain state information.
    - Lower overhead, making it more efficient.
    - **Example:** Walkie-talkie communication.

###  Connection Oriented Services
- **Definition:**  
    Requires an established session connection, similar to a phone call.
- **Characteristics:**
    - Provides a reliable network service.
    - Sets up virtual links between end systems.
    - Suitable for longer messages.
    - Higher overhead, placing greater demands on bandwidth.
    - **Example:** Email communication.
## 1.3  OSI and TCP/IP reference model, Comparison of OSI and TCP/IP reference model

###  The OSI model
- **Background:**  
    In recent decades, many networks were built using various hardware and software implementations, leading to incompatibility issues. This made communication between networks using different specifications challenging.
- **Definition:**  
    The **Open Systems Interconnection (OSI)** model is a conceptual framework that standardizes how data communications should occur, enabling any two systems to communicate regardless of their architecture.
- **Purpose:**  
    The OSI model serves as a framework for designing network systems, ensuring interoperability between different network technologies.
- **Structure:**  
    The OSI model divides the communication process into **seven layers**, each with specific functions and responsibilities. These layers are:
    1. **Physical Layer:** Deals with the physical connection between devices.
    2. **Data Link Layer:** Handles error detection and correction, and manages node-to-node data transfer.
    3. **Network Layer:** Manages routing and forwarding of data packets across the network.
    4. **Transport Layer:** Ensures complete data transfer, managing flow control and error correction.
    5. **Session Layer:** Establishes, manages, and terminates sessions between applications.
    6. **Presentation Layer:** Translates data between the application and the network, including encryption and compression.
    7. **Application Layer:** Provides network services directly to end-user applications

![[{D5DD55E0-2A9B-4EE7-8A7F-DA63060CAD3B}.png|400]]

#### Physical Layer
- **Definition:**  
    The physical layer is responsible for the physical characteristics of the transmission medium, including the hardware used to transmit data over a network.
- **Components:**  
    This layer consists of the actual physical media (wires, cables, or wireless signals) through which network signals are conducted. It defines connector and interface specifications, as well as the requirements for the medium (cable) to facilitate transmission.

![[{DC5F37E3-B254-45D6-BDFA-9DE56300D0EA}.png]]
##### Functions of the Physical Layer
1. **Physical Characteristics of Interfaces and Medium:**  
    Defines the properties of the hardware, including electrical, mechanical, and procedural standards for network connections.
2. **Representation of Bits:**  
    Converts binary data into electrical or optical signals for transmission.
3. **Data Rate:**  
    Specifies the speed of data transmission over the physical medium, usually measured in bits per second (bps).
4. **Synchronization of Bits:**  
    Ensures that the sender and receiver are synchronized, allowing for accurate data interpretation.
5. **Physical Topology:**  
    Describes the layout of the network, including how devices are interconnected (e.g., star, bus, ring).
6. **Line Configuration:**  
    Defines how devices are connected, whether in a point-to-point configuration (direct connection between two devices) or multipoint configuration (multiple devices connected to a single communication line).

#### Data Link Layer
- **Definition:**  
    The data link layer transforms the physical layer's raw transmission facility into a reliable link, ensuring effective communication between nodes.
- **Delivery Method:**  
    Focuses on **node-to-node delivery** (also known as hop-to-hop delivery), ensuring data is accurately transmitted from one node to the next.
- **Addressing:**  
    Utilizes the **MAC address** (Media Access Control address) to uniquely identify each device on the network, allowing multiple stations to share the same medium while maintaining distinct identities.
- **Responsibilities:**  
    The data link layer is concerned with various aspects, including:
    - Network topology
    - Network access
    - Error notification
    - Ordered delivery of frames
    - Flow control

![[{9A6320FA-ABA5-418A-BF04-86C93D5055AC}.png]]
##### Functions of Data Link layer: 
- **Framing:**  
    Encapsulates data into frames, adding headers and footers that define the start and end of each frame.
- **Physical Addressing:**  
    Adds a header to each frame containing the source and destination MAC addresses, facilitating proper delivery.
- **Flow Control:**  
    Manages data transmission rates between sender and receiver to prevent overwhelming the receiving device.
- **Error Control:**  
    Detects and corrects errors that may occur during data transmission, ensuring reliable communication.
- **Access Control:**  
    Determines how devices on the network gain access to the shared medium, coordinating transmission to avoid collisions.

##### Hop-to-Hop Delivery
![[Pasted image 20240923200108.png]]


#### Network Layer
- **Definition:**  
    The network layer is responsible for establishing the route between sending and receiving stations, ensuring that data packets are delivered from the source to the destination.
- **Packet Delivery:**  
    It handles the delivery of individual packets. If two systems are connected on the same link, the network layer is not required; however, it becomes essential when two systems are on different links.
- **Routing Responsibilities:**  
    The network layer manages the routing of data by directing outgoing transmissions to the correct destination and receiving incoming transmissions. This layer performs both routing and forwarding of data packets.
- **Addressing:**  
    Network layer addresses are often referred to as **logical addresses**, differentiating them from the physical addresses used in the data link layer.

![[{8FA893A3-EF09-43AB-B83B-6E30E85419AE}.png]]

##### Functions of Network Layer: 
- **Logical Addressing:**
    - **Data Link Layer Addressing:** Handles physical addressing locally within a single network.
    - **Network Layer Addressing:** Uses IP addressing for packets that cross network boundaries, ensuring they can reach their intended destinations.
- **Routing:**
    - Determines the best path for routing packets to their destination through connecting devices across large networks.
    - Involves protocols and algorithms to optimize the data flow and manage network traffic.

![[Pasted image 20240923200356.png]]

##### Source-to-destination delivery
![[{0184F53B-B15F-4AEF-8E9F-BD851434C45C}.png]]

#### Transport Layer
- **Definition:**  
    The transport layer is responsible for delivering messages from one process to another, ensuring that data is transmitted reliably and in the correct order.
- **Message Integrity:**  
    It recognizes the relationship between packets and ensures that the entire message arrives intact and sequenced correctly.
- **Data Segmentation:**  
    This layer constructs a stream of data segments, sends them, and checks for correct delivery. If data is transmitted incorrectly, it requests retransmission.
- **Interface Role:**  
    The transport layer serves as an interface between the lower layers (physical, data link, and network) and the upper layers (session, presentation, and application).
    
##### Responsibilities of the Transport Layer

1. **Service-Point Addressing:**
    - Utilizes **port addressing** to identify specific processes on the destination computer.
    - The network layer ensures that packets reach the correct computer, while the transport layer ensures they reach the correct process on that computer.
2. **Segmentation and Reassembly:**
    - Divides messages into smaller segments, assigning sequence numbers for proper reassembly at the destination.
3. **Retransmission:**
    - Responsible for requesting the retransmission of lost segments, ensuring complete data delivery.
4. **Connection Control:**
    - Supports both **connection-oriented** (establishing a connection before data transfer) and **connectionless** (data sent without establishing a connection) services.
5. **Flow Control:**
    - Manages flow control end-to-end, ensuring that the sender does not overwhelm the receiver, rather than controlling flow across a single link.
6. **Error Control:**
    - Implements error control at a process-to-process level, detecting and correcting errors that may occur during transmission.

![[{A708E6AF-AD43-4435-828E-A1B7B169BCB1}.png]]

##### Reliable process-to-process delivery of a message
![[{8DBA7080-5A09-46CF-AF33-1B955B0A645C}.png]]

#### Session Layer
- **Definition:**  
    The session layer provides services beyond those offered by the first three layers (physical, data link, and network). It defines how to start, control, and end conversations (sessions) between applications.
- **Functionality:**  
    This layer coordinates communication in an orderly manner, facilitating efficient data transfer during active sessions.

![[{66E46A8E-DB7F-45B2-BF13-28F897F51881}.png]]
##### Responsibilities of the Session Layer
1. **Dialog Control:**
    - Manages the dialog between two systems, allowing them to establish a communication session.
2. **Synchronization:**
    - Provides mechanisms for adding checkpoints in long data transfers, enabling the recovery of sessions in case of interruptions.

#### Presentation Layer
- **Definition:**  
    The presentation layer ensures that data sent from the application layer of one system is readable by the application layer of another system. It translates between multiple data formats when necessary.
- **Functionality:**  
    This layer enables applications to read and understand messages by providing a common data format.

![[{53B2EFA3-7E35-47B0-B6FB-9D41897B8FD5}.png]]
##### Responsibilities of presentation layer: 
- **Translation:**
    - Converts data into a format that can be understood by the receiving system.
- **Compression:**
    - Reduces the size of data to facilitate faster transmission without sacrificing quality.
- **Encryption:**
    - Encodes data to protect it from interception and unauthorized access.

#### Application Layer
- **Definition:**  
    The application layer enables users—whether human or software—to access network services. It provides user interfaces and supports various applications, such as email, shared databases, and remote file access.
- **Unique Role:**  
    Unlike other OSI layers, the application layer does not provide services to any other layer but exclusively to applications outside the OSI model.

![[{5ADE068A-5A3B-46E9-B89E-56B6DBAC18CE}.png]]

#### Summary of Layer Functions
![[{868B1FF0-DF81-4154-9047-F9A852514C1B}.png]]


#### TCP/IP Model
- **Background:**  
    The TCP/IP model was developed prior to the OSI model and serves as the foundational protocol for the internet.
- **Structure:**  
    The TCP/IP model is a hierarchical protocol consisting of interactive modules, each designed to provide specific functionality. Importantly, these modules are not interdependent, allowing flexibility and robustness.

#### TCP/IP PROTOCOL SUITE
The TCP/IP protocol suite is organized into **five layers**, each responsible for different aspects of network communication. These layers are:

1. **Application Layer:**
    - Provides network services directly to applications, facilitating user interface and communication for software applications.
2. **Transport Layer:**
    - Ensures reliable data transmission between systems, managing segmentation, flow control, and error correction.
3. **Internet Layer:**
    - Responsible for logical addressing and routing of packets across networks, enabling communication between devices on different networks.
4. **Link Layer (or Network Interface Layer):**
    - Handles physical addressing and the protocols required to transmit data over specific types of physical media, ensuring reliable transmission over the local network.
5. **Physical Layer:**
    - While not always explicitly defined in the TCP/IP model, this layer encompasses the actual physical transmission of data over cables or wireless media.

![[{47E45E49-BABB-47AE-B786-DDD04175A910}.png]]

![[{AB084EE0-663E-4E1E-8113-0129C92931A7}.png]]

##### Network Layer
- **General Overview:**  
    The TCP/IP model does not mandate any specific protocol at the network layer; rather, it supports a variety of standard and proprietary protocols.

IP in turn uses **4 supporting protocols.** 
▪ ARP 
▪ RARP 
▪ ICMP
▪ IGMP

- **Internetworking Protocol (IP):**
    - **Function:** IP is the primary transmission mechanism used by TCP/IP.
    - **Characteristics:**
        - It is an unreliable and connectionless protocol, providing best-effort delivery.
        - There is no error checking or tracking of packets.
        - Data is transported in units called **datagrams**.
        - IP does not maintain route information or facilitate reordering of packets.

###### Supporting Protocols for IP

At the network layer, TCP/IP supports four key protocols:

1. **Address Resolution Protocol (ARP):**
    - **Purpose:** Associates a logical IP address with a physical MAC address.
    - **Functionality:** ARP is used to determine the physical address of a node when its logical address is known.
2. **Reverse Address Resolution Protocol (RARP):**
    - **Purpose:** Determines the logical address of a node when its physical address is known.
    - **Use Case:** Typically employed when a device connects to the network for the first time.
3. **Internet Control Message Protocol (ICMP):**
    - **Purpose:** Allows hosts and gateways to send notifications regarding issues with datagram delivery to the sender.
    - **Functionality:** ICMP is crucial for error reporting and network diagnostics.
4. **Internet Group Management Protocol (IGMP):**
    - **Purpose:** Facilitates the simultaneous transmission of messages to a group of recipients.
    - **Functionality:** IGMP is essential for managing multicast group memberships.

##### Transport Layer
Transport layer has three protocols: 
• **UDP** (User Datagram Protocol) 
• **TCP** (Transmission Control Protocol) 
• **SCTP** (Stream Control Transmission Protocol)

**User Datagram Protocol (UDP):**
- **Functionality:** Provides a process-to-process communication model.
- **Characteristics:**
    - Adds minimal overhead by including only the port address, error control, checksum, and other relevant information to the data from the upper layers.
    - It is connectionless and does not guarantee reliable delivery or ordering of packets.

- **Transmission Control Protocol (TCP):**
    - **Functionality:** Provides a reliable stream-oriented communication protocol.
    - **Characteristics:**
        - Divides data into smaller segments for transmission.
        - Each segment contains a sequence number, which is essential for reordering at the receiving end.
        - At the destination, TCP collects the segments and reorders them based on their sequence numbers to ensure complete and accurate data delivery.

- **Stream Control Transmission Protocol (SCTP):**
    - **Functionality:** Combines features of both TCP and UDP.
    - **Characteristics:**
        - Supports message-oriented communication similar to UDP.
        - Provides reliable, ordered delivery of messages like TCP, with additional features such as multi-homing and multi-streaming, allowing for improved performance and reliability in certain applications.

#### Addressing

In a TCP/IP network, four distinct levels of addresses are utilized:

1. **Physical Address:**
    - **Definition:** The hardware address assigned to a network interface card (NIC).
    - **Example:** Media Access Control (MAC) address.
    - **Function:** Used for communication within the same local area network (LAN), facilitating data transmission between devices on the same network segment.

2. **Logical Address:**
    - **Definition:** An address assigned at the network layer, commonly known as an IP address.
    - **Function:** Identifies devices across different networks, enabling routing of packets from the source to the destination over the internet.

3. **Port Address:**
    - **Definition:** An address used to identify specific processes or services running on a device.
    - **Example:** Port numbers (e.g., HTTP typically uses port 80, HTTPS uses port 443).
    - **Function:** Allows multiple applications to use the network simultaneously by directing traffic to the appropriate application on the host.

4. **Specific Address:**
    - **Definition:** A more granular address that may refer to a specific service or endpoint within an application.
    - **Function:** Can include detailed information required for complex applications, facilitating direct communication with specific components of a service.

![[{888415FC-3879-4DF5-9DA2-253E334A3947}.png]]

##### Mac Address
![[Pasted image 20240923203628.png]]
![[Pasted image 20240923203648.png]]
![[Pasted image 20240923203658.png]]

##### IP Address
![[Pasted image 20240923203744.png]]

##### Addresses (Example)
![[{DAC75314-286C-4621-B6F8-89B782CA97D8}.png]]


## 1.4 Overview of connecting devices, NIC, Repeater, Hub, Bridge, Router, Gateway

### Network Interface Card (NIC)
- **Definition:** A hardware component that allows a device to connect to a network.
    - **Function:** Converts data into a format suitable for transmission over a network medium (wired or wireless).
    - **Characteristics:** Each NIC has a unique MAC address for identification on the local network.

![[Pasted image 20240923204017.png|500]]


### 2. Repeater:
- **Definition:** A device that regenerates and amplifies signals to extend the distance of transmission.
- **Function:** Receives a weak or corrupted signal, cleans it up, and retransmits it, thus overcoming distance limitations.
- **Use Case:** Commonly used in long-distance communication scenarios where signals may degrade over distance.

![[Pasted image 20240923205025.png]]

### 3. Hub:
- **Definition:** A basic networking device that connects multiple Ethernet devices, making them act as a single network segment.
- **Function:** Forwards data packets to all connected devices without filtering, leading to potential collisions.
- **Characteristics:** Operates at the physical layer and is generally less intelligent than switches.

![[Pasted image 20240923205055.png]]

### 4. Bridge:
- **Definition:** A device that connects two or more network segments and filters traffic based on MAC addresses.
- **Function:** Reduces network traffic by dividing collision domains, improving overall performance.
- **Characteristics:** Operates at the data link layer and can learn which devices are on which segments to forward traffic selectively.
![[Pasted image 20240923205116.png]]


### 5. Router:
- **Definition:** A device that connects different networks and routes data packets between them.
- **Function:** Uses IP addresses to determine the best path for data to travel across networks, enabling communication between disparate networks (e.g., local and wide area networks).
- **Characteristics:** Operates at the network layer and can perform complex routing decisions and traffic management.
![[Pasted image 20240923205327.png]]
### 6. Gateway:
- **Definition:** A device that acts as a "gate" between two networks, often with different protocols.
- **Function:** Translates communication between different network architectures or data formats, enabling interoperability.
- **Use Case:** Commonly used in connecting a local network to the internet or integrating different types of networks (e.g., TCP/IP and IPX).
![[Pasted image 20240923205433.png]]

# Made By Yashank 