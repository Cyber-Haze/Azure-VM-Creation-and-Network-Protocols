<p align="center">
<img width="444" height="313" alt="Screenshot 2025-08-19 001224" src="https://github.com/user-attachments/assets/30895719-356b-419e-99e2-258e3d62f37a" />

</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we explore network traffic between Azure Virtual Machines using Wireshark while focusing on different protocols such as ICMP, SSH, DHCP, DNS, and RDP. We also experiment with Network Security Groups (NSGs), creating a firewall rule, to control inbound and outbound traffic. This allows us to gain insight into how network traffic flows between virtual machines and how security rules can be used to restrict or permit specific types of traffic. <br />


<h2>Guided Photos Included</h2>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools (Windows Powershell or CMD)
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Part 1: Create Ressources</h2>

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
  
- Create a Resource Group within your Azure Subscription to host the virtual machines. (Take note of region)
</p>
<br />

<p>
<img width="607" height="247" alt="Screenshot 2025-08-19 004516" src="https://github.com/user-attachments/assets/7e845bff-4487-47d7-beb1-835f0efbf24a" />
</p>
<p>

- Next we move to create a Virtual Machine and ensure we select the previously created resource group with its region. For this showcase we will call the VM "Win10".
- Ensure to Select the OS disk Image for Windows 10 22h2 with a minimum of 2vcpu & 8Gb of Memory.
- Set username and password (Take note of this, needed to log into VM)

<p> 
<img width="384" height="95" alt="Screenshot 2025-08-19 010242" src="https://github.com/user-attachments/assets/0705c7c0-e3c3-4a71-9036-59978b9a4b77" />

- Ensure you confirm this licensing prompt or else you won't be able to move forward.(only for windows Vm's)
</p>
<br />

<p>
<img width="605" height="319" alt="Screenshot 2025-08-19 010503" src="https://github.com/user-attachments/assets/58043d9f-f4b6-4d75-bab4-04e806157ed1" />
  <img width="656" height="432" alt="Screenshot 2025-08-19 011358" src="https://github.com/user-attachments/assets/c03002f4-9007-48aa-a370-14fefbf707f5" />

</p>
<p>
  
- In the "Networking" section of creating the VM, create a new virtual network with the CIDR Notation of 10.0.0.0/16 and a subnet of 10.0.0.0/24.
- Review and create the Windows 10 VM
- Repeat the VM creation steps however take note to create a Linux OS vm with Ubuntu Server 24.04 LTS. 
- Select the same resource group, region and select the newly created virtual network in the "Networking" section to ensure both virtual system are on the same network.
</p>
<br />

<h2>Part 2: Monitor ICMP Traffic [Internet Control Message Protocol]</h2>

<p>
<img width="401" height="289" alt="image" src="https://github.com/user-attachments/assets/fc5a2061-1f10-498b-ba0a-2a24494b0dfd" />
</p>
<p>

1. Copy the Windows 10 VM public IP
2. launch Remote Destop, Paste IP and Connect with username and password previously created
3. Download & Install Wireshark within the Windows 10 VM
</p>
<br />
<h2></h2>
<p>
  
