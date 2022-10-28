---
title: "LLMNR Poisoning"
#date: 2022-10-28T18:13:02+01:00
draft: false
tags:
  - Active Directory
  - Poisoning & Spoofing
  - NTLMV2
  - MITM
---

**LLMNR** é um acrónimo de _Link-Local Multicast Resolution_, está activo por defeito e é usado para resolução de nomes quando não existe resposta do DNS ao pedido.

Na pratica é enviado, em ultimo recurso, um pedido para todo o segmento de rede onde a máquina se encontra **(_broadcast_)** para que o pedido seja satisfeito por alguem que esteja na mesma rede.

## Teste

![](hashcat_ntml.png)
