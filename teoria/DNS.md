# Domain Name System (DNS)

## Introducción
El Sistema de Nombres de Dominio (DNS) es un sistema jerárquico y descentralizado que traduce nombres de dominio legibles por humanos (como www.ejemplo.com) en direcciones IP numéricas (como 192.168.1.34). En el cual NO existen prioridades de resolución, es decir, no hay un servidor que tenga prioridad sobre otro.

## Por qué se optó por un sistema distribuido
Un Sistema de Nombres de Dominio distribuido permite que la carga de trabajo se reparta entre múltiples servidores, lo que mejora la eficiencia y la disponibilidad del servicio. Además, un sistema distribuido es más resistente a fallos y ataques, ya que no depende de un único punto de fallo. A diferencia de un sistema centralizado, donde un fallo en el servidor principal podría afectar a todos los usuarios, un sistema distribuido permite que otros servidores continúen operando incluso si uno falla.

## Funcionamiento del DNS
El DNS funciona mediante una serie de consultas y respuestas entre clientes y servidores. Cuando un usuario ingresa un nombre de dominio en su navegador, el cliente DNS envía una consulta a un servidor DNS para obtener la dirección IP correspondiente. Si el servidor no tiene la información, puede reenviar la consulta a otros servidores DNS hasta que se encuentre la dirección IP correcta. Una vez que se obtiene la dirección IP, el cliente puede establecer una conexión con el servidor web correspondiente.
- Se le agrega a los navegadores el protocolo DNS para que puedan resolver consultas de nombres de dominio de forma automática al consultar un sitio web.
- Soporta múltiples mensajes de consulta y respuesta, que al correr sobre UDP, se utiliza un Transaction ID para identificar la consulta y la respuesta correspondiente. Esto permite que el cliente pueda enviar múltiples consultas al mismo tiempo y recibir las respuestas de manera ordenada.

### FQDN (Fully Qualified Domain Name)
Un nombre de dominio completamente calificado (FQDN) es un nombre de dominio que especifica su ubicación exacta en la jerarquía del DNS, incluyendo todos los niveles de dominio y el dominio raíz. Un FQDN consta de varios componentes separados por puntos, comenzando con el nombre del host y terminando con el dominio raíz. Por ejemplo, en el FQDN "www.ejemplo.com.", "www" es el nombre del host, "ejemplo" es el dominio de segundo nivel, "com" es el dominio de primer nivel (TLD) y el punto final indica el dominio raíz. Los FQDN son importantes porque proporcionan una forma única de identificar un recurso en Internet y permiten que los servidores DNS resuelvan correctamente las consultas de nombres de dominio.

## Tipos de servidores DNS

### Root Servers
Son actualmente 13 servidores raíz que forman la base de la jerarquía del DNS. Estos servidores son responsables críticos de mantener la información sobre los TLD y dirigir las consultas a los servidores autoritativos correspondientes. Los root servers son operados por diferentes organizaciones en todo el mundo y están distribuidos geográficamente para garantizar la disponibilidad y la redundancia del servicio. Se denominan con letras de la A a la M, y cada uno tiene múltiples instancias distribuidas en diferentes ubicaciones para mejorar la resiliencia y el rendimiento del sistema DNS.

### Top Level Domain (TLD)
Los TLD son los dominios de nivel superior que se encuentran en la parte final de un nombre de dominio, como .com, .org, .net, .edu, entre otros. Estos dominios son administrados por organizaciones específicas y son responsables de mantener la información de los nombres de dominio registrados bajo su TLD.
Para ver la lista completa de TLDs se puede consultar el sitio web de la IANA (Internet Assigned Numbers Authority) en https://www.iana.org/domains/root/db.
Cada TLD tiene un conjunto de servidores autoritativos que son responsables de mantener la información de los nombres de dominio registrados bajo ese TLD. Cuando un resolver necesita obtener la dirección IP de un nombre de dominio, primero consulta los servidores autoritativos del TLD correspondiente para obtener la información necesaria.

### Resolvers
Es el servidor que el navegador y/o el cliente tienen configurados para resolver nombres de dominio. Los resolvers pueden ser públicos (como los de Google o Cloudflare) o privados (como los proporcionados por un proveedor de servicios de Internet). Su función principal es recibir las consultas de los clientes y buscar la información necesaria en la jerarquía del DNS para devolver la dirección IP correspondiente.

Estos tienen caché para almacenar temporalmente las respuestas a consultas recientes, lo que permite acelerar el proceso de resolución de nombres de dominio y reducir la carga en los servidores autoritativos.

Todo resolver tiene un tiempo de vida (TTL) para cada registro que almacena en caché, lo que indica cuánto tiempo puede mantener la información antes de considerarla obsoleta y volver a consultar a los servidores autoritativos.

Es un término sobreutilizado ya que están tanto en los clientes como en los servidores, y se les llama resolvers a ambos. Inclusive las aplicaciones encargadas de resolver nombres de dominio, como los navegadores web, también pueden considerarse resolvers.

