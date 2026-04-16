Week 5: VLAN Configuration and Inter-VLAN Routing

Using Open vSwitch (OVS) in a Virtual Network Environment
This laboratory exercise will provide students with experience using VLANs with inter-VLAN routing on an Open vSwitch (OVS) in a virtualized Linux environment. VLANs are a network technology that allow several individual broadcast domains to exist on a single physical cable or switch; therefore, enterprise networks can have separate communications between different departments, functions, or levels of security without adding additional hardware.

Open vSwitch (OVS) is a multilayer virtual switch designed for use in production and to automate the networking process while also providing support for standard management interfaces and protocols. Its use in data center virtualization and in the context of software-defined networking (SDN) makes it an appropriate choice when developing networking production experiences, so OVS will be utilized throughout the laboratory.

The laboratory will consist of two separate tasks:
1. Configure VLAN tag on individual OVS switch ports and confirm communication exists between hosts in the same VLAN.
2. Configure a Linux router with VLAN sub-interfaces and enable inter-VLAN routing to allow communication from one host in a VLAN to another host in a different VLAN.

The purpose of this lab is to:
•	Develop an understanding of the purpose and concept of VLANs for separating network traffic
•	Using OVS commands, configure the access and trunk ports for VLANs
•	Configure VLAN sub-interfaces on a Linux router and use those interfaces for inter-VLAN routing
•	Validate communication is viable on the network with the use of the ping utility
<img width="940" height="365" alt="image" src="https://github.com/user-attachments/assets/24f09cca-0bff-4d70-8a7e-bdf2a34ceabd" />

 

Task 1: VLAN Configuration on Open vSwitch
Open vSwitch (OVS) is the service used to provide virtual network switches with data transfer capabilities throughout your network infrastructure, allowing seamless communication between physical and virtual machines; therefore, the first step to performing any task related to OVS would be to start the OVS service using 
sh /etc/openvswitch/init.sh
Next step consists of enabling VLAN tagging on the switch interface (eth1) connected to your host computers. A VLAN tag on a switch port sets up that port as an "access" port and will only use that VLAN to carry data traffic from your host computer(s). Specifically, in this task, VLAN tagging has been applied to eth1; VLAN ID 491 will be applied/used on eth1 
ovs-vsctl set port eth1 tag=491

After configuring eth1, use the show command to verify that OVS is functioning properly
ovs-vsctl show
 <img width="940" height="503" alt="image" src="https://github.com/user-attachments/assets/20355afc-7768-4648-8322-bdac45e6e916" />
<img width="613" height="141" alt="image" src="https://github.com/user-attachments/assets/6bdc9b15-dc29-49b0-bb79-3d71558d3177" />

 
Intra-VLAN connectivity can be verified by pinging Host 2 from Host 1. Hosts 1 and 2 are on the same VLAN (VLAN 491); therefore, a successful ping between these hosts indicates that the VLAN 491 is functioning correctly and that intra-VLAN connectivity works properly.

In the virtual network, Hosts 1 through 4 are assigned the same VLAN 491, so the test to ping between all four of these hosts will verify that intra-VLAN connectivity works properly for all hosts in VLAN 491.
 <img width="849" height="266" alt="image" src="https://github.com/user-attachments/assets/0cef45d5-1b7b-460a-adc2-e1322ea68494" />
<img width="940" height="247" alt="image" src="https://github.com/user-attachments/assets/8264b299-4dd7-47d4-b76d-6445b6a32011" />

 
To support this testing, eight successful pings would be the equivalent of eight separate screenshots from Host 1 to Hosts 1 through 4 would demonstrate that all hosts in 491 can communicate with each other with no packet loss.
<img width="781" height="98" alt="image" src="https://github.com/user-attachments/assets/5eff948b-ed43-4ddd-b76d-4ce723227ff3" />

 
Host 1 shows the terminal activity during the ping test; all pings sent by Host 1 received ICMP echo replies from each of the recipients shown.
 <img width="403" height="831" alt="image" src="https://github.com/user-attachments/assets/3b34be05-e046-4b36-9ee6-56346243588a" />


