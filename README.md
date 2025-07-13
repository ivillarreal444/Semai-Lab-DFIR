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

<img src = "https://i.imgur.com/nJwJ35t.png" width="500" height="350" />

After this, all that was left to do was setup the other 2 VMs, add them to the AD domain under their correct users, and the AD environment is complete.

Before moving forward, I added 2 new interfaces to pfSense through VBoxManage and configured their firewall rules in order to continue with the project, as VirtualBox only allows 4 interfaces to be created by default.

<img src = "https://i.imgur.com/WhV9iXb.png" width="1000" height="200" />
<img src = "https://i.imgur.com/XeU7cm6.png" width="1000" height="100" />

**Tsurugi Linux Setup**
Setting up this system was supposed to be as easy as setting up Metasploitable, Kali, and Chronos, however, because of the .iso file on the download page being broken for some reason, I ended up just downloading the .ova file instead, as I was already using VirtualBox for this project, which allowed me to use .ova files for installation purposes. 

**ELK Stack Setup**
In order to fully understand what exactly is happening whenever malware is deployed onto my vulnerable machines, I'll need to find some way to capture data, particularly logs and security events. This is where the ELK Stack (Elasticsearch, Logstash, Kibana) comes into play, as all three play major roles in my DFIR environment, which can be seen when I eventually start deploying malware samples into my vulnerable machines.

Firstly, however, in order to get ELK stack working, they must be configured in its own virual machine, which I ended up using Ubuntu Server for, as the setup is pretty simple and has everything I need to get the ELK stack working, such as OpenSSH server.

<img src = "https://i.imgur.com/yh48fOC.png" width="500" height="350" />

After setting up apt to allow TLS/SSL downloads from external repositories, I was able to use APT to install the first of the stack, Elasticsearch by downloading its GPG (GnuPrivacyGuard) key and its repository to the machine.

<img src = "https://i.imgur.com/mXC5m1C.png" width="500" height="350" />

In order to get elasticsearch running, I'll need to configure a couple of things in the YAML configuration file that came with the service using vim. I'll need to set up a name for the cluster, which I ended up naming after the entire lab's name, and also set the ip and port of the network host and http port (NOTE: discovery.type is not included in the YAML file by default and must be manually added.

<img src = "https://i.imgur.com/HVAdaWP.png" width="500" height="350" />

I am now able to start and enable Elasticsearch using systemctl, browsing to our set network host address over our set http port and ensuring it is accessible.

<image goes here>

Setting up Kibana is pretty similar. Simply install the repository, configure the YAML file with the proper server port, host, and name, and starting and enabling the service, while also restarting Elasticsearch in order to allow the service to recognize that Kibana is installed.

<image goes here>

Both services should now be running.

<image goes here>

<logstash part will come later>

<image goes here>

Next, I'll install Filebeat, which will play a role in collecting and stashing my necessary logs. 

<image goes here>

I'll also be sure to configure filebeat's YAML file in vim to ensure that it contains our Elasticsearch host address in order to connect to it.

<image goes here>

<filebeat/logstash segment comes later>

<image goes here>


