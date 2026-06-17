<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h3>Step 1: Set up Azure Resources</h3>

- Log into Azure Portal and create a Resource group.

- Create a Resource Group and Virtual Network (VNet)

<p>
<img src="https://i.imgur.com/zmXNCuX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<p>
<img src="https://i.imgur.com/QAaveDe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Now create two virtual machines

- Windows 10 VM
  - Use the resource group and VNet created above.
  - Allow RDP (port 3389) during setup
  - Note the Private Ip address

<p>
<img src="https://i.imgur.com/1FbORxd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/Cz1WqcN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/6PAeuhD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/o7zbXQr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Ubuntu Linux VM
  - Same Resource Group and VNet as the Windows VM
  - Allow SSH (port 22)
  - Note the private IP address

<p>
<img src="https://i.imgur.com/4jjqIxH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/IWA6SA9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/O1CucJL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/bFlywz6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3>Step 2: Monitor Network Traffic with Wireshark</h3>

- Wireshark is a free and powerful tool used to analyze packets and protocols on a network. It helps you see what's happening behind the scenes.

  - Install Wireshark
  - Connect to the Windows 10 VM via Remote Desktop.
  - Download and install Wireshark. https://www.wireshark.org
  - Launch Wireshark and start capturing on the Ethernet adapter

<p>
<img src="https://i.imgur.com/WEDJlYV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/2yqkhIH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/A2SnIGA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- ICMP Traffic (ping)
ICMP is the protocol used when you ping another device.

- Filter ICMP in Wireshark
  - Open Wireshark and set the filter to show only ICMP traffic on the search bar.

<p>
<img src="https://i.imgur.com/2DrPGy6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Ping Ubuntu VM
  - Find the private IP address of your Ubuntu VM from your Azure.
  - Open Powershell or Command Line on the Windows 10 VM
  - Ping this Private IP address from the Windows 10 VM and watch the traffic in Wireshark.

<p>
<img src="https://i.imgur.com/0U37PwV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Ping a Public Website
  - In the Windows 10 VM, use the command line or PowerShell to ping a public website. (e.g. - ping 10.0.0.5)
  - Observe the traffic in Wireshark.

<p>
<img src="https://i.imgur.com/rJvbRAr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Continous Ping
  - Start a continuous ping from Windows 10 VM to Ubuntu VM.
  - Stop the ping with CTRL + C.

<p>
<img src="https://i.imgur.com/0HvLmDy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- Manage ICMP with NSG

  - Go to the Ubuntu VM > Networking > NSG

  - Add a new Inbound Rule:
    - Protocol: ICMPv4
    - Action: Deny
    - Priority: 290

  - Return to the Windows VM and try pinging again. It should fail.

  - Change the NSG rule to Allow ICMP and try again. It should succeed.

<p>
<img src="https://i.imgur.com/cpvNK3L.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/KQUcDMR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/3cN78El.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/zMU0ZJl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/Fi7b1AT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- SSH Traffic

  - Filter for SSH in Wireshark
    - In Wireshark, set the filter to show only SSH traffic. (e.g. tcp.port == 22) on the search bar.

  - SSH into Ubuntu VM
    - From Windows 10 VM, use the Windows Terminal or Powershell and connect to the Ubuntu VM via SSH using its private IP. (e.g. - ssh username@Private IP Address) You'll have to type yes and then the password into it.
    - The Password won't show up as you type it so make sure you carefully type it 1 to 1.
    - Type commands in the SSH session and observe the traffic in Wireshark. Use this link for commands cheats sheet (for a studay purpose) https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet/

    - Exit the SSH Session.
      - Type exit and press enter to close the SSH connection.

<p>
<img src="https://i.imgur.com/Se7QUW1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/0cbPJX6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- DHCP Traffic

  - Filter for DHCP Traffic.
    - In Wireshark, filter to show only DHCP traffic on the search bar.

  - Renew IP Address
    - On Windows 10 VM, run ipconfig /renew to request a new IP address.
    - Observe the DHCP traffic in Wireshark.
    - Use this link for a cheat sheet on commands (with explanations) https://www.ninjaone.com/blog/ipconfig-commands/

<p>
<img src="https://i.imgur.com/OKnDVF8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/LJtSFhI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- DNS Traffic

  - Filter for DNS Traffic
    - In Wireshark, filter to show only DNS traffic type "dns" on the search bar.

  - Use Nslookup
    - From the Windows 10 VM command line or Powershell, use nslookup to find IP addresses for google.com and disney.com
    - Observe the DNS traffic in Wireshark.
    - Use this link to learn more about the commands and use it for learning purposes: https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc725991(v=ws.11)

<p>
<img src="https://i.imgur.com/LhO0WM7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/9NZ0eXO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/db8T4tY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/eqJKMNq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

- RDP Traffic

  - Filter for RDP Traffic
    - In Wireshark, set the filter to show RDP traffic (tcp.port == 3389) on the search bar.

  - Observe RDP Traffic
    - Note the constant stream of traffic. This happens because RDP continuously transmits a live stream between computers.

<p>
<img src="https://i.imgur.com/LjmRu4Y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
