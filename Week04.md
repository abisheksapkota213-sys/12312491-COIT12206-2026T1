 
The diagram below represents a simple network that matches the routing and traceroute output information you shared earlier.
<img width="940" height="506" alt="image" src="https://github.com/user-attachments/assets/61a62525-2bf6-4213-a925-4f5db892ebff" />

The network consists of Host1 (10.10.1.101) and Host2 (10.10.1.102) on the left side of the diagram. They connect to Switch1, which means they belong to the same local area network (LAN), specifically 10.10.1.0/24, thus, they can talk directly to each other over the switch without using their router.

Switch1 connects to Router1 through the eth0 (10.10.1.1) interface. The eth0 interface is the default gateway for both Host1 and Host2, so if either host wants to communicate with a different network, it will send its traffic to Router1.

On the right side of the diagram,  Router1 is connected to another network via the eth1 (10.10.2.1) interface. Host3 is connected to this network and has an IP address of 10.10.2.101. This network belongs to the 10.10.2.0/24 range.

To tie this back to your previous outputs:

 In traceroute, the first hop was 10.10.1.1, which is Router1 (correct).
From that point forward, the router uses OSPF to route to other networks, as we discussed above.
This entire diagram represents the first segment of a larger OSPF network:

Key Concept:

 Switch = Layer 2 device (direct communication within same network)
 Router = Layer 3 device (connects different networks)
 Router1 is the bridge between the 10.10.1.0 and other networks like 10.10.2.0 and more.

If you don't understand this clearly, you're going to struggle with OSPF because this is the foundation/base layer: hosts → switch → router → other networks.
1.	Network configuration for host 1:
 <img width="680" height="291" alt="image" src="https://github.com/user-attachments/assets/b55cb01f-58a0-4e3d-bd99-2a0038665523" />

2.	Network configuration for host 2:
 

<img width="720" height="284" alt="image" src="https://github.com/user-attachments/assets/a5bf00d5-24fa-4b76-81a1-a29f0e50d71e" />



3.	Network configuration for host Router eth0 and eth 1:
 <img width="655" height="273" alt="image" src="https://github.com/user-attachments/assets/5a42964e-75ea-457d-bf02-e4cea93c181d" />

<img width="667" height="292" alt="image" src="https://github.com/user-attachments/assets/9cc37f7c-91c1-4715-a0b0-1a6ce4616126" />

 
4.	Network configuration for host 3:
 

<img width="759" height="303" alt="image" src="https://github.com/user-attachments/assets/be43b80b-2616-439c-8155-57c939903e55" />







Pinging host 3 from host 1(different network):
 <img width="759" height="303" alt="image" src="https://github.com/user-attachments/assets/6ee1e70d-f893-4529-86e1-b49e72c4b1aa" />

here i used 'ping' command for pinging another host in diffrent subnet.
Host 1:
 <img width="911" height="184" alt="image" src="https://github.com/user-attachments/assets/de088b39-6aa1-46f5-8a14-14ca37462a06" />

Source	 Destination 	Next route	Interface
10.10.1.101	10.10.1.0/24	Direct	Eth0
10.10.1.101	any	10.10.1.1	Eth0
			



Router:
 <img width="940" height="271" alt="image" src="https://github.com/user-attachments/assets/bd3c0da8-b449-40c8-b826-c57e41f8612e" />
Here i used ip route show to display the source and destination while sending packet.

 Destination 	Next route	Interface
10.10.1.0/24	direct	Eth0
10.10.2.0/24	direct	Eth1






TASK 2

Frr1: On this router's Operating System for Shortest Path (OSPF) status, both the show commands for OSPF existing neighbor relationships via ip and route command via ip show routers have returned no errors with all relationships being established between the neighbours (interface or systems). The Routers IDs 10.10.4.2 & 10.10.5.3 both show full connectivity as they reached full connection with each other. One system has been designated to be the designated router (DR), and the other has been selected to be the backup router to ensure maximum efficiency works between these routers with multiple access points on the same multiaccess network.

