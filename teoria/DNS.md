# Domain Name System (DNS)

## Introducción
El Sistema de Nombres de Dominio (DNS) es un sistema jerárquico y descentralizado que traduce nombres de dominio legibles por humanos (como www.ejemplo.com) en direcciones IP numéricas (como 192.168.1.34). En el cual NO existen prioridades de resolución, es decir, no hay un servidor que tenga prioridad sobre otro.

## Por qué se optó por un sistema distribuido
Un Sistema de Nombres de Dominio distribuido permite que la carga de trabajo se reparta entre múltiples servidores, lo que mejora la eficiencia y la disponibilidad del servicio. Además, un sistema distribuido es más resistente a fallos y ataques, ya que no depende de un único punto de fallo. A diferencia de un sistema centralizado, donde un fallo en el servidor principal podría afectar a todos los usuarios, un sistema distribuido permite que otros servidores continúen operando incluso si uno falla.


## Funcionamiento del DNS
El DNS funciona mediante una serie de consultas y respuestas entre clientes y servidores. Cuando un usuario ingresa un nombre de dominio en su navegador, el cliente DNS envía una consulta a un servidor DNS para obtener la dirección IP correspondiente. Si el servidor no tiene la información, puede reenviar la consulta a otros servidores DNS hasta que se encuentre la dirección IP correcta. Una vez que se obtiene la dirección IP, el cliente puede establecer una conexión con el servidor web correspondiente.
- Se le agrega a los navegadores el protocolo DNS para que puedan resolver consultas de nombres de dominio de forma automática al consultar un sitio web.

## Resolvers
Es el servidor que el navegador y/o el cliente tienen configurados para resolver nombres de dominio. Los resolvers pueden ser públicos (como los de Google o Cloudflare) o privados (como los proporcionados por un proveedor de servicios de Internet). Su función principal es recibir las consultas de los clientes y buscar la información necesaria en la jerarquía del DNS para devolver la dirección IP correspondiente.

Estos tienen caché para almacenar temporalmente las respuestas a consultas recientes, lo que permite acelerar el proceso de resolución de nombres de dominio y reducir la carga en los servidores autoritativos.

Todo resolver tiene un tiempo de vida (TTL) para cada registro que almacena en caché, lo que indica cuánto tiempo puede mantener la información antes de considerarla obsoleta y volver a consultar a los servidores autoritativos.

## Servidores autoritativos 
Son servidores encargados de mantener una sola sección del espacio de dominios, y son responsables de responder a las consultas de los resolvers sobre los nombres de dominio que están bajo su autoridad. Estos servidores contienen registros DNS que asocian nombres de dominio con direcciones IP y otros datos relevantes. 
- Dejan un flag `aa` en las consultas con el comando dig para indicar que la respuesta proviene de un servidor autoritativo.

## Top Level Domain (TLD)
Los TLD son los dominios de nivel superior que se encuentran en la parte final de un nombre de dominio, como .com, .org, .net, .edu, entre otros. Estos dominios son administrados por organizaciones específicas y son responsables de mantener la información de los nombres de dominio registrados bajo su TLD.
Para ver la lista completa de TLDs se puede consultar el sitio web de la IANA (Internet Assigned Numbers Authority) en https://www.iana.org/domains/root/db.
Cada TLD tiene un conjunto de servidores autoritativos que son responsables de mantener la información de los nombres de dominio registrados bajo ese TLD. Cuando un resolver necesita obtener la dirección IP de un nombre de dominio, primero consulta los servidores autoritativos del TLD correspondiente para obtener la información necesaria.

## Root Servers
Son actualmente 13 servidores raíz que forman la base de la jerarquía del DNS. Estos servidores son responsables críticos de mantener la información sobre los TLD y dirigir las consultas a los servidores autoritativos correspondientes. Los root servers son operados por diferentes organizaciones en todo el mundo y están distribuidos geográficamente para garantizar la disponibilidad y la redundancia del servicio. Se denominan con letras de la A a la M, y cada uno tiene múltiples instancias distribuidas en diferentes ubicaciones para mejorar la resiliencia y el rendimiento del sistema DNS.