Task 2: VLAN Routing Via Linux Router
<img width="940" height="406" alt="image" src="https://github.com/user-attachments/assets/56589e76-f48d-4b75-bf87-9b3dd5800bab" />

 
The purpose of Task 2 is to allow communication across VLANs using a Linux router. The difference in this task versus the previous task is that the hosts were all communicating within one VLAN in Task 1, but the default configuration for each of the VLANs is isolated from each other. Inter-VLAN routing must be configured in order to allow the hosts in different VLANs to communicate.

First, you must use the command ‘ovs-vsctl set port eth0 trunks=[]’ to set the Open vSwitch (OVS) port (eth0) as a trunk port; this configuration allows the port to carry traffic from multiple VLANs.
ovs-vsctl set port eth0 trunks=[]
Next, you will use the command ‘ip link add’ to create VLAN sub-interfaces for the router where you assign them to VLAN 491 (eth0.491) and VLAN 492 (eth0.492). You will use these sub-interfaces as virtual interfaces for each of the VLANs and configure an assigned IP address (10.10.1.1/24 and 10.10.2.1/24) to act as a default gateway for the VLAN traffic. You will also use the command ‘ip link set eth0.491 up’ and ‘ip link set eth0.492 up’ which will bring the sub-interfaces up.

Commands used in Router:
ip  link add link eth0 name eth0.491 type vlan id 491 
ip  link add link eth0 name eth0.492 type vlan id 492

ip address add 10.10.1.1/24 dev etho.491
ip address add 10.10.2.1/24 dev etho.492

ip link set dev eth0.491 up
ip link set dev eth0.492 up

The switch’s configuration shows that eth0 is carrying both VLANs. Finally, the ping test from Host 1 (VLAN 491) to Host 4 (VLAN 492) is successful and confirms that the router is forwarding traffic between the VLANs.
 <img width="874" height="353" alt="image" src="https://github.com/user-attachments/assets/0af7bd80-5bc6-4f9e-91ac-d54191f25916" />

 <img width="831" height="242" alt="image" src="https://github.com/user-attachments/assets/03c449ab-8924-4ef1-8faf-88ba1c95b5ea" />


Therefore, you have confirmed that the inter-VLAN routing has been configured and is functioning properly.  
The following image shows FileZilla transferring GNS3 packet capture files from a remote Linux server to a local Windows machine.
 <img width="940" height="381" alt="image" src="https://github.com/user-attachments/assets/e00a21ae-d310-4a70-8deb-6f983b983751" />


Conclusions:
This laboratory exercise demonstrated intra-VLAN communication using Open vSwitch and inter-VLAN routing using Linux VLAN sub-interfaces. In Task 1, we configured VLAN 491 on an access port, confirmed that we could communicate with devices within the same VLAN by using to ping them successfully. In Task 2, we configured a Linux router to use VLAN sub-interfaces as the gateways for both VLAN 491 and 492 (eth0.491 and eth0.492). By using pings from hosts in different VLANs, we were able to confirm that we were able to route traffic between two different VLANs across the Linux routing device. Overall, the purpose of this work was to demonstrate how VLAN’s segment networks while routing allows for devices in different segments of the same network to communicate with one another.

Reflections:
From this lab, I gained a lot of knowledge about VLANs, including the distinctions made when a switch port is set as either an access or trunk port. The configuration of trunk ports helped improve my understanding of the function of trunking by allowing me to see, firsthand, how tagged traffic looks. Additionally, I learned that Linux provides a better way to route traffic between VLAN's through their VLAN sub-interfaces and does not require additional hardware like a switch or router. One difficulty I found while completing this lab involved identifying the differences between switch interfaces and router interfaces; therefore, detail observation was required. However, the most important aspect of my experience at this lab was being able to experience working with the different kinds of networking devices present in today’s typical data centre and cloud computing environments.

