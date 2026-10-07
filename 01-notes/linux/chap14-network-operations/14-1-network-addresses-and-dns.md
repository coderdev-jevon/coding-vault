# Chapter 14.1: Network Addresses and DNS
Date: 2026-10-07

## * Introduction to Networking
==Network== -> group of computers connected through communication channels

==Nodes== -> connected devices

==**Internet**== -> largest network in the world, also called as network of networks

## * IP Addresses
Every device attached to network must have ==IP address== (unique network address identifier), IP address stands for Internet Protocol Address.

Data is sent as ==small pieces called packets==, put back together at destination.

Packet: ==Data Buffer== (a chapter of the information) + ==Header== (destination, source, sequence to put back together)

## ==* IPv4 and IPv6==

IPv4 (IP version 4) -> older, far more widely used, 32 bits for addresses
IPv6 (IP version 6) -> newer, more possible addresses, 128 bits for addresses

#### ** Why IPv4 is still widely used
There are methods to make more addresses available by NAT for example.

**==NAT==** allows sharing one IP address among locally connected computers, devices are unique if seen in local address.

![[ip-address-nat.png|486]]


## * Decoding IPv4 Addresses
Divided into four 8-bit sections called ==octets== (==byte==).

IP address →            172  .          16  .      31  .     46  
Bit format →     10101100.00010000.00011111.00101110

#### ==** 5 Classes of Network Addresses==

A,B,C: Network Addresses (Net ID), which network the device is on, and Host Address (Host ID), which device within that network
D: For multicast applications (multiple computers simultaneously)
E: Reserved for future use

## * Class A,B,C Network Addresses
SKIP

## * IP Address Allocation
The one who make IP Address for us is ==ISP (Internet Service Provider)==, an organization usually asked for a ==block of address== like 203.0.113.0 to 203.0.113.255

| Organization                      | Likely class                | Why                          |
| --------------------------------- | --------------------------- | ---------------------------- |
| Small office, a few dozen devices | Class C (~254 hosts)        | A small block is enough      |
| University or mid-size company    | Class B (~65,000 hosts)     | Needs thousands of addresses |
| Very large organization           | Class A (~16 million hosts) | Need a huge number           |
#### ==** Two Ways of IP Address Allocation==
1. ==Manual (static)== -> type address by hand
	
2. ==Dynamic Assignment== -> change over time, after reboot for example, ==DHCP== (Dynamic Host Configuration Protocol)

## * Name Resolution
Turn ==numerical IP address values to hostname==, like 3.13.31.214 to linuxfoundation.org

#### ==** Look at Host Name==

```bash
hostname
```

## * Using Domain Name System (DNS) and Name Resolution Tools

==**DNS** is used for translate names into IP addresses==

==`/etc/resolv.conf`== -> list DNS servers to ask, where to ask if not found locally
==`/etc/hosts`== ->  phonebook on your machine

#### ==** Commands to ask DNS for IP Address==

```bash
host linuxfoundation.org # short,readable
nslookup linuxfoundation.org # older interactive-style
dig linuxfoundation.org # most detailed
```

#### ** Why must I learn this?
If pinging IP address works, but name fails, the problem lies in name resolution.

Which DNS server am I asking? 