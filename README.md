# Task4_elevatelabs

This README provides a detailed explanation of the steps involved in setting up and using a firewall on Windows or Linux, as part of the Elevate Labs Cyber Security Internship Task 4.
     
     Task 4: Setup and Use a Firewall on Windows/Linux

Objective: Configure and test basic firewall rules to allow or block traffic.
Tools: Windows Firewall (for Windows) / UFW (Uncomplicated Firewall) (for Linux).
Deliverables: Screenshot/configuration file showing firewall rules applied.
###    Understanding Firewalls and Their Importance
A firewall acts as a security guard for your network, monitoring incoming and outgoing network traffic and deciding whether to allow or block specific traffic based on a defined set of security rules. It's a crucial component in improving network security by preventing unauthorized access and protecting your system from various cyber threats.
### Key Concepts:
 * Ports: Virtual points where network connections start and end. Different applications and services use specific ports (e.g., HTTP uses port 80, SSH uses port 22).
 * Inbound Rules: Control traffic entering your system.
 * Outbound Rules: Control traffic leaving your system.
 * Stateful vs. Stateless Firewalls:
   * Stateless firewalls filter traffic based purely on static rules, without considering the context of the connection. They treat each packet individually.
   * Stateful firewalls are more advanced; they keep track of the state of active connections and can make more intelligent decisions based on the context of the traffic. This means if you initiate an outbound connection, the stateful firewall will automatically allow the return inbound traffic for that established connection.

