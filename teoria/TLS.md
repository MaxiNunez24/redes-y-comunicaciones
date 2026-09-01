# Transport Layer Security
A partir de HTTP/2 las conexiones se utilizan principalmente sobre TLS, lo que proporciona una capa adicional de seguridad en la comunicación entre el cliente y el servidor. Esta capa de seguridad cifra los datos transmitidos, protegiendo la información sensible y garantizando la integridad de los datos durante la comunicación. Además, TLS también permite la autenticación del servidor, lo que ayuda a prevenir ataques de suplantación de identidad y garantiza que el cliente se esté comunicando con el servidor legítimo. Se utiliza el puerto 443 en lugar del 8080, se pueden crear un servidor para cada puerto para mantener la retrocompatibilidad si así se desea. 

## La secuencia de establecimiento de la conexión pasa a ser:
- Se establece la conexión TCP entre el cliente y el servidor.
- Cliente envía un mensaje de "Client Hello" al servidor, indicando las versiones de TLS y los algoritmos de cifrado que soporta.
- Servidor responde con un mensaje de "Server Hello", seleccionando la versión de TLS y el algoritmo de cifrado a utilizar, y enviando su certificado digital para autenticarse.
- Cliente verifica el certificado del servidor y, si es válido, genera una clave de sesión y la envía al servidor cifrada con la clave pública del certificado.
- Servidor descifra la clave de sesión y ambos establecen una conexión segura utilizando la clave de sesión compartida para cifrar y descifrar los datos transmitidos.
- Una vez establecida la conexión segura, el cliente y el servidor pueden intercambiar datos de manera confidencial y protegida contra posibles ataques de interceptación o manipulación.

### HTTP SSL (Secure Sockets Layer)
Un certificado SSL (Secure Sockets Layer) es un protocolo de seguridad que cifra los datos transmitidos entre un navegador web y un servidor, permitiendo una conexión segura bajo el protocolo HTTPS.

### Gráfico resumen de la secuencia de establecimiento de la conexión HTTP SSL:
```
Cliente                                      Servidor
   |                                            |
   |-------- Client Hello --------------------->| Algoritmos Soportados valor aleatorio
   |                                            |
   |<------- Server Hello ----------------------|
   |                                            |
   |<------- Cert + random ---------------------|
   |                                            |
   |<------- Server Hello Done -----------------|
   |                                            |
   |-------- ClientKeyXchange ----------------->| 
   |                                            |
   |-------> Generación de clave de sesión      |
   |                                            |
   |-------> Envío de clave de sesión cifrada   |
   |                                            |
   |<------- Descifrado de clave de sesión      |
   |                                            | 
   |-------> Establecimiento de conexión segura |
   |                                            |
   |<------ Intercambio de datos cifrados       |
   |                                            |
```

