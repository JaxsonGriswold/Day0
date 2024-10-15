zest 467accfb25050296431008a1357eacb1
pasta 05e5fb96e2a117e01fc1227f1c4d664c
hangry 9f7a33941828bdafd2755fd20176cdf4
neighbor d3b88e04de1e76482a1972f36734a7d8

AN EXAMPLE OF TUNNELING THROUGH A NEWTWORK WITH REV AND STRIGHT TUNNELS

1.  IH> telnet 10.50.40.12                                                    #here we are telneting to the .12 to create a reverse tunnel

2.  SSH1>  ssh student@10.50.36.109 -R 41399:localhost:22 -NT                 #here we are making the reverse tunnel back to our <IH> opening a new port 41399 on the IH leading to 22 on SSH1

3.  IH>  ssh net4_student13@localhost -p 41399 -L 41309:192.168.0.40:5555 -NT #here we are tunneling to SSH4 to get into the internal network from IH new port 41309

4. IH> ssh net4_student@localhost -p 41309 -L 41310:172.16.0.60:23 -NT        #here we are making a tunnel to the SSH6 get it ready to do a reverse tunnel

5. IH> telnet localhost 41310                                                 #here we are telneting into ssh6 to set up reverse tunnel

6. SSH6> ssh net4_student13@192.168.0.40 -p 5555 -R 41398:localhost:22 -NT    #here we are making the reverse tunnel to the SSH4

7. IH> ssh net4_comrade13@localhost -p 41309 -L 41311:localhost:41398 -NT     #here we are connecting to the SSH4 where we point to there port 41398 that point to the SSH6

8. IH> ssh net4_comrade13@localhost -p 41311 -L 41312:172.16.0.90:2222 -NT    #this makes a tunnel to ssh9 

9. IH> ssh net4_comrade13@localhost -p 41312 -L 41313:172.16.0.100:23 -NT     #this makes a tunnel to ssh10 to there telnet 

10. IH> telnet localhost 41313                                                #this will telnet into the ssh10 and now we can run our commands 

#this is a way to tunnel through a network and this follows the draw.io networkmap#
continue as followed for any further networks 




HOLY HELL LETS HOPE THIS GOES WELL...

bit example 
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/Bits_Nibbles_Bytes.png


Common Formats

Base 2 - Lowest level format and is the base language used by computer systems. Uses a series of "0" and "1" in groupings of 8-bits or 1 byte.

01000010 01100001 01110011 01100101 00100000 00110010

Base 10 - Basis for the numbering system used by humans.

66 97 115 101 32 49 48

Base 16 - Used by computers and humans to express larger decimal numbers or long streams of binary into more manageable groupings.

42 61 73 65 20 31 36

Base 64 - Like HEX, it allows groupings up to 6-bits of binary (0-63 decimal). Characters used are (A-Z), (a-z), (0-9), and (+, /). That is (26) + (26) + (10) + (2) respectively. 
In order to be compatible with binary, it uses 4 groupings of 6-bits (24 total bits) so that it will equate to 3 bytes of binary ( 24 bits). For data not consuming the full 24-bits, 
it will use "=" signs for each 6 unused bits at the end as padding.

QmFzZSA2NA==  #if using base 64 make sure to use "==" at the end 


OSI MODEL ######
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/OSI.png

Web Request Example

Application Layer: A user requests their browser to download a file from a web site. The HTTP protocol handler at this layer recognizes the secure request for a file on the web server and passes the request to the TLS Library.
#data#

Session and Presentation Layer: The TLS library needs to create a secure channel for communication which requires the establishment of a connection with the destination. It passes a connection request to TCP.
#data#

Transport Layer: The TCP handler receives the connection requests and creates a segment with the SYN flag (first part of the three-way handshake) set to the distant end server. The upper layer data is encapsulated with a TCP header and the segment is passed down to IP at the network layer.
#TCP# has to have 3 way handshake   #UDP# does not three way handshake  #segment#

Network Layer: The network layer receives the segment and creates a packet by encapsulating the TCP header and data payload in an IP header. The correct IP information is added to the header for the destination IP address. The packet is then passed down to the Data-Link layer.
#packet#

Data-Link Layer: The data-link layer creates a frame encapsulating the data payload, TCP header, and IP header. The destination MAC address of the router is added to send the frame to it’s local destination. In addition to a header a trailer/footer is added containing a checksum and padding if needed to aid in frame synchronization. This is then passed to the physical layer.
#frame#

Physical Layer: The physical layer takes the binary data and injects it onto the physical media for which transmission is taking place (wireless or wired)
#bits#

###########################
OSI Layer	         PDU	         Common Protocols
7 - Application    Data          DNS, HTTP, TELNET

6 - Presentation   Data          SSL, TLS, JPEG, GIF

5 - Session        Data          NetBIOS, PPTP, RPC, NFS

4 - Transport      Segment/Datagram      TCP, UDP

3 - Network        Packet        IP, ICMP, IGMP

2 - Data Link      Frames        PPP, ATM, 802.2/3 Ethernet, Frame Relay

1 - Physical       Bits          Bluetooth, USB, 802.11 (Wi-Fi), DSL, 1000Base-T

#########################
Internet Standards Organizations
IETF        https://www.ietf.org/standards/

IANA        https://www.iana.org/


IEEE        https://www.ieee.org/
            https://en.wikipedia.org/wiki/Institute_of_Electrical_and_Electronics_Engineers
            https://en.wikipedia.org/wiki/IEEE_Standards_Association



#########################

Data Link Sub-layers

Data link layer is unique because it has the function to communicate in "logical" and "physical". 
To accommodate this the functionality of this layer is divided into two logical sub-layers. 
An upper sub-layer, LLC, to interact with the network layer above and a lower sub-layer, MAC, to interact with the physical layer.

MAC (Media Access Control)

Act as a sublayer governing protocol access to the physical medium, physical addressing, and acts as an interface between the LLC and physical layer. 
Most of the frame construction happens at this layer.

LLC (Logical Link Control)

Manages communication between devices over a single link of the network that includes error checking and data flow. 
This layer provides the Ethertype to the MAC sublayer in the frame construction to identify the encapsulated protocol.
#############################
Ethernet Header

https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/Ethernet_II_Frame.png
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/EthernetFramePreamble.png

Ethertype (2 byte field)
Used to indicate the next protocol encapsulated in the frame.This is provided by the LLC sub-layer.

Common Ethertypes controlled by IANA.org:

0x0800 - IPv4

0x0806 - ARP

0x86DD - IPv6

0x8100 - VLAN Tagging 802.1q
#####
arp header 
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/ARP_Header.png

