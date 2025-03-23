<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1 align="center">On-premises Active Directory Deployed in the Cloud (Azure)</h1>

This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />
It simulates an enterprise network by setting up a domain controller (DC) on Windows Server 2022 and connecting a Windows 10 client to the domain.

---

<h2>🎥 Video Demonstration</h2>

- ### [YouTube: How to Deploy On-Premises Active Directory within Azure Compute](https://www.youtube.com) *(Replace with your actual link)*

---

<h2>🧰 Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Protocol (RDP)
- Active Directory Domain Services (AD DS)
- PowerShell
- DNS Server

---

<h2>🖥️ Operating Systems Used</h2>

- Windows Server 2022 (Domain Controller)
- Windows 10 Pro (21H2) (Client)

---

<h2>📋 High-Level Deployment and Configuration Steps</h2>

- Create two Virtual Machines in Azure (Server and Client)
- Promote the Server to a Domain Controller (Install AD DS)
- Configure a custom domain (e.g., `mydomain.local`)
- Join the Windows 10 Client VM to the Active Directory domain

---

<h2>⚙️ Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/NfLg3l2.png" height="80%" width="80%" alt="Azure VM Creation"/>
</p>
<p>
<strong>Step 1:</strong> Deploy two Azure VMs. One will run Windows Server 2022 and act as the Domain Controller. The other will run Windows 10 and serve as a domain-joined workstation. Make sure both VMs are in the same virtual network.
</p>
<br />

<p>
<img src="https://i.imgur.com/xuQxjvi.png" height="80%" width="80%" alt="Promoting Domain Controller"/>
</p>
<p>
<strong>Step 2:</strong> On the Server 2022 VM, install the <code>Active Directory Domain Services</code> role using Server Manager. After installation, promote the server to a domain controller and create a new forest (e.g., `mydomain.local`).
</p>
<br />

<p>
<img src="https://i.imgur.com/4dO7ZkC.png" height="80%" width="80%" alt="DNS Configuration"/>
</p>
<p>
<strong>Step 3:</strong> Update the network settings on the Windows 10 VM so its DNS points to the private IP of the Domain Controller. This is required for domain joining to work correctly.
</p>
<br />

<p>
<img src="https://i.imgur.com/6c7RQhI.png" height="80%" width="80%" alt="Join Domain"/>
</p>
<p>
<strong>Step 4:</strong> On the Windows 10 VM, go to <code>System > About > Rename this PC (Advanced)</code> and click "Join a domain". Enter your custom domain (e.g., `mydomain.local`) and provide credentials of a domain user. Restart the VM after successful domain join.
</p>
<br />

<p>
<img src="https://i.imgur.com/qcyRHMm.png" height="80%" width="80%" alt="Test Login"/>
</p>
<p>
<strong>Step 5:</strong> Log in to the Windows 10 VM using domain credentials (e.g., `mydomain\Zack.Nelson`). Verify domain policies, access, and trust are functioning correctly.
</p>

---

<h2>🔧 Optional Configuration</h2>

- Create and organize Organizational Units (OUs)
- Create users, groups, and apply Group Policy Objects (GPOs)
- Install RSAT tools to manage AD remotely
- Set up additional DNS zones or replication

---

<h2>📬 Questions or Issues?</h2>

If you have questions, feel free to open an issue in this repo or drop a comment under the YouTube tutorial!

---
