# NAT (Network Address Translation)
## Introducción
NAT es un mecanismo que permite a los dispositivos de una red privada acceder a Internet utilizando una única dirección IP pública. Esto se logra mediante la traducción de las direcciones IP privadas de los dispositivos a una dirección IP pública antes de enviar los paquetes a Internet. NAT es ampliamente utilizado en redes domésticas y empresariales para conservar direcciones IP públicas y mejorar la seguridad de la red.

## Ejemplo de funcionamiento NAT
Cada dispositivo en una red privada tiene una dirección IP privada única (por ejemplo, 192.168.1.10), en NAT se utiliza una dirección IP pública POR CADA DISPOSITIVO, por lo que si hay 10 dispositivos en la red privada, se necesitan 10 direcciones IP públicas:

- Un dispositivo en una red privada con una dirección IP privada (por ejemplo, 192.168.1.10) desea acceder a Internet.
- El router o firewall que implementa NAT traduce la dirección IP privada a una dirección IP pública (por ejemplo, 203.0.113.1).
- Los paquetes se envían a Internet con la dirección IP pública.
- Cuando se recibe una respuesta de Internet, el router o firewall traduce la dirección IP pública de vuelta a la dirección IP privada del dispositivo.

## Ejemplo de funcionamiento NAPT (Network Address Port Translation)
### Overloading / Masquerading (MASQ)
Es una mejora de NAT que permite a múltiples dispositivos en una red privada compartir una única dirección IP pública utilizando diferentes números de puerto. Esto se logra mediante la traducción de las direcciones IP privadas y los números de puerto a una dirección IP pública y un número de puerto único antes de enviar los paquetes a Internet. NAPT es ampliamente utilizado en redes domésticas y empresariales para conservar direcciones IP públicas y mejorar la seguridad de la red. Una buena práctica es utilizar el mismo puerto y cambiar la IP, ya que si se cambia el puerto y la IP, el firewall puede bloquear la conexión.

- Un dispositivo en una red privada con una dirección IP privada (por ejemplo, 192.168.1.10) desea acceder a Internet.

- El router o firewall que implementa NAPT traduce la dirección IP privada y el número de puerto a una dirección IP pública y un número de puerto único (por ejemplo, 203.0.113.1:8080).

- Los paquetes se envían a Internet con la dirección IP pública y el número de puerto único.

- Cuando se recibe una respuesta de Internet, el router o firewall traduce la dirección IP pública y el número de puerto único de vuelta a la dirección IP privada y el número de puerto del dispositivo.

- Si otro dispositivo en la red privada (por ejemplo, 192.168.1.11) desea acceder a Internet, también se le asigna el mismo número de puerto único (por ejemplo, 203.0.113.1:8081).

- Pero si otro dispositivo en la red privada (por ejemplo, 

## Tabla de Connection Tracking
Es una tabla que mantiene un registro de todas las conexiones activas en una red que utiliza NAT o NAPT. Esta tabla permite al router o firewall realizar un seguimiento de las conexiones y asegurarse de que los paquetes entrantes se enruten correctamente a los dispositivos de la red privada. La tabla de Connection Tracking contiene información sobre las direcciones IP privadas y públicas, los números de puerto, el estado de la conexión y otros detalles relevantes.

### Comando para visualizar la tabla de Connection Tracking en Linux:
```bash
sudo conntrack -L
```

## Port Forwarding
El Port Forwarding es una técnica que permite redirigir el tráfico entrante en un puerto específico de una dirección IP pública a un puerto específico de una dirección IP privada en la red interna. Esto es útil para permitir el acceso a servicios internos desde Internet, como servidores web, servidores de correo electrónico o cámaras de seguridad. El Port Forwarding se configura en el router o firewall que implementa NAT o NAPT y requiere que se especifiquen la dirección IP privada del dispositivo interno, el puerto interno y el puerto externo que se utilizará para acceder al servicio desde Internet.