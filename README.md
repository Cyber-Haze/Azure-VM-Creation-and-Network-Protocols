<p align="center">
<img width="444" height="313" alt="Screenshot 2025-08-19 001224" src="https://github.com/user-attachments/assets/30895719-356b-419e-99e2-258e3d62f37a" />

</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we explore network traffic between Azure Virtual Machines using Wireshark while focusing on different protocols such as ICMP, SSH, DHCP, DNS, and RDP. We also experiment with Network Security Groups (NSGs), creating a firewall rule, to control inbound and outbound traffic. This allows us to gain insight into how network traffic flows between virtual machines and how security rules can be used to restrict or permit specific types of traffic. <br />


<h2>Guided Photos Included</h2>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools (Windows Powershell, Terminal, CMD)
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Step 1: Create Ressources</h2>

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Create a Resource Group to host the virtual machines
</p>
<br />
