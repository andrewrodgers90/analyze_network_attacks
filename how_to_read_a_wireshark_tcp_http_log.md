# How To Read a Wireshark TCP/HTTP Log

In this reading, you’ll learn how to read a Wireshark TCP/HTTP log for network traffic between employee website visitors and the company’s web server. Most network protocol/traffic analyzer tools used to capture packets will provide this same information.
<br>
### Log entry number and time

| No. | Time |
|-----|----------|
| 47  | 3.144521 |
| 48  | 3.195755 |
| 49  | 3.246989 |


This Wireshark TCP log section provided to you starts at log entry number (No.) 47, which is three seconds and .144521 milliseconds after the logging tool started recording. This indicates that approximately 47 messages were sent and received by the web server in the 3.1 seconds after starting the log. This rapid traffic speed is why the tool tracks time in milliseconds. 

### Source and destination IP addresses

| Source | Destination |
|--------|-------------|
| 198.51.100.23 | 192.0.2.1 |
| 192.0.2.1     | 198.51.100.23 |
| 198.51.100.23 | 192.0.2.1 |


The source and destination columns contain the source IP address of the machine that is sending a packet and the intended destination IP address of the packet. In this log file, the IP address 192.0.2.1 belongs to the company’s web server. The range of IP addresses in 198.51.100.0/24 belong to the employees’ computers. 

### Protocol type and related information

| Protocol | Info |
|----------|------|
| TCP | 42584->443 [SYN] Seq=0 Win-5792 Len=120... |
| TCP | 443->42584 [SYN, ACK] Seq=0 Win-5792 Len=120... |
| TCP |42584->443 [ACK] Seq=1 Win-5792 Len=120... |


The Protocol column indicates that the packets are being sent using the TCP protocol, which is at the transport layer of the TCP/IP model. In the given log file, you will notice that the protocol will eventually change to HTTP, at the application layer, once the connection to the web server is successfully established.

The Info column provides information about the packet. It lists the source port followed by an arrow → pointing to the destination port. In this case, port 443 belongs to the web server. Port 443 is normally used for encrypted web traffic.

The next data element given in the Info column is part of the three-way handshake process to establish a connection between two machines. In this case, employees are trying to connect to the company’s web server: 

+ The [SYN] packet is the initial request from an employee visitor trying to connect to a web page hosted on the web server. SYN stands for “synchronize.” 
+ The [SYN, ACK] packet is the web server’s response to the visitor’s request agreeing to the connection. The server will reserve system resources for the final step of the handshake. SYN, ACK stands for “synchronize acknowledge.”
+ The [ACK] packet is the visitor’s machine acknowledging the permission to connect. This is the final step required to make a successful TCP connection. ACK stands for “acknowledge.”

The next few items in the Info column provide more details about the packets. However, this data is not needed to complete this activity. If you would like to learn more about packet properties, please visit Microsoft’s Introduction to Network Trace Analysis.  

### Normal website traffic

A normal transaction between a website visitor and the web server would be like:

| No. | Time | Source | Destination | Protocol | Info |
|-----|------|--------|-------------|----------|------|
| 47 | 3.144521 | 198.51.100.23 | 192.0.2.1 | TCP | 42584->443 [SYN] Seq=0 Win=5792 Len=120... |
| 48 | 3.195755 | 192.0.2.1 | 198.51.100.23 | TCP | 443->42584 [SYN, ACK] Seq=0 Win-5792 Len=120... |
| 49 | 3.246989 | 198.51.100.23 | 192.0.2.1 | TCP | 42584->443 [ACK] Seq=1 Win-5792 Len=120... |
| 50 | 3.298223 | 198.51.100.23 | 192.0.2.1 | HTTP | GET /sales.html HTTP/1.1 |
| 51 | 3.349457 | 192.0.2.1 | 198.51.100.23 | HTTP | HTTP/1.1 200 OK (text/html) |


Notice that the handshake process takes a few milliseconds to complete. Then, you can identify the employee’s browser requesting the sales.html webpage using the HTTP protocol at the application level of the TCP/IP model. Followed by the web server responding to the request.

