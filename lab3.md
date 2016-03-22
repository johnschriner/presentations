##Lab 3 - Session Data

###Setting Up Virtual Machines
Here is what we're going to be setting up:

![The Setup](https://github.com/johnschriner/presentations/blob/master/the_setup.png )

I decided to just setup a new and pristine Security Onion from an .iso.
I updated it with 
<code>sudo soup</code> and proceeded to setup the network adapters.

I gave each adapter static IPs by editing /etc/network/interfaces with nano.
Everything could ping their gateway/router but I wasn't getting internet from the bridged m0n0wall1 until I edited the remnants of WAN configurations from Lab 2.  I also added DNS 8.8.8.8 on m0n0wall1.

The appliances are all set up and now have internet access to move forward with installing SiLK et al.

![VirtualBox Environment](https://github.com/johnschriner/presentations/blob/master/VirtualBox-Environment.png ) 

Notes: Something I found was that 8gb RAM may not be enough to handle all of these machines being on at the same time.  We'll see, but I had to limit the m0n0walls to 512mb and the Ubuntu machines are sluggish at 1024mb RAM (especially for heavy CPU programs like FF).

###Installing SiLK, **Y**et **A**nother **F**lowmeter and setting up the sensors

![Make'ing SiLK](https://github.com/johnschriner/presentations/blob/master/silk-make.gif)

I installed and edited silk.conf, sensors.conf, and rwflowpack.conf.
As cautioned in the Lab3 notes, eth0 _had_ lost its 192.168.1.104 IP address. Naturally rwflowpack failed.

In <code>/etc/network/interfaces</code> I changed eth0 from manual to dhcp like eth1.
![Switching to DHCP](https://github.com/johnschriner/presentations/blob/master/switched_manual_to_dhcp.png)

rwflowpack runs with an [OK] now.

##Issues
We have this issue determining which IP should be used for eth0 or eth1:
![Security Onion IP's; 105 should be the monitoring VM?](https://github.com/johnschriner/presentations/blob/master/securityonionIPs.png)

I have tried each and, altough I don't get results, I get no error messages:
![Editing the nohup command to reflect that](https://github.com/johnschriner/presentations/blob/master/192.168.1.105_for_eth1.png)

###Next issue:
I had to explicitly add the path to site config:
![Explicitly add path to site config](https://github.com/johnschriner/presentations/blob/master/implicitly_adding_site_config.png )
