# IP

## Introducción a la capa de red
La capa de red es la encargada de routear la información, para ello requiere de una identificación única para cada dispositivo y también un número que represente el tipo de protocolo de transporte utilizado en ese paquete. En este caso, el protocolo de red que se utiliza es el Protocolo de Internet (IP), que es responsable de la entrega de paquetes de datos desde el origen hasta el destino a través de una red.

## Definición
El Protocolo de Internet (IP) es un protocolo de comunicación que se utiliza para enviar y recibir paquetes de datos a través de redes informáticas. IP es un protocolo sin conexión, lo que significa que no establece una conexión directa entre el emisor y el receptor antes de enviar los datos. En su lugar, los paquetes se envían de manera independiente y pueden tomar diferentes rutas para llegar a su destino.
- **Protocolo no orientado a conexión**: No se establece una conexión directa entre el emisor y el receptor antes de enviar los datos. Los paquetes se envían de manera independiente y pueden tomar diferentes rutas para llegar a su destino.

- **Protocolo de entrega mejor esfuerzo (best effort protocol)**: IP no garantiza la entrega de los paquetes ni el orden en que se entregan. Los paquetes pueden perderse, duplicarse o llegar fuera de orden. Es responsabilidad de los protocolos de transporte, como TCP, garantizar la entrega confiable de los datos.

- **Protocolo con direcciones únicas**: Cada dispositivo en una red tiene una dirección IP única que lo identifica. Esta dirección se utiliza para enrutar los paquetes de datos desde el emisor hasta el receptor.

## Orientado a conexión vs sin orientación a conexión
En protocolos previos a IP, como X.25 y ATM, se usaban Virtual Circuits (VC) para establecer una conexión entre el emisor y el receptor antes de enviar los datos. Esto permitía que los paquetes se enviaran en orden y se asegurara la entrega de los mismos, al reservar en cada router en su camino los recursos necesarios. Sin embargo, esto también generaba una sobrecarga en la red y limitaba la flexibilidad en la transmisión de datos.

### Teorías conspiranóicas
IP nace de la defensa de Estados Unidos en la guerra fría, para que en caso de un ataque nuclear, la red de comunicaciones no se viera afectada y pudiera seguir funcionando. Por eso se diseñó como un protocolo sin conexión, que permite que los paquetes se envíen de manera independiente y puedan tomar diferentes rutas para llegar a su destino, lo que aumenta la resiliencia de la red.

## Direcciones IP
### Codificación de direcciones IP
Las direcciones IP se codifican en 32 bits (IPv4) o 128 bits (IPv6). En IPv4, las direcciones se representan en notación decimal con puntos, dividiendo los 32 bits en cuatro octetos de 8 bits cada uno. Por ejemplo, la dirección IP 192.168.1.1 representa los 32 bits divididos en cuatro octetos: 192, 168, 1 y 1.

Se codifican en dos partes:
- **NETID**: Identifica la red a la que pertenece el dispositivo. La longitud del NETID varía según la clase de dirección IP (A, B, C, D o E). Cuanto mayor sea el NETID, menor será el número de hosts disponibles en esa red.

- **HOSTID**: Identifica al dispositivo dentro de la red. La longitud del HOSTID también varía según la clase de dirección IP. Cuanto mayor sea el HOSTID, mayor será el número de hosts disponibles en esa red.

### Modelo jerárquico
Al ser un modelo jerárquico permite al protocolo conocer solamente las direcciones de las redes particulares y no de todos los dispositivos conectados en TODO el mundo a la red, lo que reduce la cantidad de información que debe manejar cada tabla de enrutamiento y mejora la eficiencia del enrutamiento.

## Clases de Direcciones IP
Al no alcanzar 256 redes para todas las redes del mundo, se decidió dividir las direcciones IP en clases, para que cada clase tuviera un rango de direcciones IP y así poder asignar direcciones a diferentes tipos de redes. Las clases de direcciones IP son:
### Clase A: Direcciones IP que van desde 0.0.0.0 hasta 126.255.255.255
- La cantidad máxima de hosts por red es de 16.777.214 (2^24 - 2).
- La cantidad máxima de redes es de 128 (2^7).
- Se utiliza 1 Octeto para el NETID y 3 Octetos para el HOSTID.
- El bit más signiificativo del primer octeto es 0, lo que significa que las direcciones IP de clase A tienen un rango de 0 a 127 en el primer octeto.

