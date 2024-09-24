## 2.1 Error Control: Types of Errors; Redundancy, Checksum, Hamming Code and CRC.

Error Correction & Detection 
▪Types of Errors 
▪ Redundancy 
▪ Detection Versus Correction 
▪ Forward Error Correction Versus Retransmission 
▪ Coding

### Types of Errors
- **Interference:** External factors can alter the shape of the signal during transmission, leading to potential data corruption.
- **Single Bit Error:**
    - **Definition:** Occurs when a single bit in a data unit (such as a byte, character, or packet) is flipped from 0 to 1 or from 1 to 0.
    - **Example:** If the original byte is `10101100`, a single bit error might change it to `10111100`.

![[{F522E628-3E0E-41A2-BE69-3636AF604738}.png]]

- **Burst Error:**
    - **Definition:** Involves two or more bits being altered in a data unit, changing from 1 to 0 or from 0 to 1.
    - **Characteristics:** Burst errors do not necessarily affect consecutive bits; the length of a burst error is defined as the distance from the first corrupted bit to the last corrupted bit.
    - **Example:** If the original byte is `10101100` and a burst error changes bits 3 to 5, it might change to `10110010`.

![[{F279F957-E673-40A3-A1D3-4B6B0012E5FB}.png]]

### Redundancy

- **Definition:** A central concept in error detection and correction, redundancy involves the addition of extra bits to transmitted data.
- **Purpose:** Redundant bits enable the detection and correction of errors during data transmission.
- **Process:**
    - **Sender's Role:** The sender appends redundant bits to the original data before transmission.
    - **Receiver's Role:** The receiver removes these redundant bits to retrieve the original message and checks for errors.

### Detection Versus Correction

- **Error Detection:**
    - **Definition:** The process of identifying whether any errors have occurred in the transmitted data.
    - **Outcome:** Provides a simple yes or no answer regarding the presence of errors.

- **Error Correction:**
    - **Definition:** A more complex process that not only identifies errors but also determines the exact number of corrupted bits and their specific locations in the message.
    - **Challenge:** Requires more sophisticated algorithms and additional redundancy compared to error detection.

### Forward Error Correction Versus Retransmission
- **Overview:** There are two main methods of error correction:
    - **Forward Error Correction (FEC)**
    - **Retransmission**

- **Forward Error Correction (FEC):**
    - **Definition:** A process where the receiver attempts to reconstruct the original message using the redundant bits included with the data.
    - **Mechanism:** The receiver applies algorithms to deduce the correct data even if some bits have been altered, allowing for error correction without needing a resend.

- **Retransmission:**
    - **Definition:** A technique in which the receiver identifies the presence of an error and requests the sender to resend the original message.
    - **Process:** This method ensures accuracy by relying on feedback from the receiver, which can lead to increased latency due to the need for resending data.

### Coding
- **Definition of Redundancy:**  
    Redundancy is achieved through various coding schemes that add extra bits to the data being transmitted.

- **Process of Redundancy:**
    - **Sender's Role:** The sender incorporates redundant bits in a way that establishes a relationship between these bits and the actual data bits. This relationship is crucial for detecting and correcting errors.
    - **Receiver's Role:** The receiver checks the relationships between the redundant bits and the original data bits to identify and correct any errors that may have occurred during transmission.

- **Categories of Coding Schemes:**
    - **Block Coding:**  
        A method that divides the data into fixed-size blocks, each augmented with redundant bits to facilitate error detection and correction.
    - **Convolutional Coding:**  
        A technique that encodes the data as a continuous stream, where the encoding of each bit depends on previous bits, providing a more flexible approach to error correction.

![[{021A3448-3B35-47DA-85A1-004040C991CC}.png]]

#### Block Coding
- **Definition:** In block coding, a message is divided into fixed-size blocks for error detection and correction.
- **Process:**
    - **Division into Blocks:** The message is split into blocks, each consisting of **k bits** known as **datawords**.
    - **Adding Redundancy:** To each dataword, **r redundant bits** are added, resulting in a total block length of **n = k + r**.
    - **Resulting Codewords:** The n-bit blocks formed after adding the redundant bits are referred to as **codewords**.
- **Purpose:** This method allows for error detection and correction by establishing a relationship between the data words and the codewords, facilitating the identification of errors during transmission.
![[{E51CDFCF-48B9-49EC-B8E7-A3A78B5D894B}.png]]

##### Example 1
- **Assumption:** Let k=2 and n=3. The table below illustrates the relationship between datawords and codewords.

- **Encoding Process:**
    - Assume the sender encodes the dataword **01** as **011** and sends it to the receiver.
- **Cases of Received Codewords:**
    1. **Received Codeword: 011**
        - **Validity:** This is a valid codeword.
        - **Action:** The receiver successfully extracts the dataword **01**.
    2. **Received Codeword: 111**
        - **Validity:** This is not a valid codeword.
        - **Action:** The codeword is discarded by the receiver.
    3. **Received Codeword: 000**
        - **Validity:** This is a valid codeword.
        - **Action:** The receiver incorrectly extracts the dataword **00**. This scenario demonstrates that two corrupted bits made the error undetectable.

![[{860809AF-1914-4870-B2A3-427165112EBF}.png]]

### Error Correction
- **Complexity of Correction:**  
    Error correction is significantly more challenging than error detection.
- **Redundancy Requirement:**
    - More redundant bits are needed for error correction compared to error detection. This is because correcting errors requires additional information to pinpoint and fix the errors.
- **Checker Functions:**
    - While the underlying concept of using redundancy is similar to error detection, the functions involved in error correction are much more complex. These functions must not only detect errors but also identify the specific bits that are corrupted and determine how to correct them.

![[{20B2ABC8-C622-4BD0-B12E-3C7C1FCF4D40}.png]]

### Hamming Distance
- **Definition:**  
    One of the central concepts in coding for error control is **Hamming Distance**. It measures the number of differences between two words of the same size.
