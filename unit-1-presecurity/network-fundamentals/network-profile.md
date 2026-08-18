# Network Profile — Windows PC

## Identity

* IPv4 address: `10.18.172.220`
* Subnet mask / CIDR: `255.255.255.0` / `/24`
* MAC address: `58-02-05-21-46-XX`
* Network address: `10.18.172.0`
* Broadcast address: `10.18.172.255`

## Gateway and reachability

* Default gateway: `10.18.172.62`
* Ping to gateway (avg): `3 ms`
* Ping to 1.1.1.1 (avg): `28 ms`

## DNS

* Configured DNS server(s): `10.18.172.62`
* example.com resolves to: `104.20.23.154`, `172.66.147.243`, plus IPv6 addresses

## Path to the internet

* Hops to example.com: `8`
* First hop: `10.18.172.62`

## Listening ports

| Port                                    | Protocol | Interface (localhost / all) | Common use                     |
| --------------------------------------- | -------- | --------------------------- | ------------------------------ |
| 135                                     | TCP      | All                         | Windows RPC                    |
| 139                                     | TCP      | Network                     | NetBIOS Session Service        |
| 445                                     | TCP      | All                         | SMB / file and printer sharing |
| 49664–49668                             | TCP      | All                         | Windows RPC dynamic ports      |
| 49674                                   | TCP      | All                         | Windows RPC dynamic port       |
| 5040                                    | TCP      | All                         | Service-specific               |
| 4343                                    | TCP      | All                         | Service-specific               |
| 4449                                    | TCP      | All                         | Service-specific               |
| 5141                                    | TCP      | All                         | Service-specific               |
| 58995                                   | TCP/IPv6 | All IPv6 interfaces         | Service-specific               |
| 15152, 19443, 46753, 46760, 51779–51782 | TCP      | Localhost                   | Local services                 |


* I was surprised by how many services were listening on my computer, including Windows RPC and SMB-related ports. I usually think of my computer as making outgoing connections, but it also has services waiting for incoming connections.
* I would investigate ports 135, 139, and 445 first because they are related to Windows networking and RPC/SMB. I would also check the less familiar ports such as 4343, 4449, 5040, and 5141 to see which programs use them and whether they are necessary.
* I think I will use `ipconfig /all` most often because it quickly shows my IP address, subnet mask, gateway, DNS server, and network adapter information.
