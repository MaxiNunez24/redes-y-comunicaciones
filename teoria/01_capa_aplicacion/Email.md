# E-Mail
## Introducción
E-Mail (Electronic Mail) es un servicio de comunicación que permite enviar y recibir mensajes electrónicos a través de internet.

## Historia
El correo electrónico tiene sus raíces en los primeros sistemas de comunicación por computadora desarrollados en la década de 1960. Sin embargo, el primer sistema de correo electrónico moderno fue creado en 1971 por Ray Tomlinson, quien implementó el uso del símbolo "@" para separar el nombre del usuario del nombre del servidor.

## Funcionamiento
El funcionamiento del correo electrónico se basa en la utilización de protocolos de comunicación que permiten la transmisión de mensajes entre clientes y servidores de correo. Los usuarios pueden enviar y recibir correos electrónicos utilizando aplicaciones de correo electrónico, como Microsoft Outlook, Gmail, Thunderbird, entre otros. Los mensajes se componen de un encabezado (que incluye información como el remitente, destinatario, asunto y fecha) y un cuerpo (que contiene el contenido del mensaje).

## Protocolos
### SMTP (Simple Mail Transfer Protocol)
SMTP es el protocolo estándar para enviar correos electrónicos. Funciona en el puerto 25 y se encarga de la transmisión de los mensajes desde el cliente de correo al servidor de correo y entre servidores de correo. Se responde con HELO, MAIL FROM, RCPT TO, DATA y QUIT para establecer la comunicación y enviar el mensaje.

### ESMTP (Extended Simple Mail Transfer Protocol)
ESMTP es una extensión del protocolo SMTP que permite la transmisión de mensajes con características adicionales, como la autenticación de usuarios y el envío de archivos adjuntos. Funciona en el mismo puerto que SMTP (25) y es compatible con la mayoría de los servidores de correo modernos. Se responde con EHLO, MAIL FROM, RCPT TO, DATA y QUIT para establecer la comunicación y enviar el mensaje.

### ESTMPS (Extended Simple Mail Transfer Protocol Secure)
ESTMPS es una versión segura de ESMTP que utiliza cifrado SSL/TLS para proteger la comunicación entre el cliente de correo y el servidor de correo. Funciona en el puerto 465 y ofrece las mismas funcionalidades que ESMTP, pero con mayor seguridad. Se responde con EHLO, MAIL FROM, RCPT TO, DATA y QUIT para establecer la comunicación y enviar el mensaje.

### IMAP4 (Internet Message Access Protocol version 4)
IMAP4 es un protocolo que permite acceder a los correos electrónicos almacenados en un servidor de correo. Funciona en el puerto 143 y permite a los usuarios gestionar sus correos electrónicos desde múltiples dispositivos, manteniendo los mensajes en el servidor.

### IMAPS (Internet Message Access Protocol Secure)
IMAPS es una versión segura de IMAP4 que utiliza cifrado SSL/TLS para proteger la comunicación entre el cliente de correo y el servidor de correo. Funciona en el puerto 993 y ofrece las mismas funcionalidades que IMAP4, pero con mayor seguridad.

### POP3 (Post Office Protocol version 3)
POP3 es un protocolo que permite descargar los correos electrónicos desde un servidor de correo al cliente de correo. Funciona en el puerto 110 y, a diferencia de IMAP, los mensajes se eliminan del servidor después de ser descargados, lo que significa que solo se pueden acceder desde el dispositivo donde se descargaron.

### POP3S (Post Office Protocol version 3 Secure)
POP3S es una versión segura de POP3 que utiliza cifrado SSL/TLS para proteger la comunicación entre el cliente de correo y el servidor de correo. Funciona en el puerto 995 y ofrece las mismas funcionalidades que POP3, pero con mayor seguridad.

### PGP (Pretty Good Privacy)
PGP es un protocolo de cifrado que permite proteger la privacidad y autenticidad de los correos electrónicos. Utiliza un sistema de claves públicas y privadas para cifrar y descifrar los mensajes, garantizando que solo el destinatario previsto pueda leer el contenido del correo electrónico. 

## Servidores de correo
Los servidores de correo son sistemas que almacenan y gestionan los correos electrónicos. Existen diferentes tipos de servidores de correo:

### MAA (Mail Access Agent) - Servidores de correo entrante (IMAP y POP3) 
Los servidores de correo entrante permiten a los usuarios acceder a sus correos electrónicos desde diferentes dispositivos.

### MTA (Mail Transfer Agent) - Servidores de correo saliente (SMTP). 
Los servidores de correo saliente se encargan de enviar los mensajes a los destinatarios.

### MUA (Mail User Agent) - Clientes de correo electrónico.
Los clientes de correo electrónico son aplicaciones que permiten a los usuarios enviar, recibir y gestionar sus correos electrónicos. Algunos ejemplos de clientes de correo electrónico son Microsoft Outlook, Mozilla Thunderbird y Apple Mail. Se comunican a su MTA mediante los protocolos SMTP, ESMTP y ESMPTS por el puerto 25, 587 y 465 respectivamente. Para recibir correos electrónicos, se comunican con su MAA mediante los protocolos IMAP4, IMAPS, POP3 y POP3S por los puertos 143, 993, 110 y 995 respectivamente.