- **Calculation:**  
    The Hamming distance between two words xxx and yyy is represented as d(x,y)d(x, y)d(x,y) and is calculated using the XOR operation on corresponding bits. Each differing bit contributes to the distance.

- **Examples:**
    1. **For the words 000 and 011:**
        - **Calculation:**  
            d(000,011)=2 because the bits differ in two positions (second and third bits).
            ![[{8E01023B-8460-4CFB-8328-83B2D718D615}.png]]
    1. **For the words 10101 and 11110:**
        - **Calculation:**  
            d(10101,11110)=3 because the bits differ in three positions (first, second, and fourth bits).
            ![[{6E75BB9B-4731-42BB-A40A-FBEE2B9ED561}.png]]

#### Minimum Hamming Distance
- **Definition:**  
    The **minimum Hamming distance** is a critical measurement used in designing a code. It is defined as the smallest Hamming distance between all possible pairs in a set of codewords.
- **Notation:**  
    The minimum Hamming distance is denoted as dmin​ and plays a key role in determining the error-detecting and error-correcting capabilities of a coding scheme.

![[{25508055-3C4F-42ED-9954-50332B85C8EA}.png]]
![[{E5136291-715E-4BFD-861B-9D0220BF220A}.png]]

#### Minimum Hamming  Distance for Error Detection
- To ensure the detection of up to *s* errors in all cases, the minimum Hamming distance in a block code must satisfy the condition: dmin=s+1

![[{638B0C20-5071-4FF6-BDC4-7572BB14FE87}.png]]

- This means that for a code to reliably detect ~~s~~ errors, the minimum distance between any two valid codewords must be at least s+1.

#### Minimum Hamming Distance for Error Correction
- To guarantee the correction of up to t errors in all cases, the minimum Hamming distance in a block code must meet the requirement: dmin=2t+1

![[{A79C49F2-014B-4B2E-B49E-97C71F43B519}.png]]

-  This indicates that for a code to reliably correct *t* errors, the minimum distance between any two valid codewords must be at least 2t+1

![[{F5C3BFD8-9972-49F0-82A1-9E24FF14A5B8}.png]]

### Linear Block Codes
**Definition:** A linear block code is a coding scheme where the XOR of two valid codewords results in another valid codeword.

**Minimum Distance for Linear Block Codes:** 
- **Minimum Hamming Distance:** The number of **1s** in the nonzero valid codeword with the smallest number of **1s**.
- **Importance:**
    - **Error Detection:** dmin=s+1 for detecting up to **s** errors.
    - **Error Correction:** dmin=2t+1 for correcting up to **t** errors.

#### Some Linear Block Codes

1. Simple Parity-Check Code 
2. Hamming Codes 

##### 1. Simple Parity-Check Code
- **Definition:** A k-bit dataword is changed to an n-bit codeword where n=k+1n = k + 1n=k+1.
- **Parity Bit:** Added to ensure the total number of **1s** is even or odd.
- **Minimum Hamming Distance:** dmin=2 detects single-bit errors but cannot correct any.
![[{E4233E48-59CE-443D-A321-3D0F6F437475}.png]]

Assume the sender sends the dataword 1011. The codeword created from this dataword is 10111, which is sent to the receiver. We examine five cases: 
**Assumed Dataword:** 1011  
**Codeword Sent:** 10111
###### Cases:

1. **No Error:**
    - Received: 10111
    - Syndrome: 0
    - Dataword: 1011 created.
2. **Single-Bit Error (a1 changes):**
    - Received: 10011
    - Syndrome: 1
    - Dataword: Not created.
3. **Single-Bit Error (r0 changes):**
    - Received: 10110
    - Syndrome: 1
    - Dataword: Not created.
4. **Two Errors (r0 and a3 change):**
    - Received: 00110
    - Syndrome: 0
    - Dataword: 0011 created.
    - **Note:** Errors cancel out; even errors are undetected.
5. **Three Errors (a3, a2, a1 change):**
    - Received: 01011
    - Syndrome: 1
    - Dataword: Not created.

1. **Observation:** A parity-check code can detect an odd number of errors.

##### 2. Hamming Codes
- **Definition:** A set of error-correcting codes that can detect and correct errors in data transmission.
- **Minimum Hamming Distance:** Typically dmin=3 allows detection of up to 2 errors and correction of 1 error.
- **Structure:** Adds redundancy through multiple parity bits, ensuring reliable data integrity.

![[{895C50E8-8DDD-4F68-BAC8-2EE3834DE5BB}.png]]
![[{C9F614DA-8379-4B5E-9CF7-88D6E2870DAD}.png]]


### Cyclic Codes
- **Definition:** Cyclic codes are a type of linear block code where any cyclic shift (rotation) of a codeword results in another valid codeword.

- **Cyclic Redundancy Check (CRC):**
    - A specific subset of cyclic codes.
    - Primarily used for error detection.
    - Commonly implemented in networks such as LANs and WANs.

![[{E0DCC62B-9EFF-4A23-89CB-8EE1CD937591}.png]]
![[{E23441D1-5454-4A99-9D9C-690DC5D7AE20}.png]]
![[{F1027509-3C1D-4EF8-BA68-4F9B1BDB0637}.png]]
![[{93934000-0455-4F54-B654-CC62AD3CAF4A}.png]]
![[{F94DF35D-BB49-4D61-B4BC-0E70DE6CFD0F}.png]]

### Checksum
- **16-bit Checksum:** Traditionally, the Internet uses a 16-bit checksum for error detection.

- **Process Steps:**
    - The sender calculates the checksum by summing 16-bit words and taking the one's complement of the sum.
    - The calculated checksum is appended to the data packet.
    - Upon receipt, the receiver computes the checksum again and compares it with the received checksum.
    - If the two checksums match, the data is considered intact; if not, an error is detected.

![[{CD44EE5F-A39B-42C0-B006-51474769DED3}.png]]

### Data Link Layer
Data Link Layer is Divided into two sub layers:
![[{EB7D597F-B250-4634-A848-DA3F2237977B}.png]]


