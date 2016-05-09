##Lab 5 - Scapy recon

I generally read through the exercise before digging in to see what the exercise is designed to teach; the most interesting thing, already,
is to see that we run into problems with determining if ports are open--or simply filtered--when we use nmap.

Some academic reading first on stealth port-scanning attacks and defence: 
<em>Network Forensics: Detection and Analysis of Stealth Port Scanning Attack</em> (Rajni Ranjan Singh and Deepak Singh Tomar, 2015) [1]

I start with setting up a VM network with m0n0wall as the gateway and setting up pyenv on one of the machines.

Citations for pull request:

Allen, J. M. (2008). OS and Application Fingerprinting Techniques. Retrieved May 9, 2016, from https://www.sans.org/reading-room/whitepapers/authentication/os-application-fingerprinting-techniques-32923 

Singh, R. R., & Tomar, D. S. (2015). Network Forensics: Detection and Analysis of Stealth Port Scanning Attack. International Journal of Computer Networks and Communications Security, 3(2), 33-42. Retrieved May 9, 2016, from http://www.ijcncs.org/published/volume3/issue2/p2_3-2.pdf


[1]: http://www.ijcncs.org/published/volume3/issue2/p2_3-2.pdf        "Singh and Tomar, 2015"
