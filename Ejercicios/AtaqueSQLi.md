# Ataque de SQL Injection

En la página de Metasploitable puede utilizar BurpSuite para interceptar los requests del servidor.

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

