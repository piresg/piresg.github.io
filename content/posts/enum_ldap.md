---
title: "Enumeration LDAP"
#date: 2022-10-01T18:13:02+01:00
draft: false
tags:
  - Enumeration
  - LDAP
---

### Anonymous Search

`python3 windapsearch.py -d htb.local -u "" -p "" --dc-ip 10.129.139.154 -U`

`python3 windapsearch.py -d htb.local -u "" -p "" --dc-ip 10.129.139.154 -U --custom "objectClass=\*"`

### Get AD Users (with credentials)

ldapsearch -x -H ldap://10.129.5.52:389 -D svc_tgs -w GPPstillStandingStrong2k18 -b "DC=active,DC=htb" -s sub "(&(objectCategory=person)(objectClass=user) (!(useraccountcontrol:1.2.840.113556.1.4.803:=2)))" samaccountname | grep sAMAccountName

### Get Users with SPN associated (with credentials)

ldapsearch -x -H ldap://10.129.5.52:389 -D SVC*TGS -w GPPstillStandingStrong2k18 -b "dc=active,dc=htb" -s sub "(&(objectCategory=person)(objectClass=user)(!(useraccountcontrol:1.2.840.113556.1.4.803:=2))(serviceprincipalname=*/\_))" serviceprincipalname | grep -B 1 servicePrincipalName

```bash

echo 1


```
