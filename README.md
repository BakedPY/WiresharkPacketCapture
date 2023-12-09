<h1>Wireshark Packet Capture</h1>



<h2>Description</h2>
<p>In this presentation, we will go through the basics of a network protocol analyzer (NPA), in this case, Wireshark. We will explore the GUI of Wireshark. examine packet information, apply display filters, and analyze data packets to identify some of the information sent and received by the systems that connect when the network data is captured. Let’s get right into it!
</p>
<br />


<h2>Utilities Used</h2>

- <b>Wireshark</b> 

<h2>Environments Used </h2>

- <b>Mac OS</b> 

<h2>Program walk-through:</h2>

<div>
 <h2 align="center">Exploring the Wireshark GUI</h2>
</div>
<div>
 <p> 
 In the screenshot below, you will notice the columns of properties. Here is an overview of the key property columns listed for each packet:
 </p>
 <ul>
 <li><b>No. :</b> The index number of the packet</li>
 <li><b>Time:</b> The timestamp of the packet</li>
 <li><b>Source:</b> The source IP address</li>
 <li><b>Destination:</b> The destination IP address</li>
 <li><b>Protocol:</b> The protocol contained in the packet</li>
 <li><b>Length:</b> The total length of the packet</li>
 <li><b>Info:</b> Some information about the data in the packet (the payload) as interpreted by Wireshark</b></li>
 </ul>
 
 <img src="https://imgur.com/cQepQLU.png" align="center" height="80%" width="80%" alt="Wireshark GUI"/>
</div>
<div>
 <p>Note that not all data packets are the same color. Different colors are used to provide high-level visual cues to help you quickly classify the different types of data. Network packet capture files can contain large amounts of data so the coloring rules assist in quickly identifying the data that is relevant to you. In the example packet above, The blue packets contain SSH and TCP traffic, the light blue packets contain DNS traffic and the packets in pink contain ICMP traffic.
 </p>
</div>
<div>
 <h2 align="center">Applying a basic Wireshark filter and inspecting a packet</h2>
 
 <p>In this section, we will apply a filter to search for traffic associated with a specific IP address. We will input <em>ip.addr == 142.250.1.139</em> into the text box above the list of packets. The filtered results are in the following screenshot:
 </p>
 
 <img src="https://imgur.com/5YyRQa2.png" align="center" height="80%" width="80%" alt="Wireshark: inspecting a packet"/>
</div>
<div>
 <p> 
 As you can see in the picture above, the list of packets displayed is now significantly reduced and contains only the packets where either the source or the destination IP address matches the address entered in the text box. Now there are only two packet colors: light pink for ICMP protocol packets and light green for TCP (and HTTP, which is a subset of TCP) packets.
 </p>
 <h2 align="center">Exploring the subtrees within a selected packet</h2>
 <p> 
 Now we will select the first TCP packet in this list to get a detailed view of the selected packet.  In the detailed view, you will find subtrees for various parts of the selected TCP packet. You can access more information included in each subtree by expanding into it. An overview of the subtrees of information are:
 </p> 
 <ul>
 <li><b>Frame:</b> Contains the frame length and the arrival time of the packet</li>
 <li><b>Ethernet II:</b> Includes the source and destination MAC addresses and the type of internal protocol that the Ethernet protocol contains</li>
 <li><b>Internet Protocol Version 4 (IPv4):</b> Contains the source and destination IP addresses and the Internal Protocol (for example, TCP or UDP), which is carried inside the IP packet.</li>
 <li><b>Transmission Control Protocol (TCP):</b> Provides detailed information about the TCP packet, including the source and destination TCP ports, TCP sequence numbers, and the TCP flags</li>
 </ul>
 <img src="https://imgur.com/neW0zfC.png" align="center" height="80%" width="80%" alt="The subtrees within a packet"/>
</div>
<div>
 <p>  
 By observing the TCP subtree, highlighted in blue, you’ll notice the source port which is 49652, and the destination port which is port 80. Port 80 is a commonly used internet communication protocol, Hypertext Transfer Protocol (HTTP). You can also identify the source and destination IP addresses in the IPv4 subtree, the source and destination MAC addresses in the Ethernet II subtree, and in the Frame subtree, you can identify the frame length.
 </p>
 <p>  
 Let's go into these subtrees and identify the information within them. This will be a great exercise to get more familiar with what information may be in a packet.
 </p>
 <p>  
 We’ll first look into the Frame subtree, which is shown in the following screenshot:
 </p>
 <img src="https://imgur.com/tIFZi0a.png" align="center" height="80%" width="80%" alt="Wireshark frame subtree"/>
