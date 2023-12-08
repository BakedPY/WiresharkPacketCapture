<h1>Wireshark Packet Capture</h1>



<h2>Description</h2>
Project consists of a simple PowerShell script that walks the user through "zeroing out" (wiping) any drives that are connected to the system. The utility allows you to select the target disk and choose the number of passes that are performed. The PowerShell script will configure a diskpart script file based on the user's selections and then launch Diskpart to perform the disk sanitization.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Diskpart</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<p align="center">
Launch the utility: <br/>
<img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<div>
<h2 align="center">Exploring the Wireshark GUI</h2>
In the screenshot below, you will notice the columns of properties. Here is an overview of the key property columns listed for each packet:

No. : The index number of the packet
Time: The timestamp of the packet
Source: The source IP address
Destination: The destination IP address
Protocol: The protocol contained in the packet
Length: The total length of the packet
Info: Some information about the data in the packet (the payload) as interpreted by Wireshark
</div>

<div>
Note that not all data packets are the same color. Different colors are used to provide high-level visual cues to help you quickly classify the different types of data. Network packet capture files can contain large amounts of data so the coloring rules assist in quickly identifying the data that is relevant to you. In the example packet above, The blue packets contain SSH and TCP traffic, the light blue packets contain DNS traffic and the packets in pink contain ICMP traffic.

<h2 align="center">Applying a basic Wireshark filter and inspecting a packet</h2>

In this section, we will apply a filter to search for traffic associated with a specific IP address. We will input ip.addr == 142.250.1.139 into the text box above the list of packets. The filtered results are in the following screenshot:
</div>


<div>
As you can see in the picture above, the list of packets displayed is now significantly reduced and contains only the packets where either the source or the destination IP address matches the address entered in the text box. Now there are only two packet colors: light pink for ICMP protocol packets and light green for TCP (and HTTP, which is a subset of TCP) packets.

<h2 align="center">Exploring the subtrees within a selected packet</h2>

Now we will select the first TCP packet in this list to get a detailed view of the selected packet.  In the detailed view, you will find subtrees for various parts of the selected TCP packet. You can access more information included in each subtree by expanding into it. An overview of the subtrees of information are:

Frame: Contains the frame length and the arrival time of the packet
Ethernet II: Includes the source and destination MAC addresses and the type of internal protocol that the Ethernet protocol contains
Internet Protocol Version 4 (IPv4): Contains the source and destination IP addresses and the Internal Protocol (for example, TCP or UDP), which is carried inside the IP packet.

Transmission Control Protocol (TCP): Provides detailed information about the TCP packet, including the source and destination TCP ports, TCP sequence numbers, and the TCP flags
</div>

<div>
By observing the TCP subtree, highlighted in blue, you’ll notice the source port which is 49652, and the destination port which is port 80. Port 80 is a commonly used internet communication protocol, Hypertext Transfer Protocol (HTTP). You can also identify the source and destination IP addresses in the IPv4 subtree, the source and destination MAC addresses in the Ethernet II subtree, and in the Frame subtree, you can identify the frame length.

Let's go into these subtrees and identify the information within them. This will be a great exercise to get more familiar with what information may be in a packet.

We’ll first look into the Frame subtree, which is shown in the following screenshot:
</div>

<div>
The Frame subtree pictured above contains details about the overall network packet, or frame, including the length of the frame and the arrival time of the frame amongst other information.

Now let’s take a look into the detailed view of the Ethernet II subtree, shown in the following screenshot:
</div>

<div>
You’ll notice the Ethernet II subtree contains information like the source and destination MAC addresses and the type of internal protocol that the Ethernet contains.

Now look at the details view of the IPv4 subtree shown in the following screenshot:

</div>

<div>
You’ll notice the IPv4 subtree holds details about the IP data like the source and destination IP addresses, Time to Live (TTL), and the internal protocol amongst other information.

Now look at the detailed view of the TCP subtree in the following screenshot:
</div>

<div>
You’ll notice the TCP subtree provides detailed information about the TCP packet, including the source and destination ports, the TCP sequence numbers, and the TCP flags amongst other information.

Let's take a look at the information inside the Flags subtree, which is inside the TCP subtree:
</div>

<div>
Inside the Flags subtree, you can identify any TCP flags set in this packet.

The subtrees information that is within a packet is valuable to cybersecurity professionals as they can provide detailed information and aid in the detection and analysis of network traffic.

<h2 align="center">Use filters to select packets</h2>

Let's analyze specific network packets based on where the packets came from or where they were sent to. We will explore how to select packets using their physical MAC address or their IP address. Take a look at the following screenshot:
</div>

