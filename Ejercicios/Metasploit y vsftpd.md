# Uso de Metasploit para atacar vsftpd

Correr Nmap para determinar el tipo de servidor FTP presente:

`nmap -p 21 192.168.100.93 -A`  

Lo que nos entrega los siguientes resultados:  

`Starting Nmap 7.92 ( https://nmap.org ) at 2022-09-08 19:00 EDT
Nmap scan report for 192.168.100.93
Host is up (0.00080s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.3.4
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.100.99
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
Service Info: OS: Unix

Service detection performed. Please report any incorrect results a/ .
Nmap done: 1 IP address (1 host up) scanned in 0.76 seconds
zsh: segmentation fault  nmap -p 21 192.168.100.93 -A`  