########################
IPv4 header 
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/IPv4_Header.png
#########################################################################################################################################################################
offset 
take the V and multiply by IHL feild 
V=4 IHL =F
0x4F = 60
sbtract 60 from 1500                                                                                                                               #this is important how to find offset ###
then take 1440 divide by 8
then you get offset of 180

################################################################################################################################################################################
ipv6
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/IPv6_Header.png

######################################

ICMP header 

https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/ICMPHeader.png

IPv4 auto config 
*APIPA
*RFC 3927

IPv6 auto config
*SLAAC
*RFC 4862

###############################################
TCP Header
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/TCPHeader.png

https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/TCPFlagsBPF.png

##################################################

state of tcp
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/TCPchart.png
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/TCPstates.png
#########################################################
UDP
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/UDPHeader.png
#############
session layer 

protocal Socks 4/5 (TCP 1080)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/socks.png
Initiates connections through a proxy
Uses various Client / Server exchange messages
Client can provide authentication to server
Client can request connections from server



protocal PPTP (TCP 1723)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/pptp.png
Specified in RFC 2637 Developed by Microsoft. Obsolete method to create VPN tunnels. Has many well know vulnerabilities.
PPTP Wiki Reference
PPTP Example PCAP from Cloudshark

protocal L2TP (TCP 1701)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/l2tp.png
Specified in RFC 2661 Has origins from Cisco’s L2F and Microsoft’s PPTP. Does not provide any encryption itself. Relies on other encryption methods for confidentiality.
L2TP Wiki Reference
L2TP Example PCAP from Cloudshark


protocal SMB/CIFS (TCP 139/445 AND UDP 137/138)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/smb.png
Allowed devices to establish connections to other devices on network to share files, printers and other things.
SMB Rides over Netbios - allows applications to communicate over a LAN using a NetBIOS name. Depricated due to DNS. Netbios Wiki
Netbios Dgram Service - UDP 138
Netbios Session Service - TCP 139
SAMBA and CIFS are just flavors of SMB (Samba Wiki)



protocal RPC (Any Port)
RPC is a request/response protocol.
RPC Wiki Reference
User application will:
Sends a request for information to a external server
Receives the information from the external server
Display collected data to User
Examples of RPC are:
SOAP - SOAP Example PCAP from Cloudshark
XML
JSON
NFS

###############################################
Presentation Layer (OSI Layer 6)

Presentation Layer — This layer deals with the Translating, Formatting, Encryption, and Compression of data.

Translation - The presentation layer is responsible for interoperability between encoding methods as different computers use different encoding methods. 
It translates data between the formats the network requires and the format at the computer.

Formatting - This layer is responsible to put the file in a format that is readable. Such as:

ASCII or EBCDIC
.doc, .ppt or .xls
mp3 or wav
avi or mp4
bmp, jpeg, gif, tiff or png


Encryption This is the layer the encryption and decryption gets carried out.
Symetric: AES, Blowfish, Twofish, DES, and RC4
Asymetric: PKI, Deffie-Hellman, DSS, RSA, Elliptic curve

Compression Sometimes data gets to big to transmit over the network so The Presentation layer handles compression.T
he primary role of Data compression is to reduce the number of bits to be transmitted. 
It is important in transmitting multimedia such as audio, video, text etc.
Zip, TAR, RAR, 7zip, CAB
##########################################################################
Application Layer (OSI Layer 7)
Session and Presentation layers may be discussed, and their functions explained, but do not require thorough coverage.

FTP (TCP 20/21)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/ftp.png
FTP
Published in RFC 959, File Transfer Protocol is a standard network protocol that is used for file transfer between a client and a server. 
Authentication is performed via a username and password, but can also be disabled in favor of anonymous mode if the FTP server is configured for it. 
The drawback with FTP is that all communication is clear text, including the initial authentication.

FTP has two modes of operation, Active and Passiv

Active
A client initiates a connection with a server on port 21 from the client’s ephemeral high port. 
The three way handshake is completed and the client listens on it’s ephemeral high port + 1, the client sends the port N+1 command to the server on port 21 (control port). 
Ex: if the command to the server is from ephemeral port 1026, it would listen on port 1027. 
Once that is done, the server initiates a connection to the client’s ephemeral high (1027) from the server’s data port (20) and the data is transferred.
## active is bad becuse the server it might not be allowed to send you data due to firewalls or ports. the server cant connect to your open port always ##
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/ftp_active.png

Passive
Passive FTP sidesteps the issue of Active mode by reversing the conversation. The client initiates both the command and data connections.
##passive mode is better becuse you have to reachout to the ftp server and grab the data from there random high port so that the firewall wont block it and you go out to grab it##
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/ftp_passive.png
(17,9,9,20,128,9) == IP: 17.9.9.20 port: "128" x 256 + "9"= 32777



SSH (TCP 22)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/ssh.png
SSH Protocol
SSH is an open protocol with many different implementations. Examples include PuTTy, Solaris Secure Shell, Bitvise, and OpenSSH. 
OpenSSH is the open source implementation that is most common and the focus of this course as it is widely found in Linux and Unix. 
Support for Windows was introduced when OpenSSH was ported to run in Windows Power Shell in 2015. It is included in Windows 10 as of 2018, though it must be enabled in settings.

ssh allows you to secure copy --- scp 
allows tunnling 
secure shell to run commands 

#####SSH Architecture######
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/ssh.png

Components of SSH Architecture
In order for ssh to work properly between a client and server, several components are required:

Server
Known as sshd in most linux SSH implementations, this allows incoming SSH connections and handles authentication and authorization.

Clients
This is the program that connects to the SSH server for a request, examples include scp and ssh

Sessions
The client and server conversation that begins after successful mutual authentication.

Keys
There are several keys that are used in SSH:

User Key - Asymmetric Public key created used to identify the user to a server (generated by the user)
Host Key - Asymmetric Public key created to identify a server to a user (generated by an administrator)
Session Key - Symmetric Key created by the client and the server that protects the communication for a particular session

Key Generator
Creates user keys and host keys via ssh-keygen

Known-hosts database
Collection of host keys that the client and server refer to for mutual authentication.

Agent
Stores keys in memory as a convenience for users to not input pass-phrases repetitively.

Signer
This is a program that signs the host-based authentication packets.

Random Seed
Random data used for entropy in creating pseudo-random numbers

Configuration File
Settings that exist on either the client or server that dictate functionality for ssh or sshd respectively




Telnet (TCP 23)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/telnet.png
unsecure in plane text but usfull to talk to mail server also banner grabbing 




SMTP (TCP 25)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/smtp.png
simple mail transfer protocal and talks to mail server 



TACACS (TCP 49) SIMPLE/EXTENDED
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/tacacs-s.png
CISCO proctocal



