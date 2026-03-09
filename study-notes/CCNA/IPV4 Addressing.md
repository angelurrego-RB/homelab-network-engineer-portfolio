---
course: CCNA - Jeremy's IT Lab
video: 7
topic: IPV4 Addressing
date created: 2026-02-14
status: ✅ complete
last updated: 2026-02-18
tags:
  - ccna
  - ipv4
  - addressing
  - layer_3
---

# IPv4 Addressing

---

## 📝 Notes

- ## Review
	- Layer 3 (Routers) - Connectivity b/t end hosts on diff LANs 
		- Logical Addressing (IP)
		- Selects best path b/t source and destination 
- ## IPV4
	- 32 bits/4 bytes --> 4 octets --> written in decimal format
	- 192.168.1.254 **/24**
		- The /24 indicates that the first 24 bits of the IP is reserved for the network portion
		- 192.168.1 is the network portion (/24) and the .254 would be the host portion of the IP
- ## Address Classes
	- The first address in a network cant be used bc it is the network address (192.168.1.0 ≠ be used)
		- If the host portion is all 0s it is the Network Address
	- The last address in a network also cant be used bc it is the broadcast address (192.168.1.255 ≠ be used)
		- If the host portion is all 1s it is the Broadcast Address
	- Class A more address in a network (network portion smaller)
	- Class C can have more networks (larger network portion)
	- Max hosts per network = 2^n (n = # of host bits) - 2(broadcast and network address) = answer

| Class | First Octet Numerical Range | Realistic Range | First Octet | Prefix |
| ----- | --------------------------- | --------------- | ----------- | ------ |
| A     | 0 - 127                     | 0 - 126         | 0xxxxxxx    | /8     |
| B     | 128 - 191                   | 128 -191        | 10xxxxxx    | /16    |
| C     | 192 - 223                   | 192 - 223       | 110xxxxx    | /24    |
| D     | 224 - 239                   |                 | 1110xxxx    |        |
| E     | 240 - 255                   |                 | 1111xxxx    |        |

- ## Net masks

| Class | Prefix | Netmask       |
| ----- | ------ | ------------- |
| A     | /8     | 255.0.0.0     |
| B     | /16    | 255.255.0.0   |
| C     | /24    | 255.255.255.0 |

- ## Binary
	- Base 2 (each increment increases by 2)
	- EX. 192 --> 192-128 = 64 --> 64-64 = 0 --> 11000000


| **128** | **64** | **32** | **16** | **8** | **4** | **2** | **1** |
| ------- | ------ | ------ | ------ | ----- | ----- | ----- | ----- |
| 1       | 1      | 0      | 0      | 0     | 0     | 0     | 0     |

- ## Configuring IPv4 on a Router 
	- ```
	  Router>en 
	  Router#conf t
	  Router(config)#hostname R1
	  R1(config)#interface gigabitethernet0/0
	  R1(config-if)#ip address 10.255.255.254 255.0.0.0
	  R1(config-if)#description ## to PC1 ##
	  R1(config-if)#no shutdown
	  R1(config-if)#do sh ip int br
	  R1(config-if)#end
	  R1#do show running config
	  R1#write memory
	  
	  
	  %% R1>/R1# is the device (don't type) %%
	  ```
	- `en %% short cut to--> enable %%` - enter privileged exec mode
	- `conf t %% short cut to--> configure terminal %%` - enters global configure mode
	- `hostname R1` - changes routers/devices name to R1
	- `int g0/0 %% short cut to--> interface gigabitethernet0/0 %%` - enters interface configure mode in the interface to configure (gigabitethernet 0/0)
	- `ip address ip_address subnet_mask` - configures ip (10.255.255.254) to interface, then specify the subnet mask (255.0.0.0 can't write as /8, /16, /24, etc)
	- `description ## to PC1 ##` - adds a description to the interface ('## ##' is just for visual purposes not required)
	- `no shutdown` - enables the interface
	- `do sh ip int br %% short cut to--> show ip interface brief%%` - confirm/check status of each interface & IP addresses
		- `Interface` column - Lists network interfaces on the device 
		- `IP-Address` column - Lists assigned IPs 
		- `OK?` - Legacy command (not relevant)
		- `Method` - Method interface was assigned an IP
		- `Status` - Layer 1 status of the interface 
			- up = cable connected
			- administratively down = interface disabled with `shutdown` command
				- Default for Cisco routers
				- Not the default for Cisco switches (up or down)
		- `Protocol` - Layer 2 status of the interface (if Layer 1 is down, this will also be down)
	- `end` - goes back into privileged exec mode 
	- `do show running config` - see all the configs for each interfaces, descriptions, duplex & speed
	- `write memory` - saves the configuration to the device


---
