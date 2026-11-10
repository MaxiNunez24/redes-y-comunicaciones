# Ethernet
## Introducción
El Ethernet es una tecnología de red de área local (LAN) que permite la comunicación entre dispositivos mediante el uso de cables y protocolos específicos. Fue desarrollada en la década de 1970 por Robert Metcalfe y su equipo en Xerox PARC, y desde entonces ha evolucionado para convertirse en uno de los estándares más utilizados en redes locales. Ethernet utiliza un enfoque de transmisión de datos basado en tramas, donde los datos se dividen en unidades llamadas tramas que se envían a través del medio físico. Esta tecnología ha sido fundamental para el crecimiento y desarrollo de las redes informáticas, proporcionando una base sólida para la comunicación eficiente y confiable entre dispositivos conectados.

## Direcciones MAC
Son direcciones físicas de 48 bits (6 bytes) que identifican de manera única a cada dispositivo en una red local. Estas direcciones son asignadas por el fabricante del hardware y se utilizan para garantizar que los datos enviados a través de la red lleguen al dispositivo correcto. Son esenciales para la comunicación en redes Ethernet, ya que permiten que los dispositivos se reconozcan entre sí y establezcan conexiones de manera eficiente. Su formato se representa comúnmente en notación hexadecimal, dividida en seis grupos de dos dígitos separados por dos puntos o guiones o puntos (por ejemplo, 00:1A:2B:3C:4D:5E). 

## Formato de trama (Frame) 
Son las unidades de datos que se transmiten a través de la red Ethernet. Cada trama contiene información de control y datos, y su estructura está definida por el estándar IEEE 802.3. Una trama típica de Ethernet incluye los siguientes campos:
1. **Preambulo**: Una secuencia de bits que permite a los dispositivos sincronizarse antes de la transmisión de datos.
2. **Dirección MAC de destino**: La dirección física del dispositivo al que se envía la trama. Va antes que la dirección MAC de origen porque es necesario que el dispositivo receptor pueda identificar si la trama le pertenece o no.
3. **Dirección MAC de origen**: La dirección física del dispositivo que envía la trama.
4. **Tipo/Longitud**: Indica el tipo de protocolo de red que se está utilizando o la longitud de los datos en la trama.
5. **Datos**: La información que se está transmitiendo, que puede variar en tamaño dependiendo del protocolo y la aplicación.
6. **FCS (Frame Check Sequence)**: Un campo de verificación que permite a los dispositivos detectar errores en la transmisión de datos.


### Tipos de Ethernet
Existen varios tipos de Ethernet, cada uno con diferentes velocidades y características. Algunos de los más comunes incluyen:
- **Ethernet 10BASE-T**: Opera a 10 Mbps y utiliza cables de par trenzado. Es uno de los tipos más antiguos y todavía se encuentra en algunas redes.
- **Fast Ethernet 100BASE-TX**: Opera a 100 Mbps y también utiliza cables de par trenzado. Es una mejora significativa sobre el Ethernet original y es ampliamente utilizado en redes locales.
- **Gigabit Ethernet 1000BASE-T**: Opera a 1 Gbps y utiliza cables de par trenzado. Es común en redes modernas y permite una mayor velocidad de transmisión de datos.
- **10 Gigabit Ethernet 10GBASE-T**: Opera a 10 Gbps y utiliza cables de par trenzado. Es utilizado en entornos de alta demanda de ancho de banda, como centros de datos y redes empresariales.

## Flujo de una comunicación Ethernet
El flujo de comunicación en una red Ethernet sigue un proceso estructurado que permite la transmisión eficiente de datos entre dispositivos. A continuación, se describe el flujo típico de una comunicación Ethernet:
1. **Inicio de la comunicación**: Un dispositivo que desea enviar datos inicia la comunicación generando una trama Ethernet. Esta trama incluye la dirección MAC de destino, la dirección MAC de origen, el tipo/longitud, los datos y el FCS.
2. **Transmisión de la trama**: La trama se envía a través del medio de transmisión (como cables de par trenzado o fibra óptica) hacia el dispositivo de destino. Durante este proceso, los dispositivos en la red escuchan el medio para detectar si la trama está destinada a ellos.
3. **Recepción de la trama**: El dispositivo de destino recibe la trama y verifica la dirección MAC de destino. Si coincide con su propia dirección MAC, el dispositivo acepta la trama; de lo contrario, la descarta.
4. **Verificación de errores**: El dispositivo receptor utiliza el campo FCS para verificar la integridad de los datos recibidos. Si se detectan errores, el dispositivo puede solicitar la retransmisión de la trama o descartar los datos, dependiendo del protocolo utilizado. 

### Flujo de una comunicación Ethernet con IPv4
Cuando se utiliza el protocolo IPv4 en una comunicación Ethernet, el flujo de datos sigue un proceso similar al descrito anteriormente, pero con la adición de la encapsulación de los datos en paquetes IPv4. A continuación, se describe el flujo de una comunicación Ethernet con IPv4:
1. **Inicio de la comunicación**: Un dispositivo que desea enviar datos genera un paquete IPv4 que contiene la información de la capa de red, incluyendo las direcciones IP de origen y destino, así como otros campos necesarios para la entrega de datos. Este paquete se encapsula dentro de una trama Ethernet, que incluye la dirección MAC de destino, la dirección MAC de origen, el tipo/longitud, los datos (que ahora contienen el paquete IPv4) y el FCS.
2. **Transmisión de la trama**: El dispositivo revisa su tabla de routeo para determinar si la dirección IP de destino se encuentra en la misma red local o si debe enviarse a través de un router. Si la dirección IP de destino está en la misma red local, el dispositivo envía la trama Ethernet directamente al dispositivo de destino. Si la dirección IP de destino está en una red diferente, el dispositivo envía la trama al router, que se encargará de enrutar el paquete hacia su destino final.
3. **Recepción de la trama**: El dispositivo de destino recibe la trama Ethernet y verifica la dirección MAC de destino. Si coincide con su propia dirección MAC, el dispositivo acepta la trama y extrae el paquete IPv4 encapsulado. Si la dirección MAC no coincide, la trama se descarta.
4. **Procesamiento del paquete IPv4**: Una vez que el dispositivo de destino ha aceptado la trama, procesa el paquete IPv4. Esto incluye verificar la dirección IP de destino, asegurarse de que el paquete esté destinado a él y realizar cualquier acción necesaria según el protocolo de la capa de red. Si el paquete es válido y está destinado al dispositivo, se entrega a la capa de transporte para su procesamiento adicional. Si el paquete no es válido o no está destinado al dispositivo, se descarta y no se realiza ninguna acción adicional.