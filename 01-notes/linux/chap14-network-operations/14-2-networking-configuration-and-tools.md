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

#### ==** Two forms of network interface==
1. Physical: NIC (Network Interface Card)
	Connect a computer to a network
2. Software

#### ** Information on Network Interface
```bash
ip # newer
ifconfig # /sbin/ifconfig, install by net-tools
```

#### ** How to use `ip`
```bash
ip [options] OBJECT COMMAND

# OBJECT
addr
link
route

# COMMAND
show
add 
del
```
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
