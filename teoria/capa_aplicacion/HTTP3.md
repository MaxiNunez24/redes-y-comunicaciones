# HTTP 3
## Mejoras con respecto a HTTP 2
### Uso de QUIC:
HTTP/3 utiliza QUIC (Quick UDP Internet Connections) como protocolo de transporte subyacente, en lugar de TCP. QUIC es un protocolo basado en UDP que ofrece varias ventajas, como la reducción de la latencia en la conexión, la mejora en la recuperación de paquetes perdidos y la capacidad de manejar múltiples flujos de datos de manera más eficiente. Esto permite que HTTP/3 tenga un rendimiento mejorado en comparación con HTTP/2, especialmente en redes con alta latencia o pérdida de paquetes.
(Esto debido a que TCP relentizaba la conexión al detectar pérdidas afectando a todos los paquetes)

## UDP (User Datagram Protocol): 
UDP es un protocolo de comunicación sin conexión que permite enviar datagramas (paquetes de datos) entre dispositivos en una red. A diferencia de TCP, UDP no garantiza la entrega de los paquetes ni el orden en que se reciben, lo que lo hace más rápido y eficiente para ciertas aplicaciones, como transmisión de video en tiempo real, juegos en línea y VoIP. Sin embargo, debido a su naturaleza sin conexión, UDP es menos confiable que TCP y requiere que las aplicaciones manejen la pérdida de paquetes y la retransmisión si es necesario.
