<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1 align="center">Active Directory Configuration in Azure</h1>

This lab demonstrates how to deploy and configure an on-premises-style Active Directory environment using Azure Virtual Machines. You'll set up a Domain Controller and a client machine, create users and OUs, and explore core domain features including remote access and scripting.

---

<h2>🎥 Video Demonstration</h2>

- ### [YouTube: Active Directory Configuration in Azure (Part 1 & 2)](https://www.youtube.com) *(Coming Soon)*

---

<h2>🧰 Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines, Networking, DNS)
- Remote Desktop Protocol (RDP)
- Windows Server 2022
- Windows 10 Pro
- Active Directory Domain Services (AD DS)
- PowerShell + PowerShell ISE

---

<h2>🖥️ Operating Systems Used</h2>

- **DC-1:** Windows Server 2022 (Domain Controller)  
- **Client-1:** Windows 10 Pro (Domain-Joined Workstation)

---

<h2>📦 VM Details</h2>

- **Username:** `labuser`  
- **Password:** `Cyberlab123!`  
- **Domain:** `mydomain.com`

---

<h2>⚙️ Part 1: Set Up Domain Controller & Client VM</h2>

### 🏗️ Azure Infrastructure

1. **Create a Resource Group**
2. **Create a Virtual Network + Subnet**
3. **Create a Windows Server 2022 VM**  
   - **Name:** `DC-1`  
   - Assign static private IP
4. **Create a Windows 10 VM**  
   - **Name:** `Client-1`  
   - Same region & VNet as `DC-1`
   - Set DNS to `DC-1`'s private IP

---

### 🛜 Basic Connectivity Checks

5. **Disable Windows Firewall** on DC-1 for testing
6. On `Client-1`, open PowerShell:
   - Run `ping <DC-1 private IP>` → Ensure success
   - Run `ipconfig /all` → DNS should point to `DC-1`

---

### 🧱 Install & Promote Active Directory

7. On `DC-1`:
   - Install **Active Directory Domain Services**
   - Promote to Domain Controller → Create new forest: `mydomain.com`
   - Restart and log back in as: `mydomain.com\labuser`

---

### 👩‍💼 Create Domain Admin User

8. In **ADUC (Active Directory Users and Computers)**:
   - Create OU: `_EMPLOYEES`
   - Create OU: `_ADMINS`
   - Add user:  
     **Name:** `Jane Doe`  
     **Username:** `jane_admin`  
     **Password:** `Cyberlab123!`  
     - Add to: **Domain Admins** security group
   - Log in as: `mydomain.com\jane_admin`

---

### 💻 Join Client to the Domain

9. On `Client-1`:
   - Log in as local `labuser`
   - Join domain: `mydomain.com`
   - Restart VM
10. On `DC-1`, verify `Client-1` appears in ADUC
    - Create OU: `_CLIENTS`
    - Move `Client-1` into `_CLIENTS`

---

<h2>🔒 Part 2: Additional AD Configuration</h2>

### 🖥️ Enable Remote Desktop for Domain Users

11. On `Client-1` (logged in as `jane_admin`):
   - Open **System Properties > Remote Desktop**
   - Allow access for **Domain Users**

> 💡 You'd normally use Group Policy for this at scale. Future lab idea!

---

### 👥 Bulk User Creation via PowerShell

12. On `DC-1`:
   - Open **PowerShell ISE as Administrator**
   - Paste and run the user creation script (creates users in `_EMPLOYEES`)
   - Here is the script, will make 10,000 users: https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1
   - Open ADUC to confirm users were created successfully

13. Log in to `Client-1` using one of the new domain accounts  
    *(Refer to the password used in the script)*

---

<h2>✅ Final Notes</h2>

- Do **not delete** the VMs — they’ll be used in future labs
- To save on Azure billing, **stop** the VMs from the Azure Portal when not in use

---

<h2>📚 Summary</h2>

By completing this lab, you've successfully:

- Built an Active Directory environment in the cloud
- Promoted a Domain Controller and joined a client to the domain
- Managed users, OUs, and access rights
- Configured RDP permissions for domain users
- Used PowerShell scripting to automate account creation

This setup is foundational for real-world IT roles in systems administration, help desk, and enterprise support.

---

<h2>📬 Questions or Issues?</h2>

Open an issue in this repo or drop a comment on the walkthrough video!

---
