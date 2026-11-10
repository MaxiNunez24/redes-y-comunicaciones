# Comandos útiles para IP
## Comando `ip`
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
## Comando `netstat`
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

## Comando `ping`
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
## Comando `tracepath`
El comando `tracepath` es una herramienta de diagnóstico de red similar a `traceroute`, pero utiliza ICMP para rastrear la ruta que siguen los paquetes desde un origen hasta un destino en una red IP. Funciona enviando paquetes con un valor de TTL (Time to Live) inicial bajo y aumentando gradualmente el valor de TTL en cada paquete subsiguiente. Cada vez que un paquete alcanza un router, el router decrementa el valor de TTL y, si el TTL llega a cero, envía un mensaje ICMP "Time Exceeded" de vuelta al remitente. Esto permite al remitente identificar cada router en la ruta hacia el destino y medir el tiempo de ida y vuelta (RTT) para cada salto. El resultado es una lista de routers intermedios y sus tiempos de respuesta, lo que ayuda a los administradores de red a diagnosticar problemas de conectividad y rendimiento en la red.

```bash
echo "obase=2; <número_decimal>" | bc
```

Y para uno binario a decimal, se puede utilizar la siguiente sintaxis:

```bash
echo "ibase=2; <número_binario>" | bc
```
