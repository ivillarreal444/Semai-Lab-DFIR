# Semai Lab DFIR: Simulating and Detecting an Attack - Scenario 2: Basic Vulnerability Exploitation

## Objective

This DFIR-based home lab project aimed to establish a controlled environment for simulating and detecting various types of cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system and simulate scenarios from basic learning scenarios to imitating real world scenarios. In the previous part of the project, multiple open ports were found inside the domain controller, and in this part of the project, those ports will be exploited using vulnerabilities associated with those ports.

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
In the last scenario, I was unsuccesfully able to actually log into the OS itself, however, I was able to detect and mitigate the brute force attack that I purposefully set up on my kali machine in order to evaluate how logs are generated when a brute force attack occurs. Since those logs can easily generate an IP address of the attacking machine, which in this case, was my Kali machine, it was pretty easy to mitigate a common attack like that, especially when even Hydra could not find simple login credentials to the machine (I had tested a longer brute force attempt with Hydra and it ended up getting stuck on the Guest account). As you may have seen already, I have never actually updated the Domain Controller's Windows OS, which opens up the door to many vulnerabilities, especially with the Server Message Block (SMB) protocol, which is a Windows protocol utilized for file, printer, and serial number sharing over a network, among many other resources, and file sharing protocols like SMB are common targets of vulnerability exploitation attacks. Various attacks like WannaCry and EternalBlue have utilized various SMB exploits in order for attackers to gain unauthorized systems, and the main focus for this scenario is to simulate my own attack through my Domain Controller's SMB port, as well as mitigating and securing the Domain Controller against such attacks (and incase you were wondering, yes, i did take snapshots of every machine involved in this scenario incase something goes wrong!).

