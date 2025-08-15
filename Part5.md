# Semai Lab DFIR: Digital Forensics and Malware Analysis: Simulation 1

## Objective

This DFIR-based home lab project aimed to establish a controlled environment for simulating and detecting various types of cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system and simulate scenarios from basic learning scenarios to imitating real world scenarios, as well as to analyze attack forensics and strategies and how to mitigate them with the goal of creating a more secure environment. In this part of the project, I will be simulating an attack scenario by infecting a domain controller with a real malware sample in an isolated environment and improving my malware analysis and threat mitigation skillset by detecting the threat, analyzing the threat, and also mitigating the threat.

### Skills Learned

- Ability to detect threats using network logs.
- Enhanced knowledge of digital forensics and attack mitigation.
- Advanced understanding of malware behavior and the tools used in conducting basic malware analysis
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
- Type-2 Hypervisor for Virtual Machine Cluster
- Windows and Linux machines for various DFIR environments
- Security Information and Event Management (SIEM) system for log ingestion and forensic analysis.
- Automated background services for attack detection and mitigation.
- Malware Sample for attack simulation (EchoThreat)
- Malware Analysis tools for code decompilation and extensive code analysis (Ghidra, VirusTotal)

## Steps
Welcome to the first of three malware analysis simulations that I will be performing on my DFIR environment! These scenarios will scale in difficulty, from an easy sample of malware to analyze to a more sophisticated and possibly difficult sample of malware to challenge my understanding of malware analysis. In this simulation, I technically won't necessarily be using a typical malware sample per say, but it is a program called [EchoThreat](https://github.com/hulkmode/echothreat/tree/main), which triggers lots of detections in my SIEM, and the goal for this scenario is to produce detection logs using the program, closely analyze those logs and find out how the program is triggering those detections, and then isolate the program and look at the code in a much deeper depth. Since this program's purpose is only to generate logs and act as a suspicious piece of software even though it's harmless, I generally wouldn't need to isolate the domain controller, but it's still good practice to isolate your virtual machines when detonating malware, just so the malware doesn't actually escape the machine and travel to places other than the VM itself. It's also good practice to create a snapshot/backup of the machine's current state and revert to that same snapshot/backup to ensure full removal of the threat, rather than just uninstalling the malware and calling it a day.

