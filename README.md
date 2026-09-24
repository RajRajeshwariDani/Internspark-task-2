# 🔐 Cybersecurity Internship – Practical Security Tasks
## 📌 Project Overview

This repository contains my practical cybersecurity internship work completed in a controlled and authorized laboratory environment using Kali Linux.

The project focuses on practical understanding of:

- Web Application Security
- Vulnerability Identification
- DVWA
- Burp Suite
- Cross-Site Scripting (XSS)
- SQL Injection
- Network Traffic Analysis
- Wireshark
- DNS
- TCP
- HTTP/HTTPS
- ICMP
- ARP
- Basic Security Analysis
- Security Mitigation

All testing was performed only against intentionally vulnerable applications and local laboratory systems.

> ⚠️ Ethical Use: The techniques demonstrated in this repository are intended only for authorized security testing, cybersecurity education, and controlled laboratory environments.

---

# 🛠️ Tools and Technologies Used

| Tool | Purpose |
|---|---|
| Kali Linux | Cybersecurity testing environment |
| VirtualBox | Virtual machine environment |
| Docker | Container management |
| DVWA | Intentionally vulnerable web application |
| Burp Suite Community Edition | HTTP request interception and analysis |
| Wireshark | Network packet capture and analysis |
| Firefox | Web application testing |
| Nmap | Service and port identification |
| Terminal | Linux commands and troubleshooting |

---

# 📂 Project Structure

