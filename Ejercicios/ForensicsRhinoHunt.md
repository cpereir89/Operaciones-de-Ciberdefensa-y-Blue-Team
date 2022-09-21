# Ejercicio de Investigación de un Incidente de Seguridad utilizando Forensics y Análisis de Logs

# Escenario Rhino Hunt

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

**Hashes de evidencia:**

* c0d0093eb1664cd7b73f3a5225ae3f30 *rhino.log
* cd21eaf4acfb50f71ffff857d7968341 *rhino2.log
* 7e29f9d67346df25faaf18efcd95fc30 *rhino3.log
* 80348c58eec4c328ef1f7709adc56a54 *RHINOUSB.dd


# Creando el laboratorio

Para este laboratorio necesitamos descargar una distribución de Linux de SANS especializada en Análisis Forense llamada **SIFT**.
Se puede descargar de acá (se deben registrar primero para poder descargarla): https://www.sans.org/tools/sift-workstation/

Seguido de esto, se monta el OVA y se loguean con los credenciales `sansforensics` y la contraseña `forensics`.

Una vez dentro, es necesario descargar un archivo .zip que contiene los elementos necesarios para correr el escenario.

Este archivo lo pueden encontrar en https://cfreds.nist.gov/all/NIST/RhinoHunt o lo pueden descargar usando:

```
wget https://cfreds-archive.nist.gov/dfrws/DFRWS2005-RODEO.zip
```
Una vez descargado lo extraen usando la interfaz gráfica o corriendo:

```
unzip DFRWS2005-RODEO.zip
```

# Montando la imagen USB

Una vez descomprimido es necesario montar la imagen USB `RHINOUSB.dd` en algún punto de nuestra máquina NIFT.

Para hacer esto corremos el comando:

```
sudo mount -o  ro RHINOUSB.dd /mnt/usb/
```

Seguido de esto podemos movernos a la carpeta /mnt/usb/ para explorar el contenido de la imagen.


# Realizando algunos ejercicios del escenario

## Comprobando la integridad de la evidencia

El primer paso a realizar una vez recibida la evidencia es verificar la integridad de la cadena de custodia. Es necesario asegurarse que los archivos no han sido modificados previo a investigarlos.

Para hacer esto extraemos el hash md5 de cada archivo y los comparamos con lo que se nos presenta como parte del escenario:

```
md5sum rhino* RHINOUSB.dd 
cd21eaf4acfb50f71ffff857d7968341  rhino2.log
7e29f9d67346df25faaf18efcd95fc30  rhino3.log
c0d0093eb1664cd7b73f3a5225ae3f30  rhino.log
80348c58eec4c328ef1f7709adc56a54  RHINOUSB.dd
```

## Investigando la imagen USB con un editor Hexadecimal

Antes de empezar a trabajar con la imagen USB, procedemos a analizarla con un editor hexadecimal.
En SIFT podemos usar la herramienta **GHex** para abrir el archivo.

Después de abierto podemos verificar que una gran cantidad del disco tiene 0s, esto nos da una pista de que se ha intentando sobrescribir información. También podemos encontrar varios varios bloques de bytes con las palabras **CHARLIE** y **SORRY**. 
Otro indicador de que se ha intentado esconder evidencia.


## Investigar los contenidos de la llave USB recuperada

Al investigar el contenido de la llave USB, encontramos 2 archivos:

```
sansforensics@siftworkstation: /mnt/usb
$ ls -lh
total 8.0K
-rwxr-xr-x 1 root root 2.8K Apr 30  2004 gumbo1.txt
-rwxr-xr-x 1 root root 1.3K Apr 30  2004 gumbo2.txt
```

Al investigar ambos archivos no hay mayor evidencia. Son 2 recetas. Esto quiere decir que alguien borro la información de la llave USB.

## Recuperar archivos borrados de la llave USB: ¿Qué se puede recuperar de la imagen dd de la llave USB?

Para recuperar información se puede utilizar la utilidad **foremost**.

Primero creamos una carpeta donde vamos a alojar los archivos recuperados:

```
mkdir output
```

Seguido de esto corremos foremost. Indicamos la carpeta donde vamos a guardar los archivos y la imagen del disco usb como parte de los parámetros:

```
$ foremost -o output/ RHINOUSB.dd 
Processing: RHINOUSB.dd
|***|

```

Nos vamos a la carpeta **output** y ahí vamos a poder encontrar los verdaderos archivos que contienen evidencia.


## Resolviendo la pregunta: ¿Qué pasó con el disco duro de la computadora? ¿Donde está ahora?

Nos vamos dentro de la carpeta **doc** y abrimos el archivo de Word. Al final la persona indica que lo tiró al Río Mississippi:

<img width="741" alt="Captura de Pantalla 2022-09-21 a la(s) 12 07 13" src="https://user-images.githubusercontent.com/52690024/191578881-cdf3cb7b-08e0-4033-a70c-f2491625cc53.png">



