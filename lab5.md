##Lab 5 - Scapy recon

I generally read through the exercise before digging in to see what the exercise is designed to teach; the most interesting thing, already,
is to see that we run into problems with determining if ports are open--or simply filtered--when we use nmap.

Some academic reading first on stealth port-scanning attacks and defence: 
<em>Network Forensics: Detection and Analysis of Stealth Port Scanning Attack</em> (Rajni Ranjan Singh and Deepak Singh Tomar, 2015) [1]

It seemed that the machines on the network simply needed to be in the same subnet, have no greater internet access, and had to be administered by m0n0wall as the gateway.  I had tried to setup the machines to talk to each other on vboxnet0 network but to no avail--even the machines on the same subnet refused to communicate.  So I took this route as I think it simplifies the setup, and it doesn't get bogged down in dealing with em0 and em1 in m0n0wall.

Both Ubuntu machines on the internal network:
![Both ubuntu machines on internal network](/images/ubuntu-wan_and_lan_on_internal_network.png)

m0n0wall is also on the internal network 'intnet':
![m0n0wall also on internal network 'intnet'](/images/m0n0wall_on_internal_network.png)

I had to reset m0n0wall to factory defaults with the IP 192.168.1.1.  Next, I added that default gateway to both ubuntu machines and rebooted. 
m0n0wall's GUI is accessible and giving out IP's via DHCP.  
![m0n0wall GUI is accessible](/images/m0n0wall_gui_accessible.png)



Citations for pull request:

Allen, J. M. (2008). OS and Application Fingerprinting Techniques. Retrieved May 9, 2016, from https://www.sans.org/reading-room/whitepapers/authentication/os-application-fingerprinting-techniques-32923 

Singh, R. R., & Tomar, D. S. (2015). Network Forensics: Detection and Analysis of Stealth Port Scanning Attack. International Journal of Computer Networks and Communications Security, 3(2), 33-42. Retrieved May 9, 2016, from http://www.ijcncs.org/published/volume3/issue2/p2_3-2.pdf


[1]: http://www.ijcncs.org/published/volume3/issue2/p2_3-2.pdf        "Singh and Tomar, 2015"