</div>
<div>
 <p>
 The Frame subtree pictured above contains details about the overall network packet, or frame, including the length of the frame and the arrival time of the frame amongst other information.
 </p>
 <p> 
 Now let’s take a look into the detailed view of the Ethernet II subtree, shown in the following screenshot:
 </p>
 <img src="https://imgur.com/YOVtE1k.png" align="center" height="80%" width="80%" alt="Ethernet subtree"/>
</div>
<div>
 <p>  You’ll notice the Ethernet II subtree contains information like the source and destination MAC addresses and the type of internal protocol that the Ethernet contains.
 </p>

 <p> 
 Now look at the details view of the IPv4 subtree shown in the following screenshot:
 </p>
 <img src="https://imgur.com/uAuAnWZ.png" align="center" height="80%" width="80%" alt="IPv4 subtree"/>
</div>
<div>
 <p>  
 You’ll notice the IPv4 subtree holds details about the IP data like the source and destination IP addresses, Time to Live (TTL), and the internal protocol amongst other information.
 </p>
 <p>  
 Now look at the detailed view of the TCP subtree in the following screenshot:
 </p>
 
 <img src="https://imgur.com/qfQY8sO.png" align="center" height="80%" width="80%" alt="TCP subtree"/>
</div>
<div>
 <p>  
 You’ll notice the TCP subtree provides detailed information about the TCP packet, including the source and destination ports, the TCP sequence numbers, and the TCP flags amongst other information.
 </p>
 <p> 
 Let's take a look at the information inside the Flags subtree, which is inside the TCP subtree:
 </p>
 <img src="https://imgur.com/4JC4PK8.png" align="center" height="80%" width="80%" alt="Flags subtree within the TCP subtree"/>
</div>
<div>
 Inside the Flags subtree, you can identify any TCP flags set in this packet.
 
 <p><b>The subtree information that is within a packet is valuable to cybersecurity professionals as they can provide detailed information and aid in the detection and analysis of network traffic.</b></p>
 
 <h2 align="center">Use filters to select packets</h2>
 
 Let's analyze specific network packets based on where the packets came from or where they were sent to. We will explore how to select packets using their physical MAC address or their IP address. Take a look at the following screenshot:
 
 <img src="https://imgur.com/G3ZBBRL.png" align="center" height="80%" width="80%" alt="Wireshark display filters"/>
</div>
<div>
 <p>By applying a display filter in the text box (highlighted in green), which in this case is <em>ip.src == 142.250.1.139</em>, you can see a list is returned that only contains packets that came from <em>142.250.1.139</em>
 </p> 
 <p>
 Let’s apply a display filter that only contains packets that were sent to the IP address: <em>142.250.1.139</em> and see what happens. We will input to the text box: <em>ip.dst == 142.250.1.139</em>, shown in the following screenshot:
 </p>
 
 <img src="https://imgur.com/kjzmo0u.png" align="center" height="80%" width="80%" alt="Wireshark: IP address display filter"/>
</div>
<div>
 <p>You can observe in the screenshot above that only packets that were sent to the IP address: 142.250.1.139 are listed.
 </p>
 <p>
 Now let's filter for traffic to or from a specific Ethernet MAC address. To do this we will apply another display filter, which in this case is <em>eth.addr == 42:01:ac:15:e0:02</em>, shown in the following screenshot:
 </p>
 
 <img src="https://imgur.com/Zo7ermV.png" align="center" height="80%" width="80%" alt="Wireshark: MAC address display filter"/>
</div>
<div>
  <p>
 This display filter, filters traffic related to the inputted MAC address, regardless of the other protocols involved. You will be able to know this to be the case by double-clicking on any packet in the filtered list and should identify that the MAC address you specified in the filter is listed as either the source or destination MAC address, as seen in the screenshot above.
 </p>
 <p>
 Now in the following screenshot, we will observe what is inside the IPv4 subtree of this packet:
 </p>
<img src="https://imgur.com/V592K5j.png" align="center" height="80%" width="80%" alt="Wireshark: IPv4 subtree packet"/>
</div>

<div>
 <p>
 As you can see in the expanded IPv4 subtree, there is a Time to Live (TTL) field. In this packet, the TTL is 64. The number 64 is the amount of “hops” this packet is set to exist inside a network before being discarded by the router. The TTL prevents packets from being circulated indefinitely across a network. 
 </p>
 <p>
 If a packet has a very large TTL, it could cause a ton of traffic if for some reason it was caught in a circular route, and interfere with the normal operations of a network. If the TTL on a packet is too low, the packet will not make it to its destination, resulting in a loss of connectivity.
 </p>
 <h2 align="center">Use filters to explore DNS packets</h2>
 <p>
 In this section, we will use filters to select and examine DNS traffic. We will examine how the DNS packet data contains both queries (names of internet sites that are being looked up) and answers (IP addresses that are being sent back by a DNS server when the name is successfully resolved). Let’s start by applying a display filter, which will be <em>udp.port == 53</em>, shown in the following screenshot:
 </p>
 <img src="https://imgur.com/wlRFq3a.png" align="center" height="80%" width="80%" alt="Wireshark: DNS display filter "/>
