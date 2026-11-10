# Sockets
## Introducción
Los sockets son una interfaz de programación que permite la comunicación entre procesos en una red. Proporcionan un mecanismo para que las aplicaciones puedan enviar y recibir datos a través de la red, utilizando protocolos como TCP o UDP. Los sockets son fundamentales en el desarrollo de aplicaciones web y en la creación de servicios de red.

## Historia
El concepto de sockets fue introducido en la década de 1980 como parte del sistema operativo UNIX. Desde entonces, los sockets se han convertido en una herramienta esencial para la comunicación en red, y su uso se ha extendido a otros sistemas operativos, como Windows y Linux. Los sockets permiten a los desarrolladores crear aplicaciones que pueden comunicarse de manera eficiente y confiable a través de la red, facilitando la transferencia de datos y la interacción entre diferentes sistemas.

## Puertos
Es gracias a los sockets que se pueden utilizar los puertos para identificar a qué aplicación o servicio se le está enviando la información. Cada puerto está asociado a un número único, que permite a los sistemas operativos y a las aplicaciones diferenciar entre múltiples servicios que pueden estar ejecutándose en la misma máquina.
Esto se hace a través de la combinación de la dirección IP del host y el número de puerto, formando un identificador único conocido como "socket". Los puertos se dividen en tres rangos principales: puertos bien conocidos (0-1023), puertos registrados (1024-49151) y puertos dinámicos o privados (49152-65535). Los puertos bien conocidos son utilizados por servicios estándar, como HTTP (puerto 80) y FTP (puerto 21), mientras que los puertos registrados y privados pueden ser utilizados por aplicaciones personalizadas o servicios temporales.

## Tipos de sockets
Existen varios tipos de sockets, cada uno diseñado para un propósito específico en la comunicación en red. Los tipos más comunes de sockets son:
1. **Sockets de flujo (Stream Sockets)**: Utilizan el protocolo TCP para establecer una conexión confiable y orientada a la conexión entre dos procesos. Los datos se transmiten en un flujo continuo, garantizando que se entreguen en el orden correcto y sin pérdida de información. 
2. **Sockets de datagrama (Datagram Sockets)**: Utilizan el protocolo UDP para enviar y recibir datos en forma de paquetes independientes. No se establece una conexión previa, y no se garantiza la entrega ordenada o sin pérdida de los datos.

## Abtracción de sockets
Los sockets proporcionan una abstracción ante el sistema operativo, cada SO tiene una API Sockets (en Linux o WinSocket en Windows) que permite a los desarrolladores crear aplicaciones de red sin preocuparse por los detalles de bajo nivel de la comunicación en red. Esta abstracción facilita el desarrollo de aplicaciones que pueden funcionar en diferentes plataformas y sistemas operativos, ya que los sockets proporcionan una interfaz uniforme para la comunicación en red.
Para todos los sistemas operativos es necesario saber la IP de Origen, la IP de Destino, el Puerto de Origen y el Puerto de Destino y el protocolo de comunicación. Esto se hace a través de la estructura de datos llamada "socket address", que contiene la información necesaria para establecer una conexión entre dos procesos en la red. La dirección del socket se representa mediante una combinación de la dirección IP y el número de puerto, lo que permite a los sistemas operativos y a las aplicaciones identificar de manera única a cada proceso en la red.