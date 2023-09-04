# ESP-MQTT SSL Sample application 
## (mutual authentication)

Este ejemplo conecta el ESP32 al broker Mosquitto utilizando TLS



## Configuracion SSID y PASS WiFi

Este ejemplo usa la funcion "example_connect()" de la platarforma ESP-IDF.

Para configurar el SSID y PASSWORD se debe hacer clic en el icono "engranaje" (configuración)
de la barra inferior del VSCode y allí en la sección de WiFi se podrán configurar los datos
necesarios



## Configurar URI del Broker

Dentro del archivo app_main.c hay que configurar la definición "BROKER_URI" que se encuentra
al inicio del archivo, colocando los datos correctos del broker a utilizar.



## Configurar certificados:

En los archivos client.crt, client.key y broker_CA.crt, hay que pegar el contenido
de los certificados que se crean con el script crea_certs.sh.
Recordar reemplazar la IP que se encuentra dentro del script, por TU IP LOCAL



## Copiar los certificados necesarios a la carpeta del broker:

En general la carpeta es "/etc/mosquitto/certs", el path se indica en el archivo mosquito.conf

Se deben copiar allí dentro los siguientes archivos generados con el script "crea_certs.sh"
ca.crt
server.crt
server.key



## El siguiente es el contenido del archivo mosquitto.conf que permite correr este ejemplo:

persistence true

persistence_location /var/lib/mosquitto/

log_dest file /var/log/mosquitto/mosquitto.log

include_dir /etc/mosquitto/conf.d

#allow_anonymous true

#password_file /etc/mosquitto/passfile

#listener 1883

listener 8883

cafile /etc/mosquitto/certs/ca.crt

keyfile /etc/mosquitto/certs/server.key

certfile /etc/mosquitto/certs/server.crt

require_certificate true

use_identity_as_username true




### Ejemplo de la salida por consola al ejecutar la aplicación:

```
I (3714) event: sta ip: 192.168.0.139, mask: 255.255.255.0, gw: 192.168.0.2
I (3714) system_api: Base MAC address is not set, read default base MAC address from BLK0 of EFUSE
I (3964) MQTT_CLIENT: Sending MQTT CONNECT message, type: 1, id: 0000
I (4164) MQTTS_EXAMPLE: MQTT_EVENT_CONNECTED
I (4174) MQTTS_EXAMPLE: sent publish successful, msg_id=41464
I (4174) MQTTS_EXAMPLE: sent subscribe successful, msg_id=17886
I (4174) MQTTS_EXAMPLE: sent subscribe successful, msg_id=42970
I (4184) MQTTS_EXAMPLE: sent unsubscribe successful, msg_id=50241
I (4314) MQTTS_EXAMPLE: MQTT_EVENT_PUBLISHED, msg_id=41464
I (4484) MQTTS_EXAMPLE: MQTT_EVENT_SUBSCRIBED, msg_id=17886
I (4484) MQTTS_EXAMPLE: sent publish successful, msg_id=0
I (4684) MQTTS_EXAMPLE: MQTT_EVENT_SUBSCRIBED, msg_id=42970
I (4684) MQTTS_EXAMPLE: sent publish successful, msg_id=0
I (4884) MQTT_CLIENT: deliver_publish, message_length_read=19, message_length=19
I (4884) MQTTS_EXAMPLE: MQTT_EVENT_DATA
TOPIC=/topic/qos0
DATA=data
I (5194) MQTT_CLIENT: deliver_publish, message_length_read=19, message_length=19
I (5194) MQTTS_EXAMPLE: MQTT_EVENT_DATA
TOPIC=/topic/qos0
DATA=data
```

