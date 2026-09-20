🔐 Virtual Cybersecurity Lab – Kali Linux & Metasploitable 2

A hands-on cybersecurity laboratory environment built using **Oracle VirtualBox**, **Kali Linux**, and **Metasploitable 2**.

This project demonstrates how to create an isolated penetration-testing environment, perform network reconnaissance using Nmap, identify vulnerable services, and conduct controlled security testing using the Metasploit Framework.
⚠️ **Disclaimer:** This project is intended strictly for educational purposes and authorized security testing. Metasploitable 2 is intentionally vulnerable and should only be used inside an isolated laboratory environment. Do not expose the vulnerable VM directly to the public Internet or test systems without authorization.

📌 Table of Contents

* [Project Overview](#-project-overview)
* [Objectives](#-objectives)
* [Lab Architecture](#-lab-architecture)
* [Technologies and Tools](#-technologies-and-tools)
* [Prerequisites](#-prerequisites)
* [Installation](#-installation)
* [Virtual Network Configuration](#-virtual-network-configuration)
* [Verify Connectivity](#-verify-connectivity)
* [Nmap Scanning](#-nmap-scanning)
* [Metasploit Testing](#-metasploit-testing)
* [Screenshots](#-screenshots)
* [Results](#-results)
* [Security Observations](#-security-observations)
* [Conclusion](#-conclusion)
* [Future Improvements](#-future-improvements)
* [Disclaimer](#-disclaimer)



🧪 Project Overview

The purpose of this project is to build a controlled cybersecurity environment consisting of two virtual machines:

| Machine  | Role                            | Operating System |
| -------- | ------------------------------- | ---------------- |
| Attacker | Security testing                | Kali Linux       |
| Victim   | Intentionally vulnerable target | Metasploitable 2 |

The virtual machines communicate through an **isolated VirtualBox network**.

The environment can be used to practice:

* Network reconnaissance
* Port scanning
* Service enumeration
* Vulnerability identification
* Controlled exploitation
* Security analysis
* Incident investigation
* Penetration-testing methodology

---

# 🎯 Objectives

The main objectives of this project are:

1. Create an isolated cybersecurity laboratory using VirtualBox.
2. Configure Kali Linux as the attacker machine.
3. Configure Metasploitable 2 as the intentionally vulnerable target.
4. Establish communication between both virtual machines.
5. Identify the target IP address.
6. Perform network reconnaissance using Nmap.
7. Enumerate exposed services.
8. Identify potential vulnerabilities.
9. Perform controlled penetration-testing exercises using Metasploit.
10. Document the findings and security observations.

---

# 🏗️ Lab Architecture

The basic laboratory architecture is:


                 HOST COMPUTER
                       │
                 Oracle VirtualBox
                       │
             Isolated Virtual Network
                       │
          ┌────────────┴────────────┐
          │                         │
          ▼                         ▼
   ┌──────────────┐          ┌──────────────────┐
   │  Kali Linux  │          │  Metasploitable 2│
   │              │          │                  │
   │   ATTACKER   │ ───────► │     VICTIM       │
   │              │          │ Vulnerable VM    │
   └──────────────┘          └──────────────────┘


Example IP configuration:

Kali Linux:
192.168.56.10

Metasploitable 2:
192.168.56.20

Network:
192.168.56.0/24


> The IP addresses above are examples. Use the actual addresses assigned to your virtual machines.


 🛠️ Technologies and Tools

Virtualization

* Oracle VirtualBox

Operating Systems

* Kali Linux
* Metasploitable 2

Security Tools

* Nmap
* Metasploit Framework
* Netcat
* Wireshark

Documentation

* Markdown
* Git
* GitHub

---

💻 Prerequisites

Before creating the laboratory, make sure you have:

* A computer with sufficient RAM and storage
* Oracle VirtualBox
* Kali Linux ISO or virtual machine image
* Metasploitable 2
* Basic Linux command-line knowledge
* Basic networking knowledge
* Git and a GitHub account

Recommended resources:

text
RAM:
8 GB or more

Storage:
30 GB+ free space

Virtualization:
Intel VT-x / AMD-V enabled

📥 Installation

 1. Install VirtualBox

Install Oracle VirtualBox on the host computer.

After installation, open VirtualBox.

---

2. Create Kali Linux VM

Create or import a Kali Linux virtual machine.

Recommended configuration:

Operating System: Kali Linux
CPU: 2+ cores
RAM: 2–4 GB
Storage: 20 GB+
Network Adapter: Host-Only Adapter


Start the Kali Linux VM and log in.

---

3. Import Metasploitable 2

Download and import the Metasploitable 2 virtual machine into VirtualBox.

Example configuration:

Operating System: Linux
RAM: 512 MB – 1 GB
Network Adapter: Host-Only Adapter


Metasploitable 2 is intentionally vulnerable and should remain inside the isolated lab network.
 🌐 Virtual Network Configuration

For a safe laboratory environment, configure both machines so that they communicate through an isolated virtual network.

In VirtualBox:

Settings
   ↓
Network
   ↓
Adapter 1
   ↓
Enable Network Adapter
   ↓
Attached to: Host-Only Adapter

Configure the same network type for both machines.

Example:

Kali Linux
    │
    │
    ├── Host-Only Network
    │
    │
Metasploitable 2


Avoid placing the intentionally vulnerable Metasploitable 2 machine directly on a network where it can be accessed by untrusted systems.

🔎 Determine IP Addresses

 Kali Linux

Open a terminal:


ip addr


or:

ifconfig


Identify the IP address assigned to the laboratory network interface.

Example:


192.168.56.10


## Metasploitable 2

Log into the Metasploitable machine and run:


ifconfig


Example:


192.168.56.20


Record the target IP address.



# 🔗 Verify Connectivity

From Kali Linux, test connectivity to Metasploitable 2:


ping -c 4 192.168.56.20


Expected result:


64 bytes from 192.168.56.20
64 bytes from 192.168.56.20
64 bytes from 192.168.56.20
64 bytes from 192.168.56.20


If the machines can communicate successfully, the laboratory network is working.



# 🔍 Nmap Scanning

Nmap is used to discover hosts, ports, and services in the authorized laboratory network.

## 1. Host Discovery

To identify active hosts on the lab network:


nmap -sn 192.168.56.0/24


Example:


Nmap scan report for 192.168.56.10
Host is up.

Nmap scan report for 192.168.56.20
Host is up.

## 2. Basic Port Scan

Scan the Metasploitable 2 machine:


nmap 192.168.56.20


This identifies commonly accessible TCP ports.



## 3. Service Enumeration

To identify service versions:


nmap -sV 192.168.56.20


This can provide information such as:


PORT      STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
23/tcp    open  telnet
80/tcp    open  http

The exact results depend on the configuration of the target VM.


## 4. Operating System Detection

You can also perform OS detection:


sudo nmap -O 192.168.56.20



## 5. Detailed Enumeration

For authorized testing of the laboratory target:


sudo nmap -sC -sV 192.168.56.20


This combines default NSE scripts with service-version detection.

---

# 💥 Metasploit Testing

The Metasploit Framework can be used to perform controlled security testing against the intentionally vulnerable Metasploitable 2 machine.

Start Metasploit:


msfconsole


Check available modules:


search type:exploit


You can search for modules associated with a specific service:


search ftp


or:


search ssh


---

## Example Testing Workflow

A typical controlled workflow is:


Reconnaissance
      ↓
Port Scanning
      ↓
Service Enumeration
      ↓
Vulnerability Identification
      ↓
Module Selection
      ↓
Controlled Testing
      ↓
Result Analysis
      ↓
Documentation


Before using any Metasploit module, verify that:

* The target is your Metasploitable 2 VM.
* The IP address is correct.
* The test is being performed inside the isolated laboratory.
* You understand what the selected module does.

---

 📊 Example Enumeration Workflow


# Identify the target
nmap -sn 192.168.56.0/24

# Scan ports
nmap 192.168.56.20

# Identify services and versions
nmap -sV 192.168.56.20

# Run default NSE scripts
sudo nmap -sC -sV 192.168.56.20


The information collected during enumeration can then be compared against known vulnerabilities and appropriate Metasploit modules.



# 🖥️ Screenshots

Screenshots documenting the laboratory are stored in the `screenshots/` directory.

## VirtualBox Configuration

Shows the Kali Linux and Metasploitable 2 virtual machines configured in VirtualBox.



## Kali Linux

Shows the Kali Linux security-testing environment.



## Metasploitable 2

Shows the Metasploitable 2 vulnerable target machine.



## Network Configuration

Shows the network configuration used for communication between the virtual machines.



## Nmap Scan

Shows the results of network and service enumeration against the laboratory target.



## Metasploit

Shows controlled Metasploit testing performed against Metasploitable 2.



# 📋 Results

The laboratory successfully demonstrated the following:

| Activity                       | Result      |
| ------------------------------ | ----------- |
| Kali Linux installation        | ✅ Completed |
| Metasploitable 2 installation  | ✅ Completed |
| VirtualBox configuration       | ✅ Completed |
| Isolated network configuration | ✅ Completed |
| Connectivity testing           | ✅ Completed |
| Host discovery                 | ✅ Completed |
| Port scanning                  | ✅ Completed |
| Service enumeration            | ✅ Completed |
| Vulnerability assessment       | ✅ Completed |
| Controlled Metasploit testing  | ✅ Completed |



# 🔐 Security Observations

The laboratory demonstrates several important cybersecurity concepts.

### 1. Exposed Services

A vulnerable system may expose multiple network services that increase its attack surface.

### 2. Service Enumeration

Service-version detection can provide information that helps security professionals identify potentially vulnerable software.

### 3. Vulnerability Management

Known vulnerable services should be identified, assessed, patched, disabled, or isolated where appropriate.

### 4. Network Isolation

Intentionally vulnerable systems should be isolated from production and untrusted networks.

### 5. Defense in Depth

Security should not depend on a single protection mechanism. Network segmentation, patch management, authentication, monitoring, firewalls, and intrusion detection can work together to reduce risk.

---


# 📚 Learning Outcomes

Through this project, the following cybersecurity concepts were practiced:

* Virtual laboratory setup
* Linux administration
* Networking fundamentals
* TCP/IP
* Port scanning
* Service enumeration
* Vulnerability assessment
* Penetration-testing methodology
* Metasploit Framework
* Security documentation
* Network isolation
* Ethical hacking principles

---

# 🏁 Conclusion

This project demonstrates the creation of a controlled cybersecurity laboratory using Kali Linux and Metasploitable 2 in Oracle VirtualBox.

The environment provides a safe platform for learning reconnaissance, enumeration, vulnerability assessment, and controlled penetration-testing techniques.

The project also highlights the importance of network isolation when working with intentionally vulnerable systems.

This laboratory can be extended with additional security tools, monitoring systems, vulnerability assessments, and defensive security exercises.

---

# ⚠️ Disclaimer

This project is intended for **educational purposes and authorized security testing only**.

Kali Linux and Metasploit are powerful security-testing tools, while Metasploitable 2 is intentionally vulnerable. All testing documented in this repository should be performed only against systems that you own or have explicit permission to test.

Never use these techniques against unauthorized systems, networks, websites, or devices.

---

## 👨‍💻 Author

Akashgowda T R

Cybersecurity Student

---

⭐ If this project helped you understand cybersecurity laboratory setup and penetration testing, consider giving the repository a star.

