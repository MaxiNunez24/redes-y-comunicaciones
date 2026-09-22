# HTTP 2

## Agrega mejoras con respecto a HTTP 1.1
Algunas de estas mejoras son:
### Multiplexación de streams: 
Permite enviar múltiples solicitudes y respuestas en paralelo sobre una única conexión TCP, evitando la necesidad de abrir múltiples conexiones.
- Antes para solicitar varios recursos, se abrían varias conexiones TCP, lo que generaba una sobrecarga y retrasos en la comunicación. Ahora con HTTP/2, se pueden enviar múltiples solicitudes y respuestas de manera concurrente a través de una sola conexión, lo que mejora la eficiencia y reduce la latencia. Esto se logra mediante el uso de streams, que son flujos de datos independientes dentro de la misma conexión. Cada stream tiene un identificador único en un encabezado y puede enviar y recibir datos de manera independiente, lo que permite una comunicación más eficiente entre el cliente y el servidor. Además de trozar los datos en frames, lo que permite enviar partes de la información de manera más eficiente y reducir la latencia.
- Siempre que haya una nueva solicitud, se asigna un nuevo stream con un identificador único, lo que permite que las solicitudes y respuestas se procesen de manera independiente y concurrente. Esto mejora la eficiencia de la comunicación y reduce la latencia en comparación con HTTP/1.1, donde cada solicitud requería una nueva conexión TCP.

### Compresión de encabezados: 
Utiliza un algoritmo de compresión para reducir el tamaño de los encabezados HTTP, lo que mejora la eficiencia de la comunicación.

### Prioridad de streams:
Permite asignar prioridades a las solicitudes, de modo que los recursos más importantes se carguen primero. Al principio se utilizaban pesos pero luego se cambió a un sistema de dependencias, donde un stream puede depender de otro. Esto permite que los recursos más importantes se carguen primero, mejorando la experiencia del usuario y optimizando el rendimiento de la página web. Además de incorporar nuevos encabezados como "priority" y "dependency", que permiten al cliente indicar la prioridad de cada solicitud y establecer relaciones de dependencia entre los streams. Esto permite al servidor optimizar el orden en que se procesan las solicitudes y mejorar la eficiencia de la comunicación.

### Server Push:
Permite al servidor enviar recursos adicionales al cliente antes de que este los solicite, lo que puede mejorar la velocidad de carga de las páginas web. Al haber tenido varios problemas de seguridad, se deshabilitó en la mayoría de los navegadores.

### Uso de conexiones persistentes:
Mantiene las conexiones abiertas para múltiples solicitudes y respuestas, reduciendo la sobrecarga de establecer nuevas conexiones.

### Uso de [TLS](TLS.md): 

### No se usa texto ASCII: 
HPACK codifica los encabezados en binario, lo que reduce el tamaño de los encabezados y mejora la eficiencia de la comunicación.

### Surgen pseudo-headers
Estos contienen información que estaba en la línea inicial y otros headers. Por ej: 
- :method: GET
- :scheme: https o http
- :path: /index.html
- :authority: www.ejemplo.com

### Control de flujo:
Permite al cliente y al servidor controlar la cantidad de datos que se envían en cada stream(Capacidad de Rx) o por TCP (ventana de TCP). 

