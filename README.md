<h1>Installing and enlisting a honeypot on a virtual machine</h1>

 

<h2>Description</h2>
In this project I will be downloading, installing and deploying a honeypot using VMWare Workstation 17. A honeypot is essentially a decoy system that is implemented to attract cyber attackers. It imitates a target for attackers and uses their attempts at infiltration to gather intel on the techniques of the hackers as well as test network security. There are a lot of honeypots available for use and today I'm using the Cowrie SSH honeypot. Cowrie is described as "a medium to high interaction SSH and Telnet honeypot designed to log brute force attacks and the shell interaction performed by the attacker. In medium interaction mode (shell) it emulates a UNIX system in Python, in high interaction mode (proxy) it functions as an SSH and telnet proxy to observe attacker behavior to another system." - <a href="https://github.com/cowrie/cowrie">Cowrie github page</a> <br>

<br />

<h2>Utilities Used</h2>

- <b>VMWare Workstation</b> 
- <b>Docker</b>
- <b>Network scanning</b>

<h2>Environments Used </h2>

- <b>Kali Linux</b>
- <b>Kali Purple</b>

<h2>Program walk-through:</h2>

<p align="center">
<b>Launch the honeypot:</b> <br/>

<img src="https://i.imgur.com/Pk7kJCH.jpg" height="80%" width="80%" alt="Launch honeypot"/>
<br />
We start by launching the honeypot using Docker, a platform as a service that uses virtualization to deliver software in containers. Cowrie gives us the command to use, which is listed below. <br>
<b>$ docker run -p 2222:2222 cowrie/cowrie:latest</b><br><br>
Upon running this, we see at the end of the command that we are "Ready to accept SSH connections." I open up my other virtual machine, which is running Kali Purple and can prepare to scan for open ports.<br>
<br />
<b>Scanning the "vulnerable" system:</b>  <br/>
<img src="https://i.imgur.com/pymbUsQ.jpg" height="80%" width="80%" alt="scan vulnerable system"/> <br/>
One of the first things an attacker would do when searching for systems to attack is run a network scan. I do this using nmap with the following command <br/>
<b>nmap -sC -sV <92.xxx.xx.xxx></b> 
<br><br>
This reveals an open port at 2222. This is great news because this is the port that we set up to appear open with our honeypot. Now that we see that the port is open we can try to SSH into it to gain "access".<br/><br/>
<b>SSH into the open port:</b>  <br>
<img src="https://i.imgur.com/OQjyGni.jpg" height="80%" width="80%" alt="ssh vulnerable system"/> <br/><br/>
The first thing we need to do is ssh into the root of the honeypot using the open port. We can do so with the command: <br/>
<b>ssh -p 2222 root@xxx.xxx.xx.xxx</b><br/><br/>
Success! After typing yes to continue connection and typing anything for the password because it is open, we have entry into the honeypot system. I ensured this by opening up the other virtual machine side by side. A connection was established and every action that took place on the system that had connected to the honepot was logged on the decoy.<br/>
This was a quick little demonstration to show how easy it can be to deploy a honeypot system and track potential attackers. Thank you for joining me!