HTTP(S) (TCP 80/443)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/http.png
http is unencrypted and is in plain text
https is encrypted and is safer 
*messages for http 100,200,300,400


POP (TCP 110)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/pop.png
old mail server protocal
go to server and downlod mail



IMAP (TCP 143)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/imap.png
newer mail protocal and go to server and just read mail with no need to dowload the mail



 RDP (TCP 3389)
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/rdp.png
remote desktop protocal and is simple lol

DNS (QUERY/RESPONSE) (TCP/UDP 53)
this gives you the domain of an ip address 
can be used to query which is udp
and for download or transfer shit between dns server it would use tcp
https://net.cybbh.io/public/networking/latest/lesson-1-fundamentals/_images/dns.png




DHCP (UDP 67/68)
dYNAMICLY ASSIGNS IP ADDRESSES
DHCPv4              DHCPv6
Discover            Solicit 
Offer               Advertise 
Request             Request
Ack                 Reply
68-client
67-server


TFTP (UDP 69)
for file transfers and is very simple quick file transfers

NTP (UDP 123)
network time protocal
this makes sure the system has then same time and are synced across hosts


SNMP (UDP 161/162)
used for a centrelized location for managing networks and hosts 
allows to get stuff from places \


RADIUS (UDP 1645/1646 AND 1812/1813)
another centrilized server managment 


RTP (UDP ANY ABOVE 1023)
real time transport protocal
this allows for session managment 
such as voip and video calls

#############################################################################################

SWITCH OPERATIONS

Fast Forward - Only Destination MAC

Fragment Free - First 64 bytes

Store and Forward - Entire Frame and FCS

CAM TABLE
this allows a switch to store mac addresses 
this also allows the switch to forward mac addresses through the correct port 
Learn - Examining the Source MAC Address
Forward - Examining the Destination MAC Address


IEEE 802.1AD "Q-IN-Q"
this is for vlans 
like vlans inside of vlans 
0x88A8 = standerd double tag
0x9100 = non-standerd double tag


SPANNING TREE PROTOCOL (STP)
Root decision process

1. Elect root Bridge

2. Identify the Root ports on non-root bridge

3. Identify the Designated port for each segment

4. Set alternate ports to blocking state



LAYER 2 DISCOVERY PROTOCOLS
Cisco Discovery Protocol (CDP)

Foundry Discovery Protocol (FDP)

Link Layer Discovery Protocol(LLDP) open source 



DTP (DYNAMIC TRUNKING PROTOCOL)
access port for host 
trunk ports are for switches to switches and routers 


VTP (VLAN TRUNKING PROTOCOL)
this allows for automated trunking 
vtp server and vtp domains and vtp clients so there is a single place to update
not great for security 
if the server is compromised the clients are as well
if a new switch is added and it has the highest revison number it will take over all switches
Management domain
Configuration revision number
Known VLANs and their specific parameters


PORT SECURITY / Modes

shutdown - nothing will be passed 

restrict - stuff will get loged

protect - stuff will get logged and alerted 

####################################################################################################################
LAYER 3 ROUTING TECHNOLOGIES



Routing Table
The primary functions of a router are to:

Determine the best path to send packets

Forward packets toward their destination





ROUTING TABLES
Ultimate route is any routing table entry that has a next-hop IPv4 address, exit interface, or both.

Level 1 route is any route with the subnet mask (CIDR) is equal to or less than the classful mask of the network address. A level 1 route can be a:

Network route - A network route that has a subnet mask equal to that of the classful mask.

Class A - 255.0.0.0 (/8)

Class B - 255.255.0.0 (/16)

Class C - 255.255.255.0 (/24)

Supernet route - A network route with a mask less (smaller) than the classful mask.

Default route - A default route is a static route with the address 0.0.0.0/0.

Parent route is a level 1 network that is subnetted. A parent route will never be an ultimate route.

Level 2 child route are the subnets of a classful network address.
https://detailed.files.wordpress.com/2017/12/subnet-chart.jpg



LOOKUP PROCESS
Best Route = Longest Match

Routers compares the destination address in the incoming packet to its entries in the routing table.
It matches the address (bit by bit) to all the table entries and looks for the longest bit match it can find. 
Starting at the far left, it compares the bits up to the amounts of bits in the CIDR mask. 
(i.e. a /12 mask will match 12 bits and a /24 will match 24 bits.)


Routed vs Routing Protocols

Routed protocol is a protocol that allows data to be routed. 
These protocols provide an addressing scheme and sub-netting. 
The addressing scheme identifies the individual host and the network to which it belongs. 
Each host address bust be unique. All hosts on an internetwork must use the services of a routed protocol to communicate.

IPv4

IPv6

IPX

AppleTalk



Routing Protocol are used by routers communicate routing information with each other. 
Unless all routes are manually entered into the router, the router needs to learn from other routers about the networks that they know. 
They use this shared information to populate their routing tables so that they can make better decisions when forwarding routed protocols such as IPv4.

Routing protocols are broken down to 2 types:

            Interior Gateway Protocol (IGP) - is a type of protocol used for exchanging routing information between gateways (commonly routers) within an autonomous system

                        RIP (v1, v2, ng)

                        EIGRP and EIGRP or IPv6

                        OSPF (v2 and v3)

                        IS-IS

            Exterior Gateway Protocol (EGP) - is a routing protocol used to exchange routing information between autonomous systems

                        BGP




First Hop Redundancy Protocols

Hot Standby Router Protocol (HSRP) - A Cisco-proprietary FHRP designed to allow for transparent fail-over of IPv4 networks. 
One router interface will be set as "active" and the others set as "standby". Once the active interface will forward traffic to other networks. 
Standby interfaces serve as backups in case the active fails. Active interface sends multicast "Hello" packets to inform the backups that its still operational.

HSRP for IPv6 - Cisco-proprietary FHRP providing the same functionality as HSRP but for IPv6 addressing.

Virtual Router Redundancy Protocol version 2 (VRRPv2) - An open-standard FHRP similar to HSRP. Assigns the "Master" as the active forwarder and "backups".

VRRPv3 - VRRP for IPv6 addressing.

Gateway Load Balancing Protocol (GLBP) - another Cisco-proprietary FHRP like HSRP but adds the ability to have more than one Active forwarder. 
Incorporates the ability to load balance over all active interfaces rather than using just 1.

GLBP for IPv6 - CGLBP for IPv6 addressing.




Static vs Dynamic Routing
https://git.cybbh.space/net/public/raw/master/modules/networking/slides/images/AD.png


Routing protocols can learn of 2 or more routes to the same destination network. 
To determine which one is the "shortest", routing protocol uses metrics to determine the best path to a destination network. 
Routing protocols each uses different factors as its metrics to determine the best/shortest routes.

Some of the most common metrics that routing protocols can use are:

