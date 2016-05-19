##Lab 6 - Scapy Attacks on ARP

As in the previous lab, I have two Ubuntu VM's on an internal network with m0n0wall assigning IPs via DHCP.

Artist's rendering:

                  Attacker                  Target
             _______________          |*\_/*|________
            |  ___________  |        ||_/-\_|______  |
            | |           | |        | |           | |
            | |   0   0   | |        | |   0   0   | |
            | |     -     | |        | |     -     | |
            | |   \___/   | |        | |   \___/   | |
            | |___     ___| |        | |___________| |
            |_____|\_/|_____|        |_______________|
            _|__|/ \|_|_.............._|________|_
             / ********** \      |    / ********** \
            /  ************  \   |   /  ************  \
            -------------------- |  --------------------
                                 |
                                 |
                                 |
                   __/ ///////// /|
                  /              ¯/|
                 /_______________/ |
                |  __________  |  |
                | |          | |  |
                | | m0n0wall | |  |
                | |          | |  |
                | |__________| | /   
                |______________|/ ___/\
                |____>______<_____/     \
              / = ==== ==== ==== /|    _|_
            / ========= === ===/ /   ////
           / ========= === ===/ /   /  / 
          <__________________<_/    ¯¯¯


Warmup Exercise (A): <code>fragment(IP(dst=target)/ICMP()/("DEADBEEF"*25000))</code>

This command will send the payload of "DEADBEEF" 25000 times to the target machine.  By adding in a fragsize, it will fragment into byte segments of 500.

I found an elegant way to do this here [1]:

Note: <code> from scapy.all import *</code> is necessary as <code>from scapy import *</code> doesn't import the modules for my machine

      from scapy.all import *
      import netifaces as nt
      import sys
      
      target="192.168.1.104"
      packet = fragment(IP(dst=target)/ICMP()/("DEADBEEF" * 25000))
      frags=fragment(packet,fragsize=500)
      counter=1
      for fragment in frags:
            print "Packet number"+str(counter)
            print "======================================================="
            fragment.show() #displays each fragment
            counter+=1
            send(fragment)

![Scapy - Nice display!](/images/Lab6-DEADBEEF.png)

The attacking machine sent 406 packets with the payload "DEADBEEF" and it set the MF (More Fragment) bit flag.

Warmup Exercise (B):  <code>IP(src=target,dst=target)/TCP(sport=135,dport=135)</code>
From the attacker side, spoofing the source of the packet:

![Spoofed source](/images/Lab6-spoofed_src_and_des.png)

On the target side I did <code>sudo tcpdump -vv icmp</code> for Warmup Exercise 1 (with the payload) and received the following when attacked from first Ubuntu machine:

![DEADBEEF payload on target!](/images/Lab6-DEADBEEF_on_target.png)

**_Q1: What are the IP/MAC addresses of each VM and the host? Comment on the three pairs of addresses, their relationship to each other; how might these values have been assigned? What do the VMs and host believe is the default gateway?_**

The attacking machine has an IP of 192.168.1.105.  The target has 192.168.1.104.  m0n0wall has an IP of 192.168.1.1 and it's the known gateway for both Ubuntu machines.  m0n0wall assigns the IPs via DHCP that I set up using its GUI.

**_Q2. Examine the arp table (arp –a –n) on VM#1 and report any entries you find._**

I did some research on arp with <code>man arp</code>.
Unfortunately <code>arp –a –n</code> complains that "-a" is an unknown host but <code>arp</code> provides the table fine.
The only entry is that of the m0n0wall gateway.

**_Q3. Ping VM#2 from VM#1 and report any changes to the state of the ARP table after the ping._**

Before pinging the target machine, there was only the gateway registered in the cache, but after a successful ping the target with its MAC address was registered in the Arp cache.

**_Q4. Manually delete the entry for the VM#2 machine in VM#1s ARP table (arp –d <ip>). Then, run tcpdump or wireshark on VM#2 to view the network traffic. Ping VM#2 again from VM#1. Report on the traffic that you see and use it to explain the way in which VM#1 obtains VM#2's MAC address._**

<code>arp -d 192.168.1.104</code> successfully removed the entry.

<code>tcpdump -vv icmp</code> on the target machine revealed:

![tcpdump of ping](/images/Lab6-tcpdump_ping.png)

**_Q5. From VM#1, using everything observed so far, determine the MAC address of the gateway._**

I believe when I used dhclient to get an IP on boot it registered the MAC address of the gateway in the ARP cache:
m0n0wall.local has a MAC address of 08:00:27:f2:0f:ab

**_Q6. Complete the program by adding lines to the arp_callback method so as to fully specify the ARP reply; you can list the fields in an ARP packet by doing ls(ARP) in Scapy. Explain the rationale for each of your lines of code._**

So far, I have:

    arpout = ARP(op=1, hwdst="impersonating_mac",hwsrc=target_mac, pdst=192.168.1.104)
but I need to fully specify the rest of the values.  Also:

Note to self:

Look into using scapy's <code>arpcachepoison()</code>

Edit: No success with arpcachepoison with either specifying MACs or IPs.

















[1]: http://rtoodtoo.net/fragmented-ip-packet-forwarding/
