#             Develpy

## Nmap
 
 PORT      STATE  SERVICE           VERSION
22/tcp     open   ssh               OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)

10000/tcp open  snet-sensor-mgmt?

## Netcat
   
   lets connect with port 10000 
   
   ![](https://i.imgur.com/LSKr3Lw.png)
   

so a python script is running asking for a input.
it is calculating given equation hinting that there is input vulnerbility,read more at https://intx0x80.blogspot.com/2017/05/python-input-vulnerability_25.html

## Reverse_Shell
so let's create a payload to spawn a shell

![](https://i.imgur.com/blvUrBn.png)

Here we go we spawn a reverse shell

![](https://i.imgur.com/WNlBvpY.png)

##### But the spawn shell is not stable. So let's take ssh connection by uploading our public ssh key.

![](https://i.imgur.com/KbaCPEQ.png)


![](https://i.imgur.com/v62NkCQ.png)


## Privilege Escalation

Let's escalate our privilege

#### The root.sh file seem's suspected.Let's check cronjobs

![](https://i.imgur.com/vYWwNGU.png)

#### This file is being executed and other interesting thing that we have access to rm files in this directory..

Let's remove root.sh file and spawn a root shell using reverse shell payload given below and saving it with name root.sh


![](https://i.imgur.com/N8rXWPw.png)

### Here we go

![](https://i.imgur.com/fbFv3Ml.png)

Here we get our root.txt 


#### 9c37646777a53910a347f387dce025ec


