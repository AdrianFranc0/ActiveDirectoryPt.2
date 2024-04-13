# ActiveDirectoryPt.2

## Objective


In this home lab with Active directory which the majority of organizations use to manage resources such as users,computers, and groups. In this Project we will create an Active Directory domain/machine and also have a splunk/target machine to monitor the brute force attack/activity on the user from the AD domain, which I will be producing from Kali Linux to be attacking one of the Target machine's users and monitoring that activity. Along with the help of Atomic Red Team to utilize the MITRE ATT&CK framework to investigate/validate the malicious activity. 


### Skills Learned


- Using Atomic Red Team
- Performing brute force attack on Kali Linux using crowbar tool
- Development of recognizing attack patterns and critical thinking/problem-solving skills in cybersecurity. 
- MITRE ATT&CK framework
- More expirence with Splunk
- Getting more familiar with Active Directory


### Tools/Assets Used


- Splunk
- Atomic Red Team
- Powershell
- Kali Linux
- Active Directory
- crowbar
- Sysmon
- Oracle VM

## Steps

<p align="center">
Lab overview  <br/>
<img src="https://i.imgur.com/u9zGfPB.png" height="80%" width="80%" alt="Lab overview"/>
<br />
<br />


We will be using (windows 2022 server, windows 10, Kali Linux, Ubuntu server) on Oracle VM:  <br/>
<img src="https://i.imgur.com/PYNUO2C.png" height="80%" width="80%" alt="Set up network on DC VM"/>
<br />
<br />

Make sure our virtual machines are on the same network by creating our own NAT network we will applying this network setting for all of our VMs: <br/>
<img src="https://i.imgur.com/xsgLHmu.png" height="80%" width="80%" alt="DHCP IPv4 network set up"/>
<br />
<br />

Next setup static IP address and configure addresses for the (splunk machine):  <br/>
<img src="https://i.imgur.com/VAeODDa.png" height="80%" width="80%" alt="enter the powershell on DC VM"/>
<br />
<br />

I added myself as a user for virtual box and made a directory and mounted it to the shared file/project folder that has splunk and other needed files. As you can see the Share dir is highlighted. I then changed directory and will download splunk from my folder :  <br/>
<img src="https://i.imgur.com/INw3ILN.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Next after installing splunk from the shared folder, I changed directory to be where splunk is. As you can see that the limits and user belongs to “splunk” which I then acted as the user splunk to run the installer :  <br/>
<img src="https://i.imgur.com/c31dm97.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<img src="https://i.imgur.com/JjLURiT.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Next Rename windows Target PC :  <br/>
<img src="https://i.imgur.com/rWQtTnM.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

In the windows target PC download splunk universal forwarder, Sysmon with Sysmon olaf from git hub  :  <br/>
<img src="https://i.imgur.com/BTRYjLw.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Next we need to instruct our Splunk forwarder to tell it what to send over to the Splunk server, we will do this by configuring a file called inputs.conf located in the C drive
However we will not edit the inputs.conf file under the “default” directory, instead we will make a new directory to edit it, then have the editted version in the "local" dir:  <br/>
<img src="https://i.imgur.com/tT6ZMHi.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

In the windows VM still, I type the IP of my splunk system to access the splunk portal and I head to indexes and create a new index called “endpoint” :  <br/>
<img src="https://i.imgur.com/5HRxJOz.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Now on the search tab using my search for my endpoint index, you can see the events with our host of Target-PC & our Active Directory machine. We also see the security,application,and Sysmon data:  <br/>
<img src="https://i.imgur.com/wxbMkTk.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<img src="https://i.imgur.com/FDheWee.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<img src="https://i.imgur.com/R16Xhir.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />


Now we will configure splunk universal forwarder and Sysmon on the Active Directory machine as well which will add onto the splunk hosts. 

on the ADDC01 VM on the server manager I will add Active directory domain services and install :  <br/>
<img src="https://i.imgur.com/QsupWLs.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

