# Comandos y Herramientas - Operaciones de Ciberdefensa y Blue Team

###  Comandos Básicos de Linux
`apt update`  
`apt upgrade`  
`apt install <nombre del paquete>`   
`apt remove <nombre del paquete>`  
`apt list - Listar paquetes instalados, disponibles`  

___
 
`Control + A`: ir al inicio de una línea  
`Control + E`: ir al final de una línea  
`clear`: borrar la pantalla  
`| "Pipe" `: envía la salida de un aplicativo a otro  
`; `: ejecuta varios comandos en una sóla línea  
`pwd`: muestra el directorio donde se está trabajando  
`cd`: cambia de directorio  
`ls`: lista los archivos y directorios (similar a dir en Windows)  
`open <archivo>`: abre un archivo con el programa por defecto para abrir ese tipo de archivo. Si se utiliza open . nos abre el directorio en  el que estamos.  
`mkdir`: crear un directorio  
`rm`: borrar un archivo. Con el flag -r se borran directorios  
`sudo`: nos permite ejecutar comandos como si fueramos otro usuario  
___
### Aplicativos de uso común
#### man
Despliega un manual de usuario de un aplicativo. Ejemplo:
`man <programa>`  
#### nano
Es un editor de texto en la terminal.
Abrir un archivo en nano:
`nano <archivo>`
Salir y guardar cambios:
`Control + X`
Y
`Enter`

#### vim
Otro editor de texto en la terminal.
`vim <archivo>  `

#### less/more
Nos permite abrir un archivo de texto, sin poder editarlo.
`less <archivo>`
Nos podemos salir con `q`.
Podemos buscar dentro del archivo usando `/` y luego escribiendo lo que vamos a buscar.

#### head/tail
Nos despliega las primeras o últimas líneas de un texto. Por defecto son las primeras o últimas 10.
`head <archivo>`
`head -n 15 <archivo>`
`tail -n 30 <archivo>`

#### grep
Es un aplicativo que nos permite encontrar texto dentro de archivos.  
`grep "palabras a buscar" <archivo>`  
Hacer una búsqueda inversa:  
`grep -v "líneas que no hagan match con un patrón" <archivo>  
Este aplicativo se puedo utilizar muy a menudo con pipe, para filtrar el resultado de un programa.  

#### screen
Es un aplicativo que nos permite ejecutar un programa en sesiones secundarias o virtuales. Es muy útil cuando por ejemplo estamos utilizando una conexión por SSH en un servidor para ejecutar tareas que toman mucho tiempo y evitar que en caso de perder la conexión se pierda el progreso.  
Crear una sesión:  
`screen -S <nombre de una sesión>`  
Salirse (no cerrar) de una sesión:  
`Control + a + d`  
Volver a una sesión  
`screen -r <nombre de la sesión>`  
Cerrar una sesión (mientras se está dentro de ella):  
`exit`  

___
## Escaneo de Redes
### tcpdump
Es una herramienta que nos permite capturar tráfico.  
Capturar tráfico de una interfaz específica:  
`tcpdump -i eth0`  
Capturar un cierto número de paquetes:  
`tcpdump -c 5-i eth0`  
Capturar y mostrar paquetes en formato ASCII:  
`tcpdump -i eth0 -A`  
Especificar el puerto:  
`tcpdump -i eth0 port 22`  
Especificar destino u origen:  
`tcpdump -i eth0 dst x.x.x.x  
tcpdump -i eth0 src x.x.x.x`  
Guardar la captura en un archivo:  
`tcpdump -i eth0 -w <nombre del archivo>`


### Nmap

Es una de las herramientas más poderosas para realizar escaneos y auditorías de seguridad. Esta herramienta viene instalada por defecto en las distribuciones de Kali.  
Se puede utilizar en Linux, Windows y macOS. Podemos encontrar una versión alternativa con interfaz gráfica llamada Zenmap.  
Escaneo de ping. Para ver qué equipos están disponibles.  
`nmap -sP 10.10.10.0/24`  
Escaneo básico  
`nmap 10.10.10.1`  
Escaneo básico sin ping  
`nmap 10.10.10.1 -Pn`  
Escaneo básico especificando puertos. Ejemplo, puertos del 80, 443 y 3389:  
`nmap 10.10.10.1 -p 80,443,3389`  
Escaneo básico especificando rango de puertos. Ejemplo, puertos del 1 al 1024:  
`nmap 10.10.10.1 -p 1-1024`  
Escaneo de puertos UDP  
`nmap -sU 10.10.10.1`  
Escaneo que nos entrega información del sistema operativo del objetivo  
`nmap -o 10.10.10.1`  
Escaneo que nos agrega información de los servicios detrás de cada puerto  
`nmap -sV 10.10.10.1`  
Escaneo utilizando scripts. Referencia de todos los scripts disponibles: https://nmap.org/nsedoc/scripts/  
`nmap -sV --script=<nombre del script> 10.10.10.1`  
Exportar los resultados de un escaneo a varios formatos  
`nmap  10.10.10.1 -oA <nombre del archivo>`  



___
## Escaneo de Aplicaciones Web

### whatweb - https://github.com/urbanadventurer/WhatWeb
Nos sirve para realizar escaneos básicos de servidores web. 
Escaneo básico:  
`./whatweb <URL>`  
Escaneo verbose:  
`./whatweb <URL> -v`  

### nikto
Es una herramienta de escaneo de servidores web que viene por defecto en las distribuciones de Kali Linux.
Escaneo básico:
`nikto -h <URL>`

### jwt tool: https://github.com/ticarpi/jwt_tool
Esta herramiena sirve para analizar los JWT Tokens que son usualmente encontrados en sistemas de autenticación de páginas web o APIs.
Uso general:
`./jwt_tool.py <JWT Token>`  
Ejemplo:  
`./jwt_tool.py eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`

### Add-ons para Firefox

#### Wappalizer - https://addons.mozilla.org/es/firefox/addon/wappalyzer/
La versión gratuita permite ver las tecnologías usadas en la página web.
#### FoxyProxy - https://addons.mozilla.org/es/firefox/addon/foxyproxy-standard/
Permite agregar y cambiar los proxys facilmente para trabajar con Burp u otras herramientas.  

___
## Escaneo de Servicios SSH
### SSH Audit - https://github.com/jtesta/ssh-audit  
`./ssh-audit.py <URL o IP>`  

___
## Escaneo de Configuraciones SSL/TLS

### testssl - https://github.com/drwetter/testssl.sh
`./testssl.sh  <URL o IP>`  
Recuerde que por defecto se conecta al puerto 443, pero puede especificar otro con `./ssh-audit.py <URL>:<puerto>`.  
Ejemplo:  
`./testssl.sh 127.0.0.2:8080`

### openssl
Otra heramienta que viene por defecto en la mayoría de distribuciones de UNIX/Linux.
Verificar la conexión SSL/TLS a un servidor:
`openssl s_client -connect <URL>:443`  
 Ejemplo:  
 `openssl s_client -connect google.com:443`  
 Revisar los certificados:  
 `openssl s_client -connect <URL>:<puerto> -showcerts`
 


