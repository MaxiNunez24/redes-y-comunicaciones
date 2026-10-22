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

## [Direcciones IP](./direcciones_ip.md)

## [Clases de Direcciones IP](./clases_direcciones_ip.md)

## [Entes para la asignación de direcciones IP](./entes.md)

## Subnetting IP Fijo (Máscaras de subred)
Dentro del a tabla de ruteo se agregaron lo que se conoce como máscaras de subred, que permiten dividir una red en subredes más pequeñas. Esto se hace para mejorar la eficiencia del enrutamiento y para permitir una mejor gestión de los recursos de red. Las máscaras de subred se utilizan para determinar qué parte de la dirección IP representa la red y qué parte representa el host. Agrandando la parte de Red y achicando la parte de Hosts. 

### Longitud de prefijo (Prefix Length)
La longitud de prefijo es el número de bits utilizados para la parte de red de una dirección IP. Se representa en la notación **CIDR (Classless Inter-Domain Routing)** como un número después de la barra (/) en la dirección IP. Por ejemplo, en la dirección IP 192.168.1.1/24, la longitud de prefijo es 24. En la práctica ambas notaciones (CIDR y máscara de subred) se utilizan para representar la misma información, pero la notación CIDR es más concisa y fácil de leer. Si las longitudes de prefijo son iguales, las direcciones IP pertenecen a la misma red y quiere decir que las subredes fueron distribuidas equitativamente. Por ejemplo, las direcciones IP 192.168.1.1/24 y 192.168.1.2/24 pertenecen a la misma red.

### Máscaras de subred
Las máscaras de subred se utilizan para dividir una red en subredes más pequeñas. La máscara de subred se representa en notación decimal con puntos, al igual que las direcciones IP. Por ejemplo, la máscara de subred 255.255.255.0 representa una red con 24 bits para la parte de red y 8 bits para la parte de host.

### Cálculo de la máscara de subred
La máscara de subred se puede calcular utilizando la longitud de prefijo. En ese sentido, la máscara de subred se puede calcular utilizando la siguiente fórmula:
Máscara de subred = 256 - (2^(32 - longitud de prefijo))

### Ejemplos
Para una red de clase C con una dirección IP de 192.168.0.0 y una máscara de subred de /24, pero de la cual necesito 4 subredes, se puede calcular la nueva máscara de subred de la siguiente manera:
1. Determinar el número de subredes necesarias: 4 subredes.
2. Calcular el número de bits necesarios para representar las subredes: 2 bits (2^2 = 4 subredes). Para esto se utiliza la fórmula: 2^n >= número de subredes, donde n es el número de bits necesarios.
3. Calcular la nueva longitud de prefijo: 24 + 2 = 26.
4. La nueva máscara de subred es /26.
5. La red va a estar dividida en estas 4 subredes:
    - Subred 1: 192.168.0.0/26 -> 
        - Rango de direcciones IP: 192.168.0.1 - 192.168.0.62
    - Subred 2: 192.168.0.64/26 -> 
        - Rango de direcciones IP: 192.168.0.65 - 192.168.0.126
    - Subred 3: 192.168.0.128/26 -> 
        - Rango de direcciones IP: 192.168.0.129 - 192.168.0.190 
    - Subred 4: 192.168.0.192/26 -> 
        - Rango de direcciones IP: 192.168.0.193 - 192.168.0.254
6. En esta red el número de direcciones IP es de 62 direcciones, ya que cada subred tiene 64 direcciones (2^6 = 64), de las cuales 2 se reservan para la red y el broadcast, dejando 62 direcciones utilizables para hosts. Pero al tener cada una de las 4 subredes 62 direcciones, el total de direcciones IP utilizables es de 248 direcciones (62 * 4 = 248). Dejando como "desperdicio" las direcciones reservadas para la red y el broadcast de cada subred, que son 8 direcciones (2 * 4 = 8). Por lo tanto, el total de direcciones IP en la red original es de 256 direcciones (2^8 = 256), de las cuales 248 son utilizables para hosts y 8 se reservan para la red y el broadcast de cada subred.