- **Logical Link Control (LLC Sublayer):**
    - Manages frame synchronization, flow control, and error checking.
- **Media Access Control (MAC Sublayer):**
    - Responsible for transferring data packets between interfaces over a shared communication channel.


## 2.2 Framing, and Flow Control; Flow control Protocols: Stop-and-wait, Go-Back-N, Selective-Repeat, Piggybacking

### Framing
- **Purpose of Framing:**
    - To pack bits into distinguishable frames, similar to how a postal system uses envelopes as delimiters.
- **Types of Framing:**
    - **Fixed Size Framing:**
        - Each frame has a predetermined size, making the size itself act as a delimiter.
    - **Variable Size Framing:**
        - Requires a method to define the start and end of frames.
        - **Character (Byte) Oriented Framing:**
            - Uses special characters to indicate the beginning and end of a frame.
        - **Bit Oriented Framing:**
            - Uses specific bit patterns to identify frame boundaries.

#### Character Oriented Framing

- **Data Structure:**
    - Data to be carried consists of 8-bit characters.
    - Headers and trailers are also multiples of 8 bits.
- **Frame Delimiters:**
    - A flag is added at the beginning and end of each frame to separate them.
![[{EB90D331-1361-4025-8373-B95A18A66156}.png]]
##### Byte Stuffing and Unstuffing
- **Byte Stuffing:**
    - A technique where an extra byte is added whenever a flag or escape character appears in the text to avoid confusion.
![[{EA82367D-5AB9-4713-9A49-CDCB23B03378}.png]]

• In bit stuffing, if a 0 and five consecutive 1 bits are encountered, an extra 0 is added. 
• This extra stuffed bit is eventually removed from the data by the receiver.

![[{2775CA1C-10F4-48C8-A2A2-5C3BE587589B}.png]]



#### Bit-Oriented Framing
In Bit-oriented Framing, a special 8-bit pattern flag, 01111110, is used as the delimiter to define the beginning and the end of the frame.
![[{AAC75D6E-1BD5-4867-A0B5-222C17381E3D}.png]]

### Flow Control and Error Control
One of the responsibilities of the data link control sublayer is flow and error control at the data-link layer. Collectively, these functions are known as data link control. waiting for acknowledgment.

![[{53F21CD8-69B0-4B3B-909B-23681F20953D}.png]]
#### Flow Control:

- **Definition:** Flow control is a set of procedures designed to manage the rate of data transmission between a sender and a receiver. Its primary goal is to prevent the sender from overwhelming the receiver with too much data too quickly.
- **Importance:**
    - **Receiver Limitations:** The receiving device may have limited processing speed and memory capacity. If the sender transmits data faster than the receiver can process it, data can be lost or corrupted.
    - **Acknowledgment Process:** Flow control ensures that the sender waits for an acknowledgment from the receiver before sending additional data. This acknowledgment confirms that the previously sent data has been successfully received and processed.
    - 
![[{802D2537-8787-46E3-82CB-5C315C37C87C}.png]]
#### Error Control:

- **Purpose:** Error control is critical for maintaining data integrity during transmission. It involves mechanisms to detect and correct errors that may occur due to noise, interference, or other transmission issues.
- **Methodology:**
    - **Automatic Repeat reQuest (ARQ):** This is a common error control technique where the receiver checks for errors and, if any are detected, requests the sender to retransmit the affected data. This process ensures that only correctly received data is processed, thereby enhancing reliability.
![[{38C7F7F2-31BA-4A07-9CCB-20BD03952CCB}.png]]


Together, flow control and error control are essential functions of the data link layer, ensuring efficient and reliable communication between devices.

#### Noiseless Channel
Let us first assume we have an ideal channel in which no frames are lost, duplicated, or corrupted. We introduce two protocols for this type of channel. 
• Simplest Protocol 
• Stop-and-Wait Protocol

##### Simplest Protocol
- **Theoretical Model**: This protocol is purely theoretical and impractical for real-world applications.
- **Lack of Control**: It does not implement any flow control or error control mechanisms.
- **Receiver Efficiency**: The receiver can process any incoming frame with minimal delay.
- **No Overload Risk**: The protocol ensures that the receiver is never overwhelmed with multiple frames, maintaining a constant flow of data.

![[{7CCF2889-DE0A-4D7C-BEE3-EFB9A49593E2}.png]]

###### Sender-site algorithm for the simplest protocol
![[{E5B95469-EAA0-483F-81C5-C4978043BCDD}.png]]

###### Receiver-site algorithm for the simplest protocol
![[{68AC6292-9950-41F1-A35A-617C94453560}.png]]

###### Simplest Protocol (Example)
Figure shows an example of communication using this protocol.
- **Communication Flow**: The sender transmits a sequence of frames without consideration for the receiver's status.
- **Frame Transmission**: To send three frames, the sender initiates three events, each corresponding to a frame being sent.
- **Receiver Events**: Simultaneously, three events occur at the receiver as each frame is received.
- **Frame Representation**: Data frames are depicted as tilted boxes; the height of each box represents the time taken to transmit from the first bit to the last bit of the frame.
![[{3D6085F8-CD69-4169-8234-5B8D3CFF3402}.png]]

##### Stop and Wait Protocol
- **Frame Processing**: If frames arrive faster than the receiver can process them, the excess frames must be temporarily stored.
- **Flow Control**: To prevent overwhelming the receiver, it must communicate with the sender, typically through an acknowledgment (ACK).
- **Transmission Process**: The sender transmits one frame and then pauses until it receives confirmation from the receiver before sending the next frame.

![[{9951B484-AB66-4EB6-8D30-CF9EAF025589}.png]]

![[{733E146F-2103-4C04-A5F7-97FC2A5230FB}.png]]


![[{06C7AD72-D723-43FE-AD1F-D1A415E0A61A}.png]]

