---
title: "Enumeration SMB"
#date: 2022-10-28T18:13:02+01:00
draft: false
tags:
  - Enumeration
  - SMB
---

### Anonymous Logon

`nmap --script safe -445 10.10.10.100`

`smbmap -u "" -p "" -P 445 -H 10.129.120.220`

`smbclient //10.129.120.220/Replication`
`smbclient -L //10.10.10.100/Share`

### Listing Files recursive

```bash
recurse on
ls

smbmap -R Replication -H 10.129.5.41
```

### Directory Listing with credentials

smbmap -u svc_tgs -p GPPstillStandingStrong2k18 -d ACTIVE.HTB -H 10.129.120.220

Listing Files with credentials recursive

smbmap -R -H 10.129.5.41 -u svc_tgs -p GPPstillStandingStrong2k18 -d active.htb

smbclient //10.10.10.100/Share
Dowload all file
RECURSE ON
PROMPT OFF
mget \*

SMB version 2 is running, and message signing is enabled - prevents SMB Relay Atacks

Mount Share

sudo apt-get install cifs-utils
mkdir /mnt/Replication
mount -t cifs //10.10.10.100/Replication /mnt/Replication -o
username=<username>,password=<password>,domain=active.htb
grep -R password /mnt/Replication/
