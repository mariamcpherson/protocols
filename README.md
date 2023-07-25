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
- Filter Traffic by DHCP Protocol
- Filter Traffic by DSN Protocol

<h2>Actions and Observations</h2>

<p>
- Dowloading and Installing Wireshark
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
- Filtering Traffic by ICMP Protocol
</p>

<p>
ICMP stands for Internet Control Message Protocol. It is an integral part of the Internet Protocol Suite (TCP/IP) and is used for diagnostic and control purposes in IP networks. ICMP operates at the network layer (Layer 3) of the OSI model and works alongside IP to provide important feedback and error reporting to network devices. ICMP is primarily used to send error messages and perform network testing tasks.
</p>
<p>
ICMP messages are encapsulated within IP packets and are generally used by networking devices like routers and hosts to communicate network status, errors, and troubleshooting information. While ICMP plays a crucial role in network diagnostics and troubleshooting, it can also be misused for certain types of cyber attacks, such as ICMP flood attacks or ping flooding. To mitigate such risks, some network devices and firewalls may limit or control the handling of ICMP traffic.
</p>
<p>
It's worth noting that ICMP is a protocol focused on network control and diagnostic functions and is separate from protocols like TCP and UDP, which are responsible for data transmission and application-layer communications.
</p><br />
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
- Filtering Traffic by DHCP Protocol
</p>

<p>
DHCP stands for Dynamic Host Configuration Protocol. It is a network protocol used to automatically assign and manage IP addresses and other network configuration information to devices (known as DHCP clients) on a network. The DHCP protocol simplifies the process of setting up and managing IP addresses, making it easier for both administrators and end-users in a network environment.
</p>
<p>
By automating the process of IP address assignment and configuration, DHCP significantly reduces the administrative overhead of managing IP addresses in a network. It is commonly used in local area networks (LANs), home networks, and larger enterprise networks to efficiently manage IP address allocation and network settings for a large number of devices.
</p>

<p>
In order to filter traffic by DHCP protocol, type "dhcp" inside the search bar in Wireshark, or alternatively, use the port number: udp.port==68
</p>
<p>
In PowerShell enter the following command: ipconfig /renew
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/f02c53e1-032d-4f02-9256-521861eb15fa)"/>
</p>

<p>
<img src="https://github.com/mariamcpherson/protocols/assets/139581822/302392df-281e-496d-88c4-ee3d34a50c1e"/>
</p>

<p>
The ipconfig /renew command is used in Windows operating systems to renew the IPv4 address configuration for a network interface. It is a command-line utility that interacts with the Dynamic Host Configuration Protocol (DHCP) server to request a new IP address lease for the network adapter.
</p>
<p>
The ipconfig /renew command is useful in scenarios where a device is connected to a network with DHCP enabled but is unable to obtain a valid IP address automatically. It can be used to force the renewal of the IP address lease and resolve issues related to IP address conflicts or DHCP lease expirations.
</p>
<p>
Note that ipconfig /renew command is specific to IPv4 addresses. For renewing IPv6 addresses, you would use the ipconfig /renew6 command. 
</p>
<br />


<p>
- Filtering Traffic by DSN Protocol
</p>

<p>
DNS stands for Domain Name System, and it is a fundamental protocol used on the internet to translate human-readable domain names (such as www.example.com) into IP addresses (such as 203.0.113.42) that computers and networking devices use to locate resources on the internet.
</p>
<p>
The DNS protocol serves as a distributed and hierarchical naming system, allowing users to access websites and other online services without needing to remember and use the numeric IP addresses of the servers hosting those resources.
</p>

<p>
In this tutorial, a DNS server is already integrated with Active Directory and it was automatically installed in the Windows Server VM. 
</p>

<p>
Since this tutorial is picking up where the previous sections left, we have already configured the DNS settings of our Windows 10 VM to be set as the Private IP Address of the Server machine, which made this Server the Domain Controller of the Windows 10 machine, that is, its DSN server. 
</p>

<p>
In this context, we will be performing the following activities and observing the following:
</p>

<p>
- Inspect DNS A-records on the server (hostname to IP Address mappings)
</p>
<p>
- Create some of our own A-records on the server and observe them from the Client machine
</p>
<p>
- Delete records from server and inspect/clear Client DNS cache
</p>
<p>
- Touch on CNAME records (mapping one name to another)
</p>
<p>
- Discuss Root Hints
</p>
<p>

A-records: also known as "Address records" or "IPv4 address records," are a type of DNS (Domain Name System) resource record used to map domain names to specific IPv4 addresses. DNS is a system that translates human-readable domain names         (e.g., www.example.com) into IP addresses (e.g., 192.0.2.1) that computers and networks use to identify and communicate with each other on the internet.
</p>
      
<p>

 When you enter a domain name into your web browser's address bar or try to access a domain from any other application, your computer needs to find the corresponding IP address to connect to the appropriate server hosting the website or       service associated with that domain. This translation process is handled by DNS, and A-records play a crucial role in this translation.
</p>
      
<p>

      An A-record contains the following information:
</p>
      

<p>
      Hostname: The domain name (e.g., example.com) or subdomain (e.g., www.example.com).
  </p>
  <p>
      IPv4 Address: The numerical IP address associated with the domain or subdomain.
    </p>
    <p>
      For example, an A-record for the domain "example.com" might look like this:
    </p>

<p>
      When you type "example.com" in your web browser, your computer will perform a DNS lookup to find the IP address linked to that domain by querying DNS servers. Once it obtains the corresponding IPv4 address (192.0.2.1 in this case) from the A-       record, it can establish a connection to the correct server hosting the website.
    </p>
<p>
      A-records are essential for the functioning of the internet, enabling users to access websites and services using user-friendly domain names instead of having to remember and use complex IP addresses.
      </p>







<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>


</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
