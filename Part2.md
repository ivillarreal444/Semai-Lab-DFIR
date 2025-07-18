# Semai Lab DFIR: Simulating an Attack

## Objective

This DFIR-based home lab project aimed to establish a controlled environment for simulating and detecting various types of cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system and simulate scenarios from basic learning scenarios to imitating real world scenarios. In this part of the project, various programs will be simulating attack scenarios, with the main goal being to simulate a real-world attack scenario to discover and deepen my understanding in how to investigate various attack scenarios

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
In this first scenario, I will be using this [malware](https://github.com/k-perrino/malware-workshop-acm-w) provided to me by UTSA's ACM community.

Before running this malware, I took a snapshot of every machine that I will be using in this scenario, these machines being the Kali VM, the Active Directory VM, and just incase, the FlareVM and the REMnux VM. I probably only need the AD, Kali, and FlareVM machines for this scenario, but I have REMnux at the ready in case I need it.


