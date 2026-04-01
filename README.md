# Network Security Monitoring

## Overview

This project expands my previous <a href="https://github.com/Nick-Huettl/Active-Directory-Security/tree/main">Active Directory Security</a> lab by implementing network security monitoring capabilities. I deployed a network-based Intrusion Detection System (IDS) to monitor internal traffic, created custom detection rules, and analyzed generated network activity using Wireshark. The goal was to simulate real-world SOC workflows by detecting suspicious traffic, validating alerts, and analyzing packet-level data.

## Network Architecture Diagram



## Tools Used

- Ubuntu Server (IDS Host)
- Suricata (IDS)
- Wireshark (Packet Inspection)
- Nmap (Traffic Generation)
  
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

With Suricata now installed, I could start changing some configurations in the 'suricata.yaml' file. This was my first time making changes to this file, so I missed some configurations, causing the IDS not to work as intended. I only changed the $HOME_NET to the proper IP/subnet, which was not enough to properly detect events.

<img width="1288" height="265" alt="Screenshot 2026-04-01 142017" src="https://github.com/user-attachments/assets/9fe1ce08-1464-431a-b67b-086849679760" />

<img width="809" height="399" alt="Screenshot 2026-04-01 142053" src="https://github.com/user-attachments/assets/4002d984-8cc4-43af-8f09-747651887b68" />

### Other Configurations I Missed + Fixed

After changing $HOME_NET, I created a basic ICMP detection rule to see if the IDS was working as intended. I pinged the Suricata VM IP with the Windows 11 command prompt, packets were sent and received, but nothing was being detected in the 'fast.log' file.

#### Issue 1:
After troubleshooting, I found that I forgot to change the interface under "af-packet" to the proper network interface. The default interface for Suricata was 'eth0', but my VM interface was 'ens33' as previously shown in the screenshots above with the VM IP. 

#### Issue 2:
I also discovered that the "default-rule-path" was pointing to "/var/lib/suricata/rules", while my custom rules were stored in "/etc/suricata/rules". Updating this path and adding 'local.rules' under "rule-files" allowed Suricata to properly load custom detection rules.

<img width="751" height="382" alt="Screenshot 2026-03-30 150318" src="https://github.com/user-attachments/assets/b7f18f1b-8519-47ea-a101-3a8b08a94e3d" />

<img width="800" height="213" alt="Screenshot 2026-04-01 142157" src="https://github.com/user-attachments/assets/a089df1d-fcdf-4bcb-b1d5-f42b9b01af4f" />

<img width="745" height="261" alt="Screenshot 2026-04-01 143613" src="https://github.com/user-attachments/assets/28ab43da-4887-4d72-841e-8ba2f0810dde" />

<img width="1277" height="741" alt="Screenshot 2026-04-01 151200" src="https://github.com/user-attachments/assets/522cd298-fed1-44bd-b05b-e8bf8e62e0ab" />

<img width="1282" height="253" alt="Screenshot 2026-03-31 125519" src="https://github.com/user-attachments/assets/873c4e29-34b2-454f-96b5-ca507b72e27d" />

### Rules Created + Testing

Now that the IDS was catching detections, I could make some other basic rules to detect.

This included the ICMP detection, SYN scan detection, and DNS query monitoring.

After creating the rules, I generated test traffic from the Windows 11 client to validate the alerts.
- ICMP detection was triggered using the ping command
- SYN scan detection was triggered using an Nmap scan
- DNS detection was triggered using nslookup

<img width="1289" height="848" alt="Screenshot 2026-03-31 130119" src="https://github.com/user-attachments/assets/009566b3-a8ab-4f0d-bf7f-1f2acf898ef2" />

<img width="1026" height="741" alt="Screenshot 2026-03-31 131034" src="https://github.com/user-attachments/assets/737be5dc-2719-474c-8c74-d4b53c298416" />

<img width="1299" height="851" alt="Screenshot 2026-03-31 131102" src="https://github.com/user-attachments/assets/d781333c-c6c7-4a23-900e-88df59768a8c" />




