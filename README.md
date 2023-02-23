# Tech_Supp0rt: 1

## Hack into the machine and investigate the target.

I started of this challenge by running ana nmap scan also ran a gobuster scan.
```
nmap -sV -sC <IP_Machine>
```
```
gobuster dir -w /usr/share/wordlists/dirb/big.txt -u <IP_Machine>
```
The nmap scan came back and I quickly noticed that there was an smb server present.

Host Scripts Results:

account_used: guest

authentication_level: user

After many failed attempts of trying to make the credentials work with 
the smbclient command I searched online and found a command to connect.

```
smbclient //<Machine_IP>/websvr
```

Here I was into the smb server client
From here I used an 'ls' command and saw that there was an 'enter.txt' file.
I used a 'get' command to download the file onto my host machine.
After I opened the file on my machine it read:
______________________________________________________________________
```
Goals
=====
1)Make fake popup and host it online on Digital Ocean server

2)Fix subrion site, /subrion doesn't work, edit from panel

3)Edit wordpress website

IMP
===
Subrion creds

|->admin:7sKvntXdPEJaxazce9PXi24zaFrLiKWCk [cooked with magical formula]

Wordpress creds

|->
```
_______________________________________________________________________

Reading this file I see that the 'subrion/' looks like a directory on the webpage. 
There also looks to be a username and a password. (If you put the password into
cyberchef and cook it with the magic decryption which comes out to 'Scam2021')

I tried to put the subrion/ onto the end of browser search and came 
up with a directory along with a /robots.txt after it.

http://<IP_Machine>/subrion/robots.txt
with these directories >> 
______________________________________________________________________
User-agent: *

Disallow: /backup/

Disallow: /cron/?

Disallow: /front/

Disallow: /install/

Disallow: /panel/

Disallow: /tmp/

Disallow: /updates/
_________________________________________________________________________

I tried to input all of these and the one that looked most interesting
was the '/panel/' page because we already have a username and a password.

After logging in it appears we could be able to run an exploit and get a shell on this machine.

I searched for the version on exploit-db and found there was one I could use.

"Subrion CMS 4.2.1 - Arbitrary File Upload"

I then downloaded it to my machine.


