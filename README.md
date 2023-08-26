<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we will observe various network traffic to and from Azure Virtual Machines using Wireshark as well as experiment with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Command-Line Tools and Prompts
- Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04



<h2>Steps</h2>

<p>
</p>
<p>

Welcome to my tutorial on observing Network traffic using Azure virtual machines and Network Protocols. In order to get this started you will need to create two Virtual Machines on Microsoft Azure. We need to create two virtual machines. One will have a Windows 10 OS and the other will have Ubuntu Linux. Do make sure that both Virtual Machines are connected to the same Network. You will also want to make sure that both the VMs have 2 CPUs, as you don't want the VMs to be slow. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

Once both of your Virtual Machines have been created, open up the Windows desktop app (if using a Mac computer, you should be able to download it from the app store). Once opened, enter the IP address that was assigned to your Windows VM. The screen will then prompt you with a sign in, use the username and password that you created while creating both your VMs. Once you've logged in, go and download Wireshark, a packet analyzer. Here is the link for reference: https://www.wireshark.org/download.html. Click on the windows 64 bit install, and once that is downloaded and installed, go in and explore the environment.


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Let's now filter for ICMP. For refreshers, ICMP or Internet Control Message Protocol is a protocol used to send information indicated success or failure when communicating with another IP address. Once we have filtered for this, go ahead and retrieve the private IP address of the Ubuntu Linux VM and attempt to ping it from the Windows VM. Do observe the ping requests and replies. Also try and ping a public website such as Google (wwww.google.com) and observe the traffic.


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

After doing this, let us initate a perpetual/non-stop ping from our Windows 10 VM to our Ubuntu Linux VM. Open up the Network Security Group that your Ubuntu VM is using and disable incoming ICMP traffic. Go back to your Windows VM and observe...it should show you that the request timed out. 

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Now go back and re-enable ICMP traffic in the Network Security Group that your Ubuntu VM is using. Go back and observe the traffic again, it should work again. 


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<br />


<p>

</p>
<p>

Let's observe SSH traffic! As a refresher, SSH is a protocol that is used for operating network services over an unsecured network. Go back to Wireshark and filter for SSH traffic only, and then from your Windows 10 VM go and "SSH into" your Ubuntu VM through its private IP address. You can then type in some commands like username and observe the ICMP traffic in Wireshark and the command line activity.


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</p>
<br />


<p>
</p>
<p>

Amazing! At this point in the lab you must be getting some sort of intuition of how Virtual Machines communicate with one another. Let's observe another protocol, the DHCP protocol. As a reminder, the DHCP protocol or Dynamic Host Configuration Protocol, is a protocol responsible for automatically assigning IP addresses using client-server architecture. Go back to Wireshark and filter for DHCP traffic. Then go back to the command line and attempt to issue a new IP address from the command line, such as ipconfig /renew.
  
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<br />



<p>
</p>
<p>

Time to observe DNS traffic! Go back to Wireshark and filter for DNS traffic only. Then go back to the command line and use the command nslookup to see what Google's (www.google.com) IP address is. Observe the traffic as well. 

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</p>
<br />



<p>
</p>
<p>

Finally, let's observe RDP traffic. RDP, or the Remote Desktop Protocol is a protocol that provides a user with a graphical interface to connect to another computer over a network connection. In fact we are using Microsoft Remote Desktop to do this lab! Going back to Wireshark, filter for RDP traffic only by typing in (tcp.port == 3389). Observe the non-stop spam of traffic. The question I leave to you now, is why do you think that it is non-stop spamming traffic?


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</p>
<br />
<br />

