# network-walks-B084A-week1-cybersecurity-labsetup
🔐 My Cybersecurity Lab
Building an isolated virtual lab for penetration testing and ethical hacking practice

## Project Overview
This project helps me learn practical cybersecurity skill.

I am building my own cybersecurity laboratory using VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.
## 📌**Objectives**

The main objectives of this project are to:
- Install and setup virtual box
- Install/import kali Linux as a virtual machine.
- Create a private **Nat Network**
- Setup network connectivity for Kali Linux
- Assign a consistent IP address to the kali VM
- Take VM snapshot for recovery
- Prepare the environment for future cybersecurity project.
  
  ## 🪡**Purpose of the lab**
  The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation
  
⚠️ Important: This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.
  Lab Architecture
  🧑‍💻**Lab Architecture**
  <img width="720" height="366" alt="Screenshot_20261030-142430_1" src="https://github.com/user-attachments/assets/1c9fb5f8-f226-4e2a-955f-7be89a8746d4" />

## ⚙️ Lab Configuration

| Component | Configuration |
|:---|:---|
| 💻 Host OS | Windows 11 |
| 🧠 Host RAM | 4 GB |
| ⚡ Hypervisor | VirtualBox 7.2 |
| 🐉 Security OS | Kali Linux |
| 🧠 Kali RAM | 2048 MB |
| 🌐 Virtual Network | NAT Network |
| 🔐 Lab Purpose | Cybersecurity Learning |
| 🎯 Main Focus | Linux & Ethical Hacking |
| 📡Network Address | 10.0.0.0/24 |
| 🐧Kali IP Address | 10.0.0.2/24 |
| 🚪Default Gateway |  10.0.0.1 |
| 🌍DNS Server | 8.8.8.8 |

🪜 **Lab Setup Procedure**

**Step 1. Install 7-Zip**
7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a .7z archive.

**Tool:** 7-Zip

**Step 2. Install VirtualBox**

VirtualBox was installed as the hypervisor.

**Step 3. Create the NAT Network**

A dedicated NAT Network was created in VirtualBox.

Configuration: Network Name: Nat Network IPv4 Prefix: 10.0.2.0/24 DHCP: Enabled IPv6: Disabled
<img width="1336" height="769" alt="Screenshot 2026-10-28 060330" src="https://github.com/user-attachments/assets/8d253638-9523-48f8-8a58-49c5a775f1ee" />

A **NAT Network **was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

This will allow future attacker and target VMs to communicate within the lab.
**Step 4. Import Kali Linux**

The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM network adapter was configured as follows:
Adapter 1
Attached to: NAT Network 
Network: Natnetwork
Adapter Type: Intel Pro/1000 MT Desktop

**The VM was allocated**
RAM: 2048 MB
<img width="1299" height="680" alt="Screenshot 2026-10-28 062439" src="https://github.com/user-attachments/assets/5cf0b9e8-d8c2-4e78-b639-aa9add7e3c5e" />
A shared folder was also configured for transferring required files between the host operating system and the Kali VM.

## **Step 5. Configure the Kali Linux Network**

The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:

IP Address: 10.0.0.2
Subnet Mask: 255.255.255.0
Gateway: 10.0.0.1
DNS: 8.8.8.8
A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.
<img width="1362" height="717" alt="Screenshot 2026-10-28 062506" src="https://github.com/user-attachments/assets/f9a26089-8791-4526-9bda-6407932ebba2" />
## Step 6. Create a Clean VM Snapshot
After completing the initial configuration, a VirtualBox snapshot was created.

Example snapshot name:

Clean Kali - Network Setup
The snapshot represents the clean baseline of the laboratory.

If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.
## 🔎 Lab Verification
| ✅ Test |	🧾 Command	| 🎯 Expected Result |
|:---|:---|:---|
| 🌐 Check IP address	| ip a	| Correct Kali IP displayed |
| 📡 Test gateway	 | ping 10.2.0.0.1	| Successful replies |
| 🌍 Test Internet connectivity	| ping 8.8.8.8	| Successful replies |
| 🔎 Test DNS resolution |	nslookup networkwalks.com	| Domain resolves |
| 🧰 Verify Nmap |	nmap --version	| Nmap version displayed |
| 🔄 Verify snapshot |	Restore snapshot and run ip a |	Baseline configuration restored |
Example Results
IP Address:
10.0.0.2/24

Gateway:
10.0.0.1

DNS:
8.8.8.8
## 🐞 Problems Encountered & Solutions
Documenting problems is an important part of the project.

**Problem 1. Internet Connectivity After Static IP Configuration**
After manually configuring the IPv4 settings, Internet connectivity may fail depending on the Kali/NetworkManager configuration.

One workaround used during this lab was:

sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
The network connection was then restarted/rebooted and connectivity was tested again.

Important: Network interface and connection names may differ between systems. Students should first identify their actual connection name before running an nmcli command.

## Problem 2. VirtualBox VT-x / Virtualization Error
The VM initially failed to start because hardware virtualization was disabled in the system firmware/BIOS.

The issue was resolved by:

1. Restarting the computer.
2. Entering BIOS/UEFI settings.
3. Enabling Intel VT-x / hardware virtualization.
4. Saving the configuration.
5. Restarting the computer.
6. Starting the Kali VM again.
After enabling virtualization, the VM started successfully.

## 💡 What I Learned
Through this project, I learned how to create and configure a virtual environment for cybersecurity practice.

The most important concepts I learned include:

## 1. NAT vs NAT Network
A standard NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple VMs connected to the same virtual network to communicate with one another while providing network address translation for external connectivity.

This makes it useful for building a multi-machine cybersecurity laboratory.

## 2. Virtual Machine Networking
I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network configuration affects communication between machines.

## 3. Static IP Configuration
I learned how to configure and verify IPv4 addressing, subnet masks, gateways, and DNS settings in Kali Linux.

## 4. VM Snapshots
I learned that a clean snapshot should be created before performing risky or experimental activities.

This provides a known-good recovery point for future cybersecurity exercises.

## 5. Documentation
I learned that documenting commands, configuration, screenshots, problems, and solutions is an important part of a professional cybersecurity project.

## 🔐 Security & Ethical Use
This laboratory is intended strictly for education purposes only.

## Tools
. 7-Zip:
. VirtualBox:
. Kali Linux:


## Learning Objectives

- Learn Linux commands.
- Understand computer networking.
- Learn cybersecurity fundamentals.
- Practice ethical hacking safely.

## Author
Abubakar Auwal Isah
Cybersecurity Student
www.linkedin.com/in/abubakar-auwal-isah-5a0483443
## 📌 Project Information
Program Name: Cybersecurity at Networkwalks | Week: 01 | Project: Cybersecurity & Pentesting Lab Setup | Repository: GitHub
