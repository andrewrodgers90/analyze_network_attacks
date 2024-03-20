# Analyze Network Attacks

This exercise is part of the '**Connect and Protect: Networks and Network Security**' module in the '<a href="https://www.coursera.org/google-certificates/cybersecurity-certificate?network=g&utm_source=gg&creativeid=693701665321&matchtype=p&adgroupid=165119487572&gclid=Cj0KCQjwqdqvBhCPARIsANrmZhNXAt_8j18BwKrshjpWbrgJpCQfqPhGyrrYAAGAKKxGWwPNNPP4HwYaAoWqEALw_wcB&keyword=google%20cybersecurity%20professional%20certificate&utm_content=B2C&hide_mobile_promo=&utm_campaign=B2C_APAC_Google_FTCOF_Cybersecurity_Google_Professional_Certificate_ArtE_Set_2_Mar_24&campaignid=21105066676&gad_source=1&devicemodel=&adpostion=&utm_medium=sem&device=c&redirected_from_description_page=true">Google Cybersecurity Professional Certificate</a>'.
<br>

## Task

The purpose of this activity is to identify the likely cause of a service interruption for a company's website following a security issue, and to then explain how the attack occurred and the negative impact it had on the website.

## Scenario

Review the following scenario. Then complete the step-by-step instructions.

You work as a security analyst for a travel agency that advertises sales and promotions on the company’s website. The employees of the company regularly access the company’s sales webpage to search for vacation packages their customers might like. 

One afternoon, you receive an automated alert from your monitoring system indicating a problem with the web server. You attempt to visit the company’s website, but you receive a connection timeout error message in your browser.

You use a packet sniffer to capture data packets in transit to and from the web server. You notice a large number of TCP SYN requests coming from an unfamiliar IP address. The web server appears to be overwhelmed by the volume of incoming traffic and is losing its ability to respond to the abnormally large number of SYN requests. You suspect the server is under attack by a malicious actor. 

You take the server offline temporarily so that the machine can recover and return to a normal operating status. You also configure the company’s firewall to block the IP address that was sending the abnormal number of SYN requests. You know that your IP blocking solution won’t last long, as an attacker can spoof other IP addresses to get around this block. You need to alert your manager about this problem quickly and discuss the next steps to stop this attacker and prevent this problem from happening again. You will need to be prepared to tell your boss about the type of attack you discovered and how it was affecting the web server and employees.

### Step 1: Access supporting materials

+ <a href="https://github.com/andrewrodgers90/analyze_network_attacks/blob/main/how_to_read_a_wireshark_tcp_http_log.md">How to read a Wireshark TCP/HTTP log</a>

### Step 2: Identify the type of attack causing this network interruption

Reflect on the types of network intrusion attacks that you have learned about in this course so far. As a security analyst, identifying the type of network attack based on the incident is the first step to managing the attack and preventing similar attacks in the future. 

Here are some questions to consider when determining what type of attack occurred: 

+ What do you currently understand about network attacks?
+ Which type of attack would likely result in the symptoms described in the scenario?
+ What is the difference between a denial of service (DoS) and distributed denial of service (DDoS)?
+ Why is the website taking a long time to load and reporting a connection timeout error?

Review the Wireshark reading from step 2 and try to identify patterns in the logged network traffic. Analyze the patterns to determine which type of network attack occurred. Write your analysis in section one of the <a href="https://github.com/andrewrodgers90/analyze_network_attacks/blob/main/cybersecurity_incident_report.md">Cybersecurity incident report</a>. 

### Step 3: Explain how the attack is causing the website to malfunction

Review the Wireshark reading from step 2, then write your analysis in section two of the <a href="https://github.com/andrewrodgers90/analyze_network_attacks/blob/main/cybersecurity_incident_report.md">Cybersecurity incident report</a>.

When writing your report, discuss the network devices and activities that are involved in the interruption. Include the following information in your explanation:

+ Describe the attack. What are the main symptoms or characteristics of this specific type of attack?
+ Explain how it affected the organization’s network. How does this specific network attack affect the website and how it functions?
+ Describe the potential consequences of this attack and how it negatively affects the organization.
+ Optional: Suggest potential ways to secure the network so this attack can be prevented in the future.
