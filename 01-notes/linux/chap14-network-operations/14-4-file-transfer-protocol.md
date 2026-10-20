# Chapter 14.4: FTP (File Transfer Protocol)

---
## ==🔵* File Transfer Protocol==
---
FTP is one of the oldest methods of network data transfer. 

Negative: Insecure (personal data are sent in plain text)

---
## ==🔵* SSH: Executing Commands Remotely==
---
Secure Shell (SSH) is a cryptographic network protocol used for secure data communication, also used for remote services.

#### ==** SSH Mechanism (C to mail server)==
SSH Client (C) connect to SSH Server (S) and sets a tunnel -> C sends traffic into tunnel (make the data encrypted) -> S pass data to mail server

#### ==** Login to Same Username==
```bash
ssh some_system # some_system is address of computer (hostname or IP address)
# Type password or SSH key pair
```

#### ==** Login to Different Username==
```bash
# BOTH WORKS
ssh -l someone some_system # l stands for login name
ssh someone@some_system
```

#### ==** Run Command in Different Username==
```bash
# ALL WORKS 
ssh user@remote_host "command"
	ssh jal@localhost "ls -lh"
	ssh jal@localhost ls-lh 
```

---
## ==🔵* Copying Files Securely with `scp`==
---
`scp` stands for Secure Copy, it uses SSH protocol.

#### ==** Using `scp`==
```bash
scp <localfile> <user@remotesystem>:/home/user
```

---
## ==🔵* Network Troubleshooting==
---
Problem: Web browser can't find google.com
1. Check your IP address and host name
```bash
hostname
ip addr show

# IF BAD?
sudo dhclient eth0 # get fresh address for client
```
2. Check your default gateway
```bash
ip route show 
```
3. Try to reach gateway and google.com 
```bash
sudo ping -c 3 <gateway>
sudo ping -c 3 google.com
```
4. Look for IP address of google.com (use either of one)
```bash 
host google.com # default DNS
host google.com 8.8.8.8 # public DNS
dig google.com

# IF FAIL
# EDIT DIRECTLY /etc/hosts
```
5. Look at which DNS you are using
```bash
cat /etc/resolv.conf
```
6. Restart Network Manager
```bash
sudo systemctl restart NetworkManager
```
6. If DNS server is the problem (use either of one)
```bash
sudo traceroute 8.8.8.8
sudo mtr --report--cycles 3 8.8.8.8
```


#### ==** Reasons `host`, `dig` fail to connect name to IP address==
1. DNS server is down
2. DNS is not currently available in the machine
3. Route to DNS server may not be correct
#### ==** DNS Definition==
DNS stands for Domain Name System -> translate human-friendly names into IP addresses, help by `host` command.

---