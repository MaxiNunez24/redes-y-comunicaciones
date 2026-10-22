# Direcciones IP
## Codificación de direcciones IP
Las direcciones IP se codifican en 32 bits (IPv4) o 128 bits (IPv6). En IPv4, las direcciones se representan en notación decimal con puntos, dividiendo los 32 bits en cuatro octetos de 8 bits cada uno. Por ejemplo, la dirección IP 192.168.1.1 representa los 32 bits divididos en cuatro octetos: 192, 168, 1 y 1.

Se codifican en dos partes:
- **NETID**: Identifica la red a la que pertenece el dispositivo. La longitud del NETID varía según la clase de dirección IP (A, B, C, D o E). Cuanto mayor sea el NETID, menor será el número de hosts disponibles en esa red.

- **HOSTID**: Identifica al dispositivo dentro de la red. La longitud del HOSTID también varía según la clase de dirección IP. Cuanto mayor sea el HOSTID, mayor será el número de hosts disponibles en esa red.

## Modelo jerárquico
Al ser un modelo jerárquico permite al protocolo conocer solamente las direcciones de las redes particulares y no de todos los dispositivos conectados en TODO el mundo a la red, lo que reduce la cantidad de información que debe manejar cada tabla de enrutamiento y mejora la eficiencia del enrutamiento.