```text
Cybersecurity-Internship/
│
├── README.md
│
├── Screenshots/
│   ├── dvwa-login.png
│   ├── dvwa-security-low.png
│   ├── burp-interception.png
│   ├── reflected-xss.png
│   ├── sql-injection.png
│   ├── wireshark-dns.png
│   ├── wireshark-tcp.png
│   ├── wireshark-http.png
│   ├── wireshark-https.png
│   ├── wireshark-icmp.png
│   └── wireshark-packet-details.png
│
├── Reports/
│   └── Cybersecurity_Internship_Report.pdf
│
└── Evidence/
    └── network-capture.pcapng
1. LAB ENVIRONMENT
Operating System
Kali Linux
Virtualization
Oracle VirtualBox
Target Application
Damn Vulnerable Web Application (DVWA)
Target Address
http://127.0.0.1:8081
The application was intentionally hosted locally so that testing could be performed safely.
2. INITIAL SYSTEM CHECK
Check the current user:
whoami
Check Linux information:
uname -a
Check Kali version:
cat /etc/os-release
Check IP configuration:
ip addr
Check network interfaces:
ip link
Check routing:
ip route
Check NetworkManager status:
nmcli device status
3. NETWORK CONNECTIVITY TEST
Before downloading Docker images or performing network-related tasks, connectivity was checked.
Run:
ping -c 3 google.com
Successful output should show:
3 packets transmitted
3 received
0% packet loss
DNS resolution can also be checked using:
nslookup google.com
or:
dig google.com
4. DOCKER SETUP
Check Docker installation:
docker --version
Start Docker:
sudo systemctl start docker
Enable Docker at system startup:
sudo systemctl enable docker
Check Docker service:
sudo systemctl status docker
Test Docker:
sudo docker ps
If the Docker permission error appears:
permission denied while trying to connect to the Docker daemon socket
use:
sudo docker ps
The Docker service must be running before starting DVWA.
5. DOWNLOAD AND START DVWA
Run:
sudo docker run -d --name dvwa -p 8081:80 vulnerables/web-dvwa
Explanation:
docker run
Creates and starts a container.

-d
Runs the container in the background.

--name dvwa
Gives the container the name "dvwa".

-p 8081:80
Maps Kali Linux port 8081 to the container's web server port 80.

vulnerables/web-dvwa
DVWA Docker image.
If the image is not available locally, Docker downloads it from the configured registry.
Verify:
sudo docker ps
The output should show the DVWA container running.
6. CHECK DVWA CONTAINER
List running containers:
sudo docker ps
List all containers:
sudo docker ps -a
View DVWA logs:
sudo docker logs dvwa
Stop DVWA:
sudo docker stop dvwa
Start it again:
sudo docker start dvwa
Remove the container only when it is no longer required:
sudo docker rm -f dvwa
7. OPEN DVWA
Open Firefox and visit:
http://127.0.0.1:8081
Default DVWA credentials:
Username: admin
Password: password
After login, open:
Setup / Reset DB
Click:
Create / Reset Database
After successful database initialization, return to the DVWA application.
8. DVWA SECURITY CONFIGURATION
Open:
DVWA Security
Set:
Security Level: Low
Click:
Submit
The Low security level is used because DVWA is intentionally designed to demonstrate vulnerable coding practices.
This environment should remain isolated from real-world systems.
9. DVWA APPLICATION AREAS
DVWA contains several intentionally vulnerable modules:
Brute Force
Command Injection
CSRF
File Inclusion
File Upload
Insecure CAPTCHA
SQL Injection
SQL Injection (Blind)
Weak Session IDs
XSS (DOM)
XSS (Reflected)
XSS (Stored)
CSP Bypass
JavaScript
DVWA Security
PHP Info
For this practical task, the primary tests were:
XSS (Reflected)
SQL Injection
10. BURP SUITE
Start Burp Suite:
burpsuite
Select:
Temporary Project
Then open:
Proxy
→ Intercept
Set:
Intercept: ON
Burp Suite acts as an interception proxy between the browser and the web application.
Basic communication:
Browser
    |
    v
Burp Suite
    |
    v
DVWA
    |
    v
Burp Suite
    |
    v
Browser
11. BURP SUITE REQUEST INTERCEPTION
Open:
http://127.0.0.1:8081
Perform any normal action in DVWA.
Burp Suite should display the HTTP request.
Example:
GET / HTTP/1.1
Host: 127.0.0.1:8081
Click:
Forward
This sends the request to the DVWA server.
Important request components include:
HTTP Method
URL
Host
Headers
Cookies
Parameters
Request Body
12. REFLECTED XSS TEST
Navigate to:
XSS (Reflected)
Use the controlled laboratory proof-of-concept:
HTML
<script>alert('XSS-Test')</script>
Submit the input.
If the application is vulnerable at the selected security level, the browser may execute the JavaScript and display:
XSS-Test
13. REFLECTED XSS EXPLANATION
Cross-Site Scripting occurs when untrusted input is inserted into a web page without appropriate output encoding or other contextual protections.
Basic flow:
Attacker-controlled input
          |
          v
Web application
          |
          v
Input reflected into response
          |
          v
Browser
          |
          v
Script execution
In this laboratory, DVWA intentionally contains the vulnerable behavior.
14. XSS SECURITY IMPACT
Depending on the application context, XSS can potentially lead to:
Unauthorized browser-side actions
Page content manipulation
Phishing
User redirection
Session-related attacks
Data exposure
The actual impact depends on application design, browser controls, authentication mechanisms, and other security protections.
15. XSS MITIGATION
Recommended defenses include:
1. Context-aware output encoding
2. Input validation
3. Safe DOM manipulation
4. Content Security Policy (CSP)
5. Secure cookie configuration
6. Avoiding dangerous HTML insertion
7. Treating user input as untrusted
Example security header:
Content-Security-Policy
Cookies should also use appropriate attributes such as:
HttpOnly
Secure
SameSite
where applicable.
16. SQL INJECTION TEST
Navigate to:
SQL Injection
Use the controlled DVWA laboratory input:
1' OR '1'='1
Submit the input.
The purpose of this test is to demonstrate how unsafe SQL string construction can allow user input to influence SQL query structure.
17. SQL INJECTION CONCEPT
A vulnerable application may conceptually construct:
SELECT * FROM users WHERE user_id = 'USER_INPUT';
If the application directly concatenates untrusted input into the SQL statement, the resulting query structure can be altered.
Example laboratory input:
1' OR '1'='1
This demonstrates why applications must not construct SQL queries by directly concatenating user input.
18. SQL INJECTION IMPACT
Depending on the application and database permissions, SQL Injection can potentially result in:
Unauthorized data access
Authentication bypass
Data disclosure
Data modification
Database manipulation
The severity depends on database privileges and application architecture.
19. SQL INJECTION MITIGATION
The primary defense is parameterized SQL.
Unsafe concept:
SELECT * FROM users WHERE user_id = 'USER_INPUT';
Safer concept:
SELECT * FROM users WHERE user_id = ?;
The value is supplied separately as a parameter.
Additional controls:
1. Prepared statements
2. Parameterized queries
3. Input validation
4. Least-privilege database accounts
5. Secure database configuration
6. Error handling that does not expose sensitive details
20. NMAP SERVICE CHECK
Nmap can be used to identify services on the authorized local laboratory target.
Example:
nmap -sV 127.0.0.1
For the DVWA port:
nmap -sV -p 8081 127.0.0.1
Example interpretation:
PORT      STATE SERVICE VERSION
8081/tcp  open  http    ...
The scan should only be performed against systems that are owned or explicitly authorized for testing.
21. WEB APPLICATION SECURITY FINDINGS
Finding
Observation
Risk
Recommended Defense
Reflected XSS
User input reflected into response
Browser-side script execution
Output encoding + CSP
SQL Injection
Input influences SQL query structure
Unauthorized database access
Prepared statements
Missing security headers
Some headers may be absent
Browser-side security protections reduced
Configure security headers
Information disclosure
Server/application information may be visible
Fingerprinting
Minimize exposed version details
22. NIKTO WEB SERVER CHECK
Nikto can be used against the authorized local DVWA environment.
Example:
nikto -h http://127.0.0.1:8081 -output nikto-report.txt
View the report:
cat nikto-report.txt
The report may identify:
Missing security headers
Server information
Uncommon HTTP headers
Potentially interesting files
Web server configuration observations
Nikto findings should be interpreted as security observations rather than automatically confirmed vulnerabilities.
23. NIKTO REPORT INTERPRETATION
Typical observations can include:
X-Frame-Options not present
X-Content-Type-Options not set
Server information exposed
Application-specific headers
Possible mitigations:
X-Frame-Options
X-Content-Type-Options
Content-Security-Policy
Referrer-Policy
Strict-Transport-Security
Only enable headers appropriate to the application's architecture and deployment.
24. WIRESHARK PACKET ANALYSIS
Start Wireshark:
wireshark
Select the active network interface.
Check the active interface first:
nmcli device status
or:
ip addr
The interface showing:
connected
is normally the interface to select.
25. START PACKET CAPTURE
In Wireshark:
Select active interface
        ↓
Click Start
        ↓
Generate traffic
        ↓
Stop capture
        ↓
Analyze packets
        ↓
Save capture
Save the capture as:
network-capture.pcapng
26. GENERATE DNS TRAFFIC
Run:
nslookup example.com
or:
dig example.com
Wireshark filter:
dns
Observe:
Source IP
Destination IP
DNS query
DNS response
Query name
Response
UDP port 53
27. DNS EXPLANATION
DNS translates domain names into IP addresses.
Basic flow:
Client
   |
   | DNS Query
   v
DNS Server
   |
   | DNS Response
   v
Client
Common DNS port:
UDP 53
DNS can also use TCP in certain situations.
28. TCP ANALYSIS
Wireshark filter:
tcp
The TCP three-way handshake is:
Client                     Server

SYN --------------------->

     <-------------------- SYN/ACK

ACK --------------------->

Connection established
Important TCP fields:
Source Port
Destination Port
Sequence Number
Acknowledgment Number
TCP Flags
Window Size
29. TCP FLAGS
Common flags include:
SYN
ACK
FIN
RST
PSH
URG
A normal TCP connection establishment generally uses:
SYN
SYN + ACK
ACK
30. HTTPS/TLS ANALYSIS
Wireshark filter:
tls
Observe:
Client Hello
Server Hello
Certificate
Encrypted Application Data
HTTPS uses TLS to protect application data during transmission.
Basic flow:
Browser
    |
    v
TLS Handshake
    |
    v
Secure Session
    |
    v
Encrypted Application Data
31. HTTP ANALYSIS
Wireshark filter:
http
Possible HTTP information includes:
GET
POST
Host
HTTP version
Response status
Headers
Common response codes:
200 OK
301 Moved Permanently
302 Found
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
500 Internal Server Error
32. ICMP ANALYSIS
Wireshark filter:
icmp
Generate ICMP traffic:
ping -c 3 example.com
Observe:
Echo Request
Echo Reply
Communication:
Client
   |
   | Echo Request
   v
Server
   |
   | Echo Reply
   v
Client
33. ARP ANALYSIS
Wireshark filter:
arp
ARP maps an IPv4 address to a MAC address on a local network.
Typical communication:
ARP Request
"Who has this IP?"

        ↓

ARP Reply
"This MAC address has that IP."
ARP is primarily relevant to local IPv4 network communication.
34. IPV6 ANALYSIS
If IPv6 packets are present:
ipv6
Observe:
Source IPv6
Destination IPv6
Next Header
Packet Length
IPv6 uses 128-bit addresses.
35. USEFUL WIRESHARK FILTERS
DNS:
dns
TCP:
tcp
HTTP:
http
TLS:
tls
ICMP:
icmp
ARP:
arp
IPv6:
ipv6
HTTP port:
tcp.port == 80
HTTPS port:
tcp.port == 443
DNS:
udp.port == 53
Specific IP:
ip.addr == 192.168.1.10
TCP SYN:
tcp.flags.syn == 1
TCP SYN without ACK:
tcp.flags.syn == 1 && tcp.flags.ack == 0
36. USEFUL LINUX NETWORK COMMANDS
Display IP addresses:
ip addr
Display interfaces:
ip link
Display routes:
ip route
Display network status:
nmcli device status
Test connectivity:
ping -c 3 google.com
DNS lookup:
nslookup example.com
Detailed DNS lookup:
dig example.com
HTTPS request:
curl https://example.com
HTTP headers:
curl -I https://example.com
37. WIRESHARK ANALYSIS TABLE
Protocol
Purpose
Important Information
DNS
Domain resolution
Query and response
TCP
Reliable transport
Ports, flags, sequence numbers
TLS
Secure communication
Handshake and encrypted data
HTTP
Web communication
Requests and responses
ICMP
Connectivity testing
Echo request/reply
ARP
Local address resolution
IP and MAC
IPv6
IPv6 networking
IPv6 addresses
38. SECURITY OBSERVATIONS
The practical work demonstrated that cybersecurity analysis requires visibility at multiple layers.
Application Layer
XSS
SQL Injection
HTTP requests
HTTP responses
Security headers
Transport Layer
TCP
Ports
TCP flags
TLS
Network Layer
IP
IPv4
IPv6
ICMP
Local Network
ARP
MAC addresses
Network interfaces
39. IMPORTANT SECURITY LESSONS
The practical tasks demonstrated the importance of:
1. Input validation
2. Output encoding
3. Parameterized SQL queries
4. Secure HTTP headers
5. TLS encryption
6. Network monitoring
7. Packet analysis
8. Least privilege
9. Secure configuration
10. Continuous security testing
40. EVIDENCE / SCREENSHOTS
The following screenshots should be included in the repository:
1. DVWA login page
2. DVWA database setup
3. DVWA security level
4. Burp Suite interception
5. Reflected XSS result
6. SQL Injection result
7. Nmap result
8. Nikto report
9. Wireshark interface
10. DNS packet analysis
11. TCP handshake
12. HTTP packet
13. TLS/HTTPS packet
14. ICMP packet
15. ARP packet
16. Packet details
Screenshots should clearly show the relevant application, command, filter, or packet information.
41. REPORTING FORMAT
Each finding should be documented using:
Finding
↓
Description
↓
Evidence
↓
Security Impact
↓
Risk
↓
Recommended Mitigation
Example:
Finding:
Reflected Cross-Site Scripting

Description:
The controlled DVWA application reflected user-supplied input into the HTTP response without adequate output encoding.

Evidence:
DVWA XSS (Reflected) page and browser alert.

Impact:
An attacker could potentially execute browser-side script in a vulnerable application context.

Mitigation:
Use context-aware output encoding, input validation, CSP, and secure development practices.
42. OVERALL SECURITY ASSESSMENT
The practical assessment successfully demonstrated common web application vulnerabilities and basic network traffic analysis in a controlled environment.
The web application testing demonstrated:
Reflected XSS
SQL Injection
HTTP request interception
Security header observations
Web server enumeration
The network analysis demonstrated:
DNS
TCP
HTTP
TLS
ICMP
ARP
IPv6
The practical exercises provided experience with identifying security issues, collecting evidence, understanding network communication, and recommending appropriate mitigations.
43. FINAL CONCLUSION
This internship practical work provided hands-on experience in both web application security and network security analysis.
DVWA was used as an intentionally vulnerable web application to safely understand common vulnerabilities such as Cross-Site Scripting and SQL Injection.
Burp Suite was used to inspect HTTP requests, while Nmap and Nikto were used for authorized service and web-server assessment.
Wireshark was used to analyze network traffic including DNS, TCP, HTTP, TLS, ICMP, ARP, and IPv6.
The main learning outcome was understanding how security vulnerabilities appear in real application and network traffic and how defensive controls can reduce the associated risks.
44. GITHUB UPLOAD COMMANDS
After creating the project folder, open the terminal inside it.
Check files:
ls
Initialize Git:
git init
Add all files:
git add .
Check staged files:
git status
Create the first commit:
git commit -m "Add cybersecurity internship practical tasks"
Rename the branch:
git branch -M main
Connect the GitHub repository:
git remote add origin YOUR_GITHUB_REPOSITORY_URL
Example:
git remote add origin https://github.com/YOUR-USERNAME/Cybersecurity-Internship.git
Push the project:
git push -u origin main
45. FUTURE UPDATES
Additional cybersecurity tasks can be added to the same repository.
Possible future work:
SOC monitoring
Log analysis
Incident response
Vulnerability management
Linux security
Cloud security
Threat detection
SIEM analysis
Security automation
46. ETHICAL DISCLAIMER
This repository is created for:
Cybersecurity education
Authorized security testing
Internship training
Laboratory experimentation
Defensive security learning
Testing must only be performed on systems for which explicit authorization has been obtained.
Never perform security testing against public websites, networks, accounts, or systems without permission.
👩‍💻 Author
Rajeshwari Dani
Cybersecurity Student | CEH | VAPT | Web Application Security | Network Security
⭐ Skills Demonstrated
Kali Linux
Docker
DVWA
Burp Suite
Wireshark
Nmap
Nikto
Web Application Security
XSS
SQL Injection
HTTP Analysis
Network Packet Analysis
DNS Analysis
TCP Analysis
TLS Analysis
Linux Networking
Security Testing
Vulnerability Analysis
Security Mitigation
📌 Repository Purpose
This repository serves as a practical cybersecurity portfolio demonstrating hands-on understanding of:
Web Application Security
        +
Network Security
        +
Vulnerability Assessment
        +
Packet Analysis
        +
Security Documentation
All activities were performed in a controlled and authorized laboratory environment.
