# configure-ad
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>
<h2>Setup Resources in Azure</h2>

- Step 1 Create the Domain Controller VM (Windows Server 2022) named “DC-1”
          a Take note of the Resource Group and Virtual Network (Vnet) that get created at this time 
- Step 2 Set Domain Controller’s NIC Private IP address to be static
- Step 3 Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in Step 1.a
- Step 4 Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher)

<h2>Ensure Connectivity Between the Client (Client-1)and Domain Controller(DC-1)</h2>  

- Step 1 Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
- Step 2 Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
- Step 3 Check back at Client-1 to see the ping succeed
  
<h2>Install Active Directory</h2>

- Step 1 Login to DC-1 and install Active Directory Domain Services
- Step 2 Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
- Step 3 Restart and then log back into DC-1 as user: mydomain.com\user

<h2>Create an Admin and Normal User Account in AD</h2>

- Step 1 In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
- Step 2 Create a new OU named “_ADMINS”
- Step 3 Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
- Step 4 Add jane_admin to the “Domain Admins” Security Group
- Setp 5 Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
- Step 6 User jane_admin as your admin account from now on

  <h2>Join Client-1 to Your Domain (mydomain.com)</h2>

- Step 1 From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
- Step 2 From the Azure Portal, restart Client-1
- Step 3 Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
- Step 4 Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain

<h2>Setup Remote Desktop for Non-Administrative Users on Client-1</h2>

- Step 1 Log into Client-1 as mydomain.com\jane_admin and open System Properties
- Step 2 Click “Remote Desktop”
- Step 3 Allow “omain Users” access to Remote Desktop
- Step 4 You can now log into Client-1 as a normal, non-administrative user now

<h2>Create a Bunch of Additional Users and Attempt to Log into Client-1 with One of the Users</h2>

- Step 1 Login to DC-1 as jane_admin
- Step 2 Open PowerShell ISE as an administrator
- Step 3 Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
- Step 4 Run the script and observe the accounts being created
- Step 5 When finished, open ADUC and observe the accounts in the appropriate OU
- Step 6 Attempt to log into Client-1 with one of the accounts (take note of the password in the script)


<h2>Deployment and Configuration Steps</h2>

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
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
