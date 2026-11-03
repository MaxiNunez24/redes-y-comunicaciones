# Fragmentación en capa de Red

## Introducción
Debido a que hay diferentes capas de enlaces con diferentes MTUs, es posible que un datagrama IP sea demasiado grande para ser transmitido a través de una red con un MTU más pequeño. En este caso, el datagrama debe ser fragmentado en varios fragmentos más pequeños que puedan ser transmitidos a través de la red.

### MSS (Maximum Segment Size)
Este se calcula: MSS = MTU - 20 bytes (IP header) - 20 bytes (TCP header) = 1460 bytes (MSS)

Si algun router tiene un MTU menor a 1460 bytes, el datagrama IP será fragmentado en varios fragmentos más pequeños que puedan ser transmitidos a través de la red. Cada fragmento tendrá su propio encabezado IP y se enviará como un datagrama independiente.

### Fragmentos
Son múltiplos de 8 bytes, excepto el último fragmento que puede ser menor. Esto se debe a que el campo de desplazamiento de fragmento (Fragment Offset) en el encabezado IP se mide en unidades de 8 bytes. Por lo tanto, todos los fragmentos, excepto el último, deben tener un tamaño que sea un múltiplo de 8 bytes para que el receptor pueda reconstruir correctamente el datagrama original.

#### Se agregan los headers
version | header length | DS (differentiated services) | ECN (explicit congestion notification) | total length of each fragment (in bytes) | identification | 0 | DF (don't fragment) | MF (more fragments) | fragment offset (in units of 8 bytes) | TTL (time to live) | protocol | header checksum | source IP address | destination IP address

- version: 4 bits, especifica la versión del protocolo IP (IPv4).

- header length: 4 bits, indica la longitud del encabezado IP en palabras de 32 bits. El valor mínimo es 5 (20 bytes) y el máximo es 15 (60 bytes).

- DS (differentiated services): 6 bits, utilizado para clasificar y priorizar el tráfico de red. Permite a los routers y switches aplicar políticas de calidad de servicio (QoS) para garantizar un rendimiento adecuado para diferentes tipos de tráfico.

- ECN (explicit congestion notification): 2 bits, utilizado para indicar la congestión de la red sin descartar paquetes. Permite a los dispositivos de red notificar a los emisores y receptores sobre la congestión, lo que les permite ajustar sus tasas de transmisión y evitar la pérdida de paquetes.

- total length of each fragment (in bytes): 16 bits, indica la longitud total del fragmento IP, incluyendo el encabezado y los datos. El valor máximo es 65,535 bytes. 

- identification: 16 bits, utilizado para identificar fragmentos que pertenecen al mismo datagrama IP. Todos los fragmentos de un datagrama tienen el mismo valor de identificación, lo que permite al receptor reconstruir el datagrama original a partir de sus fragmentos.

- 0: 1 bit, reservado para uso futuro y debe establecerse en 0.

- DF (don't fragment): 1 bit, indica si el datagrama IP puede ser fragmentado o no. Si se establece en 1, el datagrama no puede ser fragmentado y se descartará si es demasiado grande para la red. Si se establece en 0, el datagrama puede ser fragmentado si es necesario.

- MF (more fragments): 1 bit, indica si hay más fragmentos del datagrama IP. Si se establece en 1, significa que hay más fragmentos por venir. Si se establece en 0, significa que este es el último fragmento.

- fragment offset (in units of 8 bytes): 13 bits, indica la posición del fragmento en el datagrama original. Se mide en unidades de 8 bytes, lo que permite al receptor reconstruir el datagrama original a partir de sus fragmentos.

- TTL (time to live): 8 bits, indica el tiempo de vida del datagrama IP en la red. Se decrementa en cada salto (router) y, si llega a 0, el datagrama se descarta. Esto evita que los datagramas circulen indefinidamente en la red.

- protocol: 8 bits, indica el protocolo de capa superior al que pertenece el datagrama IP (por ejemplo, TCP, UDP, ICMP).

- header checksum: 16 bits, utilizado para verificar la integridad del encabezado IP. Si el valor calculado no coincide con el valor recibido, el datagrama se descarta. El checksum se actualiza en cada salto ya que cambia el TTL.

- source IP address: 32 bits, indica la dirección IP del remitente del datagrama.

- destination IP address: 32 bits, indica la dirección IP del destinatario del datagrama.

- options: variable, contiene opciones de configuración específicas del protocolo IP. Puede incluir información adicional para el procesamiento del datagrama, como información de calidad de servicio (QoS) o información de seguridad.

### Path MTU Discovery