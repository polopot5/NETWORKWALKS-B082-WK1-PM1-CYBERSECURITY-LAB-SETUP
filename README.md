# NETWORKWALKS-B082-WK1-PM1-CYBERSECURITY-LAB-SETUP
Developed an isolated cybersecurity lab using VirtualBox and Kali Linux to support ethical hacking and security testing. The environment features a NAT-based virtual network, static IP configuration, connectivity validation, and VM snapshots. It provides a safe platform for reconnaissance, vulnerability assessment, and hands-on learning. securely.!
Objectives

The main objectives of this project are to:

Install and configure VirtualBox.
Install/import Kali Linux as a virtual machine.
Create a private NAT Network for the cybersecurity lab.
Configure network connectivity for Kali Linux.
Assign a consistent IP address to the Kali VM.
Verify network connectivity and DNS resolution.
Take a clean VM snapshot for recovery.
Document the complete setup process.
Prepare the environment for future cybersecurity projects.
Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

Network reconnaissance
Port scanning
Vulnerability assessment
Packet analysis
Web security testing
Exploitation practice
Security-tool experimentation

Important: This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.

Lab Architecture

Lab architecture diagram

Additional target machines can be added to the same virtual network in future projects.

Lab Configuration
Component	Configuration
Host OS	Windows 10
Host RAM	8 GB
Processor	Intel Core i7
Hypervisor	VirtualBox 7.2
Security OS	Kali Linux 2026.2
Kali RAM	2048 MB
Virtual Network	NAT Network
Network Address	10.0.0.0/24
Kali IP Address	10.0.0.2/24
Default Gateway	10.0.0.1
DNS Server	8.8.8.8
Future VM Range	10.0.0.3–10.0.0.99
Lab Setup Procedure
Step 1. Install 7-Zip

7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a .7z archive.

Tool: 7-Zip

Step 2. Install VirtualBox

VirtualBox was installed as the hypervisor.

Step 3. Create the NAT Network

A dedicated NAT Network was created in VirtualBox.

Configuration:

text
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled

NAT Network settings in VirtualBox

A NAT Network was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

This will allow future attacker and target VMs to communicate within the lab.

Step 4. Import Kali Linux

The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM network adapter was configured as follows:

text
Adapter 1
Attached to: NAT Network
Network:     NatNetwork
Adapter Type: Intel PRO/1000 MT Desktop

The VM was allocated:

text
RAM: 2048 MB

Kali Linux VM in VirtualBox

A shared folder was also configured for transferring required files between the host operating system and the Kali VM.

Step 5. Configure the Kali Linux Network

The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:

text
IP Address: 10.0.0.2
Subnet Mask: 255.255.255.0
Gateway: 10.0.0.1
DNS: 8.8.8.8

A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.

Kali Linux network settings

Step 6. Create a Clean VM Snapshot

After completing the initial configuration, a VirtualBox snapshot was created.

Example snapshot name:

text
Clean Kali - Network Setup

The snapshot represents the clean baseline of the laboratory.

If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.

Lab Verification
Test	Command	Expected Result
Check IP address	ip a	Correct Kali IP displayed
Test gateway	ping 10.0.0.1	Successful replies
Test Internet connectivity	ping 8.8.8.8	Successful replies
Test DNS resolution	nslookup networkwalks.com	Domain resolves
Verify Nmap	nmap --version	Nmap version displayed
Verify snapshot	Restore snapshot and run ip a	Baseline configuration restored
Example Results
text
IP Address:
10.0.0.2/24

Gateway:
10.0.0.1

DNS:
8.8.8.8
Problems Encountered & Solutions

Documenting problems is an important part of the project.

Problem 1. Internet Connectivity After Static IP Configuration

After manually configuring the IPv4 settings, Internet connectivity may fail depending on the Kali/NetworkManager configuration.

One workaround used during this lab was:

bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0

The network connection was then restarted/rebooted and connectivity was tested again.

Important: Network interface and connection names may differ between systems. Students should first identify their actual connection name before running an nmcli command.

Problem 2. VirtualBox VT-x / Virtualization Error

The VM initially failed to start because hardware virtualization was disabled in the system firmware/BIOS.

The issue was resolved by:

Restarting the computer.
Entering BIOS/UEFI settings.
Enabling Intel VT-x / hardware virtualization.
Saving the configuration.
Restarting the computer.
Starting the Kali VM again.

After enabling virtualization, the VM started successfully.

What I Learned

Through this project, I learned how to create and configure a virtual environment for cybersecurity practice.

The most important concepts I learned include:

1. NAT vs NAT Network

A standard NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple VMs connected to the same virtual network to communicate with one another while providing network address translation for external connectivity.

This makes it useful for building a multi-machine cybersecurity laboratory.

2. Virtual Machine Networking

I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network configu