###### Stop and Wait Protocol (Example)
- **Protocol Overview**: The sender sends one frame at a time and waits for feedback (ACK) from the receiver before proceeding to send the next frame.
- **Event Breakdown**:
    - **Sender Events**: For every two frames sent, there are four events:
        1. Sending the first frame.
        2. Waiting for the ACK for the first frame.
        3. Sending the second frame.
        4. Waiting for the ACK for the second frame.
    - **Receiver Events**: The receiver is involved in two main events:
        1. Receiving the first frame and sending an ACK.
        2. Receiving the second frame and sending another ACK.

![[{9CC9709E-BD63-4612-8754-053A09975929}.png]]

#### Noisy Channel
Although the Stop-and-Wait Protocol gives us an idea of how to add flow control to its predecessor, noiseless channels are nonexistent. In real-world scenarios, channels are never completely noiseless. To handle errors effectively, we introduce three protocols that incorporate error control
- **Stop-and-Wait Automatic Repeat Request (ARQ)**:
    - The sender transmits one frame and waits for an ACK.
    - If the ACK is not received within a certain time (due to potential errors), the sender retransmits the frame.
    - This method ensures reliable communication but can be inefficient if the transmission time is longer than the wait time.
- **Go-Back-N Automatic Repeat Request**:
    - The sender can transmit multiple frames before needing an ACK, but must keep track of all sent frames.
    - If an error is detected in a frame, the sender goes back and retransmits that frame and all subsequent frames, even if they were received correctly.
    - This approach improves efficiency but can lead to unnecessary retransmissions.
- **Selective Repeat Automatic Repeat Request**:
    - Similar to Go-Back-N, but only the erroneous frames are retransmitted.
    - The sender keeps a window of unacknowledged frames and can selectively resend only those that were lost or corrupted.
    - This method is more efficient than Go-Back-N, as it minimizes retransmissions and optimizes the use of the channel.

##### Stop And Wait ARQ
- **Error Correction**:
    - The sender retains a copy of the sent frame.
    - If an ACK is not received within a specified time (when the timer expires), the sender retransmits the frame.
- **Sequence Numbers**:
    - Frames are assigned sequence numbers using modulo-2 arithmetic.
    - This numbering helps differentiate between frames and manage retransmissions effectively.
- **Acknowledgment Numbers**:
    - The acknowledgment (ACK) sent by the receiver indicates the sequence number of the next expected frame.
    - This ensures the sender knows which frame has been successfully received and can proceed accordingly.
![[{12633624-6466-4D59-9117-3F914B4F1C1E}.png]]

###### Algorithm: Sender site Algorithm for Stop And Wait ARQ Protocol
![[{CA30C5D7-CB89-47A8-B30E-1223EBE4C8DE}.png]]
![[{1ADA99CD-E8B1-438A-BAF4-CD919C32A3BD}.png]]

###### Algorithm: Receiver site Algorithm for Stop And Wait ARQ Protocol
![[{F79BD8B4-3385-4728-9E13-BAEACCE39F57}.png]]

###### Stop And Wait ARQ (Example)
Figure shows an example of Stop-and-Wait ARQ. 
• Frame 0 is sent and acknowledged. 
• Frame 1 is lost and resent after the time-out. 
• The resent frame 1 is acknowledged and the timer stops.
• Frame 0 is sent and acknowledged, but the acknowledgment is lost. The sender has no idea if the frame or the acknowledgment is lost, so after the time-out, it resends frame 0, which is acknowledged.
![[{F558C3E0-F4D1-445F-A52A-22E082C33E70}.png]]

###### Efficiency of Stop-and-Wait ARQ
- **Inefficiency**:
    - The Stop-and-Wait protocol is particularly inefficient in channels with high bandwidth (thick) and long round-trip delays (long).
- **Bandwidth-Delay Product**:
    - This product measures the volume of data that can be "in flight" in the network, calculated as: Bandwidth - Delay Product=Bandwidth × Round Trip Time
    - It indicates the number of bits that can be sent while waiting for an acknowledgment (ACK) from the receiver.
- **Impact on Efficiency**:
    - In such scenarios, the sender often remains idle, waiting for ACKs, leading to underutilization of the channel capacity and decreased overall efficiency.

###### Example 1:
Assume that, in a Stop-and-Wait ARQ system, the bandwidth of the line is 1 Mbps, and 1 bit takes 20 ms to make a round trip. What is the bandwidth-delay product? If the system data frames are 1000 bits in length, what is the utilization percentage of the link?

Solution: 
The bandwidth-delay product is:
![[{F3692602-9A29-4708-B2CF-88E8AF628E90}.png]]

The system can send 20,000 bits during the time it takes for the data to go from the sender to the receiver and then back again. However, the system sends only 1000 bits.

We can say that the **link utilization** is only **1000/20,000**, or **5 percent.** 

For this reason, for a link with a high bandwidth or long delay, the use of Stop-and-Wait ARQ wastes the capacity of the link.

###### Pipelining:
• No pipelining in Stop-And-Wait ARQ.
• We need to wait for a frame to reach the destination and be acknowledged before next frame can be sent. 
• Pipelining is applicable to next two protocols, wherein several frames can be sent before receiving acknowledgement for previous frames. 
• Pipelining improves efficiency.
##### Go-Back-N ARQ

• To improve the efficiency of transmission (filling the pipe), multiple frames must be in transition while waiting for acknowledgment. 
• This protocol can send several frames before receiving acknowledgments it keep a copy of these frames until the acknowledgments arrive. 
• In the Go-Back-N Protocol, the **sequence numbers** are modulo 2^m i.e. the sequence numbers range from **0 to 2^m - 1**, where m is the size of the sequence number field in bits.

![[{4A1B33A8-6DF4-40F4-B233-268D9C7031B1}.png]]


![[{A13F5972-E3A9-47B5-BF3E-818AF23411E3}.png]]


###### Sliding Window:
• Sliding window is an abstract concept that defines the range of sequence numbers. 
• The range which is the concern of the sender is called the send sliding window; the range that is the concern of the receiver is called the receive sliding window. 
• The window at any time divides the possible sequence numbers into four regions.

