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

- Ensure you confirm this licensing prompt or else you won't be able to move forward.
</p>
<br />

<p>
<img width="605" height="319" alt="Screenshot 2025-08-19 010503" src="https://github.com/user-attachments/assets/58043d9f-f4b6-4d75-bab4-04e806157ed1" />
  <img width="656" height="432" alt="Screenshot 2025-08-19 011358" src="https://github.com/user-attachments/assets/c03002f4-9007-48aa-a370-14fefbf707f5" />

</p>
<p>
In the Networking section of creating the VM, create a new virtual network with the CIDR Notations of 10.0.0.0/16 and a sb
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="574" height="250" alt="Screenshot 2025-08-19 003504" src="https://github.com/user-attachments/assets/2f0f104c-6d54-4edb-a1f6-282b9c43b8b5" />
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
