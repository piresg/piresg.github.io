---
title: "SMB Relay Attack"
#date: 2022-10-01T18:13:02+01:00
draft: false
tags:
  - Active Directory
  - SMB
---

## Definição

Em vez de capturarmos as _hashes_ e tentarmos extrair a password podendo não existir sucesso devido à complexidade da password.
Este ataque usa a _Hash_ capturada e usa a mesma para ganhar acesso noutra maquina, fazendo _relay_ da _hash_.

### Requisitos

- _SMB Signing_ tem estar _disabled_;
- O user _relayed_ tem de ser administrator das maquinas envolvidas.

## Enumeração

# SMB Signing Disabled

`nmap -x`
