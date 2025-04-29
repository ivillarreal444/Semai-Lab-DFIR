# Semai Lab DFIR

## Objective

This DFIR-based home lab project aimed to establish a controlled environment for simulating and detecting various types of cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system and simulate scenarios from basic learning scenarios to imitating real world scenarios. This hands-on experience was designed to deepen understanding of network security, attack patterns, defensive strategies, and also basic malware analysis.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Ability to recognize and detect malicious hashes.
- Ability to mitigate malicious files and executables.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Telemetry generation tools to create realistic network traffic and attack scenarios.



## Steps
**Network Diagram**

To better visualize how my home lab will look like during basic setup, I created a network diagram that will showcase my environment upon completion. 

<img src="https://i.imgur.com/ClQwiXj.png" width="500" height="1000" />

**pfSense Setup**

Once my network diagram was finished, I grabbed a pfSense ISO file and started installing the firewall onto my VirtualBox installation. Once it finished installing, I then configured the virtual network adapter interfaces that I will be using in this portion of the homelab setup. Later on there will be more ports that I will be adding, but I will only need these interfaces for now.

<img src="https://i.imgur.com/StHJ0oT.png" width="500" height="100" />


