---
course: CCNA - Jeremy's IT Lab
video: 9
topic: Switch Interfaces & Config
date created: 2026-03-06
status: ✅ complete
last updated: 2026-03-06
tags:
  - ccna
  - interfaces
  - switching
  - layer_2
  - configure
---

# Switch Interface Configurations

- ## Concepts:
	- Used to connect end hosts to
	- No shutdown command applied, meaning can be plug and play
		- Would be in the up/up state (Status & Protocol) when a device is connected
		- When a device is not connected it would be down/down, which is different than administratively down (shutdown command)
	- Can configure an IP Address (Layer 3) on most modern switch, which would be multi-layer switching
	- ### Duplex
		- Full - send and receive data at the same time
		- Half - can't send and receive data at the same time. Has to wait to receive the frame in order to send a frame.
	- ### CSMA/CD (Carrier Sense Multiple Access with Collision Detection) 
		- Before sending frame devices look at the collision domain to detect that other devices aren't sending frames
		- When a collision occurs the device send a jamming signal to the other devices to inform them of the collision, each device then waits a period of time before sending again.
		- Hubs - flood the interfaces which can lead to a collision between 2 devices sending data at the same time
		- Switch's CD 
			- If 3 devices are connected to a switch then instead of 1 collision domain(like a hub), each interface has its own collision domain (3 CD)
			- Means devices can operate in full duplex and send data freely
			- Collisions are rare and probably a misconfiguration when it does happen
	- ### Speed & Duplex Auto-negotiation
		- Interfaces can run at different speed (Auto)
		- Interfaces show their capabilities to the neighboring device, then negotiates best speed & duplex settings they are both capable of 
		- If auto-negotiation is off?
			- If a switch fails to sense the speed it will use the lowest supported speed
			- If speed is 10 or 100 Mbps, switch will use half duplex. 1000 Mbps or higher will use full duplex.
			- Duplex mismatch can cause collisions to occurs

- ## Switch Configuration
	 ```
	  Switch>en
	  Switch#conf t
	  Switch#show interfaces status
	  Switch(config)#hostname SW1
	  SW1(config)#int f0/1
	  SW1(config-if)#speed 100
	  SW1(config-if)#duplex full
	  SW1(config-if)#desc ## to R1 ##
	  SW1(config-if)#interface range f0/5 - 12
	  SW1(config-if-range)#shutdown
	  SW1(config-if-range)#desc ## not in use ##
	  
	 ```
	- `do show interfaces status` - shows each port, name/description, status, Vlan, Duplex, Speed, and Type
		- `Port` - each interface
		- `Name` - the interface description
		- `Status` - connected or unconnected
		- `Vlan` - divides LANs into smaller LANs. Default Vlan is 1
		- `Duplex` - is whether a device is capable of sending and receiving data at the same time, auto by default and when connected negotiates. Ex. a-full & a-half(can't send and receive simultaneously)
		- `Speed` - auto by default when connected uses fastest speed the device is capable. Ex. a-10(10 Mbps) & a-100(100 Mbps).
		- `Type` - RJ45 copper or SFP. Ex. 10/100BaseTX
	- `interface f0/1` - interface to configure
	- `speed 100` - forces 100 Mbps on the interface, can be 10/100/AUTO
	- `duplex full` - forces full duplex on the interface, full/half/AUTO
	- `interface range f0/5 - 12` - configures the all the interfaces within that range, can use different ranges. Ex. `int range f0/5 - 6, f0/9 - 12`
	- `shutdown` - disables the interface(s)(administratively down), good practice to do on unused interfaces for security

- ## Interface Errors(same on a Router)
	- `do show interfaces` - command to view errors and other information about each interface
		- `Runts` - frames smaller than the min frame size (64 bytes)
		- `Giants` - frames larger than the max frame size (1518 bytes)
		- `CRC` - frames that failed the CRC check (Ethernet FCS trailer) used to detect errors
		- `Frame` - frames that have and incorrect format (due to an error)
		- `Input Errors` - total of the various counters
		- `Output Errors` - frames switch tried to send (failed due to an error)
---
