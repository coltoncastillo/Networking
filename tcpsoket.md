```python

import socket
ipaddr = '127.0.0.1'
port = 54321
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect ((ipaddr, port))
# To send a string as a bytes-like object, add the prefix b to the string. \n is newline.
s.send(b'Hello\n')
# It is recommended that the buffersize used with recvfrom is a power of 2 and a small num of bits.
response, con = s.recvfrom(1024)
#In order to recieve a message that is sent as a bytes-like object you decode into utf-8 (default)
print(response.decode())
s.close()

```

