# Day 2 💯💀😈😆

### SOCKET TYPES
- Stream Sockets - Connection oriented and sequenced; methods for connection establishment and tear-down. Used with TCP, SCTP, and Bluetooth.
- Datagram Sockets - Connectionless; designed for quickly sending and receiving data. Used with UDP.
- Raw Sockets - Direct sending and receiving of IP packets without automatic protocol-specific formatting.
### USER SPACE VS. KERNEL SPACE SOCKETS
- User Space Sockets
  - Stream Sockets
    - TCP based connections
  - Datagram Sockets
    - UDP based connections
- Kernel Space Sockets
  - Raw Sockets
### SOCKET CREATION AND PRIVILEGE LEVEL
- User Space Sockets
  - The most common sockets that do not require elevated privileges to perform actions on behalf of user applications.
- Kernel Space Sockets
  - Attempts to access hardware directly on behalf of a user application to either prevent encapsulation/decapsulation or to create packets from scratch, which requires elevated privileges.

### USER SPACE APPLICATIONS/SOCKETS
- Using tcpdump or wireshark to read a file
- Using nmap with no switches
- Using netcat to connect to a listener
- Using netcat to create a listener above the well known port range (1024+)
- Using /dev/tcp or /dev/udp to transmit data
### KERNEL SPACE APPLICATIONS/SOCKETS (elevated privilege)
- Using tcpdump or wireshark to capture packets on the wire
- Using nmap for OS identification or to set specific flags when scanning
- Using netcat to create a listener in the well known port range (0 - 1023)
- Using Scapy to craft or modify a packet for transmission
- Using Python to craft or modify Raw Sockets for transmission
- Network devices using routing protocols such as OSPF

### NETWORK PROGRAMMING WITH PYTHON3
 - Network sockets primarily use the Python3 Socket library and socket.socket function.
```
import socket
  s = socket.socket(socket.FAMILY, socket.TYPE, socket.PROTOCOL)
```  
### The socket.socket function 
Inside the socket.socket. function, you have these arguments, in order:
```
socket.socket([*family*[,*type*[*proto*]]])
```
- family constants should be: `AF_INET` (default), `AF_INET6`, `AF_UNIX`
- type constants should be: `SOCK_STREAM` (default), `SOCK_DGRAM`, `SOCK_RAW`
- proto constants should be: `0` (default), `IPPROTO_RAW`

### RAW IPv4 SOCKETS
- Raw Socket scripts must include the IP header and the next headers.
- Requires guidance from the "Request for Comments" (RFC)to follow header structure properly.
  - RFCs contain technical and organizational documents about the Internet, including specifications and policy documents.
    - See RFC 791, Section 3 - Specification for details on how to construct an IPv4 header. 
- **RAW SOCKET USE CASE**
  - Testing specific defense mechanisms - such as triggering and IDS for an effect, or filtering
  - Avoiding defense mechanisms
  - Obfuscating data during transfer
  - Manually crafting a packet with the chosen data in header fields



















