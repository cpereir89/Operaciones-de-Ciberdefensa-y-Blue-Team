# Instalación de AlphaSOC Flightsim en Kali

1. Instalar Go:
```
apt install golang-go 
```

2. Descargar AlphaSOC Flightsim de https://github.com/alphasoc/flightsim/releases/tag/v2.2.2

    2.1 Escoger la versión apropiada para Kali: **flightsim_2.2.2_linux_amd64.tar.gz**
    
    2.2 Puede simplemente correr:
    ```
    wget https://github.com/alphasoc/flightsim/releases/download/v2.2.2/flightsim_2.2.2_linux_amd64.tar.gz
    ```

3. Descomprimir el archivo .tar utilizando el comando 
```
tar xvzf flightsim_2.2.2_linux_amd64.tar.gz
```

4. Ejecutar flightsim con:
```
./flightsim run
```

# Instalación de Suricata en Kali
1. Utilizar el comando:
```
sudo apt -y install suricata
sudo suricata-update
```


# Alternativa: Utilizar SELKS
SELKS es una solución que integra varias herramientas para montar un SIEM utilizando Docker. Tiene los siguientes componentes:

S - Suricata IDPS/NSM - https://suricata.io/  
E - Elasticsearch - https://www.elastic.co/products/elasticsearch  
L - Logstash - https://www.elastic.co/products/logstash  
K - Kibana - https://www.elastic.co/products/kibana  
S - Scirius - https://github.com/StamusNetworks/scirius  
EveBox - https://evebox.org/  
Arkime - https://arkime.com/  
CyberChef - https://github.com/gchq/CyberChef  


Se encuentra en: https://github.com/StamusNetworks/SELKS  

Para instalarlo correr:

```
git clone https://github.com/StamusNetworks/SELKS.git
cd SELKS/docker/
./easy-setup.sh
docker-compose up -d
```

Una vez instalado en Kali, moverse a https://127.0.0.1/

Los credenciales de acceso son:  
user: **selks-user**  
password: **selks-user ** 

