


PC/lap 
switches
router
firewall
modem
fiber network connection

Switches:
switches it store the mac address of the source and destination in cam(Content-addressable memory) to communicate it use 2 layer is data link layer.

hubs :
hubs is like switches but in switch we send packet to the another system it only send the the packet to the destination only but in hub it send the packet to the device connected over network

tcp:
TCP stands for Transmission Control Protocol. It is a widely used transport protocol on the Internet and forms the basis of most communication between devices over a network. TCP provides reliable, ordered, and error-checked delivery of data packets.

peotocols works under tcp
TCP (Transmission Control Protocol) is a transport layer protocol that operates within the TCP/IP protocol suite. TCP provides reliable, ordered, and error-checked delivery of data packets between applications running on devices connected over a network. Here are some protocols that work in conjunction with TCP:

1. **IP (Internet Protocol)**: IP is the network layer protocol responsible for routing packets across different networks. TCP relies on IP for addressing and routing functions. TCP packets are encapsulated within IP packets for transmission over the network.

2. **HTTP (Hypertext Transfer Protocol)**: HTTP is an application layer protocol that is widely used for transmitting web pages and other resources over the Internet. HTTP utilizes TCP as its transport protocol to ensure reliable delivery of web data.

3. **FTP (File Transfer Protocol)**: FTP is an application layer protocol used for transferring files between devices over a network. FTP uses TCP for reliable data transfer during file transfers and control commands.

4. **SMTP (Simple Mail Transfer Protocol)**: SMTP is an application layer protocol used for sending email messages. It relies on TCP for reliable delivery of email data between mail servers.

5. **POP3 (Post Office Protocol version 3)**: POP3 is an application layer protocol used by email clients to retrieve email messages from a mail server. POP3 utilizes TCP for establishing a reliable connection and transferring email data.

6. **Telnet**: Telnet is an application layer protocol that allows remote login to a device over a network. It uses TCP as the transport protocol to establish a reliable connection for interactive terminal sessions.

7. **SSH (Secure Shell)**: SSH is an application layer protocol used for secure remote access to devices over a network. It uses TCP as the underlying transport protocol for establishing secure, encrypted connections.

UDP:
UDP (User Datagram Protocol) is a transport layer protocol that operates within the TCP/IP protocol suite. Unlike TCP, UDP is a connectionless protocol that does not provide reliable delivery or error checking. It is often used in situations where real-time communication and low overhead are prioritized over reliability. Here are some protocols that commonly work with UDP:

1. **DNS (Domain Name System)**: DNS is an application layer protocol used for translating domain names into IP addresses. DNS uses UDP as its transport protocol for making queries and receiving responses. UDP is preferred for DNS because of its lower overhead and faster response times compared to TCP.

2. **DHCP (Dynamic Host Configuration Protocol)**: DHCP is an application layer protocol used for automatically assigning IP addresses and other network configuration parameters to devices on a network. DHCP uses UDP to broadcast requests and receive responses from DHCP servers.

3. **TFTP (Trivial File Transfer Protocol)**: TFTP is a simple file transfer protocol used for transferring files between devices on a network. TFTP relies on UDP for its transport layer, providing minimal functionality compared to FTP (which uses TCP).

4. **SNMP (Simple Network Management Protocol)**: SNMP is an application layer protocol used for managing and monitoring network devices. SNMP uses UDP for sending and receiving management information between network devices and management systems.

5. **VoIP (Voice over IP)**: VoIP is a technology that enables voice communication over IP networks. It often utilizes UDP for real-time transmission of voice packets due to its lower latency and overhead compared to TCP.

6. **NTP (Network Time Protocol)**: NTP is a protocol used for synchronizing the time of devices on a network. NTP uses UDP for transmitting time information between time servers and clients.


multilayer switch:
A multi-layer switch, also known as a layer 3 switch or a multilayer switch, is a network device that combines the functionalities of both switches and routers. It operates at multiple layers of the OSI (Open Systems Interconnection) model, specifically at the data link layer (layer 2) and the network layer (layer 3).

subnet ip address :
A subnet IP address is a subset of a larger IP address range. It is used to create smaller, more manageable networks within a larger network.


IP address :
ip address is used to communicate with other devices connected with internet

there are 4.3 billion ip address possibles are there

ip range                                                             subnetmask
A   1.0.0.0        -  126.255.255.255                      255.0.0.0
B   128.0.0.0    -  191.255.0.0                              255.255.0.0
c   192.0.0.0    -   223.255.255.0                          255.255.255.0
D  224.0.0.0    -   239.255.255.255
E  240.0.0.0     -   255.255.255.255









  