<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Inspecting Traffic Between Azure Virtual Machines</h1>
<p>
Internet protocols are a set of rules and conventions that govern the communication and data exchange between devices over the internet. These protocols facilitate the smooth transfer of data packets and ensure that different devices and systems can understand and interact with each other.
</p>
<p>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark.
<p><br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022

<h2>High-Level Steps</h2>

- Download and Install Wireshark on Windows 10 VM
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>

<p>
- Step 1: 
</p>
<p>
For this tutorial we are going to use Wireshark, which is a widely used open-source network protocol analyzer and packet capture tool. It is also known as a network sniffer or packet sniffer. Wireshark allows users to capture and inspect network packets in real-time or from saved capture files. It is available for various operating systems, including Windows, macOS, and Linux. 
</p>
<p>
Wireshark is a powerful tool used by network administrators, security professionals, and developers for a wide range of purposes, such as network troubleshooting, monitoring network performance, analyzing security incidents, and understanding network behavior. However, it's essential to use Wireshark responsibly, as capturing network traffic may involve legal and privacy considerations.
</p>
<p>
Download and install Wireshark in the Windows 10 VM.
</p>
  
<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/f14346b0-74a2-4a16-a3de-b3a3a1467f59"/>
</p>

<p>
Once Wireshark is installed, select the Ethernet option and then click the blue fin icon at the top left corner to start filtering traffic.
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/75b6808f-a32f-4dbf-b8e5-20665dc3b79d)"/>
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/6b0e1b0d-b71d-4bb5-9f52-a5682c63f4e9)"/>
</p>

<p>
We will see all the traffic coming in and out from our virtual machine.
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/819d7906-5cc3-490b-bf20-71b3c9d4735f"/>
</p>

<p>
- Step 2:
</p>

<p>
We're going to start by filtering traffic by icmp protocol, and in order to see it better on Wireshark, we can type "icmp" on the top search bar of Wireshark.
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/da438dcd-c808-41ae-83fd-4270495af2f4"/>
</p>

<p>
Now, we're going to test the connectivity between our two Azure Virtual Machines by using the "ping" in the command line.
</p>
<p>
The "ping" command tests the reachability and responsiveness of a remote network host (typically a computer or server) over an Internet Protocol (IP) network. 
</p>
<p>
When you use the ping command, your computer sends out a small packet of data (ICMP Echo Request) to the target host. If the target host is reachable and responsive, it will reply with a corresponding packet (ICMP Echo Reply) back to your computer. The ping command measures the round-trip time it takes for the packet to travel from your computer to the target host and back, giving an indication of the network latency or delay.
</p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>



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
