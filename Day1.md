# Day 1

```
IH Info
Student#: student13

Command: ssh student@10.50.21.203 -X

Password: password
```
`https://miro.com/app/board/o9J_klSqCSY=/`
---
## OSI MODEL 
### PHYSICAL LAYER RESPONSIBILITIES (Layer 1)
- Hardware Specifications
- Encoding and Signaling
- Data Transmission and Reception
- Physical Network Design
### DATA LINK LAYER (Layer 2)
Data Link Sub-layers
  - MAC (Media Access Control)
  - LLC (Logicl Link Control)
    - where the physical interacts with the rest of the network (switch / router)
- Ethernet Headers 
  - Ether Type:
    - 0x0800: IPv4
    - 0x0806: ARP
      - ARP Header, follows ethernet header
    - 0x86DD: IPv6
    - 0x8100: VLAN Tag
      - 802.1Q Header is used for VLAN
## NETWORK LAYER (Layer 3)
- IPv4 Headers
  - very fun time ! 
  - fragmentation
- IPv6 Headers
  - Even more fun !
- Fingerprinting 
  - Vendors have chosen different values for TTL which can provide insight to which OS family a generated packet is from
    - Linux: 64
    - Windows: 128 
    - Cisco Router: 255
## TRANSPORT LAYER (Layer 4)
  - TCP and UDP
## SESSION LAYER (Layer 5)
PROTOCOLs
  - SOCKS
    - Proxy (Middle man)
  - NetBIOS
    - SMB rides over NetBIOS
      - SMB (Samba) is a way for linux to talk to windows shared drives
  - PPTP/L2TP
  - RPC
    - Request and responses, used by different applications
## PRESENTATION LAYER (Layer 6)
- Translation
- Formating
- Encoding (ASCII, EBCDIC, HEX, BASE64)
- Encryption (Symmetric or Asymmetric)
- Compression
## APPLICATION LAYER (Layer 7)
FTP (TCP 20/21)  
  - Messages:
    - FTP Commands
    - FTP Reply Codes
  - Modes:
    - Active (Default)
      - NAT and Firewall traversal issues
      - Complications with tunneling through SSH
      - Passive FTP solves issues related to Active mode and is most often used in modern systems
    - Passive 
SSH (TCP 22)
- Messages provide:
  - Client/server authentication
  - Asymmetric or PKI for key exchange
  - Symmetric for session
  - User Authentication
  - Data Stream Channeling 
  













