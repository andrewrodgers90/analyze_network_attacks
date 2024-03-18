# Cybersecurity Incident Report

### Section 1: Identify the type of attack that may have caused this network interruption

One potential explanation for the website's connection timeout error message is a DoS attack. <br><br> The logs show that the server stops responding after it is flooded with SYN packet requests. <br><br> This event could be a type of DoS attack known as SYN flooding. This does not appear to be a DDoS attack, as the SYN requests are coming from a single IP address.

<br>

### Section 2: Explain how the attack is causing the website to malfunction

When website visitors try to establish a connection with the web server, a three-way handshake occurs using the TCP protocol. The handshake consists of three steps:<br><br>+ A SYN (synchronize) packet is sent from the source to the destination. The purpose of this is to request a connection. <br><br>  + The destination sends a SYN/ACK (synchronization/acknowledgment) packet back to the source to accept the connection request. At this time, the destination will reserve the necessary resources for the source to connect. <br><br>+ Finally, the source sends an ACK (acknowledgment) packet back to the destination, acknowledging it has been granted permission to connect. <br><br> When a malicious actor sends a large number of SYN packets all at once (known as a SYN flood attack), the destination server runs out of space to reserve for connections. At this point, there are no resources left for legitimate TCP connection requests. The logs indicate that the server has been overwhelmed by a large volume of SYN packets, and as a result, is unable to process SYN requests from new visitors. The server cannot establish a connection with new visitors, who receive a connection timeout message. |
