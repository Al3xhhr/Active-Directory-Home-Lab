Enterprise Active Directory & Automation Home Lab
Project Overview
Designed and deployed a virtualized Active Directory (AD) domain environment simulating enterprise IT infrastructure. Configured core network and directory services, created custom Organizational Units (OUs), and automated bulk user account provisioning across departments using Windows PowerShell.
Environment & Technologies Used
Hypervisor: VMware Workstation
Operating System: Windows Server 2022 Standard Evaluation (Desktop Experience)
Directory Services: Active Directory Domain Services (AD DS), DNS
Automation & Scripting: Windows PowerShell
Domain Name: homelab.local
Static Server IP: 192.168.10.10
Implementation Steps
1. Virtual Machine & Network Setup
Provisioned a Windows Server 2022 Virtual Machine inside VMware with 4 GB RAM and 2 CPU cores.
Configured a static IP address (192.168.10.10), subnet mask (255.255.255.0), and local loopback DNS (127.0.0.1).
2. Active Directory Domain Services (AD DS) Deployment
Installed Active Directory Domain Services via Server Manager.
Promoted the server to a Domain Controller for the new forest homelab.local.
Verified DNS integration and local administrator authentication (HOMELAB\Administrator).
3. Automated Organizational Structure & User Provisioning
Authored and executed a PowerShell script to automatically build departmental Organizational Units (OUs): CyberSecurity, HelpDesk, IT_Dept, and Finance.
Automated the creation and attribute configuration (Titles, SamAccountNames, UserPrincipalNames) for 15 enterprise user accounts across all OUs with standard initial credentials.
4. Administrative Verification & Help Desk Simulation
Verified organizational structure and user creation using Active Directory Users and Computers (dsa.msc).
Practiced core Tier-1 Help Desk tasks including account provisioning, password resets, account unlocks, and status toggles.
## Screenshots

### Active Directory Users and Computers
![Active Directory OUs and Users](aduc.png)

### Server Manager Dashboard
![Server Manager Dashboard](server-manager.png)

Automation Script
PowerShell
# 1. Set Default Secure Password
$Password = ConvertTo-SecureString "P@ssword2026!" -AsPlainText -Force

# 2. Create Departmental OUs
New-ADOrganizationalUnit -Name "IT_Dept" -Path "DC=homelab,DC=local" -ErrorAction SilentlyContinue
New-ADOrganizationalUnit -Name "CyberSecurity" -Path "DC=homelab,DC=local" -ErrorAction SilentlyContinue
New-ADOrganizationalUnit -Name "HelpDesk" -Path "DC=homelab,DC=local" -ErrorAction SilentlyContinue
New-ADOrganizationalUnit -Name "Finance" -Path "DC=homelab,DC=local" -ErrorAction SilentlyContinue

# 3. Provision Enterprise Users Across OUs
New-ADUser -GivenName "Alex" -Surname "Hernandez" -Name "Alex Hernandez" -SamAccountName "ahernandez" -UserPrincipalName "ahernandez@homelab.local" -Path "OU=CyberSecurity,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "SOC Analyst Tier 1" -ChangePasswordAtLogon $false
New-ADUser -GivenName "Jordan" -Surname "Smith" -Name "Jordan Smith" -SamAccountName "jsmith" -UserPrincipalName "jsmith@homelab.local" -Path "OU=CyberSecurity,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "Security Engineer" -ChangePasswordAtLogon $false
New-ADUser -GivenName "Diana" -Surname "Prince" -Name "Diana Prince" -SamAccountName "dprince" -UserPrincipalName "dprince@homelab.local" -Path "OU=CyberSecurity,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "Incident Responder" -ChangePasswordAtLogon $false

New-ADUser -GivenName "Taylor" -Surname "Reed" -Name "Taylor Reed" -SamAccountName "treed" -UserPrincipalName "treed@homelab.local" -Path "OU=HelpDesk,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "Help Desk Lead" -ChangePasswordAtLogon $false
New-ADUser -GivenName "Morgan" -Surname "Vance" -Name "Morgan Vance" -SamAccountName "mvance" -UserPrincipalName "mvance@homelab.local" -Path "OU=HelpDesk,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "Tier 1 Technician" -ChangePasswordAtLogon $false
New-ADUser -GivenName "Casey" -Surname "Wright" -Name "Casey Wright" -SamAccountName "cwright" -UserPrincipalName "cwright@homelab.local" -Path "OU=HelpDesk,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "Tier 1 Technician" -ChangePasswordAtLogon $false
New-ADUser -GivenName "Clark" -Surname "Kent" -Name "Clark Kent" -SamAccountName "ckent" -UserPrincipalName "ckent@homelab.local" -Path "OU=HelpDesk,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "Support Specialist" -ChangePasswordAtLogon $false

New-ADUser -GivenName "Marcus" -Surname "Fenix" -Name "Marcus Fenix" -SamAccountName "mfenix" -UserPrincipalName "mfenix@homelab.local" -Path "OU=IT_Dept,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "SysAdmin" -ChangePasswordAtLogon $false
New-ADUser -GivenName "Elena" -Surname "Fisher" -Name "Elena Fisher" -SamAccountName "efisher" -UserPrincipalName "efisher@homelab.local" -Path "OU=IT_Dept,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "Network Engineer" -ChangePasswordAtLogon $false
New-ADUser -GivenName "David" -Surname "Miller" -Name "David Miller" -SamAccountName "dmiller" -UserPrincipalName "dmiller@homelab.local" -Path "OU=IT_Dept,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "Database Admin" -ChangePasswordAtLogon $false
New-ADUser -GivenName "Peter" -Surname "Parker" -Name "Peter Parker" -SamAccountName "pparker" -UserPrincipalName "pparker@homelab.local" -Path "OU=IT_Dept,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "IT Intern" -ChangePasswordAtLogon $false
New-ADUser -GivenName "Tony" -Surname "Stark" -Name "Tony Stark" -SamAccountName "tstark" -UserPrincipalName "tstark@homelab.local" -Path "OU=IT_Dept,DC=homelab,DC=local" -AccountPassword $Password -Enabled $true -Title "CTO" -ChangePasswordAtLogon $false
