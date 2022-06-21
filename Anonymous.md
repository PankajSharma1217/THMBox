# Anonymous
let's start with scanning ports
![](https://i.imgur.com/q0dtiqP.png)
so we have ftp open with anonymous login
and also  smb port is open

so let's start with smb 
![](https://i.imgur.com/PLOrSnn.png)
i get two pictures of dogs corgo2.jpg and puppos.jpeg .
I scanned it for the known basic stegnographic techniques 
but i got nothing out of it.
so lets move on ftp 
![](https://i.imgur.com/7w9T8f4.png)
  

i found  a shared folder scripts with writing permission
The another interesting thing is a script is already present in there that's executing a code and saving it inside removed_files.log so I thought of manipulating script and getting a reverse shell of it.First i check how much time it is taking to execute clean.sh

![](https://i.imgur.com/ARaClyY.png)

![](https://i.imgur.com/fNRekrj.png)


![](https://i.imgur.com/WSOnopQ.png)

I manipulate to check time of execution of clean.sh and check removed_files.log.
![](https://i.imgur.com/pd8d8Fi.png)
After manipulation pic shows it  takes  1 min in executing clean.sh


### Lets create a reverse shell
![](https://i.imgur.com/SelQN0Q.png)

![](https://i.imgur.com/4AgGr1w.png)

Here we got our user.txt
## 90d6f992585815ff991e68748c414740

### Lets start privilege escalation 

Let's search for suid files
![](https://i.imgur.com/piIMyJw.png)
suid is set on env we can use it to escalate root privilege as follows:
![](https://i.imgur.com/8y6JQcM.png)


![](https://i.imgur.com/qXyEYxT.png)
![](https://i.imgur.com/sybNn4t.png)
## Here we go!
1. we get root access and  root.txt is 
### 4d930091c31a622a7ed10f27999af363

# Alternative Method


![](https://i.imgur.com/KZs76cO.png)
we can see lxd is set to user.In this case we can escalate using below method:

   
# Steps to be performed on the attacker machine:
* Download build-alpine in your local machine through the git repository.
* execute the script “build -alpine” that will build the latest Alpine image as a compressed file, this step must be executed by the root user.
* Transfer the tar file to the host machine

## Steps to   performed on the host machine:
* Download the alpine image
* Import image for lxd
* Initialize the image inside a new container.
* Mount the container inside the /root directory

![](https://i.imgur.com/FnoxuLy.png)

![](https://i.imgur.com/ZDPHTmA.png)

![](https://i.imgur.com/X4cWmS8.png)

![](https://i.imgur.com/UU2AsY6.png)

![](https://i.imgur.com/hmEVpCN.png)
![](https://i.imgur.com/Di4mulf.png)



Here we go !
we gain access using  lxd .

