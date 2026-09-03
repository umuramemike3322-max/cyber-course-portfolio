[U1-03e 16.6.4 Packet Tracer - Use Telnet and SSH.zip](https://github.com/user-attachments/files/31774982/U1-03e.16.6.4.Packet.Tracer.-.Use.Telnet.and.SSH.zip)
# 16.6.4 Packet Tracer – Use Telnet and SSH

## Addressing Table

| Device | Interface | IP Address   | Subnet Mask     |
|--------|-----------|--------------|-----------------|
| HQ     | G0/0/1    | 64.100.1.1   | 255.255.255.0   |
| PC0    | NIC       | DHCP         |                 |
| PC1    | NIC       | DHCP         |                 |

---

## Part 1: Verify Connectivity

### Step 1: Verify IP address on a PC

**Question:** What command did you use to verify the IP address from DHCP?

**Answer:**  
`ipconfig`  
(or `ipconfig /all` if you want more details)

### Step 2: Verify connectivity to HQ

Ping the router using:

```
ping 64.100.1.1
```

You should get successful replies.

---

## Part 2: Access a Remote Device

### Step 1: Telnet to HQ

Command used:

```
telnet 64.100.1.1
```

**Question:** Were you successful? What was the output?

**Answer:**  
No.  

```
C:\>telnet 64.100.1.1
Trying 64.100.1.1 ...Open
[Connection to 64.100.1.1 closed by foreign host]
```

Telnet is blocked on the router (only SSH is allowed).

### Step 2: SSH to HQ

Command used:

```
ssh -l admin 64.100.1.1
```

Password: `class`

**Question:** What is the prompt after accessing the router successfully via SSH?

**Answer:**  
`HQ#`
