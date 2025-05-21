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

**Kali Linux, pfSense Firewall, and Cyber Range Setup**

I then set up my main environment, which I chose to be a Kali Linux environment as it is the linux distro I am more familiar with, and it also has a bunch of nice tools that I could use to conduct my own vulnerability assessments of the other machines that I will be creating throughout this project. Once my main environment was setup, I was able to access the pfSense dashboard through pfSense's provided DNS server. From here I set up my own domain and hostname for the lab, as well as changing the password of the admin user. 
<img src = "https://i.imgur.com/4QJh9qh.png" width="700" height="500" />

Once setup was completed, I set up the firewall rules for the LAN, CYBER_RANGE, and AD_LAB subnets. These rules ensure that traffic flows to the subnets they are supposed to flow through, and that traffic does not flow to subnets they are not supposed to flow through.

<img src = "https://i.imgur.com/47PT5xm.png" width="1000" height="200" />
<img src = "https://i.imgur.com/R5kZBEL.png" width="1000" height="250" />
<img src = "https://i.imgur.com/eAvMFbH.png" width="1000" height="200" />

After all the firewall rules were setup, I then set up Metasploitable 2 and Chronos instances, which were super simple, as all I had to do was download the ISOs, drop them in VirtualBox, and they were ready to go immediately (other than chronos, still figuring out how to get the login for chronos as of writing this...).

**Active Directory Setup**

My Active Directory environment consists of 3 Windows VMs, one of them being the Domain Controller (running Windows Server 2019), and the other two serving as clients for the Domain Controller (both running Windows 10 Enterprise). After setting up my Domain Controller VM, I then installed all of the essentials required for the machine to serve as the Domain Controller, such as the Active Directory Certificate Service and the Active Directory Domain Service. Once those were installed and running, I then configured the DNS and DHCP services so that the clients are able to properly connect to the domain controller. The DNS service will be configured with a forwarder that will forward DNS queries to pfSense if the domain controller cannot resolve them. The DHCP will assign random IP addresses to the two clients in order for them to connect to the domain controller's DNS. The Active Directory Certificate Service is the "Certificate Authority" of the domain controller, which will be responsible for signing, issuing, and storing digital certificates.

<img src = "https://i.imgur.com/U6cys6Y.png" width="1000" height="500" />

In this active directory environment, the other two machines should serve as clients, not administrators, so in order to do this, I created three users in the directory. One user, which will be under my name and was used during the AD setup, and two other users which will be under different names. These two users will be the logins for the other two machines.

<img src = "https://i.imgur.com/lHVUUtL.png" width="200" height="100" />

And since this entire lab was supposed to be for DFIR purposes, it will be a lot more fun to have at least one vulnerable machine in the entire environment, thus, I executed a script that created multiple vulnerabilities up to and including the addition of multiple random users into the AD. This, in turn, is why my AD user list currently looks like this:
