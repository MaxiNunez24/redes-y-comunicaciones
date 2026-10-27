# Routing (Ruteo)

## Introducción
El ruteo es el proceso de determinar la ruta que deben seguir los paquetes de datos desde su origen hasta su destino a través de una red. Los routers son dispositivos de red que se encargan de recibir, analizar y reenviar los paquetes de datos hacia su destino final, utilizando tablas de enrutamiento y protocolos de ruteo para tomar decisiones sobre la mejor ruta a seguir.

## Router vs Host
El router es un dispositivo de red que se encarga de recibir, analizar y reenviar los paquetes de datos hacia su destino final, mientras que un host es un dispositivo final que se conecta a la red y puede enviar y recibir datos. Los routers operan en la capa de red del modelo OSI y utilizan direcciones IP para enrutar los paquetes, mientras que los hosts pueden ser computadoras, servidores, teléfonos inteligentes u otros dispositivos que utilizan la red para comunicarse.

- La diferencia principal es que los routers tienen como máximo 2 interfaces de red, mientras que los hosts pueden tener múltiples interfaces de red. Los routers también tienen la capacidad de tomar decisiones de enrutamiento y determinar la mejor ruta para enviar los paquetes, mientras que los hosts simplemente envían y reciben datos sin preocuparse por el enrutamiento.

## Tabla de Ruteo
Una tabla de ruteo es una estructura de datos que contiene información sobre las rutas disponibles en una red y se utiliza para determinar la mejor ruta para enviar paquetes de datos hacia su destino. Cada entrada en la tabla de ruteo contiene información sobre la dirección de destino, la máscara de subred, la dirección del siguiente salto (next hop) y la interfaz de salida que se debe utilizar para enviar los paquetes. Los routers utilizan estas tablas para tomar decisiones de enrutamiento y garantizar que los paquetes lleguen a su destino de manera eficiente y confiable.

## Comandos útiles
- netstat -nr: Muestra la tabla de ruteo del sistema operativo.
    - Ejemplo de salida:
    ```
    Kernel IP routing table
    Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface 
    0.0.0.0         192.168.1.1     0.0.0.0         UG        0 0          0 eth0
    127.0.0.0       127.0.0.1       255.0.0.0       UH        0 0          0 lo
    192.168.1.0     192.168.1.1     255.255.255.0   UG        0 0          0 eth0
    ```
- ifconfig: Muestra o modifica la configuración de las interfaces de red del sistema operativo, incluyendo direcciones IP, máscaras de subred y direcciones MAC.
    - Ejemplo `ifconfig` - salida:
    ```
    eth0      Link encap:Ethernet  HWaddr 00:1a:2b:3c:4d:5e  
              inet addr: 192.168.1.100  netmask: 255.255.255.0
              inet6 addr: fe80::21a:2bff:fe3c:4d5e/64 Scope:Link
              ether 00:1a:2b:3c:4d:5e  txqueuelen:1000  (Ethernet)
              RX packets:1234 errors:0 dropped:0 overruns:0 frame:0
              TX packets:567 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0
    ```
    - Ejemplo añadido de una ip `ifconfig eth0:1 192.168.1.101 netmask 255.255.255.0` - resultado:
        Agrega a la tabla de ruteo una nueva dirección IP a la interfaz eth0, con la dirección IP 192.168.1.101.

- ip: Muestra o modifica la configuración de las interfaces de red del sistema operativo, incluyendo direcciones IP, máscaras de subred y direcciones MAC. Es una herramienta más moderna y versátil que ifconfig.
    - Ejemplo muestra `ip addr show` - salida:
    ```
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host
           valid_lft forever preferred_lft forever
    2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 100
        link/ether 00:1a:2b:3c:4d:  5e brd ff:ff:ff:ff:ff:ff
        inet 192.168.1.100/24 brd 192.168.1.255 scope host eth0
           valid_lft forever preferred_lft forever
        inet6 fe80::21a:2bff:fe3c:4d5e/64 scope link
           valid_lft forever preferred_lft forever
    ```

    - Ejemplo añade una ip `ip addr add 192.168.1.101/24 dev eth0` - resultado:
        Agrega a la tabla de ruteo una nueva dirección IP a la interfaz eth0, con la dirección IP 192.168.1.101.
    
    - Ejemplo añade una ruta por defecto (gateway) `ip route add default via 192.168.1.1` - resultado:
        Agrega a la tabla de ruteo una nueva ruta por defecto (gateway) a través de la dirección IP 192.168.1.1.
    
## Diferencia entre HUB y SWITCH
- HUB: Es un dispositivo de red que permite la conexión de múltiples dispositivos en una red local. Funciona como un repetidor, enviando los datos recibidos a todos los dispositivos conectados, sin importar si el destinatario es el correcto o no. Esto puede generar colisiones y reducir el rendimiento de la red, ya que todos los dispositivos comparten el mismo ancho de banda.
- SWITCH: Es un dispositivo de red que también permite la conexión de múltiples dispositivos en una red local, pero a diferencia del HUB, el SWITCH es más inteligente y eficiente. El SWITCH analiza las direcciones MAC de los dispositivos conectados y envía los datos únicamente al destinatario correcto, evitando colisiones y mejorando el rendimiento de la red. Además, los SWITCHES pueden operar en modo full-duplex, lo que permite la transmisión simultánea de datos en ambas direcciones, mientras que los HUBS solo pueden operar en modo half-duplex. Hoy en día casi no existen HUBS, ya que los SWITCHES son más eficientes y ofrecen un mejor rendimiento en redes modernas.