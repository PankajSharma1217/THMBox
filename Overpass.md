# Overpass

## Nmap
PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    syn-ack Golang net/http server

## Gobuster

##### Gobuster v2.0.1              OJ Reeves (@TheColonial)
=====================================================
##### [+] Mode         : dir
##### Url/Domain   : http://10.10.198.246/
##### Threads      : 100
##### Wordlist     : /home/mikey/wordlists/common.txt
##### Status codes : 200,204,301,302,307,403
##### Timeout      : 10s
=====================================================
##### 2022/06/23 22:47:51 Starting gobuster
=====================================================
/aboutus (Status: 301)
/admin (Status: 301)
/css (Status: 301)
/downloads (Status: 301)
/img (Status: 301)
/index.html (Status: 301)

# Web Exploitation

![](https://i.imgur.com/LbVyNbb.png)

Let's check source code

![](https://i.imgur.com/97251pr.png)

we can see three interesting scripts.Let's check them out

![](https://i.imgur.com/E3oknpB.png)

so there is a flow in the script can see ( Broken Authentication  )  for more ,let's set cookie as 
SessionToken and see if it works! 

![](https://i.imgur.com/CnB3Elw.png)

we logged in as admin.We can see ssh private key of user James.

## SSH 

![](https://i.imgur.com/HpNUbJS.png)

But it is protected by passphrase let's try to crack it with john using rockyou.txt

![](https://i.imgur.com/YeDdVfZ.png)

Cracked ,we get james13 passphrase.

![](https://i.imgur.com/wdzuNaX.png)
#### User.txt is thm{65c1aaf000506e56996822c6281e6bf7}

## Privilege Escalation

Let's check crontab 
![](https://i.imgur.com/u9jrEPn.png)
It is executing buildscript.sh. Check if we can change server and execute our script for root access.

![](https://i.imgur.com/Gr4BOA3.png)
/etc/hosts have writing access by user .

We can see in /etc/hosts it is set to localhost let's change it with our ip .




