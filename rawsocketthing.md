```python 

#for building the socket
import socket

#for system level commands
import sys

#for establishing the packet structure *Used later
from struct import *

# Create the raw socket
try:
        s = socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_RAW)
except socket.error as msg:
        print(msg)
        sys.exit()

packet = ''

src_ip = "10.1.0.2"
dst_ip = "10.3.0.2"

# create the IPv4 header info

ip_ver_ihl = 69 #This is putting the decimal version of 0x45 for version and internet
                #Header length

ip_tos = 0      #This combines the DSCP and ECN fields
ip_len = 0      #The kernel will fill in the actual length of the packet
ip_id = 12345   #This sets the IP identification for the packet
ip_frag = 0     #This sets fragmentation to off
ip_ttl = 64     #This sets the TTL of the packet
ip_proto = 16   #This sets the ip protocol to 16 (Chaos) , if wanted tcp(6) and udp (17)
ip_check = 0    #The kernel will fill in the checksum
ip_srcadd = socket.inet_aton(src_ip) #inet_aton will convert IP to 32 bit binary num
ip_dstadd = socket.inet_aton(dst_ip)

#Now we need to combine all our fields!
ip_header = pack('!BBHHHBBH4s4s' , ip_ver_ihl, ip_tos, ip_len, ip_id, ip_frag, ip_ttl, ip_proto, ip_check, ip_srcadd, ip_dstadd)

message =b'This is where message goes!!'
packet = ip_header + message

#send the packet
s.sendto(packet, (dst_ip, 0))

```
