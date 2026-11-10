# Detección de colisión (CSMA / CD)

## Introducción
La detección de colisiones es un mecanismo utilizado en redes de área local (LAN) para gestionar el acceso al medio compartido y evitar que múltiples dispositivos transmitan datos al mismo tiempo, lo que podría causar interferencias y pérdida de información. Este mecanismo es especialmente relevante en redes Ethernet que utilizan el protocolo CSMA/CD (Carrier Sense Multiple Access with Collision Detection).

### Funcionamiento del CSMA/CD
1. **Carrier Sense (Detección de portadora)**: Antes de transmitir, un dispositivo escucha el canal para determinar si está libre o ocupado. Si el canal está ocupado, el dispositivo espera un tiempo aleatorio antes de intentar transmitir nuevamente.

2. **Multiple Access (Acceso múltiple)**: Todos los dispositivos en la red tienen igual derecho a acceder al medio compartido. Esto significa que cualquier dispositivo puede intentar transmitir datos en cualquier momento, siempre y cuando el canal esté libre.

3. **Collision Detection (Detección de colisiones)**: Si dos o más dispositivos intentan transmitir datos al mismo tiempo, se produce una colisión. Los dispositivos detectan esta colisión y detienen la transmisión. Luego, esperan un tiempo aleatorio antes de intentar transmitir nuevamente.

