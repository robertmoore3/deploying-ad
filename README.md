<p align="center">
<img src="https://github.com/user-attachments/assets/2a666083-7f44-48eb-ab51-728daafd40dd" />
</p>

<h1>Deploying Active Directory</h1>
This tutorial outlines how to set up Active Directory, preparing for real world usage.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
- Windows Server 2022

<h2>Deployment</h2>
<h3>Install Active Directory</h3>
<p>
<img src="https://github.com/user-attachments/assets/9eee39a8-7a0a-4e84-b6f6-7afdfbf287e4" />
<img src="https://github.com/user-attachments/assets/607b005a-a423-4282-968f-55fae04dcec9" />
</p>
<ol>
  <li>Login to DC-1 and install Active Directory Domain Services</li>
  <b>control panel → turn windows features on or off → next 3x → Active Directory Domain Services → Add Features → next 3x → install</b>
  <li>Promote as a DC: Setup a new forest as mydomain.com</li>
  <b>Service Manager → click the flag in the grey task bar → promote this server to a domain controller → add new forest → enter domain name (mydomain.com) → create password → uncheck the box in DNS options → click next until install </b>
  <li>Restart, then log back into DC-1 as user: mydomain.com\labuser (the password will be the same) </li>
  <b> </b>
</ol>
<br />

<h3>Create a Domain Admin user within the domain</h3>
<p>
<img src="https://github.com/user-attachments/assets/7393846d-73ca-4084-8af0-a7cc62003b48"/>
</p>
<ol>
  <li>In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”</li>
  <b>task bar search Active Directory Users and Computers → click mydomain.com → right click in open space → new →  Organization Unit </b>
  <li>Create a new OU named “_ADMINS”</li>
  <li>Create a new employee named “Jane Doe” with the username of “jane_admin” / Cyberlab123!</li>
  <b>click _EMPLOYEES → right click in open space → new → user </b>
  <li>Add jane_admin to the “Domain Admins” Security Group</li>
  <b>right click Jane Doe → add to a group... → type "Domain Admins" → check names → ok </b>
  <li>Log out / close the connection to DC-1 and log back in as “mydomain.com\jane_admin”</li>
  User jane_admin as your admin account from now on
  
</ol>
<br />

<h3>Join Client-1 to the Domain</h3>
<p>
<img src="https://github.com/user-attachments/assets/28826171-6f22-4a90-94ee-dfe6e6d1c4f8" />
</p>
<ol>
  <li>Login to Client-1 as the original local admin (labuser) and join it to the domain (computer will restart)</li>
  <b>settings → system → about → advanced system settings → computer name → change </b>
  <li>Login to the Domain Controller and verify Client-1 shows up in ADUC</li>
  <li>Create a new OU named “_CLIENTS” and drag Client-1 into there</li>
</ol>
<br />

<h3>Setup Remote Desktop for non-administrative users on Client-1</h3>
<p>
<img src="https://github.com/user-attachments/assets/ad05db81-e628-4278-b25f-ef612ddebf49" />
</p>
<ol>
  <li>Login to Client-1 as mydomain.com\jane_admin</li>
  <li>Open system properties</b>
  <li>Click “Remote Desktop”</li>
  <li>Allow “domain users” access to remote desktop</li>
</ol>
<b>You can now log into Client-1 as a normal, non-administrative user</b>
<br />

<h3>Create a bunch of additional users and attempt to log into client-1 with one of the users</h3>
<p>
<img src="https://github.com/user-attachments/assets/9a4d2bed-b7d6-4e80-a8b0-89459362ac9c" />
</p>
<ol>
  <li>Login to DC-1 as jane_admin</li>
  <b></b>
  <li>Open PowerShell_ise as an administrator</li>
  <li>Create a new File and paste the contents of the <a href='https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1'>script</a> into it</li>
  <li>Run the script and observe the accounts being created</li>
  <li>When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES)</li>
  <li>attempt to log into Client-1 with one of the accounts (take note of the password in the script)</li>
</ol>
<br />
