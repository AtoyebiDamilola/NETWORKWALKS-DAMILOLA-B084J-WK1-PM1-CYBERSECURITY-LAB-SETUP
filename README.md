# Cybersecurity Lab Environment Setup

### Networkwalks Cybersecurity Internship | Week 1 | Project WK1-PM1

## 1. Project Overview

This project involved setting up a cybersecurity testing lab environment on a Windows laptop using Oracle VirtualBox and Kali Linux.

The objective was to create a virtualised environment that could serve as a controlled space for cybersecurity testing and ethical hacking practice.

The lab was configured using a custom NAT Network with the IPv4 subnet 10.0.0.0/24, while Kali Linux was configured as the attacking machine with a static IP address of 10.0.0.2/24.

This documentation presents the implementation process, network configuration, verification procedures, challenges encountered, and the solutions applied.

## 2. Project Objectives

The objectives of this project were to:

- Install and configure Oracle VirtualBox.
- Set up Kali Linux as the attacking machine.
- Create a custom NAT Network using the 10.0.0.0/24 subnet.
- Configure Kali Linux with the required static IP address.
- Enable bidirectional shared clipboard and drag-and-drop.
- Configure a shared folder between the Windows host and Kali Linux.
- Verify internet connectivity from the Kali Linux virtual machine.
- Take a virtual machine snapshot to preserve the completed configuration.

## 3. Tools and Technologies

The following tools and technologies were used:

| Tool | Purpose |
|---|---|
| Oracle VirtualBox 7.2.8 | Virtualisation platform |
| Kali Linux 2026.1 | Cybersecurity testing machine |
| Windows | Host operating system |
| NetworkManager (nmcli) | Network configuration |
| Terminal | Executing configuration and verification commands |

## 4. Lab Network Configuration

The lab environment was configured with the following network settings:

| Component | Configuration |
|---|---|
| Network type | NAT Network |
| Network name | NatNetwork |
| IPv4 subnet | 10.0.0.0/24 |
| Kali Linux IP | 10.0.0.2/24 |
| Default gateway | 10.0.0.1 |
| DNS server | 8.8.8.8 |
| DHCP | Enabled on NAT Network |

The Kali Linux virtual machine was connected to the custom NAT Network to provide network connectivity within the virtualised lab environment.
## 5. Implementation Steps

### Step 1: Confirm VirtualBox Installation

Oracle VirtualBox 7.2.8 was installed on the Windows host. The installed version was verified through Help > About VirtualBox.

### Step 2: Create the NAT Network

A custom NAT Network named `NatNetwork` was created through File > Tools > Network > NAT Networks.

The default IPv4 prefix was changed from `10.0.2.0/24` to `10.0.0.0/24`, while DHCP was left enabled.

### Step 3: Attach Kali Linux to the NAT Network

The Kali Linux virtual machine was configured to use the newly created `NatNetwork`.

Under Network > Adapter 1:
- Attached to: NAT Network
- Name: NatNetwork
- Promiscuous Mode: Allow All

### Step 4: Enable Shared Clipboard and Drag-and-Drop

Under General > Features, both Shared Clipboard and Drag-and-Drop were configured as Bidirectional.

### Step 5: Configure the Shared Folder

The Windows Downloads folder was added to the VirtualBox Shared Folders settings.

The following options were enabled:
- Access: Full
- Auto Mount: Yes

### Step 6: Configure a Static IP Address

NetworkManager (`nmcli`) was used to configure Kali Linux with the required static IP address, default gateway and DNS server.

The configured address was `10.0.0.2/24`.

### Step 7: Verify Internet Connectivity

Connectivity was tested by pinging the default gateway, Google's public DNS server and a domain name.

Both network connectivity and DNS resolution were verified.

### Step 8: Verify the Shared Folder

The shared Downloads folder was confirmed to be accessible inside Kali Linux through the `sf_Downloads` directory.

The folder contents were visible in the Thunar file manager.

### Step 9: Create a Virtual Machine Snapshot

After confirming that the lab was functioning correctly, a snapshot named `Lab setup complete 10.0.0.2` was created.

This provides a restore point for the configured environment.

## 6. Commands Used

### Static IP Configuration

The following commands were executed in the Kali Linux terminal:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.method manual \
ipv4.addresses 10.0.0.2/24 ipv4.gateway 10.0.0.1 \
ipv4.dns 8.8.8.8 ipv4.dad-timeout 0

sudo nmcli connection down "Wired connection 1"

sudo nmcli connection up "Wired connection 1"
### Network Verification

The following commands were used to verify network connectivity and DNS resolution:

```bash
ip a
ping -c 3 10.0.0.1
ping -c 3 8.8.8.8
ping -c 3 google.com

```
cmd"C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" modifyvm ^
"kali-linux-2026.1-virtualbox-amd64" --nicpromisc1 allow-all
## 7. Issues Encountered and Troubleshooting

During the lab setup, I encountered a few configuration challenges that required troubleshooting.

### Issue 1: NAT Network Settings Were Greyed Out

While configuring the NAT Network in VirtualBox, I noticed that some of the network settings were greyed out and could not be edited.

**Resolution:** I discovered that I needed to create and select a NAT Network entry first. Once I did this, the configuration fields became accessible.

### Issue 2: Apply Button Was Disabled

After accessing the NAT Network settings, the Apply button remained inactive.

**Resolution:** I changed the default IPv4 prefix to `10.0.0.0/24`. This activated the Apply button and allowed me to save the configuration.

### Issue 3: Network Adapter Reverted to NAT

While configuring the Kali Linux virtual machine, I noticed that the network adapter had reverted to the default NAT option instead of the custom NAT Network.

**Resolution:** I powered off the virtual machine, changed the adapter back to NAT Network, selected `NatNetwork`, and saved the settings.

### Issue 4: Internet Connectivity Challenge

I experienced a network connectivity issue while configuring Kali Linux with a static IP address.

**Resolution:** I used NetworkManager to set `ipv4.dad-timeout` to `0` and restarted the network connection. After applying these changes, internet connectivity worked successfully.
  
## 8. Conclusion

The Week 1 project was successfully completed by setting up a cybersecurity testing lab using Oracle VirtualBox and Kali Linux.

I configured a custom NAT Network using the `10.0.0.0/24` subnet, assigned Kali Linux a static IP address of `10.0.0.2/24`, enabled bidirectional clipboard and drag-and-drop functionality, and configured a shared folder between the Windows host and Kali Linux.

I also verified network connectivity and DNS resolution and created a virtual machine snapshot to preserve the completed configuration.

Although I encountered some challenges during the setup, troubleshooting them helped me strengthen my understanding of virtual networking, Linux network configuration, and the importance of verifying system settings.

  
