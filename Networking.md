##Day 1
Protocol Data Unit(PDU)
    Session-Application = Data
    Transport = Segment/Datagram
    Network = Packet
    Data Link = frame
    Physical = Bit



#Internet Protocol Versions
    -IPv4 (ARPANET 1982)
        Classful subnetting
        Classless subnetting (CIDR)
        NAT
    -IPv6 (Standardized 2017)

#Describe Classful IPv4
    Class A (0 to 127)
    Class B (128 to 191)
    Class C (192 to 223)
    Class D (224 to 239) - Multicasting
    Class E (240 to 255) - Not used

#Subnetting
    -IP addresses:
        Network Portion
        Host Portion

#Identify IPv4 address types
    Unicast
        Any Class A thu C
    Multicast
        Class D
    Broadcast
        Any IP were the host portion is all on

#IPv4 address scopes
    Public
    Private (RFC 1918)
    Loopback (127.0.0.0/8)
    Link-Local (APIPA)
    Multicast (class D)

#IPv4 Fragmentation
    Breaking up packets from higher MTU to lower MTU network
    Performed by routers
    MF flag is on from 1st until 2nd to last
    Offset is on from 2nd until the last
    Offset = (MTU - (IHL x 4)) ÷ 8

#IPv6 Fragmentation
    IPv6 does not support fragmentation within it’s header
    Routers do not fragment IPv6 packets
    Source adjusts MTU to avoid fragmentation
    Source can use IPv6 fragmentation extension header

#Fragmentation Vulnerability
    Can use fragmentation overlaps to avoid firewall detection
    Attack depends on how OS deals with overlap
    Example: Teardrop attack

#IPv4 Auto Configuration
    APIPA
        169.254.0.0/16
        RFC 3927
    DHCP
        DORA process
        RFC 1531
    
#IPv4 Auto Configuration Vulnerability
    Rogue DHCP
    Evil Twin
    DHCP Starvation

#ICMPv4 OS Fingerprinting
    Linux:
        Default size: 64 bytes
        Payload message:
            !\”#\$%&\‘()*+,-./01234567
    Windows:
        Default size: 40 bytes
        Payload message:
            abcdefghijklmnopqrstuvwabcdefghi

#ICMPv4 Traceroute
    Can use various protocols and ports
        ICMP (windows default)
        UDP (linux default)
        TCP

#ICMPv4 Attacks
    Firewalking (traceroute)
    Oversized ICMP messages
    ICMP Redirects
    SMURF Attack
    Map network w/ IP unreachables
    ICMP Covert Channels

#Describe IPv6 addressing
    IPv6 Addressing
        128 bit address
        64-bit Prefix (4 hextets)
        64-bit Interface ID (4 hextets)
        340 undecillian addresses

#Describe IPv6 subnetting
    Organizations asigned a 48-bit Prefix by IANA
    Last 16-bits of prefix is used for subnetting
    Allows for upto 65,536 subnets to be created

#Explain IPv6 address representation
   2001:ABCD:1234:DEF0:1111:2222:3333:4444
        128-bit (64bit Prefix and 64bit Int ID)
        Represented using 32 Hex digits
        Hextet: 4 hex separated by (:)

#Explain IPv6 address representation (shortening)
    2001:0000:0000:0001:0000:0000:0000:0001
      Can shorten consecutive 0’s with (::)
        Can only use it once
        2001:0:0:1::1

#Identify IPv6 address types
    Unicast
    Multicast
    Anycast

#IPv6 address scopes
    Global Unicast Addresses (2000::/3)
    Unique Local (fc00::/7)
    Loopback (::1/128)
    Link-Local (fe80::/10)
    Multicast (ff00::/8)

#IPv6 zero configuration (Link-Local)
    Hosts generate link-local prefix (FE80::/8)
    Interface ID can be:
        Random (Windows default)
        EUI-64 (nix* and Cisco default)

#IPv6 zero configuration (Global)
    Hosts requests global prefix
        SLAAC (RFC 4862) (default)
        DHCPv6 (configured)
    Interface ID can be:
        EUI-64 (nix* and Cisco default)
        Random (Windows default)  

# IPv6 zero configuration (EUI-64 link-local)
    MAC: fa:16:3e:c3:68:f2
    Append: ff:fe between OUI and Vendor assigned
    Flip 7th bit
    Result: FE80::f816:3eff:fec3:68f2

#IPv6 zero configuration (EUI-64 Global)
    Prefix from RA: 2001:ABCD:1234:DEF0::
    MAC: fa:16:3e:c3:68:f2
    Append: ff:fe between OUI and Vendor assigned
    Flip 7th bit
    Result: 2001:ABCD:1234:DEF0:f816:3eff:fec3:68f2

#IPv6 zero configuration Vulnerability
    SLAAC MitM
    Can be used to figerprint OS
    Rogue DHCP
    Evil Twin
    DHCP Starvation

#Explain Neighbor Discovery Protocol (NDP)
    Router Solicitation (Type 133)
    Router Advertisement (Type 134)
    Neighbor Solicitation (Type 135)
    Neighbor Advertisement (Type 136)
    Redirect (Type 137)

#Metrics
    RIP: Hop
    EIGRP: Bandwidth, Delay, Load, Reliability
    OSPF: Cost
    BGP: Policy

#