- Open Wireshark and filter for ICMP Traffic (often used in tools like ping and traceroute to check network connectivity and diagnose issues.)
- Open Windows Powershell or CMD as administrator
- Back In Azure,identify Linux Ubuntu VM private IP address and perform a Ping command from the Windows 10 VM ( ping 
- Observe ping request & reply traffic via Wireshark between the two VM's
</p>
<p>
<img width="1266" height="450" alt="image" src="https://github.com/user-attachments/assets/e6fc875c-1847-4431-a45a-6dda31fd5235" />

</p>
<p>

Next lets test connectivity to public websites using ping
- From the Windows VM, run Windows Powershell and Ping google.com and youtube.com
- Observe ping request & reply traffic via Wireshark between the Windows 10 VM and these Sites.
</p>
<p>
<img width="1300" height="462" alt="image" src="https://github.com/user-attachments/assets/ca3c3645-fccc-4529-9385-7e3e1043e7fa" />

</p>
<br />

<h3> Configuring a Firewall [Network Security Group]</h3>


<p>
  
- Initiate a continuous ping from the Windows Vm to the Linux VM using [Ping 10.0.0.5 -t]
- From the Azure portal, access the Network Security Group (NSG) assigned to the Linux VM and deny inbound ICMP traffic
    - Ensure to select the ICMPv4 Protocol
    - Set action to "Deny"
</p>
<p>
<img width="1212" height="591" alt="Screenshot 2025-08-21 224606" src="https://github.com/user-attachments/assets/d3e90085-af49-44bb-ba5b-8d4edaadeb27" />
<img width="382" height="593" alt="Screenshot 2025-08-21 225359" src="https://github.com/user-attachments/assets/ebda37a2-cbe1-4040-bb6d-96607f821c6f" />
</p>

<p>
<img width="1288" height="460" alt="image" src="https://github.com/user-attachments/assets/df26899d-0c78-4f88-b9a8-c7f258a90421" />

</p>
<br />

<p>
  
- Notice how the ICMP traffic stops due to the new firewall rule
- Previously we would see "Request and Reply" traffic via Wireshark and Powershell. Now we are only seeing "Request" traffic. Due to the the new firewall rule the Linux VM has stopped receiving communication from the Windows VM therefore it cannot "reply".
<h2></h2>
<p>
  
- Remove the firewall rule to enable ICMP traffic flow once more.
- Observe the ICMP traffic working again in Wireshark and on the command line.
- Stop the continuous ping activity from the Windows 10 VM using [crtl+C].
</p>
<p>
<img width="1330" height="676" alt="image" src="https://github.com/user-attachments/assets/9b601d0d-ec76-45d1-9409-df865a9e332f" />

</p>
<br />

<h2> Part 3: Monitor SSH Traffic[Secure Shell]</h2>

<p>

  - In Wireshark, Filter for SSH traffic, SSH uses TCP port 22.
      - We can search "ssh" or "tcp.port==22".
  - From the Windows VM create a connection to the Linux Vm via Powershell.
      - type "ssh username@<private IP address>" eg. ssh labuser@10.0.0.5.
      - enter user password to login.
  - Observe the SSH traffic via Wireshark.
  - Notice in Wireshark that the username has changed and is now highlighted in green showing a successful access to the Linux VM.
  - type "exit" to close connection and observe "red" highlight in Wireshark confirming connection has been closed
</p> 
<br />
<p>
<img width="1366" height="572" alt="image" src="https://github.com/user-attachments/assets/99a4a64f-6f4b-49d2-a1eb-01f03460b9c6" />
</p>

<h2> Part 4: Monitor DHCP Traffic [Dynamic Host Comfiguration Protocol] </h2>

<p>

- In Wireshark, Filter for DHCP traffic, DHCP uses UDP port 67 & 68.
      - We can search "dhcp" or "udp.port==67||udp.port==68".
- Normally we could run the ipconfig /renew command to request a new IP , however that creates a connection issue within the VM environment. Heres the work-around.
    - Open Notepad as Admin
    - type the commands (each to there own line) ipconfig /release, ipconfig /renew
    - <img width="220" height="124" alt="image" src="https://github.com/user-attachments/assets/475a4e8d-22e7-45e5-95cb-72c4d1f4c711" />
    - save it as dhcp.bat file in the C:\ProgramData folder
- From Powershell, change directory to locate the ProgramData folder ( CD  c:\programdata)
- Type the command  "./dhcp.bat" to run the file commands
- Observe the DHCP traffic in Wireshark as the VM communicates with the DHCP server to release then renew its IP address.
</p>
<p>
<img width="1496" height="481" alt="image" src="https://github.com/user-attachments/assets/9aff1286-0780-4e71-9b10-06789f4d00dc" />

</p>

<h2> Part 5: Monitor DNS Traffic [Domain Name Server]</h2>

<p>

- In Wireshark, filter for DNS traffic
    - We can search for "dns", "udp.port==53" or "tcp.port==53"
- To identify DNS traffic we will use the "nslookup" command to gain the IP address of known websites.
- Observe the DNS traffic in Wireshark
- Observe the response providing the IP address in Powershell

- Google.com
<img width="1160" height="438" alt="image" src="https://github.com/user-attachments/assets/069d7d69-b9a0-4b99-9fc0-7d64417097b9" />

- Disney.com
<img width="1234" height="446" alt="image" src="https://github.com/user-attachments/assets/f5a51ff8-c143-4096-92b8-275d550c87e8" />
<br />

<h2> Part 6: Monitor RDP Traffic[Remote Desktop Protocol]</h2>

<p>
  
- In Wireshark, filter to capture RDP traffic
    -We can search using "tcp.port == 3389".
- Observe the continuous traffic movement in Wireshark. This is because the RDP records all foreground nd background processes.
  -  This constant stream is from RDP continuous transmition of data to keep the live remote session active regardless if the user is active or not.
    
<img width="943" height="461" alt="image" src="https://github.com/user-attachments/assets/5ba9bfff-2f13-42d8-980f-44c0738cb0c7" />

<br />

<h2> In Summary </h2>

<p>
In this lab, we walked through creating two Virtual Machines ( Windows and Linux) along with a Virtual Network, we explored different types of network traffic between two Azure Virtual Machines using Wireshark to analyze protocols such as ICMP, SSH, DHCP, DNS, and RDP. We also experimented with Network Security Groups [Firewall Rules] to control the flow of ICMP traffic and observed how security settings can affect network behavior. In completing these exercises we learnt how to filter for specific traffic from there respective TCP/UDP Ports, how network traffic flows between virtual machines in Azure, how network security controls can be implemented to manage this traffic effectively along with several terminal commands.
</p>



