# Chap 14.2: Networking Configuration and Tools
Date: 2026-10-07

---
## ==🔵* Terminology==
---
1. ==**Host name**== is the name for IP address to make it easier to remember.
2. ==**Remote host**== is the opposite of local host, the computer you reach over the network.
3. **==Network host==** is any device connected to a network that has an IP address and can send or receive data on it.
4. ==**Website**== is the content and software that host serves.
5. ==**DNS**== is Domain Name System, is the Internet's phone book, it translates human friendly name into IP address.
6. ==**Mail server**== is the computer that receives email address to a certain domain.
7. ==**Name server**== is a computer that stores DNS records and answers DNS questions.


---
## ==🔵* Network Configuration Files==
---
They are ==text files where Linux stores its network settings==: IP address, gateway, DNS servers, hostname, and so on.

For Debian Family, they are stored inside==`/etc/network`==

==`etc` stands for `editable text configuration` or `et cetera`==

#### ==** `nmtui` (network manager text user interface)==
It is a text user interface

#### ==** `nmcli` (network manager command line interface)==
Does the same thing through typed commands

---
## ==🔵* Network Interfaces==
---
Interface means ==connection point.== It ==can be activated or deactivated.==

==IP address belongs to network interface.==



#### ==** Two forms of network interface==
1. Physical: NIC (Network Interface Card)
	Connect a computer to a network
2. Software

#### ** Information on Network Interface
```bash
ip # newer
ifconfig # /sbin/ifconfig, install by net-tools
```

#### ==** How to use `ip`==
```bash
ip [options] OBJECT COMMAND

# OBJECT
addr # ip addresses
link # interface
route

# COMMAND
show
add 
del
```

---
## ==🔵* How to read `ip addr` output==
---
```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:ab:cd:ef brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.25/24 brd 192.168.1.255 scope global dynamic eth0
       valid_lft 86000sec preferred_lft 86000sec
    inet6 fe80::a00:27ff:feab:cdef/64 scope link
       valid_lft forever preferred_lft forever
```

**Line 1: the interface itself**

