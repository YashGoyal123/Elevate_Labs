# Elevate_Labs

## Task 1

# 🔐 Cyber Security Internship Task – Network Reconnaissance (Linux)

## 📌 Objective
The goal of this task is to:
- Discover devices in the **local network**.
- Identify their **open ports** using **Nmap**.
- Capture and analyze the scanning activity with **Wireshark**.
- Understand the **security risks** of exposed ports.

---

## 🛠 Tools Used
- **Linux (Ubuntu/Kali)**  
- **Nmap** → for scanning open ports.  
- **Wireshark** → for analyzing network traffic.  

---

## 🚀 Steps Performed

### 1️⃣ Install Tools
On Linux (Ubuntu/Kali), installed tools with:
```bash```
sudo apt update
sudo apt install nmap wireshark -y


### 2️⃣ Find Local IP Range

Checked the machine’s IP and subnet:
ifconfig

### 3️⃣ Run Nmap Scan

Performed a TCP SYN scan across the network:

nmap -sS 192.168.1.0/24 -oN scan_results.txt


-sS → TCP SYN scan (stealth scan).

-oN → saved results in normal text format.


### 4️⃣ Analyze with Wireshark

Opened Wireshark with:

sudo wireshark


Selected the active network interface (wlan0 or eth0).

Started capturing packets.

Ran the Nmap scan again during capture.

Applied filters:

ip → show only IPv4 traffic.

tcp.flags.syn == 1 → show SYN packets from scan.

Observed:

Open port: SYN → SYN/ACK → RST.

Closed port: SYN → RST.

Saved the capture as scan_capture.pcapng.

### 📊 Results
✅ Nmap Output (Sample)
Nmap scan report for 192.168.1.1
Host is up (0.0030s latency).
PORT     STATE  SERVICE
22/tcp   open   ssh
80/tcp   open   http
443/tcp  open   https

Nmap scan report for 192.168.1.15
Host is up (0.0010s latency).
PORT     STATE  SERVICE
3389/tcp open   ms-wbt-server

✅ Wireshark Endpoints Table (Sample)
IP Address	Packets	Bytes
192.168.1.15	230	18 KB
192.168.1.1	150	12 KB
192.168.1.10	80	6 KB

(IPs anonymized for privacy – replace with your own results)

📝 Key Learnings

How to perform a TCP SYN scan with Nmap.

How to analyze scan packets in Wireshark.

Difference between open/closed port responses.


-----------------------------------------------------------------------------------------------------------------------------------------------------------------

Task 2
📧 Cyber Security Internship Task – Phishing Email Analysis (Linux)
📌 Objective

The goal of this task is to:

Obtain a sample phishing email.

Analyze its headers, sender details, and links.

Identify phishing indicators like spoofed domains, fake links, and urgent language.

Document findings in a structured report.

🛠 Tools Used

Linux (Ubuntu/Kali)

Nano / Cat → for viewing email file contents.

Grep → for extracting suspicious links.

Whois → for domain verification.

Curl → for checking suspicious links safely.

🚀 Steps Performed
1️⃣ Get a Sample Phishing Email

Created a sample phishing email file:

nano phishing_sample.eml


Example content:

From: "PayPal Security" <security@paypai.com>
Reply-To: security@paypai.com
Subject: URGENT: Verify Your Account Immediately!
Date: Tue, 23 Sep 2025 09:30:00 +0000

Dear Customer,

We noticed unusual activity on your PayPal account. 
Please verify your account immediately to avoid suspension.

Click here to verify: http://paypalsecure-login.com

Thank you,
PayPal Support


Saved the file as phishing_sample.eml.

2️⃣ Analyze Email Headers

Displayed headers with:

cat phishing_sample.eml | less


Findings:

From: security@paypai.com → spoofed domain (typo: "paypai.com").

Reply-To: attacker-controlled email.

Subject: urgent request → classic social engineering.

3️⃣ Extract Suspicious Links

Used grep to list URLs:

grep -oP '(http|https)://[^\s]+' phishing_sample.eml


Output:

http://paypalsecure-login.com

4️⃣ Verify the Domain

Checked domain registration:

whois paypalsecure-login.com


Result:

No match for domain "PAYPALSECURE-LOGIN.COM".


✅ This shows the phishing domain was either taken down or never properly registered.

5️⃣ Test Link Safely

Fetched headers only (no page load):

curl -I http://paypalsecure-login.com


No valid response.

Confirms the domain is inactive, but the email itself remains malicious.

📊 Results
✅ Phishing Indicators Found

Spoofed Sender: Pretending to be PayPal (paypai.com).

Suspicious Link: Fake URL paypalsecure-login.com.

Urgent Language: “Verify immediately or account suspended.”

Social Engineering: Uses fear to trick user.

📝 Key Learnings

How to read and analyze raw email headers.

How to detect spoofed domains and mismatched links.

Use of whois and curl to validate domains safely.

Real-world phishing often uses urgency, fear, and fake branding.

Even inactive domains can indicate prior phishing infrastructure.

Why open ports can expose services to attackers.

Importance of using firewalls to control access.
