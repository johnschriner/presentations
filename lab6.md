(VIEW in RAW to see the ASCII art!!)
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
 /  ************  \    |   /  ************  \
--------------------   |  --------------------
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


Q1: fragment(IP(dst=target)/ICMP()/("DEADBEEF"*25000))

This command will send the payload of "DEADBEEF" 25000 times to the target machine.  It will fragment it but I didn't set a fragment amount.

From here [1] I found an elegant way to do this:

      from scapy.all import *
      import netifaces as nt
      import sys
      
      target="192.168.1.104"
      packet = fragment(IP(dst=target)/ICMP()/("DEADBEEF" * 25000))
      frags=fragment(packet,fragsize=500)
      counter=1
      for fragment in frags:
            print "Packet no#"+str(counter)
            print "==================================================="
            fragment.show() #displays each fragment
            counter+=1
            send(fragment)













[1]: http://rtoodtoo.net/fragmented-ip-packet-forwarding/
