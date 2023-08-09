---
title: Title
date: 2023-07-08 16:53:00 +/-TTTT
categories: [Easy]
tags: []     # TAG names should always be lowercase
img_path: 
image: 
---

Máquina Windows de categoría fácil con:
- Enumeración SMB

## **Enumeración**
### **Nmap**
Empleando el comando `nmap -p- --open 10.10.10.100` podemos escanear todo el rango de puertos existentes y que solo nos reporte los puertos abiertos de la máquina.

Agregando las flags `-sC` y `-sV` a los puertos descubiertos, podemos lanzar una serie de scripts básicos de reconocimiento para ver los servicios que corren para esta máquina y sus respectivas versiones.

```bash
nmap -p 53,88,135,139,389,445,464,593,636,3268,3269,5722,9389,47001,49152,49153,49154,49155,49157,49158,49165,49166,49168 -sC -sV -oN target.txt 10.10.10.100
```

```
Nmap scan report for 10.10.10.100
Host is up (0.18s latency).
```

Gracias a que vemos los servicios de DNS, Kerberos, SMB y LDAP expuestos, podemos deducir que nos encontramos ante un DC (Domain Controller).

> Con el comando `crackmapexec smb 10.10.10.100` podemos ver información relevante del DC.
{: .prompt-tip }

![DC_details](Pasted image 20230702170151.png)
- OS: **Windows 6.1 x64**
- Nombre: **DC**
- Dominio: **active.htb**

> Debido a que nos encontramos ante una máquina de Directorio Activo debemos agregar el dominio (active.htb) al archivo _/etc/hosts_ de nuestra máquina de atacante.
{: .prompt-warning}

## **Explotación**

## **Escalada de Privilegios**

pwned!