hop

bandwidth

delay

reliability

load

MTU

cost

administratively defined



Static Routing
            Static routing provides some advantages over dynamic routing, including:

                        Static routes do not advertise over the network, resulting in better security.

                        Static routes do not use bandwidth like dynamic routing protocols to send updates and no CPU cycles are used to calculate and communicate routes.

                        The path a static route uses to send data is predetermined.



            Static routing has the following disadvantages:

                        Initial configuration and maintenance is time-consuming.

                        Configuration is prone to error, especially on large networks.

                        Administrator must intervene to update routing information or to bypass network faults.

                        Does not scale well with growing networks; maintenance becomes cumbersome.

                        Requires complete knowledge of the whole network for proper implementation.



Dynamic Routing

Routing protocols allow routers to dynamically exchange routing information to build routing tables. 
If 2 or more routers share the same protocol they can communicate with each other. The purpose of dynamic routing protocols includes:

            Discover new remote networks

            Maintaining current routing information

            Choose best path to remote networks
            
            Recalculate a new patch to a remote network should the primary fail

Dynamic routing provides some advantages over static routing, including:

            Easier to configure and maintain.

            Administrator does not need to intervene to update tables during network outages.

            Scales very well on growing networks.

            Dynamic routing has the following disadvantages:
            
            Routing protocols flood the network updates which consumes bandwidth and can be intercepted.

            Uses extensive CPU and RAM to run its algorithms and build its databases.

            Path data can travel is not deterministic and can change fluidly.



BGP
Road-map of the Internet

Routes traffic between Autonomous System (AS) Number

Advertises IP CIDR address blocks

Establishes Peer relationships

Complicated configuration

Complicated and slow path selection




BGP OPERATION
How BGP chooses the best path:

Advertise a more specific route. 192.168.1.0 /24 is more specific than 192.168.0.0 /16.

Offer a shorter route to certain blocks of IP addresses. A route to ip prefix with 4 AS 'hops" is better than route with 5 AS 'hops'


BGP HIJACKING
Illegitimate advertising of addresses

BGP propagates false information

Purpose:

stealing prefixes

monitoring traffic

intercept (and possibly modify) Internet traffic

'black holing' traffic

perform MitM
###############################################################################



tcp dump 
-X or -XX     some dumb shit with dump
-XXvv     double verbose options and more info / integrety cheching
-XXvvn 
-XXvvn -w     writes to a pcap file then name file right after 
-XXnnn -r     then write the name of the pcap

can combine commands
sudo tcpdump -i eth0 -XXvvn not tcp port 22




BERKELEY PACKET FILTERS (BPF)
Requests a SOCK_RAW socket and setsockopt calls SO_ATTACH_FILTER

sock = socket(PF_PACKET, SOCK_RAW, htons(ETH_P_ALL))
...
setsockopt(sock, SOL_SOCKET, SO_ATTACH_FILTER, ...)


BERKELEY PACKET FILTERS
Using BPFs with operators, bitmasking, and TCPDump creates a powerful tool for traffic filtering and parsing.

tcpdump {A} [B:C] {D} {E} {F} {G}

A = Protocol (ether | arp | ip | ip6 | icmp | tcp | udp)
B = Header Byte offset
C = optional: Byte Length. Can be 1, 2 or 4 (default 1)
D = optional: Bitwise mask (&)
E = Operator (= | == | > | < | <= | >= | != | () | << | >>)
F = Result of Expresion
G = optional: Logical Operator (&& ||) to bridge expressions

Example:
tcpdump 'ether[12:2] = 0x0800 && (tcp[2:2] != 22 && tcp[2:2] != 23)'

BITWISE MASKING
To filter down to the bit(s) and not just the byte.

ip[0] & 0x0F > 0x05
ver ihl bpf
FILTER LOGIC - MOST EXCLUSIVE
All designated bit values must be set; no others can be set

tcp[13] = 0x11
--or--
tcp[13] & 0xFF = 0x11


find ALL TTL LESS THAN 64
sudo tcpdump -n 'ip[8] <= 0x40 || ip6[7]<=0x40' -r BPFCheck.pcap

