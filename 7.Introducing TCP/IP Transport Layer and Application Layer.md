### Internet Protocol #ip 
- IP uses packets to carry information through the network
	- A packet is a self-contained, independent entity that contains data and sufficient information to be routed from the source to the destination without reliance on previous packets
- IP has these characteristics:
	- Operates at Layer 3 or the network layer of OSI reference model and at the Internet layer of the TCP/IP stack
	- Connectionless protocol
		- One way packet is sent to the destination without advance notification to the destination device
		- Destination device receives the data and does not return any status information to the sending device
	- Each packet is treated independently, can travel a different way to the destination
		- Also operates independently of the medium that is carrying the data
	- Uses hierarchical addressing, network identification is the equivalent of a street, host ID is equivalent of a house or office building on the street
	- Provides service on a best-effort basis and does not guarantee packet delivery
		- Packet can be misdirected, duplicated or lost on the way to its destination
	- Does not provide any special features that recover corrupted packets
		- The end systems of the network provide these services
	- IPv4 and IPv6, IPv6 becoming increasingly important in modern networks

![[Pasted image 20241006204217.png]]
> Sample of Company A obtaining a public IP address
### Binary to Decimal Vice Versa Conversion

| 256   | 128   | 64    | 32    | 16    | 8     | 4     | 2     | 1     | 0   |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | --- |
| $2^8$ | $2^7$ | $2^6$ | $2^5$ | $2^4$ | $2^3$ | $2^2$ | $2^1$ | $2^0$ | 0   |

### IPv4 Address Representation
- IPv4 Address is a 32-bit number, is hierarchical and consists of 2 parts:
	- The network address portion (network ID)
		- Uniquely identifies the network in which the device with this IPv4 address resides
		- If the hosts need to communicate with devices with interfaces assigned to some other network ID, a network device (router or a multilayer switch) can route data between the networks
	- The host address portion (host ID)
		- Uniquely identifies a device on a given IPv4 network
		- Assigned to individual devices, both hosts or endpoints and intermediary devices
![[Pasted image 20241007143549.png]]
> Sample of how IP address, in dotted-decimal notation
> Consists of 4 sets of 8 bits (octets)
### IPv4 Header Fields
![[Pasted image 20241007143957.png]]
- Has several fields:
	- Service type = Provides information on the desired quality of service
	- TTL = Defines the number of available hopes and limits the lifetime of a packet
		- Does not use time measurement units, uses per hop 
	- Source address = Specifies the 32-bit binary value that represents the IPv4 address of the sending endpoint
	- Destination address = Specifies the 32-bit binary value that represents the IPv4 address of the receiving endpoint
- Other fields:
	- Version = Describes the version of IP
	- IHL = Internet Header Length, describes the length of the header
	- Total Length = Describes the length of the packet, including header and data
	- Identification = Used for unique fragment identification
	- Flag = Sets various control flags regarding fragmentation
	- Fragment Offset = Indicates where a specific fragment belongs
	- Protocol  = Indicates the upper-layer protocol that is used in the data portion of an IPv4 packet
		- For example, a protocol value of 6 indicates this packet carries a TCP segment
	- Header checksum = Used for header error detection
	- Options = Includes optional parameters
	- Padding= Used to ensure that the header ends on a 32-bit boundary
### IPv4 Address Classes
- Assigning IPv4 addresses to classes is known as classful addressing
	- Each IPv4 address is broken down into a network ID and a host  ID
	- A bit or a bit sequence at the start of each address determines the class of the address
- Classes defines the network part of the IP address, which cannot be changed, and the host part of the IP address can be selected and used (if the IP address is available)
- For example:
![[Pasted image 20241007152830.png]]

![[Pasted image 20241007153029.png]]
> Classes overview
> *127.0.0.0 - 127.255.255.255 is used for loopback and diagnostic functions
#### Class A
- Designed to support extremely large networks with more than 16 million host addresses
- Uses only the first 8 bits 
	- The remaining is used for host addresses
- First bit is always 0, highest number represented is 0111 1111 (127), but cannot be represented as it is reserved
#### Class B
- Designed to support the needs of moderate to large networks with more than 65,000 hosts
- Uses 16 bits to indicate the network address
- Starts with 10, lowest number that can be represented is 1000 0000 (128 ) and between the range of 128-191
#### Class C
- Most commonly available address class
- Intended to provide address for small networks with a maximum of 254 hosts
- Uses 24 bits 
- Starts with 110, lowest number is 1100 0000 (192) and between the range of 192-223
#### Class D
- Dedicated to multicast applications such as streaming media
	- Multicasts are a special type of broadcast in that only hosts that request to participate in the multicast group will receive the traffic to the IPv4 address of that group
- Multicast addresses are always the destination address and never the source
- Begins with 1110, lowest is 1110 0000 (224), range between 224-239
#### Class E
- Reserved by IANA as a block of experimental addresses
- Should never be assigned to IPv4 hosts
- Begins with 1111, lowest number 1111 0000 (240), range between 240-255

### Subnet Masks
- Is a 32-bit number that describes which portion of an IPv4 address refers to the network ID and which part refers to the host ID
- Is configured on a device along with the IPv4 address
- The main purpose of subnet mask is to identify the network address of a host, which is crucial for routing purposes
- Based on the network address, the host can identify whether a packet's destination address is within the same network or not
![[Pasted image 20241007155933.png]]
> Prefix /16 is another way of expressing the subnet mask and matches the number of network bits that are set to binary 1 in the subnet mask
#### Calculating the Network address
- 1 AND 1 = 1, the rest 0
![[Pasted image 20241007160542.png]]
> Notice the /16

![[Pasted image 20241007160645.png]]
> Conversion to dotted decimal
### Subnets
![[Pasted image 20241007162836.png]]
>Flat topology
- Flat topology is an OSI Layer 2 - switch connected network where all devices see all the broadcasts in the Layer 2 broadcast domain
- Flat network design is easy to implement and manage, reducing cost, maintenance and administration
- Concerns:
	- Security
		- Because network is not segmented, you cannot apply security policies adapted to individual segments
		- If one device is compromised, it can quickly affect the whole network
	- Troubleshooting
		- Isolation of network faults is more challenging, especially in bigger flat networks because there is not logical separation or hierarchy
	- Address space utilization
		- Can end up with a lot of wasted IP addresses, cannot use addresses from this network anywhere else
	- Scalability and speed
		- A flat network represents a single Layer 2 broadcast domain
		- If there is a large amount of broadcast traffic, this can impose considerable pressure on the available resources
		- A single broadcast domain typically should not include more than a couple hundred of devices


![[Pasted image 20241007162806.png]]
> Segmented networks
- Benefits of segmented networks
	- Smaller networks are easier to manage and map to geographical or functional requirements
	- Better utilization of IP addressing space, because you can adapt subnets sizes
	- Enables to create multiple logical networks from a single network prefix
	- Traffic is reduced, which can improve performance
	- Easily apply network security measures at the interconnections between subnets than within a single large network

![[Pasted image 20241007163059.png]]
> Sample of a multiple subnetwork environments
> *Each subnetwork may be connected to the internet by a single router*
### Implementing Subnetting: Borrowing bits


### Benefits of VLSM and Implementing VLSM


### Private vs Public IPv4 Addresses


### Reserved IPv4 Addresses


### Verifying IPv4 Address of a host

