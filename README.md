# azure-network-protocols

So I can find this easier
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h1>Part 1: Set up Azure Resources</h1>

<h3>Step 1: Create a Resource Group and Virtual Network</h3>

- Log into Azure Portal and create a Resource group.

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Create a Virtual Network (VNet)

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Now create two virtual machines

- Windows 10 VM
  - Use the resource group and VNet created above.
  - Allow RDP (port 3389) during setup
  - Note the Private Ip address

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Ubuntu Linux VM
  - Same Resource Group and VNet as the Windows VM
  - Allow SSH (port 22)
  - Note the private IP address

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3>Step 2: Monitor Network Traffic with Wireshark</h3>

- Wireshark is a free and powerful tool used to analyze packets and protocols on a network. It helps you see what's happening behind the scenes.

  - Install Wireshark
  - Connect to the Windows 10 VM via Remote Desktop.
  - Download and install Wireshark. https://www.wireshark.org
  - Launch Wireshark and start capturing on the Ethernet adapter

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- ICMP Traffic (ping)

