# ICMP
## Introducción
Es un protocolo de control de mensajes de Internet que se utiliza para enviar mensajes de error y de control en redes IP. ICMP es parte del conjunto de protocolos de Internet y se utiliza para diagnosticar problemas de conectividad, informar sobre errores en la entrega de paquetes y proporcionar información sobre el estado de la red.

### Funciones principales
- **Mensajes de error**: ICMP se utiliza para enviar mensajes de error cuando un paquete no puede ser entregado a su destino. Por ejemplo, si un router no puede encontrar una ruta hacia el destino, enviará un mensaje ICMP de "Destination Unreachable" al remitente.

- **Mensajes de control**: ICMP también se utiliza para enviar mensajes de control, como "Echo Request" y "Echo Reply", que se utilizan en la herramienta de diagnóstico de red conocida como "ping". Estos mensajes permiten a los administradores de red verificar la conectividad entre dos dispositivos en una red.

- **Diagnóstico de red**: ICMP proporciona información sobre el estado de la red, como la latencia y la pérdida de paquetes. Esto ayuda a los administradores de red a identificar problemas de rendimiento y a tomar medidas para mejorar la calidad del servicio.

- **Seguridad**: Aunque ICMP es útil para el diagnóstico de red, también puede ser explotado por atacantes para realizar ataques de denegación de servicio (DoS) o para recopilar información sobre la red. Por esta razón, algunos administradores de red pueden optar por filtrar o limitar el tráfico ICMP en sus redes.

### Tipos de mensajes ICMP
#### Echo Request y Echo Reply (PING)
- **Echo Request**: Es un mensaje enviado por un dispositivo para solicitar una respuesta de otro dispositivo. Se utiliza en la herramienta "ping" para verificar la conectividad entre dos dispositivos en una red. El mensaje contiene un identificador y un número de secuencia que permiten al remitente correlacionar la respuesta con la solicitud original.

- **Echo Reply**: Es un mensaje enviado en respuesta a un Echo Request. Cuando un dispositivo recibe un Echo Request, genera un Echo Reply y lo envía de vuelta al remitente. La respuesta contiene el mismo identificador y número de secuencia que la solicitud original, lo que permite al remitente medir el tiempo de ida y vuelta (RTT) y determinar si hay pérdida de paquetes.

#### Destination Unreachable
- **Port Unreachable**: Indica que el puerto de destino no está disponible o no está escuchando en el host de destino. Esto puede ocurrir si la aplicación que debería estar escuchando en ese puerto no está en ejecución o si el puerto está bloqueado por un firewall.

- **Host Unreachable**: Indica que el host de destino no puede ser alcanzado. Esto puede deberse a problemas de conectividad, como un router caído, una dirección IP incorrecta o una configuración de red incorrecta.

- **Network Unreachable**: Indica que la red de destino no puede ser alcanzada. Esto puede ocurrir si no hay una ruta válida hacia la red de destino o si un router intermedio no puede enrutar el paquete correctamente.

#### TTL exceeded
- **Time Exceeded**: Indica que el tiempo de vida (TTL) de un paquete ha expirado antes de llegar a su destino. Esto puede ocurrir si un paquete queda atrapo en un bucle de enrutamiento o si la ruta hacia el destino es demasiado larga. Se utiliza para diagnosticar problemas de enrutamiento y para evitar que los paquetes circulen indefinidamente en la red.

#### Fragmentation Needed
- **Fragmentation Needed**: Indica que un paquete IP es demasiado grande para ser transmitido a través de un enlace con un MTU más pequeño y que debe ser fragmentado. Este mensaje se utiliza para informar al remitente que debe fragmentar el paquete antes de enviarlo. El mensaje también puede incluir información sobre el MTU del enlace, lo que permite al remitente ajustar el tamaño de los paquetes que envía para evitar la fragmentación en el futuro.

#### Redirección de ruta (Redirect)
- **Redirect**: Indica que un paquete ha sido enviado a través de una ruta subóptima y que el remitente debe actualizar su tabla de enrutamiento para utilizar una ruta más eficiente. Este mensaje se utiliza para optimizar el enrutamiento y mejorar el rendimiento de la red. El mensaje incluye la dirección IP del router que envió la redirección y la dirección IP del destino al que se debe enviar el paquete.

## Trace Route
### Explicación
El comando "traceroute" es una herramienta de diagnóstico de red que utiliza ICMP para rastrear la ruta que siguen los paquetes desde un origen hasta un destino en una red IP. Funciona enviando paquetes con un valor de TTL (Time to Live) inicial bajo y aumentando gradualmente el valor de TTL en cada paquete subsiguiente. Cada vez que un paquete alcanza un router, el router decrementa el valor de TTL y, si el TTL llega a cero, envía un mensaje ICMP "Time Exceeded" de vuelta al remitente. Esto permite al remitente identificar cada router en la ruta hacia el destino y medir el tiempo de ida y vuelta (RTT) para cada salto. El resultado es una lista de routers intermedios y sus tiempos de respuesta, lo que ayuda a los administradores de red a diagnosticar problemas de conectividad y rendimiento en la red.

### Flags
- Por defecto la herramienta utiliza UDP

- Se puede agregar el flag -I para que utilice ICMP

- Se puede utilizar el flag -T para que utilice TCP

- Se puede utilizar el flag -n para que no resuelva los nombres de host y muestre solo las direcciones IP

## Trace Path
### Explicación
El comando "tracepath" es una herramienta de diagnóstico de red similar a "traceroute", pero utiliza ICMP para rastrear la ruta que siguen los paquetes desde un origen hasta un destino en una red IP. Funciona enviando paquetes con un valor de TTL (Time to Live) inicial bajo y aumentando gradualmente el valor de TTL en cada paquete subsiguiente. Cada vez que un paquete alcanza un router, el router decrementa el valor de TTL y, si el TTL llega a cero, envía un mensaje ICMP "Time Exceeded" de vuelta al remitente. Esto permite al remitente identificar cada router en la ruta hacia el destino y medir el tiempo de ida y vuelta (RTT) para cada salto. El resultado es una lista de routers intermedios y sus tiempos de respuesta, lo que ayuda a los administradores de red a diagnosticar problemas de conectividad y rendimiento en la red.

## Comando útil para bloquear ICMP
El comando `iptables` se utiliza para configurar reglas de filtrado de paquetes en sistemas operativos basados en Linux. A continuación, se presentan algunos ejemplos de cómo bloquear el tráfico ICMP utilizando `iptables`, estos pueden ser útiles para proteger el sistema contra ataques de denegación de servicio (DoS) o para limitar la exposición del host a posibles amenazas de seguridad. Sin embargo, bloquear todo el tráfico ICMP también puede dificultar la resolución de problemas de conectividad y afectar la funcionalidad de algunas aplicaciones que dependen de ICMP para la comunicación:

- `iptables -I OUTPUT --proto ICMP -j DROP` - Bloquea todo el tráfico ICMP saliente en el sistema operativo, evitando que se envíen mensajes ICMP desde el host.

- `iptables -I INPUT --proto ICMP -j DROP` - Bloquea todo el tráfico ICMP entrante en el sistema operativo, evitando que se reciban mensajes ICMP desde otros hosts en la red.

- `iptables -I FORWARD --proto ICMP -j DROP` - Bloquea todo el tráfico ICMP que pasa a través del sistema operativo, evitando que se reenvíen mensajes ICMP entre otros hosts en la red.