## Subnetting IP Variable (VLSM)
El Subnetting IP Variable (VLSM) es una técnica que permite dividir una red en subredes de diferentes tamaños, lo que permite un uso más eficiente del espacio de direcciones IP. Con VLSM, se pueden asignar diferentes longitudes de prefijo a cada subred, lo que permite crear subredes más grandes o más pequeñas según las necesidades de la red. Esto es especialmente útil en redes donde se tienen diferentes tipos de dispositivos con diferentes necesidades de direcciones IP. Por ejemplo, se puede asignar una subred más grande a un servidor que necesita muchas direcciones IP, mientras que se puede asignar una subred más pequeña a un dispositivo que necesita pocas direcciones IP. Esto permite un uso más eficiente del espacio de direcciones IP y reduce el desperdicio de direcciones IP.

### Ejemplo de VLSM
Necesito crear 4 subredes donde la red A tiene 70 hosts, la red B tiene 40 hosts y las redes C y D tienen 25 c/u. Para esto, se siguieron los siguientes pasos:
1. Determinar el número de hosts necesarios para cada subred:
- Red A: 70 hosts
- Red B: 40 hosts
- Red C: 25 hosts
- Red D: 25 hosts
2. Dada la dirección IP 193.168.4.0, se puede calcular la máscara de subred para cada subred utilizando la fórmula: 2^n - 2 >= número de hosts necesarios, donde n es el número de bits necesarios para representar los hosts. Por ejemplo, para la red A, se necesitan 7 bits para representar 70 hosts (2^7 - 2 = 126), por lo que la máscara de subred es /25. Para la red B, se necesitan 6 bits para representar 40 hosts (2^6 - 2 = 62), por lo que la máscara de subred es /26. Para las redes C y D, se necesitan 5 bits para representar 25 hosts (2^5 - 2 = 30), por lo que la máscara de subred es /27.
3. Se puede calcular el rango de direcciones IP para cada subred utilizando la dirección IP de la red y la máscara de subred. Por ejemplo, para la red A, la dirección de red es, tomando la última división de la red asignada para esta misma, 193.168.4.128/25, por lo que el rango de direcciones IP es 

## Comandos útiles para IP
### Comando `ip`
El comando `ip` es una herramienta de línea de comandos que se utiliza para configurar y administrar interfaces de red, direcciones IP y rutas en sistemas Linux. Este comando reemplaza al antiguo comando `ifconfig` y proporciona una interfaz más completa y flexible para la administración de redes. Algunas de las funciones que se pueden realizar con el comando `ip` incluyen:
- Configuración de direcciones IP en interfaces de red.
    - ejemplo:
        ```bash
        ip addr add <dirección_ip>/<longitud_de_prefijo> dev <interfaz>
        ```
- Visualización de la configuración de red y las interfaces.
    - ejemplo:
        ```bash
        ip addr show
        ```
- Configuración de rutas y tablas de enrutamiento.
    - ejemplo:
        ```bash
        ip route show
        ```
    - ejemplo:
        ```bash
        ip route add <red>/<longitud_de_prefijo> via <puerta_de_enlace>
        ```
    - ejemplo:
        ```bash
        ip route del <red>/<longitud_de_prefijo>
        ```
- Administración de túneles y VPNs.
    - ejemplo:
        ```bash
        ip tunnel add <nombre_del_túnel> mode <tipo_de_túnel> remote <dirección_ip_remota> local <dirección_ip_local>
        ```
- Configuración de reglas de filtrado y políticas de enrutamiento.
    - ejemplo:
        ```bash
        ip rule add from <dirección_ip> table <tabla_de_enrutamiento>
        ```
- Eliminación de direcciones IP y rutas.
    - ejemplo:
        ```bash
        ip addr del <dirección_ip>/<longitud_de_prefijo> dev <interfaz>
        ```
- Visualización de estadísticas de tráfico y estado de las interfaces.
    - ejemplo:
        ```bash
        ip -s link show
        ```