## Resolvers vs Autoritativos
### Resolvers
- Realizan caché de consultas recientes para acelerar la resolución de nombres de dominio.
- Pueden ser públicos o privados, dependiendo de la configuración del cliente.
- Su función principal es recibir consultas de los clientes y buscar la información necesaria en la jerarquía del DNS para devolver la dirección IP correspondiente.
- Tienen un tiempo de vida (TTL) para cada registro que almacenan en caché, lo que indica cuánto tiempo pueden mantener la información antes de considerarla obsoleta y volver a consultar a los servidores autoritativos.
- Realizan consultas recursivas, lo que significa que si no tienen la información necesaria, pueden consultar a otros servidores DNS hasta obtener la respuesta correcta.
### Autoritativos
- No realizan caché de consultas recientes ni consultas recursivas, ya que su función principal es proporcionar información precisa y actualizada sobre los nombres de dominio bajo su autoridad.
- Mantienen registros DNS que asocian nombres de dominio con direcciones IP y otros datos relevantes.
- Son responsables de responder a las consultas de los resolvers sobre los nombres de dominio que están bajo su autoridad.
- Contienen información específica sobre los nombres de dominio registrados bajo su TLD y son responsables de mantener la integridad y precisión de esa información.
- Los servidores raíces son un tipo especial de servidores autoritativos que mantienen información sobre los TLD y dirigen las consultas a los servidores autoritativos correspondientes.

## Fowarder Name Server
Son servidores que actúan como un Proxy entre los resolvers y los servidores autoritativos. Su función principal es recibir consultas de los resolvers y reenviarlas a los servidores autoritativos correspondientes para obtener la información necesaria. Una vez que reciben la respuesta, la devuelven al resolver que realizó la consulta original. Los forwarders pueden ser configurados para filtrar o bloquear ciertas consultas, lo que permite a las organizaciones controlar el acceso a ciertos nombres de dominio o direcciones IP.

## Servidores primarios y secundarios
Los servidores primarios y secundarios son tipos de servidores autoritativos que trabajan juntos para garantizar la disponibilidad y la redundancia de la información de los nombres de dominio. El servidor primario es el servidor autoritativo principal que mantiene la información original de los nombres de dominio bajo su autoridad. El servidor secundario es una copia de seguridad del servidor primario y se utiliza para garantizar que la información esté disponible incluso si el servidor primario falla o no está disponible. Los servidores secundarios reciben actualizaciones periódicas del servidor primario para mantener la información sincronizada y garantizar que los resolvers puedan obtener la información correcta en todo momento. Estas actualizaciones se realizan mediante un proceso llamado transferencia de zona, que permite a los servidores secundarios obtener la información más reciente del servidor primario, este proceso está integrado en el protocolo DNS y se realiza de manera automática utilizando TCP para garantizar la consistencia de la información.

## Tipos de registros
### A
El registro A es un tipo de registro DNS que asocia un nombre de dominio con una dirección IP versión 4 (IPv4). Por ejemplo, el registro A para "www.example.com" podría apuntar a la dirección IP "192.168.1.1".

### AAAA
El registro AAAA es un tipo de registro DNS que asocia un nombre de dominio con una dirección IP versión 6 (IPv6). Por ejemplo, el registro AAAA para "www.example.com" podría apuntar a la dirección IP "2001:0db8:85a3:0000:0000:8a2e:0370:7334".

### NS
El registro NS (Name Server) especifica los servidores DNS que son autoritativos para un dominio. Estos registros indican qué servidores DNS deben ser consultados para obtener información sobre el dominio.

### TXT
El registro TXT (Text) permite almacenar texto asociado a un nombre de dominio. Es comúnmente utilizado para verificar la propiedad de un dominio o para incluir información adicional sobre el dominio.

### TTL
El registro TTL (Time To Live) especifica el tiempo durante el cual un registro DNS debe ser almacenado en caché por los servidores DNS. Una vez que el tiempo de vida del registro ha expirado, los servidores DNS deben consultar nuevamente al servidor primario para obtener la información más reciente.

