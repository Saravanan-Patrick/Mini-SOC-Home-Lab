# Mini-SOC-Home-Lab
## Security Operations Center — Practical Lab Documentation By Saravanan

This is a fully isolated, controlled lab environment. No real systems were targeted. All simulations performed on personal VMs for educational purposes only.

## About This Lab
This Mini SOC Home Lab was built from scratch to simulate real-world attack and defense scenarios. As someone transitioning from Food Technology into Cybersecurity with a focus on SOC Analysis, this lab documents my hands-on learning journey — from setting up an isolated network to running actual attack simulations and capturing the traffic as a SOC analyst would.

This lab proves that you don't need a corporate network or expensive equipment to build real cybersecurity skills. Just two VMs, VMware, and curiosity.

## Lab Environment
Component                                     Details
Hypervisor                         VMware Workstation Pro 25H2
Attacker                         Machine Kali Linux 2025.4 (amd64)
Defender / Target                         Windows 10 x64
Network Type                VMware LAN Segment — Isolated (testpractice)
Attacker IP                            192.168.20.11 (Static)
Target IP                              192.168.20.10 (Static)
Internet Access                      None — Fully Air-Gapped Lab

The isolated LAN segment means zero risk of traffic escaping to the real network. Static IPs ensure consistent, repeatable results across every lab session — exactly how enterprise security labs are configured.