################################################################################################################
   16  sudo tcpdump -n 'ip[8] <= 0x40 || ipv6[7]<=0x40
   17  sudo tcpdump -n 'ip[8] <= 0x40 || ipv6[7]<=0x40' -r BPFCheck.pcap 
   18  sudo tcpdump -n 'ip[8] <= 0x40 || ip6[7]<=0x40' -r BPFCheck.pcap 
   19  clear
   20  sudo tcpdump -n 'tcpdump -i eth0 'ip[6] & 0xE0 = 0x40'' -r BPFCheck.pcap 
   21  sudo tcpdump -n 'tcpdump -i eth0 'ip[6] & 0xE0 = 0x40' -r BPFCheck.pcap 
   22  sudo tcpdump -n 'ip[6] & 0xE0 = 0x40' -r BPFCheck.pcap 
   23  sudo tcpdump -n 'tcp[0:2] >1024' -r BPFCheck.pcap 
   24  sudo tcpdump -n 'tcp[0:2] >1024' -r BPFCheck.pcap | wc -l
   25  sudo tcpdump -n 'tcp[0:2] > 1024' -r BPFCheck.pcap | wc -l
   26  sudo tcpdump -n 'ip[0:2] > 1024' -r BPFCheck.pcap | wc -l
   27  sudo tcpdump -n 'tcp[0:2] > 1024 || udp[0:2] > 1024' -r BPFCheck.pcap 
   28  sudo tcpdump -n 'tcp[0:2] > 1024 || udp[0:2] > 1024' -r BPFCheck.pcap | wc -l
   29  sudo tcpdump -n 'ip[9]=0x11||ip6[6]=0x11' -r BPFCheck.pcap | wc -l
   30  sudo tcpdump -n 'tcp[13] 0x11=0x11 || tcp[13] 0x14=0x14' -r BPFCheck.pcap | wc -l
   31  sudo tcpdump -n 'tcp[13] 0x11 = 0x11 || tcp[13] 0x14 = 0x14' -r BPFCheck.pcap | wc -l
   32  sudo tcpdump -n 'tcp[13] & 0x11 = 0x11 || tcp[13] & 0x14 = 0x14' -r BPFCheck.pcap | wc -l
   33  sudo tcpdump -n 'tcp[13] = 0x11 || tcp[13] = 0x14' -r BPFCheck.pcap | wc -l
   34  sudo tcpdump -n 'ip[4:2]=0xd5' -r BPFCheck.pcap | wc -l
   35  sudo tcpdump -n 'ip[4:2]=0xD5' -r BPFCheck.pcap | wc -l
   36  sudo tcpdump -n 'ether[12:2]=0x8100' -r BPFCheck.pcap | wc -l
   37  sudo tcpdump -n 'tcp[0:2]=0x23||udp[0:2]=0x23' -r BPFCheck.pcap | wc -l
   38  sudo tcpdump -n 'tcp[0:2]=53||udp[0:2]=53' -r BPFCheck.pcap | wc -l
   39  sudo tcpdump -n 'tcp[0:2]=23||udp[0:2]=23' -r BPFCheck.pcap | wc -l
   40  sudo tcpdump -n 'tcp[0:2]=0x23||tcp[2:2]=0x23||udp[2:2]=0x23||udp[0:2]=0x23' -r BPFCheck.pcap | wc -l
   41  sudo tcpdump -n 'tcp[0:2]=0x23||tcp[2:2]=0x23||udp[2:2]=0x23||udp[0:2]=23' -r BPFCheck.pcap | wc -l
   42  sudo tcpdump -n 'tcp[0:2]=0x23||tcp[2:2]=0x23||udp[2:2]=23||udp[0:2]=23' -r BPFCheck.pcap | wc -l
   43  sudo tcpdump -n 'tcp[0:2]=53||tcp[2:2]=53||udp[2:2]=53||udp[0:2]=53' -r BPFCheck.pcap | wc -l
   44  sudo tcpdump -n 'tcp[13]=0x02' -r BPFCheck.pcap | wc -l
   45  sudo tcpdump -n 'tcp[13]=0x12' -r BPFCheck.pcap | wc -l
   46  sudo tcpdump -n 'tcp[13]=0x01' -r BPFCheck.pcap | wc -l
   47  sudo tcpdump -n 'tcp[13]=0x11' -r BPFCheck.pcap | wc -l
   48  sudo tcpdump -n 'tcp[13]=0x04' -r BPFCheck.pcap | wc -l
   49* sudo tcpdump -n 'tcp[2:2]=' -r BPFCheck.pcap | wc -l
   50  sudo tcpdump -n 'tcp[0:2]=80||tcp[2:2]=80' -r BPFCheck.pcap | wc -l
   51  sudo tcpdump -n 'tcp[0:2]=23||tcp[2:2]=23' -r BPFCheck.pcap | wc -l
   52  sudo tcpdump -n 'ether[12:2]=0x800' -r BPFCheck.pcap | wc -l
   53  sudo tcpdump -n 'ether[12:2]=0x806' -r BPFCheck.pcap | wc -l
   54  sudo tcpdump -n 'ip[6]=0x80' -r BPFCheck.pcap | wc -l
   55  sudo tcpdump -n 'ip[9]==0x14' -r BPFCheck.pcap | wc -l
   56  sudo tcpdump -n 'ip[9]=0x14' -r BPFCheck.pcap | wc -l
   57  sudo tcpdump -n 'ip[9]==0x14' -r BPFCheck.pcap | wc -l
   58  sudo tcpdump -n 'ip[9]=16' -r BPFCheck.pcap | wc -l
   59  sudo tcpdump -n 'ip[1]=37' -r BPFCheck.pcap | wc -l
   60  sudo tcpdump -n 'ip[1] >> 2 = 37' -r BPFCheck.pcap | wc -l
   61  sudo tcpdump -n 'tcp[18:2] > 0' -r BPFCheck.pcap | wc -l
   62  sudo tcpdump -n 'tcp[18:2] > 0 && tcp[13]=0xff' -r BPFCheck.pcap | wc -l
   63  sudo tcpdump -n 'tcp[18:2] > 0 && !tcp[13]=0x20' -r BPFCheck.pcap | wc -l
   64  sudo tcpdump -n 'ip[16:4]&0xFFFFFF00=0x0A0A0A0A' -r BPFCheck.pcap | wc -l
   65  sudo tcpdump -n 'ip[16:4]&0xFFFFFF]=0x0A0A0A0A' -r BPFCheck.pcap | wc -l
   66  sudo tcpdump -n 'ip[16:4]&0xFFFFFF=0x0A0A0A0A' -r BPFCheck.pcap | wc -l
   67  sudo tcpdump -n 'ip[16:4]0xFFFFFF=0x0A0A0A0A' -r BPFCheck.pcap | wc -l
   68  sudo tcpdump -n 'ip[16:4]&0xFFFFFFFF=0x0A0A0A0A' -r BPFCheck.pcap | wc -l
   69  sudo tcpdump -n 'tcp[18:2] > 0 && !tcp[13]=0x20' -r BPFCheck.pcap | wc -l
   70  sudo tcpdump -n 'tcp[18:2] > 0 && tcp[13]!=0x20' -r BPFCheck.pcap | wc -l
   71  sudo tcpdump -n 'tcp[18:2] > 0 && tcp[13]&0x20!=0' -r BPFCheck.pcap | wc -l
   72  sudo tcpdump -n 'tcp[18:2] > 0 && tcp[13]&0x20!=1' -r BPFCheck.pcap | wc -l
   73  sudo tcpdump -n 'tcp[18:2] > 0 && tcp[13] & 20 !=1' -r BPFCheck.pcap | wc -l
   74  sudo tcpdump -n 'tcp[18:2] > 0 && tcp[13] & 20 !=0' -r BPFCheck.pcap | wc -l
   75  sudo tcpdump -n 'tcp[18:2] ! = 0 && tcp[13] & 0x20 = 0' -r BPFCheck.pcap | wc -l
   76  sudo tcpdump -n 'tcp[18:2] != 0 && tcp[13] & 0x20 = 0' -r BPFCheck.pcap | wc -l
   77  sudo tcpdump -n 'tcp[13]=0 && ip[16:4]&0xFFFFFFFF=0x0A0A0A0A' -r BPFCheck.pcap | wc -l
   78  ether[12:4] & 0xffff0fff = 0x81000001 && ether[16:4] & 0xffff0fff = 0x8100000A
   79  sudo tcpdump -n 'ether[12:4] & 0xffff0fff = 0x81000001 && ether[16:4] & 0xffff0fff = 0x8100000A' -r BPFCheck.pcap | wc -l
   80  sudo tcpdump -n 'ip[8] = 0x04' -r BPFCheck.pcap | wc -l
   81  sudo tcpdump -n 'ip[9]=0x01 && (ip[8]=0x04 || ip[8]=0x01 ' -r BPFCheck.pcap | wc -l
   82  sudo tcpdump -n 'ip[9]=0x01 && ip[8]=0x01 ' -r BPFCheck.pcap | wc -l
   83  sudo tcpdump -n 'ip[9]=0x01&&(ip[8]=0x01||ip[9]=0x14 ' -r BPFCheck.pcap | wc -l
   84  sudo tcpdump -n 'ip[9]=0x01&&(ip[8]=0x01||ip[9]=0x14)' -r BPFCheck.pcap | wc -l
   85  sudo tcpdump -n 'ip[9]=0x01&&(ip[8]=0x01||ip[9]=0x17)' -r BPFCheck.pcap | wc -l
   86  sudo tcpdump -n 'ip[8]=0x01&&(ip[9]=0x01||ip[9]=0x17)' -r BPFCheck.pcap | wc -l
   87  sudo tcpdump -n 'ip[8]=1&&(ip[9]=0x01||ip[9]=0x17)' -r BPFCheck.pcap | wc -l
   88  sudo tcpdump -n 'ip[8]=1&&(ip[9]=0x01||ip[9]=0x11)' -r BPFCheck.pcap | wc -l



