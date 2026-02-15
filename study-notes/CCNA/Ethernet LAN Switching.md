---
topic: Ethernet LAN Switching
video: 5
date: 2026-02-14
last updated: 2026-02-14
tags:
  - ccna
  - OSI
  - Ethernet
  - Switching
  - layer_2
---

# Quick Reference

- ### Review:
	- Layer 1 Physical
		- Cables, voltage levels, max transmission distances, physical connectors
		- Bits converted to electrical or radio signals
	- Layer 2 Data Link
		- Node to Node connectivity & data transfer
		- How data is formatted
		- Detected and corrects Physical Layer 1 errors 
		- Uses layer 2 addressing (IP is Layer 3)
	- LAN 
		- Local Area Network
		- Network contained inside another network
	- PDUs
		- Protocol Data Units - different stages of preparing data to be forwarded (encapsulation)
		- Layer 2 --> Frame (used in almost every LAN today)
		- Layer 3 --> Packet
		- Layer 4 --> Segment
		- Layer 5 --> Data
- ### **Key Concepts**:
	- #### Ethernet Frame
		- Size of Header and trailer is 18 bytes (Preamble & SFD generally not considered part of the the Ethernet header)
		- Minimum size of **Frame** is 64 bytes (Header + Payload/Packet + Trailer)
		- Minimum size of **Payload** is 46 bytes (64-18 bytes)
		- **Ethernet Header**
			- Preamble - Allow receiving to devices to prepare to receive the data
			- SFD (Start Frame Delimiter)- Synchronization, allow receiving device to prepare to receive data
			- Destination
			- Source
			- Type (sometimes length) - layer 3 protocol used in the packet EX. IPV4/IPV6 (length --> length of encapsulated data)
		- **Ethernet Trailer**
			- FCS (Frame Check Sequence) - in receiving device to detect errors in transmission
		- **Preamble**
			- 7 bytes long (56 bits)
			- Alternating 1 & 0 (10101010 * 7)
			- Allows devices to sync their receiver clocks
		- **SFD** 
			- 1 byte (8 bits)
			- 10101011 (ending in 1 unlike the Preamble)
			- Marks the end of the preamble & beginning of the rest of the frame
		- **Destination & Source**
			- 6 bytes (48 bit)
			- Devices sending and receiving the frame 
			- Consists of the MAC Addresses
		- **Type/Length**
			- 2 bytes (16 bits)
			- Represent the type of encapsulated packet or length
				- Value ≤1500 indicates length in bytes
				- Value ≥1536 indicates type --> IPV4/IPV6 (length determined via other methods)
		- **FCS**
			- 4 bytes (32 bits)
			- Runs a CRC (Cyclic Redundancy Check) algorithm to detect errors over the receiving data
	- #### MAC Address (Media Access Control) 
		- 6 bytes (48 bit) address of physical device when made
		- BIA/Burn-In Address
		- FIRST 3 bytes are OUI (Organizationally Unique Identifier) assigned to company making the devices
		- LAST 3 bytes unique to the device itself
		- Written as 12 hexadecimal characters
		- Unicast Frame - a frame destined for a single target
		- 
	- #### MAC Address In Action
		- Dynamically learned/Dynamic MAC address
			- Every switch keeps a MAC Address table & stores MAC by looking at frames received  
		- Unknown Unicast Frame = Flood - copies the frame and sends it out to all active interfaces except the one that sent it
		- Known Unicast Frame = Forward - sends the frame to the KNOWN MAC address thats store in the MAC Address Table
			- MAC Addresses removed from table after 5 minutes of inactivity
		- When a device sends data to another device an IP packet is encapsulated with that frame 
			- Includes source and destination IP Address
		- When sending a computer doesn't know the destination PCs MAC Address
		- ARP (Address Resolution Protocol)
			- To discover Layer 2 address (MAC) of a know Layer 3 address (IP)
			- Broadcast - send to all host on the network
			- Broadcast MAC Address = FFFF.FFFF.FFFF
			- ARP request = broadcast![[Screenshot 2026-02-14 at 5.40.59 PM.png]]
			- ARP reply = unicast![[Screenshot 2026-02-14 at 5.39.49 PM.png]]

	- #### ping
		- Network utility used to test reachability 
		- Measures round-trip time
		- 2 messages 
			- ICMP Echo Request
			- ICMP Echo Reply
- ### Interview Answer:
	- "10/100/1000BASE-T means the port auto-negotiates speed from 10 Mbps up to 1 Gbps. Auto MDI-X means it automatically detects cable type so you can use straight-through cables anywhere."


---

# Commands
- ARP Table
	- `arp -a` --> Windows, MacOS, Linux
	- `show arp` --> Cisco CLI
	- Int. Address - IP
	- Physical Address - MAC
	- Type:
		- Static - default entry
		- Dynamic - learned via ARP
- `ping (IP-address)` 
	- same in all
	- Ex. `ping 8.8.8.8` (google.com)
	- Used to test reachability 
- `show mac address-table` --> Cisco CLI
	- View the MAC Address Table
- `clear mac-address-table dynamic` --> Cisco CLI
	- Clear MAC Address table
	- `clear mac-address-table dynamic address (mac address)` --> specific address to clear
	- `clear mac-address-table dynamic interface (interface-id)` --> specific MAC interface to clear
	
- 