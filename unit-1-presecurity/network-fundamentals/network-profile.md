Network Profile — Windows PC

Q1 — IPv4 and MAC address

IPv4 address: 10.18.172.220

MAC address: 58-02-05-21-46-XX (last group masked for privacy)

Q2 — Private vs public IP

A private IP address is used inside a local network and is not directly routable on the public internet, while a public IP address identifies a network connection on the internet. A home router uses private addresses so multiple devices can communicate on the local network while sharing an internet connection.

Q3 — IP address vs MAC address

An IP address identifies a device's location on a network and can change when the device joins a different network. A MAC address identifies the network interface and is mostly fixed to the hardware. IP addressing operates at OSI Layer 3 (Network), while MAC addressing operates at OSI Layer 2 (Data Link).

Q4 — Subnet

Subnet mask: 255.255.255.0

CIDR: /24

Total addresses: 256

Usable device addresses: 254

Network address: 10.18.172.0

Broadcast address: 10.18.172.255

Q5 — Default gateway

Default gateway: 10.18.172.62

It is on the same subnet as the computer because both 10.18.172.220 and 10.18.172.62 belong to the 10.18.172.0/24 network.

Q6 — Ping

Gateway average: 3 ms

1.1.1.1 average: 28 ms

The gateway is faster because it is directly on the local network, while traffic to 1.1.1.1 has to travel through the router and across external networks.

Q7 — DNS

The service that made it possible to ping example.com by name is DNS (Domain Name System). DNS translates human-readable domain names into IP addresses.

Q8 — DNS server

Configured DNS server: 10.18.172.62

The DNS server is the same address as the default gateway.

Q9 — DNS lookups

example.com: 104.20.23.154, 172.66.147.243, plus IPv6 addresses

google.com: 142.251.38.78, plus an IPv6 address

youtube.com: 64.233.162.91, 64.233.162.93, 64.233.162.136, 64.233.162.190, plus multiple IPv6 addresses

Large websites can return multiple IP addresses for load balancing, redundancy, and distributing traffic.

Q10 — DNS privacy

If someone could monitor DNS queries, they could learn which domain names I am looking up and therefore infer which websites or online services I use. This information can still reveal browsing patterns even when the actual website connection is protected by HTTPS.

Q11 — Traceroute

Hops to example.com: 8

First hop: 10.18.172.62

Q12 — Traceroute * * *

No. A * * * result does not necessarily mean the connection is broken. Some routers or network devices do not respond to traceroute probes or filter/rate-limit those responses. In this trace, the destination was still reached successfully.

Q13 — Listening ports

Port

Protocol

Interface

Common use

135

TCP

All interfaces

Windows RPC

139

TCP

10.18.172.220

NetBIOS Session Service

445

TCP

All interfaces

SMB / Windows file and printer sharing

5040

TCP

All interfaces

Windows/service-specific listener

4343

TCP

All interfaces

Application/service-specific listener

4449

TCP

All interfaces

Application/service-specific listener

5141

TCP

All interfaces

Application/service-specific listener

49664–49668

TCP

All interfaces

Windows RPC dynamic ports

49674

TCP

All interfaces

Windows RPC dynamic port

58995

TCP/IPv6

All IPv6 interfaces

Application/service-specific listener

15152, 19443, 46753, 46760, 51779–51782

TCP

127.0.0.1

Localhost-only services

Q14 — Two ports and security

Port 135 is commonly used for Windows RPC services, while port 445 is commonly used for SMB file and printer sharing. A service listening only on 127.0.0.1 can normally be reached only from the same computer. A service listening on 0.0.0.0 or a network interface can accept connections from the network, which gives it greater exposure and therefore greater security importance.

Q15 — Network-facing exposure

The computer is exposing several network-facing services, including ports 135, 139, 445, several Windows RPC dynamic ports, and some application/service-specific ports. This is more network exposure than I would expect from a basic personal computer, so the services behind the less familiar ports would be worth investigating to make sure they are needed.

Network Profile

Identity

IPv4 address: 10.18.172.220

Subnet mask / CIDR: 255.255.255.0 / /24

MAC address: 58-02-05-21-46-XX

Network address: 10.18.172.0

Broadcast address: 10.18.172.255

Gateway and reachability

Default gateway: 10.18.172.62

Ping to gateway (avg): 3 ms

Ping to 1.1.1.1 (avg): 28 ms

DNS

Configured DNS server(s): 10.18.172.62

example.com resolves to: 104.20.23.154, 172.66.147.243, plus IPv6 addresses

Path to the internet

Hops to example.com: 8

First hop: 10.18.172.62

Listening ports

Port

Protocol

Interface (localhost / all)

Common use

135

TCP

All

Windows RPC

139

TCP

Network interface

NetBIOS Session Service

445

TCP

All

SMB / file and printer sharing

49664–49668

TCP

All

Windows RPC dynamic ports

49674

TCP

All

Windows RPC dynamic port

5040

TCP

All

Service-specific

4343

TCP

All

Service-specific

4449

TCP

All

Service-specific

5141

TCP

All

Service-specific

58995

TCP/IPv6

All IPv6 interfaces

Service-specific

15152, 19443, 46753, 46760, 51779–51782

TCP

Localhost

Local services

Reflection

What surprised me most was how many services were listening on my computer, including several Windows RPC ports and SMB-related ports. Before doing this exercise, I mainly thought of my computer as making outgoing connections rather than also having services waiting for incoming connections. The port scan showed that the distinction between localhost-only services and network-facing services is important. A localhost-only port is much less exposed because other devices on the network normally cannot connect to it, while a service listening on all interfaces can potentially receive network traffic. The open ports I would investigate first are 135, 139, and 445, because they are associated with Windows networking and RPC/SMB and can be security-sensitive if unnecessarily exposed. I would also investigate the less familiar ports such as 4343, 4449, 5040, and 5141 to identify the programs using them. The command I think I will use most often is ipconfig /all because it quickly shows the computer's IP configuration, gateway, DNS server, and network adapter information.