###### Send Window : 
• Sliding window is an abstract concept that defines the range of sequence numbers. 
• The send window can slide one or more slots when a valid acknowledgment arrives.

![[{A7740EE1-A990-4E40-A2CF-60469C2FFAB0}.png]]

###### Receive Window :
• The receive window is an abstract concept defining an imaginary box of size 1 with one single variable Rn. 
• The window slides when a correct frame has arrived; sliding occurs one slot at a time.
![[{71DDCB55-FF00-450A-92B7-F118310AF82A}.png]]

![[{1EE0D6F1-BCB5-4986-BE31-3CBB3CCBB4A6}.png]]

###### Algorithm: Go-Back-N sender algorithm
![[{32A52116-3715-4B8F-8EAB-8B68762BBDBE}.png]]
![[{9E735E35-B298-4F60-848C-7DE7E5DABAE4}.png]]

###### Algorithm: Go-Back-N sender algorithm
![[{16B87A2A-3639-4B12-8BF7-248C49705E1A}.png]]

###### Piggybacking in Go Back N ARQ
![[{DDF5B4FC-4DDE-4C52-8739-F07DD210482E}.png]]

##### Selective Repeat ARQ
• Go-Back-N ARQ simplifies the process at the receiver site. 
• The receiver keeps track of only one variable, and there is no need to buffer out-of-order frames; they are simply discarded. 
• However, this protocol is very inefficient for a noisy link. 
• In a noisy link a frame has a higher probability of damage, which means the resending of multiple frames. This resending uses up the bandwidth and slows down the transmission.
• Mechanism that does not resend N frames when just one frame is damaged; only the damaged frame is resent. 
• More efficient for noisy links, but the processing at the receiver is more complex. 
• the size of the send window is much smaller; it is 2^(m- 1). 
• sizes of the send window and receive window are the same.

![[{E1F8E34A-0086-45C7-AD9C-1EF19FC7C9D4}.png]]

![[{CF21CB17-A69F-4BF0-9F42-C9CA0BF093B4}.png]]

![[{F187E924-4B68-4AAA-8287-840AB83A6773}.png]]

![[{4B919A49-C3B7-4CCE-A1BE-668DEC6F80E8}.png]]

###### Sender Site SR ARQ Algorithm:
![[{C7EA8502-03F2-428C-872C-88F6F05C90D9}.png]]
![[{C14232B4-D979-483F-BD6E-397E82E24FD8}.png]]
![[{7B65BF7E-3BC7-47AA-AD23-DE3CD333541F}.png]]

###### Receiver Site SR ARQ Algorithm
![[{7FE0F3FF-38C5-421A-9209-C317D7C18DF9}.png]]
![[{AC4D5FA4-0E79-4794-BDD8-697C7AA22964}.png]]

###### Delivery of data in Selective Repeat ARQ:
![[{7A4E1624-26B7-4093-A065-C3DB470F95AF}.png]]

###### Flow Diagram:
![[{04FD16B7-9753-4132-85F1-F0D939D5FCEF}.png]]

### HDLC
- **Type:** Bit-oriented protocol for point-to-point and multipoint links.
- **Functionality:** Implements Automatic Repeat reQuest (ARQ) mechanisms.
#### Configurations and Transfer Modes
- **Normal Response Mode (NRM):**
    - Master/slave configuration where the master controls the communication.
- **Asynchronous Balanced Mode (ABM):**
    - Peer-to-peer configuration allowing both stations to initiate communication.

##### Normal Response Mode
![[{5C9924F0-5C69-4F81-B044-44028E883199}.png]]

##### Asynchronous Balanced Mode
![[{E62A1487-6B28-487A-82BC-964CB64B1AF9}.png]]

#### HDLC frames
![[{59B0A362-36B8-40A3-A15D-61CC56D08300}.png]]
![[{5E56E0EF-0B74-40AA-8AF8-C52FA7EAB4C0}.png]]

#### Control field format for the different frame types
![[{F8936085-EF42-4926-AAF7-D57D2195EEED}.png]]

#### U-frame control command and response
![[{C9C55D68-D494-4C52-9E38-FECC3FF58CC1}.png]]

## 2.3  MAC address; Random Access: ALOHA, slotted ALOHA, Efficiency; CSMA, CSMA/CD, CSMA/CA.

### Multiple Access
- **Multiple Access Mechanisms:**
    - Methods used to allow multiple devices to communicate over the same communication channel.
    - Ensures efficient use of shared media without collisions or data loss.

- **Random Access:**
    - Devices transmit whenever the channel is free, but collisions may occur.
    - Mechanisms:
        - **ALOHA:** Simplest random access technique where devices send data whenever they have it, relying on retransmission in case of collisions.
        - **CSMA (Carrier Sense Multiple Access):** Devices check if the channel is clear before transmitting, reducing the chance of collisions.
            - **CSMA/CD (Collision Detection):** Detects collisions and retransmits data after a random delay (used in Ethernet).
            - **CSMA/CA (Collision Avoidance):** Prevents collisions through acknowledgments (used in Wi-Fi networks).

- **Controlled Access:**
    - Devices coordinate with each other to avoid collisions.
    - Mechanisms:
        - **Polling:** Central controller polls each device to check if it needs to send data.
        - **Token Passing:** A token is passed between devices, and only the device with the token can transmit.

- **Channelization:**
    - Divides the channel into separate, non-overlapping channels, allowing multiple devices to communicate simultaneously.
    - Mechanisms:
        - **FDMA (Frequency Division Multiple Access):** Divides bandwidth into frequency bands assigned to different users.
        - **TDMA (Time Division Multiple Access):** Allocates time slots for devices to transmit in turns.
        - **CDMA (Code Division Multiple Access):** Assigns unique codes to each device, allowing simultaneous transmission over the same frequency band.

#### Sublayers of Data Link Layer
![[{69890E33-6AAF-42C5-9ACA-A80BC4DF352A}.png]]

