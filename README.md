# Cybersecurity Incident Report: Network Traffic Analysis

> [!NOTE]
> This exercise is a component of the [Google Cybersecurity Professional Certificate](https://www.coursera.org/professional-certificates/google-cybersecurity) program. It's designed as a simulated scenario to solidify my understanding of Network Analysis.

## Activity Overview
In this activity, you will analyze DNS and ICMP traffic in transit using data from a network protocol analyzer tool. You will identify which network protocol was utilized in assessment of the cybersecurity incident. 

In the internet layer of the TCP/IP model, the IP formats data packets into IP datagrams. The information provided in the datagram of an IP packet can provide security analysts with insight into suspicious data packets in transit.

Knowing how to identify potentially malicious traffic on a network can help cybersecurity analysts assess security risks on a network and reinforce network security.

## Scenario
You are a cybersecurity analyst working at a company that specializes in providing IT services for clients. Several customers of clients reported that they were not able to access the client company website ´www.yummyrecipesforme.com´, and saw the error “destination port unreachable” after waiting for the page to load. 

You are tasked with analyzing the situation and determining which network protocol was affected during this incident. To start, you attempt to visit the website and you also receive the error “destination port unreachable.” To troubleshoot the issue, you load your network analyzer tool, tcpdump, and attempt to load the webpage again. To load the webpage, your browser sends a query to a DNS server via the UDP protocol to retrieve the IP address for the website's domain name; this is part of the DNS protocol. Your browser then uses this IP address as the destination IP for sending an HTTPS request to the web server to display the webpage  The analyzer shows that when you send UDP packets to the DNS server, you receive ICMP packets containing the error message: “udp port 53 unreachable.” 

![image](https://github.com/user-attachments/assets/394f597c-697d-477f-96dd-61f7dbf517fe)

# Report
### Cybersecurity Incident Report: Network Traffic Analysis

| Part 1: Provide a summary of the problem found in the DNS and ICMP traffic log. | 
|-------------------------------------------------------------------------------- |
|The UDP protocol reveals that the UDP is not establishing a persistent connection between the requester and the receiver server. Each packet is sent independently without prior negotiation (handshake). This is based on the results of the network analysis, which show that the ICMP echo reply returned the error message: “udp port 53 unreachable.” The port noted in the error message is used for the Domain Name System (DNS) protocol, which translates domain names into IP addresses. The most likely issue is that there is a problem with the Domain Name System server because the "port unreachable" error indicates that the DNS server is not responding on port 53.|

| Part 2: Explain your analysis of the data and provide at least one cause of the incident. | 
|-------------------------------------------------------------------------------------------|
|The IT team became aware of the incident because several customers complained about not being able to access the website. This occurred around 1:24 p.m, the time the analysis began with the tcpdump tool.  An IT team member attempted to access the website  and also encountered the "destination port unreachable" error, confirming the issue. Then, the tcpdump tool was used to capture packets while attempting to access the website. The tcpdump log was analyzed to identify the patterns, protocols used, and error messages. The key finding was the "udp port 53 unreachable" error message, indicating that the DNS server was not responding on the standard DNS port (port 53). The investigation also confirmed the involvement of the UDP protocol for DNS queries and the ICMP protocol for error reporting. Some likely causes of the incident involve problems with the DNS server, such as server downtime (malfunction), misconfiguration (not responding on port 53), or a firewall that might be blocking UDP traffic on port 53. A DoS attack is also considered a possible cause. To confirm this, it is recommended to deeply analyze server logs and perform a vulnerability scan.|



