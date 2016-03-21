##Lab 3 - Session Data

###Setting Up Virtual Machines
Here is what we're going to be setting up:

![The Setup](https://github.com/johnschriner/presentations/blob/master/the_setup.png )

I decided to just setup a new and pristine Security Onion from an .iso.
I update it with 
<code>sudo soup</code> and proceeded to setup the network adapters.

I gave each adapter static IPs by editing /etc/network/interfaces with nano.
Everything could ping their gateway/router but I wasn't getting internet from the bridged m0n0wall1 until I edited the remnants of WAN configurations from Lab 2.  I also added DNS 8.8.8.8 on m0n0wall1.

The appliances are all set up and now have internet access to move forward with installing SiLK et al.

![VirtualBox Environment](https://github.com/johnschriner/presentations/blob/master/VirtualBox-Environment.png ) 

Notes: Something I found was that 8gb RAM may not be enough to handle all of these machines being on at the same time.  We'll see, but I had to limit the m0n0walls to 512mb and the Ubuntu machines are very sluggish at 1024mb RAM.

###Installing SiLK, **Y**et **A**nother **F**lowmeter and setting up the sensors

<video>https://github.com/johnschriner/presentations/blob/master/silk-make.mov</video>
