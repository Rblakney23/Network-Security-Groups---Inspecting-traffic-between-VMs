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

- Log into the Windows VM using Remote Desktop Protocol (RDP).

- Download and install Wireshark from the official site:
[Wireshark Download](https://www.wireshark.org/download.html)

- Open Wireshark and apply a filter for ICMP traffic only. ICMP (Internet Control Message Protocol) is a Layer 3 protocol used for diagnostic purposes — for example, by the ping command to test connectivity between two hosts.

- From the Windows VM, ping the private IP address of the Linux VM. As you do this, you’ll observe real-time ICMP packets being captured in Wireshark.

This exercise allows you to visually inspect network communication, better understand how protocols behave, and begin experimenting with NSG rules to control traffic flow.


<p>
<img src="https://i.imgur.com/lbXnrc7.png" height="400%" width="70%" alt="AD-users&computers"/>
</p>
<p>
We can examine each individual packet to view the detailed data transmitted during each ping request. The image below highlights this, showing the contents and structure of the ICMP packets captured in Wireshark.
</p>
<br />

<p>
<img src="https://i.imgur.com/sQf9Bup.png" height="400%" width="80%" alt="AD-adminCreation"/>
</p>
<p>
<img src="https://i.imgur.com/j8r1r01.png" height="400%" width="80%" alt="AD-adminCreation"/>
</p>
<p>
In the next phase of the lab, we’ll initiate a continuous ping from the Windows machine to the Linux VM using the ping -t command. This command sends repeated ICMP echo requests until manually stopped.

While the ping is running, switch to the Linux VM and configure its Network Security Group (NSG) to block inbound ICMP traffic. Once this rule is applied, the Windows machine will stop receiving echo replies — effectively demonstrating how NSGs control network traffic.

To reverse the change, simply modify the NSG to allow ICMP traffic again through the Azure portal on the Linux VM’s NSG settings.

This section of the lab helps visualize how firewall rules directly impact real-time communication between cloud-hosted machines.
</p>
<br />

<p>
<img src="https://i.imgur.com/wgPjX9P.png" height="400%" width="80%" alt="AD-joinClientDomain"/>
</p>
<p>
Next, we’ll use the Windows VM to initiate an SSH connection to the Linux machine. SSH (Secure Shell) is a command-line-based protocol that provides secure remote access to a machine’s terminal without a graphical interface.

Before initiating the connection, set your Wireshark filter to capture only SSH traffic by using the filter tcp.port == 22.

Once the connection is established, you’ll immediately see SSH packets being captured in Wireshark, allowing you to observe the secure session in real time.
</p>
<br />

<p>
<img src="https://i.imgur.com/X93flTl.png" height="400%" width="80%" alt="DHCP filter"/>
</p>
<p>
Next, we’ll use Wireshark to analyze DHCP (Dynamic Host Configuration Protocol) traffic. DHCP operates on UDP ports 67 and 68 and is responsible for automatically assigning IP addresses and network configuration to devices.

To trigger DHCP traffic, run the following command in the Windows VM:

"ipconfig /renew"

This command forces the system to request a new IP address from the DHCP server.
</p>
<br />

<p>
<img src="https://i.imgur.com/UYLtPvN.png" height="400%" width="80%" alt="AD-remoteDesktop"/>
</p>
<p>
Now we’ll examine DNS (Domain Name System) traffic using Wireshark. DNS is responsible for translating human-readable domain names into IP addresses.

From the Windows VM, initiate a DNS query by running the command:

"nslookup www.google.com"

This command sends a request to the configured DNS server asking for the IP address of www.google.com. Wireshark will capture and display the DNS request and the corresponding response, allowing you to observe how domain resolution works in real time.
</p>
<br />

<p>
<img src="https://i.imgur.com/j3GQ0a3.png" height="400%" width="80%" alt="AD-remoteDesktop"/>
</p>
<p>
Lastly, we’ll filter for Remote Desktop Protocol (RDP) traffic, which uses TCP port 3389. To do this in Wireshark, apply the following filter:

"tcp.port ==3389"

Since we are actively connected to the Windows VM via RDP, you’ll notice a constant stream of traffic being captured. This is because RDP maintains a persistent connection and continuously transmits data to reflect GUI activity and user input in real time.

This observation demonstrates how RDP operates as a chatty protocol and highlights its behavior within a live network environment.
</p>
<br />
