<h1>Active Directory Home Lab Project - Setting up RAS/NAT/DHCP</h1>

<h2>Description</h2>
This project is a continuation of https://github.com/brandonvansylalom/Active-Directory-HomeLab-Setup and I will be setting up RAS/NAT, or Remote Access Server and Network Address Translation. The purpose behind this is to allow any Windows 10 Client that we join to our domain to be part of the virtual private network (being your AD/DC server) while still being able to access the internet outside through the DC. Then, we will setup a DCHP server on our DC with the scope information from RAS/NAT. It will allow our Windows 10 clients to get an IP address to go to the Internet while being on a private internal network, just like in your SOHO office or if you were at school browsing the Internet and taking a break from studying. See diagram below for reference/network information.

<br>
<br/>

<b>ALL CREDITS ON THIS PROJECT GOES TO JOSH MADAKOR. <b> 

<br/>
<img src="https://imgur.com/yibftVW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<h2>Languages and Utilities Used</h2>

- <b>None yet but next project will incorporate PowerShell and scripts.
  
<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b>Windows Server 2016</b>
- <b>Oracle VirtualBox</b>

<h2>Lab walk-through/details:</h2>

<p align="center">

Go to Server Manager and select 2) Add Roles and Features  <br/>
<img src="https://imgur.com/nwpiBiv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Hit next for all the steps. Make sure your server is selected on Server Selection Tab. When on Server Roles tab, find and check "Remote Access", then next. When you get to Role Services below Remote Access, select and check Routing, then hit next. Afterwards, next until install. Wait for install to finish. <br/>
<img src="https://imgur.com/clKhngL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Go to Tools and find Routing and Remote Access.  <br/>
<img src="https://imgur.com/P1EWnyh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Go to DC local, right click and select Configure and Enable Remote Routing and Access. Next, then select Network Address Translation (this will allow our Windows clients to connect to the internet with a public IP address). <br/>
<img src="https://imgur.com/Q1p4KLM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next, select Use this public interface to connect to the internet. If it's greyed upon this step, close out the process and repeat until back at this step. Choose the Internet interface (not your internal), hit next and Finish.  <br/>
<img src="https://imgur.com/1zIk6yY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Once done, everything should look like below (up and colored green, with more network options that appear).  <br/>
<img src="https://imgur.com/W8PXW8i.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next is setting up the DHCP server. Similarly to the steps before, go to Server Manager, Add Roles and Features, next all the way until you get to Server Roles. On there, find and check DHCP Server. Then, continue with Next until Install and hit Install. <br/>
<img src="https://imgur.com/dWjBhfd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next, go to Tools and open DHCP Server up. <br/>
<img src="https://imgur.com/J1f4JWI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Click on DC.domain, right click on IPV4, and enter 172.16.0.100-200 as the Name (that'll be the range for our clients to use) 
<br/>
<img src="https://imgur.com/DjmfAGR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the information below on the next window.
<img src="https://imgur.com/3eYNppg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Hit next for the other steps until you get to Router (Default Gateway). Enter the information below then hit next until you reach "I want to activate the scope." The previous steps not pictured describes how long devices can least IP addresses within a DHCP server; it varies on IT environments, for example, Starbucks or coffee cafes might set it at 2 hours or so, so that other guests can hop on their Wi-Fi to browse and use especially if they get high traffic. For this project, keep it at the default it was set at. <br/>
<img src="https://imgur.com/1Mzj4ad.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Once activated, right click on the DHCP server and Authorize it. Once done, go to IPV4, right click on it and hit refresh. You should see IPV4 up in green and your scope. <br/>
<img src="https://imgur.com/zOk68FF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
We have now configured RAS, NAT and our DHCP and overall DNS setup. <br/>
<img src="https://imgur.com/iyXd3gm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next we will go back to the DC and make a configuration that let will us browse the internet from the DC. Usually in a standard production environment this isn't done but will be done on this project.
Go to Server Manager, Configure this local server, find IE Enhanced Security Configuration, and set both selections to off, shown below. This will make it easier to browse the internet without the annoying warning ads and notices (which is why production settings keep it on). <br/>
<img src="https://imgur.com/7ZR80b7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next repository will go over PowerShell, scripts, creating users and setting up Windows clients to be joined to the domain.

