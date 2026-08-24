Wireshark – Cleartext vs Encrypted Traffic

Course: IT, Varia Vantaa
Files analyzed: U1-03a_http_login.pcap, U1-03a_https_login.pcap
Tool: Wireshark (Follow HTTP Stream / Follow TCP Stream)

Part A – HTTP Capture

1. Login credentials

When filtering for HTTP traffic and following the HTTP stream, the login information can be seen directly in plain text:

username=anna.virtanen&password=Summer2026!&remember=on

So the username is anna.virtanen and the password is Summer2026!.

This shows how unsafe HTTP can be because anyone who is able to capture the traffic could potentially see the user’s login information.

2. HTTP method

Looking at the request directly above the login information shows that the website uses the POST method:

POST /login HTTP/1.1

This means the login information was sent to the server using a POST request rather than being included in the URL with a GET request.

3. Session cookie

After the login, the server sends a session cookie:

Set-Cookie: SESSIONID=a3f9c2e7b81d4f60a5e2c9d10f4b7e88; Path=/; HttpOnly

The session cookie is important because it can be used to identify the logged-in user. If an attacker gets hold of this cookie, they could potentially use it to access the account without knowing the actual password. This is known as session hijacking.

4. Data exposed on the dashboard

The dashboard response also contains information about the user:

<h1>Welcome back, Anna Virtanen</h1>
<p>Role: Finance Administrator</p>
<p>Email: anna.virtanen@pohjola-logistics.local</p>
<p>Last login from 10.10.10.50</p>

This reveals several pieces of information, including Anna’s full name, job role, email address and the IP address of her previous login.

The most sensitive information here is probably her Finance Administrator role and her email address, since this information could potentially be useful to someone trying to target her account.

⸻

Part B – HTTPS Capture

5. Credentials in the HTTPS capture

The login credentials cannot be seen in the HTTPS capture.

After the TLS handshake is completed, the HTTP information, including the request, headers and POST body, is encrypted. Wireshark can still show that communication is happening, but it cannot show the actual login information unless the necessary session keys are provided.

6. SNI in the Client Hello

Even though HTTPS encrypts the actual communication, some information is still visible during the TLS handshake.

The Server Name Indication (SNI) in the Client Hello shows:

lab-portal.local

This means that someone monitoring the network can still see which hostname the client is trying to connect to.

7. What is still observable

Even with HTTPS, some information can still be seen in the capture, such as:

* Source and destination IP addresses: 10.10.10.50 → 10.10.10.10
* Destination port: 443
* Packet sizes
* Timing of the packets
* The SNI hostname

This information does not reveal the actual login credentials or page contents, but it can still show that a connection to a particular service was made and roughly when it happened.

⸻

Part C – Analysis

8. Why protocol choice matters

The main difference between HTTP and HTTPS is how the data is protected.

With HTTP, information such as usernames, passwords, session cookies and webpage content can be read if someone captures the traffic.

With HTTPS, this information is encrypted before being sent across the network. A person monitoring the traffic can still see that a connection exists, but they cannot normally see what is being sent inside that connection.

9. Example of an untrusted network

A good example would be using a laptop on open Wi-Fi at a coffee shop.

If a website uses HTTP, someone else on the same network could potentially capture the traffic and see sensitive information such as login details or session cookies.

HTTPS makes this much safer because the actual content of the connection is encrypted. However, HTTPS does not hide everything. Information such as the destination IP address, SNI, connection timing and traffic size can still be visible.

Conclusion

The biggest thing I noticed from comparing the two captures was how much information was exposed when HTTP was used. It wasn’t only the username and password that could be read. The session cookie and personal account information were also visible in the traffic.

With HTTPS, the connection itself could still be detected, but the actual login information and webpage contents were protected by encryption. This shows why using HTTPS is so important, especially when connecting through networks that cannot be trusted.
