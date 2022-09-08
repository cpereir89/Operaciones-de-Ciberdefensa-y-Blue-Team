# Ataque de Enumeración de Usuarios en un servidor SSH

Ejecutamos Nmap para hacer un reconocimiento del servidor SSH presente en Metasploitable 2.  

```
nmap -p 22 192.168.100.93 -A

Starting Nmap 7.92 ( https://nmap.org ) at 2022-09-08 19:27 EDT
Nmap scan report for 192.168.100.93
Host is up (0.00063s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey: 
|   1024 60:0f:cf:e1:c0:5f:6a:74:d6:90:24:fa:c4:d5:6c:cd (DSA)
|_  2048 56:56:24:0f:21:1d:de:a7:2b:ae:61:b1:24:3d:e8:f3 (RSA)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.51 seconds
```
