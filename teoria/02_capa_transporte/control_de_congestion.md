# Control de congestion

## UDP vs TCP
En UDP al no existir un mecanismo de control de congestión, el emisor puede enviar datos a una velocidad muy alta sin tener en cuenta la capacidad de la red, lo que puede llevar a la pérdida de paquetes y a la saturación de la red. Por otro lado, TCP implementa un mecanismo de control de congestión que ajusta dinámicamente la velocidad de envío de datos en función de la capacidad de la red y la detección de congestión.

## Old Version vs Tahoe vs Reno
- La versión antigua de TCP no implementaba un mecanismo de control de congestión efectivo, lo que llevaba a la congestión de la red y a la pérdida de paquetes. 

- La versión Tahoe introdujo un mecanismo de control de congestión basado en el algoritmo de Slow Start y Congestion Avoidance, lo que mejoró significativamente el rendimiento de la red.

- La versión Reno mejoró aún más el mecanismo de control de congestión al introducir el algoritmo de Fast Retransmit y Fast Recovery, lo que permitió una recuperación más rápida de la pérdida de paquetes y una mayor eficiencia en la transmisión de datos.

## Cwnd (congestion window) 
Es una variable que controla la cantidad de datos que un emisor puede enviar sin recibir un ACK. El tamaño de cwnd se ajusta dinámicamente en función de la detección de congestión en la red en TCP. Cuando se detecta congestión, el tamaño de cwnd se reduce para evitar que se envíen demasiados datos y se agrave la congestión. Por otro lado, cuando no hay congestión, el tamaño de cwnd puede aumentar para permitir un mayor flujo de datos.

### W = MIN(RWND, CWND)
Window = Mínimo entre la ventana de recepción (RWND) y la ventana de congestión (CWND). La ventana de recepción (RWND) es el tamaño máximo de datos que el receptor puede aceptar sin desbordar su búfer, mientras que la ventana de congestión (CWND) es el tamaño máximo de datos que el emisor puede enviar sin recibir un acuse de recibo (ACK). El valor mínimo entre estas dos ventanas determina la cantidad máxima de datos que se pueden enviar en un momento dado.

## SS vs CA (Slow Start vs Congestion Avoidance) - Tahoe
- Slow Start (SS): Es un algoritmo de orden **exponencial** que se utiliza al inicio de una conexión TCP para aumentar rápidamente el tamaño de cwnd. Comienza con un valor pequeño y lo duplica cada vez que se recibe un ACK, hasta alcanzar un umbral (ssthresh). Una vez alcanzado el umbral, se pasa al algoritmo de Congestion Avoidance.
- Congestion Avoidance (CA): Es un algoritmo de orden **lineal** que se utiliza después de Slow Start para evitar la congestión en la red. En este algoritmo, el tamaño de cwnd se incrementa de manera más lenta, generalmente en una cantidad fija por cada RTT (Round Trip Time) hasta que se detecta congestión.

### ssthresh (slow start threshold)
Es un umbral que determina cuándo se debe cambiar del algoritmo de Slow Start al de Congestion Avoidance. Cuando el tamaño de cwnd alcanza ssthresh, se pasa del crecimiento exponencial al crecimiento lineal para evitar la congestión en la red. Si se detecta congestión, el valor de ssthresh se ajusta a la mitad del tamaño actual de cwnd, y el tamaño de cwnd se reinicia a un valor pequeño para comenzar nuevamente el proceso de Slow Start.

### RTT (Round Trip Time)
Es el tiempo que toma un segmento de datos para viajar desde el emisor hasta el receptor y regresar al emisor. Se utiliza para calcular el RTO (Retransmission Timeout) y para ajustar el tamaño de la ventana de congestión.

## Fast Retransmit y Fast Recovery - Reno
- Fast Retransmit: Es un mecanismo que permite al emisor retransmitir un segmento perdido sin esperar a que se agote el tiempo de espera (RTO). Esto se logra mediante la detección de 3 ACKs duplicados, lo que indica que un segmento se ha perdido o llegó con errores. Al recibir 3 ACKs duplicados, el emisor retransmite el segmento correspondiente y continúa con el proceso de Congestion Avoidance.

- Fast Recovery: Es un mecanismo que permite al emisor recuperarse rápidamente de la pérdida de paquetes sin tener que reiniciar el proceso de Slow Start. Después de retransmitir un segmento perdido mediante Fast Retransmit, el emisor ajusta el tamaño de cwnd y ssthresh para continuar con el proceso de Congestion Avoidance, evitando así una caída drástica en la velocidad de transmisión.

## Fases
1. **Slow Start**: El emisor comienza con un valor pequeño de cwnd y lo duplica cada vez que recibe un ACK.
    - Cuando cwnd alcanza ssthresh, se pasa a la fase de Congestion Avoidance.
    - Si se detecta congestión (por ejemplo, mediante la recepción de 3 ACKs duplicados o un Timeout), se reduce el tamaño de cwnd a 1 MSS y se reinicia el proceso de Slow Start.
    - Si no se detecta congestión, el emisor continúa con el proceso de Slow Start hasta que alcance ssthresh.

2. **Congestion Avoidance**: El emisor incrementa cwnd de manera lineal para evitar la congestión.
    - Si se detecta congestión, se reduce el tamaño de cwnd a la mitad y se ajusta ssthresh en consecuencia.
    - Si no se detecta congestión, el emisor continúa con el proceso de Congestion Avoidance hasta que se complete la transmisión de datos.

