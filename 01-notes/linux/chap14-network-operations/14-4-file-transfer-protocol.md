# Chapter 14.4: FTP (File Transfer Protocol)

---
## * File Transfer Protocol
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