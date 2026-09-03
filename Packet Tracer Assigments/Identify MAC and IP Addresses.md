[U1-02c 13.1.3 Packet Tracer - Identify MAC and IP Addresses.zip](https://github.com/user-attachments/files/31773961/U1-02c.13.1.3.Packet.Tracer.-.Identify.MAC.and.IP.Addresses.zip)
# 13.1.3 Packet Tracer – Identify MAC and IP Addresses

## Part 1 – Local communication (172.16.31.3 → 172.16.31.2)

| At Device          | Src MAC          | Dest. MAC        | Src IPv4     | Dest IPv4    |
|--------------------|------------------|------------------|--------------|--------------|
| 172.16.31.3        | 0060.7036.2849   | 000C:85CC:1DA7   | 172.16.31.3  | 172.16.31.2  |
| Switch 2           | 0060.7036.2849   | 000C:85CC:1DA7   | N/A          | N/A          |
| 172.16.31.2 (in)   | 000C:85CC:1DA7   | 000C:85CC:1DA7   | 172.16.31.3  | 172.16.31.2  |
| 172.16.31.2 (out)  | 0060.7036.2849   | 0060.7036.2849   | 172.16.31.2  | 172.16.31.3  |

**Question (outbound PDU):**  
Source and destination addresses are swapped (both MAC and IP) because this is the echo-reply going back to 172.16.31.3.

---

## Part 2 – Remote communication (172.16.31.3 → 10.10.10.2)

**Question:** The destination MAC (`00D0:BA8E:741A`) belongs to the router’s FastEthernet interface on the 172.16.31.0 network.

### Echo request table

| At Device     | Src MAC          | Dest. MAC        | Src IPv4     | Dest IPv4    |
|---------------|------------------|------------------|--------------|--------------|
| 172.16.31.3   | 0060.7036.2849   | 00D0:BA8E:741A   | 172.16.31.3  | 10.10.10.2   |
| Switch 2      | 0060.7036.2849   | 00D0:BA8E:741A   | N/A          | N/A          |
| Router (in)   | 0060.7036.2849   | 00D0:BA8E:741A   | 172.16.31.3  | 10.10.10.2   |
| Router (out)  | 00D0:588C:2401   | 0060:2F84:4AB6   | 172.16.31.3  | 10.10.10.2   |
| Switch 1      | 00D0:588C:2401   | 0060:2F84:4AB6   | N/A          | N/A          |
| Access Point  | N/A              | N/A              | N/A          | N/A          |
| 10.10.10.2    | 0060:2F84:4AB6   | 00D0:588C:2401   | 10.10.10.2   | 172.16.31.3  |

### Echo-reply table (from 10.10.10.2 back)

| At Device     | Src MAC          | Dest. MAC        | Src IPv4     | Dest IPv4    |
|---------------|------------------|------------------|--------------|--------------|
| 10.10.10.2    | 0060:2F84:4AB6   | 00D0:588C:2401   | 10.10.10.2   | 172.16.31.3  |
| Access Point  | N/A              | N/A              | N/A          | N/A          |
| Switch 1      | 0060:2F84:4AB6   | 00D0:588C:2401   | N/A          | N/A          |
| Router (in)   | 0060:2F84:4AB6   | 00D0:588C:2401   | 10.10.10.2   | 172.16.31.3  |
| Router (out)  | 00D0:BA8E:741A   | 0060.7036.2849   | 10.10.10.2   | 172.16.31.3  |
| Switch 2      | 00D0:BA8E:741A   | 0060.7036.2849   | N/A          | N/A          |
| 172.16.31.3   | 00D0:BA8E:741A   | 0060.7036.2849   | 10.10.10.2   | 172.16.31.3  |

---

## Reflection Questions

1. **What different types of cables/media were used to connect devices?**  
   Copper (Ethernet) and wireless.

2. **Did the cables change the handling of the PDU in any way?**  
   No.

3. **Did the wireless Access Point do anything to the PDUs that it received?**  
   It converts the frame to wireless (802.11) and back.

4. **Was PDU addressing changed by the access point?**  
   No.

5. **What was the highest OSI layer that the Access Point used?**  
   Layer 1 / Layer 2 (data-link for the wireless side).

6. **At what Layer of the OSI model do cables and access points operate?**  
   Layer 1 (physical) and Layer 2 (data-link).

7. **When examining the PDU Details tab, which MAC address appeared first, the source or the destination?**  
   Destination MAC.

8. **Sometimes PDUs were marked with red Xs while others had green check marks. What is the significance of these markings?**  
   Green check = successful delivery, red X = dropped / failed.

9. **Every time that the PDU was sent between the 10 network and the 172 network, there was a point where the MAC addresses suddenly changed. Where did that occur?**  
   At the router.

10. **Which device uses MAC addresses that start with 00D0:BA?**  
    The router.

11. **What devices did the other MAC addresses belong to?**  
    The two end hosts (PCs).

12. **Did the sending and receiving IPv4 addresses change in any of the PDUs?**  
    No – source and destination IPs stay the same the whole way.

13. **When you follow the reply to a ping, sometimes called a *pong*, what happens to the source and destination addresses?**  
    They swap (source becomes destination and vice-versa).

14. **Why do you think the interfaces of the router are part of two different IP networks?**  
    So each interface can be on a different network and route between them.

15. **Which IP networks are connected by the router?**  
    172.16.31.0/24 and 10.10.10.0/24.