<div>
 By applying a display filter in the text box (highlighted in green), which in this case is ip.src == 142.250.1.139, you can see a list is returned that only contains packets that came from 142.250.1.139

Let’s apply a display filter that only contains packets that were sent to the IP address: 142.250.1.139 and see what happens. We will input to the text box: ip.dst == 142.250.1.139, shown in the following screenshot:
</div>

<div>
 You can observe in the screenshot above that only packets that were sent to the IP address: 142.250.1.139 are listed.

Now let's filter for traffic to or from a specific Ethernet MAC address. To do this we will apply another display filter, which in this case is eth.addr == 42:01:ac:15:e0:02, shown in the following screenshot:
</div>

<div>
 This display filter, filters traffic related to the inputted MAC address, regardless of the other protocols involved. You will be able to know this to be the case by double-clicking on any packet in the filtered list and should identify that the MAC address you specified in the filter is listed as either the source or destination MAC address, as seen in the screenshot above.

Now in the following screenshot, we will observe what is inside the IPv4 subtree of this packet:
</div>

<div>
As you can see in the expanded IPv4 subtree, there is a Time to Live (TTL) field. In this packet, the TTL is 64. The number 64 is the amount of “hops” this packet is set to exist inside a network before being discarded by the router. The TTL prevents packets from being circulated indefinitely across a network. 

If a packet has a very large TTL, it could cause a ton of traffic if for some reason it was caught in a circular route, and interfere with the normal operations of a network. If the TTL on a packet is too low, the packet will not make it to its destination, resulting in a loss of connectivity.

<h2 align="center">Use filters to explore DNS packets</h2>

In this section, we will use filters to select and examine DNS traffic. We will examine how the DNS packet data contains both queries (names of internet sites that are being looked up) and answers (IP addresses that are being sent back by a DNS server when the name is successfully resolved). Let’s start by applying a display filter, which will be udp.port == 53, shown in the following screenshot:
</div>

<div>
As you can see in the screenshot above, the list only contains UDP port 53 traffic. You should note, that UDP port 53 handles DNS traffic, so you will see the list being traffic related to DNS queries and responses only.

Let’s go into the first packet and observe the details in this packet, which is shown in the following screenshot:
</div>

<div>
You will see details about this packet but bring your attention to the queries field. When the DNS subtree is expanded and then the queries subtree is expanded, you’ll notice that the name of the website that was queried was opensource.google.com 

Now let's take a look at another packet in this list, pictured below. For this example let’s select the fourth packet in this list, then go into the DNS subtree, and then into the Answers subtree, shown in the following screenshot:
</div>

<div>
You’ll notice that the Answers data, which is in the DNS subtree, has the name that was queried (opensource.google.com) and the addresses that are associated with that name.
</div>

<div>
<h2 align="center">Use filters to explore TCP packets</h2>
</div>
<div>
In this section we will go over additional filters to select and examine TCP packets as well as how to search for text that is present in payload data contained in network packets.

We will start by adding a display filter (tcp.port == 80) to select TCP port 80 traffic. Keep note that TCP port 80 is the default port that is associated with web traffic. The filtered results are shown in the following screenshot:
</div>

<div>
You’ll notice that quite a few packets were returned that are associated with TCP port 80 traffic. Now we’ll select the first packet in the list and observe its details, in the following screenshot:
</div>

<div>
We can gather some information from the subtrees without going into them. For example, the source and destinations of IP addresses and MAC addresses. 

We’ll now go into the IPv4 subtree and observe the detailed information, shown in the following screenshot:
</div>

<div>
Within this IPv4 subtree, you’ll be able to gather key information like the header length, the destination IP address, and the Time to Live (TTL) among other information.

Now let’s expand into the Frame subtree and see what information we can identify, shown in the following screenshot:
</div>

<div>
You’ll notice the Frame length being 54 bytes and the arrival time of this packet, which includes date, time, and timezone.

Finally, we will filter to select TCP packet data that contains specific text data. Let's filter for TCP packet data that contains “curl”. To do this we will input tcp contains “curl” into the text box. The results are shown in the following screenshot:
</div>

<div>
Now the list is filtered to contain only packets that have a web request made with the “curl” command.

<h2 align="center">Final thoughts</h2>

This tutorial shows only a fraction of what can be done with a Network Protocol Analyzer like Wireshark. I hope that in providing this written and visual tutorial, you are able to become more confident in your detection and analyzation skills, and possibly become motivated to explore Wireshark on your own. 

</div>