3. **Fast Retransmit**: Si se reciben 3 ACKs duplicados, se retransmite el segmento perdido sin esperar al timeout.
    - Se reduce el tamaño de **cwnd** y de **ssthresh** a la **mitad** para continuar con el proceso de Congestion Avoidance.
    - Si no se detecta congestión, el emisor continúa con el proceso de Congestion Avoidance hasta que se complete la transmisión de datos.

4. **Fast Recovery**: El emisor se recupera rápidamente de la pérdida de paquetes.
    - Se ajusta

## Timeout vs 3 Dup ACKs
Cuando se reciben 3 ACKs duplicados, se considera que ha habido una pérdida de paquetes y se inicia un proceso de retransmisión rápida. En lugar de esperar a que se produzca un Timeout, el emisor retransmite el segmento perdido y continúa con el proceso de Congestion Avoidance.

### Dato sobre Timeout
El Timeout es siempre 4 veces más grande que el RTT (Round Trip Time) estimado, y se calcula utilizando un algoritmo de estimación de RTT y su variación. Cuando se produce un Timeout, se considera que ha habido una pérdida de paquetes y se reduce el tamaño de cwnd a 1 MSS (Maximum Segment Size) y se reinicia el proceso de Slow Start.

## AIMD (Additive Increase / Multiplicative Decrease)
El algoritmo AIMD es un enfoque de control de congestión que se basa en la idea de aumentar la ventana de congestión (CWND) de manera aditiva cuando no hay congestión, y disminuirla de manera multiplicativa cuando se detecta congestión. Este enfoque ayuda a mantener un equilibrio entre la utilización del ancho de banda y la estabilidad de la red.

## Otros algoritmos de control de congestión
- **TCP New Reno**: Este algoritmo es una mejora de TCP Reno que introduce un mecanismo de retransmisión rápida mejorado para manejar múltiples pérdidas de paquetes dentro de una misma ventana de transmisión. TCP New Reno permite al emisor retransmitir segmentos perdidos sin tener que esperar a que se agote el tiempo de espera (RTO), lo que mejora la eficiencia en la recuperación de errores y reduce la latencia en la transmisión de datos.

- **TCP Vegas**: Este algoritmo utiliza la estimación del RTT para ajustar dinámicamente el tamaño de la ventana de congestión (CWND) y evitar la congestión antes de que ocurra. TCP Vegas compara el RTT estimado con el RTT real para determinar si la red está congestionada y ajusta CWND en consecuencia. Este algoritmo tiene la debilidad con respecto a los otros algoritmos de control de congestión, ya que puede ser menos agresivo en la utilización del ancho de banda disponible, lo que puede llevar a un menor rendimiento en ciertas condiciones de red. La mejor eficiencia de TCP Vegas se logra si todos utilizan este algoritmo, ya que de lo contrario puede ser superado por otros algoritmos más agresivos en la utilización del ancho de banda disponible.

- **TCP Cubic**: Este algoritmo utiliza una función cúbica para ajustar el tamaño de la ventana de congestión (CWND) en función del tiempo desde la última pérdida de paquetes. TCP Cubic es especialmente útil en redes de alta velocidad y alta latencia, ya que permite un crecimiento más rápido de CWND después de una pérdida de paquetes, mejorando así el rendimiento en estas condiciones de red.

- **TCP BBR (Bottleneck Bandwidth and Round-trip propagation time)**: Este algoritmo se basa en la estimación del ancho de banda disponible y el tiempo de propagación de ida y vuelta (RTT) para ajustar dinámicamente el tamaño de la ventana de congestión (CWND). TCP BBR busca maximizar el rendimiento de la red al mantener un flujo constante de datos sin saturar la red, lo que lo hace especialmente útil en redes con alta variabilidad en el ancho de banda y la latencia.

- **TCP Hybla**: Este algoritmo está diseñado para mejorar el rendimiento de TCP en redes de alta latencia, como las conexiones satelitales. TCP Hybla ajusta el tamaño de la ventana de congestión (CWND) y el tiempo de espera para la retransmisión (RTO) en función de la latencia de la red, lo que permite un mejor aprovechamiento del ancho de banda disponible y una mayor eficiencia en la transmisión de datos.

- **TCP Illinois**: Este algoritmo combina técnicas de control de congestión basadas en la estimación del RTT y el ancho de banda disponible para ajustar dinámicamente el tamaño de la ventana de congestión (CWND). TCP Illinois busca mejorar el rendimiento en redes con alta variabilidad en el ancho de banda y la latencia, al tiempo que mantiene la estabilidad de la red y evita la congestión.

- **TCP Compound**: Este algoritmo combina técnicas de control de congestión basadas en la estimación del RTT y el ancho de banda disponible, así como un enfoque de control de congestión basado en la pérdida de paquetes. TCP Compound ajusta dinámicamente el tamaño de la ventana de congestión (CWND) en función de las condiciones de la red, lo que permite un mejor aprovechamiento del ancho de banda disponible y una mayor eficiencia en la transmisión de datos. Es el algoritmo utilizado por defecto en Windows Vista y versiones posteriores, y está diseñado para mejorar el rendimiento de TCP en redes de alta velocidad y alta latencia.

- **TCP Westwood**: Este algoritmo se centra en la estimación del ancho de banda disponible y la pérdida de paquetes para ajustar dinámicamente el tamaño de la ventana de congestión (CWND) y el tiempo de espera para la retransmisión (RTO). TCP Westwood busca mejorar el rendimiento en redes con alta variabilidad en el ancho de banda y la latencia, al tiempo que mantiene la estabilidad de la red y evita la congestión.


## TCP + IP ECT + CE. ECN 