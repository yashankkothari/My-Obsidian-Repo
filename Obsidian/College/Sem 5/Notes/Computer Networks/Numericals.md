### Checksum

Checksum is created at senders side
Checksum is validated at receivers side
#### Checksum Operations at Sender Side
![[{E57AA454-86ED-4EF2-B09B-532C4200F4FF}.png]]

![[{59D3A2C3-15E3-4F2C-91A0-F0341440D510}.png]]

#### Checksum Example
![[{E3E06A06-8553-46D2-AFFB-F8E5EC1AC427}.png]]

After dividing it into parts we need to add them all up

![[{165D13EB-51EB-46F2-837B-46F084EAB2C0}.png]]

in this example we have got **10** as the carry but we cant keep it there so we have to add it to the overall answer we got so it'll be

![[Drawing 2024-09-24 01.44.28.excalidraw|700]]

Now we will do 1's compliment of the below number that we get
![[{7FDB9B18-8CBD-4E36-9178-19A1D94E61A2}.png|700]]

After we get the checksum, it is added to the beginning of the data that we want to transmit
![[Numericals 2024-09-24 01.48.26.excalidraw|700]]

Now the sender part is over

#### Checksum Operations at Receiver Side
![[{DF1E1F29-77D6-48E3-A7B4-FEE2C59E922D}.png]]

lets assume that the receiver is receiving the same data block without any errors

![[Numericals 2024-09-24 01.51.56.excalidraw|700]]

if the result is all 1, the receiver will accept it as there are no transmission errors
#### Performance of checksum
![[{58626FD2-C790-4234-8B90-AF861C4EC3E3}.png]]


### CRC (Cyclic Redundancy Check)

#### CRC Generation at Sender Side
![[{FB55C6D4-526C-4A30-A178-81B2A7B2FDCD}.png]]

![[{30981A6B-C786-4E75-9808-0B63682E312E}.png|700]]

Since our divisor ha L=4 (length of divisor is 4)
we will do step 2
L-1=3 so we will append 3 0's to the original message

![[{B7459525-4AAA-4277-AEDE-83CD93D12779}.png|700]]

==**your number should always start with a 1, if it starts with a 0 you need to do an XOR operation with 0**==

![[Numericals 2024-09-24 02.05.14.excalidraw]]

==Your Final remainder will be the CRC==

![[{7C82FEBA-9FD3-435E-8303-3FFD82C34AF3}.png|500]]

![[Numericals 2024-09-24 02.09.08.excalidraw|600]]

#### Polynomial to Divisor Conversion
![[{B1BF2EC2-E549-47DA-A2A3-0B4A5658DF4E}.png|300]]

If the polynomial is given and you want to do a binary division, you can use this conversion
#### CRC From Receiver

lets take the same example : 100100001 is the received message

your divisor will remain the same which is 1101 which is taken from the polynomial given

now just perform division 

![[{D426F4F9-E948-4F70-8C46-310C0C1B806D}.png]]

since the remainder is all 0s the receiver can conclude that the data is right


### single parity
### hamming dist
### hamming code 

### subnetting vale

![[{F2B39A92-3F42-4576-8E31-B767D9D7A165}.png]]
![[{13296CA2-B0C1-41DC-8A65-48986DD5607F}.png]]








![[{84CD050F-B671-48E2-87FB-D8B65A480F38}.png]]

![[{98011E13-E51D-4A52-8E7A-543C428789F6}.png]]

![[{CE581AE3-EB9D-4FAF-A98B-12AFD02058F0}.png]]




### upernetting
### cidr
### aloha



