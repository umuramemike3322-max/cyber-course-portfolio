Wireshark - Cleartext vs Encrypted Traffic
Course: IT, Varia Vantaa Files analyzed: U1-03a_http_login.pcap, U1-03a_https_login.pcap Tool: Wireshark (Follow HTTP Stream / Follow TCP Stream)
Part A - HTTP capture
1. Login credentials
Filtering on http and following the HTTP stream shows the login POST body in plain text:
username=anna.virtanen&password=Summer2026!&remember=on
Username: anna.virtanen Password: Summer2026!
2. HTTP method
The request line directly above the credentials confirms the form used POST, not GET:
POST /login HTTP/1.1
3. Session cookie
The server's response after authentication sets a session cookie:
Set-Cookie: SESSIONID=a3f9c2e7b81d4f60a5e2c9d10f4b7e88; Path=/; HttpOnly
This matters because sessions are typically trusted the same way a password is. If someone captures this cookie value and attaches it to their own request to the server, the server has no way of knowing it isn't Anna - this is session hijacking. The attacker never needs to know the actual password.
4. Data exposed on the dashboard
The dashboard response returned after login includes:
<h1>Welcome back, Anna Virtanen</h1>
<p>Role: Finance Administrator</p>
<p>Email: anna.virtanen@pohjola-logistics.local</p>
<p>Last login from 10.10.10.50</p>
Two sensitive items here: her job role (Finance Administrator) and her email address. Her full name and the last-login IP are also disclosed in the same response.
Part B - HTTPS capture
5. Credentials in the HTTPS capture
Not visible anywhere. Once the TLS handshake completes, all HTTP-layer data - the request line, headers, and POST body - is encrypted. Wireshark can show that a request happened, but not what it contained, unless you supply the session keys.
6. SNI in the Client Hello
The Client Hello packet (before encryption begins) still exposes the destination hostname in the Server Name Indication field:
lab-portal.local
7. What's still observable
Even fully encrypted, the capture leaks:
Source/destination IP (10.10.10.50 → 10.10.10.10)
Destination port (443)
Packet sizes and timing
The SNI hostname noted above
None of this reveals login content, but it's enough to know that a connection to a specific service happened, and roughly when.
Part C - Analysis
8. Why protocol choice matters
HTTP leaves everything - credentials, cookies, page content - readable to anyone capturing the traffic. HTTPS encrypts that same data end-to-end, so a passive observer on the network sees only that a connection exists, not what's inside it.
9. Untrusted network example
Connecting a laptop to open Wi-Fi at a coffee shop is a common case. HTTPS keeps the actual content of logins and messages private from anyone else on that network, but it doesn't hide who you're connecting to, when, or how much data is moving - that metadata is still exposed via IP addresses, SNI, and traffic patterns.

The biggest takeaway from this comparison was how completely readable the HTTP capture was - not just the password, but the session cookie and account details right after it. Switching to HTTPS didn't hide the fact that a connection happened, but it did stop the actual login data from being readable on the wire.
