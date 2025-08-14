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

After installing a package manager of our choice, which I decided to use Chocolatey, I installed the MinGW package, which includes the GCC compiler normally used for C compilation.

<img src="https://i.imgur.com/ogyJlFC.png" width="500" height="1000" />

Now we're ready to download the malware sample directly from the github page!

<img src="https://i.imgur.com/3BGAHFK.png" width="500" height="1000" />

**NOTE: If you're following along, PLEASE isolate your OS before continuing further! I take no responsibility for misuse! CONTINUE AT YOUR OWN RISK!**

After isolating my domain controller using pfsense, I then compiled the file, which ended up becoming successful so far! Elastic Security did not alert me about the compiled executable file. Time to have some fun!

<img src="https://i.imgur.com/5szxs64.png" width="500" height="1000" />

After executing the file, the program went straight to action. It didn't even take that long for me to find evidence of the executable file editing registry entries right after execution.

<img src="https://i.imgur.com/rPKQdIt.png" width="500" height="1000" />

Not only were registries changed, while filtering logs by "process.name: dns_rev_shell.exe", I found a log that shows a DNS query to a dns called "c2.malicious.local". What makes this stand out from typical DNS queries is the first two characters in the domain: C2. This DNS query is leading to a Command-And-Control infrastructure, an essential tool used by bad actors to control malware on affected devices. If I planted something like this in Celesta's instance in the last scenario, I probably would've been able to gain easier access to her desktop environment, as well as potentially abuse exploits that would lead to privilege escelation, and this is only one scenario that becomes possible with malware.

**Malware Analysis and Mitigation**
Now comes the question, how would we be able to transport this malware to a safe environment to analyze it? We know some of the things that the malware did just from elastic logs, but that's generally not enough as agents like winlogbeat can only log so much. This is where Tsurugi, FlareVM, and Remnux come into play.

After adding a couple of firewall rules that allow communication ONLY to and from Tsurugi and domain controller, I transfer the malicious file from the domain controller, as well as remove the file from the OS completely.

<img src="https://i.imgur.com/HqavsJF.png" width="500" height="1000" />

Going to the Tsurugi Linux VM, the file was successfully imported to the VM. Analyzing the file here would not be a great idea, however, as it does have open internet access.
