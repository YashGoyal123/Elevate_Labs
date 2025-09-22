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

Why open ports can expose services to attackers.

Importance of using firewalls to control access.
