

<h1>Network File Shares and Permissions</h1>
In this tutorial, we understand how networking file sharing and permissions work and play with it a little bit. <br />

Prerequisite project: My guide to active directory exploration (https://github.com/rohaniat/configure-ad)



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Create some sample file shares with various permissions
- Step 2: Attempt to access file shares as a normal user
- Step 3: Create an “ACCOUNTANTS” Security Group, assign permissions, and test access

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/8U5sDCl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 1: Create some sample file shares with various permissions

Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)

Connect/log into Client-1 as a normal user (mydomain\<someuser>)

On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”

Set the following permissions (share the folder) for the “Domain Users” group:

Folder: “read-access”, Group: “Domain Users”, Permission: “Read”

Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”

Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”

(Skip accounting for now)

</p>
<br />

<p>
<img src="https://i.imgur.com/OadYYf6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 2: Attempt to access file shares as a normal user

On Client-1, navigate to the shared folder (start, run, \\dc-1)
Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in?

</p>
<br />

<p>
<img src="https://i.imgur.com/Lc8NASt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 3: Create an “ACCOUNTANTS” Security Group, assign permissions, and test access

Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”

On the “accounting” folder you created earlier, set the following permissions:

Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”

On Client-1, as  <someuser>, try to access the accountants folder. It should fail.
 
Log out of Client-1 as  <someuser>

On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group

Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - does it work now? It should.

</p>
<br />
