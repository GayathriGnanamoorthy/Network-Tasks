# Network Port Scanning Report

## Task 1: Scan Your Local Network for Open Ports

### Steps Performed
1. Installed Nmap from official website
   - Version: 7.94
![image](https://github.com/user-attachments/assets/098fa8b5-8903-4e49-8fc6-1ae3878dda0c)

2. Found local IP range
   - 10.0.2.10/24
![image](https://github.com/user-attachments/assets/6d2d25c0-5f71-496b-8b0b-e51b72eda54d)

3. Executed TCP SYN scan command
   - `nmap -sS 192.168.1.0/24`
![image](https://github.com/user-attachments/assets/8e106ff9-66e1-43e7-9399-8da68dbb4410)

4. Documented findings:

| IP Address | Open Ports | Services Identified |
|------------|------------|---------------------|
| 10.0.2.1   | 53         | Domain Name System |
| 10.0.2.2   | 445, 135   | Microsoft ds, msrpc |
| 10.0.2.3   | -          | -                   |
| 10.0.2.10  | -          | -                   |

5. Optional: Packet capture analysis with Wireshark
![image](https://github.com/user-attachments/assets/a610ae85-ecf4-46c5-a1cf-ac3b56783d59)

6. Researched common services on found ports:
   - 53: Domain Name System
   - 135: msrpc
   - 445: Microsoft ds
7. Identified security risks:
   - Port 53: DNS Amplification, poisoning/spoofing, Information leakage, Tunneling
   - Port 135: Blast worm, remote code execution
   - Port 445: Eternal blue, relay attack (pass-the-hash)

## Questions & Answers

### 1. What is an open port?
An open port is a communication endpoint on a computer or network device that is actively accepting connections. It indicates that a service or application is running on that port and listening for incoming network traffic. Open ports are necessary for networked services, but they can also expose systems to external threats if not properly secured.

### 2. How does Nmap perform a TCP SYN scan?
Nmap performs a TCP SYN scan by sending a SYN (synchronize) packet to a target port and analyzing the response. If the port is open, the target responds with a SYN-ACK packet. Instead of completing the handshake, Nmap sends a RST (reset) packet to avoid making a full connection, which makes this type of scan stealthier and less likely to be logged by the target system. If the port is closed, the target responds with a RST packet. If no response or an ICMP unreachable message is received, the port may be filtered by a firewall.

### 3. What risks are associated with open ports?
Open ports can introduce various security risks, especially if they are associated with unpatched or poorly configured services. Attackers may exploit these ports to gain unauthorized access, perform brute-force attacks, deliver malware, or gather information about the system. Services exposed through open ports can also be used for lateral movement within a network or as entry points for ransomware and botnets.

### 4. Explain the difference between TCP and UDP scanning
TCP and UDP scanning differ primarily in how they communicate. TCP scanning relies on the handshake mechanism and provides more reliable feedback, as it clearly indicates whether a port is open, closed, or filtered. In contrast, UDP scanning does not establish a connection, making it harder to detect open ports, especially when firewalls silently drop packets. UDP scans may produce fewer responses, making them slower and more difficult to interpret, but they are crucial for identifying services like DNS, SNMP, and TFTP that operate over UDP.

### 5. How can open ports be secured?
To secure open ports, it is important to first identify and close any ports that are not needed for business or operational purposes. Firewalls should be configured to restrict access to essential ports only, preferably allowing traffic from specific IP addresses. Services running on open ports should be regularly updated and monitored for vulnerabilities. Additionally, techniques like port knocking or VPN access can help limit exposure by hiding services from unauthorized users.

### 6. What is a firewall's role regarding ports?
A firewall acts as a gatekeeper that filters network traffic based on predetermined security rules. It controls which ports can send or receive data, effectively blocking unauthorized access to services. Firewalls can prevent port scans, limit the attack surface, and log suspicious activities, making them a critical component in network security. By selectively allowing or denying traffic on certain ports, firewalls help enforce security policies and reduce the risk of exploitation.

### 7. What is a port scan and why do attackers perform it?
A port scan is a technique used to identify open, closed, or filtered ports on a target system. It provides insight into which services are running and potentially exploitable. Attackers perform port scans during the reconnaissance phase of a cyberattack to map the network, find vulnerable services, and gather information that can be used for more targeted attacks. It is often the first step in identifying weaknesses within a network.

### 8. How does Wireshark complement port scanning?
Wireshark is a network protocol analyzer that captures and inspects packets in real time. When used alongside port scanning, it allows security analysts to observe the actual packet exchange between the scanner and the target. This helps in understanding how the scan operates, verifying the responses received, and identifying patterns or anomalies. It also provides valuable insights for detecting unauthorized scanning activity on a network.



## Tools Used
- Nmap 7.94
- Wireshark (optional)