• The upper sub layer that is responsible for flow and error control is called the **logical link control (LLC) layer.**
• Lower sub layer that is mostly responsible for multiple access resolution is called the **media access control (MAC) layer.**

#### Multiple Access Mechanisms
![[{F2F74B4F-8520-4093-B97C-FA4459D8795A}.png]]

### Random Access
• **No station is assigned to control another**: In random access mechanisms, there is no centralized control system. Each station operates independently and makes its own decisions about when to transmit data.

• **Each station independently decides when to send data**: Every station that has data to send uses the protocol to make a decision. There is no pre-determined schedule or allocation for transmission times.

• **Transmission is random**: Stations do not follow any predefined order; they transmit data whenever they have it, making it a **contention-based** approach where stations compete to send.

• **Stations compete to access the shared medium**: Since there is no centralized control, stations that want to send data must contend with one another to gain access to the shared communication medium.

• **Every station has equal access rights to the medium**: In this model, all stations are equal in their ability to access the network. Any station can attempt to send data at any time.

• **When more than one station transmits simultaneously, collisions occur**: Since multiple stations may try to send data at the same time, their signals can interfere with one another, causing collisions.

• **Collisions result in destroyed or modified frames**: When a collision happens, the transmitted frames are either lost or altered, requiring **retransmission** to ensure accurate communication.

### ALOHA Network
- **When a station sends data**, another station may attempt to send data **at the same time**, leading to a **collision**.
- In the event of a collision, the **data from both stations becomes garbled**.
two types of random access methods
✓ Pure Aloha
✓ Slotted Aloha

#### Pure ALOHA
- **Frame Transmission**: Each station sends a frame whenever it has data to send.
- **Single Channel**: Since all stations share the same channel, **collision** between frames is possible.
- **Collision**: If even **one bit** from different frames overlaps, a collision occurs, and **both frames** are destroyed.
- **Resend on Collision**: Stations resend destroyed frames after receiving a **timeout or acknowledgment**.
- **Pure ALOHA**: After a **timeout**, each station waits a ==**random amount of time**== before retransmitting the frame to avoid repeated collisions.
- **Random Backoff Time (TB)**: Random time intervals help reduce the likelihood of further collisions.
- **Congestion Control**: To prevent the channel from being congested, there's a limit on the number of retransmissions (Kmax). After **Kmax retries**, the station stops trying and attempts later.

![[{112C3A57-A145-4880-8DC4-287D5B0CFA84}.png]]

##### Frames in Pure ALOHA
![[{47D60DE1-011A-4D3D-8791-3BB67758D9A9}.png]]

##### Example

Calculate possible values of TB when stations on an ALOHA network are a maximum of 600 km apart; signal propagates at 3 x 10^8 m/s.

Tp = (600 × 103) / (3 × 10^8) = 2 ms

When K=1, TB Є {0 ms,2 ms} 
When K=2, TB Є {0 ms,2 ms,4 ms, 6ms}

#### ALOHA: Vulnerable Time
![[{21E890BA-BF2F-4F91-BDD8-2CDB1370C417}.png]]

##### ALOHA: Throughput
- **Poisson Distribution**: Assume the number of stations trying to transmit follows a **Poisson Distribution**.
- **Throughput Formula**: The throughput for **Pure ALOHA** is given by: ==S=G×e^−2G==
    - where **G** is the average number of frames requested/generated by the system per frame-time.
- **Maximum Throughput**: The maximum throughput ==Smax=0.184 when G=1/2==

##### Slotted ALOHA
• Pure ALOHA has a vulnerable time of **2 x Tfr** - no rule that defines when the station can send. 
• Slotted ALOHA was invented to improve the efficiency of pure ALOHA. 
• Slotted ALOHA divide time into slots of Tfr and force the station to send only at the beginning of the time slot.

##### Slotted ALOHA: Vulnerable Time
![[{7716CCB6-4AED-4825-AF75-53735CFE8683}.png]]

##### Slotted ALOHA: Throughput
• The throughput for Slotted ALOHA is 
**S = G × e−G** 
where G is the average number of frames requested per frame- time 
• The maximum throughput 
**Smax = 0.368 when G= 1**

##### Slotted ALOHA: Throughput Example
Q. A pure ALOHA network transmits 200-bit frames on a shared channel of 200 kbps. What is the throughput if the system (all stations together) produces 
a. 1000 frames per second? 
b. 500 frames per second? 
c. 250 frames per second?

![[{53FE6844-A9EF-4B85-9937-7967B3FC8A31}.png]]

Q. A slotted ALOHA network transmits 200-bit frames using a shared channel with a 200-kbps bandwidth. Find the throughput if the system (all stations together) produces 
a. 1000 frames per second. 
b. 500 frames per second. 
c. 250 frames per second.

![[{228CE365-B324-4AD5-9D4D-FF5A63FB5BBA}.png]]

### CSMA
- **Carrier Sense Multiple Access (CSMA)**: Known as "Listen before talk."
- **Collision Reduction**: CSMA reduces the possibility of collision but cannot completely eliminate it.
- **Medium Check**: Each station must first check the state of the medium before sending data.
- **Propagation Delay**: Collision possibility still exists due to **propagation delay**; even after a station sends a frame, it takes time for the first bit to reach every station, leading to potential collisions.

#### Collision in CSMA
![[{B6A6F7B3-7BEE-4B50-9DB1-501FA1734E0D}.png]]

==The vulnerable time for CSMA is the propagation time Tp==

![[{B0C2E3DD-5A73-40F8-B777-844D4CB881A4}.png]]

#### Persistence Methods
![[{BAA6E356-3034-49CE-AC8D-6098028C1ADF}.png]]
![[{6A1E963C-192B-4221-B7BF-C5CCFBA67AB8}.png]]

