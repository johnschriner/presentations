

##FCM-742 - Network Security - Lab 4
####I started with a fresh 15.10 Ubuntu VM in VirtualBox.<br> I had no trouble with installations except I needed to install libpcap0.8 or libpcap-dev.<br> I prefer, as you do, to import modules right into a python shell - in my case, iPython.<br>
---
I had no trouble with seeing the default values for scapy:<p>
<img src="images/Lab4-1.png" width="300"><p>
---
I used ifaddresses in netifaces to extract my local IP and the gateway:<p>
<img src="images/Lab4-2.png" width="300"><p>
---
I encapsulated an ICMP packet inside of an IP packet:<p>
<img src="images/Lab4-3.png" width="300"><p>
---
We made a custom payload:<br>
<img src="images/Lab4-4.png" width="300"><p>
---
And we successfully sent the packet and received a response:<p>
<img src="images/Lab4-5.png" width="300"><p>
---
One of the cooler things I discovered is <code>%save</code> and <code>%load</code> to save and load .py files for use in iPython.<br>
Of course, it's exporting all the commands from the notebook--even the mistakes--so it's necessary to scrub some of the commands with nano or gedit.<p> 
<img src="images/Lab4-6.png" width="500"><p>
I can certainly see how these are the fundamentals to crafting packets.  Of course since it's in python, the next steps could be conditionals, monitors, and ways to automate network tasks--even the start to penetration testing.
