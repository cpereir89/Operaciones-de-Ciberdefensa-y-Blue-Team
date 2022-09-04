# Curso Ciber Defensa y Atención a Incidentes

## Comandos Básicos de Linux
`apt update`  
`apt upgrade`  
`apt install <nombre del paquete>`   
`apt remove <nombre del paquete>`  
`apt list - Listar paquetes instalados, disponibles `´  
 
`Control + A: `ir al inicio de una línea  
`Control + E: `ir al final de una línea  
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
`grep -v "líneas que no hagan match con un patrón" <archivo>`
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


## Escaneo de Redes

### Nmap


## Escaneo de Aplicaciones Web

### whatweb

### nikto

### jwt tool: https://github.com/ticarpi/jwt_tool

### Whatweb - https://github.com/urbanadventurer/WhatWeb
### Wappalizer - https://addons.mozilla.org/es/firefox/addon/wappalyzer/
### FoxyProxy - https://addons.mozilla.org/es/firefox/addon/foxyproxy-standard/


## Escaneo de Servicios SSH
### SSH Audit

## Escaneo de Configuraciones SSL/TLS
### testssl
### openssl