</div>

<div>
<p> 
As you can see in the screenshot above, the list only contains UDP port 53 traffic. You should note, that UDP port 53 handles DNS traffic, so you will see the list being traffic related to DNS queries and responses only.
</p>
<p> 
Let’s go into the first packet and observe the details in this packet, which is shown in the following screenshot:
</p>
<img src="https://imgur.com/jo6BW2q.png" align="center" height="80%" width="80%" alt="Wireshark: Packet filter"/>
</div>

<div>
 <p> 
 You will see details about this packet but bring your attention to the queries field. When the DNS subtree is expanded and then the queries subtree is expanded, you’ll notice that the name of the website that was queried was opensource.google.com 
 </p>
 <p> 
 Now let's take a look at another packet in this list, pictured below. For this example let’s select the fourth packet in this list, then go into the DNS subtree, and then into the Answers subtree, shown in the following screenshot:
 </p>
 <img src="https://imgur.com/NFfmoAE.png" align="center" height="80%" width="80%" alt="Wireshark: Answers subtree"/>
</div>
<div>
You’ll notice that the Answers data, which is in the DNS subtree, has the name that was queried <em>opensource.google.com)</em> and the addresses that are associated with that name.
</div>
<div>
 <h2 align="center">Use filters to explore TCP packets</h2>
</div>
<div>
 <p>
 In this section, we will go over additional filters to select and examine TCP packets as well as how to search for text that is present in payload data contained in network packets.
 </p> 
 <p> 
 We will start by adding a display filter <em>(tcp.port == 80)</em> to select TCP port 80 traffic. Keep note that TCP port 80 is the default port that is associated with web traffic. The filtered results are shown in the following screenshot:
 </p> 
 <img src="https://imgur.com/78kSKTB.png" align="center" height="80%" width="80%" alt="Wireshark: TCP traffic"/>
</div>
<div>
 <p>
 You’ll notice that quite a few packets were returned that are associated with TCP port 80 traffic. Now we’ll select the first packet in the list and observe its details, in the following screenshot:
 </p> 
 <img src="https://imgur.com/DvTq6Ex.png" align="center" height="80%" width="80%" alt="Wireshark: TCP traffic details "/>
</div>
<div>
<p> 
 We can gather some information from the subtrees without going into them. For example, the source and destinations of IP addresses and MAC addresses. 
 </p> 
 <p> 
 We’ll now go into the IPv4 subtree and observe the detailed information, shown in the following screenshot:
 </p> 
 <img src="https://imgur.com/Sp13RLl.png" align="center" height="80%" width="80%" alt="Wireshark: IPv4 subtree within the TCP filter"/>
</div>
<div>
 <p>
 Within this IPv4 subtree, you’ll be able to gather key information like the header length, the destination IP address, and the Time to Live (TTL) among other information.
 </p>
 <p>
 Now let’s expand into the Frame subtree and see what information we can identify, shown in the following screenshot:
 </p>
 <img src="https://imgur.com/d8PqeCc.png" align="center" height="80%" width="80%" alt="Wireshark: Expanded Frame subtree "/>
</div>
<div>
 <p>
 You’ll notice the Frame length being 54 bytes and the arrival time of this packet, which includes date, time, and timezone.
 </p>
 <p> 
 Finally, we will filter to select TCP packet data that contains specific text data. Let's filter for TCP packet data that contains “curl”. To do this we will input tcp contains “curl” into the text box. The results are shown in the following screenshot:
 </p> 
 <img src="https://imgur.com/PxNSFSj.png" align="center" height="80%" width="80%" alt="Wireshark: TCP packet data containing -curl "/>
</div>
<div>
 <p>
 Now the list is filtered to contain only packets that have a web request made with the “curl” command.
 </p>
 <h2 align="center">Final thoughts</h2>
 <p>
 This tutorial shows only a fraction of what can be done with a Network Protocol Analyzer like Wireshark. I hope that in providing this written and visual tutorial, you are able to become more confident in your detection and analyzation skills, and possibly become motivated to explore Wireshark on your own. 
 </p>
</div>
