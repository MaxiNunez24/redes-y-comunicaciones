# UDP (User Datagram Protocol)

## Historia
UDP es un protocolo de comunicación de la capa de transporte del modelo TCP/IP. Fue definido en 1980 por David P. Reed en el RFC 768. UDP se diseñó para aplicaciones que requieren baja latencia y tolerancia a la pérdida de datos, como transmisión de video en tiempo real, juegos en línea y VoIP.

## Características principales
- **No orientado a conexión**: UDP no establece una conexión antes de enviar datos, lo que reduce la sobrecarga y permite una comunicación más rápida.

- **Sin garantía de entrega**: UDP no garantiza que los paquetes lleguen a su destino, ni que lleguen en orden. Esto significa que los datos pueden perderse o llegar duplicados.

- **Encabezado simple**: El encabezado de UDP es más pequeño que el de TCP, lo que reduce la sobrecarga de datos y mejora la eficiencia en la transmisión.

- **Transmisión de datagramas**: UDP envía datos en unidades llamadas datagramas, que son independientes y pueden llegar en cualquier orden.

- **Uso en aplicaciones específicas**: UDP es ideal para aplicaciones que pueden tolerar la pérdida de datos y requieren una comunicación rápida, como streaming de video, juegos en línea y VoIP.

- **Multicast y broadcast**: UDP permite la transmisión de datos a múltiples destinatarios mediante multicast y broadcast, lo que es útil en aplicaciones como videoconferencias y actualizaciones de software.

## Datagramas UDP
Un datagrama UDP es la unidad básica de datos que se envía a través de la red utilizando el protocolo UDP. Cada datagrama contiene un encabezado y los datos del mensaje. El encabezado de un datagrama UDP tiene un tamaño fijo de 8 bytes y contiene la siguiente información:
- **Puerto de origen**: Identifica el puerto del remitente.
- **Puerto de destino**: Identifica el puerto del destinatario.
- **Longitud**: Indica la longitud total del datagrama.
- **Checksum**: Se utiliza para verificar la integridad de los datos. (Es opcional en IPv4 y obligatorio en IPv6)

## Protocolo ICMP (Internet Control Message Protocol)
ICMP es otro protocolo de la capa de red que se utiliza junto con UDP para enviar mensajes de control y error. ICMP se utiliza para diagnosticar problemas de red y para informar sobre errores en la entrega de paquetes.
Es utilizado tanto por UDP como por TCP y por IP para enviar mensajes de error y control, como "Destination Unreachable" o "Time Exceeded". Aunque ICMP no es parte de UDP, es importante para la gestión de la red y la resolución de problemas.

### El comando ping 
`ping` utiliza ICMP para verificar la conectividad entre dos dispositivos en una red. Cuando se envía un paquete ICMP Echo Request, el dispositivo de destino responde con un paquete ICMP Echo Reply, lo que permite medir el tiempo de respuesta y la pérdida de paquetes.

## Comparación con TCP
| Característica | UDP | TCP |
|----------------|-----|-----|
| Orientación a conexión | No | Sí |
| Garantía de entrega | No | Sí |
| Orden de entrega | No | Sí |
| Tamaño del encabezado | 8 bytes | 20 bytes |

## El viaje de un mensaje UDP
1. **Aplicación**: La aplicación genera un mensaje que necesita ser enviado a través de la red.

2. **Encapsulación**: El mensaje se encapsula en un datagrama UDP, que incluye un encabezado con información como el puerto de origen y destino.

3. **Envío**: El datagrama UDP se envía a través de la red utilizando el protocolo IP. El datagrama puede pasar por varios routers y redes antes de llegar a su destino.

4. **Recepción**: El dispositivo de destino recibe el datagrama UDP y lo entrega a la aplicación correspondiente, que procesa el mensaje.  

5. **Posibles pérdidas**: Durante el viaje, algunos datagramas pueden perderse o llegar fuera de orden, ya que UDP no garantiza la entrega ni el orden de los mensajes.

## Para utilizar UDP desde terminal
Para enviar y recibir datos utilizando UDP desde la terminal, se pueden utilizar herramientas como `netcat` (nc) o `socat`. A continuación se muestran ejemplos de cómo hacerlo:
### Enviar datos con netcat
```bash
# Enviar un mensaje a un servidor UDP en el puerto 12345
echo "Hola, UDP!" | nc -u <IP_DEL_SERVIDOR> 12345
```
### Recibir datos con netcat
```bash
# Escuchar en el puerto 12345 para recibir mensajes UDP
nc -u -l 12345
```


