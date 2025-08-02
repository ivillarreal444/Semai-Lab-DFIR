# Semai Lab DFIR: Simulating and Detecting an Attack using Elastic Defend

## Objective

This DFIR-based home lab project aimed to establish a controlled environment for simulating and detecting various types of cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system and simulate scenarios from basic learning scenarios to imitating real world scenarios. Elasticsearch's "Defend" feature is an EDR tool that assists with security by providing malware protection, threat detection, and automated response capabilities. In this part of the project, I will be setting up Elastic Defend and simulating an attack in order to gain a better understanding of log analysis.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Ability to ingest and generate network logs.
- Enhanced knowledge of Certificate Authorities and the Windows Active Directory Environment
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
- Type-2 Hypervisor for Virtual Machine Cluster setup
- Windows and Linux machines for various DFIR environments
- Security Information and Event Management (SIEM) system for log ingestion and analysis.



## Steps
In this first scenario, I will be using my Kali VM that was created in Part 1 of this project series. Kali contains many attack modules that can be utilized to perform various attacks, and in this part of the project, I will demonstrate some of these attack modules, as well as the event logs in elastic that were generated from these attacks.

Before running this malware, I took a snapshot of every machine that I will be using in this scenario, these machines being the Kali VM, the Active Directory VM, and just incase, the FlareVM and the REMnux VM. I probably only need Kali, Kali, and the Domain Controller for this scenario, but I have REMnux and FlareVM at the ready in case I need them.


**Elastic Defend Setup**
In Part 1, the agent I had deployed into my Domain Controller machine was previously configured with Elastic Security as I had used Windows integrations in order to ingest various systems logs, however, in order to actually pick up other various logs, such as things that might occur in other areas of the machine, such as endpoints, I need to add an additional integration to my elastic instance. This is where the "Endpoint Security" integration comes into play, as it will be extremely useful for capturing endpoint logs for various attacks I will demonstrate in this part of the project.

<img src="https://i.imgur.com/GswHYfB.png" width="500" height="1000" />

I decided to add the integration to the default agent policy, just incase I add any agents to other instances like my Kali instance or my REMnux instance.

<img src="https://i.imgur.com/PJb61UZ.png" width="500" height="1000" />

I had also configured a Windows specific agent policy which was responsible for initially capturing certain logs, but we want to also capture additional logs like Endpoint logs, and endpoint integration should help do the trick.

<img src="https://i.imgur.com/VeNJvx1.png" width="500" height="1000" />

**Scenario 1: Password Spraying**
Password Spraying is one of the easiest and most common attack techniques as it involves utilizing lists of common usernames and passwords, repeatedly brute-forcing those usernames and passwords throughout an entire server, and analyzing which accounts have successful logins from these attempts. In a very secure environment, this should not be that much of a problem, but even in today's environment it can still be a viable strategy, especially when targeting individuals who might not have much knowledge of internet security.

When scanning the environment with nmap, I noticed that there are a LOT of ports open in the Domain Controller. This is most likely the result of the script I downloaded during the AD setup, which opened the domain controller to many vulnerabilities, such as these open ports that I am now able to exploit.

<img src="https://i.imgur.com/ugMnIjM.png" width="500" height="1000" />

This might make it easy to get Hydra, a password sprayer, up and running in the simplest way possible. 

