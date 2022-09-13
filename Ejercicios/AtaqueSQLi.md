# Ataque de SQL Injection

En la página de Metasploitable puede utilizar BurpSuite para interceptar los requests del servidor.

Para evaluar como reacciona el servidor a diferentes peticiones que contengan cadenas de caracteres de SQLi puede usar las siguientes listas:

https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/SQLi/Generic-SQLi.txt​
https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/SQLi/quick-SQLi.txt​
https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/SQLi/Generic-BlindSQLi.fuzzdb.txt


Guardar peticiones al servidor web de la siguiente forma:

```
Click derecho en las peticiones que contengan parametros.
Seleccionar "Save Item".
Nombrar el archivo y guardarlo.
```


En la vista de Proxy History en Burp Suite hacer click derecho para guardar las peticiones al servidor.

Con la herramienta **SQLMap** cargar las peticiones utilizando el flag `-r`:

```
sqlmap -r <archivo de peticion>
```

Puede utilizar el flag --dump para descargar la base de datos, romper contraseñas inseguras en las bases de datos, etc.


```
sqlmap -r <archivo de peticion> --dump
```

