`snort --version`

`sudo snort -D -l /var/log/snort -c /etc/snort/snort.conf`

`ps -ef | grep snort`

`sudo tcpdump -Xr snort.log.1655blahblah`

`sudo snort -r ids.pcap -c /etc/snort/cows.rules`