- `2:` is the interface index, and `eth0` is its name.
- `<BROADCAST,MULTICAST,UP,LOWER_UP>` are flags. `UP` means it is enabled, and `LOWER_UP` means the cable or Wi-Fi link is actually connected.
- `mtu 1500` is the largest packet size it sends. (`mtu` stands for Maximum Transmission Unit), 1500 bytes
- `state UP` is the current status (`DOWN` if it's off or disconnected).

**Line 2: the MAC address** (Media Access Control Address)

- `link/ether 08:00:27:...` is the hardware address of the interface.

#### ==** MAC Address vs IP Address==
MAC address is the interface identifier, while IP address is interface's place in a network. The scope of MAC address is local link only, while IP address is across networks.

#### ==** How Interface is attached to device==
Computer has NIC (Network Interface Card) -> Program called driver acts as instruction manual for that chip -> OS gives it a name -> Interface gets an IP address.

#### ==** What is a Driver==
It is a software that allows operating system to control a specific piece of hardware, like translator between OS and hardware.
#### ==** "NIC" in Mobile Phones==
1. Wi-Fi chip
2. Cellular modem
3. Bluetooth chip
4. NFC chip

#### ==** Chip vs Card==
Chip is a tiny piece of silicon, while card is a circuit board, often with several chips. Chip is like the engine and card is the whole module.

**Line 3: the IPv4 address**

- `inet 192.168.1.25/24` is the IP address and network size.
	==`inet` is short for internet==
- `brd` is the broadcast address of the network.
- `scope global` means it is reachable beyond your local link.
	`scope` tells you how far an address is valid
- `dynamic` means it came from DHCP.

**Line 4: the lease**

- `valid_lft 86000sec` is how long the DHCP lease lasts before renewal.
	`lft` stands for lifetime

**Lines 5-6: the IPv6 address**

- `inet6` is the IPv6 address. `fe80::` addresses are link-local, meaning they work only on your local network.

So `ip addr` shows state, MAC, IPv4, IPv6, and lease info.

A lease is a temporary loan, DHCP server lets your device use an IP address for a set amount of time.

#### ** Brief Output from `ip addr`
```bash
ip -br addr # br stands for brief
```

---
## ==🔵* `ip link`==
---
Same like `ip addr` but without IP addresses.

---
## ==🔵* `ip route`==
---
Shows the routing table, "where to send each packet", shows default route, your local network.

#### ==** `ip route` Commands==
```bash
ip route
ip route add
ip route del
```

#### ==** How to read `ip route output`==
```
default via 192.168.1.1 dev eth0 proto dhcp metric 100
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.25 metric 100
```
The ==rule of each line== is for destinations in this range, send packets this way.

`default via 192.168.1.1 dev eth0 proto dhcp metric 100`
Destination + Via (what router) + Which Interface the packet leaves from + Source (own IP address)

==`default`== means the last resort if destination is not found.
 
---
## ==🔵* `ip neig`==
---
It stands for neighbor, it shows list of ==IP addresses on your local network map to which MAC addresses.==
```
192.168.1.1 dev eth0 lladdr 52:54:00:12:35:02 REACHABLE
192.168.1.40 dev eth0 lladdr 08:00:27:aa:bb:cc STALE
192.168.1.50 dev eth0  FAILED
```
192.168.1.1 is the neighbor's IP address, `dev etho` is the interface it was learned on, `lladdr 52:54:..` means neighbor's MAC address, REACHABLE is the entry's state.

---
## ==🔵* `ip netns`==
---
It manage network namespaces. With namespaces, you can have name duplicates on the same program.

---
## ==🔵* `ping`==
---
To check ==whether a machine is attached to a network== or not, how long trip it takes.
#### ==** Commands==
```bash
ping <hostname>
ping <ip_address>

ping -c N <hostname> # to limit how many packets to send
CTRL-C # to stop sending packets
```

---
## ==🔵* `traceroute`==
---
It prints the route to reach the network host.

#### ==** URL Simple Breakdown==
```
https://www.google.com/search
  |         |             |
protocol   host          path
```

#### ==** Difference between `ip route` and `traceroute`==
`ip route` shows your computer's rule to send packets, while `traceroute` discovers actual path to send packet to network host.

---
## ==🔵* More Networking Tools==
---
```bash
# HIGH PRIORITY
dig
mtr
ethtool

# MEDIUM PRIORITY
netstat
tcpdump
```

#### ==** `host` command==
It is the simplest tool for asking DNS a question from terminal.

It includes IPv4 address, IPv6 address, and mail server
#### ==** `dig` command==
Ask DNS a question and shows you full, detailed answer.

```bash
dig google.com A # IPv4
	dig +short google.com A # for cleaner output
dig google.com AAAA # IPv6
dig google.com MX # MX record or mail server
dig google.com NS # name server for the domain
dig google.com TXT # for text records (email security, domain verification)

dig @8.8.8.8 google.com # to ask for a specific DNS server
```

Name server can be a ==resolver or authoritative name server==, resolver is the DNS server your computer sends question to, authoritative name server is the one who owns the answer (official records.)

## ==🔵* Additional==
---
#### ==** Different Area Different IP Address==
It is done to group nodes up, to make router task easier.

#### ==** What a Router is==
It connect networks to each other. It is a member of two networks

#### ==* Why people use Router to connect to Wi-Fi==
It is not router actually but ==range extender (repeater)==, receives Wi-Fi and rebroadcasts it.
#### ==** How to Different Out Networks==
Having the same network means they can be connected without a router.

`192.168.1.25/24`. -> first 24 bits are the Net IDs, same Net IDs mean the same network.

#### ==** Why People need to change IP Address, Gateway==
Different place might mean different network, so different IP Address is needed.

#### ==** Why switch between DHCP and Static==
People change from DHCP to Static to make device to be findable to other people or for recover machine.

People change from Static to DHCP to have less maintenance and make it easier to move to a different network.
#### ==** What is a Gateway==
It is the job, router is a gateway for a device when that device uses it as way out to other networks.

#### ==** What does it mean to connect or disconnect from network==
Join Wi-Fi means join wireless network by router to exchange data from it.

#### ==** What is cellular data and how does Wi-Fi works in correlation to cellular data==
Your phone talks by radio to nearby cell tower, and the carrier connects tower to internet, with monthly data limit.

#### ==** Why bad signals can occur==
1. Distance from tower is quite far
2. Obstacle such as walls that block radio waves
3. Congestion (many people using it at once)
4. Weak antenna (your phone)

---
