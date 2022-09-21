# Ejercicio de Forensics utilizando el escenario de Rhino Hunt

Este ejercicio simula un escenario ficticio donde se ha cometido un delito informático y se deben encontrar respuestas a ciertas preguntas propuestas.

Traducido del sitio oficial, este es el escenario:

```
La ciudad de Nueva Orleans aprobó una ley en 2004 que convierte en delito grave la posesión de nueve o más imágenes únicas de rinocerontes.   
El administrador de red de la Universidad de Nueva Orleans alertó recientemente a la policía cuando su instancia de RHINOVORE detectó el tráfico   
ilegal de rinocerontes. La evidencia en el caso incluye una computadora y una llave USB incautadas de uno de los laboratorios de la Universidad.   
Desafortunadamente, la computadora no tenía disco duro. Se creó una imagen de la llave USB y hay una copia de la imagen dd en el CD-ROM que le dieron.  
Además de la imagen de la unidad de llave USB, también están disponibles tres logs de red: estos fueron proporcionados por el administrador de la   
red e involucran a la máquina a la que le falta el disco duro.   

El sospechoso es el principal usuario de esta máquina, que ha estado realizando su doctorado en la Universidad desde 1972.

```

Se plantean algunas preguntas y objetivos:

Recupere al menos nueve imágenes de rinocerontes de la evidencia disponible e inclúyalas en un breve informe.
En su informe, proporcione respuestas a tantas de las siguientes preguntas como sea posible:  

* ¿Quién le dio al acusado una cuenta telnet/ftp?
* ¿Cuál es el nombre de usuario/contraseña de la cuenta?
* ¿Qué transferencias de archivos relevantes aparecen en los seguimientos de la red?
* ¿Qué pasó con el disco duro de la computadora? ¿Donde esta ahora?
* ¿Qué pasó con la llave USB?
* ¿Qué se puede recuperar de la imagen dd de la llave USB?
* ¿Hay alguna evidencia que conecte la llave USB y los rastros de la red? Si es así, ¿qué?


# Creando el laboratorio

Para este laboratorio necesitamos descargar una distribución de Linux de SANS especializada en Análisis Forense llamada **SIFT**.
Se puede descargar de acá (se deben registrar primero para poder descargarla): https://www.sans.org/tools/sift-workstation/

Seguido de esto, se monta el OVA y se loguean con los credenciales `sansforensics` y la contraseña `forensics`.

Una vez dentro, es necesario descargar un archivo .zip que contiene los elementos necesarios para correr el escenario.

Este archivo lo pueden encontrar en https://cfreds.nist.gov/all/NIST/RhinoHunt o lo pueden descargar usando:

```
wget https://cfreds-archive.nist.gov/dfrws/DFRWS2005-RODEO.zip

Una vez descargado lo extraen usando la interfaz gráfica o corriendo:

```
unzip DFRWS2005-RODEO.zip
```




Una vez descomprimido es necesario montar la imagen USB `RHINOUSB.dd` en algún punto de nuestra máquina NIFT.

Para hacer esto corremos el comando:

```
sudo mount -o  ro RHINOUSB.dd /mnt/usb/