### The Attack

As you learned previously, malicious actors can take advantage of the TCP protocol by flooding a server with SYN packet requests for the first part of the handshake. However, if the number of SYN requests is greater than the server resources available to handle the requests, then the server will become overwhelmed and unable to respond to the requests. This is a network level denial of service (DoS) attack, called a SYN flood attack, that targets network bandwidth to slow traffic. A SYN flood attack simulates a TCP connection and floods the server with SYN packets. A DoS direct attack originates from a single source. A distributed denial of service (DDoS) attack comes from multiple sources, often in different locations, making it more difficult to identify the attacker or attackers. 

![img_1](https://github.com/andrewrodgers90/analyze_network_attacks/assets/132149730/71077b96-f282-4f6b-9289-b53768422144)

There are two tabs at the bottom of the log file. One is labeled “Color coded TCP log.” If you click on that tab, you will find the server interactions with the attacker’s IP address (203.0.113.0) marked with red highlighting (and the word “red” in column A).

![img_3](https://github.com/andrewrodgers90/analyze_network_attacks/assets/132149730/6d677ac8-e3d9-4f9e-840a-88cf55c1edd6)
![img_2](https://github.com/andrewrodgers90/analyze_network_attacks/assets/132149730/f9724ba6-d709-4819-9e14-42d5c83a47ed)

Initially, the attacker’s SYN request is answered normally by the web server (log items 52-54). However, the attacker keeps sending more SYN requests, which is abnormal. At this point, the web server is still able to respond to normal visitor traffic, which is highlighted and labeled as green. An employee visitor with the IP address of 198.51.100.14 successfully completes a SYN/ACK connection handshake with the webserver (log item nos. 55, 56, 58). Then, the employee’s browser requests the sales.html webpage with the GET command and the web server responds (log item no. 60 and 62).

![img_4](https://github.com/andrewrodgers90/analyze_network_attacks/assets/132149730/5253684f-526f-4971-ae28-44d5dcb466bd)
![img_5](https://github.com/andrewrodgers90/analyze_network_attacks/assets/132149730/ed1daba2-c8d6-429a-9b06-06f209510f94)
![img_6](https://github.com/andrewrodgers90/analyze_network_attacks/assets/132149730/a65570e0-a53f-4836-927e-cfdcb9a638ee)

In the next 20 rows, the log begins to reflect the struggle the web server is having to keep up with the abnormal number of SYN requests coming in at a rapid pace. The attacker is sending several SYN requests every second. The rows highlighted and labeled yellow are failed communications between legitimate employee website visitors and the web server.

The two types of errors in the logs include:

+ An HTTP/1.1 504 Gateway Time-out (text/html) error message. This message is generated by a gateway server that was waiting for a response from the web server. If the web server takes too long to respond, the gateway server will send a timeout error message to the requesting browser.
+ An [RST, ACK] packet, which would be sent to the requesting visitor if the [SYN, ACK] packet is not received by the web server. RST stands for reset, acknowledge. The visitor will receive a timeout error message in their browser and the connection attempt is dropped. The visitor can refresh their browser to attempt to send a new SYN request.

![img_7](https://github.com/andrewrodgers90/analyze_network_attacks/assets/132149730/ac64d9e7-2362-412d-b477-0e249fa70cef)
![img_8](https://github.com/andrewrodgers90/analyze_network_attacks/assets/132149730/ca145b55-2d63-4dbd-afdf-49f96dc6275d)
![img_9](https://github.com/andrewrodgers90/analyze_network_attacks/assets/132149730/70af90b2-e8d4-4edb-9dc1-771f7fdf6220)
![img_10](https://github.com/andrewrodgers90/analyze_network_attacks/assets/132149730/1aea0791-9922-45df-956c-1fa1328c0091)

As you scroll through the rest of the log, you will notice the web server stops responding to  legitimate employee visitor traffic. The visitors receive more error messages indicating that they cannot establish or maintain a connection to the web server. From log item number 125 on, the web server stops responding. The only items logged at that point are from the attack. As there is only one IP address attacking the web server, you can assume this is a direct DoS SYN flood attack.
