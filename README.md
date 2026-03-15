# ■■ Mini SOC Home Lab
**Security Operations Center — Practical Lab Documentation**
By Saravanan | [GitHub](https://github.com/Saravanan-Patrick) | [LinkedIn](https://linkedin.com/in/saravanan-cyber)

> ■■ This is a fully isolated, controlled lab environment. No real systems were targeted. All simulations performed on personal VMs for educational purposes only.
---
## ■ About This Lab
This Mini SOC Home Lab was built from scratch to simulate real-world attack and defense scenarios. As someone transitioning from Food Technology into Cybersecurity with a focus on SOC Analysis, this lab documents my hands-on learning journey — from setting up an isolated network to running actual attack simulations and capturing the traffic as a SOC analyst would.

> ■ This lab proves that you don't need a corporate network or expensive equipment to build real cybersecurity skills. Just two VMs, VMware, and curiosity.
---

## ■■ Lab Environment
| Component | Details |
|-----------|---------|
| Hypervisor | VMware Workstation Pro 25H2 |
| Attacker Machine | Kali Linux 2025.4 (amd64) |
| Defender / Target | Windows 10 x64 |
| Network Type | VMware LAN Segment — Isolated (testpractice) |
| Attacker IP | 192.168.20.11 (Static) |
| Target IP | 192.168.20.10 (Static) |
| Internet Access | None — Fully Air-Gapped Lab |
| Nmap Version | 7.95 |

## ■ Lab 01 — Network Reconnaissance with Nmap
### Objective
Simulate how an attacker performs network reconnaissance against a Windows target, and document findings the way a SOC analyst would.
### Tools Used
- Nmap 7.95 — Network scanner and port discovery
- Wireshark — Packet capture and traffic analysis
- Kali Linux Terminal — Attacker platform
### ■■ Attack Simulation (Kali Linux)
**Step 1 — Verify Connectivity**
```bash
ping 192.168.20.10
```
Result: Successful ICMP replies — target is reachable.
**Step 2 — Service Version Scan**
```bash
nmap -sV 192.168.20.10
```
**Step 3 — Save Results**
```bash
nmap -sV 192.168.20.10 -oN nmap-scan-results.txt
```

### ■ Nmap Findings
| Port | State | Service | Version |
|------|-------|---------|---------|
| 135/tcp | OPEN | msrpc | Microsoft Windows RPC |
| 139/tcp | OPEN | netbios-ssn | Microsoft Windows NetBIOS |
| 445/tcp | OPEN | microsoft-ds | SMB — Windows File Sharing |
| 997 ports | CLOSED | — | TCP RST response |
**OS Detected:** Windows — CPE: cpe:/o:microsoft:windows

### ■ Detection — Wireshark Analysis
| Metric | Value |
|--------|-------|
| Total Packets Captured | 2,248 |
| Packets Dropped | 0 (0.0%) |
| Source IP (Attacker) | 192.168.20.11 |
| Destination IP (Target) | 192.168.20.10 |

**Key Protocol Observations:**
| Protocol | Observation |
|----------|-------------|
| TCP SYN | Kali sending SYN to all 1000 ports — classic port scan pattern |
| TCP RST/ACK | Windows responding — confirming port states |
| SMB | Server Message Block traffic on port 445 |
| NBSS | NetBIOS Session Service activity |
| MS Browser | Microsoft Windows Browser Protocol |

### ■ Indicators of Compromise (IOCs)
| IOC | Details |
|-----|---------|
| Source IP | 192.168.20.11 (Kali — Attacker) |
| Scan Type | TCP SYN Service Version Detection |
| Ports Targeted | Top 1000 TCP ports |
| Date/Time | 2026-03-14 at 06:48 EDT |
| Scan Duration | ~22 seconds |
| Tool Identified | Nmap 7.95 |
| Packets Generated | 2,248 |

### ■■ Security Observations
- **Port 445 (SMB)** — Same port exploited in WannaCry ransomware (2017). Should be blocked at perimeter firewall.
- **Port 135 (RPC)** — Used for lateral movement in enterprise attacks.
- **Windows Firewall** — When enabled, all 1000 ports showed as FILTERED. Firewall is effective.
- **Scan Speed** — 1000 ports in 22 seconds. A real SIEM would trigger a port scan alert.

### ■ What I Learned
- How to perform network reconnaissance using Nmap
- How to capture and analyze live traffic with Wireshark
- How to identify port scan patterns from TCP SYN/RST packets
- Security significance of SMB (445) and RPC (135)
- How Windows Firewall affects scan results
- How to document findings as IOCs

## ■ Repository Structure
```
Mini-SOC-Home-Lab/
■■■ README.md
■■■ Lab-01-Nmap-Reconnaissance/
■ ■■■ nmap-scan-results.txt
■ ■■■ nmap-scan-capture.pcapng
■ ■■■ screenshots/
■ ■■■ vmware-lab-setup.png
■ ■■■ kali-ifconfig.png
■ ■■■ win10-ipconfig.png
■ ■■■ nmap-scan-output.png
■ ■■■ wireshark-capture.png


## ■■ About Me
Transitioning from Food Technology into Cybersecurity with a focus on SOC Analysis and Blue Team operations. This lab documents my hands-on learning journey.
- ■ LinkedIn:
[linkedin.com/in/saravanan-cyber](https://linkedin.com/in/saravanan-cyber)
- ■ Email: career.entrydesk@gmail.com
- ■ Thiruvallur, Tamil Nadu, India
---
*"The best way to learn cybersecurity is to break things in a safe environment and understand why they broke."*
■ If this lab helped you, give it a star!
