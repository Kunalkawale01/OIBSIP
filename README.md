# OIBSIP

### Task 1 :-

## Basic Network Scanning with Nmap

This repository contains practical Nmap commands and scan outputs performed on Kali Linux.  
It includes host discovery, open-port scanning, service/version detection, and explanations of each result.

---

## Tools Used
- Kali Linux
- Nmap 7.95

---
Important :- Bellow IP Is Just an Example

# 1. Host Discovery (Ping Scan)

```bash
nmap -sn 10.09.99.0/24
```

**Result:**
- Host is up → the device is active on the network.

---

# 2. Basic Port Scan (Top 1000 Ports)

```bash
nmap 10.09.99.255
```

**Open Ports Detected:**
```
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
5432/tcp open  postgresql
```
---

# 3. Service & Version Detection

```bash
nmap -sV 10.09.99.255
```

**Detected Services & Versions:**
```
80/tcp   open  http          Microsoft IIS httpd 10.0
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds  SMB File Sharing
5432/tcp open  postgresql    PostgreSQL DB 9.6.0 or later
```
---

# Explanation of Each Open Port

### **Port 80 – HTTP (Microsoft IIS 10.0)**
- Runs the web server.
- Target for web vulnerabilities.

### **Port 135 – MSRPC**
- Windows RPC service communication.
- Sensitive for Windows-based attacks.

### **Port 139 – NetBIOS**
- LAN file sharing.
- Can leak system information if unsecured.

### **Port 445 – SMB**
- Windows File Sharing.
- Historically vulnerable (EternalBlue, WannaCry).

### **Port 5432 – PostgreSQL**
- Database service.
- Should not be open externally without strict firewall rules.

---

# Scripts

### `discover_hosts.sh`
```bash
#!/bin/bash
nmap -sn 10.09.99.255
```

### `basic_scan.sh`
```bash
#!/bin/bash
nmap $1
```

### `full_scan.sh`
```bash
#!/bin/bash
nmap -p- $1
```

### `service_scan.sh`
```bash
#!/bin/bash
nmap -sV $1
```
---
---

### Nmap Scan Explanation

The Nmap scan was performed on the target machine 10.09.99.255 to identify active services and open ports. The results show the following:

1. Host is Up
    The target machine responded to network probes, confirming it is active and reachable on the network.

2. Open Ports and Services

  - 80/tcp – HTTP (Microsoft IIS Web Server)
      This port indicates that a web server is running on the machine. It is used to host websites. IIS 10.0 is identified, which is a Windows-based web server.

  - 135/tcp – MSRPC (Microsoft RPC Service)
      This service is used by Windows for remote communication between applications. It is commonly used for system management tasks.

  - 139/tcp – NetBIOS Session Service
      Used for older Windows file sharing and network communication. It allows systems to share files, printers, and system information inside a network.

  - 445/tcp – SMB (Microsoft Directory Services)
      This port runs modern Windows file sharing (SMB). It allows users to access shared folders, printers, and authentication services. SMB has had historical vulnerabilities, so it is important to monitor.

  - 5432/tcp – PostgreSQL Database Server
      This port indicates that a PostgreSQL database is running on the target machine. This service is commonly used to store and manage data.

 3. Overall Summary
     The scan results show that the target is a Windows-based system running a web server, RPC services, file sharing services, and a PostgreSQL database. These open ports reveal what services are available and help understand the system's network exposure.
    
---
### Screenshot

![Nmap scan  (1)](https://github.com/user-attachments/assets/20ec6b37-3d52-4250-8967-80657d88f085)
![Nmap scan  (2)](https://github.com/user-attachments/assets/bd9dff81-8fc4-4031-99d2-f3af47663e43)
![Nmap scan  (3)](https://github.com/user-attachments/assets/8d84b2ed-16ce-43b0-9f49-f12e3f9b60a7)
![Nmap scan  (4)](https://github.com/user-attachments/assets/0cc62225-d251-481a-ac19-d26e4c9e4c8f)
