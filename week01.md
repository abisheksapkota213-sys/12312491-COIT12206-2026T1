








Lab Report
Course: COIT12206: TCP/IP Principles and Protocols
Date: 10 March 2026
Student Name: Abishek Sapkota
Student ID: 12312491










1.	Aim:
The purpose of this lab exercise is to learn about the GNS3 Network Simulation Tool. A Project will be created. Static IP addresses will be assigned to Linux nodes. Nodes will be started and stopped using the web console. Connectivity between hosts will be verified with Linux Network Commands.

2.	Introduction:
GNS3 (Graphical Network Simulator-3) allows you to design and test computer networks simulate software without any physical equipment or devices. With GNS3, you can create simulations involving routers, switches, and hosts to better understand how networks work.

On this lab exercise, we created two Linux hosts that were added to a GNS3 topology with static IP addresses set through the configuration file "/etc/network/interfaces". After we configured the nodes, they were powered up and we used Linux commands to verify their respective IP addresses. Lastly, we tested the connectivity between the two hosts using the command ‘ping’.

3.	Equipment / Software:
-	GNS3
-	Linux host nodes in GNS3
-	Web console (terminal)
-	Basic Linux networking commands

4.	Procedure:
i.	Create  a local server using ‘oracle virtual box
ii.	Run ip address given by that local server in browser 
iii.	It will run GNS3 
iv.	Create a new project in GNS3 with name ‘ GNS#-Intro-12312491’
v.	Add 2 Linux host and assign IP Address 10.10.0.11 and 10.10.0.12 for hist 12 and host 2 respectively. 
The command we used is:
auto eth0
iface eth0 inet static
	address 10.10.0.11  
	netmask 255.255.255.0
up sysctl net ipv4 in_forward
 

For host 2 all commands are same but the ip address is 10.10.0.12

Host	IP address	 Netmark
Host 1 	10.10.0.11	255.255.255.0
Host 2 	10.10.0.12	255.255.255.0


 
 


vi.	Start nodes
vii.	Web console was opened for each host to intract with the Linux terminal
viii.	Verify IP Address by simply using command ‘ ip address show’
 
ix.	To test connectivity the ‘ping’ command was used.


5.	Discussion:
The lab demonstrated that we could configure network configurations in a Linux environment using static IP addresses through GNS3 by editing the /etc/network/interfaces file directly.

By entering the ‘ping’ command from each host, we verified that both hosts successfully communicated over the network by receiving an acknowledgement back from the other host.

6.	Conclusion:
The lab was designed to teach some of the fundamental operations of GNS3 by providing hands-on experience in all aspects of basic lab function such as:
-	creating a new GNS3 project
-	how to be able to configure the GNS3 node
-	assigning a static IP to a node
-	testing the connectivity of nodes.

The labs provided students the opportunity to learn about configuration and verification of communication between two hosts on a simulated network.








	



<img width="1383" height="685" alt="Screenshot 2026-03-15 171834" src="https://github.com/user-attachments/assets/9205645c-cb0d-4bf5-b0bf-98cb48ed6de3" />