### CSMA/CD
- **Carrier Sense Multiple Access with Collision Detection (CSMA/CD)**: Enhances CSMA by handling collisions.
- **Monitoring During Transmission**: Each station monitors the channel while sending a frame.
- **Collision Detection**: A station checks the medium after sending a frame to see if the transmission was successful.
- **Frame Size Restriction**: For CSMA/CD to function properly, there must be a restriction on frame size.
- **Collision Detection Requirement**: The station must detect a collision before the last bit is sent, as it does not keep a copy of the frame once sent.
- **Frame Transmission Time**: The transmission time Tfr​ must be at least 2×TP​ (twice the maximum propagation time) to allow collision detection.
- **Frame Size Consideration**: Each frame must be large enough for the sender to detect a collision effectively.
- **Worst Case Scenario**: If Station "A" is transmitting and Station "D" starts transmitting just before "A's" signal arrives, a collision may occur.

![[{F04C93BA-CDD8-4766-8BA6-E9F80CA90313}.png]]

#### CSMA/CD: Energy Levels
![[{FF4983C3-EC6E-46AB-AABE-C0DFEC3470DF}.png]]
![[{C146D1A1-A559-4FEE-921A-29F05CD73BB0}.png]]

### Difference ALOHA and CSMA/CD
- **Persistence Process**:
    - ALOHA does not have a persistence mechanism for sensing the medium, whereas CSMA/CD requires stations to listen to the channel before transmitting.
- **Frame Transmission**:
    - In ALOHA, a station transmits the entire frame and then waits for an acknowledgment.
    - In CSMA/CD, the transmission and collision detection happen continuously.
- **Jamming Signal**:
    - ALOHA does not utilize jamming signals.
    - CSMA/CD includes a short jamming signal to ensure that all stations are aware of a collision if it occurs before they can sense it.

### CSMA/CA
### Carrier Sense Multiple Access with Collision Avoidance (CSMA/CA)

- **Purpose**: 
  - Used in networks where collisions cannot be detected, such as wireless LANs. 
  - Aims to avoid collisions due to the inability to detect them.

- **Collision Avoidance Strategies**:
  1. **Inter-frame Space (IFS)**: 
     - Collisions are avoided by deferring transmission even when the channel is found idle.
     - When an idle channel is detected, the station waits for a designated period called IFS before sending.
     - IFS can prioritize stations or frame types; shorter IFS means higher priority.

  2. **Contention Window**: 
     - The contention window is a time interval divided into slots.
     - A station ready to transmit chooses a random number of slots to wait before sending.
     - The number of slots adjusts based on the binary exponential back-off strategy; it starts with one slot and doubles each time the channel is busy after the IFS.

![[{8721F8A1-9CC1-4C7E-826C-CB754A3D8DF5}.png]]
  
  3. **Acknowledgments**: 
     - Collisions may still occur, resulting in lost or corrupted data.
     - Positive acknowledgments and time-out timers help ensure that the receiver has successfully received the frame.

![[{1D3766F1-DDEB-46A2-9889-218EE874630A}.png]]

#### CSMA/CA: Hidden and Exposed Terminal Problem
![[{0392EEE3-C124-491B-A047-B889852E59E0}.png]]

## 2.4 Controlled Access, Channelization, IEEE standards, different Ethernets

### Controlled Access
- **Definition**: 
  - In controlled access, stations coordinate to determine which has the right to transmit data. 
  - A station must receive authorization from others before sending.

- **Common Methods**:
  1. **Reservation**:
     - A station must make a reservation before transmitting data.
     - Time is divided into intervals for transmission.
     - A reservation frame is sent before the data frames in that interval.
     - For N stations in the system, there are exactly N reservation mini-slots, allowing each station to reserve its time to send data.

  2. **Polling**:
     - A central controller polls each station in sequence to ask if it has data to send.
     - Only the station that responds can transmit, ensuring orderly access.

  3. **Token Passing**:
     - A token is passed around the stations in the network.
     - Only the station holding the token can transmit, preventing collisions and ensuring controlled access.


#### Reservation
- **Reservation Requirement**: A station must make a reservation before sending data.
- **Time Division**: Time is divided into specific intervals for organized transmissions.
- **Reservation Frame**: A reservation frame precedes the data frames in each interval, indicating the station's intention to transmit.
- **Mini-Slots**: In a system with **N stations**, there are **N reservation mini-slots** available, allowing each station to make reservations efficiently.

##### Reservation Method
![[{FC467D54-D922-4EAC-86A0-5212D934872C}.png]]

#### Polling Method
- **Polling**: Works with topologies where one device is the primary station and others are secondary stations. 
- **Data Exchange**: All data exchanges occur through the primary device. 
- **Channel Control**: The primary device determines which secondary device can use the channel. 
- **Initiator Role**: The primary device is always the initiator of a session. 
- **Select Function**: Used when the primary device has something to send. 
- **Poll Function**: Used by the primary device to solicit transmissions from secondary devices.

![[{F7626F07-9860-4479-8792-DC1AAB771983}.png]]

#### Token Passing
- **Logical Ring Structure**: Stations in the network are organized in a logical ring, with each having a predecessor and a successor. 
- **Current Station**: The current station is the one accessing the channel now, having received the right to access from its predecessor. 
- **Access Transfer**: The right to access the channel is passed to the successor when the current station has no more data to send. 
- **Token Circulation**: A special packet called a token circulates through the ring to control access. 
- **Token Management**: Management of the token is necessary for this access method. 
- **Time Limitation**: Stations must be limited in the time they can possess the token. 
- **Token Monitoring**: The token must be monitored to ensure it has not been lost or destroyed. 
- **Priority Assignment**: Assign priorities to stations and types of data, allowing low-priority stations to release the token to high-priority stations.

![[{CF319400-DD5F-48C9-8441-7221ACB07A19}.png]]

### Channelization

- **Channelization**: Similar to multiplexing, allowing multiple stations to share the same communication medium.

**Three Schemes**
- **Frequency-Division Multiple Access (FDMA)**: Divides the frequency spectrum into separate channels, with each station assigned a specific frequency for transmission.
- **Time-Division Multiple Access (TDMA)**: Allocates time slots for each station to transmit, ensuring that each has a designated time to access the channel.
- **Code-Division Multiple Access (CDMA)**: Uses unique codes for each station, allowing them to transmit simultaneously over the same frequency band by distinguishing their signals through coding.

