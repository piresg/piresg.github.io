---
title: "SMB Relay Attack"
#date: 2022-10-01T18:13:02+01:00
draft: false
tags:
  - Active Directory
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

- #### SMB Signing Disabled

`nmap -x`
