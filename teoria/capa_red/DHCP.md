# DHCP (Dynamic Host Configuration Protocol)
## Introducción
Es un protocolo de L3, que de forma simplificada solo requiere una dirección IP, una máscara y gateway. Se utiliza para solicitar una dirección IP en una red de forma automática.

## Pasos
- Se hace un broadcast a la red solicitando una dirección IP. Al no tener una dirección IP asignada se utiliza la dirección 0.0.0.0 y el broadcast 255.255.255.255 ya que no se conoce la dirección del servidor DHCP. El mensaje enviado es un ***DHCPDISCOVER***.

- El servidor DHCP responde con un ***DHCPOFFER***, ofreciendo una dirección IP disponible y otros parámetros de configuración de red, como la máscara de subred, la puerta de enlace predeterminada y los servidores DNS.

- El cliente responde con un ***DHCPREQUEST***, solicitando la dirección IP ofrecida por el servidor DHCP.

- El servidor DHCP responde con un ***DHCPACK***, confirmando la asignación de la dirección IP y proporcionando los parámetros de configuración de red al cliente. Además de guardar la dirección MAC del cliente y la dirección IP asignada en su base de datos para futuras referencias.

- El cliente configura su interfaz de red con la dirección IP asignada y los parámetros de configuración proporcionados por el servidor DHCP.

- El cliente puede renovar su dirección IP antes de que expire el tiempo de arrendamiento (lease time) enviando un mensaje ***DHCPREQUEST*** al servidor DHCP. El servidor responde con un ***DHCPACK***, confirmando la renovación de la dirección IP y actualizando el tiempo de arrendamiento en su base de datos. En caso de que haya expirado el tiempo de arrendamiento el servidor devuelve un ***DHCPNAK*** y el cliente debe repetir el proceso de descubrimiento y solicitud de dirección IP.

## Configuración
Es recomendable que si se tiene más de un servidor DHCP cada uno otorgue un rango configurado de direcciones IP.

Cualquier dispositivo puede ser un servidor DHCP, pero es recomendable que sea un servidor dedicado para evitar conflictos de direcciones IP y problemas de configuración en la red. Además, se recomienda configurar el servidor DHCP con una lista de direcciones IP reservadas para dispositivos específicos, como servidores o impresoras, para garantizar que siempre tengan la misma dirección IP asignada.

En sistemas basados en Linux la configuración se encuentra en el archivo `/etc/dhcp/dhcpd.conf`, mientras que en sistemas basados en Windows se puede configurar a través de la interfaz gráfica del servidor DHCP.

### Ejemplo de archivo dhcpd.conf
```bash
# Configuración global
default-lease-time 600; # Tiempo de arrendamiento por defecto en segundos
max-lease-time 7200; # Tiempo máximo de arrendamiento en segundos
# Configuración de la subred
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200; # Rango de direcciones IP disponibles para asignar
  option routers 192.168.1.1; # Dirección de la puerta de enlace predeterminada
  option domain-name-servers 8.8.8.8, 8.8.4.4; # Direcciones de los servidores DNS
}

# Configuración de direcciones IP reservadas
host servidor {
  hardware ethernet 00:11:22:33:44:55; # Dirección MAC del dispositivo
  fixed-address 192.168.1.10; # Dirección IP fija para el dispositivo
}
host impresora {
  hardware ethernet 66:77:88:99:AA:BB; # Dirección MAC del dispositivo
  fixed-address 192.168.1.11; # Dirección IP fija para el dispositivo
}
```