#### FDMA and FDM
- **FDM vs. FDMA**: FDM (Frequency-Division Multiplexing) is a physical layer multiplexing technique, while FDMA (Frequency-Division Multiple Access) is a data link layer access method.
- **FDMA Utilization**: Using FDM to allow multiple users to utilize the same bandwidth is referred to as FDMA.
- **Multiplexer Requirement**: FDM uses a physical multiplexer to combine signals, whereas FDMA does not require a physical multiplexer.
![[{D193B603-BCBD-416D-B03C-FFC63D35D4DB}.png]]

#### TDMA
- **TDMA Overview**: TDMA (Time-Division Multiple Access) is a data link layer access method that allows multiple users to share the same frequency channel by dividing the signal into time slots.
- **Time Slot Allocation**: In TDMA, each user is assigned a specific time slot during which they can transmit data, ensuring that only one user transmits at a time.
- **Efficient Bandwidth Use**: TDMA improves bandwidth efficiency by minimizing the chance of collisions since each station has a defined time to send its data.
- **Synchronization Requirement**: TDMA systems require precise synchronization between users to ensure that time slots are used correctly and no overlaps occur.
- **Comparison to FDM**: Unlike FDMA, which divides the frequency spectrum, TDMA divides the time domain for access to the shared medium.

![[{3AC72EAB-4963-469E-A828-85DA4FB02037}.png]]

#### CDMA
- **One Channel Usage**: A single channel carries all transmissions simultaneously.
- **Code Separation**: Each transmission is separated by unique codes, allowing multiple users to share the same frequency band without interference.

##### CDMA: Chip Sequences
- **Unique Chip Sequence**: Each station is assigned a unique chip sequence for transmission.
- **Orthogonal Vectors**: Chip sequences are orthogonal, meaning the inner product of any pair must be zero, ensuring no interference.
- **Length and Properties**: For N stations, the sequences must be of length NNN and have a self inner product of N.

![[{B6305FA6-4CF5-4A6D-8E49-E1BC1FD0E651}.png]]

##### CDMA: Bit Representation
![[{E9555650-E458-46A6-B400-6065917E6159}.png]]

##### Transmission in CDMA
![[{A63D95A3-0C13-4FC0-97A5-15FFC4095065}.png]]

##### CDMA Encoding
![[{F930C75D-CD46-41CF-A207-5440E4B26556}.png]]

##### Signal Created by CDMA
![[{707F577F-86AD-4051-B303-45AE8D267853}.png]]

##### CDMA Decoding
![[{ADE197FA-F7F0-4072-8F47-15D0E6D6BE39}.png]]

### Sequence Generation
- **Walsh Table**: A common method for generating sequences in CDMA.
- **Power of Two**: The number of sequences generated is always a power of two, ensuring efficient utilization of the available space.

![[{BD1AE012-17D7-45EE-9CB1-2738D7F6AFCA}.png]]

### IEEE Standards
- **Project 802**: Initiated in 1985 by the Computer Society of the IEEE to establish standards for intercommunication among equipment from various manufacturers.
- **Purpose**: Specifies functions of the **physical layer** and **data link layer** for major LAN protocols, facilitating interoperability.
- **Significance**: Aims to promote compatibility and communication between devices from different manufacturers.
![[{E3BC159A-62B1-4D5F-8A80-8E1AA04FC397}.png]]


![[{C9EA0A8F-6761-4896-8AC2-A07CB044EF08}.png]]

#### Mac Frame 
- **Preamble**:
    - Consists of **seven bytes** (10101010).
    - Used by the receiver to establish **bit synchronization**.

- **Start Frame Delimiter (SFD)**:
    - A single byte (10101011) indicating the start of a frame.
    - Signals that the **Destination MAC Address** field begins with the next byte.

- **Destination MAC Address**:
    - Identifies the intended recipient of the frame.

- **Source MAC Address**:
    - Identifies the sender of the frame.

- **Length or Type**:
    - Defines the type of protocol inside the frame (e.g., IPv4, IPv6, ARP, OSPF).
    - Indicates the number of bytes in the frame's payload (0 to 1500 bytes).
    - Frames must be at least **64 bytes long** (excluding the preamble). If the data field is shorter than **46 bytes**, it must be padded.

- **Data**:
    - Carries data encapsulated from upper-layer protocols.
    - Minimum size: **46 bytes**; maximum size: **1500 bytes**.
    - If data exceeds **1500 bytes**, it must be fragmented into multiple frames. If less than **46 bytes**, it is padded with extra **0s**.

- **CRC (Cyclic Redundancy Check)**:
    - Contains error detection information.
    - Calculated over the addresses, type, and data fields.
    - If the receiver calculates the CRC and finds it is not zero, the frame is discarded.

![[{0E19F090-1D22-422F-940F-4D85CF77ABE3}.png]]
![[{58A888C6-A193-4B11-91A9-D488EB25E287}.png]]
![[{E31AC0A6-CD3F-4027-8DB6-3891C0F044E2}.png]]

##### Unicast and multicast addresses

![[{0AD0FCAD-2097-4240-AB8C-C75D9EB851B6}.png]]

- **Broadcast Destination Address**:
    - A special case of the multicast address where **all bits are 1s**.
- **Address Type Indicator**:
    - The least significant bit of the **first byte** defines the type of address.
        - If the bit is **0**, the address is **unicast**.
        - If the bit is **1**, the address is **multicast**.

#### Examples

![[{9007F4F6-F04F-4C52-8088-FAA31C6E546D}.png]]
![[{D5C05AF5-70BD-44B7-8022-8EE4E0C2D464}.png]]

### Categories of Standard Ethernet
![[{B610631C-2259-409B-AF1B-0C7F49ED71E9}.png]]![[{457EA04E-5CDF-4097-8069-7CA548678628}.png]]

# Made By Yashank