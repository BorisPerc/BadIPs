# BadIPs
BadIPs List PCSNET

BadIP List Piramide Studio NET

<a href="https://perc.ddns.net/iplist.txt" title="BadIP List PCSNET Live list"><h1 style="color:green;">BADIP LIST PIRAMIDE STUDIO NET LIVE LIST & CUMULATIVE LIST FIREWALL</h1></a>
<a href="https://piramide.zapto.org/iplist.txt" title="BadIP List PCSNET"><h1 style="color:green;">BADIP LIST PIRAMIDE STUDIO NET STATIC LIST</h1></a>

<a href="https://perc.ddns.net/iplist-pcsnet.txt" title="BAD IPS LIST DOWNLOAD TXT File Comulative list 24h autoupdate WinNTServer/Linux PCSNET" ><img src="https://piramide.zapto.org/i/123enigmaddl.png" /></a>


DIRECT TXT FILE ACCESS:
![maltrailcustomblocklist](https://user-images.githubusercontent.com/27965834/221394264-90eb74a7-0867-4938-89ae-6c2dcc5b5711.jpg)

YOU CAN PUT IN YOUR MALTRAIL CUSTOM URL LIVE LIST IS ON PERC.DDNS.NET STATIC LIST IS ON PIRAMIDE.ZAPTO.ORG 

# FOR MALTRAIL <a href="https://github.com/stamparm/maltrail" title="MalTrail">https://github.com/stamparm/maltrail</a>

Custom trails config put this 

URL: https://perc.ddns.net/iplist-pcsnet.txt 

or live list 

https://perc.ddns.net/iplist.txt 

# example maltrail.conf
<code>
# Use remote custom feed (too) in trail updates
#CUSTOM_TRAILS_URL http://www.test.com/custom.txt
CUSTOM_TRAILS_URL https://perc.ddns.net/iplist-pcsnet.txt
</code>

<a href="https://perc.ddns.net/iplist.txt" title="BadIP List PCSNET"><h1 style="color:green;">https://perc.ddns.net/iplist.txt</h1></a>

<a href="https://piramide.zapto.org/iplist.txt" title="BadIP List PCSNET"><h1 style="color:green;">https://piramide.zapto.org/iplist.txt</h1></a>

OR PRIVATE LIST AUTO-UPDATE PCSNET@2020 CUMULATIVE LIST

<a href="https://perc.ddns.net/iplist-pcsnet.txt" title="BadIP List RealTime-PCSNET"><h1 style="color:green;">https://perc.ddns.net/iplist-pcsnet.txt</h1></a>
<a href="https://piramide.zapto.org/iplist-pcsnet.txt" title="BadIP List PCSNET Comulative"><h1 style="color:green;">https://piramide.zapto.org/iplist-pcsnet.txt</h1></a>

<a href="https://pcsnet.myftp.org/" title="Piramide Studio NET" ><img src="https://piramide.zapto.org/i/education_pcs.png" /></a>

BadIP list for CMS Systems
<a href="https://perc.ddns.net/ip.txt" title="BadIP List for CMS Systems Wordpress/Drupal/Joomla"><h1 style="color:green;">https://perc.ddns.net/ip.txt</h1></a>
<a href="https://perc.ddns.net/cms.txt" title="BadIP List for CMS Systems Wordpress/Drupal"><h1 style="color:green;">https://perc.ddns.net/cms.txt</h1></a>

# Config Fail2Ban for MalTrail

Edit custom filter for example maltrail.conf
```
sudo nano /etc/fail2ban/filter.d/maltrail.conf
```
## How to CONGIGURE MALTRAIL AND FAIL2BAN to block Malware Activity on your server:
## for hostname use your hostname of your server and for IP x\.x\.x\.x use your IP or your server:
```
            ^.*hostname\.com <HOST> \d+ x\.x\.x\.x .*(attacker|scanner|reputation).*
```
# My example no.1:
```
[Definition]

failregex =  ^.*hostname <HOST> \d+ 192\.168\.0\.100 .*(malware|sinkhole|andromeda|potential|attacker|scanner|reputation|suspicious).*

ignoreregex = 

```
# My example no.2:
```
[Definition]

failregex =  ^.*hostname <HOST>.*192.168.0.100 (21|25|110|53|80|443|143|465|993|995|587|10000|8338) (TCP|UDP).*(reputation|malware|malicious|iot-malware|download|andromeda|sinkhole|conficker|potential|remote|code|execution|probe|config|file|access|systembc|xss|injection|non-existent|directory|traversal|php|onion|emotet|cobaltstrike|blacklisted).* 

                        
ignoreregex = 
```
# My example no.3:
```
[Definition]

failregex =  ^.*hostname\.com <HOST> \d+ 192\.168\.0\.100 .*(malware|sinkhole|andromeda|potential|attacker|scanner|reputation|suspicious).*

ignoreregex = 
```
## Custom jail config Maltrail:
```
sudo nano /etc/fail2ban/jail.local
```
Copy this in the end of file
```
[maltrail]

enabled    = true

filter     = maltrail

logpath    = /var/log/maltrail/*-*-*.log

port       = all

maxretry   = 1

bantime    = 1h

banaction  = %(banaction_allports)s

protocol   = all

blocktype  = RETURN

returntype = DROP
```

# Config Fail2Ban for MalTrail login protection
```
sudo nano /etc/fail2ban/filter.d/maltrail.conf
```
```
[INCLUDES]

before = common.conf


[Definition]

_daemon = maltrail-auth

failregex = ^%(__prefix_line)sFailed password for.* from <HOST> port.*

            .*[hostname] maltrail.*Failed password for.* from <HOST> port.*

ignoreregex = .*Failed password for None from <HOST>.*
```
## Custom jail config Maltrail-AUTH:
```
sudo nano /etc/fail2ban/jail.local
```
Copy this in the end of file
```
[maltrail-auth]

enabled    = true

filter     = maltrail-auth

logpath    = %(syslog_authpriv)s

backend    = %(syslog_backend)s

port       = all

maxretry   = 3

bantime    = 1h

banaction  = %(banaction_allports)s

action     = %(action_mwl)s

protocol   = all

blocktype  = RETURN

returntype = DROP

```

