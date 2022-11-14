---
title: "Powerview"
#date: 2022-10-01T18:13:02+01:00
draft: false
tags:
  - Active Directory
  - Enumeration
---

## Activar PowerView

### Desabilitar _Execution policy_ e carregar script

```
powershell -ep bypass
```

```
PS C:\Users\jcid> powershell -ep bypass
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\jcid>

```

```
. .\PowerView.ps1
```

## Comandos Uteis

### Informação de Dominio

- Get-NetDomain
- Get-NetDomainConroller

```
Forest                  : insecure.local
DomainControllers       : {DC01.insecure.local}
Children                : {}
DomainMode              : Unknown
DomainModeLevel         : 7
Parent                  :
PdcRoleOwner            : DC01.insecure.local
RidRoleOwner            : DC01.insecure.local
InfrastructureRoleOwner : DC01.insecure.local
Name                    : insecure.local



PS C:\Users\jcid\Desktop> Get-NetDomainController


Forest                     : insecure.local
CurrentTime                : 11/14/2022 7:20:47 PM
HighestCommittedUsn        : 65695
OSVersion                  : Windows Server 2019 Standard Evaluation
Roles                      : {SchemaRole, NamingRole, PdcRole, RidRole...}
Domain                     : insecure.local
IPAddress                  : 192.168.0.200
SiteName                   : Default-First-Site-Name
SyncFromAllServersCallback :
InboundConnections         : {}
OutboundConnections        : {}
Name                       : DC01.insecure.local
Partitions                 : {DC=insecure,DC=local, CN=Configuration,DC=insecure,DC=local, CN=Schema,CN=Configuration,DC=insecure,DC=local, DC=DomainDnsZones,DC=insecure,DC=local...}


```

### Informação de Politicas de Dominio

```
Get-DomainPolicy
```

```
Unicode : @{Unicode=yes}
SystemAccess : @{MinimumPasswordAge=1; MaximumPasswordAge=42; MinimumPasswordLength=7; PasswordComplexity=1; PasswordHistorySize=24; LockoutBadCount=0; RequireLogonToChangePassword=0; ForceLogoffWhenHourExpire=0; ClearTextPassword=0; LSAAnonymousNameLookup=0}
KerberosPolicy : @{MaxTicketAge=10; MaxRenewAge=7; MaxServiceAge=600; MaxClockSkew=5; TicketValidateClient=1}
RegistryValues : @{MACHINE\System\CurrentControlSet\Control\Lsa\NoLMHash=System.Object[]}
Version : @{signature="$CHICAGO$"; Revision=1}
Path : \\insecure.local\sysvol\insecure.local\Policies\{31B2F340-016D-11D2-945F-00C04FB984F9}\MACHINE\Microsoft\Windows NT\SecEdit\GptTmpl.inf
GPOName : {31B2F340-016D-11D2-945F-00C04FB984F9}
GPODisplayName : Default Domain Policy

```

```
(Get-DomainPolicy)."Systemaccess"
```

```
MinimumPasswordAge : 1
MaximumPasswordAge : 42
MinimumPasswordLength : 7
PasswordComplexity : 1
PasswordHistorySize : 24
LockoutBadCount : 0
RequireLogonToChangePassword : 0
ForceLogoffWhenHourExpire : 0
ClearTextPassword : 0
LSAAnonymousNameLookup : 0

```

### informação de utilizadores

- Get-NetUser | select cn, samaccountname, description

```
cn            samaccountname description
--            -------------- -----------
Administrator Administrator  Built-in account for administering the computer/domain
Guest         Guest          Built-in account for guest access to the computer/domain
krbtgt        krbtgt         Key Distribution Center Service Account
Peter Parker  pparker
SQL Service   SQLService     Password: MYpassword123!
Jose Cid      jcid
Rao Kyao      rkyao
admin         admin
VTPZPhHNiK    VTPZPhHNiK
ynyICBEMvl    ynyICBEMvl
```

- Get-Netuser |select samaccountname, pwdlastset, logoncount

```
samaccountname pwdlastset             logoncount
-------------- ----------             ----------
Administrator  10/27/2022 11:16:07 AM         61
Guest          1/1/1601 12:00:00 AM            0
krbtgt         10/27/2022 11:57:29 AM          0
pparker        10/27/2022 3:25:45 PM          13
SQLService     10/27/2022 3:27:35 PM           0
jcid           10/28/2022 2:53:03 PM          40
rkyao          10/28/2022 2:53:51 PM          32
admin          11/2/2022 11:23:33 AM          53
VTPZPhHNiK     11/14/2022 12:29:54 PM          0
ynyICBEMvl     11/14/2022 12:38:57 PM          0
```

### Informação de maquinas

- Get-NetComputer
- Get-NetComputer | select samaccountname, operatingsystem, lastlogontimestamp

```
samaccountname operatingsystem                         lastlogontimestamp
-------------- ---------------                         ------------------
DC01$          Windows Server 2019 Standard Evaluation 11/7/2022 10:19:21 AM
WS01$          Windows 10 Enterprise Evaluation        11/8/2022 2:23:50 PM
WS02$          Windows 10 Enterprise Evaluation        11/14/2022 9:34:41 AM


```

### informação de Grupos

- Get-NetGroup
- Get-NetGroup | select samaccountname

```
samaccountname
--------------
Administrators
Users
Guests
Print Operators
Backup Operators
Replicator
Remote Desktop Users
Network Configuration Operators
Performance Monitor Users
Performance Log Users
Distributed COM Users
IIS_IUSRS
Cryptographic Operators
Event Log Readers
Certificate Service DCOM Access
RDS Remote Access Servers
RDS Endpoint Servers
RDS Management Servers
Hyper-V Administrators
Access Control Assistance Operators
Remote Management Users
Storage Replica Administrators
Domain Computers
Domain Controllers
Schema Admins
Enterprise Admins
Cert Publishers
Domain Admins
Domain Users
Domain Guests
Group Policy Creator Owners
RAS and IAS Servers
Server Operators
Account Operators
Pre-Windows 2000 Compatible Access
Incoming Forest Trust Builders
Windows Authorization Access Group
Terminal Server License Servers
Allowed RODC Password Replication Group
Denied RODC Password Replication Group
Read-only Domain Controllers
Enterprise Read-only Domain Controllers
Cloneable Domain Controllers
Protected Users
Key Admins
Enterprise Key Admins
DnsAdmins
DnsUpdateProxy
```

## Download

https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1

## Cheat Sheet

https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993