#####################################################################################################################




SOCKET TYPES
Stream Sockets - Connection oriented and sequenced; methods for connection establishment and tear-down. Used with TCP, SCTP, and Bluetooth.

Datagram Sockets - Connectionless; designed for quickly sending and receiving data. Used with UDP.

Raw Sockets - Direct sending and receiving of IP packets without automatic protocol-specific formatting.


USER SPACE VS. KERNEL SPACE SOCKETS
     User Space Sockets

            Stream Sockets

            Datagram Sockets

    Kernel Space Sockets

            Raw Sockets


SOCKET CREATION AND PRIVILEGE LEVEL
User Space Sockets - The most common sockets that do not require elevated privileges to perform actions on behalf of user applications.

Kernel Space Sockets - Attempts to access hardware directly on behalf of a user application to either prevent encapsulation/decapsulation or to create packets from scratch, which requires elevated privileges.


USER SPACE APPLICATIONS/SOCKETS
Using tcpdump or wireshark to read a file

Using nmap with no switches

Using netcat to connect to a listener

Using netcat to create a listener above the well known port range(1024+)

Using /dev/tcp or /dev/udp to transmit data




KERNEL SPACE APPLICATIONS/SOCKETS
Using tcpdump or wireshark to capture packets on the wire

Using nmap for OS identification or to set specific flags when scanning

Using netcat to create a listener in the well known port range (0 - 1023)

Using Scapy to craft or modify a packet for transmission

Using Python to craft or modify Raw Sockets for transmission

Network devices using routing protocols such as OSPF




UNDERSTANDING PYTHON TERMINOLOGY
Libraries

Modules

Functions

Exceptions

Constants

Objects

Types


NETWORK PROGRAMMING WITH PYTHON3
Network sockets primarily use the Python3 Socket library and socket.socket function.

import socket
  s = socket.socket(socket.FAMILY, socket.TYPE, socket.PROTOCOL)
THE SOCKET.SOCKET FUNCTION
Inside the socket.socket. function, you have these arguments, in order:

socket.socket([*family*[,*type*[*proto*]]])
family constants should be: AF_INET (default), AF_INET6, AF_UNIX

type constants should be: SOCK_STREAM (default), SOCK_DGRAM, SOCK_RAW

proto constants should be: 0 (default), IPPROTO_RAW



PYTHON3 LIBRARIES AND REFERENCES
Socket-------------https://docs.python.org/3/library/socket.html

Struct-----------------https://docs.python.org/3/library/struct.html

Sys---------------https://docs.python.org/3/library/sys.html

PYTHON3 LIBRARIES AND REFERENCES (CONT)
Errors-----------https://docs.python.org/3/tutorial/errors.html

Exceptions---------------https://docs.python.org/3/library/exceptions.html

STREAM AND DATAGRAM SOCKET DEMOS
Follow along with the instructor on the Internet Host




THE SOCKET.SOCKET FUNCTION
Inside the socket.socket. function, you have these arguments, in order:

socket.socket([*family*[,*type*[*proto*]]])
family constants should be: AF_INET (default), AF_INET6, AF_UNIX

type constants should be: SOCK_STREAM (default), SOCK_DGRAM, SOCK_RAW

proto constants should be: 0 (default), IPPROTO_RAW



#################################################################################################################3
#################################################################################################################
\#################################################################################################################
if tunnel is created set to loopback then the port is the port you set your tunnel to                                                                  for later use in tunneling
#################################################################################################################
#################################################################################################################
#################################################################################################################


TCP------nc -l -p 54321
UDP------nc -l -p 12345 -u 



************************************************************************************************************************
************************************************************************************************************************
************************************************************************************************************************
reconnaissance
************************************************************************************************************************
************************************************************************************************************************
************************************************************************************************************************
external passive
            DNS lookup
            whois
            job site listings

internal passive
            packet Sniffing

active external
            network scanning
active internal
            dns queries
            arp requests


dig google.com 

dig google.com SOA 
dig google.com MX

use the SOA 
dig axfr @ns1.google.com 
dig axfr @nsztm1.digi.ninja zonetransfer.me             # this will show all the stuff they are offering across the internet 


waybackmachine is a site that pulls back archives


Linux Ping Sweep
for i in {1..254} ;do (ping -c 1 192.168.1.$i | grep "bytes from" &) ;done
find devices on network

sudo namp -sT 10.50.44.119 -T4 -vv -p 21-23,80
sudo namp -sT 10.50.44.119,150,120 -T4 -vv -p 21-23,80
sudo namp -sF 10.50.44.119 -T4 -vv -p 21-23,80
sudo nmap -sX 10.50.44.119 -p 21-23,80 -T4
sudo nmap -sU -vv -T4 10.50.44.119 -p 21-23,80
          -sI zombie scan
sudo nmap -O 10.50.44.119
sudo nmap -A 10.50.44.119

echo " " | nc 10.50.44.119 25 # banner grabbing

echo " " | nc -zv 10.50.44.119 21-15

next recon methedology
host discovery
            nmap
            nc
            scan script
            ping sweep
port discovery
            nmap
            nc
            scan script
port validation
            banner grabbing using nc
follow on based on ports
            if 22 or 23 connect and passive recon
            if 21 or 80 wget -r IP_ADDRESS or wget -r ftp://IP_ADDRESS or firefox

hostname
interface and subnets
            ip addr
            ip route
            ip neigh
file of intrest 
            find command 

other listenning ports 
            ss -ntlp




#######################################################
file manipulation day

type "passive" when you first connect to a ftp server to enable passive mode

scp -P 1111 student


########################################################################
NETCAT TECHNEQES

NOD MAKING
mknod <name of pipe> p #the p option makes a pipe

TWO WAY TUNNALL for moving file

~~~ this is for if a person is calling to you
#this id on the relay side#            nc -lp 1234 0< | nc $$.$$.$$.$$ 2003 1> 
#this is on the recever side#          nc -lp 2003 > outfile.txt

