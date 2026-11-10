# ARP (Address Resolution Protocol)

## Introducción
El protocolo ARP (Address Resolution Protocol) es un protocolo de red utilizado para mapear direcciones IP a direcciones MAC en una red local. Su función principal es permitir que los dispositivos de una red local se comuniquen entre sí mediante la resolución de direcciones IP a direcciones físicas (MAC). ARP es esencial para el funcionamiento de las redes Ethernet, ya que permite que los dispositivos encuentren la dirección MAC correspondiente a una dirección IP antes de enviar datos.

## Funcionamiento de ARP
Cuando un dispositivo necesita enviar datos a otro dispositivo en la misma red local, primero verifica si ya conoce la dirección MAC correspondiente a la dirección IP de destino. Si no la conoce, envía una solicitud ARP (ARP request) a todos los dispositivos de la red local, preguntando "¿Quién tiene esta dirección IP?". El dispositivo que posee la dirección IP solicitada responde con su dirección MAC (ARP reply). Una vez que el dispositivo emisor recibe la respuesta, almacena la dirección MAC en su caché ARP para futuras comunicaciones y puede enviar los datos al dispositivo de destino.z|

## Comandos útiles de ARP
En sistemas operativos como Windows, Linux y macOS, existen comandos que permiten interactuar con la caché ARP y realizar consultas. Algunos de los comandos más comunes son:
- `arp -a`: Muestra la tabla ARP actual, que contiene las direcciones IP y sus correspondientes direcciones MAC.
- `arp -d <dirección IP>`: Elimina una entrada específica de la tabla ARP.
- `arp -s <dirección IP> <dirección MAC>`: Agrega una entrada estática a la tabla ARP, asociando una dirección IP con una dirección MAC específica.