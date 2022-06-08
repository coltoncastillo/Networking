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

#TCP header fields
tcp_src = 54321 #source port
tcp_dst = 7777 #destination port
tcp_seq = 454 #sequence number
tcp_ack_seq = 0 #TCP ack seq number
tcp_data_off = 5 #data offset specifying the size of tcp header * 4  which is 20
tcp_reserve = 0 #The 3 reserve bits + ns flag in reserve field
tcp_flags = 0 #tcp flags field before the bits are turned on
tcp_win = 65535 #Maximum allowed window size reordered to network order
tcp_chk = 0 #TCP chcksum which will be calculated later on
tcp_urg_ptr = 0 #Urgent pointer only if urg flag is set

#Combine the left shifted 4 bit tcp offset and the reserve field
tcp_off_res = (tcp_data_off << 4) + tcp_reserve

# TCP flags by bit starting from right to left
tcp_fin = 0 #Fin flag
tcp_syn = 1 #Synchronization
tcp_rst = 0 #reset
tcp_psh = 0 #Push
tcp_ack = 0 #Acknowledge
tcp_urg = 0 #Urgent
tcp_ece = 0 #explicit Congestion Notification Echo
tcp_cwr = 0 #Congestion Window Reduced

#Combine the tcp flags by left shifting the bit locations and addin the bits
tcp_flags = tcp_fin + (tcp_syn << 1) + (tcp_rst << 2) + (tcp_psh << 3) + (tcp_ack << 4) + (tcp_urg << 5) + (tcp_ece << 6) + (tcp_cwr << 7)

# The ! in pack format means for network order
tcp_hdr = pack('HHLLBBHHH', tcp_src, tcp_dst, tcp_seq, tcp_ack_seq, tcp_data_off, tcp_off_res, tcp_reserve, tcp_flags, tcp_win, tcp_chk, tcp_urg_ptr)

user_data = b'Hello? Dad?!'

#pseudo Header fields
src_address = socket.inet_aton(src_ip)
dst_address = socket.inet_aton(dst_ip)
reserved = 0 
protocol = socket.IPPROTO_TCP
tcp_length = len(tcp_hdr) + len(user_data)

#Pack the pseudo header and combine with user data 
ps_hdr = pack('!4s4sBBH', src_address, dst_address, reserved, protocol, tcp_length)
ps_hdr = ps_hdr + tcp_hdr + user_data

def checksum(user_data):
        if len(user_data) % 2 != 0:
                data += b'\0'
        res = sum(array.array("H", user_data))
        res = (res >> 16) + (res & 0xffff)
        res += res >> 16
        return (~res) & 0xffff
tcp_chk = checksum(ps_hdr)

# Pack the tcp header to fill in the correct checksum - remember checksum is NOT in network byte order
tcp_hdr = pack('!HHLLBBH', tcp_src, tcp_dst, tcp_seq, tcp_ack_seq, tcp_off_res, tcp_flags, tcp_win) + pack('H', tcp_chk) + pack('!H', tcp_urg_ptr)



message =b'Hello? Dad?!!'
packet = ip_header + tcp_hdr + user_data


























```
