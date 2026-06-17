---
title: pfSense Install and VM Configuration
date: 2026-03-28 12:00:00 
categories: [Virtualization,Security]
tags: [VMware,pfSense,Firewalls]
---


## Objectives

 Set up pfSense as a virtual machine in VMware Workstation to act as a firewall between the internet and my virtual machines. This will improve the security of my VMs by serving as the foundation to configure firewall rules, control communication, segment the virtual network, monitor traffic, and enable VPN capabilities.

### Tools and Technologies Used

| Tool/Technology     | Purpose |
| ----------- | ----------- |
| VMware    | Hypervisor for all VMs    |
| Pfense | Firewall for all VMs       |
| Ubuntu | Linux VM for all LInux labs|
| Windows | Windows VM for all Windows labs|

## Procedure
### VM Environment Setup
1.	Downloaded the pfSense ISO from Netgate and extracted it using 7-Zip.
2.	Opened VMware and selected New VM.
3.	VMware automatically recognized pfSense as FreeBSD and prompted for resource allocation.
4.	Assigned 5.3 GB RAM, 2 processors, and 30 GB disk space to the VM, then completed the setup wizard.
5.	Added a second network adapter in the pfSense VM settings: one adapter facing the internet, and the other connected to an internal network.
6.	Configured the first network adapter as NAT to share the host’s IP address. Configured the second adapter as Custom using VMnet2, which will be the internal network shared among all VMs.
7.	Configured all existing VMs to use VMnet2 as their network.
8.	Started the pfSense VM.

### pfSense VM Setup
1.	Accepted the license agreement on the initial screen.

2.	Selected Install from the welcome menu to start installation.


3.	Since this is an online installer, it required network configuration.

4.	Selected the WAN interface by matching the MAC address of the network 
adapter facing the internet. To find the MAC address, hovered over VM > Settings > Network Adapter > Advanced in VMware.


5.	Assigned the WAN interface to the matching MAC address.

6.	Left WAN network configuration at default.

7.	Confirmed network configuration and proceeded with installation.

8.	Selected the LAN interface similarly by identifying the corresponding MAC address.

9.	Left LAN network settings at default and confirmed interface assignments.

10.	Opted for the community edition of pfSense when prompted about subscription status.

11.	Chose ZFS as the file system (more resilient to power loss), and GPT as the partition scheme.


12.	Confirmed the disk would be wiped for installation.

13.	Installed the latest stable version and rebooted the VM.

## Modifications to LAN IP Address on pfSense
1.	Opened VMware Virtual Network Editor to check the LAN subnet for VMnet2.
2.	Within pfSense, changed the LAN IP address to fit the subnet noted in VMware.

### New IP Address for Windows VM (DHCP)
1.	Opened Command Prompt in the Windows VM.
2.	Checked current IP  `ipconfig`
3.	Released IP address using `ipconfig /release`.
4.	Renewed IP address using `ipconfig /renew`.
5.  Verify the newIP adress using `ipconfig`

### New IP Address for Linux VM (DHCP)
1.	Checked IP and interface name with ip addr.
2.	Released IP with `sudo dhclient -r <interface_name>`.
3.	Requested a new IP with `sudo dhclient <interface_name>`.
4.	Verified new IP with `ip addr`.

## Results

Successfully configured VMware virtual machines, installed and configured pfSense, and released/renewed IP addresses on both Linux and Windows VMs.