~~~ you calling to person
#this id on the relay side#            nc $$.$$.$$.$$ 1234 0< | nc $$.$$.$$.$$ 2003 1> 
#this is on the recever side#          nc -lp 2003 > outfile.txt


############################################################################################
SSH TUNNELING

ssh student@172.16.82.106 -L 1111:loclhost:80 -NT             #-NT is no terminal so you dont fuck up the session
            #this opens a 1111 on our loopback and points to the 172. port 80

~~~~~~~~~~~
#tunnel type
ssh student@172.16.1.15 -L 1111:172.16.40.10:22 -NT
            #what this does send traffic through 172.16.1.15 and makes the .15 send traffic to the .10

ssh student@localhost -p 1111 -L 2222:172.16.82.106:80 -NT
            #this is making you ssh to your loopback which is the 1111, where 1111 sends the information to the .10 which is the third box.
            this forawrds info through the .10 to the .106 on its port 80.
            the 2222 which is also connected through the 1111 points to the .106
firefox localhost:2222
            #this opens firefox to the .106 box

~~~~~~~~~~~~~~~
Proxy chains
            default port 9050
            this allows you to dynamicly go to diffrent ports 
            the -D options says to use proxy chain on the box
ssh student@172.16.82.106 -D 9050 -NT

proxychains ./scan.sh 
            #this is like if you wanted to send a script to the .106
proxychains ssh student@10.10.0.40
            this send it all the way to the .106 then the 106 connects to .40

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

steps for recon and tunneling 

1. ssh student@172.16.82.106 -D 9050 -NT             #ssh to .106 
or 
1. ssh 172.16.82.106 -L 1111:192.168.1.10:22 -NT
2. ssh localhost -p 1111 -D 9050 


enumerating
2.proxychains wget -r ftp 192.168.1.10 # if not specifying ftp it will go http
or wget -r localhost:1111 or wget -r ftp://localhost:1111 
3.proxychains nc 192.168.1.10 21             #BANNER GRABBING            
4.proxychains ./netcat_scan.py             #scan network



trouble shooting 
ss -ntlp 
ss -antp

REverse of -L
Blue Host-1
ssh student@10.10.0.40 -R 1111:localhost:80 -NT
 #Creates a remote port on the remote’s local host that forwards to the target specified


finding shit on devices
1.  find / -name hint* 2> /dev/null

2.  find / -name flag* 2> /dev/null

making reverse tunnel
1. ssh net4_student13@10.3.0.10 -R 41300:10.2.0.1:22

making tunnel from int through t3 to t4
2. ssh net4_student13@10.50.42.216 -L 41301:localhost:41300

~~~~~
ssh to the t4 device 
3. ssh net4_student13@localhost -p 41301
~~~~~~~

ssh mutiple tunnels

1.  ssh net4_student13@10.50.42.216 -L 41303:localhost:22

2. ssh net4_student13@localhost -p 41303

3. ssh net4_student13@localhost -L 41304:10.4.0.1:22

4.ssh net4_student13@localhost -p 41303 -L 41305:localhost:41304
5. ssh net4_student13@localhost -p 41305 -D 9050

ssh net4_student13@localhost -p 41303 -L 41305:localhost:41304


###################################################
example
1. ssh net4_student13@10.50.42.216 -L 40306:10.4.0.1:22       #IH through T3 to Baja
2. ssh net4_student13@localhost -p 40306 -L 40307:10.5.0.1:22 #IH through Baja to t4





IT<>ssh net4_student13@localhost -p 41309 -L 41310:172.16.0.60:23 -NT

telnet localhost 41310

ssh net4_student13@192.168.0.40 -p 5555 -R 41398:localhost:22


ssh net4_student13@localhost -p 41309 -L 41311:localhost:41398 -NT


ssh net4_comrade13@localhost -p 41311 -D 9050

$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$
AN EXAMPLE OF TUNNELING THROUGH A NEWTWORK WITH REV AND STRIGHT TUNNELS

1.  IH> telnet 10.50.40.12                                                #here we are telneting to the .12 to create a reverse tunnel

2.  SSH1>  ssh student@10.50.36.109 -R 41399:localhost:22 -NT             # here we are making the reverse tunnel back to our <IH> opening a new port 41399 on the IH leading to 22 on SSH1

3.  IH>  ssh net4_student13@localhost -p 41399 -L 41309:192.168.0.40:5555 -NT #here we are tunneling to SSH4 to get into the internal network from IH new port 41309

4. IH> ssh net4_student@localhost -p 41309 -L 41310:172.16.0.60:23 -NT        #here we are making a tunnel to the SSH6 get it ready to do a reverse tunnel

5. IH> telnet localhost 41310                                             #here we are telneting into ssh6 to set up reverse tunnel

6. SSH6> ssh net4_student13@192.168.0.40 -p 5555 -R 41398:localhost:22 -NT #here we are making the reverse tunnel to the SSH4

7. IH> ssh net4_comrade13@localhost -p 41309 -L 41311:localhost:41398 -NT  #here we are connecting to the SSH4 where we point to there port 41398 that point to the SSH6

8. IH> ssh net4_comrade13@localhost -p 41311 -L 41312:172.16.0.90:2222 -NT #this makes a tunnel to ssh9 

9. IH> ssh net4_comrade13@localhost -p 41312 -L 41313:172.16.0.100:23 -NT # this makes a tunnel to ssh10 to there telnet 

10. IH> telnet localhost 41313 # this will telnet into the ssh10 and now we can run our commands 

#this is a way to tunnel through a network and this follows the draw.io networkmap#
continue as followed for any further networks 
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$

IPTABLES SYNTAX
iptables -t [table] -A [chain] [rules] -j [action]
Rules:

-i or -o [iface]
-s or -d [ip.add | network/mask]
-p [protocol(in ipv4 header)]

-m is used with:
  state --state [state]
  mac [--mac-source | --mac-destination] [mac]
  tcp | udp [--dport | --sport] [port | port1:port2]
  multiport [--sports | --dports | --ports]
                [port1,[port2,[port3:port15]]]
  bpf --bytecode [ 'bytecode' ]

[action] - ACCEPT, REJECT, DROP


%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

MODIFY IPTABLES
Flush table

iptables -t [table] -F
Change default policy

iptables -t [table] -P [chain] [action]
Lists rules with rule numbers

iptables -t [table] -L --line-numbers
Lists rules as commands interpreted by the system

iptables -t [table] -S
Inserts rule before Rule number

iptables -t [table] -I [chain] [rule num] [rules] -j [action]

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
NFTABLE
1. CREATE THE TABLE
nft add table [family] [table]
[family] = ip, ip6, inet, arp, bridge and netdev.

[table] = user provided name for the table.




