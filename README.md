# Network Security Monitoring

## Overview

This project is expanding my previous <a href="https://github.com/Nick-Huettl/Active-Directory-Security/tree/main">Active Directory Security</a> lab to implement improved network security monitoring. The lab was also used to gain more hands-on experience with Intrusion Detection System (IDS) configuration and rule creation. Additionally, I wanted to gain more experience with Wireshark, as I know it is a valuable tool for network monitoring and packet inspection.

## Network Architecture Diagram



## Tools Used/Added

- Suricata (IDS)
- Wireshark (Packet Inspection)
  
## Objectives
- Deploy a network-based IDS within an existing AD lab environment
- Configure Suricata to monitor internal subnet traffic
- Create multiple custom IDS rules
- Generate simulated attack traffic
- Capture and analyze network packets using Wireshark
- Forward Suricata logs into Splunk

### Suricata VM

First, I created a new Ubuntu Server VM to host my Suricata Intrusion Detection System (IDS).

<img width="1324" height="844" alt="Screenshot 2026-03-23 124332" src="https://github.com/user-attachments/assets/e485bfec-9138-46c4-a25b-9c9373b9492a" />

<img width="1304" height="847" alt="Screenshot 2026-03-23 124813" src="https://github.com/user-attachments/assets/5b5f0ee4-5a73-4010-9f40-7dbd49853584" />

<img width="1281" height="828" alt="Screenshot 2026-03-23 125636" src="https://github.com/user-attachments/assets/738ef2ca-f661-4816-bca6-7ec380a816a9" />

After the initial system and Suricata installations were complete, I needed the IP address and network interface of the Suricata VM for configurations later.

<img width="1259" height="815" alt="Screenshot 2026-03-23 125946" src="https://github.com/user-attachments/assets/1b611465-4444-4563-8b41-780401411b4f" />

<img width="1285" height="834" alt="Screenshot 2026-03-23 130609" src="https://github.com/user-attachments/assets/3edd88b3-9a0d-46a2-9da2-8c3df932fe12" />

### Suricata File Configurations


















