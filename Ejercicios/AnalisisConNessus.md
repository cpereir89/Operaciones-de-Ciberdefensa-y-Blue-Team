# Instalación de Nessus

Descargue la versión de Nessus necesaria de https://www.tenable.com/downloads/nessus?loginAttempted=true.  

Para **Kali** puede utilizar la versión **Nessus-10.3.0-debian9_amd64.deb**.

Instale Nessus con el siguiente comando:

```
dpkg -i Nessus-10.3.0-debian9_amd64.deb  
```

Para iniciar Nessus ejecute:
```
/bin/systemctl start nessusd.service
```

Seguidamente navegue a https://127.0.0.1:8834/ y seleccione la opción de Nessus a correr. 

Puede generar una licencia de prueba de 7 días para Nessus acá: https://www.tenable.com/products/nessus/nessus-professional/evaluate

Después de seleccionar cualquiera de las 2 opciones, debe crear un usuario y contraseña para utilizar la instancia de Nessus.

Una vez finalizado este proceso, Nessus va a descargar los plugins necesarios, esto puede tomar algún tiempo en completarse.

