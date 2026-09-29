# TCP (Transmission Control Protocol)
TCP es un protocolo de comunicación confiable y orientado a conexión que se utiliza en la capa de transporte del modelo OSI. Proporciona una comunicación segura y garantiza la entrega de datos entre aplicaciones en diferentes dispositivos de una red.

## Características principales
- **Orientado a conexión**: TCP establece una conexión entre el emisor y el receptor antes de enviar datos, lo que permite una comunicación confiable y ordenada.

- **Garantía de entrega**: TCP garantiza que los datos enviados lleguen a su destino sin pérdida ni duplicación. Si se detecta algún error, TCP retransmite los datos.

- **Control de flujo**: TCP utiliza un mecanismo de control de flujo para evitar que el emisor envíe datos más rápido de lo que el receptor puede procesar, asegurando una comunicación eficiente.

- **Control de congestión**: TCP implementa algoritmos de control de congestión para evitar la saturación de la red y mejorar el rendimiento general de la comunicación.

- **Segmentación de datos**: TCP divide los datos en segmentos más pequeños antes de enviarlos, lo que facilita la transmisión y permite la reensamblación de los datos en el receptor.

## Encabezado TCP
El encabezado de TCP tiene un tamaño mínimo de 20 bytes y contiene información crucial para la comunicación, incluyendo:
- **Puerto de origen**: Identifica el puerto del remitente.
- **Puerto de destino**: Identifica el puerto del destinatario.
- **Número de secuencia**: Indica el orden de los segmentos enviados, lo que permite al receptor reensamblar los datos correctamente.
- **Número de acuse de recibo (ACK)**: Indica el número de secuencia del siguiente segmento que el receptor espera recibir, confirmando la recepción de los datos anteriores.
- **Longitud del encabezado**: Indica el tamaño del encabezado TCP.
- **Banderas de control**: Incluyen indicadores como SYN, ACK, FIN, RST, PSH y URG, que controlan el establecimiento, la terminación y la gestión de la conexión.
- **Ventana de recepción**: Indica la cantidad de datos que el receptor está dispuesto a aceptar, lo que permite el control de flujo.
- **Checksum**: Se utiliza para verificar la integridad de los datos y detectar errores durante la transmisión.
- **Puntero urgente**: Indica la posición de los datos urgentes en el flujo de datos, si los hay.

## Establecimiento de conexión (Three-way handshake)
El establecimiento de una conexión TCP se realiza mediante un proceso llamado "three-way handshake", que consta de tres pasos:
1. **SYN**: El cliente envía un segmento SYN (synchronize) al servidor para iniciar la conexión.
2. **SYN-ACK**: El servidor responde con un segmento SYN-ACK (synchronize-acknowledge) para confirmar la recepción del segmento del cliente.
3. **ACK**: El cliente envía un segmento ACK (acknowledge) al servidor para confirmar la recepción del segmento del servidor y completar el establecimiento de la conexión.

## Terminación de conexión (Four-way handshake)
La terminación de una conexión TCP se realiza mediante un proceso llamado "four-way handshake", que consta de cuatro pasos:
1. **FIN**: El cliente envía un segmento FIN (finish) al servidor para indicar que desea finalizar la conexión.
2. **ACK**: El servidor responde con un segmento ACK para confirmar la recepción del segmento FIN del cliente.
3. **FIN**: El servidor envía un segmento FIN al cliente para indicar que también desea finalizar la conexión.
4. **ACK**: El cliente responde con un segmento ACK para confirmar la recepción del segmento FIN del servidor y completar la terminación de la conexión.

## Relación entre SEQ y ACK
En TCP, los números de secuencia (SEQ) y los números de acuse de recibo (ACK) están estrechamente relacionados. El número de secuencia indica el orden de los segmentos enviados, mientras que el número de acuse de recibo indica el siguiente número de secuencia que el receptor espera recibir. Esta relación permite al receptor reensamblar los datos correctamente y garantiza la entrega confiable de los datos. Por ejemplo, si el emisor envía un segmento con un número de secuencia de 100 y el receptor recibe correctamente ese segmento, enviará un acuse de recibo con un número de secuencia de 101, indicando que espera recibir el siguiente segmento con ese número de secuencia. Y viceversa, si el receptor recibe un segmento con un número de secuencia de 101, enviará un acuse de recibo con un número de secuencia de 102, indicando que espera recibir el siguiente segmento con ese número de secuencia. Esta relación entre SEQ y ACK permite a TCP garantizar la entrega confiable de los datos y mantener el orden correcto de los segmentos durante la transmisión.

## Stop and Wait (SW)
El protocolo Stop and Wait es un método simple de control de flujo y retransmisión utilizado en TCP. En este método, el emisor envía un segmento y espera un acuse de recibo (ACK) del receptor antes de enviar el siguiente segmento. Si no se recibe un ACK dentro de un tiempo determinado, el emisor retransmite el segmento. Este método garantiza la entrega confiable de datos, pero puede ser ineficiente en redes con alta latencia, ya que el emisor debe esperar a que el receptor confirme la recepción de cada segmento antes de enviar el siguiente.


## Go Back-N (GBN) y Selective Repeat (SR)
TCP utiliza mecanismos de control de flujo y retransmisión para garantizar la entrega confiable de datos. Dos de los algoritmos más comunes son Go Back-N (GBN) y Selective Repeat (SR):

- **Go Back-N (GBN)**: En este algoritmo, el emisor puede enviar múltiples segmentos sin esperar un acuse de recibo, pero si se detecta un error en un segmento, el emisor retransmite ese segmento y todos los segmentos posteriores, incluso si algunos de ellos fueron recibidos correctamente. 

- **Selective Repeat (SR)**: En este algoritmo, el emisor puede enviar múltiples segmentos sin esperar un acuse de recibo, y si se detecta un error en un segmento, solo se retransmite ese segmento específico, no todos los segmentos posteriores. Se debe de indicar al establecer la conexión el uso de SR, por defecto siempre se utiliza GBN, y luego en cada segmento se indica si se utiliza GBN o SR indicando en la parte opcional del encabezado qué segmentos se deben retransmitir. Esto mejora la eficiencia de la comunicación, ya que solo se retransmiten los segmentos que realmente se perdieron o llegaron con errores.

## Pipelining
El pipelining es una técnica utilizada en TCP para mejorar la eficiencia de la transmisión de datos. Permite al emisor enviar múltiples segmentos sin esperar a que se reciban los acuses de recibo (ACK) de cada uno. Esto reduce el tiempo de espera y aumenta el rendimiento de la comunicación, especialmente en redes con alta latencia. Se utiliza el encabezado de ventana de recepción para controlar la cantidad de datos que el receptor puede aceptar, evitando la saturación de la red y asegurando una comunicación eficiente. 
- Para calcular el tamaño óptimo de la ventana se aplica esta fórmula: 
```
Tamaño de la ventana = Ancho de banda * Retardo de ida y vuelta (RTT)
```
