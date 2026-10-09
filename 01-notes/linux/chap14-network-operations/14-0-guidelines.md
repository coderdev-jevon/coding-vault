## Learning Objectives
1. Explain basic networking concepts, including types of networks and addressing issues
2. Configure network interfaces and use basic networking utilities, such as `ifconfig`, `ip`, `ping`, `route`, and `traceroute`
3. Use graphical and non-graphical browsers, such as `Lynx`, `w3m`, `Firefox`, `Chrome`, and `Epiphany`
4. Transfer files to and from clients and servers using both graphical and text mode applications, such as `scp`, `ftp`, `sftp`, `curl`, and `wget`

## Network Addresses and DNS
1. 🟡 **Introduction to Networking**: skim for the vocabulary
2. 🟢 **IP Addresses**: learn until you understand
3. 🟢 **IPv4 and IPv6**: learn until you understand
4. 🟡 **Decoding IPv4 Addresses**: skim the concept (network vs. host, subnet masks) and skip the bit math
5. 🔴 **Class A Network Addresses**: skip
6. 🔴 **Class B Network Addresses**: skip
7. 🔴 **Class C Network Addresses**: skip
8. 🟡 **IP Address Allocation**: skim (static vs. DHCP, private ranges)
9. 🟢 **Name Resolution**: learn until you understand
10. 🟢 **Using Domain Name System (DNS) and Name Resolution Tools**: learn until you understand
11. 🟢 **Try-It-Yourself: Using DNS and Name Resolution Tools**: do the lab

## Network Configuration and Tools
- 🟡 **Network Configuration Files**: know that network settings live in files and that the location differs by distro (`NetworkManager, netplan, etc.`). Don’t memorize the paths.
- 🟢 **Network Interfaces**: understand what an interface is (physical, loopback, virtual), plus IP address, netmask, and gateway. GPU clusters depend on this.
- 🟢 **The ip Utility**: the modern tool you’ll use constantly (`ip addr`, `ip link`, `ip route`). Learn it well.
- 🟢 **ping**: simple, but it’s your first check that a machine is reachable.
- 🟡 **route**: it’s deprecated and replaced by `ip route`. Learn the concept of a routing table, but practice it with `ip route`.
- 🟡 **traceroute**: worth understanding how it works (it uses TTL to show each hop). You’ll use it for debugging, but not daily.
- 🟢 **Try-It-Yourself: ping, route, traceroute**: do it, and type the commands yourself. This is where the learning happens.
- 🟡 **More Networking Tools**: tools like `netstat`, `nmap`, `tcpdump`, `wget`/`curl`, and `dig` usually show up here. Know what each is for. `ss` has replaced `netstat`, and `tcpdump` is the one worth revisiting later.
- 🟡 **Using More Networking Tools**: follow along and try a few of the commands, but don’t spend long on any single tool.
- 🟢 **Try-It-Yourself: Using Network Tools**: do the hands-on exercise.