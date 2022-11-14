---
title: "BloodHound"
#date: 2022-10-01T18:13:02+01:00
draft: false
tags:
  - Active Directory
  - Enumeration
---

## Instalação

A ferramenta _BloodHound_ tem como requisito a instalação de uma base de dados _Neo4J_. Dependendo da versão java instalada poderão ter problemas em correr a ferramenta, visto que apenas é suportada a versão 11 do JDK.

Os passos abaixo ajudam na configuração do ambiente.

- **sudo apt install bloodhound**

  - Instala os pacotes necessários

- **java --version**

  - para confirmarmos a versão

- sudo update-alternatives --config java
- sudo update-alternatives --config javac

- sudo apt-cache search openjdk
  - Caso o OpenJDK11 não esteja disponivel

## Inicialização

- **sudo neo4j console**
- **bloodhound**