### Clase B: Direcciones IP que van desde 128.0.0.0 hasta 191.255.255.255
- La cantidad máxima de hosts por red es de 65.534 (2^16 - 2).
- La cantidad máxima de redes es de 16.384 (2^14).
- Se utiliza 2 Octetos para el NETID y 2 Octetos para el HOSTID.
- Los 2 bits más significativos del primer octeto son 10, lo que significa que las direcciones IP de clase B tienen un rango de 128 a 191 en el primer octeto.

### Clase C: Direcciones IP que van desde 192.0.0.0 hasta 239.255.255.255
- La cantidad máxima de hosts por red es de 254 (2^8 - 2).
- La cantidad máxima de redes es de 2.097.152 (2^21).
- Se utiliza 3 Octetos para el NETID y 1 Octeto para el HOSTID.
- Los 3 bits más significativos del primer octeto son 110, lo que significa que las direcciones IP de clase C tienen un rango de 192 a 223 en el primer octeto.

### Clase D: Direcciones IP que van desde 240.0.0.0 hasta 255.255.255.255
Se utilizan para **Multicast**, son direcciones en forma plana y no jerárquica, por lo que no se pueden dividir en NETID y HOSTID. Estas direcciones se utilizan para enviar paquetes a un grupo de dispositivos en lugar de a un solo dispositivo. Las direcciones IP de clase D tienen un rango de 224 a 239 en el primer octeto.
- La cantidad máxima de hosts por red es de 0.
- La cantidad máxima de redes es de 256 (2^8).
- Se utiliza 1 Octeto para el NETID y 3 Octetos para el HOSTID.
- Los 4 bits más significativos del primer octeto son 1110, lo que significa que las direcciones IP de clase D tienen un rango de 224 a 239 en el primer octeto.

### Clase E: Direcciones IP que van desde 240.0.0.0 hasta 255.255.255.255
Se utilizan para fines de investigación y desarrollo, y no se utilizan en redes públicas.
- La cantidad máxima de hosts por red es de 0.
- La cantidad máxima de redes es de 256 (2^8).
- Se utiliza 1 Octeto para el NETID y 3 Octetos para el HOSTID.
- Los 4 bits más significativos del primer octeto son 1111, lo que significa que las direcciones IP de clase E tienen un rango de 240 a 255 en el primer octeto.

### Dirección IP No especificada: 127.0.0.0
Utilizada comúnmente para DHCP, para que el cliente pueda solicitar una dirección IP al servidor DHCP. Esta dirección no se puede utilizar como dirección de host en una red, ya que está reservada para fines especiales.

### LOOPBACK: Direcciones IP reservadas que van desde 127.0.0.1 hasta 127.255.255.255
- La cantidad máxima de hosts por red es de 16.777.214 (2^24 - 2).
- La cantidad máxima de redes es de 128 (2^7).
- Se utiliza 1 Octeto para el NETID y 3 Octetos para el HOSTID.

## Direcciones IP privadas
Las direcciones IP privadas son un conjunto de direcciones reservadas para su uso en redes internas y no son enrutables a través de Internet. Estas direcciones permiten que los dispositivos dentro de una red local se comuniquen entre sí sin necesidad de utilizar direcciones IP públicas. Las direcciones IP privadas se definen en el RFC 1918 y se dividen en tres rangos principales:
- **Clase A**:  
    - Rango: 10.0.0.0 - 10.255.255.255
    - Máscara de subred: 255.0.0.0
- **Clase B**:
    - Rango: 172.16.0.0 - 172.31.255.255
    - Máscara de subred: 255.240.0.0
- **Clase C**:
    - Rango: 192.168.0.0 - 192.168.255.255
    - Máscara de subred: 255.255.0.0

## Anatomía de las direcciones IP
Con solo ver una dirección IP se puede determinar si es una dirección pública o privada, a qué clase pertenece y si es una dirección de host, de red o de broadcast.

### Broadcast
Una dirección de broadcast es una dirección IP que se utiliza para enviar paquetes a todos los dispositivos en una red local. En una red con máscara de subred de 255.255.255.0, la dirección de broadcast es la dirección en la que el octeto de host es 255. Por ejemplo, en la red 192.168.1.0/24, la dirección de broadcast es 192.168.1.255.