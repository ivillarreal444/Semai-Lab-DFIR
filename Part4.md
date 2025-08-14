# Semai Lab DFIR: Simulating and Detecting an Attack - Scenario 3: Introduction to Malware and Malware Analysis

## Objective

This DFIR-based home lab project aimed to establish a controlled environment for simulating and detecting various types of cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system and simulate scenarios from basic learning scenarios to imitating real world scenarios. In this part of the project, I will be simulating attack scenarios to gain a better understanding of log analysis and threat detection and mitigation.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Ability to ingest and generate network logs.
- Enhanced knowledge of digital forensics and attack mitigation.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
- Type-2 Hypervisor for Virtual Machine Cluster setup
- Windows and Linux machines for various DFIR environments
- Security Information and Event Management (SIEM) system for log ingestion and forensic analysis.
- Automated background services for attack detection and mitigation.



## Steps
In the previous scenario, we demonstrated an attack scenario involving poor security configurations and poor login credentials. This scenario then led to an exploit attempt that became unsuccessful by the end of it, but also led into our next scenario involving malware, which will lead into the "Malware Analysis" section of the project where we begin to reverse-engineer malware in order to determine what it's exactly doing.

**Malware 1**
For this scenario, I'm using a [malware sample](https://github.com/k-perrino/malware-workshop-acm-w) provided to me by the University of Texas at San Antonio's ACM-W club, which is a pretty fun club to get involved in (they also demonstrated the malware sample at a malware analysis workshop which was pretty cool). 

**NOTE: Before executing the malware, PLEASE be sure to isolate your environment from your entire network, or perhaps even disable internet connectivity from the VM entirely. I'm running a different pfsense setup for this environment as winlogbeat still requires an outbound connection to the ELK stack VM in order to work, so I want to disconnect the domain controller from everything but the ELK stack VM, for now.**

Before we isolate the domain controller, we want to actually download and compile the malware first. Since the malware runs on a C file, we're going to have to compile it in order for it to run, but because of Elastic Security being a potential issue, there is a chance we'll have to find a way to compile and then immediately run the file right after compilation, hoping that Elastic Security won't be a problem once again, but first, let's install the C compiler.