2. CREATE THE BASE CHAIN
nft add chain [family] [table] [chain] { type [type] hook [hook]
    priority [priority] \; policy [policy] \;}
[chain] = User defined name for the chain.

[type] =  can be filter, route or nat.

[hook] = prerouting, ingress, input, forward, output or
         postrouting.

[priority] = user provided integer. Lower number = higher
             priority. default = 0. Use "--" before
             negative numbers.

; [policy] ; = set policy for the chain. Can be
              accept (default) or drop.

 Use "\" to escape the ";" in bash




3. CREATE A RULE IN THE CHAIN
nft add rule [family] [table] [chain] [matches (matches)] [statement]
[matches] = typically protocol headers(i.e. ip, ip6, tcp,
            udp, icmp, ether, etc)

(matches) = these are specific to the [matches] field.

[statement] = action performed when packet is matched. Some
              examples are: log, accept, drop, reject,
              counter, nat (dnat, snat, masquerade)



MODIFY NFTABLES
nft {list | flush} ruleset
nft {delete | list | flush } table [family] [table]
nft {delete | list | flush } chain [family] [table] [chain]



MODIFY NFTABLES
nft list table [family] [table] [-a]
Adds after position

nft add rule [family] [table] [chain] [position <position>] [matches (matches)] [statement]
Inserts before position

nft insert rule [family] [table] [chain] [position <position>] [matches (matches)] [statement]
Replaces rule at handle

nft replace rule [family] [table] [chain] [handle <handle>] [matches (matches)] [statement]
Deletes rule at handle

nft delete rule [family] [table] [chain] [handle <handle>]


%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

EXP:
sudo iptables -A INPUT -p tcp -dport 22 -j ACCEPT
sudo iptables -A OUTPUT -p tcp -sport 22 -j ACCEPT
sudo iptables -P INPUT DROP
sudo iptables -P OUTPUT DROP
sudo iptables -L   # list table
sudo iptables -L -n --line-numbers  # shows actual number assosiated with ports also shpws the line numbers 
sudo iptables -A INPUT -p tcp -m multiport --ports 22,23,80 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp -m multiport --ports 22,23,80 -j ACCEPT

NFT EXP:
sudo nft add table ip CCTC
sudo nft add chain ip MYTABLE input { type <filter> hook <input> priority <0>\;policy <accept> \; }

sudo nft add rule ip MYTABLE input tcp dport { ssh,telnet,http }
sudo nft add rule ip MYTABLE input tcp sport { 22,23,80 }


sudo nft add chain ip MYTABLE output { type <filter> hook <output> priority <0>\;policy <accept> \; }
sudo nft add rule ip MYTABLE output tcp dport { ssh,telnet,http }
sudo nft add rule ip MYTABLE output tcp sport { 22,23,80 }

#######################################################################################################################
student@blue-host-1-student-13:~$ sudo iptables-save > iptable.conf
student@blue-host-1-student-13:~$ cat iptable.conf 
# Generated by xtables-save v1.8.2 on Tue Oct 10 18:32:14 2023
*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT DROP [0:0]
-A INPUT -p tcp -m multiport --ports 22,23,3389,80 -m state --state NEW,ESTABLISHED -j ACCEPT
-A INPUT -p tcp -m multiport --ports 6579,4444 -j ACCEPT
-A INPUT -p udp -m multiport --ports 6579,4444 -j ACCEPT
-A INPUT -s 10.10.0.40/32 -p icmp -m icmp --icmp-type 8 -j ACCEPT
-A INPUT -s 10.10.0.40/32 -p icmp -m icmp --icmp-type 0 -j ACCEPT
-A OUTPUT -p tcp -m multiport --ports 22,23,3389,80 -m state --state NEW,ESTABLISHED -j ACCEPT
-A OUTPUT -p tcp -m multiport --ports 6579,4444 -j ACCEPT
-A OUTPUT -p udp -m multiport --ports 6579,4444 -j ACCEPT
-A OUTPUT -d 10.10.0.40/32 -p icmp -m icmp --icmp-type 8 -j ACCEPT
-A OUTPUT -d 10.10.0.40/32 -p icmp -m icmp --icmp-type 0 -j ACCEPT
COMMIT
# Completed on Tue Oct 10 18:32:14 2023

Your Host Filtering T1 Flag is:

467accfb25050296431008a1357eacb1
#########################################################################################################################
student@blue-int-dmz-host-1-student-13:~$ sudo iptables-save > iptable.conf
student@blue-int-dmz-host-1-student-13:~$ cat iptable.conf 
# Generated by xtables-save v1.8.2 on Tue Oct 10 18:52:08 2023
*filter
:INPUT DROP [797861:62279173]
:FORWARD DROP [0:0]
:OUTPUT DROP [837353:46589630]
-A INPUT -p tcp -m multiport --ports 22,23,3389,80 -m state --state NEW,ESTABLISHED -j ACCEPT
-A OUTPUT -p tcp -m multiport --ports 22,23,3389,80 -m state --state NEW,ESTABLISHED -j ACCEPT
COMMIT
# Completed on Tue Oct 10 18:52:08 2023

Your Host Filtering T3 Flag is:

05e5fb96e2a117e01fc1227f1c4d664c
########################################################################################################################3
table ip CCTC {
	chain input {
		type filter hook input priority 0; policy drop;
		tcp dport { ssh, telnet, http, 3389 } ct state { established, new } accept
		tcp sport { ssh, telnet, http, 3389 } ct state { established, new } accept
		tcp dport { mmcc, 5150 } accept
		tcp sport { mmcc, 5150 } accept
		ip saddr 10.10.0.40 icmp type { echo-reply, echo-request } accept
	}

	chain output {
		type filter hook output priority 0; policy drop;
		tcp dport { ssh, telnet, http, 3389 } ct state { established, new } accept
		tcp sport { ssh, telnet, http, 3389 } ct state { established, new } accept
		tcp dport { mmcc, 5150 } accept
		tcp sport { mmcc, 5150 } accept
		ip daddr 10.10.0.40 icmp type { echo-reply, echo-request } accept
	}
}

Your Host Filtering T2 Flag is:

9f7a33941828bdafd2755fd20176cdf4

###################################################################################################################################

SNORT RULES

echo "alert icmp any any -> any any (msg: "check the data! IDS rulecheck"; content: "IDSRuleCheck"; sid: 9003;)"
echo "alert icmp any any -> any any (msg: "PING!!!"; sid: 9004;)"
echo "alert icmp any any -> any 80 (msg: "WEB TRAFFIC"; sid: 112;)

sudo snort -D -c /etc/snort/snort.conf -l /var/log/snort/

look at conf file and look at logs to see what is alert on 

curl google.com

 *history -> sudo !<number> * this will run command just a tip**