### Servidores autoritativos 
Son servidores encargados de mantener una sola sección del espacio de dominios, y son responsables de responder a las consultas de los resolvers sobre los nombres de dominio que están bajo su autoridad. Estos servidores contienen registros DNS que asocian nombres de dominio con direcciones IP y otros datos relevantes. 
- Dejan un flag `aa` en las consultas con el comando dig para indicar que la respuesta proviene de un servidor autoritativo.

#### Servidores primarios y secundarios
Los servidores primarios y secundarios son tipos de servidores autoritativos que trabajan juntos para garantizar la disponibilidad y la redundancia de la información de los nombres de dominio. El servidor primario es el servidor autoritativo principal que mantiene la información original de los nombres de dominio bajo su autoridad. El servidor secundario es una copia de seguridad del servidor primario y se utiliza para garantizar que la información esté disponible incluso si el servidor primario falla o no está disponible. Los servidores secundarios reciben actualizaciones periódicas del servidor primario para mantener la información sincronizada y garantizar que los resolvers puedan obtener la información correcta en todo momento. Estas actualizaciones se realizan mediante un proceso llamado transferencia de zona, que permite a los servidores secundarios obtener la información más reciente del servidor primario, este proceso está integrado en el protocolo DNS y se realiza de manera automática utilizando TCP para garantizar la consistencia de la información.

### Resolvers vs Autoritativos
#### Resolvers
- Realizan caché de consultas recientes para acelerar la resolución de nombres de dominio.
- Pueden ser públicos o privados, dependiendo de la configuración del cliente.
- Su función principal es recibir consultas de los clientes y buscar la información necesaria en la jerarquía del DNS para devolver la dirección IP correspondiente.
- Tienen un tiempo de vida (TTL) para cada registro que almacenan en caché, lo que indica cuánto tiempo pueden mantener la información antes de considerarla obsoleta y volver a consultar a los servidores autoritativos.
- Realizan consultas recursivas, lo que significa que si no tienen la información necesaria, pueden consultar a otros servidores DNS hasta obtener la respuesta correcta.

#### Autoritativos
- No realizan caché de consultas recientes ni consultas recursivas, ya que su función principal es proporcionar información precisa y actualizada sobre los nombres de dominio bajo su autoridad.
- Mantienen registros DNS que asocian nombres de dominio con direcciones IP y otros datos relevantes.
- Son responsables de responder a las consultas de los resolvers sobre los nombres de dominio que están bajo su autoridad.
- Contienen información específica sobre los nombres de dominio registrados bajo su TLD y son responsables de mantener la integridad y precisión de esa información.
- Los servidores raíz son un tipo especial de servidores autoritativos que mantienen información sobre los TLD y dirigen las consultas a los servidores autoritativos correspondientes.

### Fowarder Name Server
Son servidores que actúan como un Proxy entre los resolvers y los servidores autoritativos. Su función principal es recibir consultas de los resolvers y reenviarlas a los servidores autoritativos correspondientes para obtener la información necesaria. Una vez que reciben la respuesta, la devuelven al resolver que realizó la consulta original. Los forwarders pueden ser configurados para filtrar o bloquear ciertas consultas, lo que permite a las organizaciones controlar el acceso a ciertos nombres de dominio o direcciones IP.

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

### CNAME (Canonical Name)
El registro CNAME (Canonical Name) es un tipo de registro DNS que permite asociar un nombre de dominio con otro nombre de dominio canónico. Esto significa que cuando se realiza una consulta para el nombre de dominio asociado al registro CNAME, el servidor DNS devuelve la dirección IP del nombre de dominio canónico en lugar de la dirección IP del nombre de dominio original. Por ejemplo, si se tiene un registro CNAME que asocia "www.example.com" con "example.com", cuando un usuario realiza una consulta para "www.example.com", el servidor DNS devuelve la dirección IP de "example.com". Esto es útil para simplificar la administración de nombres de dominio y permitir que varios nombres de dominio apunten a la misma dirección IP sin tener que crear registros A separados para cada uno.

### PTR (Pointer) / Registros inversos
El registro PTR (Pointer) es un tipo de registro DNS que se utiliza para realizar consultas inversas, es decir, para obtener el nombre de dominio asociado a una dirección IP. A diferencia de los registros A y AAAA, que asocian un nombre de dominio con una dirección IP, los registros PTR permiten realizar la operación inversa, lo que es útil para la verificación de la autenticidad de los correos electrónicos y la resolución de problemas de red. Por ejemplo, si se tiene una dirección IP "192.168.1.1", el registro PTR asociado a esa dirección IP podría apuntar a "host1.example.com". Se utiliza comúnmente en servidores de correo electrónico para verificar que el remitente de un correo electrónico es legítimo y no un spammer.