### Registros SOA (Start of Authority)
Los registros SOA son un tipo de registro DNS que contienen información sobre la autoridad de un dominio y su configuración. Estos registros incluyen información sobre el servidor primario, el correo electrónico del administrador del dominio, el número de serie del registro, los tiempos de actualización y expiración, y otros parámetros relevantes.
- Serial: Es un número que se incrementa cada vez que se realiza un cambio en la zona del dominio. Esto permite a los servidores secundarios saber cuándo deben actualizar su información.
- Refresh: Es el tiempo que un servidor secundario debe esperar antes de verificar si hay actualizaciones en la zona del dominio.
- Retry: Es el tiempo que un servidor secundario debe esperar antes de intentar nuevamente una transferencia de zona fallida.
- Expiry: Es el tiempo que un servidor secundario debe esperar antes de considerar que la información de la zona del dominio ha expirado.
- Neg Cache TTL: Es el tiempo durante el cual se almacena en caché la negación de un registro DNS.


## Envenenamiento de Caché
El envenenamiento de caché es un ataque en el que un atacante introduce información falsa en la caché de un servidor DNS, lo que provoca que los usuarios sean redirigidos a sitios web maliciosos o fraudulentos. Esto puede ocurrir cuando un servidor DNS almacena información incorrecta sobre un nombre de dominio, lo que hace que los usuarios que consultan ese dominio sean dirigidos a una dirección IP controlada por el atacante. El envenenamiento de caché puede tener consecuencias graves, como el robo de información personal, la propagación de malware y la pérdida de confianza en los servicios en línea. 

## DHCP (Dynamic Host Configuration Protocol)
El Protocolo de Configuración Dinámica de Host (DHCP) es un protocolo de red que permite a los dispositivos obtener automáticamente una dirección IP y otra información de configuración de red, como la máscara de subred, la puerta de enlace predeterminada y los servidores DNS. Cuando un dispositivo se conecta a una red, envía una solicitud DHCP para obtener una dirección IP disponible. El servidor DHCP responde con una dirección IP y otra información de configuración, lo que permite al dispositivo comunicarse con otros dispositivos en la red y acceder a Internet. 

## DDNS (Dynamic DNS)

## DoH (DNS over HTTPS)

## DoT (DNS over TLS)

## DNSSec (DNS Security Extensions)
    

## Comandos útiles

### dig command
`dig <hostname>` es una herramienta de línea de comandos que permite realizar consultas DNS para obtener información sobre nombres de dominio y direcciones IP. Al ejecutar este comando, se puede obtener la dirección IP asociada a un nombre de dominio, así como información sobre los servidores DNS que manejan ese dominio. También se pueden realizar consultas inversas para obtener el nombre de dominio asociado a una dirección IP específica. Esta herramienta es útil para diagnosticar problemas de resolución de nombres y verificar la configuración de los servidores DNS.

### MTR (My Trace Route) command
`mtr <hostname>` es una herramienta de diagnóstico de red que combina las funciones de traceroute y ping. Permite rastrear la ruta que siguen los paquetes de datos desde el origen hasta el destino, mostrando información sobre cada salto intermedio y el tiempo que tarda en llegar a cada uno. Esto ayuda a identificar problemas de conectividad y latencia en la red.

### nslookup command
`nslookup <hostname>` es una herramienta de línea de comandos que permite realizar consultas DNS para obtener información sobre nombres de dominio y direcciones IP. Al ejecutar este comando, se puede obtener la dirección IP asociada a un nombre de dominio, así como información sobre los servidores DNS que manejan ese dominio. También se pueden realizar consultas inversas para obtener el nombre de dominio asociado a una dirección IP específica. Esta herramienta es útil para diagnosticar problemas de resolución de nombres y verificar la configuración de los servidores DNS.

### Cuándo utilizar cada comando
- `dig`: Es útil para obtener información detallada sobre un nombre de dominio específico, incluyendo registros DNS y servidores autoritativos. Se recomienda utilizarlo cuando se necesita un análisis más profundo de la resolución de nombres.
- `mtr`: Es útil para diagnosticar problemas de conectividad y latencia en la red. Se recomienda utilizarlo cuando se sospecha de problemas en la ruta de los paquetes de datos.
- `nslookup`: Es útil para obtener información básica sobre un nombre de dominio o dirección IP. Se recomienda utilizarlo cuando se necesita una consulta rápida y sencilla sobre la resolución de nombres.

## Consultas
Se prevee que se va a utilizar completamente DoH en los siguientes años?

Cómo se pueden interceptar comunicaciones NFC?