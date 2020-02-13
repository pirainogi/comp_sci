#### [Internet Protocol Resource](https://www.cloudflare.com/learning/ddos/glossary/internet-protocol/)

# Internet Protocol
- set of rules for routing and addressing packets of data so they can travel across networks and arrive at the correct destination
  - packet is a small piece of data
    - header length
    - packet length
    - TTL (time to live): number of network hops a packet can make before it is discarded
    - transportation protocol
    - 14 fields for information in IPv4 headers
- IP information is attached to each packet
  - helps routers to send packets to the right destination
- all devices or domain that connects to the  internet is assigned an IP address
  - as packets are directed to the IP address attached, data arrives where it is needed
- when packets arrive to a destination, they are handled based on their transportation protocol (usually TCP or UDP)

![TCP vs. UDP](/0_img-resources/tcp_vs_udp.png)

# TCP/IP
- Transmission Control Protocol/Internet Protocol is a suite of communication protocols used to interconnect network devices on the internet (or private networks)
- specifies how data is exchanged over the internet by providing end-to-end communications that identify how it should be broken into packets, addressed, transmitted, routed, and received
- requires little central management
- designed to make networks reliable  with the ability to recover automatically from the failure of any device on the network
- TCP defines how applications can create channels of communication across a network
  - manages how a message is assembled into smaller packets before they are transmitted over the internet and  reassembled in the right order at the destination address
- IP defines how to address and route each packet  to the right destination
  - each gateway computer  on the network checks this IP address to determine where to forward the message
- TCP/IP uses the client/server model of communication
- classified as stateless
  - each client request is considered a new request because it is unrelated to previous requests
  - frees up network paths so they can be used continuously
- transport ITSELF is stateful
  - transmits a single message and its connection remains in place until all the packets in a message have been received and reassembled
- nonproprietary and not controlled by any single company
  - modified easily
  - compatible with all operating systems, hardware, and networks
  - highly scalable and can determine the most efficient route through the network


### Layers
- application layer
  - provides applications with standardized data exchange
includes HTTP (hypertext transfer protocol), FTP (file transfer protocol), POP3 (post office protocol 3), SMTP (simple mail transfer protocol), and SNMP (simple network management protocol)
- transport layer
  - responsible for maintaining end-to-end communications across the network
  - handles communication between hosts
  - provides flow control, multiplexing, and reliability
  - includes TCP and UDP (user datagram protocol)
- network layer
  - (also called the internet layer)
  - deals with packets and connects independent networks to transport the packets across network boundaries
  - IP and ICMP (internet control message protocol) for error reporting
- physical layer
  - protocols that only operate on a link (network component that interconnects nodes or hosts)
  - ethernet for LANs (local area networks) and ARP (address resolution protocol)


# UDP/IP
- user datagram protocol
- communication protocol used across the internet for time-sensitive transmissions (voice, video playback, gaming, or DNS lookups)
- speeds up communications by not requiring a handshake
  - allows data to be transferred before the receiving party agreed to the communication
- creates an opening for exploitation though
  - no error checking and ordering functionality of TCP
  - DDoS attacks (including DNS amplification and NTP amplification) make use of the vulnerable instances of these servers (flood the target with UDP traffic)


# IPv4 vs. IPv6
### IPv4
- introduced in 1983
- because there are only so many permutations of IPv4 addresses is very depleted
- most domains and devices still have IPv4 addresses

### IPv6
- more characters and more possible permutations
- not completely adopted
