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
<img src="https://i.imgur.com/FhAkz84.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/gwmYmH5.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/sTUk1cr.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3>Step 2: Creating two virtual machines </h3>

- Windows 10 VM
  - Use the resource group and VNet created above.
  - Allow RDP (port 3389) during setup
  - Note the Private Ip address

<h3>                    </h3>

<p>
<img src="https://i.imgur.com/KgVIPF9.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/tSaT9eO.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/wdvu1yh.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/tq0VIey.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3>Step 3: Creating the second Virutal Machine</h3>

- Ubuntu Linux VM
  - Same Resource Group and VNet as the Windows VM
  - Allow SSH (port 22)
  - Note the private IP address

<h3>                                      </h3>

<p>
<img src="https://i.imgur.com/IZVUB18.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/GVYXNV9.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/awZV6fm.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h2> Using Wireshark</h2>

<h3>Step 4: Monitor Network Traffic with Wireshark</h3>

- Wireshark is a free and powerful tool used to analyze packets and protocols on a network. It helps you see what's happening behind the scenes.

  - Connect to the Windows 10 VM via Remote Desktop.
  - Download and install Wireshark. https://www.wireshark.org
  - Just click through next until you reach install and then click install. Same for Npcap,
  - Launch Wireshark and start capturing on the Ethernet adapter

<h3>                                              </h3>

<p>
<img src="https://i.imgur.com/bIlZXin.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/5U5TUDS.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/iSWqYnb.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3> Step 5: ICMP Traffic part 1</h3>

- ICMP Traffic (ping)
ICMP is the protocol used when you ping another device.

- Filter ICMP in Wireshark
  - Open Wireshark and set the filter to show only ICMP traffic on the search bar.
- Ping Ubuntu VM
  - Find the private IP address of your Ubuntu VM from your Azure.
  - Open Powershell or Command Line on the Windows 10 VM
  - Ping the Private IP address from the Ubuntu VM and watch the traffic in Wireshark.

<h3>                          </h3>

<p>
<img src="https://i.imgur.com/QSYj2m0.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/rtk9YpS.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/er4UAR2.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3> Step 6: ICMP Traffic part 2</h3>

- Ping a Public Website
  - In the Windows 10 VM, use the command line or PowerShell to ping a public website. (e.g. - ping 10.0.0.5)
  - Observe the traffic in Wireshark.

<p>
<img src="https://i.imgur.com/5fcAfMd.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>


<h3> Step 7: ICMP Traffic part 3</h3>

- Continous Ping
  - Start a continuous ping from Windows 10 VM to Ubuntu VM.
  - Stop the ping with CTRL + C.

<p>
<img src="https://i.imgur.com/2EFchsV.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>


<h3>Step 8: Manage ICMP with NSG </h3>

  - Go to the Ubuntu VM > Networking > Network Settings

  - Add a new Inbound Rule:
    - Protocol: ICMPv4
    - Action: Deny
    - Priority: 290

  - Return to the Windows VM and try pinging again. It should fail.

  - Change the Network Settings rule to Allow ICMP and try again. It should succeed.

<p>
<img src="https://i.imgur.com/SQEzRPo.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/D9A8il3.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/p5snFPt.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/QxPkzMc.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3>Step 9: SSH Traffic </h3>

  - Filter for SSH in Wireshark
    - In Wireshark, set the filter to show only SSH traffic. (e.g. tcp.port == 22) on the search bar.

  - SSH into Ubuntu VM
    - From Windows 10 VM, use the Windows Terminal or Powershell and connect to the Ubuntu VM via SSH using its private IP. e.g. - ssh username@Private IP Address, you can find this in the connect panel.
    - You'll have to type yes and then type the password into it.
    - The Password won't show up as you type it so make sure you carefully type it 1 to 1.
    - Type commands in the SSH session and observe the traffic in Wireshark. Use this link for commands cheats sheet (for a studay purpose) https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet/

    - Exit the SSH Session.
      - Type exit and press enter to close the SSH connection.

<p>
<img src="https://i.imgur.com/CNZ1uF2.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/ND8p4wA.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/G8FLWmg.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/Yg5r6o0.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3>Step 10: DHCP Traffic </h3>

  - Filter for DHCP Traffic.
    - In Wireshark, filter to show only DHCP traffic on the search bar.

  - Renew IP Address
    - On Windows 10 VM, run ipconfig /renew to request a new IP address.
    - Observe the DHCP traffic in Wireshark.
    - Use this link for a cheat sheet on commands (with explanations) https://www.ninjaone.com/blog/ipconfig-commands/

<p>
<img src="https://i.imgur.com/QbUZErQ.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/YpysCvd.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3>Step 11: DNS Traffic </h3>

  - Filter for DNS Traffic
    - In Wireshark, filter to show only DNS traffic type "dns" on the search bar.

  - Use Nslookup
    - From the Windows 10 VM command line or Powershell, use nslookup to find IP addresses for google.com and disney.com
    - Observe the DNS traffic in Wireshark.
    - Use this link to learn more about the commands and use it for learning purposes: https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc725991(v=ws.11)

<p>
<img src="https://i.imgur.com/OeOExan.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/mIwzNGl.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3>Step 12: RDP Traffic </h3>

  - Filter for RDP Traffic
    - In Wireshark, set the filter to show RDP traffic (tcp.port == 3389) on the search bar.

  - Observe RDP Traffic
    - Note the constant stream of traffic. This happens because RDP continuously transmits a live stream between computers.

<p>
<img src="https://i.imgur.com/Hhuokmy.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/J5fvYIr.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h3> Step 13: Finishing with our tools</h3>

  - Once your finished with this lab, make sure to delete your Virtual Machines and resource group so you can save your funds. You can find my instructions on it in Ticket Lifecycles. (https://github.com/TylerJH-IT/ticket-lifecycle)
