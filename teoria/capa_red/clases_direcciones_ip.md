# Clasificación de direcciones IP
Al no alcanzar 256 redes para todas las redes del mundo, se decidió dividir las direcciones IP en clases, para que cada clase tuviera un rango de direcciones IP y así poder asignar direcciones a diferentes tipos de redes. 

## Clases de direcciones IP
Las direcciones IP se dividen en cinco clases principales: A, B, C, D y E. Cada clase tiene un rango específico de direcciones IP y se utiliza para diferentes propósitos. Las clases A, B y C se utilizan para redes públicas, mientras que las clases D y E se utilizan para propósitos especiales, como multicast y experimentación.

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

### Clase C: Direcciones IP que van desde 192.0.0.0 hasta 223.255.255.255
- La cantidad máxima de hosts por red es de 254 (2^8 - 2).
- La cantidad máxima de redes es de 2.097.152 (2^21).
- Se utiliza 3 Octetos para el NETID y 1 Octeto para el HOSTID.
- Los 3 bits más significativos del primer octeto son 110, lo que significa que las direcciones IP de clase C tienen un rango de 192 a 223 en el primer octeto.

### Clase D: Direcciones IP que van desde 224.0.0.0 hasta 239.255.255.255
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

## IPD (IP de Dominio)
Las direcciones IP de dominio son direcciones IP que se utilizan para identificar y localizar dispositivos en una red. Estas direcciones son únicas dentro de una red y se utilizan para la comunicación entre dispositivos.

### IPO (IP de Origen)
La dirección IP de origen es la dirección IP del dispositivo que envía un paquete de datos.


