# Networking Fundamentals
## Basic Networking Terms
### Network: 
A computer network is a digital telecommunications network for sharing resources between nodes(computing devices) that use common telecommunication technology.

### Network Interface Controller (NIC):
It is the card in computers and laptops which has **MAC Address**, using which communication happens

### MAC Address:
A media access control address is a unique identifier assigned to a network interface controller for use as a network address in communications within a network segment. This use is common in most IEEE 802 networking technologies, including Ethernet, Wi-Fi, and Bluetooth.

MAC Address Burned Reference stored in Hardware's read-only memory by firmware mechanism. So that the original MAC Address stays with the hardware.

### Data Transmission:
Electrical signals were used as mode of transmission and cables were the means of transmission.

Different types of cables from 10Base5, 10Base2, UTP (Unshielded Twisted Pair), Fiber cables (single mode, multimode) are used based on the devices and their interfaces.

### Client and Server:
<dl>
  <dt>Server</dt>
  <dd>It is a program or device that provides functionality for other programs or devices (clients).</dd>
  <dt>Client</dt>
  <dd>It is a piece of computer or software that accesses a service which is made avaialble by a server. </dd>
</dl>

### Protocol:
Set of rules on which communication happens is defined as protocol.

For Example: English language acts as protocol between me (typing this text) and you (reading the text).

### Port:
+ It is the communication endpoint.
+ It is a 16 bit unsigned integer from `1` to `65535`
+ Few Predefined ports are:
	+ HTTP - 80
	+ HTTPS - 443
	+ FTP - 20

### DHCP:
DHCP is a network management protocol used on IP networks where a DHCP server dynamically assignas an IP address and other network configuration parameters to each device connected to a network so they can communicate with other IP networks.

In absence of DHCP server, a computer needs to be manually assigned an IP address or it can use a special local link IP address to allow communication on the local network.

### Attenuation: 
Reduction in strength or intensity of the signal as it's transmission distance increases.

## Network Devices:
### Repeater:
+ Repeats the signal from one port to another port.
+ It amplifies the signal strength without analysing the data in signal.
+ It has only `2` ports and a power source.
+ There exists a special type of repeater which has more than `2` ports, it is called as **Hub**.
+ It is a Layer 1 device (Physical Layer).


### Hub:
+ It acts just like repeater, but with multiple ports.
+ Repeats signal to all other ports without understanding the signal.
+ Usually has 24 ports.
+ Wi-Fi is a hub in air.

### Switch:
+ Switch has intelligence, unlike Hub.
+ It uses a **MAC Address Table** and sends **Frames** to only where it has to be sent.
+ Number of ports may vary depending on manufacturer and product.
+ It is mainly used in **Local Area Network**
+ It is a Layer 2 device (Data Link Layer).

### Bridge:
+ Bridge acts a intermediate between Switch and Hub.
+ Also a Layer 2 device.

### Routers:
+ Allows us to route from one network to another network.
+ It is used to connect LAN's to Internet (WAN).

### Firewall:
+ Based on the rules defined, inbound and outbound traffic can be regulated.
+ It acts as a switch in network, monitoring the traffic.

### Access Points:
+ They are used to manage multiple devices connected to WAN Controller.
#### IDS (Intrusion Detection System):
+ It detects and alerts if any unwanted traffic is trying to enter a network
+ Just like Alarm, just detects the intruder.

#### IPS (Intrusion Prevention System):
+ It detects and prevents the unwanted traffic entering the network.
+ Offers better security than IDS.