The OSPF route portion of the output shows the routing tables of OSPF networks located directly connected to this router (10.10.2.3 and 10.10.1.22 & eth2) and routing tables containing OSPF learned from other routers (eg. 10.10/4/4.25 DFS Net); thus indicating efficiently learned routers between router and 10.10.3.3 due to multiple routing methods (10.10.4.0 and 10.10.5.0).

Finally, the output of "ip route" from this router confirms the existence of all routes present in the routing table with code indicating the type of route (ie. C for directly connected, O for OSPF) therefore demonstrating a fully functional OSPF network with all neighbour relationships stable and fully functional as intended by OSPF.
 <img width="940" height="955" alt="image" src="https://github.com/user-attachments/assets/e1d4f663-a588-4a62-b7f6-31844b3b33c0" />

Interface	Local Network	Neighbor Router ID	Neighbor IP	Role	Learned Networks
eth0	10.10.1.0/24	—	—	Direct	Local network only
eth1	10.10.2.0/24	10.10.4.2	10.10.2.2	DR	10.10.4.0, 10.10.6.0
eth2	10.10.3.0/24	10.10.5.3	10.10.3.3	Backup DR	10.10.5.0, 10.10.6.0


Traceroute host 2 from host 1
This traceroute results indicate the route taken by packets sent from source address 10.10.6.102 (destination) through at least four routers/hops (with the first hop being a local gateway or router). The first hop (10.10.1.1) is the first router the packet went through; this is typically your own organization’s router connected directly to your LAN. After this, the packet continues to the next hop (10.10.3.3), which matches an OSPF/specified router that is connected on the eth2 interface. The third hop is 10.10.4.4, which represents another router that resides further down the nest. Finally, packets will eventually arrive at 10.10.6.102.

Packets traveling through each hop are reported using three time values (in milliseconds) specifying how long it will take a packet to travel from its originating location through all of the respective routers back to its originating location. These values are representative of normal variations in network delays; however, the routing table, in a previous activity under ECMP, well exhibit two different calculated paths (via both eth1 and eth2) that can be taken to reach destination(s).

In summary, the routing diagram validates that routing is functioning about as expected and that the packets have arrived at their matched destination address(es).

 <img width="940" height="182" alt="image" src="https://github.com/user-attachments/assets/24511291-df7e-40a0-9f06-e98a1a437175" />


Hop	IP Address	Meaning
1	10.10.1.1	First gateway (your local router interface)
2	10.10.3.3	Second router (neighbor via eth2)
3	10.10.4.4	Next router deeper in the network
4	10.10.6.102	Final destination


Conclusion    
 This project illustrates an appropriately designed and well-functioning network with both basic LAN communications using OSPF (Open Shortest Path First) as well as dynamic routing functionality. The topology depicted shows an obvious delineation between Layer 2 and Layer 3 functions, whereby hosts on the same subnet communicate with one another via a switch while communication between different subnets is routed through a router.

The OSPF configuration within the router is stable and operationally functional, as corroborated by neighbor routers reaching FULL state and successfully electing a Designated Router (DR) and Backup DR. In addition, the router's routing table indicates that the router has successfully learned about both directly connected and remote subnets. Furthermore, there are multiple routes available for all routing destinations on the router, indicating the presence of ECMP routing, which provides load balancing on the network as well as fault tolerance.

Traceroute output corroborates that packets are actually forwarded via the correct routing decisions and not just being routed based on routing tables or configuration files. In conclusion, the network delivers dependable data communications, efficient data routing, and scalability because of OSPF.


Reflection

It was demonstrated in this project how much more important traffic flow comprehension is when compared to memorizing routing command syntax. Creating an understanding of how routing tables, OSPF, and the traceroute command work together allows a mental model to come together that connects the dots between them all. Additionally, discovering that multiple paths exist within a single session; however, only one path will be present at a time can prove to be confusing.

