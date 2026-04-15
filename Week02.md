Week 2: Setting IP Addresses and testing network connectivity

Introduction:
The demonstration will teach us how to establish a fixed/static IP address for a Linux machine and to test network connectivity using the ping command through three different methods. The demonstration is conducted using GNS3 software with a switch connecting four Linux computers together.

Task 1: Network topology
This network consist of 
-	4 Linux Hosts
-	1 Ethernet Switch
And form a single LAN. 
 <img width="940" height="680" alt="image" src="https://github.com/user-attachments/assets/51c4ca32-e98b-45a6-8539-a803c62bf852" />

Ip address were assigned according to this table:
HOST	IP Address
Host 1	10.10.1.1
Host 2	10.10.1.2
Host 3	10.10.1.3
Host 4	10.10.1.4
We tried 3 different method to configure these nodes, for host 1 and host 2 we used GNS3 GUI configuration panel. These settings are automatically applied when the nodes start.  Secondly for host 3 , we used  nono /etc/network/interfaces , this command helps us to chande network configuration using web console, and for the last host (host 4 ) we used  some commands lines ie.
ip address add 10.10.1.4/24 dev eth0
and for verification we used ip address show 
 
 <img width="581" height="384" alt="image" src="https://github.com/user-attachments/assets/67966714-0919-4efb-ae2b-3015095a9752" />

Host 4:
 <img width="940" height="193" alt="image" src="https://github.com/user-attachments/assets/fdd38248-d98d-4830-a0cf-50366f2753c8" />



Task 2: Testing Network Connectivity 
For basic ping we use ping command, and to control the data flow we use different additionlal commands such as 
Option 	Function	Example
-c	Control Count	Ping -c 10.10.1.1
-i	Control interval	Ping -2 10.10.1.1
-s	Control packet size	Ping -s 10.10.1.1

	Pinging each hosts :
 Pinging host 1,2,3 from host 4 
 <img width="580" height="564" alt="image" src="https://github.com/user-attachments/assets/5961c5ad-7abf-437c-b2a4-40627b8cb85e" />


Changing size, count while pinging:
 <img width="902" height="313" alt="image" src="https://github.com/user-attachments/assets/30b47d42-45e9-4bde-acf0-7a6a9d3f8130" />

Out of 5 sent packets, there was a full delivery of these packets to IP address 10.10.1.1 with a 100% success rate. All evidence points to an effective operational state on the network, with performance consistently reliable. All packets took between 10.6 ms and 2.4 ms to transmit to the selected destination; therefore, this indicates that the connections between devices on the network are sufficiently rapid to suffice for optimal performance and that 10.6 ms is an acceptable amount of time to send packets. As a result, it can be reasonably expected that the present level of performance will continue from the network.





Conclusion: 
This lab exercise successfully demonstrated:
•	Three different method to assign IP address in Lunix. 
•	Use of ping to verify connectivity between all hosts  and network performance 
•	Differences between persistent and temporary configurations



	



