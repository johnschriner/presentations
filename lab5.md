##Lab 5 - Scapy recon

I generally read through the exercise before digging in to see what the exercise is designed to teach; the most interesting thing, already,
is to see that we run into problems with determining if ports are open--or simply filtered--when we use nmap.

Some academic reading first on stealth port-scanning attacks and defence: 
<em>Network Forensics: Detection and Analysis of Stealth Port Scanning Attack</em> (Rajni Ranjan Singh and Deepak Singh Tomar, 2015) [1]

It seemed that the machines on the network simply needed to be in the same subnet, have no greater internet access, and had to be administered by m0n0wall as the gateway.  I had tried to setup the machines to talk to each other on vboxnet0 network but to no avail--even the machines on the same subnet refused to communicate.  So I took this route as I think it simplifies the setup, and it doesn't get bogged down in dealing with em0 and em1 in m0n0wall. In fact, I disabled adapter 2 in m0n0wall so its watchdog complains.

Both Ubuntu machines on the internal network:
![Both ubuntu machines on internal network](/images/ubuntu-wan_and_lan_on_internal_network.png)

m0n0wall is also on the internal network 'intnet':
![m0n0wall also on internal network 'intnet'](/images/m0n0wall_on_internal_network.png)

I had to reset m0n0wall to factory defaults with the IP 192.168.1.1.  Next, I added that default gateway to both ubuntu machines and rebooted. They have IPs of 192.168.1.104 and 192.168.1.105.
m0n0wall's GUI is accessible and giving out IP's via DHCP.  
![m0n0wall GUI is accessible](/images/m0n0wall_gui_accessible.png)

Next, to setup pyenv and start sending packets!

I did a <code>whoami</code> to see which home to reference in root's .bashrc.
I did <code>sudo su</code> to make sure I was exploring the directory as root to edit .bashrc:
![Root's .bashrc edited](/images/roots_bashrc.png)

As these machines are on an internal network, I momentarily gave my ubuntu-LAN machine a bridged network to download pyenv. I also had to install both scapy, python-netifaces, and nmap as this is a new VM.  I then shutdown and removed the adapter because I want everything to be in this internal network.

I then installed pyenv using this resource: http://opencafe.readthedocs.io/en/latest/getting_started/pyenv/
I found that I needed to install curl.  Once cloned and place in my home directory from Git, to run pyenv, I needed to navigate to <em>/home/d4cs-student/.pyenv/bin</em> where I could then <code>./pyenv install 2.7.6
</code> and <code>./pyenv global 2.7.6</code>.

It appears I _did_ the editing to root's .bashrc out-of-order, but the config should still work given that _now_ it knows where the python environment is.  

Edit: no, upon installation of pyenv, something overwrote root's .bashrc.

To find it again, I need to remember to <code>ls -a</code> to see the hidden files:
![ls -a](/images/LAB5-using_ls-a.png)

I went through and again edited it, but I still had permission errors when using scapy (probably because I didn't log out or reboot).

I decided to simply <code>sudo python</code> (as you would be running as root in Kali or most pen-testing OS's anyway) and scapy worked great!

To suppress many: "WARNING: Mac address to reach destination not found. Using broadcast" I added the following to the import modules  [2]:

    import logging
    logging.getLogger("scapy.runtime").setLevel(logging.ERROR)

This cleans up the output greatly.

Firstly, we'll send along an ICMP packet and see how the other Ubuntu VM responds:

![python shell, scapy, and an ICMP packet](/images/LAB5-scapy-ICMP.png)

Next, we'll send a TCP packet and see the response:

![python shell, scapy, and a TCP packet](/images/LAB5-scapy-TCP.png)

**To do:  find out why it sends "ftp_data"--is it sending this data to each port in the scan via TCP?**

I decided to run nmap to see if it could find any open ports:

![using nmap on remote Ubuntu VM](/images/LAB5-using_nmap.png)








Citations for pull request:

Allen, J. M. (2008). OS and Application Fingerprinting Techniques. Retrieved May 9, 2016, from https://www.sans.org/reading-room/whitepapers/authentication/os-application-fingerprinting-techniques-32923 

Singh, R. R., & Tomar, D. S. (2015). Network Forensics: Detection and Analysis of Stealth Port Scanning Attack. International Journal of Computer Networks and Communications Security, 3(2), 33-42. Retrieved May 9, 2016, from http://www.ijcncs.org/published/volume3/issue2/p2_3-2.pdf


[1]: http://www.ijcncs.org/published/volume3/issue2/p2_3-2.pdf        "Singh and Tomar, 2015"
[2]: http://resources.infosecinstitute.com/what-is-scapy/
