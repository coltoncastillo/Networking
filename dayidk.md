# Tunneling Stuff

SSH local port forwarding

`ssh -p <optional alt port> <user>@<pivot ip> -L <local bind port>:<tgt ip>:<tgt port> -NT`

or

`ssh -L <local bind port>:<tgt ip>:<tgt port> -p <alt port> <user>@<pivot ip> -NT`

  - syntax below creates a local port (1111) on the local host that forwards to a target machine’s port 80.

    - `ssh student@172.16.82.106 -L 1111:localhost:80 -NT`

      or

    - `ssh -L 1111:localhost:80 student@172.16.82.106 -NT`

SSH dynamic port forwarding
`ssh -D <port> -p <alt port> <user>@<pivot ip> -NT`


`proxychains wget -r localhost`

`proxychains wget -r ftp://localhost`


net3_student13 , password13


## Dynamic Port Forward example
`ssh net3_student13@10.50.29.96 -D 9050 -NT`
  - establishes tunnel

`proxychains wget -r ftp://10.3.0.1`
  - where 10.3.0.1 is target IP