- Configuración de VLANs y etiquetado de tráfico.
    - ejemplo:
        ```bash
        ip link add link <interfaz> name <nombre_de_la_vlan> type vlan id <id_de_la_vlan>
        ```
- Configuración de direcciones IPv6 y administración de vecinos.
    - ejemplo:
        ```bash
        ip -6 addr add <dirección_ipv6>/<longitud_de_prefijo> dev <interfaz>
        ```
- Configuración de direcciones IP temporales y privacidad.
    - ejemplo:
        ```bash
        ip addr add <dirección_ip_temporal>/<longitud_de_prefijo> dev <interfaz> scope temporary
        ```
- Visualización de información sobre la tabla de vecinos y la resolución de direcciones.
    - ejemplo:
        ```bash
        ip neigh show
        ```
### Comando `netstat`
El comando `netstat` es una herramienta de línea de comandos que se utiliza para mostrar información sobre las conexiones de red, las tablas de enrutamiento y las estadísticas de tráfico en sistemas Linux. Este comando proporciona información detallada sobre las conexiones de red activas, los puertos abiertos y las interfaces de red. Algunas de las funciones que se pueden realizar con el comando `netstat` incluyen:
- Visualización de conexiones de red activas.
    - ejemplo:
        ```bash
        netstat -tuln
        ```
- Visualización de la tabla de enrutamiento.
    - ejemplo:
        ```bash
        netstat -r
        ```
- Visualización de estadísticas de tráfico y errores de red.
    - ejemplo:
        ```bash
        netstat -s
        ```
- Visualización de puertos abiertos y servicios en ejecución.
    - ejemplo:
        ```bash
        netstat -anp
        ```
- Visualización de conexiones de red por protocolo (TCP, UDP, etc.).
    - ejemplo:
        ```bash
        netstat -p
        ```
- Visualización de conexiones de red por dirección IP y puerto.
    - ejemplo:
        ```bash
        netstat -an | grep <dirección_ip>:<puerto>
        ```
- Visualización de conexiones de red por estado (ESTABLISHED, LISTENING, etc.).
    - ejemplo:
        ```bash
        netstat -an | grep <estado>
        ```
- Visualización de conexiones de red por usuario.
    - ejemplo:
        ```bash
        netstat -anp | grep <usuario>
        ```
- Visualización de conexiones de red por interfaz de red.
    - ejemplo:
        ```bash
        netstat -i
        ```
- Visualización de conexiones de red por dirección MAC.
    - ejemplo:
        ```bash
        netstat -e
        ```
- Visualización de conexiones de red por protocolo y dirección IP.
    - ejemplo:
        ```bash
        netstat -anp | grep <protocolo> | grep <dirección_ip>
        ```

### Comando `ping`
El comando `ping` es una herramienta de línea de comandos que se utiliza para verificar la conectividad de red entre dos dispositivos en una red. Este comando envía paquetes ICMP (Internet Control Message Protocol) a un dispositivo de destino y espera una respuesta. El comando `ping` es útil para diagnosticar problemas de conectividad, medir el tiempo de respuesta y determinar la pérdida de paquetes en una red. Algunas de las funciones que se pueden realizar con el comando `ping` incluyen:
- Verificación de la conectividad de red.
    - ejemplo:
        ```bash
        ping <dirección_ip_o_nombre_de_host>
        ```
- Medición del tiempo de respuesta (latencia) entre dos dispositivos.
    - ejemplo:
        ```bash
        ping -c <número_de_paquetes> <dirección_ip_o_nombre_de_host>
        ```
### Calculadora para binario a decimal y viceversa
Una herramienta útil para realizar cálculos de decimal a binario y viceversa en Linux es el comando `bc`. Este comando permite realizar operaciones matemáticas y conversiones entre diferentes bases numéricas. Para convertir un número decimal a binario, se puede utilizar la siguiente sintaxis:

```bash
echo "obase=2; <número_decimal>" | bc
```

Y para uno binario a decimal, se puede utilizar la siguiente sintaxis:

```bash
echo "ibase=2; <número_binario>" | bc
```