In the flag indicator I will select “promote this server to a domain controller”
Next I will select Add new forest because we will be creating a new domain and create a password for it then finish installing:  <br/>
<img src="https://i.imgur.com/w1Ruq6p.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<img src="https://i.imgur.com/WoQYzu4.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Next we will create users, by right clicking our New domain and selecting organizational Unit and name it as well as add a couple users to our organization:  <br/>
<img src="https://i.imgur.com/ezWN8GT.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<img src="https://i.imgur.com/MH88Pk0.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Now we have our Active Directory set up and our server is a domain controller, we will go to our Windows Target machine and join it to our Falso domain using “Jeremy Smith’s” account when I log in :  <br/>
<img src="https://i.imgur.com/DEUc8M1.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<img src="https://i.imgur.com/TIwznk0.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

We will use our Kali linux machine to perform a brute force attack on our users.
First we will set up our IP based on our diagram from earlier:  <br/>
<img src="https://i.imgur.com/Ps0Vz86.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Next I made a new directory called “ad-project” and installed a tool that we will be using for our attack called crowbar. This tool is for our brute force attack (this is for educational purposes):  <br/>
<img src="https://i.imgur.com/gocrkDC.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Under the user wordlists directory there is a file called “rockyou.txt” which we will unzip with gunzip and make a copy into our project directory:  <br/>
<img src="https://i.imgur.com/YBjPrtC.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

After unzipping the rockyoutxt, I then listed 20 passwords for the tool to try all of them including the correct one that I have added after for security reasons :  <br/>
<img src="https://i.imgur.com/rn8dFkz.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Before we start our attack, on our (target windows machine) we will go on the settings and enable remote desktop because the tool supports rdp protocol :  <br/>
<img src="https://i.imgur.com/X6VR4Xf.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Now back to out Kali linux machine, we will be using out brute force tool and using it on the jsmith user in our domain. As you can see it reveals the password of that users account :  <br/>
<img src="https://i.imgur.com/Cgim5Of.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Now we check on splunk to see what telemetry was generated. As you can see there was # attempts to log into jsmith’s account which is on the list of 20 passwords from before not including the real password I added which I did not show for security reasons. You can also see the event id of 4625 which means failed attempts to log in showing that the brute force tried all the passwords from the list :  <br/>
<img src="https://i.imgur.com/4d9oNG3.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Following with the information that we have I added the event code to the search query, as you can see the events happening almost at the same time also indicates a brute force attack due to all the simultaneous attempts to log in from trying all the passwords :  <br/>
<img src="https://i.imgur.com/8aVBE4U.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />


Now still in my Target machine, We will now set up and use Atomic Red Team to run tests and generate telemetry and be able to detect similar attacks in the future. 

First on powershell we will set an exclusion in our C drive because Microsoft defender may remove files for ART :  <br/>
<img src="https://i.imgur.com/IohVz2E.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Using this from github allows us to download AtomicRedTeam which should now be seen in our files under local C disk :  <br/>
<img src="https://i.imgur.com/Lqvrcef.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Using MITRE ATT&CK framework as reference, in the Persistence tactic under create account we have local acc, domain acc, and cloud acc under atomics :  <br/>
<img src="https://i.imgur.com/T1M0HBm.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

Now in Powershell we will use AtomicRedTeam and use the code from the MITRE framework, which after running the command we will check for activity on splunk. We are doing this because we want to see if the attacker created a local account or another type of account after the password being compromised. This also allows me to check and see if I can identify certain activity from running automic tests :  <br/>
<img src="https://i.imgur.com/ANYdRwz.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />

As you can see there was activity :  <br/>
<img src="https://i.imgur.com/YCjmxOI.png" height="80%" width="80%" alt="Once the page is loaded use the link to access OpenVAS and use the username to log in"/>
<br />
<br />


I hope you learned and enjoyed my Active Directory Project! :)
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
*Ref 1: Network Diagram*
