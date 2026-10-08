# Chap 14.2: Networking Configuration and Tools
Date: 2026-10-07

## * Network Configuration Files
They are ==text files where Linux stores its network settings==: IP address, gateway, DNS servers, hostname, and so on.

For Debian Family, they are stored inside==`/etc/network`==

==`etc` stands for `editable text configuration` or `et cetera`==

#### ==** `nmtui` (network manager text user interface)==
It is a text user interface

#### ==** `nmcli` (network manager command line interface)==
Does the same thing through typed commands

## * Network Interfaces
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

## ==* How to read `ip addr` output==
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


## ==* `ip link`==
Same like `ip addr` but without IP addresses.

## ==* `ip route`==
Shows the routing table, "where to send each packet", shows default route, your local network.

## ==* `ip neig`==
It stands for neighbor, it shows list of ==IP addresses on your local network map to which MAC addresses.==
```
192.168.1.1 dev eth0 lladdr 52:54:00:12:35:02 REACHABLE
192.168.1.40 dev eth0 lladdr 08:00:27:aa:bb:cc STALE
192.168.1.50 dev eth0  FAILED
```
192.168.1.1 is the neighbor's IP address, `dev etho` is the interface it was learned on, `lladdr 52:54:..` means neighbor's MAC address, REACHABLE is the entry's state.

## * `ip netns`
It manage network namespaces, it's a tool for creating, listing, and entering private apartments 


|Object|What it manages|Example|
|---|---|---|
|`address` (`addr`, `a`)|IP addresses on interfaces|`ip addr`|
|`link` (`l`)|Interface state, MAC address, MTU|`ip link`|
|`route` (`r`)|Routing table, default gateway|`ip route`|
|`neighbor` (`neigh`)|ARP table: which IP maps to which MAC|`ip neigh`|
|`netns`|Network namespaces, the isolation behind containers|`ip netns list`|
## * Additional

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