Step-by-Step Guide for Firewall Configuration
This guide covers both Windows Firewall and UFW on Linux. Choose the section relevant to your operating system.
Option 1: Windows Firewall
 * Open Firewall Configuration Tool:
   * Search for "Windows Defender Firewall with Advanced Security" in the Windows search bar and open it. This provides more granular control than the standard Windows Firewall settings.
 * List Current Firewall Rules:
   * In the "Windows Defender Firewall with Advanced Security" window, navigate to "Inbound Rules" or "Outbound Rules" in the left-hand pane to view the existing rules.
   * Screenshot/Configuration File: Take a screenshot of the "Inbound Rules" section to show the initial state.
 * Add a Rule to Block Inbound Traffic on a Specific Port (e.g., Port 23 for Telnet):
   * Telnet (port 23) is often blocked due to its unencrypted nature, making it a security risk.
   * In the "Windows Defender Firewall with Advanced Security" window, right-click on "Inbound Rules" and select "New Rule...".
   * Choose "Port" and click "Next."
   * Select "Specific local ports" and enter 23. Click "Next."
   * Select "Block the connection." Click "Next."
   * Choose when the rule applies (Domain, Private, Public). For a general block, you might select all three. Click "Next."
   * Give the rule a name (e.g., "Block Telnet Inbound") and an optional description. Click "Finish."
   * Screenshot/Configuration File: Take a screenshot of the newly created rule in the "Inbound Rules" list.
     ![Screenshot 2025-06-27 191557](https://github.com/user-attachments/assets/27019ac7-0eb6-4ae5-9411-00ed5683e117)
     ![Screenshot 2025-06-27 191722](https://github.com/user-attachments/assets/7f95cb7c-8a39-48d2-8a5d-baa4a46cb33a)
     ![Screenshot 2025-06-27 191747](https://github.com/user-attachments/assets/13239e83-e522-489a-a873-253441cf8874)
     ![Screenshot 2025-06-27 192123](https://github.com/user-attachments/assets/40beef1b-c259-4b48-988a-0c9faa2142ab)

![Screenshot 2025-06-27 192402](https://github.com/user-attachments/assets/2c2ba43e-125f-4548-bc6d-b1a695a430a2)
![Screenshot 2025-06-27 192449](https://github.com/user-attachments/assets/5d7d3487-6eb3-4e25-942b-fc1694f68ec4)

![Screenshot 2025-06-27 192545](https://github.com/user-attachments/assets/cfb4c0bb-1a45-4b26-867b-c140e49d72bf)
![Screenshot 2025-06-27 192646](https://github.com/user-attachments/assets/8e28d1ea-fd04-4bac-91a4-fd9f4d3adf07)
![Screenshot 2025-06-27 192724](https://github.com/user-attachments/assets/c6ca16ff-04b5-4035-8188-0dad5a455a8a)

   * Test the Rule by Attempting to Connect to that Port Locally or Remotely:
   * You can use the telnet client (you might need to enable it via "Turn Windows features on or off") or a network utility like nmap if you have it installed.
   * Using telnet (if enabled): Open Command Prompt and type telnet localhost 23. If the rule is working, the connection should be refused or time out.
   * Using Test-NetConnection in PowerShell: Open PowerShell and type Test-NetConnection -ComputerName localhost -Port 23. Look for TcpTestSucceeded : False.
   * Screenshot/Configuration File: Take a screenshot of the command prompt/PowerShell output showing the failed connection attempt.
![Screenshot 2025-06-27 193132](https://github.com/user-attachments/assets/0f914ef9-9b88-45b1-be38-b5c2a10efbca)
![Screenshot 2025-06-27 191354](https://github.com/user-attachments/assets/799351f4-e01b-49f6-ab10-cecbd101b2b5)

    * Remove the Test Block Rule to Restore Original State:
   * Go back to "Windows Defender Firewall with Advanced Security," navigate to "Inbound Rules," find the "Block Telnet Inbound" rule you created, right-click it, and select "Delete"
   * Document Commands or GUI Steps Used:
   * Include the specific steps and menu navigation you followed in your documentation (as provided in this README).

Option 2: UFW (Uncomplicated Firewall) on Linux
 * Open Firewall Configuration Tool (Terminal):
   * Open your terminal.
   * UFW is designed to simplify firewall management on Linux.
 * List Current Firewall Rules:
   * To check the status of UFW and list current rules, type:
     sudo ufw status verbose

     
   * Add a Rule to Block Inbound Traffic on a Specific Port (e.g., Port 23 for Telnet):
   * To block incoming connections on port 23 (Telnet), use the command:
     sudo ufw deny 23/tcp

    * Test the Rule by Attempting to Connect to that Port Locally or Remotely:
   * You can use netcat (often abbreviated as nc) to attempt a connection.
   * To test locally:
     nc -zv localhost 23

     You should see "Connection refused" or similar, indicating the block.
     
   * Add Rule to Allow SSH (Port 22):
   * If you are managing your Linux machine remotely via SSH, it's crucial to allow SSH traffic before enabling UFW or after blocking other ports, otherwise you might lock yourself out.
   * To allow incoming SSH connections on port 22:
     sudo ufw allow 22/tcp
     
   * Remove the Test Block Rule to Restore Original State:
   * To delete the rule blocking port 23, first list the rules with numbers:
     sudo ufw status numbered

   * Identify the number corresponding to the "DENY 23/tcp" rule. Let's say it's X. Then delete it:
     sudo ufw delete X

   * Alternatively, you can delete by rule content:
     sudo ufw delete deny 23/tcp

### Summarizing How a Firewall Filters Traffic
    A firewall filters traffic by examining network packets against a set of predefined rules. These rules dictate whether a packet should be allowed to pass through, blocked, or dropped. The filtering process typically involves checking:
 * Source IP Address: Where the traffic is coming from.
 * Destination IP Address: Where the traffic is going.
 * Source Port: The port on the originating machine.
 * Destination Port: The port on the target machine.
 * Protocol: The type of communication (e.g., TCP, UDP, ICMP).
 * State of the connection: (for stateful firewalls) whether the packet is part of an established, related, or new connection.
When a packet arrives at the firewall, it is compared against the rules in order. The first rule that matches the packet's characteristics is applied, and the corresponding action (allow, deny, or drop) is taken.

### Common Firewall Mistakes
 * Not enabling the firewall: Leaving the firewall disabled exposes the system to various threats.
 * Overly permissive rules: Allowing too much traffic can defeat the purpose of a firewall.
 * Blocking essential services: Accidentally blocking necessary ports can disrupt legitimate operations (e.g., blocking SSH on a remote server).
 * Not regularly updating rules: As network needs change, firewall rules should be reviewed and updated to maintain optimal security and functionality.
 * Poor logging and monitoring: Not monitoring firewall logs can lead to missed security events.

#### Interview questions based on the provided document:
 * What is a firewall?
   A firewall filters network traffic. It is a tool used to configure and test basic firewall rules to allow or block traffic.
 * Difference between stateful and stateless firewall?
   The provided document does not contain information to answer this question.
 * What are inbound and outbound rules?
   The provided document does not explicitly define inbound and outbound rules, but it mentions adding a rule to block inbound traffic on a specific port.
 * How does UFW simplify firewall management?
   UFW (Uncomplicated Firewall) is a tool used on Linux to simplify firewall management.
 * Why block port 23 (Telnet)?
   Port 23 is for Telnet. The task suggests blocking inbound traffic on this port as an example for testing firewall rules. Blocking Telnet is often recommended because it transmits data, including login credentials, in plain text, making it vulnerable to eavesdropping.
 * What are common firewall mistakes?
   The provided document does not contain information to answer this question.
 * How does a firewall improve network security?
   A firewall improves network security by filtering network traffic. It allows you to configure rules to allow or block traffic.
 * What is NAT in Firewalls?
NAT stands for Network Address Translation. In the context of firewalls, NAT is a method of remapping one IP address space into another by modifying network address information in the IP header of packets while they are in transit across a traffic routing device. This is commonly used to:
 * Allow multiple devices on a private network to share a single public IP address, conserving public IP addresses.
 * Hide the internal IP addresses of devices on a private network from the outside world, adding a layer of security.
### Outcome
By completing this task, you will gain basic firewall management skills and a foundational understanding of how firewalls filter network traffic to enhance security.
