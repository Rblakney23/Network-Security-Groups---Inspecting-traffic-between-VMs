<p align="center">
<img src="https://i.imgur.com/P9zr6KW.jpeg" alt="NSG Logo"/>
</p>

<h1>Network-Security-Groups---Inspecting-traffic-between-VMs</h1>
In this lab, we use Wireshark to analyze inbound and outbound network traffic on Azure Virtual Machines. We also explore how Network Security Groups (NSGs) control traffic flow by configuring and testing custom security rules in a cloud environment.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Networking Protocols (SSH, RDP, DNS, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Ubuntu Server 20.04
- Windows 10 (21H2) (Client Machine)

<h2>Lab Objectives</h2>

- Deploy Azure Virtual Machines
- Capture and analyze traffic w/ Wireshark
- Test network communication between VMs
- Experiment w/ NSGs

  
<h2>Actions and Observations</h2>
Welcome to this tutorial on using Network Security Groups (NSGs) and inspecting network protocols with Wireshark in an Azure environment.

We’ll begin by creating two virtual machines in Azure:

- One Linux (Ubuntu) VM

- One Windows 10 VM
Each VM should be provisioned with 2 CPUs and placed within the same Virtual Network (VNet) to ensure they can communicate privately.

Once both VMs are set up:

Log into the Windows VM using Remote Desktop Protocol (RDP).

Download and install Wireshark from the official site:
🔗 Wireshark Download

Open Wireshark and apply a filter for ICMP traffic only. ICMP (Internet Control Message Protocol) is a Layer 3 protocol used for diagnostic purposes — for example, by the ping command to test connectivity between two hosts.

From the Windows VM, ping the private IP address of the Linux VM. As you do this, you’ll observe real-time ICMP packets being captured in Wireshark.

This exercise allows you to visually inspect network communication, better understand how protocols behave, and begin experimenting with NSG rules to control traffic flow.


<p>
<img src="https://i.imgur.com/XeKEhk2.png" height="400%" width="70%" alt="AD-users&computers"/>
</p>
<p>
Now we will start creating Organizational Units or "OUs". The first set of OU's will be "_EMPLOYEES" and "_ADMINS". To do that, you will right-click on the domain name, select New, then Organizational Unit.

In the "_ADMINS" OU, right-click -> new -> User and create the user "Jane Doe". For the user login name, insert "jane_admin". Once that is done, add Jane to the domain admins security group. 
</p>
<br />

<p>
<img src="https://i.imgur.com/jBgCBrs.png" height="400%" width="80%" alt="AD-adminCreation"/>
</p>
<p>
Next, we have to join Client-1 machine to the Domain. To do this, right-click the Windows icon in the bottom left of the screen. Select System -> Rename this PC (advanced) -> under Computer Name select Change -> domain -> enter "mydomain.com". After your computer restarts, log back into the client machine with the "mydomain.com\labuser" credentials. Client-1 will now be a part of mydomain.com
</p>
<br />

<p>
<img src="https://i.imgur.com/m8PnNVm.png" height="400%" width="80%" alt="AD-joinClientDomain"/>
</p>
<p>
Now that Client-1 is joined to the Domain, the next part is to set up Remote Desktop for non-admin users on the client machine. Log into Client-1 as jane_admin -> right-click the Windows icon in the bottom left of the screen. Select System -> Remote Desktop -> add "Domain Users" to give that group access to remote desktop.  
</p>
<br />

<p>
<img src="https://i.imgur.com/TsX8VaG.png" height="400%" width="80%" alt="AD-remoteDesktop"/>
</p>
<p>
In this next part, I used PowerShell to create additional users, picked one random user to RDP into Client-1, and confirmed the successful login.
</p>
<br />

<p>
<img src="https://i.imgur.com/bVx5cRC.png" height="400%" width="80%" alt="AD-powerShellUsers"/>
</p>
<p>
<img src="https://i.imgur.com/1NNidgy.png" height="400%" width="80%" alt="AD-powerShellUsers"/>
</p>
<p>
<img src="https://i.imgur.com/dk4usQ7.png" height="400%" width="80%" alt="AD-userRDP"/>
</p>