### Registros MX (Mail Exchange)
Los registros MX (Mail Exchange) son registros DNS que especifican los servidores de correo electrónico que deben recibir los correos electrónicos para un dominio. Estos registros incluyen una prioridad que determina el orden en que los servidores deben ser utilizados para el envío de correos electrónicos. Por ejemplo, si un dominio tiene dos servidores de correo electrónico, se pueden crear registros MX con diferentes prioridades para indicar cuál debe ser utilizado primero.

## Envenenamiento de Caché
El envenenamiento de caché es un ataque en el que un atacante introduce información falsa en la caché de un servidor DNS, lo que provoca que los usuarios sean redirigidos a sitios web maliciosos o fraudulentos. Esto puede ocurrir cuando un servidor DNS almacena información incorrecta sobre un nombre de dominio, lo que hace que los usuarios que consultan ese dominio sean dirigidos a una dirección IP controlada por el atacante. El envenenamiento de caché puede tener consecuencias graves, como el robo de información personal, la propagación de malware y la pérdida de confianza en los servicios en línea. 

## Otras tecnologías relacionadas con DNS

### DHCP (Dynamic Host Configuration Protocol)
El Protocolo de Configuración Dinámica de Host (DHCP) es un protocolo de red que permite a los dispositivos obtener automáticamente una dirección IP y otra información de configuración de red, como la máscara de subred, la puerta de enlace predeterminada y los servidores DNS. Cuando un dispositivo se conecta a una red, envía una solicitud DHCP para obtener una dirección IP disponible. El servidor DHCP responde con una dirección IP y otra información de configuración, lo que permite al dispositivo comunicarse con otros dispositivos en la red y acceder a Internet. 

### DDNS (Dynamic DNS)
El DNS dinámico (DDNS) es un servicio que permite actualizar automáticamente los registros DNS cuando cambia la dirección IP de un dispositivo. Esto es útil para mantener la conectividad y la accesibilidad de los servicios en línea, especialmente cuando se utilizan direcciones IP dinámicas.

### DoH (DNS over HTTPS)
DoH es una técnica que permite realizar consultas DNS a través del protocolo HTTPS, lo que proporciona una capa adicional de seguridad y privacidad. Al utilizar DoH, las consultas DNS se cifran y se envían a través de conexiones HTTPS, lo que dificulta el seguimiento y la manipulación de estas consultas por parte de terceros.

### DoT (DNS over TLS)
DoT es una técnica que permite realizar consultas DNS a través del protocolo TLS (Transport Layer Security), lo que proporciona una capa adicional de seguridad y privacidad. Al utilizar DoT, las consultas DNS se cifran y se envían a través de conexiones TLS, lo que dificulta el seguimiento y la manipulación de estas consultas por parte de terceros.

### DNSSec (DNS Security Extensions)
DNSSec es un conjunto de extensiones al protocolo DNS que proporciona autenticación y integridad a los datos DNS. Esto ayuda a prevenir ataques como el spoofing de registros DNS y la manipulación de información de resolución de nombres.

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

## Entidades dentro del DNS
### ICANN (Internet Corporation for Assigned Names and Numbers)
La ICANN es una organización sin fines de lucro responsable de coordinar y administrar los nombres de dominio y las direcciones IP en Internet. Su objetivo principal es garantizar la estabilidad y seguridad de la infraestructura de Internet, así como promover la competencia y la innovación en el espacio de nombres de dominio. La ICANN trabaja en estrecha colaboración con otras organizaciones y partes interesadas para desarrollar políticas y procedimientos que regulen la asignación y gestión de los nombres de dominio y las direcciones IP.

### IANA (Internet Assigned Numbers Authority)
La IANA es una organización responsable de coordinar y administrar los recursos de numeración de Internet, incluyendo la asignación de direcciones IP, la gestión de los nombres de dominio y la administración de los protocolos de Internet. La IANA es una parte integral de la ICANN (Internet Corporation for Assigned Names and Numbers) y trabaja en estrecha colaboración con otras organizaciones para garantizar la estabilidad y seguridad de la infraestructura de Internet. La IANA también es responsable de mantener la base de datos de los TLD y de coordinar la delegación de la autoridad de los nombres de dominio a los servidores autoritativos correspondientes.

### RIR (Registro de Internet Regional)
Los RIR son organizaciones responsables de la asignación y gestión de direcciones IP y otros recursos de numeración de Internet en regiones geográficas específicas. Existen cinco RIR principales: ARIN (América del Norte), RIPE NCC (Europa, Medio Oriente y partes de Asia Central), APNIC (Asia-Pacífico), LACNIC (América Latina y el Caribe) y AFRINIC (África). Cada RIR trabaja en estrecha colaboración con los proveedores de servicios de Internet, las organizaciones gubernamentales y otras partes interesadas para garantizar la distribución equitativa y eficiente de los recursos de numeración de Internet en su región. Los RIR también participan en la coordinación global de la asignación de direcciones IP y otros recursos de numeración a través de la IANA y la ICANN.

## Consultas
Se prevee que se va a utilizar completamente DoH en los siguientes años?