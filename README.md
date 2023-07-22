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
- Filter Traffic by ICMP Protocol
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
We'll open PowerShell from the Start Menu of our Windows 10 VM to open the command line, then go to our Azure portal on our local PC, and copy the Private IP Adress of our Windows Server VM. Then, back to our Windows 10 VM, we type "ping" followed by that IP Address.
</p>
<p>
If there are no connectivity issues, or any Firewall blocking traffic, you will get 4 replies from the IP Address, showing that connectivity is established and traffic between the two machines is unhindered.
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/36dcf86b-7300-4fba-9a98-8912a3e0ad13"/>
</p>

<p>
Go to Wireshark and it will show the ICMP traffic flow resulting from that "ping" command.
</p>

<p>
<img src=https://github.com/mariamcpherson/protocols/assets/139581822/2143654a-0b32-473f-9731-39ca58cf1f0c"/>
</p>

<p>
Here, we can see the request sent from our source, which is the Windows 10 VM with IP 10.0.0.5, and right below the reply from the destination, which is the Windows Server VM, with IP 10.0.0.5.
</p>

<p>
There is also the option of perpetually pinging specific IP Addresses, which in Wireshark will show as continues requests and replies between one IP Address and the other. The command for this is "ping -t" followed by the IP Address you want to ping. In order to stop that function, enter Control + C.
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/ec5aee61-963e-419c-80ba-26dcdfa6f331"/>
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/ea24122a-dc46-4fc8-a5c2-5a26e165628f)"/>  
</p>


<p>
From both of those images from PowerShell and Wireshark we see a continuous string of replies and responses between both IP Addresses resulting from that perpetual ping commmand.
</p>

<p>
Now, for the sake of becoming more familiar with network protocols and filtering traffic, let's see what happens when we change the Firewall configuration of the Windows Server machine to block any inbound icmp traffic.
</p>
<p>
In your local PC, in your Azure portal, type Network Security Groups, and then click on the VM name for the Server Machine.
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/dba9f01e-3ea1-4054-9a33-34f955fd2948"/>
</p>


<p>
Click on Inbound Rules on the left side menu, then click Add at the top, select IMCP, Deny. In Priority, type any number before 300, so that this new rule will be first on the list, so 200 for instance. 
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/588ea738-7c72-4e10-a67e-d49f1937d8a6"/>
</p>

<p>
Now, let's use the ping command again like we did earlier in this step and see what happens. 
</p>

<p>
<img src=(https://github.com/mariamcpherson/protocols/assets/139581822/23f19e9b-d5bf-4d64-af10-02cb7dd35726)"/>
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/b83b1107-1b89-49a3-9ebf-28789136417b"/>
</p>


<p>
In the images above we can see that there was no response when our Windows 10 machine tries to contact our Windows Server machine, as this last one does not allow inbound ICMP traffic anymore.
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
